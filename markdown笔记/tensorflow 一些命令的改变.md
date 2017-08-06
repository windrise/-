## tensorflow 最新版本一些命令的改变

> 大部分是Api版本问题：
>
> tf.train.SummaryWriter改为：tf.summary.FileWriter
>
>  tf.merge_all_summaries()改为：summary_op = tf.summaries.merge_all()
>
> tf.histogram_summary(var.op.name, var)改为：  tf.summary.histogram()
>
> tf.scalar_summary(l.op.name + ' (raw)', l)
>
> tf.scalar_summary('images', images)改为：tf.summary.scalar('images', images)
>
> tf.image_summary('images', images)改为：tf.summary.image('images', images)
>
>  cifar10.loss(labels, logits) 改为：cifar10.loss(logits=logits, labels=labels)
>
>  cross_entropy = tf.nn.softmax_cross_entropy_with_logits(
>         logits, dense_labels, name='cross_entropy_per_example')
>
> 改为：
>
>    cross_entropy = tf.nn.softmax_cross_entropy_with_logits(
>         logits=logits, labels=dense_labels, name='cross_entropy_per_example')
>
> if grad: 改为  if grad is not None:
>
> concated = tf.concat(1, [indices, sparse_labels])改为：
>
> concated = tf.concat([indices, sparse_labels], 1)