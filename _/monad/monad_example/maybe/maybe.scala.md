#### Maybe in scala

```scala
sealed trait Maybe[A] {

  // (>>=)  :: Maybe a -> (a -> Maybe b) -> Maybe b
  // m >>= g = case m of
  //              Nothing -> Nothing
  //              Just x  -> g x

  def flatMap[B](fn: A => Maybe[B]): Maybe[B] =
    this match {
      case Full(v) => fn(v)
      case Empty() => Empty[B]()
    }
}

// return :: a -> Maybe a
// return x = Full(x)
final case class Full[A](value: A) extends Maybe[A]
final case class Empty[A]() extends Maybe[A]


Full(1) flatMap { x =>
    Full(2) flatMap { y =>
      Full(3) flatMap { z =>
        Full(x + y + z)
      }
    }
  } // 6

Full(1) flatMap { x =>
    Full(x + 1)
} // 2

```
