#### map, flatMap

- F[A] => F[B] by A => B , 이 함수를 map 이라 한다.
- F[A] => F[B] by A => F[B] , 이 함수를 flatMap 이라 한다.

- functor : F[A] 이고 map 연산이 가능하면, 펑터이다
- monad : F[A] 이고 map ,flatMap 연산이 가능하면, 모나드이다

#### functor

```haskell
fmap :: (a -> b) -> fa -> fb
```

```js
const f = [1, 2, 3];
f.map(double); //[2, 4, 6]
```

#### functor's law

- 항등 pure
- 합성 compose

```js
const f = [1, 2, 3];
f.map((x) => x); //[1, 2, 3]
```

```js
Functor.map(f.g) === Functor.map(g).map(f);
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
