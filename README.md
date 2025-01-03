# coding-interview-handbook
Problem anayliss for leetcode questions

# **Prefix Sum vs On-the-Fly (Running Sum) Computation**

## **1. Prefix Sum**
### **Definition**
- The prefix sum at index `i` is the sum of all elements from the start of the array to `i`.

### **Formula**
- **Prefix Sum Array**: 
  - `prefixSum[i] = nums[0] + nums[1] + ... + nums[i]`
  - For subarray sum between indices `i` and `j`:  
    `sum(i, j) = prefixSum[j] - prefixSum[i-1]` (if `i > 0`).

### **Usage**
- Precompute `prefixSum` once, then reuse it for fast subarray queries.

---

## **2. Running Sum (On-the-Fly Computation)**
### **Definition**
- A running sum is calculated incrementally during a single pass, without storing all cumulative sums.

### **Formula**
- Keep a variable `runningSum`:
  - At any index `i`: `runningSum += nums[i]`.
  - Use `runningSum` directly for further calculations (e.g., `rightSum = totalSum - runningSum`).

---

## **Key Comparison**

| **Aspect**           | **Prefix Sum**                | **Running Sum**              |
|-----------------------|-------------------------------|------------------------------|
| **Space Complexity**  | **O(n)** (stores all sums)    | **O(1)** (no extra storage)  |
| **Flexibility**       | Reusable for multiple queries | Single-use during traversal  |
| **Use Case**          | Efficient subarray queries    | Single traversal problems    |

---

## **When to Use**
- **Prefix Sum**: 
  - Use when you need to calculate subarray sums repeatedly or reuse intermediate sums.
- **Running Sum**:
  - Use when prefix sums are required only for a single pass and space optimization is critical.

---

## **Practical Example**
### Problem: Count Valid Splits in an Array
```typescript
// Prefix Sum Approach
function waysToSplitArray(nums: number[]): number {
    const prefixSum = [];
    let runningSum = 0, validSplits = 0;
    for (let num of nums) prefixSum.push(runningSum += num);
    for (let i = 0; i < nums.length - 1; i++) {
        if (prefixSum[i] >= prefixSum[nums.length - 1] - prefixSum[i]) validSplits++;
    }
    return validSplits;
}
