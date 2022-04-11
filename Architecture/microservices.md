# **Microservices Architecture**
- a method of developing software systems that tries to focus on building single-function modules with well-defined interfaces and operations
- In microservices application, we build the application as a suite of small services, each running its own process and independently deployable
- These **services** can be written in different programming languages amd ise different data storage techniques
- Microservices are often connected via API, and can leverage many of the same tools and solutions that have grown in RESTFUL and web service ecosystem
## **1. Multiple Components**
- software is broken down into multiple component services so that each services can be deployed, tweaked and then redeployed independently
## **2. Built for business**
- traditional monolithic development approach, different teams each have a specific focus to stay, such as UI, databases, technology layers, server-side logic
- Microservice utilizes cross-functional teams, responsibilities of each team are to make specific products based on one or more individual services communicationg via message bus
- "You build it, you run it"
## **3. Simple Routing**
- microservices are simple: they receive requests, the process them, and generate a response accordingly
- we can say that microservices have smart endpoints that process info and apply logic, and dumb pipes through which the info flows
## **4. Decentralized**
- Microservices involves a variety of technologies and platforms
- Developers strive to produce useful tools that can then be used by others to solve the same problem
- Favors decentralized data management, each service usually manages its unique database
## **5. Failure Resistant**
- Microservice are designed to cope with failure
- neighbouring service can continue to function when one or more services has failed
- **Monitoring microservices** can help prevent the risk of a failure
## **6. Evolutionary**
- microservices architecture is an evolutionary design, and ideal for evolutionary systems where we cant fully anticipate the type of devices that may be accessing our app in future
## **Pros**
- development of systems can be **scalable** and **flexible**
- simpler to deploy, can deploy in literal pieces without affecting other services
- simpler to understand, easier to read and follow code since the function is isolated and less dependent
- high reusability, can be shared accross different use cases and scenarios such as payment or login system can be used multiple times accross the business
- faster defect isolation, when a test fails or services goes down, it will be isolated and woldnt affect other part of the services
- minimize the risk of changing, can avoid the locking in technologies or languages
## **Cons**
- requires dynamic makeover
- expensive remote calls (instead of in-process calls)
- coarser-grained remote APIs
- increase complexity when redistributing responsibilities between components, developer will have to mitigate fault tolerance, network latency, and deal with a variety of message formats as well as load balancing
# **Monolithic Architecture**
- Monolith application is built as a single, autonomous unit, cause changes to the application slow as it affects the entire system
## **Cons**
- modification to a small section of code might require building and deploying an entirely new version of software
- **Scaling** is difficult as scaling means we will need to scale the entire application as well
