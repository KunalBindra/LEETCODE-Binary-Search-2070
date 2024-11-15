# LEETCODE-Binary-Search-2070
### Overview of the Solution:
1. **Sort the items** by price in ascending order.
2. **Update beauty values** to make them non-decreasing as prices increase.
3. **For each query**, perform a binary search to find the maximum beauty for prices less than or equal to the query price.

### Test Case:
Suppose we have the following inputs:
- `items = [[3, 5], [1, 2], [5, 8]]` (price, beauty pairs)
- `queries = [2, 4, 5]`

### Step 1: Sort `items` by price
Sorted `items` becomes:
```
[[1, 2], [3, 5], [5, 8]]
```

### Step 2: Update beauty values to ensure non-decreasing beauty:
Iterate over the sorted `items`:
- `maxBeautySeen = 2` (from [1, 2])
- Next, compare with [3, 5]: `maxBeautySeen = max(2, 5) = 5`
  - Update [3, 5] to [3, 5]
- Then compare with [5, 8]: `maxBeautySeen = max(5, 8) = 8`
  - Update [5, 8] to [5, 8]

Updated `items`:
```
[[1, 2], [3, 5], [5, 8]]
```

### Step 3: Process each query
For each query, apply `customBinarySearch`:
#### Query 1: `queryPrice = 2`
- Binary search in `[[1, 2], [3, 5], [5, 8]]`:
  - Mid index = 1, items[1][0] = 3 > 2 → Move `right` to 0.
  - Mid index = 0, items[0][0] = 1 ≤ 2 → Update `maxBeauty = 2`. Move `left` to 1.
  - End of search. Result for query 2 is `2`.

#### Query 2: `queryPrice = 4`
- Binary search in `[[1, 2], [3, 5], [5, 8]]`:
  - Mid index = 1, items[1][0] = 3 ≤ 4 → Update `maxBeauty = 5`. Move `left` to 2.
  - Mid index = 2, items[2][0] = 5 > 4 → Move `right` to 1.
  - End of search. Result for query 4 is `5`.

#### Query 3: `queryPrice = 5`
- Binary search in `[[1, 2], [3, 5], [5, 8]]`:
  - Mid index = 1, items[1][0] = 3 ≤ 5 → Update `maxBeauty = 5`. Move `left` to 2.
  - Mid index = 2, items[2][0] = 5 ≤ 5 → Update `maxBeauty = 8`. Move `left` to 3.
  - End of search. Result for query 5 is `8`.

### Final Output:
The result array is:
```
[2, 5, 8]
```
