#### functor

- list [] of map = map
- functor f of map = fmap

```haskell
fmap :: Functor f => (a -> b) -> f a -> f b -- functor f of map
map :: (a -> b) -> [a] -> [b] -- list [] of map
```

#### functor 와 map 차이

- map 은 list 를 대상으로 하기때문에 , list 에만 적용가능
- fmap 은 list 를 포함한 다른 functor 모두를 대상으로 하기 때문에, 모두 적용가능

```haskell
main = do

  -- map
   print(map (subtract 1) [2,4,8,16]) -- [1,3,7,15]

  -- fmap
   print(fmap (subtract 1) [2,4,8,16]) -- [1,3,7,15]
   print (fmap  (+7)(Just 10)) -- Just 17
   print (fmap  (+7) Nothing) -- Nothing

```

#### functor's law

```md
# Identity

fmap id = id

# Composition

fmap f . fmap g = fmap (f . g)
```

#### functor in short

```haskell
fmap :: (a -> b) -> f a -> f b
```

#### map, flatMap

- 다른 방식으로 표현

```md
- F[A] => F[B] by A => B , 이 함수를 map 이라 한다.
- F[A] => F[B] by A => F[B] , 이 함수를 flatMap 이라 한다.

- functor : F[A] 이고 map 연산이 가능하면, 펑터이다
- monad : F[A] 이고 map ,flatMap 연산이 가능하면, 모나드이다
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
https://www.tutorialspoint.com/haskell/haskell_functor.htm
