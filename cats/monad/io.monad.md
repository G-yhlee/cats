#### IOMonad

```scala
abstract class IO[+A]{
    def unsafeRunSync()(implicit runtime: IORuntime): A
    def flatMap[B](f: A=> IO[B]): IO[B]
}

object IO {
    def delay[A](computation: => A) : IO[A]
    def apply[A](thunk: => A):IO[A]
    def pure[A](value: A): IO[A]
}
```
