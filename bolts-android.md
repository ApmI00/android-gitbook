# Bolts-Android

`Bolts.Task.continueWith()` 相當於 `Observable.map()`,
`Bolts.Task.continueWithTask()` 相當於 `Observable.flatMap()`

```java
Observable<ParseObject> saveObs;
...
saveObs.flatMap(o -> Observable.just(o)).subscribe();
```

```java
Task<ParseObject> saveAsync;
...
saveAsync(obj).continueWith(new Continuation<ParseObject, Void>() {
  public Void then(Task<ParseObject> task) throws Exception {
    if (task.isCancelled()) {
      // 取消
    } else if (task.isFaulted()) {
      // 失敗
      Exception error = task.getError();
    } else {
      // 成功
      ParseObject object = task.getResult();
    }
    return null;
  }
});
```

## See Also

* https://github.com/BoltsFramework/Bolts-Android