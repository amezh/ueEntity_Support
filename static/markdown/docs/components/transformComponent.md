# Transform Component

Removing the component from the entity will result in the removal of Rendering and Animation components as well since we can't render or transform anything without their transform storage.

It contains two fields

* *FTransform transform;* -  this is BP exposed transform itself
* *bool isDirty;* - managed internally by animation and rendering systems.

>WARNING: _if you ever change it by ref from C++ make sure to mark it Dirty as well or rendering system will ignore it_

manipulating the component is simple:

C++

```C++
bool GetTransformComponent(int entityId, FTransformComponent& valueOut);
bool SetTransformComponent(int entityId, FTransformComponent value);
void DeleteTransformComponent(int entityId);
```

BP:
![alt text](static/img/screens/transform_component.png "")
