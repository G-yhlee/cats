```scala
trait Comparator[A] {
  def compare(x: A, y: A): Int
}

object Comparator {
  implicit object IntComparator extends Comparator[Int] {
    def compare(x: Int, y: Int): Int = Integer.compare(x, y)
  }

  implicit object StringComparator extends Comparator[String] {
    def compare(x: String, y: String): Int = x.compareTo(y)
  }
}

def max[A](x: A, y: A)(implicit comparator: Comparator[A]): A =
  if (comparator.compare(x, y) >= 0) x
  else y

println(max(10, 6))             // 10
println(max("hello", "world"))  // world
```

```scala
trait Comparator[A]:
  def compare(x: A, y: A): Int

object Comparator:
  given Comparator[Int] with
    def compare(x: Int, y: Int): Int = Integer.compare(x, y)

  given Comparator[String] with
    def compare(x: String, y: String): Int = x.compareTo(y)
end Comparator

def max[A](x: A, y: A)(using comparator: Comparator[A]): A =
  if comparator.compare(x, y) >= 0 then x
  else y

println(max(10, 6))             // 10
println(max("hello", "world"))  // world
```
