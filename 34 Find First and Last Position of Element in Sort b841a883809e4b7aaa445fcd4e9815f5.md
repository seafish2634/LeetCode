# 34. Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

```

**Example 3:**

```
Input: nums = [], target = 0
Output: [-1,-1]

```

**Constraints:**

- `0 <= nums.length <= 105`
- `109 <= nums[i] <= 109`
- `nums` is a non-decreasing array.
- `109 <= target <= 109`

### Code:

```csharp
**class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res(2,-1);
        int begin=0,end=nums.size(),mid;
        while(begin<end)
        {
            mid=(begin+end)/2;
            cout<<mid<<endl;
            if(nums[mid]<target)begin=mid+1;
            else if(nums[mid]>target) end=mid;
            else
            {
                if(mid==0||nums[mid-1]<target)
                {
                    res[0]=mid;
                    break;
                }
                else
                    end=mid;
            }
        }
        if(res[0]!=-1)
        {
            begin=0,end=nums.size();
            while(begin<end)
            {
                mid=(begin+end)/2;
                if(nums[mid]<target)begin=mid+1;
                else if(nums[mid]>target) end=mid;
                else
                {
                    if(mid==nums.size()-1||nums[mid+1]>target)
                    {
                        res[1]=mid;
                        break;
                    }
                    else
                        begin=mid+1;
                }
            }
        }
        
        return res;
    }
};**
```

## Solution:

**We use Binary Search ,but we have to find the begin and end.**

---

 **—>if we find target ⇒ check whether it is begin(position=0 or nums[ position-1 ] < target).**

 **—> if we find target ⇒ check whether it is end(position=nums.size()-1 or nums[ position+1 ] > target).**

---