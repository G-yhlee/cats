#### maybe in haskell

- 모나드 클래스

```hs
class Monad m where
    (>>=)  :: m a -> (a -> m b) -> m b
    return :: a -> m a
```

- ver1. 직접 정의한 maybe 모나드

```hs
return :: a -> Maybe a
return x  = Just x

(>>=)  :: Maybe a -> (a -> Maybe b) -> Maybe b
m >>= g = case m of
             Nothing -> Nothing
             Just x  -> g x
```

- ver2. 모나드 클래스로 생성한 maybe 모나드

```hs
instance Monad Maybe where
    Nothing  >>= f = Nothing
    (Just x) >>= f = f x
    return         = Just

```
