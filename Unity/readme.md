**Windows-asset Store**，we will see the asset resource

**Layer** Inspector-Sorting Layer, add a layer at any time and choose it **Order in Layer**, the higher, the closer

**Add Component** when you want to add some effect on the item

box-controller ——the BVH?

Rigidbody —— set the height and it will fall down

**Windows-2D-tile palette** a helpful tool to design scene 



## 组件获取

```c
MyComponment myCom=gameObject.GetComponent<MyComponment>();  
//GetCompoment <T>()从当前游戏对象获取组件T，只在当前游戏对象中获取，没得到的就返回null，不会去子物体中去寻找。
  
MyComponment childCom=gameObject.GetComponentInChildren<MyComponment>();  
//GetCompomentInChildren<T>()先从本对象中找，有就返回，没就子物体中找，知道找完为止。
  
MyComponment[] comS=gameObject.GetComponents<MyComponment>();  
//GetComponents<T>()获取本游戏对象的所有T组件，不会去子物体中找。

MyComponment[] comS1=gameObject.GetComponentsInChildren<MyComponment>();    
MyComponment[] comSTrue=gameObject.GetComponentsInChildren<MyComponment>(true); 
//GetComponentsInChildren<T>()=GetComponentsInChildren<T>(true)取本游戏对象及子物体的所有组件 
  
MyComponment[] comSFalse=gameObject.GetComponentsInChildren<MyComponment>(false); 
//GetComponentsInChildren<T>(false)取本游戏对象及子物体的所有组件 除开非活跃的游戏对象，不是该组件是否活跃。
```

对象被关闭（not avtive)的时候，其中的所有组件都不会被获取到

#### 停用脚本

脚本内的enabled指向当前脚本，设置为false即停止

可以通过getComponent().enabled控制脚本运行状态

### 射线检测

#### 球形射线检测，可以用于检测距离的UI提示

Physics.SphereCast([Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html) **origin**, float **radius**, [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html) **direction**, out [RaycastHit](https://docs.unity3d.com/ScriptReference/RaycastHit.html) **hitInfo**, float **maxDistance** = Mathf.Infinity, int **layerMask** = DefaultRaycastLayers, [QueryTriggerInteraction](https://docs.unity3d.com/ScriptReference/QueryTriggerInteraction.html) **queryTriggerInteraction** = QueryTriggerInteraction.UseGlobal)

#### SweepTest,可以用于防止穿模

public bool **SweepTest**([Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html) **direction**, out [RaycastHit](https://docs.unity3d.com/ScriptReference/RaycastHit.html) **hitInfo**, float **maxDistance** = Mathf.Infinity, [QueryTriggerInteraction](https://docs.unity3d.com/ScriptReference/QueryTriggerInteraction.html) **queryTriggerInteraction** = QueryTriggerInteraction.UseGlobal);





# 项目入门

## Animation

### Tip

Transition中的Has Exit Time属性会让状态在固定事件后退出

### Root Motion

开启该选项可以让动画中的动作影响到Animator所在的object

在使用RigidBody的对象上，应该将UpdateMode改为Animate Physics

Animations are used to move and rotate all the GameObjects within a particular hierarchy.

Apply Root Motion is enabled on your Animator component,  any movement of the root in the animation will be applied every frame. 