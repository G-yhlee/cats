#### functor

```haskell
fmap :: (a -> b) -> fa -> fb
```

#### map, flatMap

- (정확하지 않음. 수정필요)

```md
- F[A] => F[B] by A => B , 이 함수를 map 이라 한다.
- F[A] => F[B] by A => F[B] , 이 함수를 flatMap 이라 한다.

- functor : F[A] 이고 map 연산이 가능하면, 펑터이다
- monad : F[A] 이고 map ,flatMap 연산이 가능하면, 모나드이다
```

```js
const f = [1, 2, 3];
f.map(double); //[2, 4, 6]
```

#### map 함수 예시

- LinkedList[A] 에 정의된 map 함수

```scala
sealed trait LinkedList[A] {
  def map[B](fn: A => B): LinkedList[B] =
    this match {
      case Pair(hd, tl) => ???
      case End() => ???
    }
}
final case class Pair[A](head: A, tail: LinkedList[A]) extends LinkedList[A]
final case class End[A]() extends LinkedList[A]
```

#### functor's law

- functor는 다음의 두가지를 만족한다.

```md
- 항등성 (= identity)
- 합성 (= compose)
```

#### pure

```js
const f = [1, 2, 3];
f.map((x) => x); //[1, 2, 3]
```

#### compose

```js
Functor.map((x) => f(g(x))) === Functor.map(g).map(f);
```

#### endofunctors

Functor :: X -> Y
endoFunctor :: X -> X

- ...monad is monoid in the category of endofunctors

#### functor 구현

```js
const Identity = (value) => ({ map: (fn) => Identity(fn(value)) });

// trace() is a utility to let you easily inspect
// the contents.
const trace = (x) => {
  console.log(x);
  return x;
};

const u = Identity(2);

// Identity law
u.map(trace); // 2
u.map((x) => x).map(trace); // 2

const f = (n) => n + 1;
const g = (n) => n * 2;

// Composition law
const r1 = u.map((x) => f(g(x)));
const r2 = u.map(g).map(f);

r1.map(trace); // 5
r2.map(trace); // 5
```

#### functor의 이점

- map 연산을 통해 펑터에 대해 다앙한 함수를 발견할수있다.
- F[A] => F[B] 를 만족하는 모든 함수는 map 함수로 정의 가능.

```scala
// map 함수로 표현한 unzip
val list = List((1,2),(3,4),(4,5))

val unZipByMap = ( list.map(e => e._1), list.map(e => e._2) )
val unZip = list.unzip
```

#### 참고

https://kpug.github.io/fp-gitbook/Chapter4.html
