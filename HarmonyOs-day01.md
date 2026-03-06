- 拼写：Har mo ny Os
- 官网：https://developer.huawei.com/consumer/cn/
- 工具：DevEco Studio（老版本安装完打开后，会要求安装 NodeJs 和 OHPM，OHPM是包管理工具）
- 语言：ArkTS
- 程序入口：Ability -> entry（Android对应的叫 Module -> app）
- Hello World
```ArkTS
@Entry
@Component
struct Index {
  @State message: string = 'Hello World';

  build() {
    RelativeContainer() {
      Text(this.message)
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
