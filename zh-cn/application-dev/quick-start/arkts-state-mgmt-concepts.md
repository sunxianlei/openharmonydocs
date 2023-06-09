# 基本概念

ArkTS提供了多维度的状态管理机制，在ArkUI开发框架中，和UI相关联的数据，不仅可以在组件内使用，还可以在不同组件层级间传递，比如父子组件之间、爷孙组件之间，也可以是应用全局范围内的传递。另外，从数据的传递形式来看，可分为只读的单向传递和可变更的双向传递。开发者可以灵活地利用这些能力来实现数据和UI的联动。


![](figures/CoreSpec_figures_state-mgmt-overview.png)


## 页面级变量的状态管理

| 装饰器      | 装饰内容                  | 说明                                                         |
| ----------- | ------------------------- | ------------------------------------------------------------ |
| @State      | 基本数据类型，类，数组    | 修饰的状态数据被修改时会触发组件的build方法进行UI界面更新。  |
| @Prop       | 基本数据类型              | 修改后的状态数据用于在父组件和子组件之间建立单向数据依赖关系。修改父组件关联数据时，当前组件会重新渲染。 |
| @Link       | 基本数据类型，类，数组    | 父子组件之间的双向数据绑定，父组件的内部状态数据作为数据源，任何一方所做的修改都会反映给另一方。 |
| @Observed   | 类                        | @Observed应用于类，表示该类中的数据变更被UI页面管理。        |
| @ObjectLink | 被@Observed所装饰类的对象 | @ObjectLink装饰的状态数据被修改时，在父组件或者其他兄弟组件内与它关联的状态数据所在的组件都会重新渲染。 |
| @Provide    | 基本数据类型，类，数组    | @Provide作为数据的提供方，可以更新其子孙节点的数据，并触发页面重新渲染。 |
| @Consume    | 基本数据类型，类，数组    | @Consume装饰的变量在感知到@Provide装饰的变量更新后，会触发当前自定义组件的重新渲染。 |

## 应用级变量的状态管理

AppStorage是整个应用程序状态的中心“数据库”，UI框架会针对应用程序创建单例AppStorage对象，并提供相应的装饰器和接口供应用程序使用。

- @StorageLink：@StorageLink(name)的原理类似于@Consume(name)，不同的是，该给定名称的链接对象是从AppStorage中获得的，在UI组件和AppStorage之间建立双向绑定同步数据。
- @StorageProp：@StorageProp(name)将UI组件数据与AppStorage进行单向同步，AppStorage中值的更改会更新UI组件中的数据，但UI组件无法更改AppStorage中的数据。
- AppStorage还提供了用于业务逻辑实现的API，用于添加、读取、修改和删除应用程序的状态数据，此API所做的更改会导致修改的状态数据同步到UI组件上进行UI更新。
- LocalStorage是应用程序中每一个Ability的存储器。
- @LocalStorageLink：组件通过使用@LocalStorageLink(key)装饰的状态变量，key值为LocalStorage中的属性键值，与LocalStorage建立双向数据绑定。
- @LocalStorageProp：组件通过使用@LocalStorageProp(key)装饰的状态变量，key值为LocalStorage中的属性键值，与LocalStorage建立单向数据绑定。
- PersistentStorage提供了一些静态方法用来管理应用持久化数据，可以将特定标记的持久化数据链接到AppStorage中，并由AppStorage接口访问对应持久化数据，或者通过@StorageLink装饰器来访问对应key的变量。 
- Environment是框架在应用程序启动时创建的单例对象，它为AppStorage提供了一系列应用程序需要的环境状态数据，这些数据描述了应用程序运行的设备环境。 

请参考[状态变量数据类型声明的使用限制](arkts-restrictions-and-extensions.md)了解状态变量使用规范。
