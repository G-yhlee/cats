#### ordering

```scala
import scala.math.Ordering

object Hello {
  def main(args: Array[String]): Unit = {
    implicit val ordering =
      Ordering.fromLessThan[Int]((a, b) => a < b)
    val absOrdering =
      Ordering.fromLessThan[Int]((x, y) => Math.abs(x) < Math.abs(y))

    final case class Rational(numerator: Int, denominator: Int)

    implicit val Rational_ordering = Ordering.fromLessThan[Rational]((x, y) =>
      (x.numerator.toDouble / x.denominator.toDouble) <
        (y.numerator.toDouble / y.denominator.toDouble)
    )

    val list = List(3, 4, 2).sorted
    val list2 = List(3, 4, 2).sorted(ordering)
    val list3 = List(-4, -1, 0, 2, 3).sorted(absOrdering)
    val list4 =
      List(Rational(1, 13), Rational(1, 22), Rational(3, 4)).sorted(
        Rational_ordering
      )
    println(list) // 2,3,4
    println(list2) // 2,3,4
    println(list3) // List(0, -1, 2, 3, -4)
    println(list4) // List(0, -1, 2, 3, -4)
  }
}


```
