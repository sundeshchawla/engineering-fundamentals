# Hashing Pattern

## Core idea
Use Hashmap to tradeoff space for time.
When we need to lookup something. reducing O(n²) lookups to O(n).

By storing what you have seen and checking it instantly.

## When to recognise it
- Find two elements that...
- Count frequency of ...
- Group elements by ..
- Anytime I need to check "have I seen this value before .. "

## Template (C++)
unordered_map<int,int> seenThis;

for(int i=0; i< arr.size(); i++)
{
	int diff = target - arr[i];
	if(seen.contains(diff)){
		// do something with it.
	}
	
	seen[nums[i]] = i;
}



## Time/Space
Time: O(n) — one pass
Space: O(n) — worst case all elements in map

## Problems using this pattern
- Two Sum → store value:index, look for complement
- Group Anagrams → store sorted_word:list_of_words
- Top K Frequent → frequency map + heap

## Edge cases to remember
- What if the same element can't be used twice? (check index)
- What if no solution exists? (return -1 or empty)

## My mistakes
- [3 Apr] Forgot to check seen BEFORE adding to map → wrong index returned