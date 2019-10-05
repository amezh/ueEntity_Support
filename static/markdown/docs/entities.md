
## Introduction


*Entity* in context of ueEntity is just an integer id. 

Manipulating entities is easy and fast. 
To do that we use USceneComponent: *EntityRegistryContainer*.
Attach it to any actor to spawn. 

To create and destroy an _Entity_ call

From C++
```C++
int CreateEntity();
void DeleteEntity(int entityId);
```

From BP:
![BP](./static/img/screens/create_delete_entity.png "")