# **Data Source Name (DSN)**
- `Data Source Name (DSN)` is a data structure that contains the information about a specific database than an `Open Database Connectivity (OCBC)` driver needs in order to connect to it
- included in the `DSN`, which resides either in the `registry` or a separate text file, are the information such as name, directory and driver of the database, and depending on the type of the `DSN`, the ID and password of the user
- developer creates a seperate `DSN` for each database, in order to connect to a database, the developer specifies its `DSN` within a program
- in contrast, a `DSN-less` connection require that all the necessary information to be specified within the program
1. `User DSN`: sometimes also called `machine DSN`, speicified to a particular computer, and store information in the registry
2. `System DSN`: also specified to a particular computer, and store information in the registry
3. `File DSN`: contains the relevant information within a text file with a .DSN file extension, can be shared by users of different computer who have the same drivers installed