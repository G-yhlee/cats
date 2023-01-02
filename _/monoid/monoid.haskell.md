```hs
Prelude> :info Monoid

type Monoid :: * -> Constraint
class Semigroup a => Monoid a where
  mempty :: a
  mappend :: a -> a -> a
  mconcat :: [a] -> a -- 필수 아님
```
