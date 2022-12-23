#### monad in cats

- monad is a monoid in the category of endofunctors.
- endofunctor is a functor mapping a category to itself

#### 두개의 결합기를 가지는 functor = monad

```hs
fmap   :: (a -> b) -> M a -> M b  -- functor

return :: a -> M a
join   :: M (M a) -> M a
```
