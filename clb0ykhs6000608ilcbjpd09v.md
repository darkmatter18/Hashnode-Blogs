# Why you should use Kubernetes for your enterprise software?

# The Story

In the previous story, I discussed why we use `Docker`. We saw that Docker has many features like Environment Abstraction, Network Management, etc. Docker can help us deploy and manage containers anywhere and run them seamlessly.

But, is using Docker solved all our problems? **Noo.., It doesn't.** There are many other features that we need while running enterprise software, like

- Auto-scaling of Deployment depending upon the load.
- Load-balancing between containers.
- Auto healing of errored or stopped containers.
- Ingress Management.
- Secret and Configuration management.
- Monitoring and Application Logging
- And many many more...


![Kubernetes Ice Burg](https://cdn.hashnode.com/res/hashnode/image/upload/v1669640352754/92iCg_cum.png align="center")

# So, what's the solution? 🤔

So, the answer is to put your containers inside Kubernetes. Yes, **Kubernetes** aka **K8S** is a collection of Software or Applications that helps you to run and orchestrate and manage containers in a very easy fashion.

> From Kubernetes Website, "Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available."""

# How does Kubernetes actually help?

In a production enterprise environment, we must have to ensure no downtime in the first place, if one container goes down, a new container must spin-off to rescue the incident. And that's the magic of Kubernetes, it can manage your containers easily and effectively. Kubernetes provides you with a framework to run distributed systems resiliently.

### Let's discuss all the Kubernetes features one-by-one


![featues.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1669648182542/WT7rA81eK.png align="center")

1. **Self-Healing** - Kubernetes can automatically create fresh new containers to maintain the system's durability. If any old container is not responding or is down, Kubernetes can replace them with a new one, so that there is no or minimal downtime in the system. And on top of that, all this is done automatically in the background without any human interaction.

2. **Load Balancing and Service Discovery** - Kubernetes comes with its own DNS and Service Discovery service known as [CoreDNS](https://coredns.io/). It makes it easy for all services inside Kubernetes to talk to them seamlessly. Moreover, it helps to expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.

3. **Auto-Sealing** - Kubernetes `Horizontal Pod Auto-scaler (HPA)` can scale up or down the number of containers of deployment as per many matrics. From the number of requests to the CPU usage, it can use 1,000+ matrics to auto-scale the deployments, so that the deployment stays stable.

4. **Secret and configuration management** -  To protect secrets and other information, Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys in a very secure manner. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.

5. **Automatic bin packing** - You provide Kubernetes with a cluster of nodes that it can use to run containerized deployments and tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources. It'll ensure that all the resources of the underlying node are utilized properly. 

6. **Cloud Native Support** - All cloud providers (GCP, AWS, Azure, etc.) supports Kubernetes natively and most of them manage the cluster for you so that you can only focus on building software. They also provide a list of 100+ plugins that can be used to connect with the other cloud services.

7. **Robust Community** - Kubernetes is backed by [Cloud Native Compute Foundation(CNCF)](https://www.cncf.io/) and it has a very large and stable community base.

8. **Other Features** - There are so many features of Kubernetes that I can't even finish in one story. Other features are **Storage orchestration**, **Automated rollouts and rollbacks**, and many more.

# Conculsion

In the modern era of microservice architecture, the usage of Kubernetes will help you to make the best and most robust software. 

I hope it helps you to clarify many of your doubts. Consider a like ❤ and follow 🙏. Thanks!!