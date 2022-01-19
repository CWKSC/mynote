# Django

## rest_framework

### serializers.py

```python
from django.db.models import fields
from rest_framework import serializers
from .models import ...

class ...Serializer(serializers.ModelSerializer):
    class Meta:
        model = ...
        fields = [
           ...
        ]
```

### urls.py

```python
from rest_framework.routers import DefaultRouter
from .views import ...

router = DefaultRouter()
router.register(r'...', ...ViewSet, basename='...')
# Need basename if no define queryset (user may define get_queryset), else ignore

urlpatterns = router.urls
```

### view.py

```python
from django.shortcuts import render

from rest_framework import viewsets

from .models import ...
from .serializers import ...

class ...ViewSet(viewsets.ModelViewSet):
    queryset = ... .objects.all()
    serializer_class = ...
```

### Change id of get `url/<id>`

```python
class ...ViewSet(viewsets.ModelViewSet):
    queryset = ...
    serializer_class = ...
    lookup_field = '<field>'  # add this
```

