#### maybe in typescript

```ts
type Maybe<A> = A | null;

function pure<A>(value: A): Maybe<A> {
  return value;
}

function compose<A, B, C>(
  f: (a: A) => Maybe<B>,
  g: (a: B) => Maybe<C>
): (a: A) => Maybe<C> {
  return (a: A): Maybe<C> => {
    const ma = f(a);

    if (ma === null) return null;
    else g(ma);
  };
}
```
