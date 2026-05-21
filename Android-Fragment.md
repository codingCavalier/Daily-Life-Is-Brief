1. 关于事务
- 如果分成多个事务，前一个事务remove，后一个事务add，将会导致fragment内部状态错乱，无法正确添加和显示，需要先执行executePendingTransactions方法
- 建议使用detach和attach（会走onDestroyView和重走onCreateView），而不是使用remove和add

```kotlin
childFragmentManager.executePendingTransactions() // 这一行很重要，它能让之前的事务执行完
childFragmentManager.beginTransaction().remove(fragmentA).commitAllowingStateLoss()

childFragmentManager.executePendingTransactions() // 这一行很重要，它能让之前的事务执行完，fragmentA 的状态才会处于正常状态
childFragmentManager.beginTransaction()
            .add(R.id.content_base, fragmentA, tag)
            .commitAllowingStateLoss()
```
