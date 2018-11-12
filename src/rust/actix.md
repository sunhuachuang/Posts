### Actix

一个Actor模型

#### Actor的生命周期 (lifecycle)

- started - method: started()
- running
- stopping
  - call `Context::stop` 调用stop方法
  - all addresses to the actor get dropped (no reference to this) 关闭所有的地址链接
  - no event objects are registered in the context 不再有内部的事件对象
  - 可以从 stopping 切换回 running 状态
  - Context::stop() => Actor::stopping() => Running::Stop
- stopped

#### Message - Actor信息交互的载体

#### Address - Message - Mailbox
- Message
  - Addr::do_send(M) 忽略actor的邮箱容量，并无条件地将邮件放入邮箱。此方法不返回消息处理的结果，并且如果actor消失，则无提示失败。
  - Addr::try_send(M) 此方法尝试立即发送消息。如果邮箱已满或已关闭（actor已死），则此方法返回SendError。
  - Addr::send(M) 此消息返回将解析为消息处理过程结果的future对象。如果删除返回的Future对象，则会取消该消息。
- Recipient
  - 收件人是地址的专用版本，仅支持一种类型的邮件。它可以用于需要将消息发送给不同类型的actor的情况。可以使用Addr::recipient() 从地址创建收件人对象。
