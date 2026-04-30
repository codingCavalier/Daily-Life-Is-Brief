#### 关于彻底关闭应用
1. System.exit(0) 会直接杀死虚拟机进程，导致 Activity（还有里面的Fragment）和 Service 无法回调 onDestroy 方法，而 onStartCommand 方法返回 START_STICKY 的那些服务，如果被意外杀死（经过测试验证，不是通过 stopService 方法关闭的，属于意外关闭），则系统会尝试重启该服务，这是安卓系统默认的保活机制，System.exit(0) 恰恰符合了这一点
2. 根本原因是，我们应用内依赖了很多第三方库，而这些第三方库里会启动一些服务，这些服务的销毁动作，我们一般都放在 onDestroy 方法里，这恰好导致 System.exit(0) 时，此服务未正常关闭
3. 经过测试，发现只要调用了context.stopService(要被关闭的服务)方法，就可以不被安卓系统重启，即使没有调用 onDestroy 方法也没关系。

<img width="914" height="710" alt="image" src="https://github.com/user-attachments/assets/cb6232ab-c4a3-4afe-ae32-99f0d832f924" />
