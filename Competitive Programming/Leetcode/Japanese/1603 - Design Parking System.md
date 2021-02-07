tags: #leetcode #easy #ruby #japanese #design

<hr />

[1603. Design Parking System](https://leetcode.com/problems/design-parking-system/)

```rb
# Runtime: 88 ms, faster than 74.36%
# Memory Usage: 210.5 MB, less than 6.41%
#
# Your ParkingSystem object will be instantiated and called as such:
# obj = ParkingSystem.new(big, medium, small)
# param_1 = obj.add_car(car_type)
class ParkingSystem
  attr_accessor :cnt, :cntCapacity

=begin
    :type big: Integer
    :type medium: Integer
    :type small: Integer
=end
  def initialize(big, medium, small)
    @cntCapacity = [big, medium, small]
    @cnt = [0, 0, 0]
  end

=begin
    :type car_type: Integer
    :rtype: Boolean
=end
  def add_car(car_type)
    if @cnt[car_type-1] >= @cntCapacity[car_type-1]
      return false
    else
      @cnt[car_type-1] += 1
      return true
    end
  end
end
```