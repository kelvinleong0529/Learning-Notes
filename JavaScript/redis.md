# **Redis**

```javascript
import redis from "JavaScript/redis"
import express from "express"

const redisClient = redis.createClient();
const app = express()

const DEFAULT_EXPIRATION = 3600

app.get("/photos", async (req, res) => {

    const albumId = req.query.albumId
    // try to query the "value" for "photos" with ${albumId} in redis
    redisClient.get(`photos?albumId=${albumId}`, async (error, data) => {
        if (error) console.log(error)
        if (data != null) {
            // REDIS return the result as string, we need to PARSE it as JSON
            return res.json(JSON.parse(data))
        }
        // redis query failed, value for "photos" doesnt exist
        else {
            const data = await
        ...  // query data from somewhere else
            // "redisClient.setex" sets an expiration time
            // the 1st param is the key value that will apply all the config
            redisClient.setex(`photos?albumId=${albumId}`, DEFAULT_EXPIRATION, JSON.stringify(data))
            return res.json(data)
        }
    })
})

```