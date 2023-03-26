# Table of contents


### Two sum:
  **Ques:** https://leetcode.com/problems/two-sum/  
  **Requirements:**  
    - complexity: less than O(n^2)  
    - range:  2 <= nums.length <= 104  **&** -109 <= nums[i] <= 109 **&** -109 <= target <= 109  
  **Solution**  
      - Using a `Object` or `Map` as a storage to keep value (Schema: ```{ value: index }```)  
      - Loop throw each item in `nums` array  
      - We call `shouldBeExist` = `target` - `number` (each item in `nums` array)  
      - Check expected number existed in storage ? (YES) return [`current index`, `storage index`] : store value into storage object and jump to next round
      - Bad scenario: return [-1, -1]
  **Talk about complexity**  
    - One loop (loop throw `nums`): O(n)
    - `has` and `get` method of Map: ??? (updating...)
    
  **Code**
  ```ts
  function twoSum(nums: number[], target: number): number[] {
    const memo = new Map<number, number>();// Map schema: value => index
    for (const [index, num] of nums.entries()) {
      const shouldBeExist = target - num;
      if (memo.has(shouldBeExist)) {
        return [memo.get(shouldBeExist), index];
      } else {
        memo.set(num, index);
      }
    }
    return [-1, -1];
  };
  ```
