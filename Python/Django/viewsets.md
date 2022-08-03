# **ViewSets**
- a type of `class-based view`
- most significant advantage of ViewSets is that tge URL construction is handled automatically (with a router class), which helps with the consistency of the URL conventions across our API and minimizes the amount of code we need to write
- 4 types of ViewSets, from the most basic to the most powerful:
1. ViewSet
2. GenericViewSet
3. ReadOnlyModelViewSet
4. ModelViewSet

![ViewSet](https://testdriven.io/static/images/blog/django/drf-views/all_viewsets.png)

# **ViewSet Class**

```python
from django.shortcuts import get_object_or_404
from rest_framework.response import Response
from rest_framework.viewsets import ViewSet

class ItemViewSet(ViewSet):
    queryset = Item.objects.all()

    def list(self, request):
        serializer = ItemSerializer(self.queryset, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        item = get_object_or_404(self.queryset, pk=pk)
        serializer = ItemSerializer(item)
        return Response(serializer.data)
```
- we can also create custom actions with the `@action` decorator
```python
from django.shortcuts import get_object_or_404
from rest_framework.response import Response
from rest_framework.viewsets import ViewSet

class ItemsViewSet(ViewSet):

    queryset = Item.objects.all()

    def list(self, request):
        serializer = ItemSerializer(self.queryset, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        item = get_object_or_404(self.queryset, pk=pk)
        serializer = ItemSerializer(item)
        return Response(serializer.data)

    # the 'methods' parameter is optional, whereas the 'detail' parameter is not
    # 'detail' parameter should be set as 'True' if the action is meant for single object
    # or 'False' if it's meant for all objects
    @action(detail=False, methods=['get'])
    def items_not_done(self, request):
        user_count = Item.objects.filter(done=False).count()

        return Response(user_count)
```