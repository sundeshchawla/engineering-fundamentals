Valid_Palindrome

Date: 3 Apr 2026
Difficulty: Easy
Pattern: → TwoPointers
Language: C++

## Approach
use std library
use isalnum(char) to identify valid characters else move two pointers ahead
use tolower(char) to compare the values as its case insensitive
use a single loop for max optimized

run 1 loop only

	check if start is not alnum, 
		if yes then start++;

	else check if end is not alnum, 
		if yes then end--;
	
	else
		compare start and end values
			if not equal return false
			
		
		start++;
		end--;
		

return true if loop ends successfully. that means no values were unequal therefore valid palindrome
	
	
## My code
class Solution {
public:
    bool isPalindrome(string s) {
     int start = 0;
     int end  = s.size()-1;

     while(start<end){
        if(!isalnum(s[start])){
            start++;
        }

        else if(!isalnum(s[end])){
            end--;
        }
        
        else {
            if(tolower(s[start]) != tolower(s[end]))
            return false;

            start++;
            end--;
        }
     }

     return true;   
    }
};

## Time: O(n)  |  Space: O(1)

## What tripped me
// I didnt know what method to use for alnum. now i know use std::alnum(char)
// same i didnt know for lower. now i used std::tolower(char)
//also i created a separate method for removing non alphanumeric string but it takes more time
because of string creation and all. therefore did everything in same loop iteration.



## Follow-up questions to think about

1. What if the string is empty ("") — does your code handle it?
   (Trace through mentally: start=0, end=-1, while(0 < -1) is false → returns true. 
   Is empty string a valid palindrome? Yes. Good.)

2. What if ALL characters are non-alphanumeric, like "!@#$%"?
   (Both pointers skip everything, loop ends, returns true.
   Is that correct? Interviewers love this edge case.)

3. Valid Palindrome II (LeetCode #680) — harder follow-up:
   Given a string, can you make it a palindrome by removing AT MOST one character?
   (Your current solution can't handle this — think about what changes.)

4. How would you solve this without the std library (isalnum, tolower)?
   Write your own isAlphaNumeric(char c) using ASCII ranges:
   a-z: 97–122, A-Z: 65–90, 0-9: 48–57
   Interviewers occasionally ask you to avoid std helpers.

5. What if the input is not a string but a stream of characters —
   you can only read it once and can't index backwards?
   (You can no longer use two pointers. What data structure helps? → Stack/Deque)



