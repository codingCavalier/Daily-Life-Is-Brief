- 拼写：Har mo ny Os
- 官网：https://developer.huawei.com/consumer/cn/
- 工具：DevEco Studio（老版本安装完打开后，会要求安装 NodeJs 和 OHPM，OHPM是包管理工具）
- 语言：ArkTS <- TypeScript <- JavaScript
- 程序入口：Ability -> entry（Android对应的叫 Module -> app）
- Hello World
```ArkTS
@Entry // @Entry是装饰器，表明可以独立访问，这是一个页面的入口
@Component // @Component是装饰器，表明这是一个组件
struct Index { // 自定义组件，可复用的UI单元
  @State message: string = 'Hello World'; // @State是装饰器，用于数据和UI动态联动更新

  build() {
    RelativeContainer() { // 容器组件
      Text(this.message) // 基础组件
        .id('HelloWorld')
        .fontSize($r('app.float.page_text_font_size'))
        .fontWeight(FontWeight.Bold)
        .alignRules({
          center: { anchor: '__container__', align: VerticalAlign.Center },
          middle: { anchor: '__container__', align: HorizontalAlign.Center }
        })
        .onClick(() => {
          this.message = 'Welcome';
        })
    }
    .height('100%')
    .width('100%')
  }
}
```
- <img width="355" height="213" alt="image" src="https://github.com/user-attachments/assets/3878e094-5dff-41c3-b3ea-6a0b73114485" />
- TypeScript 在 JavaScript 的基础上加入了静态类型检查功能，因此每一个变量都有固定的数据类型。
- let声明变量，const声明常量。let message: string = 'Hello World'
- string：字符串，单引号双引号都行
- number：数字，不区分是不是浮点型，支持ob二进制，ox十六进制等写法
- boolean：布尔，true，false
- any：类似Java里的Object类型，或者Kotlin里的Any类型，你懂的
- Union类型：竖线分隔，即这个值可以是多个类型中的某一个类型。let banana: string|boolean|number = 'Hello'
- 结构类型：使用大括号{}定义。或者叫对象类型，其实就是一个Struct结构。let a = {name: 'Andy', age: 19}，取值的时候这样写console.log(a.name)
- console.log：打印日志到控制台
