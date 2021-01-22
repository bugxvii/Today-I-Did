tags: #math #euclidean
related:  [[201018 Chebyshev Distance | Chebyshev Distance]] | [[201018 Manhattan Distance | Manhattan Distance]]

<hr />

## Euclidean Distance
Also known as the *L2 distance*.

The euclidean distance finds the distance between two points. 

Suppose that the bottom-left point and upper-right point is `(x1, y1)` and `(x2, y2)` respectively.
The euclidean distance of two points can be calculated as `sqrt{ (x1 - x2)^2 + (y1 - y2)^2 }`.

You can think of the *Pythagorean Theorem*, `a^2 + b^2 = c^2`, where you're solving for the hypotenuse (`c`).

So the final form of the euclidean distance formula looks like this:

$$d_2(x, y) = ||x - y||_2 = \sqrt{\sum^{n}_{i=1} (a_i-b_i)^{2}}$$

## Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

double euclideanDistance(vector<int> x, vector<int> y)
{
  int distance = 0;
  const int SIZE = x.size();

  for (int i=0; i<SIZE; ++i) 
  {
    int t = x[i] - y[i];
    distance += (t * t);
  }

  return sqrt(distance);
}

int main()
{
  vector<int> x {-1, 2, 3};
  vector<int> y {4, 0, -3};
  cout << euclideanDistance(x, y) << endl;

  return 0;
}
```

## Reference
- [Euclidean Distance](https://www.sciencedirect.com/topics/mathematics/euclidean-distance)