- 拼写：Har mo ny Os
- 官网：https://developer.huawei.com/consumer/cn/
- 工具：DevEco Studio（老版本安装完打开后，会要求安装 NodeJs 和 OHPM，OHPM是包管理工具）
- 语言：ArkTS <- TypeScript <- JavaScript
- 架构
  - <img width="981" height="419" alt="image" src="https://github.com/user-attachments/assets/daac148f-6b75-4677-b3d7-ba5c0447b4b3" />

- Ability
  - UIAbility​ - Activity（安卓）​ - 负责 UI 交互和界面展示。
  - **Stage模型​ (API 10+) 开始，用ServiceExtensionAbility**。ParticleAbility​ (或 ServiceAbility) - Service（安卓） - 用于在后台运行任务，无 UI。
  - **Stage模型​ (API 10+) 开始，用DataShareExtensionAbility**。DataAbility​ - ContentProvider（安卓）​ - 用于跨应用数据共享。
  - FormExtensionAbility，提供服务卡片（桌面小部件）的能力。
  - InputMethodExtensionAbility，自定义输入法。
  - AccessibilityExtensionAbility，无障碍。
  - WorkSchedulerExtensionAbility，在特定条件（如充电、连网）下执行后台任务。
- entry
  - 对应安卓配置为 "com.android.application" 类型的Module
- feature
  - 对应安卓配置为 "com.android.library" 类型的Module

- 结构
  - <img width="360" height="360" alt="image" src="https://github.com/user-attachments/assets/49733e6b-9132-4b97-9e00-66450c8fa661" />

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

