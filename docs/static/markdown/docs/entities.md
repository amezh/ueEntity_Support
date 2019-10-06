
# Introduction

*Entity* in context of ueEntity is just an integer id. 
> WARNING: IDs are reusable, so if you plan to destroy entities and create new ones - don't store IDs around

Manipulating entities is easy and fast.
To do that we use USceneComponent: *EntityRegistryContainer*.
Attach it to any actor to spawn.

To create and destroy an _Entity_ do one of the following:

From C++

```C++
int CreateEntity();
void DeleteEntity(int entityId);
```

From BP:

![alt text](static/img/screens/create_delete_entt.png "")
