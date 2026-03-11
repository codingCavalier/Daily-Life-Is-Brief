<img width="964" height="661" alt="image" src="https://github.com/user-attachments/assets/1e47e6de-b2d9-41af-bc17-b22725a6b688" />#### 实现一个倒计时功能，看看学到了哪些知识
- 模块化开发：倒计时功能（逻辑+ui）要抽取出一个倒计时工具类（逻辑），这个工具类不应该放在主模块里，要放在har或者hsp类型的library模块里
  - 模块间依赖：被依赖模块的oh-package.json5文件中的name字段，就是依赖模块的oh-package.json5文件中的dependencies字段里的key
  - 类的导出：工具类要导出，才能被其他模块使用。导出的管理，Index.ets文件。export修饰类。export { CountdownImpl as Countdown, CountdownCallback } from './src/main/ets/utils/public/CountdownUtil'
  - 类的导入：import { Countdown, CountdownCallback } from 'lib_b_shared_3568';
- 实现工具类：
  - 定义一个接口：包含开始，暂停，恢复，重置，递减，结束
  - 工具类实现这个接口，并实现倒计时的完整逻辑，使用 setTimeOut & clearTimeOut 或者 setInterval & clearInterval 实现倒计时
  - 定义一个回调接口，接口里至少有一个方法，就是onTick(current: number): void，用于将每次递减后的值回调给使用方
  - 如果接口里的方法是可选的，即允许不实现此方法，那么用`?`修饰
  - <img width="542" height="372" alt="image" src="https://github.com/user-attachments/assets/1e882f96-4f70-4c02-9e71-93300379ee4b" />
- 注解：
  - 状态管理：
    - @State：组件私有，变化触发UI更新
    - @Prop：单向传递，父传给子，子可改但不同步回父
    - @Link：双向同步，子改父也变
    - @Provide/@Consume：跨层级传递
    - @ObjectLink：监听对象内部属性变化
    - @Watch：状态变化时执行回调
  - UI组件：
    - @Component：可复用的UI单元
    - @Entry：应用启动的页面
    - @Builder：构建UI的函数
    - @BuilderParam：接收UI构建函数作为参数
  - 生命周期：
    - @StorageProp：读取持久化数据，变化不自动同步
    - @StorageLink：读写持久化数据，变化自动同步
    - @LocalStorageLink：页面间共享状态
  - 性能优化：
    - @Reusable：复用已销毁的组件实例
    - @Track：精准控制属性更新范围
  - 自定义：
    - @Styles：定义可复用的样式
    - @Extend：扩展已有组件的样式



  
