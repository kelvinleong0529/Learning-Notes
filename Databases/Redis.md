# **what is Redis**
- Redis stores data in the form of key-value pair, it's not good in storing sturctured data like in SQL
- Redis does not run on the disk or stores the information on disk, instead it runs on the working memory, the RAM of our computer. means it's incredibily **FAST**, but it also means **HIGH VOLATILITY** becuase if system crashes we will lose all the info unless we backed them up
- Mostly used for **CACHING**, things that we access a lot, or those that need alot of time to compute
- Redis is to be built on top of a traditional database, sitting in front of **MONGODB**, **POSTGRESQL**, if we have data that need to queried frqeuently, can stored the data in **REDIS** (both in the traditional databases as well)

# **Commands**
## **Basic**
1. SET name kelvin: create a key-value pair with "name" as the key and "kelvin" as the value
2. GET name: returns the value of the key "name"
3. EXISTS name: check if the key "name" exists
4. KEYS *: get all the keys
5. SETEX name 10 kelvin: create the key-value pair that lasts for 10 seconds (SET EXPIRE)
- **GET** only work for strings

## **Array**
1. LPUSH friends kelvin: "L" stands for **left**-push, push the value "kelvin" into the **beginning** of an array called "friends"
2. LRANGE friends 0 -1: get the elements in the array "friends" starting from index 0:-1 (means all the elements)
3. RPUSH friends sally: "R" stands for **right**-push, push the value "kelvin" into the **end** of an array called "friends"
4. LPOP friends: pop / remove the **left**-most element in the "friends" array
5. RPOP friends: pop / remove the **right**-most element in the "friends" array
```
LPUSH friends kelvin
LPUSH friens john
RPUSH sally
LRANGE friends 0 -1
-----------
1)"john"
2)"kelvin"
3)"sally"
-----------
LPOP friends
-----------
"john"
-----------
RPOP friends
-----------
"sally"
-----------
```

## **Sets**
1. SADD hobbies "weight lifting": add the value "weight lifting" into a set called "hobbies"
2. SREM hobbies "weight lifiting": remove the value "weight lifting" from a set called "hobbies"
3. SMEMBERS hobbies: return all the elements in the set called "hobbies"

## **Hashes**
1. HSET person name kelvin: add the key-value pair of "name":"kelvin" into a has object called person
2. HGETALL person: get all the key-value pairs in the hash object called "person"
3. HGET person name: get the value of the "name" key in the hash object called "person"
4. HDEL person age: delete the prpoperty of age in the hash object "person"
5. HEXISTS person name: check if the "name" property exists in the hash object called "person"
```
HSET person name kelvin
HSET person age 25
HGET person name
-----------
"25"
-----------
HGETALL person
-----------
1)"name"
2)"kelvin"
3)"age"
4)"25"
-----------
HDEL person name
HGETALL person
-----------
1)"age"
2)"25"
-----------
```