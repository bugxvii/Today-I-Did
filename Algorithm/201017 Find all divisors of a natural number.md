tags: #algorithm #divisor #math #english 

## Linear (naive) approach

Iterate all numbers from `1` to `n` and print it if a number divides `n`.

```cpp
#define ll long long;

int main(){
  ll n;
  cin >> n;
  for (ll i = 1; i <= n; ++i) {
    if (n%i == 0) {
      cout << i << endl;
    }
  }

  return 0;
}
```

Time Complexity: **O(N)**

## Improved algorithm

Suppose that `n = 50`. Divisors are in pairs

```
(1, 50)
(2, 25)
(5, 10)
```

So it's sufficient to iterate only upto `sqrt(n)` or `i*i <= n`.

And as you can see from the pairs above, numbers are printed in zig-zag fashion. 
To print them in sorted order, we save the latter number in a separate set (`50, 25, 10`). 
And print them in reversed order (`10, 25 50`).

Or use `set` which orders the element in increasing order by default.

```cpp
#define ll long long;

int main(){
  set<ll> s;
  ll n;
  cin >> n;

  for (ll x=1; x*x <= n; ++x) {
    if (n%x != 0) continue;
    s.insert(x);
    s.insert(n/x);
  }

  for (ll x : s) cout << x << endl;

  return 0;
}
```

Time Complexity: **O(sqrt(N))**

## Reference
- [Find all divisors of a natural number](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)