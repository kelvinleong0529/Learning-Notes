# **GORM**

- `Object Relational Mapping (ORM)` makes it easier to write code
- consider the folloing scenario: we have a database on which we need to perform CRUD operations, since `Go` emphasizes simplicity, it seems sensible that we would use a database's native language, such as SQL, PostGRE etc, to interface with it
- `ORMs` assist us in writing quick SQL queries in the language we are most familiar with, as well as developing a SQL wrapper for the language

# **Model**
- models are normal structs with basic Go types
- `GORM` prefers convention over configuration, by default it uses `ID` as primary key, pluralizes struct name to `snake_case`, and uses `CreatedAt` & `UpdatedAt` to track creating / updating time
## **gorm.Model**
```golang
// gorm.Model definition
type Model struct {
  ID        uint           `gorm:"primaryKey"`
  CreatedAt time.Time
  UpdatedAt time.Time
  DeletedAt gorm.DeletedAt `gorm:"index"`
}
```

## **Field-Level Permission**
- exported fields have all permission when doing CRUD with `GORM`, and `GORM` allows us to change the filed-level permission with tag, so we can make a field to be read-only, write-only, create-only, update-only or ignored
```golang
type User struct {
  Name string `gorm:"<-:create"` // allow read and create
  Name string `gorm:"<-:update"` // allow read and update
  Name string `gorm:"<-"`        // allow read and write (create and update)
  Name string `gorm:"<-:false"`  // allow read, disable write permission
  Name string `gorm:"->"`        // readonly (disable write permission unless it configured)
  Name string `gorm:"->;<-:create"` // allow read and create
  Name string `gorm:"->:false;<-:create"` // createonly (disabled read from db)
  Name string `gorm:"-"`            // ignore this field when write and read with struct
  Name string `gorm:"-:all"`        // ignore this field when write, read and migrate with struct
  Name string `gorm:"-:migration"`  // ignore this field when migrate with struct
}
```

## **declaring models**
```golang
type User struct {
  gorm.Model
  Name string
}
// equals
type User struct {
  ID        uint           `gorm:"primaryKey"`
  CreatedAt time.Time
  UpdatedAt time.Time
  DeletedAt gorm.DeletedAt `gorm:"index"`
  Name string
}
```
```golang
type Author struct {
  Name  string
  Email string
}

type Blog struct {
  ID      int
  Author  Author `gorm:"embedded"`
  Upvotes int32
}
// equals
type Blog struct {
  ID    int64
  Name  string
  Email string
  Upvotes  int32
}
```
- we can use tag `embeddedPrefix` to add prefix to embedded fields' db name, for example:
```golang
type Blog struct {
  ID      int
  Author  Author `gorm:"embedded;embeddedPrefix:author_"`
  Upvotes int32
}
// equals
type Blog struct {
  ID          int64
  AuthorName  string
  AuthorEmail string
  Upvotes     int32
}
```

# **Create**
## **Create Record**
```golang
user := User{Name: "Jinzhu", Age: 18, Birthday: time.Now()}

result := db.Create(&user) // pass pointer of data to Create

user.ID             // returns inserted data's primary key
result.Error        // returns error
result.RowsAffected // returns inserted records count
```
## **Create record with selected fields**
```golang
db.Select("Name", "Age", "CreatedAt").Create(&user)
// INSERT INTO `users` (`name`,`age`,`created_at`) VALUES ("jinzhu", 18, "2020-07-04 11:05:21.775")

db.Omit("Name", "Age", "CreatedAt").Create(&user)
// INSERT INTO `users` (`birthday`,`updated_at`) VALUES ("2020-01-01 00:00:00.000", "2020-07-04 11:05:21.775")
```
## **Batch insert**
- to efficiently insert large number of records, pass a slice to `Create` method, `GORM` will generate a single SQL statement to insert all the data and backfill primary key values, hook methods will be invoked too
```golang
var users = []User{{Name: "jinzhu1"}, {Name: "jinzhu2"}, {Name: "jinzhu3"}}
db.Create(&users)

for _, user := range users {
  user.ID // 1,2,3
}
```
- we can also specify the baych size when creating with `CreateInBacthes`, eg:
```golang
var users = []User{{Name: "jinzhu_1"}, ...., {Name: "jinzhu_10000"}}

// batch size 100
db.CreateInBatches(users, 100)
```
## **Create from map**
- `GORM` supports create from `map[string]interface{}` and `[]map[string]interface{}{}`
```golang
db.Model(&User{}).Create(map[string]interface{}{
  "Name": "jinzhu", "Age": 18,
})

// batch insert from `[]map[string]interface{}{}`
db.Model(&User{}).Create([]map[string]interface{}{
  {"Name": "jinzhu_1", "Age": 18},
  {"Name": "jinzhu_2", "Age": 20},
})
```

# **Query**
## **Retrieving a single object**
- `GORM` provides `First`, `Take`, `Last` methods to retrieve a single object from the database, it adds `LIMIT 1` condition when querying the database, and it will return the error `ErrRecordNotFound` if no record is found
```golang
// Get the first record ordered by primary key
db.First(&user)
// SELECT * FROM users ORDER BY id LIMIT 1;

// Get one record, no specified order
db.Take(&user)
// SELECT * FROM users LIMIT 1;

// Get last record, ordered by primary key desc
db.Last(&user)
// SELECT * FROM users ORDER BY id DESC LIMIT 1;

result := db.First(&user)
result.RowsAffected // returns count of records found
result.Error        // returns error or nil

// check error ErrRecordNotFound
errors.Is(result.Error, gorm.ErrRecordNotFound)
```
- the `First` and `Last` methods will find the first and last records (respectively) as ordered by primary key
- they only work when a pointer to the destination struct is passed to the methods as argument or when the model is specified using `db.Model()`
- additionally, if no primary key is defined for relevant model, then the model will be ordered by the first field
```golang
var user User
var users []User

// works because destination struct is passed in
db.First(&user)
// SELECT * FROM `users` ORDER BY `users`.`id` LIMIT 1

// works because model is specified using `db.Model()`
result := map[string]interface{}{}
db.Model(&User{}).First(&result)
// SELECT * FROM `users` ORDER BY `users`.`id` LIMIT 1

// doesn't work
result := map[string]interface{}{}
db.Table("users").First(&result)

// works with Take
result := map[string]interface{}{}
db.Table("users").Take(&result)

// no primary key defined, results will be ordered by first field (i.e., `Code`)
type Language struct {
  Code string
  Name string
}
db.First(&Language{})
// SELECT * FROM `languages` ORDER BY `languages`.`code` LIMIT 1
```

# **Associations**

## **Belongs To**
- `belongs to` sets up a one-to-one connection with another model, such that each instance of the declaring model "belongs to" one instance of the other model
```golang
type User struct {
  gorm.Model
  Name      string
  CompanyID int
  Company   Company
}

type Company struct {
  ID   int
  Name string
}
```
- in the example above, each user can be assigned to exactly one company
- inside the `user` object, there is both a `CompanyID` as well as a `Company`, the `CompangID` is implicitly used to create a foreign key relationship between the `User` and `Company` tables, and thus must be included in the `User` struct in order to fill the `Company` inner struct

```golang
// override foreign key
type User struct {
  gorm.Model
  Name         string
  CompanyRefer int
  Company      Company `gorm:"foreignKey:CompanyRefer"`
  // use User.CompanyRefer as foreign key
}

type Company struct {
  ID   int
  Name string
}
```

```golang
// override references
type User struct {
  gorm.Model
  Name      string
  CompanyID string
  Company   Company `gorm:"references:Code"` // use Company.Code as references
}

type Company struct {
  ID   int
  Code string
  Name string
}
```