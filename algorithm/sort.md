---
title: "排序"
---

### 冒泡排序

```js
function bubbleSort(list) {
  for (let i = 0; i < list.length; i++) {
    let isSorted = true;
    for (let j = 0; j < list.length - 1 - i; j++) {
      if (list[j] > list[j + 1]) {
        [list[j + 1], list[j]] = [list[j], list[j + 1]];
        isSorted = false;
      }
    }
    if (isSorted) break;
  }
  return list;
}
```

### 选择排序

每次循环选取一个最小的数字放到前面的有序序列中。

```js
function selectSort(arr) {
  let minIndex = 0;
  for (let i = 0; i < arr.length - 1; i++) {
    minIndex = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
  }
  return arr;
}
```

### 插入排序

将左侧序列看成一个有序序列，每次将一个数字插入该有序序列。插入时，从有序序列最右侧开始比较，若比较的数较大，后移一位。

```js
function insertSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    for (let j = i; j > 0; j--) {
      if (arr[j] < arr[j - 1]) {
        [arr[j - 1], arr[j]] = [arr[j], arr[j - 1]];
      }
    }
  }
  return arr;
}
```

### 归并排序

利用递归思和分治想，将原序列从中间分割成两个子序列，
对分割好的子序列进行重复操作，
最后将拆分好的子序列进行排序，形成新的子序列，然后对子序列进行合并
形成排好序的新序列。

```js
// 递归实现

function mergeSort(arr) {
  if (arr == null || arr.length <= 0) {
    return [];
  }
  sortProcess(arr, 0, arr.length - 1);
  return arr;
}

function sortProcess(arr, L, R) {
  //递归的终止条件，就是左右边界索引一样
  if (L == R) {
    return;
  }
  var middle = L + ((R - L) >> 1); //找出中间值
  sortProcess(arr, L, middle); //对左侧部分进行递归
  sortProcess(arr, middle + 1, R); //对右侧部分进行递归
  merge(arr, L, middle, R); //然后利用外排方式进行结合
}

function merge(arr, L, middle, R) {
  var help = [];
  var l = L;
  var r = middle + 1;
  var index = 0;
  //利用外排方式进行
  while (l <= middle && r <= R) {
    help[index++] = arr[l] < arr[r] ? arr[l++] : arr[r++];
  }
  while (l <= middle) {
    help.push(arr[l++]);
  }
  while (r <= R) {
    help.push(arr[r++]);
  }

  for (var i = 0; i < help.length; i++) {
    arr[L + i] = help[i];
  }
  //arr.splice(L, help.length, ...help);//这个利用了ES6的语法
}

// 循环实现

function mergeSort(arr) {
  if (arr == null || arr.length <= 0) {
    return [];
  }
  var len = arr.length;
  //i每次乘2，是因为每次合并以后小组元素就变成两倍个了
  for (var i = 1; i < len; i *= 2) {
    var index = 0; //第一组的起始索引
    while (2 * i + index <= len) {
      index += 2 * i;
      merge(arr, index - 2 * i, index - i, index);
    }
    //说明剩余两个小组，但其中一个小组数据的数量已经不足2的幂次方个
    if (index + i < len) {
      merge(arr, index, index + i, len);
    }
  }
  return arr;
}

//利用外排的方式进行结合
function merge(arr, start, mid, end) {
  //新建一个辅助数组
  var help = [];
  var l = start,
    r = mid;
  var i = 0;
  while (l < mid && r < end) {
    help[i++] = arr[l] < arr[r] ? arr[l++] : arr[r++];
  }
  while (l < mid) {
    help[i++] = arr[l++];
  }
  while (r < end) {
    help[i++] = arr[r++];
  }
  for (var j = 0; j < help.length; j++) {
    arr[start + j] = help[j];
  }
}
```

### 快速排序

通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

```js
function partition(arr, l, r) {
  let pivot = arr[l];
  while (l < r) {
    while (l < r && arr[r] >= pivot) {
      r--;
    }
    arr[l] = arr[r];
    while (l < r && arr[l] < pivot) {
      l++;
    }
    arr[r] = arr[l];
  }
  arr[l] = pivot;
  return l;
}

// 递归实现
function quickSort1(arr, l, r) {
  if (l < r) {
    let p = partition(arr, l, r);
    quickSort1(arr, l, p - 1);
    quickSort1(arr, p + 1, r);
  }
}

// 循环实现
function quickSort2(arr) {
  // 用push()和pop()函数创建一个将作为栈使用的数组
  stack = [];

  // 将整个初始数组做为“未排序的子数组”
  stack.push(0);
  stack.push(arr.length - 1);

  // 没有显式的peek()函数
  // 只要存在未排序的子数组，就重复循环
  while (stack[stack.length - 1] >= 0) {
    // 提取顶部未排序的子数组
    end = stack.pop();
    start = stack.pop();

    pivotIndex = partition(arr, start, end);

    // 如果基准的左侧有未排序的元素，
    // 则将该子数组添加到栈中，以便稍后对其进行排序
    if (pivotIndex - 1 > start) {
      stack.push(start);
      stack.push(pivotIndex - 1);
    }

    // 如果基准的右侧有未排序的元素，
    // 则将该子数组添加到栈中，以便稍后对其进行排序
    if (pivotIndex + 1 < end) {
      stack.push(pivotIndex + 1);
      stack.push(end);
    }
  }
}
```
