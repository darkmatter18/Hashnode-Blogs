---
title: "Developing a DevOps Mindset: Building the Thinking for Success"
datePublished: Tue Apr 04 2023 16:21:01 GMT+0000 (Coordinated Universal Time)
cuid: clg2gvywb000e09mm5gg64788
slug: developing-devops-mindset
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678377415753/5e46d65b-2382-44ea-8499-883aac0ed4ec.png
tags: tdd, devops, agile, mvp

---

# Introduction

This is the continuation and 2nd story of the Series, **DevOps.** In the [previous story](https://blog.arkadip.dev/what-is-devops), we discussed DevOps, its brief history, definition, and culture.

In this story, we'll focus on the culture part of DevOps and develop the mindset required to adopt DevOps as a team.

# Social Coding

In the past, developers worked in *private* repositories (repos) and you had to be a member of the team to contribute. Access control lists controlled everything and a strict "*need to know*" basis. The problem with that is no one knows that you're working on it, so there is no possibility of reusing code because no one even knows it exists.

With social coding, repositories are public, and everyone is encouraged to fork the code and contribute. You would think that anarchy would ensue, but actually, it works pretty well because the repository owner controls it.

**This is how open-source works and how companies should treat their inner source.**

## Pair Programming

Pair programming is an aspect of social coding that is taken from [Extreme Programming](https://www.agilealliance.org/glossary/xp). It consists of two programmers sharing a single workstation (one screen, one keyboard, and a mouse between the pair).

* The programmer at the keyboard is usually called the “**driver"**.
    
* The other programmer, also actively involved in the programming task, but focused more on the overall direction, is called the “**navigator"**.
    

![Driver and Navigator (Pair Programming)](https://cdn.hashnode.com/res/hashnode/image/upload/v1678694002280/a35f507b-3957-4671-878a-f8e8e66cc52e.png align="center")

While the driver is typing, the navigator is checking their work, or perhaps looking something up, or thinking about what's coming next. Then, after about 20 minutes they swap roles.

You might think that pair programming is using twice the resources to get the same amount of work, but it’s not like that.

### Benefits

![Benefits of Pair Programming](https://cdn.hashnode.com/res/hashnode/image/upload/v1678694718177/d92e3d65-353e-4554-95e7-739168cb7d38.jpeg align="center")

There are many benefits of pair programming.

1. The first benefit is higher code quality. That's a good thing because it lowers the maintenance costs right down the line.
    
2. It also forces skills transfer, creating better programmers, like pairing junior programmer developers with senior developers. So that each one learns from the other’s approach to a problem and picks up tips and tricks that the other one uses.
    
3. If one programmer goes on vacation, and someone knows how to fix their code.
    

## Working in small batches

Working in small batches is a concept from Lean Manufacturing. It is important in situations where fast feedback is required because it enables you to learn quickly from your decisions. Working in small batches allows you to experiment more and quickly gain insights. In contrast, working in large batches that take months to complete means that you don't get feedback for months.

Working in small batches also minimizes waste. Because you gain feedback faster and you don't waste time developing things your customer doesn't like. Using large batches, you may spend months developing something that isn't what the customer wants.

In keeping with DevOps practices of cross-functional teams and lightweight approaches, the best way to rapidly progress from development through test and operations into production in minutes is by working in small batches. Working in small batches helps you implement other DevOps practices like Continuous Integration and Continuous Delivery.

### How to identify a small batch?

You can ask yourself these questions to see if you are working in a small batch or not

* Are your application features decomposed in such a way as to support frequent releases? If not, then you are working in a large batch.
    
* Are there delays in the release because the features are too large? If Yes, then you are working in a large batch.
    
* Can features be completed in a sprint? If not, then your batches are too large.
    

Optimally a feature should be small enough to be completed in a week or less. The features you build are **one step toward a goal**. Many people feel that only a completed goal is worth shipping. Instead of thinking of useful subsets that can be delivered in increments to gain feedback toward the ultimate goal.

## Minimum Viable Product (MVP)

A **minimum viable product** is a minimal thing that you can do to test a value hypothesis and gain learning and understanding.

MVP is not the same as phase one of the project, the first beta, the first delivery, or something like that.

It is all about learning. The main goal here is to get feedback and then maybe make the next MVP even better. So, it's essential that at the end of each MVP, you decide whether to **pivot** (do something different) or **persevere** (continue doing what you're doing).

A minimal viable product is a tool for learning. It is an experiment to explore the value proposition with your customer. This experiment may fail and that's okay because failure leads to understanding. What did you learn from that failure? Its purpose is to gain knowledge and understanding about what you are building. This is why we use MVPs in DevOps.

# Test Driven Development

> If it's worth building, it's worth testing.
> 
> If it's not worth testing, why are you wasting your time working on it?
> 
> \-Scott Ambler

Test-Driven Development (TDD) means that your test case drives the design and development of your code. You don't write code and then test it. You write the test cases first. You write the tests for the code you wish you had, then you write the code to make them pass.

Wait!! How can you write a design for code you haven't written yet? You describe in the design how the code should behave and then you write the code that behaves that way. TDD is no different. The test case describes the behavior that you want the code to have.

### Importance of TDD

1. TDD keeps you focused on the purpose of the code, that is, what's it supposed to do. You should be able to specify that before you start writing any code.
    
2. TDD always verifies your Code. If you are working on a repo make sure to run the test cases before doing the coding work so that you can see if you broke the code or if it was already broken.
    
3. TDD gives you the caller’s perspective. So if you are writing an API, how do you know if the request and response format is complying with the caller? Well, write a test case with the request and response formats in it. It allows you to explore how you would want to call the code before even writing it.
    
4. TDD helps you to check your dependencies or libraries. Suppose, someone will say something like, “We have a vulnerability in the Apache Struts library. Can we update it on our servers?” Unless you have test cases that test your code and make sure that it works with a new version of that library, you probably shouldn't do that.
    
5. TDD saves a lot of time. The time you spend writing a few test cases now is going to save you hours and hours of debugging later. You don't know who's going to use your code in the future and you want to make sure your code is solid. TDD will keep you writing solid code.
    

### TDD Workflow

Let's discuss the general workflow of TDD.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680242105756/b38d65d0-8c84-4adb-aca0-e7fc481f5776.png align="center")

1. Write a test Case. the test case will fail because you aren't written any code for that. \[<mark>RED</mark>\]
    
2. Now write just enough code to make the test case pass. It doesn’t have to be perfect. It doesn't have to be pretty. It does have to make the test pass. \[<mark>GREEN</mark>\]
    
3. \[<mark>REFACTOR</mark>\] the code to make it better and increase the quality.
    
4. Finally, repeat the process. This is known as Red, Green, and Refactor.
    

# Behavior Driven Development

Behavior driven development (BDD), as its name implies, focuses on the behavior of the system as observed from the outside in.

This is different from test driven development, which focuses on the minutia of how the system works inside. BDD is great for integration testing to see if all of the components are behaving together.

One of the advantages of BDD is that it describes behaviors in a single notation, which is directly accessible to domain experts, testers, developers, and customers. This improves communications across the team.

### BDD v/s TDD

If we compare BDD to TDD we see that they are coming from opposite directions.

* BDD describes the behavior of the system from the outside in. It is looking at the system as a consumer of it would. BDD is ensuring that you are building the right thing.
    
* TDD tests the functions of the system from the inside out. TDD is ensuring that you are building the thing right. Does each feature perform the task that it was intended to? It is making sure that each component is working correctly while BDD is making sure that they all work together at a higher level.
    

### BDD Workflow

1. The workflow starts with the developers, testers, and customers exploring the problem's domain and collaborating to produce concrete examples that describe the behavior they want.
    
2. They document these behaviors using a language known as Gherkin. It is a natural language representation.
    
3. Next, the team uses a BDD tool like Behave for Python, jBehave for Java, or Cucumber for Ruby, to run these examples as automated acceptance tests.
    
4. As the team works on the solution, the BDD tool tells them which examples are implemented and working and warns them about the ones that aren’t.
    

### Benefits of BDD

1. BDD improves communication among the team members like developers, testers, product owners, and other stakeholders.
    
2. It leads to more precise guidance on how the system should behave.
    
3. The BDD tools can automatically generate technical and end-user documentation from the BDD feature specification.
    
4. Having clear behavior visibility results in higher-quality code, which reduces the cost of maintenance and eliminates the risk.
    

## Gherkin

* Gherkin is an easy-to-read natural language syntax.
    
* It is used in Behavior Driven Development.
    
* It uses a familiar ***Given... When... Then...*** syntax.
    
* *Gherkin is easily understandable by both technical and non-technical people.*
    

If you're wondering where the name Gherkin came from, the original tool that used this syntax was called Cucumber, and Gherkin is a pickle and pickles are made from cucumbers.

### Gherkin Syntax

In Gherkin, you have feature files or feature documents and you will have one feature per document and many scenarios describing a feature.

#### Each feature will have the following keywords:

1. #### **Given**
    
    This is setting up the context or the precondition that sets the stage for the test. The purpose is to put the system in a known state before the user (or external system) starts interacting with it.
    
2. **When**
    
    This is the principal action or actions that describe what is being performed.
    
    This is what takes you from the initial state to the new observed state.
    
3. **Then**
    
    Then is used to observe the outcomes.
    
    The observations should be related to the business value or the benefit of the feature.
    
4. **And**
    
    And is used for continuations.
    
    It gives you a natural way of adding more context, events, or outcomes.
    

### Gherkin Example

Let's look at an example from a retail store.

In this example, there is only one scenario, but there could be certainly more to cover all of the permutations.

This feature in this example is called **“Returns go to stock.”** This feature is described by the behavior of the system when a customer returns an item that they have purchased.

The following can be a simple Gherkin Story to describe the feature:

```plaintext
Given that a customer previously bought a black sweater from me,
And I have 3 black sweaters in stock, 

When they return the black sweater for a refund,

Then I should have 4 black sweaters in stock.
```

This is written by the product owners or other stakeholders and will be used by the developers to build the **“Returns go to stock.”** feature and test it using the syntax.

The point is stakeholders are helping you define the behavior of the system in a formal syntax that you can now execute test cases against.

BDD tools like **Behave** and **Cucumber** can consume this document with no further editing or manipulation and execute test cases to prove that the system does indeed exhibit the behavior.

---

# **Epilogue**

In this story, we understand how to develop a DevOps Mindset, and the benefits of Social Coding. We also got an idea that what is a Minimum Viable Product (MVP). Lastly we understand 2 important concepts, Test Driven Development(TDD), Behavior Driven Development(BDD) along with Gherkin.

If you think that I missed anything, and if you have any ideas or comments, let me know.

Thanks for giving me your valuable time and thanks for reading. I'll see you in the next story.