# DRF-Paginator
Paginate your Model QuerySet by simply passing it to the your custom paginator class with serializer specified in it.


# Example
```python3
user = User.objects.first()
data = Model.objects.all()
page_size = 3
page = 1

class CustomPaginator(NumberPaginatorResponse):
  serializer_class = YourSerializerHere
 

CustomPaginator(
      data, page_size, page,
      serializer_params = {"many": True, context={"user_id": user.id}}
      ).paginated_response()


# In this case: CustomPaginator(
#                   QuerySet, 3, 1, serializer_params = data(
#                           many=True, context={"user_id": user.id}
#                           )
#                   ).paginated_response()
# {
#    "count": 5,
#    "previous": None,
#    "next": 1,
#    "result": [
#                 {"model": 5},
#                 {"model": 6},
#                 {"model": 7},
#              ]
# }
# Where count - overall length of objects, 
# previous and next pages number 
# (if one of them doesn't exist then it will return None) and result itself.
```
