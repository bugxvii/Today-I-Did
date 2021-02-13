tags: #ps #MacOS #english

<hr />

## <bits/stdc++.h>
Seems like Mac does not come with `bits/stdc++.h`. So I added it manually.

1.  open your terminal and move to `/usr/local/library`
2. create and open  `bits/stdc++.h` with your favorite editor.
3.  copy the following `stdc++.h` ([libstdc++](https://gcc.gnu.org/onlinedocs/gcc-4.6.2/libstdc++/api/a01040_source.html))
    
    ```c
    // C
    #ifndef _GLIBCXX_NO_ASSERT
    #include <cassert>
    #endif
    #include <cctype>
    #include <cerrno>
    #include <cfloat>
    #include <ciso646>
    #include <climits>
    #include <clocale>
    #include <cmath>
    #include <csetjmp>
    #include <csignal>
    #include <cstdarg>
    #include <cstddef>
    #include <cstdio>
    #include <cstdlib>
    #include <cstring>
    #include <ctime>
    
    #ifdef __GXX_EXPERIMENTAL_CXX0X__
    #include <ccomplex>
    #include <cfenv>
    #include <cinttypes>
    #include <cstdbool>
    #include <cstdint>
    #include <ctgmath>
    #include <cwchar>
    #include <cwctype>
    #endif
    
    // C++
    #include <algorithm>
    #include <bitset>
    #include <complex>
    #include <deque>
    #include <exception>
    #include <fstream>
    #include <functional>
    #include <iomanip>
    #include <ios>
    #include <iosfwd>
    #include <iostream>
    #include <istream>
    #include <iterator>
    #include <limits>
    #include <list>
    #include <locale>
    #include <map>
    #include <memory>
    #include <new>
    #include <numeric>
    #include <ostream>
    #include <queue>
    #include <set>
    #include <sstream>
    #include <stack>
    #include <stdexcept>
    #include <streambuf>
    #include <string>
    #include <typeinfo>
    #include <utility>
    #include <valarray>
    #include <vector>
    
    #ifdef __GXX_EXPERIMENTAL_CXX0X__
    #include <array>
    #include <atomic>
    #include <chrono>
    #include <condition_variable>
    #include <forward_list>
    #include <future>
    #include <initializer_list>
    #include <mutex>
    #include <random>
    #include <ratio>
    #include <regex>
    #include <system_error>
    #include <thread>
    #include <tuple>
    #include <typeindex>
    #include <type_traits>
    #include <unordered_map>
    #include <unordered_set>
    #endif
    ```
    
4.  Save it and compile your code.

## Reference
- [https://qiita.com/K\_Lightning/items/55821df2fe850f12659d](https://qiita.com/K_Lightning/items/55821df2fe850f12659d)