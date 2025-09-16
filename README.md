# Leetcode-202.-Happy-Number
# Description
Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.

Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.

Those numbers for which this process ends in 1 are happy.

Return true if n is a happy number, and false if not.
# Solution
We have been given an integer number n and we have to prove whether it is a happy number ot not.

A happy number is a number whose sumofsquares is equal to 1 .

Example 1:

Input: n = 19

Output: true

Explanation:

Start: n = 19, visit = {}

→ Sum of squares: 1² + 9² = 82 → n = 82.

Now: n = 82, visit = {19}

→ Sum of squares: 8² + 2² = 68 → n = 68.

Now: n = 68, visit = {19, 82}

→ Sum of squares: 6² + 8² = 100 → n = 100.

Now: n = 100, visit = {19, 82, 68}

→ Sum of squares: 1² + 0² + 0² = 1 → n = 1.

Example 2:

Input: n = 2

Output: false

Explanation: 

Start: n = 2, visit = {}

→ Sum of squares: 2² = 4.

Now: n = 4, visit = {2}

→ Sum of squares: 4² = 16.

Now: n = 16, visit = {2, 4}

→ Sum of squares: 1² + 6² = 37.

37 → 58 → 89 → 145 → 42 → 20 → 4

Hence an endless loop is formed in this case.

To avoid this loop we can use a hashmap to keep track of the elements which have already been used .

# Algorithm
ishappy() function:
1. Create an empty hashset visit which keeps track of unique numbers used only once.
2. Check if the number n is already in visit , if it is not there then add it to the set visit .
3. Check if the number n is equal to 1 , if it is then return True.
4. Else return False

sumofsquares() function:
1. To extract the digits from the number: find the remainder of the number by dividing it by 10.
2. Then find out the square of that digit and add it to the total
3. To repeat the same operation with the next digit divide it by 10 .
4. Return the total to the ishappy() function to check whether it is happy number or not.
# Code
class Solution:

    def isHappy(self, n: int) -> bool:
    
        visit=set()

        while n not in visit:
            visit.add(n)
            n=self.sumofsquares(n)

            if n==1:
                return True
        return False
        
    def sumofsquares(self,n:int) -> int:
        total=0

        while n>0:
            digit=n%10
            digit=digit**2
            total+=digit
            n=n//10
        return total
# Complexity
Time Complexity: 

O(log n) per transformation, since extracting digits is proportional to the number of digits in n.
In practice, the sequence converges quickly, so runtime is efficient.

Space Complexity: 

O(log n) for the set to store visited numbers.
