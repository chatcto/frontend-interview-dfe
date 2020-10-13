---
title: "查找"
---

### 二分法查找

```js
// 循环查找
function bsearch(arr, value) {
  let low = 0,
    high = arr.length - 1;
  let mid;
  while (low < high) {
    mid = ~~((low + high) / 2);
    if (arr[mid] === value) {
      return mid;
    }
    if (arr[mid] > value) {
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }
  return -1;
}

//递归实现
function bsearch1(arr, value, low, high) {
  if (low > high) {
    return -1;
  }
  let mid = ~~((low + high) / 2);
  if (arr[mid] === value) {
    return mid;
  }
  if (value > arr[mid]) {
    return bsearch1(arr, value, mid + 1, high);
  } else {
    return bsearch1(arr, value, low, mid - 1);
  }
}
```
