#### 모노이드

```scala
trait SemiGroup[T]:
  extension (x: T) def combine (y: T): T

trait Monoid[T] extends SemiGroup[T]:
  def unit: T
```

#### 모노이드 인스턴스

```scala
given Monoid[String] with
  extension (x: String) def combine (y: String): String = x.concat(y)
  def unit: String = ""
```

```scala
given Monoid[Int] with
  extension (x: Int) def combine (y: Int): Int = x + y
  def unit: Int = 0
```

#### 모노이드 combineAll

```scala
def combineAll[T: Monoid](xs: List[T]): T =
  xs.foldLeft(summon[Monoid[T]].unit)(_.combine(_))
```

- apply 를 붙이면, summon을 생략가능

```scala
object Monoid:
  def apply[T](using m: Monoid[T]) = m

def combineAll[T: Monoid](xs: List[T]): T =
  xs.foldLeft(Monoid[T].unit)(_.combine(_))

```
