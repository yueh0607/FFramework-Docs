---
sidebar_position: 1
---

# FEvent - 事件系统

## 1.优势

- **事件类型安全**

  即事件系统能够区分“有返回值事件”和“无返回值事件”，能够实时给出错误防止错误的事件调用。

  传统基于观察者模式的事件系统采用各种标识符(int，string，enum，Type)作为事件标识，无法在编译时区分事件有无返回值，只能依赖开发者记忆，而FEvent能够实时的提示调用类型是否正确。

- **参数类型安全**

  FEvent也提供实时的参数类型检查，要求开发者调用事件时就提供正确的参数类型。

  传统基于观察者模式的事件系统一般使用接口要求实现并开发者封装参数类，或者使用object[]擦除类型，不能方便的实现参数类型安全，而FEvent在调用时即要求类型，且无需各种繁杂的类定义。

## 2.简单使用

### 定义事件

在FEvent中，定义事件需要定义接口，例如

```c#
/// <summary>
/// 测试事件，第一个参数传入年龄 0-200 ，第二个参数传入姓名如"Joe"，无返回值
/// </summary>
public interface ITestEvent : ISendEvent<int,string> { }   //或ICallEvent<int,string,int> 
```

建议在声明事件时说清楚其用途和参数，返回值信息，而参数类型和`ISendEvent<>`的泛型参数一致。`ICallEvent<>`中最后一个参数为返回值类型。FEvent提供了至少5个参数的泛型适配（也就是说每个泛型匹配都会至少维护0-5个参数的 版本，如果有返回值，则为0-6个）



### 订阅事件

```c#
 //可以使用lambda表达式注册，但是不建议这样做，可能会因为lambda闭包不当使用引入GCAlloc或者带来内存泄漏风险
 FEvent.Instance.Operator<ITestEvent>().Subscribe((x, y) =>
 {
      Console.WriteLine(x.ToString() + y);
 });


	
 //订阅一个事件(this可以是任意一个object)
 this.Operator<ITestEvent>().Subscribe(TestEvent);
 
 public void TestEvent(int x,string y)
 {
     Console.WriteLine(x + y);
 }

 //重复订阅是允许的，可以在一个事件中添加多个订阅者
```

### 取消订阅

```c#
 //取消订阅一个事件
 this.Operator<ITestEvent>().UnSubscribe(TestEvent);

 //如果担心有二次GC，可以这样做，不过事实上取消订阅的频率往往非常小，甚至不会取消，一般不需要这样做
 Action<int,string> method = TestEvent;
 this.Operator<ITestEvent>().Subscribe(method);
 this.Operator<ITestEvent>().UnSubscribe(method);
```

### Send方式发布事件

```c#
 //取消订阅一个事件
 this.Operator<ITestEvent>().Send(10,"Joe");

 //Console输出
 10Joe
```

### Call方式发布事件

```c#
 //因为订阅是可以叠加的，但是返回值只能有一个，此方式将调用第一个订阅
 var result = this.Operator<ITestEvent2>().CallFirst(10,"Joe");
 //返回整个返回值列表
 var result2 = this.Operator<ITestEvent2>().Call(10,"Joe");
```

