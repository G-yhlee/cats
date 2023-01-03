#### 기본형

-

```scala
trait Printer[A] {
  def print(a: A): String
}
object Printer {
  def apply[A](implicit p: Printer[A]): Printer[A] = summon[Printer[A]]
}
implicit val intPrinter: Printer[Int] = new Printer[Int] {
  def print(i: Int): String = s"int $i"
}
implicit val stringPrinter: Printer[String] = new Printer[String] {
  def print(s: String): String = s"string $s"
}
implicit class PrinterOps[A](val a: A) extends AnyVal {
  def print(implicit p: Printer[A]): String = p.print(a)
}

object Hello {

  def main(args: Array[String]): Unit = {
    import Printer._
    println(Printer[Int].print(100))
    println(Printer[String].print("100"))
    println(Printer[(String,Int)].print(("100",100)))
    println(new PrinterOps(100).print)
    println(new PrinterOps("100").print)
    println(new PrinterOps(("100",100)).print)a
    println(100.print)aaaa
    println("100".print)
    println(("100",100).print)
  }
}



```

#### 기본형

```scala
trait Printer[A]{
  def print(a: A): String
}

object Printer {
  def apply[A](implicit p: Printer[A]): Printer[A] = p

  implicit val intPrinter: Printer[Int] = new Printer[Int] {
    def print(i: Int):String = s"int $i"
  }

  implicit class PrinterOps[A](val a: A) extends AnyVal {
    def print(implicit p: Printer[A]):String = p.print(a)
  }
}

object Hello {
  def main(args: Array[String]): Unit = {
    import Printer._
    println(Printer[Int].print(100))
    println(new PrinterOps(100).print)
    println(PrinterOps(100).print)
    println(100.print)
    println("100".print)
  }
}
```

#### 기본형 + 람다

- 자바8 부터 trait에 메서드가 하나일경우 람다로 쓸수있다

```scala
package simplex


trait Printer[A]{
  def print(a: A): String
}

object Printer {
  def apply[A](implicit p: Printer[A]): Printer[A] = p

  implicit val intPrinter: Printer[Int] = (i: Int)=>s"int $i"

  implicit val stringPrinter: Printer[String] = (i: String)=>s"String $i"

  implicit class PrinterOps[A](val a: A) extends AnyVal {
    def print(implicit p: Printer[A]):String = p.print(a)
  }

  // implicit def tuple2Printer[A,B](implicit ap: Printer[A], bp: Printer[B]): Printer[(A,B)] = {
  //   case (a ,b) => s"tuple ${a.print} ${b.print}"
  // }

  // context bound
  // implicit 파라미터 부분을 없앰
  implicit def tuple2Printer[A: Printer,B: Printer]: Printer[(A,B)] = {
    case (a ,b) => s"tuple ${a.print} ${b.print}"
  }
}

object Hello {
  def main(args: Array[String]): Unit = {
    import Printer._
    println(Printer[Int].print(100))
    println(new PrinterOps(100).print)
    println(PrinterOps(100).print)
    println(100.print)
    println("100".print)
    println(("100",100).print)
  }
}


```

#### 스칼라3 버젼

- 자바8 부터 trait에 메서드가 하나일경우 람다로 쓸수있다

```scala
package simplex


trait Printer[A]{
  def print(a: A): String
}

object Printer {
//   def apply[A](using p: Printer[A]): Printer[A] = p
//   def apply[A](using p: Printer[A]): Printer[A] = implicitly[Printer[A]]
//   def apply[A](using p: Printer[A]): Printer[A] = sommon[Printer[A]]
  def apply[A](using p: Printer[A]): Printer[A] = summon

  given Printer[Int] = (i: Int)=>s"int $i"

  given Printer[String] = (i: String)=>s"String $i"

    // implicit class PrinterOps[A](val a: A) extends AnyVal {
  //   def print(implicit p: Printer[A]):String = p.print(a)
  // }

  extension [A](a: A)
    def print(using p: Printer[A]):String = p.print(a)

  given [A: Printer,B: Printer]: Printer[(A,B)] =
    case (a ,b) => s"tuple ${a.print} ${b.print}"
}

object Hello {
  def main(args: Array[String]): Unit = {
    import Printer._
    println(100.print)
  }
}


```
