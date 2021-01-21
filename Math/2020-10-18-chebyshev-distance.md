tags: #math #chebyshev
related:  [[2020-10-18-euclidean-distance | Euclidean Distance]] | [[2020-10-18-manhattan-distance | Manhattan Distance]]

<hr />

## Chebyshev Distance

Also known as the *chessboard distance* or *maximum value distance*, finds the greatest distance between two vectors in a vector space.

$$d(x, y) = max{ (\ |\ {f(x_i,\  y_i)\ |} \ ),\    1 \le i \le n \quad }$$

## Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int chebyshevDistance(vector<int> x, vector<int> y)
{
  int chebyshev = 0;
  const int SIZE = x.size();

  for (int i=0; i<SIZE; ++i) 
  {
    int v = abs(x[i] - y[i]); 
    chebyshev = (v > chebyshev) ? v : chebyshev;
  }

  return chebyshev;
}

int main()
{
  vector<int> x {-1, 2, 3};
  vector<int> y {4, 0, -3};
  cout << chebyshevDistance(x, y) << endl;

  return 0;
}
```

## Reference
- [Chebyshev Distance](https://en.wikipedia.org/wiki/Chebyshev_distance)
- Image source: https://iq.opengenus.org/euclidean-vs-manhattan-vs-chebyshev-distance/