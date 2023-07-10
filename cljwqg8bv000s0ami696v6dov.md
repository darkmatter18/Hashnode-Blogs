---
title: "5 injection vulnerabilities hackers don't want developers to know about (and how to prevent them)"
datePublished: Mon Jul 10 2023 10:40:55 GMT+0000 (Coordinated Universal Time)
cuid: cljwqg8bv000s0ami696v6dov
slug: 5-injection-vulnerabilities-hackers-dont-want-developers-to-know-about-and-how-to-prevent-them
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/SYofhg_IX3A/upload/88b042b86a8af45259a61ad4ed1877d4.jpeg
tags: sql, vulnerability, cybersecurity-1

---

There are specific topics in security (e.g., cryptography) that only security-focused engineers typically need to worry about. However, there are a few topics that ***every*** developer should understand because it’s so easy to introduce vulnerabilities into web applications otherwise. Injection vulnerabilities fall into this category.

The most widely-known forms of injection vulnerabilities are [SQL injection](https://owasp.org/www-community/attacks/SQL_Injection) (SQLi) and [cross-site scripting](https://owasp.org/www-community/attacks/xss/) (XSS), but the same pattern shows up in a variety of places you might not think of. I'll cover the general practice first, and then go over a few specific types of injection vulnerabilities and how to avoid them.

## What is an injection vulnerability?

An injection vulnerability arises whenever untrusted input can alter the **semantics** of an operation. Untrusted input means any input an attacker might be able to control. This includes anything in an incoming HTTP request (URL, headers, body), responses from third-party APIs, and previously stored untrusted inputs (e.g., user data read from a DB), among others. **If you're not sure whether to trust some data, it's best to assume it's untrusted.**

> Parsers and untrusted inputs should never meet.

Example parsers are:

* browser rendering raw HTML
    
* SQL database parsing a query
    
* REST API handler routing a request based on path, query params, or body
    
* Shell (e.g., Bash) interpreting a command string
    
* OS resolving a file path to a specific file on disk (e.g., interpreting slashes and \`..\` to have specific meanings within a path string)
    

The best protection against injection vulnerabilities is for the semantics of an operation to be determined before untrusted input ever enters the picture. For SQL injection, this means using prepared statements or an ORM to define queries. For XSS, this means inserting untrusted input into the client-side DOM only as specific element text properties (or using frameworks like React that do this for you unless it's explicitly disabled via [***dangerouslySetInnerHTML***](https://react.dev/reference/react-dom/components/common#dangerously-setting-the-inner-html)).

In cases where it's not possible to statically define an operation without the untrusted input (e.g. when returning rendered HTML from the server), the untrusted input must first be **sanitized**. The rules for sanitizing an input (i.e., which characters need to be escaped and how they should be escaped) depend on where that input will be used. It's notoriously difficult to write effective sanitizers, and ***it's best to assume that a skilled attacker is better at circumventing your sanitizer than you are at thinking of every possible edge case***.

> OWASP maintains a lengthy [***XSS Filter Evasion Cheat Sheet***](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html) just to give you an idea of the difficulty involved in writing a sanitizer.

## Input Sanitization

1. Try very hard to avoid the need for a sanitizer by keeping untrusted input away from parsers. It's worth investing resources to do this whenever possible.
    
2. Use a mature, widely distributed, and thoroughly tested sanitizer when (1) isn't possible. **Writing your own sanitizer is asking for trouble.**
    
3. Structure your code such that sanitization happens in as few places as possible, and write tests to make sure problematic inputs are sanitized as expected. **If every line in your codebase that does a SQL query or other sensitive operation has to call a sanitization function, someone will eventually forget to do that**!
    

## Injection Methods

### SQL Injection (SQLi)

[SQL injection](https://owasp.org/www-community/attacks/SQL_Injection) vulnerabilities happen whenever untrusted input is inserted into a query without proper sanitization. A popular example is xkcd's [Little Bobby Tables](https://xkcd.com/327/). Consider the query:

```javascript
db.query(`SELECT * from students WHERE first_name = '${request.first_name}'`)
```

When the code above interpolates Little Bobby Tables's first name `Robert'; DROP TABLE Students;--` into the query, the query becomes:

```sql
SELECT * from students WHERE first_name = 'Robert'; DROP TABLE Students;--'
```

SQL treats `--` and anything after it as a comment, so this is a valid SQL query. However, the query will now drop the entire table!

To avoid SQLi, use [prepared statements](https://dev.mysql.com/doc/refman/8.0/en/sql-prepared-statements.html) such as:

```sql
SELECT * from students WHERE first_name = ?
```

With a prepared statement, the SQL DB engine parses the query before user input is ever passed to it. When the prepared query is executed with specific parameters, those parameters have no way to alter the semantics of the query, avoiding an injection vulnerability.

A typical [ORM](https://en.wikipedia.org/wiki/Object%E2%80%93relational_mapping) similarly separates input values from query semantics and usually avoids injection issues.

### Cross-site Scripting (XSS)

[XSS](https://owasp.org/www-community/attacks/xss/) is a complex topic I'll only touch on briefly here. Like other injection vulnerabilities, XSS arises when untrusted input can be injected (into HTML, in this case) prior to parsing/rendering. The untrusted input can come from server request parameters such as the query string (reflected XSS), previously-stored values (stored/persistent XSS), or manifest entirely within the client ([DOM-based XSS](https://owasp.org/www-community/attacks/DOM_Based_XSS)).

XSS is effectively a client-side remote code execution (RCE) vulnerability in which an attacker can insert their own JavaScript into a page. That JavaScript can access anything within the page's [origin](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy), including cookies and local storage that may include sensitive secrets such as session tokens. The attacker's code can also make HTTP API requests from the page, which will include even [***HttpOnly*** cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies). Essentially, the attacker can do anything the page can do.

The most robust protection against XSS is to use a client-side framework like [React](https://react.dev/) that lets you intuitively render untrusted inputs on a page without risking XSS. Be sure to avoid using [dangerouslySetInnerHTML](https://react.dev/reference/react-dom/components/common#dangerously-setting-the-inner-html), which bypasses XSS protections.

Sanitization is particularly difficult for protecting against XSS since the sanitization rules are *context-dependent* (i.e., the rules for escaping untrusted inputs in a `<div>` body, `input.value` property, or `<style>` body are all different). If you need to insert untrusted input into raw HTML, use a well-tested sanitizer such as [DOMPurify](https://github.com/cure53/DOMPurify).

Setting a strong [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) without `unsafe-inline` or `unsafe-eval` in the `script-src` or `default-src` directive is an effective [defense-in-depth](https://en.wikipedia.org/wiki/Defense_in_depth_(computing)) measure to prevent modern browsers from executing attacker code even if the attacker is able to insert `<script>` elements into the page.

### HTTP API injection

RESTful APIs, GraphQL, and other HTTP-based APIs are ubiquitous. When a web application makes an API call to another service, injection vulnerabilities are possible when that request includes untrusted input.

Consider a contrived example in which a web app integrates with a payments service that has a REST API endpoint for creating a subscription: `POST /subscriptions/{product_id}?price_usd=<price>` where `price_usd` is optional, and a pre-configured price is used if omitted. If an attacker controls the value of `product_id` and passes a value of `desired_product_id?price_id=0`, the web app would end up making a request to `POST /subscriptions/desired_product_id?price_id=0`, which would allow the attacker to sign up for a free subscription.

In JavaScript, the standard way to sanitize untrusted inputs in URL paths is [**encodeURIComponent**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent), which replaces problematic characters such as `?` and `/` with safe percent-encoded sequences. When inserting untrusted input into URL query parameters, [`new URLSearchParams(queryParams)`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams/URLSearchParams) provides a convenient, safe interface for building a query string from a JavaScript object of key-value pairs.

### Shell injection

Backend APIs sometimes need to execute external commands on the machine where they run. Consider an API that performs [WHOIS](https://en.wikipedia.org/wiki/WHOIS) lookups for a requested domain by executing the `whois` command locally.

Consider the following ***vulnerable*** Node.js code:

```javascript
const whois = child_process.execSync(`whois ${whoisRequest.domain}`);
```

If an attacker can pass the domain `reddit.com && rm -rf /`, the backend will execute the command `whois reddit.com && rm -rf /`. The [`child_process.execSync`](https://nodejs.org/api/child_process.html#child_processexecsynccommand-options) function passes the command string to the shell (`/bin/sh` by default on Linux), which parses `&& rm -rf /` as a subsequent command to wipe the filesystem.

To avoid this issue, ***never pass untrusted input to a shell***. Instead, use an interface such as [`child_process.execFileSync`](https://nodejs.org/api/child_process.html#child_processexecfilesyncfile-args-options) that executes a specific binary (which shouldn't be a shell!) and passes arguments **as an array**:

```javascript
const whois = child_process.execFileSync("whois", [whoisRequest.domain]);
```

Now, even if the user passes a domain `reddit.com && rm -rf /`, that entire string will be passed as the command-line argument to `whois`, which will exit with an error but will not cause any harmful side-effects. Perhaps an even better solution would be to use a library to perform WHOIS queries without needing to execute a separate command.

Astute readers may point out that validating the domain against a regex would also likely prevent shell injection in this case. However, avoiding the possibility of shell injection by using a safe interface that keeps untrusted input away from a shell's command parser is a more robust solution that avoids shell injection in all cases.

### Path traversal

Finally, a path traversal vulnerability arises when an untrusted input is inserted into a filesystem path, which can cause the wrong file to be read or even written. Consider a backend API that reads a file at the path `/teams/${team_id}/${report_name}.csv`. If an attacker controls the value of `report_name` but not `team_id`, they could pass a `report_name` of `../other_team_id/private`. This would cause the file `/teams/team_id/../other_team_id/private.csv` (resolved to `/teams/other_team_id/private.csv`) to be read, leaking data from a different team.

To avoid path traversal vulnerabilities, ***never use untrusted input in file or directory names***. It's safest always to control the names of files and directories, including IDs that you generate and control (e.g., **UUIDs**, **KSUIDs**, etc.). If the name of a file or directory absolutely **must** be derived from untrusted input, consider hashing it (e.g., using SHA-256) or at least encoding it into a format that doesn't include dots or slashes (e.g., [URL-safe base64](https://datatracker.ietf.org/doc/html/rfc4648#section-5)).

​