#### monad

```ts
type Pure = <A>(a: A) => M<A>;
type Compose = <A, B, C>(
  f: (a: A) => M<B>,
  g: (a: B) => M<C>
) => (a: A) => M<C>;
```
