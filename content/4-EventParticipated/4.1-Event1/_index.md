---
title: "Meetup 1"
date: 2026-06-06
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# Meetup Session – June 6, 2026

### Purpose of the Event

- Share THE ART OF EFFECTIVE TEAMWORK
- Share a self-learning journey and roadmap for transitioning into Cloud/DevOps
- Share how to build a GraphRAG application using Amazon Bedrock and Amazon Neptune
- Share how to connect Godot clients with AWS WebSockets
- Share Docker – A containerization technology
- Share about a Machine Learning-based Network Intrusion Detection System (NIDS) on AWS

### List of Speakers

- Nguyen Quoc Bao – Connecting Godot Clients with AWS WebSockets
- Huynh Nguyen Quoc Bao – Docker – A containerization technology
- Le Hoang Gia Dai – Machine Learning-based Network Intrusion Detection System (NIDS) on AWS
- Tran Trung Vinh – A practical career journey from IT Helpdesk to Senior Sysadmin  and the first steps toward Cloud and DevOps.
- Viet Phat – Build GraphRAG applications using Amazon Bedrock and Amazon Neptune
- Truong Huy Phuoc – THE ART OF EFFECTIVE TEAMWORK

### Key Highlights
- Docker – A containerization technology

#### Negative Effects of Legacy Application Architecture

- Copying code from one machine to another → wastes time
- Prone to errors due to missing libraries

#### Transitioning to a New Application Architecture

- **Containerization**: Packaging an application together with all its libraries and runtime environment into a container.
- **Fast Deployment**: Deploying applications quickly, reducing installation and configuration time.
- **Resource Optimization**: Containers use fewer resources than virtual machines because they share the host operating system's kernel.
- **Portability**: Applications can be moved and run across different platforms without changing configuration.

#### Domain-Driven Design (DDD)

- **Business Domain**: Analyzing and understanding the business problem thoroughly before designing the system.
- **Domain Events**: Identifying important events that occur during business process execution.
- **Bounded Context**: Dividing the system into independent functional areas to reduce dependencies between components.
- **Ubiquitous Language**: Building a shared vocabulary between the development team and business stakeholders to minimize misunderstandings of requirements.
- **Event Storming**: A collaborative workshop technique used to identify business processes, events, and their relationships before implementing the system.
- **Context Mapping**: Defining the relationships and communication patterns between Bounded Contexts within the same system.

#### Event-Driven Architecture

- **Event Producer**: The component that generates an event when an action or state change occurs (e.g., an order is created, a user registers).
- **Event Router/Broker**: The intermediary that receives and routes events to the appropriate destination (e.g., Amazon EventBridge, Amazon SNS, Amazon SQS, Kafka).
- **Event Consumer**: The component that listens for and processes events once they are delivered.

#### Compute Evolution

- **Virtualization → Containerization**: A shift from the virtual machine model (each VM has its own OS, heavy and resource-intensive) to containers (sharing a common Host OS, faster startup, and much lighter weight).
- **VM vs Container**: A VM requires a hypervisor and a separate guest OS for each application, taking minutes to boot; a container only needs a container engine, boots in milliseconds, and delivers near-native performance.
- **Deployment Density**: A single physical server can run 10-100 VMs, but can run 100-1000 containers, making resource utilization far more efficient.

#### Amazon Q Developer

- **SDLC automation**: Covers the full lifecycle from planning to maintenance
- **Code transformation**: Java upgrades, .NET modernization
- **AWS Transform agents**: VMware, Mainframe, .NET migration

### Key Takeaways

#### Design Thinking

- **Comparing technologies before choosing one**: Understanding the differences between virtualization and containerization helps make architecture decisions suited to each specific problem, rather than defaulting to VMs for every case.
- **Trade-off between isolation and performance**: VMs offer stronger isolation and security (fully isolated), while containers prioritize speed and deployment density (process-level security) — the right choice depends on the system's security requirements.
- **The "package everything" mindset**: Bundling an application together with its entire runtime environment eliminates the classic problem of "it works on my machine but not on yours."

#### Technical Architecture

- **Container's layered structure**: Kernel → Base Image → intermediate Images (adding packages, libraries) → the writable Container layer on top — understanding this mechanism helps optimize Dockerfiles and image size.
- **Docker Engine sits between the Host OS and applications**: This allows multiple containers to share a single Host OS while still running independently of one another, unlike VMs which each require their own Guest OS.
- **A Dockerfile is the "recipe" for building an image**: Instructions such as FROM, ARG, RUN, WORKDIR, COPY, and CMD/ENTRYPOINT determine how the image is built and how the application is started.

#### Modernization Strategy

- **Containerizing legacy applications**: Repackaging legacy applications into containers makes it easy to move them (portability) across different environments (physical, virtual, cloud) without changing configuration.
- **Optimizing infrastructure costs**: Thanks to their lightweight nature and ability to run multiple applications on a single host, containerization helps reduce infrastructure costs compared to using many separate VMs.
- **No rushing, test incrementally**: It's best to start containerizing small, low-risk services before applying the approach to the entire system.

### Applying This to My Work

- **Containerizing existing services**: Packaging applications currently under development into Docker images to ensure a consistent runtime environment across local, staging, and production.
- **Building a CI/CD pipeline with Docker**: Using Docker images as the standardized deployment unit within the pipeline, reducing errors caused by environment differences.
- **Applying this to a microservices architecture**: Each service runs in its own container, making it easier to scale independently and deploy faster.
- **Experimenting with Docker Compose**: Managing multiple related containers (application + database + cache, etc.) within a single declarative stack, instead of running each container manually.
- **Optimizing Dockerfiles**: Applying knowledge of layer caching to write more efficient Dockerfiles and reduce build time.

### My Experience at the Event

Attending this meetup was a very rewarding experience, especially the session on Docker — a familiar topic presented in an approachable, easy-to-understand, and genuinely funny way.

#### Learning from Highly Skilled Speakers

Speaker Huynh Nguyen Quoc Bao (Junior Cloud Native Developer at Endava Vietnam, Founder of ITea Lab) presented Docker as **"a friendly intro,"** focusing on intuition and real-world examples rather than deep academic theory.

- The way he led from the problems of **virtualization** (heavy VMs, resource-intensive) into the solution of **containerization** made it easy for the audience to understand why Docker emerged and became so widely adopted.

#### Hands-On Technical Experience

- Watching a live Docker demo — from building an image with a Dockerfile to running a container — made the actual workflow much clearer than just reading about it in theory.
- Gained a deeper understanding of the layer caching mechanism: when a line in the Dockerfile changes, only that layer and everything after it gets rebuilt, which helps optimize build time in practice.
- Learned the core Docker CLI commands (image, container lifecycle, network, volume, docker-compose), enough to start experimenting hands-on right after the session.

#### Applying Modern Tools

- Learned firsthand how Docker packages an application together with all its dependencies, effectively solving the "missing library" or "different environment" problems often encountered during teamwork.
- Learned how to decide when to use a container instead of a traditional VM, based on criteria like performance, deployment density, and the level of isolation required.

#### Connecting and Exchanging Ideas

- The session was run in a **"relaxed, fun, and interactive"** style, creating a comfortable atmosphere to ask questions and interact directly with the speaker.
- Had the chance to exchange experiences with other attendees about using Docker in their own personal projects and real-world work.

#### Lessons Learned

- Choosing between a VM and a container isn't about which one is "better overall" — it's about **choosing what fits the problem**: prioritize VMs when security/isolation matters most, and containers when you need lightweight, fast-scaling deployments.
- Docker isn't just a tool for deep DevOps specialists — with a "friendly intro" mindset, anyone can start experimenting and apply it to their daily work.
- Understanding the layering mechanism of Docker images helps in writing more optimized Dockerfiles, saving both build time and image size in practice.

#### Photos from the Event
* Add your photos here

> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
