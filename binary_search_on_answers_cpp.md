# Binary Search on Answers — Classic LeetCode C++ Notes

## What is "Binary Search on Answers"?
Instead of searching for an element's *index*, you binary search on the **answer value itself**.

**Template:**
```cpp
long long lo = min_possible, hi = max_possible;
while (lo < hi) {
    long long mid = lo + (hi - lo) / 2;
    if (canAchieve(mid))  // feasibility check
        hi = mid;         // mid works, try smaller (for minimization)
    else
        lo = mid + 1;     // mid too small, try larger
}
return lo;
```
For **maximization** problems, flip: if `canAchieve(mid)` → `lo = mid + 1`, else `hi = mid - 1`.

**Key insight:** The feasibility function must be **monotonic** — if answer X works, then all values > X also work (for minimization), creating a clean binary search space.

---

## 📋 Problem Index

| # | Problem | Pattern | Link |
|---|---------|---------|------|
| 378 | [Kth Smallest in Sorted Matrix](#378-kth-smallest-element-in-a-sorted-matrix) | BS on value | [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix) |
| 786 | [K-th Smallest Prime Fraction](#786-k-th-smallest-prime-fraction) | BS on value | [LeetCode](https://leetcode.com/problems/k-th-smallest-prime-fraction) |
| 875 | [Koko Eating Bananas](#875-koko-eating-bananas) | Minimize speed | [LeetCode](https://leetcode.com/problems/koko-eating-bananas) |
| 1011 | [Capacity To Ship Packages Within D Days](#1011-capacity-to-ship-packages-within-d-days) | Minimize capacity | [LeetCode](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days) |
| 1283 | [Find the Smallest Divisor Given a Threshold](#1283-find-the-smallest-divisor-given-a-threshold) | Minimize divisor | [LeetCode](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold) |
| 1300 | [Sum of Mutated Array Closest to Target](#1300-sum-of-mutated-array-closest-to-target) | BS on mutation value | [LeetCode](https://leetcode.com/problems/sum-of-mutated-array-closest-to-target) |
| 1482 | [Minimum Days to Make m Bouquets](#1482-minimum-number-of-days-to-make-m-bouquets) | Minimize days | [LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets) |
| 1552 | [Magnetic Force Between Two Balls](#1552-magnetic-force-between-two-balls) | Maximize minimum | [LeetCode](https://leetcode.com/problems/magnetic-force-between-two-balls) |
| 1760 | [Minimum Limit of Balls in a Bag](#1760-minimum-limit-of-balls-in-a-bag) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag) |
| 1802 | [Maximum Value at a Given Index in a Bounded Array](#1802-maximum-value-at-a-given-index-in-a-bounded-array) | Maximize value | [LeetCode](https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array) |
| 1870 | [Minimum Speed to Arrive on Time](#1870-minimum-speed-to-arrive-on-time) | Minimize speed | [LeetCode](https://leetcode.com/problems/minimum-speed-to-arrive-on-time) |
| 1891 | [Cutting Ribbons](#1891-cutting-ribbons) | Maximize length | [LeetCode](https://leetcode.com/problems/cutting-ribbons) |
| 2064 | [Minimized Maximum of Products Distributed](#2064-minimized-maximum-of-products-distributed-to-any-store) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store) |
| 2187 | [Minimum Time to Complete Trips](#2187-minimum-time-to-complete-trips) | Minimize time | [LeetCode](https://leetcode.com/problems/minimum-time-to-complete-trips) |
| 2226 | [Maximum Candies Allocated to K Children](#2226-maximum-candies-allocated-to-k-children) | Maximize candies | [LeetCode](https://leetcode.com/problems/maximum-candies-allocated-to-k-children) |
| 2439 | [Minimize Maximum of Array](#2439-minimize-maximum-of-array) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimize-maximum-of-array) |
| 2498 | [Frog Jump II](#2498-frog-jump-ii) | Maximize minimum | [LeetCode](https://leetcode.com/problems/frog-jump-ii) |
| 2513 | [Minimize the Maximum of Two Arrays](#2513-minimize-the-maximum-of-two-arrays) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimize-the-maximum-of-two-arrays) |
| 2517 | [Maximum Tastiness of Candy Basket](#2517-maximum-tastiness-of-candy-basket) | Maximize minimum | [LeetCode](https://leetcode.com/problems/maximum-tastiness-of-candy-basket) |
| 2560 | [House Robber IV](#2560-house-robber-iv) | Minimize maximum | [LeetCode](https://leetcode.com/problems/house-robber-iv) |
| 2594 | [Minimum Time to Repair Cars](#2594-minimum-time-to-repair-cars) | Minimize time | [LeetCode](https://leetcode.com/problems/minimum-time-to-repair-cars) |
| 2616 | [Minimize the Maximum Difference of Pairs](#2616-minimize-the-maximum-difference-of-pairs) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimize-the-maximum-difference-of-pairs) |
| 2861 | [Maximum Number of Alloys](#2861-maximum-number-of-alloys) | Maximize count | [LeetCode](https://leetcode.com/problems/maximum-number-of-alloys) |
| 3281 | [Maximize Score of Numbers in Ranges](#3281-maximize-score-of-numbers-in-ranges) | Maximize minimum | [LeetCode](https://leetcode.com/problems/maximize-score-of-numbers-in-ranges) |
| 3296 | [Minimum Seconds to Make Mountain Height Zero](#3296-minimum-number-of-seconds-to-make-mountain-height-zero) | Minimize time | [LeetCode](https://leetcode.com/problems/minimum-number-of-seconds-to-make-mountain-height-zero) |
| 3356 | [Zero Array Transformation II](#3356-zero-array-transformation-ii) | Minimize k | [LeetCode](https://leetcode.com/problems/zero-array-transformation-ii) |
| 3419 | [Minimize the Maximum Edge Weight of Graph](#3419-minimize-the-maximum-edge-weight-of-graph) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimize-the-maximum-edge-weight-of-graph) |
| 3453 | [Separate Squares I](#3453-separate-squares-i) | BS on split line | [LeetCode](https://leetcode.com/problems/separate-squares-i) |
| 3613 | [Minimize Maximum Component Cost](#3613-minimize-maximum-component-cost) | Minimize maximum | [LeetCode](https://leetcode.com/problems/minimize-maximum-component-cost) |

---

## 875. Koko Eating Bananas
🔗 [LeetCode](https://leetcode.com/problems/koko-eating-bananas)

**Logic:** Binary search on the eating speed `k` (range: 1 to max pile). For a given speed, check if Koko can finish all piles in `h` hours — each pile takes `ceil(pile/k)` hours. If total hours ≤ h, speed `k` is feasible. We want the *minimum* feasible speed, so shrink `hi` when feasible.

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int lo = 1, hi = *max_element(piles.begin(), piles.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canFinish(piles, mid, h))
                hi = mid;        // mid works, try slower
            else
                lo = mid + 1;    // too slow, need faster
        }
        return lo;
    }

    bool canFinish(vector<int>& piles, int speed, int h) {
        long long hours = 0;
        for (int p : piles)
            hours += (p + speed - 1) / speed;  // ceil(p / speed)
        return hours <= h;
    }
};
```

---

## 1011. Capacity To Ship Packages Within D Days
🔗 [LeetCode](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days)

**Logic:** Binary search on ship capacity (range: max single weight to total sum). For a given capacity, greedily simulate loading: keep adding packages to the current day until the next package would exceed capacity — then start a new day. If days needed ≤ D, capacity is feasible. Minimize the capacity.

```cpp
class Solution {
public:
    int shipWithinDays(vector<int>& weights, int days) {
        int lo = *max_element(weights.begin(), weights.end()); // must carry heaviest
        int hi = accumulate(weights.begin(), weights.end(), 0); // carry all in 1 day
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canShip(weights, mid, days))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canShip(vector<int>& weights, int cap, int days) {
        int daysNeeded = 1, currentLoad = 0;
        for (int w : weights) {
            if (currentLoad + w > cap) {   // can't fit, start new day
                daysNeeded++;
                currentLoad = 0;
            }
            currentLoad += w;
        }
        return daysNeeded <= days;
    }
};
```

---

## 1283. Find the Smallest Divisor Given a Threshold
🔗 [LeetCode](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold)

**Logic:** Binary search on the divisor (range: 1 to max element). For a given divisor, the sum = Σ ceil(num/divisor). Larger divisor → smaller sum (monotonic). Find the smallest divisor where sum ≤ threshold.

```cpp
class Solution {
public:
    int smallestDivisor(vector<int>& nums, int threshold) {
        int lo = 1, hi = *max_element(nums.begin(), nums.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (getSum(nums, mid) <= threshold)
                hi = mid;        // divisor works, try smaller
            else
                lo = mid + 1;
        }
        return lo;
    }

    int getSum(vector<int>& nums, int div) {
        int sum = 0;
        for (int n : nums)
            sum += (n + div - 1) / div;   // ceil(n / div)
        return sum;
    }
};
```

---

## 1300. Sum of Mutated Array Closest to Target
🔗 [LeetCode](https://leetcode.com/problems/sum-of-mutated-array-closest-to-target)

**Logic:** Binary search on the mutation value `v` (range: 0 to max element). Each element becomes min(element, v). The sum is monotonically increasing with v. Find the v that makes sum closest to target. Check both `v` and `v-1` at convergence since we need closest, not exact.

```cpp
class Solution {
public:
    int findBestValue(vector<int>& arr, int target) {
        sort(arr.begin(), arr.end());
        int lo = 0, hi = arr.back();
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (getSum(arr, mid) < target)
                lo = mid + 1;
            else
                hi = mid;
        }
        // check lo and lo-1: pick whichever sum is closer to target
        int s1 = getSum(arr, lo - 1), s2 = getSum(arr, lo);
        return abs(s1 - target) <= abs(s2 - target) ? lo - 1 : lo;
    }

    int getSum(vector<int>& arr, int val) {
        int sum = 0;
        for (int x : arr)
            sum += min(x, val);   // cap each element at val
        return sum;
    }
};
```

---

## 1482. Minimum Number of Days to Make m Bouquets
🔗 [LeetCode](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets)

**Logic:** Binary search on the day (range: 1 to max bloom day). On a given day, a flower has bloomed if `bloomDay[i] <= day`. Count how many bouquets of k consecutive bloomed flowers we can make by scanning left to right. If bouquets ≥ m, this day is feasible. Minimize the day.

```cpp
class Solution {
public:
    int minDays(vector<int>& bloomDay, int m, int k) {
        long long total = (long long)m * k;
        if (total > bloomDay.size()) return -1;  // impossible

        int lo = 1, hi = *max_element(bloomDay.begin(), bloomDay.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canMake(bloomDay, mid, m, k))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canMake(vector<int>& bd, int day, int m, int k) {
        int bouquets = 0, consecutive = 0;
        for (int b : bd) {
            if (b <= day) {
                consecutive++;
                if (consecutive == k) {   // completed one bouquet
                    bouquets++;
                    consecutive = 0;
                }
            } else {
                consecutive = 0;          // chain broken
            }
        }
        return bouquets >= m;
    }
};
```

---

## 1552. Magnetic Force Between Two Balls
🔗 [LeetCode](https://leetcode.com/problems/magnetic-force-between-two-balls)

**Logic:** Classic "maximize the minimum distance." Binary search on the minimum gap between balls (range: 1 to (max-min)/(m-1)). For a given gap, greedily place balls: always place the next ball at the earliest position that is at least `gap` away from the last placed ball. If we can place all m balls, this gap is feasible. Maximize it.

```cpp
class Solution {
public:
    int maxDistance(vector<int>& position, int m) {
        sort(position.begin(), position.end());
        int lo = 1, hi = (position.back() - position[0]) / (m - 1);
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;  // upper mid for maximization
            if (canPlace(position, mid, m))
                lo = mid;        // gap works, try larger
            else
                hi = mid - 1;
        }
        return lo;
    }

    bool canPlace(vector<int>& pos, int gap, int m) {
        int count = 1, last = pos[0];   // place first ball at pos[0]
        for (int i = 1; i < pos.size(); i++) {
            if (pos[i] - last >= gap) { // far enough from last placed ball
                count++;
                last = pos[i];
            }
        }
        return count >= m;
    }
};
```

---

## 1760. Minimum Limit of Balls in a Bag
🔗 [LeetCode](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag)

**Logic:** Binary search on the answer — the maximum bag size allowed. For a given max size, each bag of size `n` needs `ceil(n/maxSize) - 1` splits to bring all sub-bags to ≤ maxSize. Total splits needed must be ≤ maxOperations. Minimize the max size.

```cpp
class Solution {
public:
    int minimumSize(vector<int>& nums, int maxOperations) {
        int lo = 1, hi = *max_element(nums.begin(), nums.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canDo(nums, mid, maxOperations))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canDo(vector<int>& nums, int maxSize, int ops) {
        int splits = 0;
        for (int n : nums)
            splits += (n - 1) / maxSize;   // ceil(n/maxSize) - 1 splits needed
        return splits <= ops;
    }
};
```

---

## 1802. Maximum Value at a Given Index in a Bounded Array
🔗 [LeetCode](https://leetcode.com/problems/maximum-value-at-a-given-index-in-a-bounded-array)

**Logic:** Binary search on the value at index `index`. For a given value v, the minimum possible array sum is achieved by placing values that decrease by 1 as we move away from index (like a mountain). Compute the minimum sum achievable with `nums[index] = v` using the arithmetic series formula. If that sum ≤ maxSum, v is feasible. Maximize v.

```cpp
class Solution {
public:
    int maxValue(int n, int index, int maxSum) {
        int lo = 1, hi = maxSum;
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;   // upper mid for maximization
            if (minSum(n, index, mid) <= maxSum)
                lo = mid;
            else
                hi = mid - 1;
        }
        return lo;
    }

    // minimum sum of array if nums[index] = val (values drop by 1 each step, floor at 1)
    long long minSum(int n, int index, long long val) {
        return sumSide(val, index) + sumSide(val, n - 1 - index) - val;
    }

    // sum of a side of length `len` starting at val, decreasing by 1, min 1
    long long sumSide(long long val, long long len) {
        if (val >= len)
            // full arithmetic series: val + (val-1) + ... + (val-len+1)
            return (val + val - len + 1) * len / 2;
        else
            // series hits 1 before reaching the end: val + ... + 1 + 1 + 1
            return val * (val + 1) / 2 + (len - val);
    }
};
```

---

## 1870. Minimum Speed to Arrive on Time
🔗 [LeetCode](https://leetcode.com/problems/minimum-speed-to-arrive-on-time)

**Logic:** Binary search on speed (range: 1 to 10^7). For all trains except the last, you must wait for the next whole hour — so time per train = `ceil(dist/speed)`. For the last train, fractional time is fine. Sum all times and check if ≤ hour. Minimize speed.

```cpp
class Solution {
public:
    int minSpeedOnTime(vector<int>& dist, double hour) {
        int n = dist.size();
        // need at least n-1 hours for first n-1 trains (each takes ≥1 full hour)
        if (hour <= n - 1) return -1;

        int lo = 1, hi = 1e7;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canArrive(dist, mid, hour))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canArrive(vector<int>& dist, int speed, double hour) {
        double time = 0;
        for (int i = 0; i < dist.size() - 1; i++)
            time += ceil((double)dist[i] / speed);  // must wait for full hour
        time += (double)dist.back() / speed;         // last train: exact time
        return time <= hour;
    }
};
```

---

## 1891. Cutting Ribbons
🔗 [LeetCode](https://leetcode.com/problems/cutting-ribbons)

**Logic:** Binary search on ribbon length (range: 1 to max ribbon). For a given length, count how many pieces of that length we can cut total: for each ribbon, `floor(ribbon/length)` pieces. If total count ≥ k, this length is feasible. Maximize length.

```cpp
class Solution {
public:
    int maxLength(vector<int>& ribbons, int k) {
        int lo = 1, hi = *max_element(ribbons.begin(), ribbons.end());
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;   // upper mid for maximization
            if (canCut(ribbons, mid, k))
                lo = mid;
            else
                hi = mid - 1;
        }
        // check if even lo=1 gives k pieces
        return canCut(ribbons, lo, k) ? lo : 0;
    }

    bool canCut(vector<int>& ribbons, int len, int k) {
        int count = 0;
        for (int r : ribbons)
            count += r / len;    // how many pieces of 'len' from this ribbon
        return count >= k;
    }
};
```

---

## 2064. Minimized Maximum of Products Distributed to Any Store
🔗 [LeetCode](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store)

**Logic:** Binary search on the answer — the maximum products any single store receives. For a given max `x`, product type with `q` quantities needs `ceil(q/x)` stores. If total stores needed ≤ n, this max is feasible. Minimize x.

```cpp
class Solution {
public:
    int minimizedMaximum(int n, vector<int>& quantities) {
        int lo = 1, hi = *max_element(quantities.begin(), quantities.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canDistribute(quantities, mid, n))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canDistribute(vector<int>& q, int maxPerStore, int n) {
        int stores = 0;
        for (int qty : q)
            stores += (qty + maxPerStore - 1) / maxPerStore;  // ceil(qty/maxPerStore)
        return stores <= n;
    }
};
```

---

## 2187. Minimum Time to Complete Trips
🔗 [LeetCode](https://leetcode.com/problems/minimum-time-to-complete-trips)

**Logic:** Binary search on time (range: 1 to min_time * totalTrips). In a given time `t`, bus i completes `floor(t / time[i])` trips. Sum all trips across all buses and check if ≥ totalTrips. Minimize t.

```cpp
class Solution {
public:
    long long minimumTime(vector<int>& time, int totalTrips) {
        long long lo = 1;
        long long hi = (long long)*min_element(time.begin(), time.end()) * totalTrips;
        while (lo < hi) {
            long long mid = lo + (hi - lo) / 2;
            if (tripsCompleted(time, mid) >= totalTrips)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    long long tripsCompleted(vector<int>& time, long long t) {
        long long trips = 0;
        for (int bus : time)
            trips += t / bus;    // bus completes floor(t/bus) trips in time t
        return trips;
    }
};
```

---

## 2226. Maximum Candies Allocated to K Children
🔗 [LeetCode](https://leetcode.com/problems/maximum-candies-allocated-to-k-children)

**Logic:** Binary search on candies per child (range: 1 to max pile). For a given amount, pile of size `p` can serve `floor(p/amount)` children. Sum up children servable and check if ≥ k. Maximize the amount.

```cpp
class Solution {
public:
    int maximumCandies(vector<int>& candies, long long k) {
        long long lo = 1, hi = *max_element(candies.begin(), candies.end());
        while (lo < hi) {
            long long mid = lo + (hi - lo + 1) / 2;  // upper mid for maximization
            if (canAllocate(candies, mid, k))
                lo = mid;
            else
                hi = mid - 1;
        }
        return canAllocate(candies, lo, k) ? lo : 0;
    }

    bool canAllocate(vector<int>& candies, long long amount, long long k) {
        long long children = 0;
        for (int c : candies)
            children += c / amount;   // how many children this pile serves
        return children >= k;
    }
};
```

---

## 2439. Minimize Maximum of Array
🔗 [LeetCode](https://leetcode.com/problems/minimize-maximum-of-array)

**Logic:** Binary search on the answer — the maximum value in the final array. For a given max `m`, check if the array can be reduced such that no element exceeds `m`: process left to right, carrying excess forward (you can only move value leftward). If the running excess ever makes it impossible, return false.

```cpp
class Solution {
public:
    int minimizeArrayValue(vector<int>& nums) {
        long long lo = *min_element(nums.begin(), nums.end());
        long long hi = *max_element(nums.begin(), nums.end());
        while (lo < hi) {
            long long mid = lo + (hi - lo) / 2;
            if (canAchieve(nums, mid))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canAchieve(vector<int>& nums, long long maxVal) {
        long long carry = 0;  // excess that needs to be absorbed by earlier elements
        for (int i = nums.size() - 1; i >= 0; i--) {
            long long total = nums[i] + carry;
            if (total > maxVal * (i + 1))  // even spreading over [0..i] exceeds maxVal
                return false;
            carry = max(0LL, total - maxVal);  // leftover pushed to earlier
        }
        return true;
    }
};
```

---

## 2498. Frog Jump II
🔗 [LeetCode](https://leetcode.com/problems/frog-jump-ii)

**Logic:** Binary search on the maximum jump length. For a given max jump `d`, check if the frog can go from stone[0] to stone[n-1] and back such that no jump exceeds `d`. Key insight: on the optimal round trip, every stone is visited exactly once total, and the worst jump is determined by taking every other stone. So the answer is simply the max gap between stones[i] and stones[i+2] (alternating stones pattern) — but we binary search to confirm.

```cpp
class Solution {
public:
    int maxJump(vector<int>& stones) {
        // Observation: optimal is to take alternating stones on each leg
        // → answer = max(stones[i+2] - stones[i]) for all i, also check adjacent
        int ans = stones[1] - stones[0]; // must always jump first and last
        for (int i = 2; i < stones.size(); i++)
            ans = max(ans, stones[i] - stones[i - 2]); // skip every other stone
        return ans;
    }
    // Binary search version for understanding the pattern:
    // lo=1, hi=stones.back()-stones[0]
    // canAchieve(d): check if we can cover all stones with max gap d in both directions
};
```

---

## 2513. Minimize the Maximum of Two Arrays
🔗 [LeetCode](https://leetcode.com/problems/minimize-the-maximum-of-two-arrays)

**Logic:** Binary search on the answer — the maximum value used. For a given max `m`, count how many values ≤ m are available for array1 (not divisible by divisor2), for array2 (not divisible by divisor1), and for either (not divisible by LCM). Use inclusion-exclusion to see if we can fill both arrays. Uses LCM arithmetic.

```cpp
class Solution {
public:
    int minimizeSet(int d1, int d2, int u1, int u2) {
        long long lcm = (long long)d1 / __gcd(d1, d2) * d2;
        long long lo = 1, hi = 2e10;
        while (lo < hi) {
            long long mid = lo + (hi - lo) / 2;
            // available exclusively for arr1 (not mult of d2), for arr2, for both
            long long both = mid - mid / lcm;
            long long for1 = mid - mid / d2;   // not divisible by d2
            long long for2 = mid - mid / d1;   // not divisible by d1
            if (for1 >= u1 && for2 >= u2 && both >= u1 + u2)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }
};
```

---

## 2517. Maximum Tastiness of Candy Basket
🔗 [LeetCode](https://leetcode.com/problems/maximum-tastiness-of-candy-basket)

**Logic:** "Maximize minimum difference" — classic BS on answers. Binary search on the minimum price gap (tastiness). Sort the prices. For a given gap, greedily pick candies: take the first candy, then only pick the next one if its price differs by at least `gap`. If we can pick k candies this way, gap is feasible. Maximize it.

```cpp
class Solution {
public:
    int maximumTastiness(vector<int>& price, int k) {
        sort(price.begin(), price.end());
        int lo = 0, hi = price.back() - price[0];
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;   // upper mid for maximization
            if (canPick(price, mid, k))
                lo = mid;
            else
                hi = mid - 1;
        }
        return lo;
    }

    bool canPick(vector<int>& price, int minGap, int k) {
        int count = 1, last = price[0];
        for (int i = 1; i < price.size(); i++) {
            if (price[i] - last >= minGap) {  // gap is large enough
                count++;
                last = price[i];
            }
        }
        return count >= k;
    }
};
```

---

## 2560. House Robber IV
🔗 [LeetCode](https://leetcode.com/problems/house-robber-iv)

**Logic:** Binary search on the "capability" — the maximum value robbed from any single house. For a given capability `cap`, check if we can rob at least `k` houses such that no two are adjacent and each house's value ≤ cap. Greedy: iterate and greedily rob whenever the house value ≤ cap (skip adjacent). Minimize cap.

```cpp
class Solution {
public:
    int minCapability(vector<int>& nums, int k) {
        int lo = *min_element(nums.begin(), nums.end());
        int hi = *max_element(nums.begin(), nums.end());
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canRob(nums, mid, k))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canRob(vector<int>& nums, int cap, int k) {
        int count = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] <= cap) {   // can rob this house
                count++;
                i++;                // skip adjacent house
            }
        }
        return count >= k;
    }
};
```

---

## 2594. Minimum Time to Repair Cars
🔗 [LeetCode](https://leetcode.com/problems/minimum-time-to-repair-cars)

**Logic:** Binary search on total time. Mechanic with rank `r` repairs `n` cars in time `r * n²`. So in time `t`, mechanic r can repair `floor(sqrt(t/r))` cars. Sum across all mechanics and check if ≥ cars. Minimize t.

```cpp
class Solution {
public:
    long long repairCars(vector<int>& ranks, int cars) {
        long long lo = 1, hi = (long long)*min_element(ranks.begin(), ranks.end()) * cars * cars;
        while (lo < hi) {
            long long mid = lo + (hi - lo) / 2;
            if (carsRepaired(ranks, mid) >= cars)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    long long carsRepaired(vector<int>& ranks, long long t) {
        long long total = 0;
        for (int r : ranks)
            total += (long long)sqrt(t / r);  // mechanic r repairs floor(sqrt(t/r)) cars
        return total;
    }
};
```

---

## 2616. Minimize the Maximum Difference of Pairs
🔗 [LeetCode](https://leetcode.com/problems/minimize-the-maximum-difference-of-pairs)

**Logic:** Binary search on the max allowed difference. Sort the array — minimum differences always come from adjacent elements. For a given max diff `d`, greedily pair adjacent elements: if `nums[i+1] - nums[i] ≤ d`, form a pair and skip both. Count pairs and check if ≥ p. Minimize d.

```cpp
class Solution {
public:
    int minimizeMax(vector<int>& nums, int p) {
        sort(nums.begin(), nums.end());
        int lo = 0, hi = nums.back() - nums[0];
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (countPairs(nums, mid) >= p)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    int countPairs(vector<int>& nums, int maxDiff) {
        int pairs = 0;
        for (int i = 0; i + 1 < nums.size(); i++) {
            if (nums[i + 1] - nums[i] <= maxDiff) {
                pairs++;
                i++;    // skip both elements of this pair
            }
        }
        return pairs;
    }
};
```

---

## 2861. Maximum Number of Alloys
🔗 [LeetCode](https://leetcode.com/problems/maximum-number-of-alloys)

**Logic:** Binary search on the number of alloys produced. For each machine, check if it can produce `mid` alloys: cost = Σ max(0, mid*composition[k] - stock[k]) * cost[k]. If any machine can do it within budget, mid is feasible. Maximize the alloy count.

```cpp
class Solution {
public:
    int maxNumberOfAlloys(int n, int k, int budget,
                          vector<vector<int>>& composition,
                          vector<int>& stock, vector<int>& cost) {
        int lo = 0, hi = 1e8;
        while (lo < hi) {
            long long mid = lo + (hi - lo + 1) / 2;
            if (canProduce(mid, n, budget, composition, stock, cost))
                lo = mid;
            else
                hi = mid - 1;
        }
        return lo;
    }

    bool canProduce(long long alloys, int n, long long budget,
                    vector<vector<int>>& comp, vector<int>& stock, vector<int>& cost) {
        for (int m = 0; m < comp.size(); m++) {   // try each machine
            long long totalCost = 0;
            bool ok = true;
            for (int j = 0; j < n; j++) {
                long long need = alloys * comp[m][j];
                if (need > stock[j])
                    totalCost += (need - stock[j]) * cost[j];  // buy deficit
                if (totalCost > budget) { ok = false; break; }
            }
            if (ok) return true;   // at least one machine can do it
        }
        return false;
    }
};
```

---

## 3281. Maximize Score of Numbers in Ranges
🔗 [LeetCode](https://leetcode.com/problems/maximize-score-of-numbers-in-ranges)

**Logic:** Each range is [start[i], start[i]+d]. You pick one number per range. Score = minimum difference between any two picked numbers. Binary search on the score (minimum gap). Sort ranges by start. Greedily assign the smallest valid number in each range (at least `prev + gap`). If feasible for all ranges, gap is achievable. Maximize.

```cpp
class Solution {
public:
    int maxScore(vector<int>& start, int d) {
        int n = start.size();
        vector<int> s = start;
        sort(s.begin(), s.end());
        int lo = 0, hi = s.back() + d - s[0];
        while (lo < hi) {
            int mid = lo + (hi - lo + 1) / 2;
            if (canAchieve(s, d, mid, n))
                lo = mid;
            else
                hi = mid - 1;
        }
        return lo;
    }

    bool canAchieve(vector<int>& s, int d, int gap, int n) {
        long long prev = s[0];   // pick smallest in first range
        for (int i = 1; i < n; i++) {
            long long next = max((long long)s[i], prev + gap);  // earliest valid pick
            if (next > s[i] + d) return false;   // exceeds range
            prev = next;
        }
        return true;
    }
};
```

---

## 3296. Minimum Number of Seconds to Make Mountain Height Zero
🔗 [LeetCode](https://leetcode.com/problems/minimum-number-of-seconds-to-make-mountain-height-zero)

**Logic:** Worker i needs `time[i] * (1+2+...+h) = time[i] * h*(h+1)/2` seconds to reduce mountain by h. Binary search on total seconds. For a given time `t`, each worker can reduce height by the largest `h` where `time[i]*h*(h+1)/2 ≤ t`. Sum reductions and check ≥ mountainHeight. Minimize t.

```cpp
class Solution {
public:
    long long minNumberOfSeconds(int mountainHeight, vector<int>& workerTimes) {
        long long lo = 0;
        long long hi = (long long)*max_element(workerTimes.begin(), workerTimes.end())
                       * mountainHeight * (mountainHeight + 1) / 2;
        while (lo < hi) {
            long long mid = lo + (hi - lo) / 2;
            if (canReduce(workerTimes, mid, mountainHeight))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canReduce(vector<int>& times, long long t, int target) {
        long long totalReduction = 0;
        for (int wt : times) {
            // find max h such that wt * h*(h+1)/2 <= t
            // solve h*(h+1) <= 2t/wt using binary search or formula
            long long h = (long long)((-1 + sqrt(1 + 8.0 * t / wt)) / 2);
            totalReduction += h;
            if (totalReduction >= target) return true;
        }
        return totalReduction >= target;
    }
};
```

---

## 3356. Zero Array Transformation II
🔗 [LeetCode](https://leetcode.com/problems/zero-array-transformation-ii)

**Logic:** Binary search on k — the number of queries used. For a given k, use the first k queries. Apply them via difference array (range decrement). Check if every element in nums can be reduced to 0 (i.e., the cumulative decrement at each index ≥ nums[i]). Minimize k.

```cpp
class Solution {
public:
    int minZeroArray(vector<int>& nums, vector<vector<int>>& queries) {
        int n = nums.size(), lo = 0, hi = queries.size();
        if (!canZero(nums, queries, hi)) return -1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (canZero(nums, queries, mid))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool canZero(vector<int>& nums, vector<vector<int>>& queries, int k) {
        int n = nums.size();
        vector<long long> diff(n + 1, 0);
        for (int i = 0; i < k; i++) {
            diff[queries[i][0]] += queries[i][2];         // range add val
            diff[queries[i][1] + 1] -= queries[i][2];
        }
        long long running = 0;
        for (int i = 0; i < n; i++) {
            running += diff[i];
            if (running < nums[i]) return false;          // not enough decrement
        }
        return true;
    }
};
```

---

## 3419. Minimize the Maximum Edge Weight of Graph
🔗 [LeetCode](https://leetcode.com/problems/minimize-the-maximum-edge-weight-of-graph)

**Logic:** Binary search on the maximum edge weight allowed. For a given threshold, include only edges with weight ≤ threshold. Check if the graph remains connected (BFS/DFS from node 0 reaches all n nodes). Minimize the threshold.

```cpp
class Solution {
public:
    int minMaxWeight(int n, vector<vector<int>>& edges, int threshold) {
        // sort edges by weight
        sort(edges.begin(), edges.end(), [](auto& a, auto& b){ return a[2] < b[2]; });
        int lo = 0, hi = edges.back()[2];
        if (!isConnected(n, edges, hi)) return -1;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (isConnected(n, edges, mid))
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    bool isConnected(int n, vector<vector<int>>& edges, int maxW) {
        vector<vector<int>> adj(n);
        for (auto& e : edges) {
            if (e[2] <= maxW) {
                adj[e[0]].push_back(e[1]);
                adj[e[1]].push_back(e[0]);
            }
        }
        vector<bool> visited(n, false);
        queue<int> q;
        q.push(0); visited[0] = true;
        int count = 1;
        while (!q.empty()) {
            int u = q.front(); q.pop();
            for (int v : adj[u]) if (!visited[v]) {
                visited[v] = true; count++; q.push(v);
            }
        }
        return count == n;
    }
};
```

---

## 3453. Separate Squares I
🔗 [LeetCode](https://leetcode.com/problems/separate-squares-i)

**Logic:** Binary search on the y-coordinate of the horizontal line. For a given line y, compute area of squares above and below. If area_below ≥ area_above, line is high enough. Find the exact y where areas balance (may be fractional — use floating point or careful integer math).

```cpp
class Solution {
public:
    double separateSquares(vector<vector<int>>& squares) {
        double lo = 0, hi = 2e9;
        for (int i = 0; i < 100; i++) {   // 100 iterations gives enough precision
            double mid = (lo + hi) / 2;
            if (areaBelow(squares, mid) >= areaAbove(squares, mid))
                hi = mid;
            else
                lo = mid;
        }
        return lo;
    }

    double areaBelow(vector<vector<int>>& sq, double line) {
        double area = 0;
        for (auto& s : sq) {
            double y = s[1], l = s[2];
            double overlap = min((double)(y + l), line) - y;
            if (overlap > 0) area += overlap * l;
        }
        return area;
    }

    double areaAbove(vector<vector<int>>& sq, double line) {
        double area = 0;
        for (auto& s : sq) {
            double y = s[1], l = s[2];
            double overlap = (double)(y + l) - max((double)y, line);
            if (overlap > 0) area += overlap * l;
        }
        return area;
    }
};
```

---

## 378. Kth Smallest Element in a Sorted Matrix
🔗 [LeetCode](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix)

**Logic:** Binary search on the value (range: matrix[0][0] to matrix[n-1][n-1]). For a given value `mid`, count how many elements ≤ mid using the sorted property: start from bottom-left, move right if ≤ mid, move up if > mid. If count ≥ k, mid is too large or exactly right — shrink hi. The answer is always an actual matrix element.

```cpp
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        int lo = matrix[0][0], hi = matrix[n-1][n-1];
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (countLE(matrix, mid, n) >= k)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    int countLE(vector<vector<int>>& matrix, int val, int n) {
        int row = n - 1, col = 0, count = 0;
        while (row >= 0 && col < n) {
            if (matrix[row][col] <= val) {
                count += row + 1;   // all elements in this column up to row are ≤ val
                col++;
            } else {
                row--;              // current element too large, go up
            }
        }
        return count;
    }
};
```

---

## 786. K-th Smallest Prime Fraction
🔗 [LeetCode](https://leetcode.com/problems/k-th-smallest-prime-fraction)

**Logic:** Binary search on the fraction value (range: 0.0 to 1.0). For a given value `mid`, count how many fractions `arr[i]/arr[j]` are ≤ mid. For each numerator i, use two pointers or binary search to find the cutoff j. If count ≥ k, hi = mid. Track the largest fraction ≤ mid seen — that's our answer at convergence.

```cpp
class Solution {
public:
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        int n = arr.size();
        double lo = 0, hi = 1;
        vector<int> result;
        while (hi - lo > 1e-9) {
            double mid = (lo + hi) / 2;
            int count = 0;
            int p = 0, q = 1;            // track the largest fraction ≤ mid
            for (int i = 0; i < n - 1; i++) {
                int j = i + 1;
                while (j < n && arr[i] > mid * arr[j]) j++;  // find cutoff
                count += n - j;
                if (j < n && (double)arr[i] / arr[j] > (double)p / q) {
                    p = arr[i]; q = arr[j];
                }
            }
            if (count == k) { result = {p, q}; break; }
            else if (count < k) lo = mid;
            else hi = mid;
        }
        return result;
    }
};
```

---

## 3613. Minimize Maximum Component Cost
🔗 [LeetCode](https://leetcode.com/problems/minimize-maximum-component-cost)

**Logic:** Binary search on the max edge cost allowed. For a given threshold, keep only edges with cost ≤ threshold (using Union-Find to count connected components). Check if the number of components ≤ k. Minimize the threshold.

```cpp
class Solution {
public:
    int minCost(int n, vector<vector<int>>& edges, int k) {
        sort(edges.begin(), edges.end(), [](auto& a, auto& b){ return a[2] < b[2]; });
        int lo = 0, hi = edges.back()[2];
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (components(n, edges, mid) <= k)
                hi = mid;
            else
                lo = mid + 1;
        }
        return lo;
    }

    int components(int n, vector<vector<int>>& edges, int maxCost) {
        vector<int> parent(n);
        iota(parent.begin(), parent.end(), 0);
        function<int(int)> find = [&](int x) {
            return parent[x] == x ? x : parent[x] = find(parent[x]);
        };
        int comps = n;
        for (auto& e : edges) {
            if (e[2] > maxCost) break;
            int pu = find(e[0]), pv = find(e[1]);
            if (pu != pv) { parent[pu] = pv; comps--; }
        }
        return comps;
    }
};
```

---

## Quick Reference — BS on Answers Patterns

| Sub-pattern | Problems | Feasibility Check |
|---|---|---|
| **Minimize time/speed** | 875, 1011, 1870, 2187, 2594, 3296 | count ops in time t ≥ required |
| **Minimize days** | 1482 | greedy count with day threshold |
| **Minimize maximum** | 1760, 2064, 2439, 2560, 2616, 3356 | greedy or simulation |
| **Maximize minimum gap** | 1552, 2517, 2498, 3281 | greedy placement with gap |
| **Maximize count/value** | 2226, 2861, 1802, 1891 | sum of capacities ≥ k |
| **BS on numeric value** | 378, 786, 1283, 1300 | count of elements meeting threshold |
| **Graph connectivity** | 3419, 3613 | BFS/DFS or Union-Find |

### The Two Templates

```cpp
// MINIMIZE: find smallest x where condition(x) is true
int lo = min_val, hi = max_val;
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (condition(mid)) hi = mid;
    else lo = mid + 1;
}
return lo;

// MAXIMIZE: find largest x where condition(x) is true
int lo = min_val, hi = max_val;
while (lo < hi) {
    int mid = lo + (hi - lo + 1) / 2;  // upper mid to avoid infinite loop
    if (condition(mid)) lo = mid;
    else hi = mid - 1;
}
return lo;
```
