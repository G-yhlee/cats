#### map, flatMap

- F[A] => F[B] by A => B , 이 함수를 map 이라 한다.
- F[A] => F[B] by A => F[B] , 이 함수를 flatMap 이라 한다.

- functor : F[A] 이고 map 연산이 가능하면, 펑터이다
- monad : F[A] 이고 map ,flatMap 연산이 가능하면, 모나드이다

#### monad

어떤 타입 M에 대해 다음의 두 연산이 가능하면 모나드이다.

- pure :: a -> M a
- compose :: (M a) -> (a -> M b) -> (M b)

#### monad in cats

- monad is a monoid in the category of endofunctors.
- endofunctor is a functor mapping a category to itself

#### flatmap 추상화

```scala
def flatMap[A, B](fa: Option[A])(fb: A => Option[B]): Option[B] = fa flatMap fb
def flatMap[A, B](fa: List[A])(fb: A => List[B]): List[B] = fa flatMap fb
...

// 일반화
def flatMap[A, B](fa: F[A])(fb: A => F[B]): F[B]


```

#### monad

```scala
def flatMap[A, B](oa: Option[A])(fb: A => Option[B]): Option[B] = oa flatMap fb





```
