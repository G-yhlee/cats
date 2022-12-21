#### maybe in haskell

- 모나드 클래스

```hs
class Monad m where
    (>>=)  :: m a -> (a -> m b) -> m b
    return :: a -> m a
```

- 모나드 클래스로 생성한 maybe 모나드

```hs
instance Monad Maybe where
    Nothing  >>= f = Nothing
    (Just x) >>= f = f x
    return         = Just

```

- 다른 방식으로 작성한 maybe 모나드

```hs
return :: a -> Maybe a
return x  = Just x

(>>=)  :: Maybe a -> (a -> Maybe b) -> Maybe b
m >>= g = case m of
             Nothing -> Nothing
             Just x  -> g x
```

#### maybe monad example

- monad 인스턴스로 만든 Maybe 타입은, 기본적으로 >>= 연산을 쓸수있게 된다

```hs
-- we can use monadic operations to build complicated sequences
maternalGrandfather :: Sheep -> Maybe Sheep
maternalGrandfather s = (return s) >>= mother >>= father

fathersMaternalGrandmother :: Sheep -> Maybe Sheep
fathersMaternalGrandmother s = (return s) >>= father >>= mother >>= mother


```

#### maybe monad example \_ do 표현식

```hs
-- do 표현식
mothersPaternalGrandfather :: Sheep -> Maybe Sheep
mothersPaternalGrandfather s = do m  <- mother s
                                  gf <- father m
                                  father gf

-- >>= 표현식
mothersPaternalGrandfather s = mother s >>= (\m ->
                               father m >>= (\gf ->
                               father gf))
```
