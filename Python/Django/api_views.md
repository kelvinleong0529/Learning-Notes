# **Class-based views**
- `class-based views` extends the `APIView` class, with them we determine how requests will be handled and which policy attributes we're going to use
- for example, let's say we have an `Item` class for our shopping list API:
```python
class Item(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4)
    name = models.CharField(max_length=100)
    done = models.BooleanField()
```

```python
# view that allows users to delete all the items at once:
from rest_framework.response import Response
from rest_framework.views import APIView

class DeleteAllItems(APIView):

    def delete(self, request):

        Item.objects.all().delete()

        return Response(status=status.HTTP_204_NO_CONTENT)

# view that list all the items:
from rest_framework.response import Response
from rest_framework.views import APIView

class ListItems(APIView):

    def get(self, request):
        items = Item.objects.all()
        serializer = ItemSerializer(items, many=True)
        return Response(serializer.data)
```

# **Function-based Views**
- if we are writing a view in the form of a function, we'll need to use the `@api_view` decorator
```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['DELETE'])
def delete_all_items(request):
    Item.objects.all().delete()
    return Response(status=status.HTTP_200_OK)
```
- here we converted `delete_all_items` to `APIview` subclass, only thr `DELETE` method os allowed, other methods will respond with "405 Method Not Allowed"