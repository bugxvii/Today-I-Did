tags: #leetcode #easy #JavaScript #korean #design

<hr />

[1603. Design Parking System](https://leetcode.com/problems/design-parking-system/)

```js
/**
 * Runtime: 156 ms, faster than 37.73%
 * Memory Usage: 46.8 MB, less than 20.10%
 */

let cntCapacity;
let cnt;

/**
 * @param {number} big
 * @param {number} medium
 * @param {number} small
 */
var ParkingSystem = function(big, medium, small) {
  cntCapacity = [big, medium, small];
  cnt = [0, 0, 0];
};

/** 
 * @param {number} carType
 * @return {boolean}
 */
ParkingSystem.prototype.addCar = function(carType) {
  if (cntCapacity[carType-1] == cnt[carType-1]) return false;
  else {
    cnt[carType-1] += 1;
    return true;
  }
};

/** 
 * Your ParkingSystem object will be instantiated and called as such:
 * var obj = new ParkingSystem(big, medium, small)
 * var param_1 = obj.addCar(carType)
 */
```

[[Competitive Programming/Leetcode/English/1603 - Design Parking System | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1603 - Design Parking System | Ruby solution]]