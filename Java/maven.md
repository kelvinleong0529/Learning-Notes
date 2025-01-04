# **Project Object Model (POM)**
- the basement of Maven framework
- a type of XML file that contains data from the project and configuration details
- includes project, group ID, POM model version, artifact ID (project ID) and version

# **Maven Repository**
## **Local Repository**
- stored on the developer's machine (default: `~/.m2/repository`)
- acts as a cache for downloaded dependencies from remote or central repositories
- also stores JARs built locally
- Maven first checks local repository for dependencies before attempting to fetch them from remote repositories

## **Central Repository**
- public repository maintained by Maven community (default: `https://repo.maven.apache.org/maven2`)
- provides a vast collection of commonly used libraries and artifacts
- if dependency is not found in local repository, Maven fetches it from central repository

## **Remote Repository**
- can be a private repository hosted on a server accessible over HTTP, HTTPS or FTP
- typically used by organizations to host custom or internal dependencies that are not available in central repository

# **Maven Lifecycles**
- build lifecycle is made up of different phases
- default lifecycle consists of the following phases
1. **validate**: authorise the project's correctness and ensures necessary data are available
2. **compile**: compile the source code of the project
3. **test**: test the compiled source code with the unit testing framework
4. **package**: source code will be packaged as a deliverable
5. **verify**: ensure code's quality with an integration test
6. **install**: installed code in local repository
7. **deploy**: share the code with other developers

# **Maven Project**
- maven project can inherit configurations, dependencies, plugins and properties from a parent project
- this hierarchy allows centralized management of shared configurations, and easier maintenance of multiple related projects

### **Group Id**:
1. a unique identifier for a project or group of related projects, typically following a reverse domain name structure
2. represents the organization or project group the artifact belongs to

### **Artifact Id**:
1. a unique identifier for a specific artifact (project) within a group
2. represents the actual name of the project or library
3. combined with `groupId` to uniquely identify an artifact in a repository
4. typically matches the name of the JAR/WAR produced by the project