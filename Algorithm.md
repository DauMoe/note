# Table of contents
 - [Two sum](#two-sum)
 - [Add Two Numbers](#add-two-numbers)

<br/><br/>

## Two sum
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

## Add Two Numbers
 **Ques:** https://leetcode.com/problems/add-two-numbers/  
 **Solution:**  
  - As a primary student. Just take each element in the same index of each ListNode and calculate sum, don't forget the remainder value  
  - By the way, my solution takes a lot of memory and time to run (runtime) so it doesn't the most effective way but the idea is the same  
 
 **Code:**  (My solution)
 ```ts
  /**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function createListNode(arr: number[]): ListNode {
  let currentNode: ListNode | null = null;
  let prevNode: ListNode | null = null;
  for (const val of arr.reverse()) {
    currentNode = new ListNode(val, prevNode);
    prevNode = currentNode;
  }
  return currentNode;
}

function addTwoNumbers(l1: ListNode | null, l2: ListNode | null): ListNode | null {
  if (!l1) return l2;
  if (!l2) return l1;
  let l1Array: number[] = [], l2Array: number[] = [];
  do {
    l1Array.push(l1.val);
    l1 = l1.next;
  } while(l1 !== null);
  do {
    l2Array.push(l2.val);
    l2 = l2.next;
  } while(l2 !== null);
  
  if (l1Array.length < l2Array.length) {
    //Swap to make sure l1Array length is longer than l2Array
    [l1Array, l2Array] = [l2Array, l1Array];
  }

  let Remainder: number = 0;
  let resultArray: number[] = [];
  for (const [index, val] of l1Array.entries()) {
    let resultThisLoop: number;
    if (index < l2Array.length) {
      resultThisLoop = val + l2Array[index] + Remainder;
    } else {
      resultThisLoop = val + Remainder;
    }
    Remainder = Math.floor(resultThisLoop/10);
    resultArray.push(resultThisLoop%10);
  }
  if (Remainder != 0) resultArray.push(Remainder);
  return createListNode(resultArray);
};
 ```
