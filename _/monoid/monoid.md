#### 요약

- set : set{}
- magma : set{이항연산}
- Semigroup : set{이항연산 when 결합법칙}
- monoid : set{이항연산 when 결합법칙,항등원 }
- group : set{이항연산 when 결합법칙,항등원,역원 }

#### 예시

```scala
trait Monoid[A]{
    def op(a1:A, a2: A):A
    def zero: A
}

// 정수 집합에서의 모노이드
val 정수의_덧셈_모노이드 = new Monoid[Int] {
  def op(a1: Int, a2: Int): Int = a1 + a2
  def identity = 0
}

val 정수의_곱셈_모노이드 = new Monoid[Int] {
  def op(a1: Int, a2: Int): Int = a1 * a2
  def identity = 1
}

// 문자열 집합에서의 모노이드
val stringConcatMonoid = new Monoid[String] {
  def op(a1: String, a2: String): String = a1 + a2
  def identity = ""
}

// 리스트 집합의 모노이드
val listConcatMonoid[A] = new Monoid[List[A]] {
  def op(a1: List[A], a2: List[A]): List[A] = a1 ++ a2
  def identity = Nil // scala에서 Nil은 empty list와 같다
}

// 옵션 집합의 모노이드
val optionMonoid[A] = new Monoid[Option[A]] {
  def op(a1: Option[A], a2: Option[A]): Option[A] = a1 orElse a2
  val identity = None
}

```

#### 모노이드의 이점

- 병렬연산

```scala
op(op(op(1, 2), 3), 4) // foldLeft
op(1, op(2, op(3, 4))) // foldRight

op(op(1, 2), op(3, 4)) // 병렬 연산

```
