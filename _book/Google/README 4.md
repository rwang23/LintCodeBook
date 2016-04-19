##Binary Search

####正常用法
- 需要sorted
- 一般不带duplicate,有duplicate就有变化

####log(n)
- k numbers ---> k/2 numbers

####Basic Model

```java
int end = nums.length - 1;
int start = 0;

while (end > start+1) {
    int mid = start + (end - start) / 2;
    if (nums[mid] == target) {
        end = mid;
    } else if (nums[mid] > target) {
        end = mid;
    } else {
        start = mid;
    }
}

if (nums[end] == target) {
    return end;
} else if(nums[start] == target) {
    return start;
}

```

<!-- Place this tag right after the last button or just before your close body tag. -->
<script async defer id="github-bjs" src="https://buttons.github.io/buttons.js"></script>
