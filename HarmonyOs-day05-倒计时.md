#### 实现一个倒计时功能，看看学到了哪些知识
- 模块化开发：倒计时功能（逻辑+ui）要抽取出一个倒计时工具类（逻辑），这个工具类不应该放在主模块里，要放在har或者hsp类型的library模块里
  - 模块间依赖：被依赖模块的oh-package.json5文件中的name字段，就是依赖模块的oh-package.json5文件中的dependencies字段里的key
  - 类的导出：工具类要导出，才能被其他模块使用。导出的管理，Index.ets文件。export修饰类。export { CountdownImpl as Countdown, CountdownCallback } from './src/main/ets/utils/public/CountdownUtil'
  - 类的导入：import { Countdown, CountdownCallback } from 'lib_b_shared_3568';
- 实现工具类：
  - 定义一个接口：包含开始，暂停，恢复，重置，递减，结束
  - 工具类实现这个接口，并实现倒计时的完整逻辑，使用 setTimeOut & clearTimeOut 或者 setInterval & clearInterval 实现倒计时
  - 定义一个回调接口，接口里至少有一个方法，就是onTick(current: number): void，用于将每次递减后的值回调给使用方
  
  



  
