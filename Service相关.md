#### 关于彻底关闭应用
- 不要用System.exit(0)退出，它会直接关闭当前进程的虚拟机，导致Activity和Service无法回调onDestroy方法。
- 而`onStartCommand`方法返回`START_STICKY`的服务，它的意思是，如果我被杀死了（意外杀死，即未调用onDestroy），请系统尝试重启我。
- System.exit(0)恰恰符合了这一点，这就导致1秒或者2秒后，Application又被重新创建了，即我们的应用没被彻底关闭

<img width="914" height="710" alt="image" src="https://github.com/user-attachments/assets/cb6232ab-c4a3-4afe-ae32-99f0d832f924" />
