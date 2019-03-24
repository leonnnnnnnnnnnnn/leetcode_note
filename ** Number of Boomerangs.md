# Number of Boomerangs - LC 447

## Description

Given *n* points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between `i` and `j` equals the distance between `i` and `k` (**the order of the tuple matters**).

Find the number of boomerangs. You may assume that *n* will be at most **500** and coordinates of points are all in the range **[-10000, 10000]** (inclusive).

**Example:**

```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

## Solution 1

```cpp
int dist(const pair<int, int>& p, const pair<int, int>& q) {
    return (p.first - q.first) * (p.first - q.first) + (p.second - q.second) * (p.second - q.second);
}

int numberOfBoomerangs(vector<pair<int, int>>& points) {
    int res = 0;

    for(int i = 0; i < points.size(); i++) {
        unordered_map<int, int> record;

        for(int j = 0; j < points.size(); j++)
            if(i != j)
                record[dist(points[i], points[j])]++;

        for (auto &iter : record)
            if(iter.second >1)
                res += iter.second * (iter.second - 1);
    }

    return res;
}
```

$T(n)=O(n^2)$, *N* is no larger than 500, an $O(n^2)$ algo is sufficient.