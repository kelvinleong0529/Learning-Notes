# **Connection**
- to check the connection details between host and docker in JSON format
```
docker inspect {name_of_the_container} "{{json .NetworkSettings.Networks }}"

for eg:
docker inspect postgres "{{json .NetworkSettings.Networks }}"
```