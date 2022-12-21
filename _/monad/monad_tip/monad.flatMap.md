#### flatmap 추상화

```scala
def flatMap[A, B](fa: Option[A])(fb: A => Option[B]): Option[B] = fa flatMap fb
def flatMap[A, B](fa: List[A])(fb: A => List[B]): List[B] = fa flatMap fb
...

// 일반화
def flatMap[A, B](fa: F[A])(fb: A => F[B]): F[B]


```
