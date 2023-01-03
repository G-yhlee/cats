#### ordering

```scala
import scala.math.Ordering

object Hello {
  def main(args: Array[String]): Unit = {
    implicit val ordering =
      Ordering.fromLessThan[Int]((a, b) => a < b)
    val absOrdering =
      Ordering.fromLessThan[Int]((x, y) => Math.abs(x) < Math.abs(y))

    val list = List(3, 4, 2).sorted
    val list2 = List(3, 4, 2).sorted(ordering)
    val list3 = List(-4, -1, 0, 2, 3).sorted(absOrdering)
    println(list) // 2,3,4
    println(list2) // 2,3,4
    println(list3) // List(0, -1, 2, 3, -4)
  }
}


```
