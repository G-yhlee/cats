#### monad

- 모나드는 functor이자 applicative 이다.
- 따라서, 모나드에서도 fmap, pure, <\*> 을 사용 할수있다.
- monad 인스턴스를 작성하려면 functor 와 applicative 인스턴스도 작성해야한다

```hs
class Monad m where
    (>>=)  :: m a -> (a -> m b) -> m b -- bind
    return :: a -> m a -- return
    ------------------------------------
    (>>)   :: m a -> m b -> m b -- then
    fail   :: String -> m a -- fail
```

#### applicative

```hs
(*>) :: Applicative f => f a -> f b -> f b
(>>) :: Monad m => m a -> m b -> m b

pure :: Applicative f => a -> f a
return :: Monad m => a -> m a
```
