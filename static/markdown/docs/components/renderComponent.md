# Render Component 

Render component works with *InstancedStaticMesh*(ISM) or *HierarchicalInstancedStaticMesh*

Component is quite simple and consists from two fields:

* _UInstancedStaticMeshComponent* meshComponent_ - a ref to component itself
* *int instanceId* - a copy of assigned InstanceID in the ISM above. This property is not exposed to BP since rendering system will manage it for you.

Render Components can be assigned to any Entity at any time and removed in any time. Entity will keep animating even if it's not rendering anymore.

Rendering system will be notified any time any Rendering component assigned or destroyed and will manage instances according to the situation.

Entity can travel frely across the ISMs. Just remove one component and assign another one.

For example if your apple tree grew big enough and you want to swap it to another model - you can do that.

Or if you have an unloaded truck and you want to change the model to loaded one - create two ISMs and travel your entity between them.

You can control Rendering mesh with the following:

C++:

```C++
bool GetRendererComponent(int entityId, FRenderComponent& valueOut);
bool SetRendererComponent(int entityId, FRenderComponent value);
void DeleteRendererComponent(int entityId);
```

BP
![alt text](static/img/screens/render_component.png "")
