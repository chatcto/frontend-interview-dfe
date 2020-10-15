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

#### 二分法查找变体

1. 查找第一个值等于给定值的元素

```js
function searchFirst(arr, value) {
  let low = 0,
    high = arr.length - 1,
    mid;
  while (low < high) {
    mid = low + ((high - low) >> 1);
    if (value < arr[mid]) {
      high = mid - 1;
    } else if (value > arr[mid]) {
      low = mid + 1;
    } else {
      if (mid === 0 || arr[mid - 1] !== value) {
        return mid;
      } else {
        high = mid - 1;
      }
    }
  }
  return -1;
}
```
如果mid等于0，那这个元素已经是数组的第一个元素，那它肯定是我们要找的;

如果mid不等于0，a[mid]的前一个元素a[mid-1]不等于value，那也说明a[mid]就是我们要找的第一个值等于给定值的元素。



2. 查找最后一个值等于给定值的元素

```js
function searchLast(arr, value) {
  let low = 0,
    high = arr.length - 1,
    mid;
  while (low <= high) {
    mid = low + ((high - low) >> 1);
    if (value < arr[mid]) {
      high = mid - 1;
    } else if (value > arr[mid]) {
      low = mid + 1;
    } else {
      if (mid === arr.length - 1 || arr[mid + 1] !== value) {
        return mid;
      } else {
        low = mid + 1;
      }
    }
  }
  return -1;
}
```

3. 查找第一个大于等于给定值的元素

```js
function searchB(arr, value) {
  let low = 0,
    high = arr.length - 1,
    mid;
  while (low <= high) {
    mid = low + ((high - low) >> 1);
    if (arr[mid] >= value) {
      if (mid === 0 || arr[mid - 1] < value) {
        return mid;
      } else {
        high = mid - 1
      }
    } else {
        low = mid + 1
    }
  }
  return -1;
}
```
如果a[mid]前面已经没有元素，或者前面一个元素小于要查找的值value，那a[mid]就是我们要找的
元素。

如果a[mid-1]也大于等于要查找的值value，那说明要查找的元素在[low, mid-1]之间，所以，我们将high更新为mid-1。

4. 查找最后一个小于等于给定值的元素

```js
function searchL(arr, value) {
  let low = 0,
    high = arr.length - 1,
    mid;
  while (low <= high) {
    mid = low + ((high - low) >> 1);
    if (arr[mid] <= value) {
      if (mid === arr.length - 1 || arr[mid + 1] > value) {
        return mid;
      } else {
        low = mid + 1;
      }
    } else {
      high = mid - 1;
    }
  }
  return -1;
}
```
