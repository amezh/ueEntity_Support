# Custom Component

* [Introduction](/#/ueentity/docs/components/CustomComponent#intro)
* [Creating bag and component](/#/ueentity/docs/components/CustomComponent#component)
* [Modifying fields](/#/ueentity/docs/components/CustomComponent#fields)

## Introduction <a id="intro" name="intro"></a>

Since in C++ we can't create classes in runtime and we want to be able to manipulate data from BP - we invented Custom component

It's a named list of components attached to your [Entity](/#/ueentity/docs/entities) in a bag (aka FBagComponent).
To make it look like a structure we are grouping fields in a bag as "Components"

Each entity has a bag.
Each component has a name and its own set of fields

To visualize it looks like this:

![alt text](static/img/screens/bag_structure.png "")

It looks heavy for performance but in reality, it's not bad at all. More info on performance in section: [System](/#/ueentity/docs/systems)
___

<a id="component" name="component"></a>

## Bag and component

With a bag - it's simple, you don't have to worry about them at all. We'll create them as needed and delete them from memory with Entity.

Components, on the other hand, are a bit more tricky.

There are 3 ways to do that:
![alt text](static/img/screens/bp_component_add.png "")

* 1. You create an empty component with no pre-defined fields. Whenever you will do SetValue we'll create a field on the fly if it's not there.
* 2. Option 2 is to create component structure from the existing BP structure, we'll cache it for future uses and you can attach it to any or all the entities you need.
* 3. We can create a component from the existing structure *and* copy all the values to fields. However while convenient this is a very slow operation and will kill performance for you if done inside the system loop (well maybe if you do it for like 100 entities it will be alright) but seriously, use on your own risk.

___

<a id="fields" name="fields"></a>

## Fields

We have our component how do we Get\Set field? And what type of fields are supported out of the box?
Let's take a look.

Since components are structs and you're not allowed to use *UFUNCTION* in the struct and since we are not blessed with wildcard blueprint output nodes for value types we have a BP Function library with a bunch of setters and getters:

![alt text](static/img/screens/custom_comp_getset.png "")

From C++ they are all static functions of _UComponentFunctions_

Supported types are:

* int
* float
* FText
* FString
* FName
* bool
* FVector
* FEntityComponent - for nested stuctures

In reality, components will support any type you want. Just not everything has Get and Set fields exposed. if you look at implementation, get and set values are templated.
So even if you're not very good with C++, copy code below into your own C++ Blueprint Function Library and add whatever types you need between <>

```C++
static bool GetValueInt(UPARAM(ref) FEntityComponent& Component, FString fieldName, int& valueOut)
{
    return Component.GetFieldValue<int>(fieldName, valueOut);
};
static bool SetValueInt(UPARAM(ref) FEntityComponent& Component, FString fieldName, int value)
{
    return Component.SetFieldValue<int>(fieldName, value);
};
```

If you have a reference to the _Bag_  (which you will in systems loop functions), you may also use _GetCustomComponent_ function from the same BP library to get your component by name.
