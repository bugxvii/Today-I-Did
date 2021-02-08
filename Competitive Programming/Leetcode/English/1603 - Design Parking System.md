tags: #leetcode #easy #cpp #english #design

<hr />

[1603. Design Parking System](https://leetcode.com/problems/design-parking-system/)

```cpp
/**
 * Your ParkingSystem object will be instantiated and called as such:
 * ParkingSystem* obj = new ParkingSystem(big, medium, small);
 * bool param_1 = obj->addCar(carType);
 *
 * Runtime: 84 ms, faster than 90.67%
 * Memory Usage: 33.5 MB, less than 7.82%
 */
class ParkingSystem {
  private:
    int carCapacity[3];
    int cnt[3];
  public:
    ParkingSystem(int big, int medium, int small) {
      carCapacity[0] = big;
      carCapacity[1] = medium;
      carCapacity[2] = small;

      cnt[0] = cnt[1] = cnt[2] = 0;
    }

    bool addCar(int carType) {
      return carCapacity[carType-1] > (cnt[carType-1])++;
    }
};
```