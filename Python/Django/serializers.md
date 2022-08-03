# **Serializers**
- `serializers` allow complex data such as querysets and model instances to be converted to native Python datatypes that can then be easily rendered into `JSON`,`XML` or other content types
- also provides deserialization, allowing parsed data to be converted back into complex types, after first validating the incoming data
```python
from datetime import datetime

class Comment:
    def __init__(self,email,content,created=None)
    self.email = email
    self.content = content
    self.created = created or datetime.now()

from rest_framework import serializers

class CommentSerializer(serializers.Serializer):
    email = serializers.EmailField()
    content = serializers.CharField(max_length=200)
    created = serializers.DateTimeField()

comment = Comment(email='leila@example.com', content='foo bar')

serializer = CommentSerializer(comment)
serializer.data
# {'email': 'leila@example.com', 'content': 'foo bar', 'created': '2016-01-27T15:17:10.375877'}
```

## **Serializing Objects**
- at this point we have translated the model instance into Python native datatypes, to finalize the serialization process we render the data in `json`
```python
from rest_framework.renderers import JSONRenderer

json = JSONRenderer().render(serializer.data)
json
# b'{"email":"leila@example.com","content":"foo bar","created":"2016-01-27T15:17:10.375877"}'
```
## **Deserializing Objects**
```python
import io
from rest_framework.parsers import JSONParser

stream = io.BytesIO(json)
data = JSONParser().parse(stream)

serializer = CommentSerializer(data=data)
serializer.is_valid()
# True
serializer.validated_data
# {'content': 'foo bar', 'email': 'leila@example.com', 'created': datetime.datetime(2012, 08, 22, 16, 20, 09, 822243)}
```