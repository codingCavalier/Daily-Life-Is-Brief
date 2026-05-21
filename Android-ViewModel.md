#### 关于Activity中的ViewModel是如何自动取消内部的viewModelScope的
1. ComponentActivity 不仅仅实现了 LifecycleOwner 还实现了 ViewModelStoreOwner
   <img width="845" height="343" alt="image" src="https://github.com/user-attachments/assets/05d1aba2-d2ff-4caa-bd95-134f774e522c" />
2. ViewModelStoreOwner 的作用是在 Lifecycle 监听到 ON_DESTROY 时，调用 ViewModelStoreOwner 的 clear() 方法
   <img width="865" height="380" alt="image" src="https://github.com/user-attachments/assets/374a0c17-8f04-4ec0-ae45-6061cddd1858" />
3. 这会使得 ViewModelStoreOwner 里面持有的所有 ViewModel 都调用自己的 clear() 方法
   <img width="810" height="598" alt="image" src="https://github.com/user-attachments/assets/2b4533ba-971b-499d-92e4-807750f7d0e9" />
4. 而我们使用的 viewModelScope 是作为一个 键值对的值，存在 ViewModel 内部的，key 是 JOB_KEY，value 是 viewModelScope
   <img width="876" height="427" alt="image" src="https://github.com/user-attachments/assets/b5612104-3dcd-42a7-9669-e55639737b50" />
5. 在 ViewModel 的 closeWithRuntimeException 方法中，会判断是否是 Closeable ，进而调用其 close() 方法，而上述的 viewModelScope 就是一个 CloseableCoroutineScope（看第4条）
   <img width="666" height="262" alt="image" src="https://github.com/user-attachments/assets/bfdf305a-00e9-4f20-9d4c-84540b6caedd" />
6. **假如自己创建了一个ViewModel实例，是没有上述效果的，想实现上述效果，不仅要实现 LifecycleOwner 还得实现 ViewModelStoreOwner，而且要主动在合适的时机调用 ViewModelStoreOwner 的 clear() 方法**
7. 其实绕来绕去，就是调用 ViewModel 的 clear() 方法即可。可以自己手动调用。
