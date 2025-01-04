# **Overview**
- `CI/CD` is a method to frequently deliver apps to customers by introducing automation into the stages of app development
- main concepts attributed are **continuous integration**, **continuous delivery**, and **continuous deployment**
- successful **Continuous Integration** means new code changes to an app are regularly built, tested and merged to a shared repository, it's a solution to the problem of having too many branches of an app at once that might conflict with each other
- **Continuous Delivery** usually means a developer's changes to an app are automatically bug tested and uploaded to a repository, where they can be deployed to a live production environment by the Ops team, the main purpose of **Continuous Delivery** is to ensure that it takes minimal effort to deploy new code
- **Continuous Deployment** can refer to automatically releasing a developer's changes from the repository to production, where it is usable by customers
- **CI/CD** is just a process, often visualized as a pipeline, that involves adding a high degree of ongoing automation and continuous monitoring to app development

![CI/CD](https://www.redhat.com/cms/managed-files/styles/wysiwyg_full_width/s3/ci-cd-flow-desktop.png?itok=2EX0MpQZ)

# **Continuous Integration**
- in modern application development, the goal is to have multiple developers working simultaneously on different features of the same app
- however, if an organization is set up to merge all branching source code together on 1 day (known as "merge day"), the resulting work can be tedious, manual, and time-intensive
- this problem can be further compounded if each developers has customized their own local IDE, rather than the team agreeing on one cloud-based IDE
- **Continuous Integration** helps developers merge their code changes back to a shared branch, or "trunk" more frequently (sometimes even daily)
- once a developer's changes are merged, those changes are validated by automatically building the application and running different levels of automated testing, typically unit and integration tests, to ensure the changes havent broken the app (testing everything from classes to function to the different modules that comprises the entire app)
- if automated testing discovers a conflict between new and existing code, CI makes it easier to fix those bugs quickly and often

# **Continuous Delivery**
- following the automation of builds and unit and integration testing in CI, continuous delivery automates the release of that validated code to a repository
- In order to have an effective continuous delivery process, it’s important that CI is already built into your development pipeline
- the goal of continuous delivery is to have a codebase that is always ready for deployment to a production environment
- in continuous delivery, every stage—from the merger of code changes to the delivery of production-ready builds—involves test automation and code release automation
- at the end of that process, the operations team is able to deploy an app to production quickly and easily

# **Continuous Deployment**
- final stage of a mature CI/CD pipeline is continuous deployment, as an extension of continuous delivery, which automates the release of a production-ready build to a code repository, continuous deployment automates releasing an app to production. 
- because there is no manual gate at the stage of the pipeline before production, continuous deployment relies heavily on well-designed test automation
- in practice, continuous deployment means that a developer’s change to a cloud application could go live within minutes of writing it (assuming it passes automated testing)
- this makes it much easier to continuously receive and incorporate user feedback. Taken together, all of these connected CI/CD practices make deployment of an application less risky, whereby it’s easier to release changes to apps in small pieces, rather than all at once
- there’s also a lot of upfront investment, though, since automated tests will need to be written to accommodate a variety of testing and release stages in the CI/CD pipeline