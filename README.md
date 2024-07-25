
# Mastering Two-Pointer Arrays for Coding Interviews

The Two Pointer approach is a pivotal technique frequently explored in coding interviews, renowned for its efficiency in solving array-related problems. It involves leveraging two indices (or pointers) to traverse the array, often from different directions or speeds. This method significantly enhances the efficiency of solutions that might otherwise require nested loops or additional space.

In this guide, we delve deep into mastering the Two Pointer approach, exploring a curated selection of the most commonly asked interview questions that employ this technique. Whether you're aiming to solidify your understanding as a beginner or seeking advanced strategies to refine your skills, this guide will equip you with comprehensive knowledge and practical examples.

We begin by outlining foundational strategies for using Two Pointers:
- **Opposite Ends**: Initiate pointers at both ends of the array to facilitate comparisons, particularly useful for tasks such as finding pairs that sum up to a specific target.
- **Same End**: Start both pointers at the same position but advance them at different rates, ideal for problems like identifying the longest substring without repeating characters.

In subsequent articles, we'll explore:
- **Hash Table Approach**: Utilizing hash tables for quick value retrieval, solving problems related to duplicates, frequency counting, and efficient searching.
- **Greedy Approach**: Building solutions piece by piece by always selecting the locally optimal choice, useful for a variety of optimization problems in arrays.

Each section will provide detailed explanations and C++ code examples to illustrate concepts and solutions effectively. By the end, you'll have gained proficiency in leveraging the Two Pointer approach and be well-prepared to tackle array-related challenges in coding interviews and beyond.

Whether you're preparing for coding interviews or aiming to expand your algorithmic toolkit, mastering the Two Pointer approach will undoubtedly enhance your problem-solving skills and set you apart as a capable software engineer. Stay tuned for our upcoming articles on Hash Table and Greedy approaches!

---

## 1. Remove Duplicates from Sorted Array

**Problem**: Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in `nums`.

**Example 1**:
- **Input**: `nums = [1,1,2]`
- **Output**: `2`, `nums = [1,2,_]`
- **Explanation**: Your function should return `k = 2`, with the first two elements of `nums` being 1 and 2 respectively.

**Example 2**:
- **Input**: `nums = [0,0,1,1,1,2,2,3,3,4]`
- **Output**: `5`, `nums = [0,1,2,3,4,_,_,_,_,_]`
- **Explanation**: Your function should return `k = 5`, with the first five elements of `nums` being 0, 1, 2, 3, and 4 respectively.

**Solution**:
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int j = 1;
        int i = 0;
        for(i = 1; i < nums.size(); i++) {
            if(nums[i] > nums[i-1]) {
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
};
```

**Explanation**:
- **Initialization**: We initialize two pointers, `j` and `i`. Pointer `j` is set to 1, which will track the position of the next unique element. Pointer `i` is set to 0 to start traversing the array from the second element.
- **Traversal**: We use a for loop to traverse the array starting from index 1.
- **Comparison**: For each element in the array, we compare it with the previous element. If the current element (`nums[i]`) is greater than the previous element (`nums[i - 1]`), it means the current element is unique.
- **Updating Unique Elements**: If the element is unique, we assign it to the position indicated by pointer `j` (`nums[j] = nums[i]`), and then increment `j` to point to the next position.
- **Skipping Duplicates**: If the current element is not greater than the previous element, it means it is a duplicate, and we skip it by continuing the loop.
- **Return Value**: After the loop completes, the value of `j` will be the new length of the array with unique elements.

---

## 2. Remove Duplicates from Sorted Array II

**Problem**: Given an integer array `nums` sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

**Example 1**:
- **Input**: `nums = [1,1,1,2,2,3]`
- **Output**: `5`, `nums = [1,1,2,2,3,_]`
- **Explanation**: Your function should return `k = 5`, with the first five elements of `nums` being 1, 1, 2, 2, and 3 respectively.

**Example 2**:
- **Input**: `nums = [0,0,1,1,1,1,2,3,3]`
- **Output**: `7`, `nums = [0,0,1,1,2,3,3,_,_]`
- **Explanation**: Your function should return `k = 7`, with the first seven elements of `nums` being 0, 0, 1, 1, 2, 3, and 3 respectively.

**Solution**:
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size() < 3) return nums.size();

        int j = 2;
        for(int i = 2; i < nums.size(); i++) {
            if(nums[i] != nums[j - 2]) {
                nums[j++] = nums[i];
            }
        }
        return j;
    }
};
```

**Explanation**:
- **Initialization**: We start with two pointers: `j` and `i`, both initialized to 2. The pointer `j` will track the index where the next valid element (that adheres to the constraint of at most two occurrences) should be placed.
- **Traversal**: Traverse the array with pointer `i`. For each element `nums[i]`, compare it with the element `nums[j - 2]` (which represents the last element that is valid according to the constraint).
- **Updating Valid Elements**: If `nums[i]` is different from `nums[j - 2]`, it means we have encountered a new element (or a valid occurrence after the second occurrence), so we can safely place it in `nums[j]` and increment `j`.
- **Result**: After completing the traversal, `j` will represent the length of the modified array, as all elements up to `j-1` are valid and meet the criteria.

---

## 3. Move Zeroes

**Problem**: Given an integer array `nums`, move all `0`s to the end of it while maintaining the relative order of the non-zero elements. Note that you must do this in-place without making a copy of the array.

**Example 1**:
- **Input**: `nums = [0,1,0,3,12]`
- **Output**: `[1,3,12,0,0]`

**Example 2**:
- **Input**: `nums = [0]`
- **Output**: `[0]`

**Solution**:
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for (int lastNonZeroFoundAt = 0, cur = 0; cur < nums.size(); cur++) {
            if (nums[cur] != 0) {
                swap(nums[lastNonZeroFoundAt++], nums[cur]);
            }
        }
    }
};
```

**Explanation**:
- **Initialization**: We initialize two pointers, `lastNonZeroFoundAt` and `cur`. Pointer `lastNonZeroFoundAt` is set to 0 and will track the position of the last non-zero element found. Pointer `cur` is also set to 0 and is used to traverse the array.
- **Traversal**: We use a for loop to traverse the array with the `cur` pointer from the beginning to the end of the array.
- **Check for Non-Zero Elements**: For each element in the array, we check if it is not zero (`nums[cur] != 0`).
- **Swapping Non-Zero Elements**: If the current element is not zero, we swap it with the element at the `lastNonZeroFoundAt` position (`swap(nums[lastNonZeroFoundAt++], nums[cur])`). After the swap, we increment the `lastNonZeroFoundAt` pointer to the next position.
- **Skip Zero Elements**: If the current element is zero, we simply continue to the next element in the loop.
  
- This approach ensures that all non-zero elements are moved to the beginning of the array while maintaining their relative order. All zero elements are moved to the end of the array. This solution operates in-place with a time complexity of O(n), where n is the length of the array, and uses constant extra space.
---

## 4. Merge Sorted Arrays

**Problem**: You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively. The task is to merge `nums1` and `nums2` into `

nums1` as one sorted array. 

**Example 1**:
- **Input**: `nums1 = [1,2,3,0,0,0]`, `m = 3`, `nums2 = [2,5,6]`, `n = 3`
- **Output**: `nums1 = [1,2,2,3,5,6]`

**Example 2**:
- **Input**: `nums1 = [1], m = 1`, `nums2 = []`, `n = 0`
- **Output**: `nums1 = [1]`

**Solution**:
```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;
        
        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }
        
        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }
    }
};
```

**Explanation**:
- **Initialization**: We initialize three pointers: `i` for the end of the initialized portion of `nums1`, `j` for the end of `nums2`, and `k` for the end of the merged array within `nums1`.
- **Merging**: We compare elements from the end of `nums1` and `nums2`. The larger element is placed at the end of `nums1` (`nums1[k--]`), and the corresponding pointer (`i` or `j`) is decremented.
- **Handling Remaining Elements**: If elements remain in `nums2` after merging, they are copied to `nums1`.
Here’s how you can format your article for GitHub README using Markdown:

---

# 5. Container With Most Water

You are given an integer array `height` of length `n`; there are `n` vertical lines drawn such that the two endpoints of the `i`-th line are `(i, 0)` and `(i, height[i])`. Your task is to find two lines that, together with the x-axis, form a container that contains the most water. Return the maximum amount of water a container can store. Note that you may not slant the container.

## Example

### Example 1
- **Input**: `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`
- **Output**: `49`
- **Explanation**: The vertical lines are represented by the array `[1, 8, 6, 2, 5, 4, 8, 3, 7]`. The container that can contain the most water is formed by the lines at indices 1 and 8, with heights 8 and 7, respectively. The maximum area of water the container can contain is `49`.

### Example 2
- **Input**: `height = [1, 1]`
- **Output**: `1`
- **Explanation**: The container formed by the lines at indices 0 and 1 can contain `1` unit of water.

## Solution Explanation

This problem can be solved using the two-pointer technique, which is explained below:

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int begin = 0;
        int end = height.size() - 1;
        int maxArea = 0;

        std::cout << height.at(end);
        for (; begin < end;) {
            int area = min(height[begin], height[end]) * (end - begin);
            maxArea = max(area, maxArea);

            if (height[end] <= height[begin]) {
                end--;
            } else {
                begin++;
            }
        }
        return maxArea;
    }
};
```

### Explanation

- **Initialization**: Two pointers, `begin` and `end`, are initialized. The `begin` pointer is set to the start of the array, and the `end` pointer is set to the end of the array. We also initialize `maxArea` to store the maximum area found.
- **Traversal**: A while loop is used to traverse the array with the two pointers until `begin` is less than `end`.
- **Calculate Area**: For each pair of lines pointed to by `begin` and `end`, we calculate the area formed by the container they make with the x-axis. The area is given by the minimum of the heights of the two lines multiplied by the distance between them (`min(height[begin], height[end]) * (end - begin)`).
- **Update Max Area**: We update `maxArea` if the calculated area is greater than the current `maxArea`.
- **Move Pointers**: To potentially find a larger area, we move the pointer pointing to the shorter line towards the center. If the line at `end` is shorter or equal in height to the line at `begin`, we decrement the `end` pointer; otherwise, we increment the `begin` pointer.

This approach ensures that we efficiently explore potential containers while maintaining \(O(n)\) time complexity, where `n` is the length of the array, by leveraging the two-pointer technique to minimize unnecessary comparisons.

---

# 6. Two Sum II - Input Array Is Sorted

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice. Your solution must use only constant extra space.

## Example

### Example 1
- **Input**: `numbers = [2, 7, 11, 15]`, `target = 9`
- **Output**: `[1, 2]`
- **Explanation**: The sum of `2` and `7` is `9`. Therefore, `index1 = 1`, `index2 = 2`. We return `[1, 2]`.

### Example 2
- **Input**: `numbers = [2, 3, 4]`, `target = 6`
- **Output**: `[1, 3]`
- **Explanation**: The sum of `2` and `4` is `6`. Therefore, `index1 = 1`, `index2 = 3`. We return `[1, 3]`.

### Example 3
- **Input**: `numbers = [-1, 0]`, `target = -1`
- **Output**: `[

1, 2]`
- **Explanation**: The sum of `-1` and `0` is `-1`. Therefore, `index1 = 1`, `index2 = 2`. We return `[1, 2]`.

## Solution

We can solve this problem using the two pointers technique. Here’s an explanation of the provided solution:

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int lo = 0;
        int hi = numbers.size() - 1;
        vector<int> res;

        for (; lo < hi;) {
            if ((numbers[lo] + numbers[hi]) < target) {
                lo++;
            } else if ((numbers[lo] + numbers[hi]) > target) {
                hi--;
            } else {
                res = {lo + 1, hi + 1};
                break;
            }
        }
        return res;
    }
};
```

### Explanation

- **Initialization**: We initialize two pointers, `lo` and `hi`. The `lo` pointer is set to the start of the array, and the `hi` pointer is set to the end of the array.
- **Traversal**: We use a while loop to traverse the array with the two pointers until `lo` is less than `hi`.
- **Calculate Sum**: For each pair of elements pointed to by `lo` and `hi`, we calculate their sum:
  - If the sum is less than the target, we move the `lo` pointer to the right to increase the sum.
  - If the sum is greater than the target, we move the `hi` pointer to the left to decrease the sum.
  - If the sum is equal to the target, we have found the two numbers, so we store their 1-indexed positions in the result array `res` and break the loop.
- **Return Result**: The result array `res` containing the indices of the two numbers is returned.

This approach ensures that we find the two numbers that sum to the target using \(O(n)\) time complexity and \(O(1)\) extra space. This efficiency is achieved by leveraging the sorted order of the array and the two pointers technique.

---

# 7. 3Sum

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`. The solution set must not contain duplicate triplets.

## Example

### Example 1
- **Input**: `nums = [-1, 0, 1, 2, -1, -4]`
- **Output**: `[[-1, -1, 2], [-1, 0, 1]]`

### Example 2
- **Input**: `nums = [0, 1, 1]`
- **Output**: `[]`
- **Explanation**: The only possible triplet does not sum up to 0.

### Example 3
- **Input**: `nums = [0, 0, 0]`
- **Output**: `[[0, 0, 0]]`
- **Explanation**: The only possible triplet sums up to 0.

## Solution

We can solve this problem using the two pointers technique similar to the previous problem. Here’s an explanation of the provided solution:

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(begin(nums), end(nums));
        for (int i = 0; i < nums.size() && nums[i] <= 0; i++) {
            if (i == 0 || nums[i - 1] != nums[i]) {
                twosum(nums, i, res);
            }
        }
        return res;
    }

    void twosum(vector<int>& nums, int i, vector<vector<int>>& res) {
        int lo = i + 1;
        int hi = nums.size() - 1;
        while (lo < hi) {
            if (nums[lo] + nums[hi] + nums[i] < 0) {
                lo++;
            } else if (nums[lo] + nums[hi] + nums[i] > 0) {
                hi--;
            } else {
                res.push_back({nums[i], nums[lo++], nums[hi--]});
                while (lo < hi && nums[lo] == nums[lo - 1]) ++lo;
                while (lo < hi && nums[hi] == nums[hi + 1]) --hi;
            }
        }
    }
};
```

### Explanation

- **Sorting**: First, we sort the array to facilitate the two pointers technique and to easily skip duplicates.
- **Traverse the Array**: We traverse the array using a for loop. For each element `nums[i]`, we set two pointers: `lo` to `i + 1` and `hi` to the end of the array.
- **Avoid Duplicates**: We skip duplicate elements to avoid duplicate triplets by checking if the current element is the same as the previous one.
- **Two Pointers Technique**:
  - Calculate the sum of the current element `nums[i]` and the elements at the `lo` and `hi` pointers.
  - If the sum is zero, we add the triplet to the result.
  - Move the `lo` pointer to the right, skipping duplicate elements, and similarly, move the `hi` pointer to the left, skipping duplicates.
  - If the sum is less than zero, move the `lo` pointer to the right to increase the sum.
  - If the sum is greater than zero, move the `hi` pointer to the left to decrease the sum.

This approach ensures that we find all unique triplets that sum to zero with a time complexity of \(O(n^2)\), where `n` is the length of the array.

---

# Relationship to Previous Problems

The `3Sum` problem is similar to the `Two Sum II` problem in the following ways:
- **Two Pointers Technique**: Both problems use the two pointers technique to find the required elements. In `Two Sum II`, we use two pointers to find two elements that sum up to the target. In `3Sum`, we use two pointers to find two elements that, together with the current element, sum up to zero.
- **Sorting**: Both problems benefit from sorting the array first, which helps in efficiently finding the elements and avoiding duplicates.
- **Avoiding Duplicates**: Both problems include mechanisms to avoid counting duplicate solutions. In `Two Sum II`, this is simpler as we only need to avoid using the same element twice. In `3Sum`, we skip over duplicate elements during the traversal to ensure unique triplets.

By understanding and implementing the two pointers technique, you can efficiently solve both of these problems with optimal time and space complexity.

# Algorithm Solutions

This repository contains solutions to several algorithmic problems, implemented in C++. The problems covered include sorting colors, removing elements, rotating arrays, finding the next permutation, and more.

Here’s the content for the **Sort Colors** problem formatted for your GitHub README:

---

## 8. Sort Colors

**Problem Statement:** Given an array `nums` with `n` objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue. We use the integers `0`, `1`, and `2` to represent the colors red, white, and blue, respectively.

**Example:**

- **Example 1:**
  - **Input:** `nums = [2, 0, 2, 1, 1, 0]`
  - **Output:** `[0, 0, 1, 1, 2, 2]`

- **Example 2:**
  - **Input:** `nums = [2, 0, 1]`
  - **Output:** `[0, 1, 2]`

**Constraints:**
- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.

**Solution:**

We can solve this problem using the Dutch National Flag algorithm by Edsger W. Dijkstra, which involves a single pass through the array with three pointers. 

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int lo = 0;
        int hi = nums.size() - 1;
        int curr = 0;

        while (curr <= hi) {
            if (nums[curr] == 0) {
                swap(nums[lo++], nums[curr++]);
            } else if (nums[curr] == 2) {
                swap(nums[hi--], nums[curr]);
            } else {
                curr++;
            }
        }
    }
};
```

**Explanation:**

- **Initialization:**
  - Three pointers are initialized: `lo`, `hi`, and `curr`.
    - `lo` is set to the start of the array and is used to place `0`s.
    - `hi` is set to the end of the array and is used to place `2`s.
    - `curr` is used to traverse the array.

- **Traversal:**
  - Use a `while` loop to traverse the array with the `curr` pointer until it surpasses `hi`.

- **Placing `0`s:**
  - If `nums[curr]` is `0`, swap it with the element at the `lo` pointer and increment both `lo` and `curr`.
  - This ensures that all `0`s are moved to the beginning of the array.

- **Placing `2`s:**
  - If `nums[curr]` is `2`, swap it with the element at the `hi` pointer and decrement `hi`.
  - Do not increment `curr` here because the element swapped from the end needs to be checked.

- **Skipping `1`s:**
  - If `nums[curr]` is `1`, simply move `curr` to the next position.

This approach ensures that the array is sorted in one pass with constant extra space, making it highly efficient. The time complexity is `O(n)`, where `n` is the length of the array, and the space complexity is `O(1)`.

---
## 9. Remove Element

**Problem Statement:** Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. After removing the elements, return the number of remaining elements.

**Example:**

- **Example 1:**
  - **Input:** `nums = [3, 2, 2, 3], val = 3`
  - **Output:** `2` (remaining elements are `[2, 2]`)

- **Example 2:**
  - **Input:** `nums = [0, 1, 2, 2, 3, 0, 4, 2], val = 2`
  - **Output:** `5` (remaining elements are `[0, 1, 3, 0, 4]`)

**Constraints:**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

**Solution:**

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int j = 0;
        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != val) {
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
};
```

**Explanation:**

- **Initialization:** We initialize `j` to 0, which will track the index where valid (non-val) elements should be placed in `nums`.

- **Iteration:** We loop through each element of the vector `nums`.
  - **Condition Check:** For each element `nums[i]`, we check if it is not equal to `val`.
  - **Replacing Elements:** If `nums[i]` is not equal to `val`, we assign `nums[i]` to `nums[j]` and then increment `j`. This effectively "removes" `val` from the sequence by overwriting it with subsequent non-val elements.
  - **Returning the New Length:** Finally, we return `j`, which now represents the new length of `nums` after removing all occurrences of `val`.

- **Complexity:** The approach operates in-place with \(O(n)\) time complexity and does not require extra space.

## 10. Rotate Array

**Problem Statement:** Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

**Example:**

- **Example 1:**
  - **Input:** `nums = [1,2,3,4,5,6,7], k = 3`
  - **Output:** `[5,6,7,1,2,3,4]`
  - **Explanation:** Rotate 1 step to the right: `[7,1,2,3,4,5,6]` Rotate 2 steps to the right: `[6,7,1,2,3,4,5]` Rotate 3 steps to the right: `[5,6,7,1,2,3,4]`

- **Example 2:**
  - **Input:** `nums = [-1,-100,3,99], k = 2`
  - **Output:** `[3,99,-1,-100]`
  - **Explanation:** Rotate 1 step to the right: `[99,-1,-100,3]` Rotate 2 steps to the right: `[3,99,-1,-100]`

**Solution:**

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> a(nums.size());
        for (int i = 0; i < a.size(); i++) {
            a[(i + k) % a.size()] = nums[i];
        }
        int j = 0;
        for (int i : a) {
            nums[j] = i;
            j++;
        }
    }
};
```

**Explanation:**

- **Initialization:** Create a temporary array `a` of the same size as `nums` to hold the rotated values.

- **Rotation Logic:** Iterate through each element `nums[i]` using the index `i`. Compute the new index in the rotated array `a` using `(i + k) % a.size()`. This formula calculates where each element in `nums` should be placed in the rotated array `a`.

- **Copying to Original Array:** After computing the rotated positions in `a`, copy each element back from `a` to `nums` using a separate loop. This step ensures that the original array `nums` reflects the rotated state.

## 11. Next Permutation

**Problem Statement:** A permutation of an array of integers is an arrangement of its members into a sequence or linear order. The next permutation of an array of integers is the next lexicographically greater permutation of its integer. If such an arrangement is not possible, the array must be rearranged as the lowest possible order (i.e., sorted in ascending order).

**Example:**

- **Example 1:**
  - **Input:** `nums = [1,2,3]`
  - **Output:** `[1,3,2]`

- **Example 2:**
  - **Input:** `nums = [3,2,1]`
  - **Output:** `[1,2,3]`

- **Example 3:**
  - **Input:** `nums = [1,1,5]`
  - **Output:** `[1,5,1]`

**Solution:**

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int i = nums.size() - 2;
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        if (i >= 0) {
            int j = nums.size() - 1;
            while (nums[j] <= nums[i]) {
                j--;
            }
            swap(nums[i], nums[j]);
        }
        reverse(nums.begin() + i + 1, nums.end());
    }
};
```

**Explanation:**

- **Finding the Pivot:** Start from the right end of the array (i.e., `nums.size() - 2`) and

 move leftwards to find the first element `nums[i]` that is smaller than its next element `nums[i+1]`. This identifies the pivot where a change needs to be made to get the next permutation.

- **Finding the Swap Point:** Once the pivot `i` is identified, find the smallest element to the right of `nums[i]` that is larger than `nums[i]`. This element `nums[j]` will be swapped with `nums[i]` to ensure the next permutation.

- **Swapping:** Swap `nums[i]` with `nums[j]` to achieve the next permutation.

- **Reversing the Remaining Sequence:** After swapping, reverse the sequence of elements to the right of `nums[i]` (from `i + 1` to the end of the array). This step ensures that the sequence remains in ascending order, making it the smallest possible permutation after the original order.

## 12. Two Sum II - Input Array Is Sorted

**Problem Statement:** Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`. Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2. The tests are generated such that there is exactly one solution. You may not use the same element twice.

**Example:**

- **Example 1:**
  - **Input:** `numbers = [2,7,11,15], target = 9`
  - **Output:** `[1,2]`
  - **Explanation:** The sum of 2 and 7 is 9. Therefore, `index1 = 1`, `index2 = 2`. We return `[1, 2]`.

- **Example 2:**
  - **Input:** `numbers = [2,3,4], target = 6`
  - **Output:** `[1,3]`
  - **Explanation:** The sum of 2 and 4 is 6. Therefore, `index1 = 1`, `index2 = 3`. We return `[1, 3]`.

- **Example 3:**
  - **Input:** `numbers = [-1,0], target = -1`
  - **Output:** `[1,2]`
  - **Explanation:** The sum of -1 and 0 is -1. Therefore, `index1 = 1`, `index2 = 2`. We return `[1, 2]`.

**Solution:**

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int lo = 0;
        int hi = numbers.size() - 1;
        vector<int> res;

        for (; lo < hi;) {
            if ((numbers[lo] + numbers[hi]) < target) {
                lo++;
            } else if ((numbers[lo] + numbers[hi]) > target) {
                hi--;
            } else {
                res = {lo + 1, hi + 1};
                break;
            }
        }
        return res;
    }
};
```

**Explanation:**

- **Initialization:** Initialize two pointers, `lo` (pointing to the beginning of the array) and `hi` (pointing to the end of the array).

- **Two Pointer Technique:** Use a while loop to iterate until `lo` is less than `hi`. This loop efficiently narrows down the possible pairs of numbers that could sum up to the target.

- **Comparison:**
  - Inside the loop, check if the sum of `numbers[lo]` and `numbers[hi]` is less than the target. If it is, increment `lo` to move to a larger number that might make the sum closer to the target.
  - If the sum is greater than the target, decrement `hi` to move to a smaller number.
  - If the sum equals the target, store `lo + 1` and `hi + 1` (adjusted for 1-based index as per the problem requirements) in the `res` vector and break out of the loop.

- **Returning Result:** After exiting the loop, return `res`, which contains the indices of the two numbers that sum up to the target.

---
Here’s the formatted content for your GitHub README:

---

# Algorithm Solutions

This repository contains solutions to several algorithmic problems, implemented in C++. The problems covered include sorting colors, removing elements, rotating arrays, finding the next permutation, checking subsequences, validating palindromes, and trapping rain water.

## 13. Is Subsequence

**Problem Statement:** Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise. A subsequence of a string is a new string that is formed from the original string by deleting some (or none) of the characters without disturbing the relative positions of the remaining characters.

**Example:**

- **Example 1:**
  - **Input:** `s = "abc", t = "ahbgdc"`
  - **Output:** `true`

- **Example 2:**
  - **Input:** `s = "axc", t = "ahbgdc"`
  - **Output:** `false`

**Solution:**

```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i = 0;
        int j = 0;

        while (i < t.length() && j < s.length()) {
            if (s[j] == t[i]) {
                j++;
            }
            i++;
        }
        
        return j == s.length();
    }
};
```

**Explanation:**

- **Initialization:** Two pointers, `i` and `j`, are initialized for iterating through `t` (potential supersequence) and `s` (subsequence to check), respectively.

- **Two-Pointer Technique:** Use a while loop to traverse `t` and `s`:
  - If `s[j]` matches `t[i]`, increment both pointers (`j++` and `i++`).
  - If they do not match, only increment `i` to continue checking the rest of `t`.

- **Completion Check:** After the loop, check if `j` has reached the length of `s` (`j == s.length()`). If true, `s` is a subsequence of `t`; otherwise, it is not.

- **Edge Case Handling:** If `s` is an empty string, it is always considered a subsequence of any string `t`.

## 14. Valid Palindrome

**Problem Statement:** A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

**Example:**

- **Example 1:**
  - **Input:** `s = "A man, a plan, a canal: Panama"`
  - **Output:** `true`
  - **Explanation:** `"amanaplanacanalpanama"` is a palindrome.

- **Example 2:**
  - **Input:** `s = "race a car"`
  - **Output:** `false`
  - **Explanation:** `"raceacar"` is not a palindrome.

- **Example 3:**
  - **Input:** `s = " "`
  - **Output:** `true`
  - **Explanation:** An empty string is considered a palindrome.

**Solution:**

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int i = 0;
        int j = s.length() - 1;

        while (i < j) {
            while (i < j && !isalnum(s[i])) {
                i++;
            }
            while (j > i && !isalnum(s[j])) {
                j--;
            }
            if (tolower(s[i]) != tolower(s[j])) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
};
```

**Explanation:**

- **Initialization:** Two pointers, `i` starting from the beginning and `j` from the end of the string.

- **Two-Pointer Technique:** Use a while loop to compare characters from both ends:
  - Skip non-alphanumeric characters using nested while loops.
  - Convert characters to lowercase and compare. If they differ, return `false`.
  - Move pointers towards the center of the string.

- **Completion Check:** If the loop completes without finding unequal characters, return `true`, indicating the string is a palindrome.

## 15. Trapping Rain Water

**Problem Statement:** Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

**Example:**

- **Example 1:**
  - **Input:** `height = [0,1,0,2,1,0,1,3,2,1,2,1]`
  - **Output:** `6`

- **Example 2:**
  - **Input:** `height = [4,2,0,3,2,5]`
  - **Output:** `9`

**Solution:**

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int left = 0, right = height.size() - 1;
        int ans = 0;
        int left_max = 0, right_max = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                left_max = max(left_max, height[left]);
                ans += (left_max - height[left]);
                ++left;
            } else {
                right_max = max(right_max, height[right]);
                ans += (right_max - height[right]);
                --right;
            }
        }
        return ans;
    }
};
```

**Explanation:**

- **Initialization:** Two pointers, `left` starting at the beginning and `right` at the end of the array. Initialize `ans` for accumulating trapped water, and `left_max` and `right_max` to track the maximum heights encountered from the left and right.

- **Two-Pointer Technique:** Use a while loop to process elements from both ends:
  - Compare `height[left]` and `height[right]`.
  - If `height[left]` is less than `height[right]`, update `left_max` and calculate trapped water at `left`. Increment `left`.
  - If `height[right]` is less than or equal to `height[left]`, update `right_max` and calculate trapped water at `right`. Decrement `right`.

- **Result:** After the loop, `ans` contains the total amount of trapped water.



