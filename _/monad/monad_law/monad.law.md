#### monad law

```hs
m >>= return ==== m -- right unit
(return x) >>= f ==== f x -- left unit
(m >>= f) >>= g ==== m >>= (\x -> f x >>= g) -- associativity
```

#### monad law 활용

- right unit

```hs
maternalGrandfather p = do
        mom <- mother p
        gf  <- father mom
        return gf

-- right unit 법칙으로 다음과 같다
maternalGrandfather p = do
        mom  <- mother p
        father mom
```

- bind

```hs
bothGrandfathers p =
   (father p >>= father) >>=
       (\gf1 -> (mother p >>= father) >>=
           (\gf2 -> return (gf1,gf2) ))

-- right unit 법칙으로 다음과 같다
(m >> n) >> o  =  m >> (n >> o)
```

- monadic 합성

```hs
(f >=> g) >=> h  =  f >=> (g >=> h)

-- (>=>) 정의
(>=>) :: Monad m => (a -> m b) -> (b -> m c) -> a -> m c
f >=> g = \x -> f x >>= g

```
