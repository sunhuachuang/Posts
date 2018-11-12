##### std::sync::Arc
引用计数

```
let connections = Arc::new(Mutex::new(HashMap::new()));
connections.lock()

```

##### std::sync::Mutex
锁

##### futures::sync::mpsc
多个生产者，一个消费者模型。实现为FIFO。
`let (tx, rx) = futures::sync::mpsc::unbounded();`
`pub fn unbounded<T>() -> (UnboundedSender<T>, UnboundedReceiver<T>)`
