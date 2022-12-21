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

#### ref.

[All_About_Monads](https://wiki.haskell.org/All_About_Monads#Introduction)
[모나드란무엇인가](https://ence2.github.io/2020/11/%EB%AA%A8%EB%82%98%EB%93%9Cmonad%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80/#:~:text=%EC%97%AD%EC%82%AC%EC%A0%81%EC%9C%BC%EB%A1%9C%20%EB%B3%B4%EB%A9%B4%20%EB%AA%A8%EB%82%98%EB%93%9C%EB%8A%94,%EC%9E%85%EC%B6%9C%EB%A0%A5%EC%97%90%20%ED%95%9C%EC%A0%95%EB%90%98%EC%A7%80%20%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4)
