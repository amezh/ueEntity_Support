# Transform Component

Transform component is a storage for entity Transform
It's also very important part of a plugin infrastructure.
It's a dependancy for Rendering component and Transform Animation components family.

Removing the component from entity will result in removal of Rendering and Animation compoments as well since we can't render or transform anything without their transform storage.

It contains two fields

* *FTransform transform;* -  this is BP exposed transform itself
* *bool isDirty;* - managed internaly by aanimation and rendering systems.

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
