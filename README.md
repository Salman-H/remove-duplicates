# remove-duplicates
A few approaches to the problem of removing duplicates from a sorted array.

<div style="font-family: Arial, Verdana, Sans-serif;">
	<h3>Problem Statement</h3>
	<p>In this problem, we are asked to write a function that removes duplicate integers from a sorted array such that every integer occurs only once. This is to be done in O(n) time and in constant memory i.e. without allocating memory for a new array. The function takes as input, a sorted array of ints, and returns the length (int) of an array with the duplicates removed. e.g. an input of [1, 1, 2, 3, 3, 3, 7] will return 4, since the array with duplicates removed will be [1, 2, 3, 7].</p> 
</div>

<hr>

<div style="font-family: Arial, Verdana, Sans-serif;">
	<h3>Unsorted Array – O(n<sup>2</sup>)</h3>
	<p>Here is a possible solution in Python for an unsorted array in O(n2). It takes as input, an unsorted array, and returns the length of this array with duplicates removed.</p>
</div>

<img src="https://cloud.githubusercontent.com/assets/5385065/11949829/1c1b2928-a851-11e5-8e62-3a6f62f0310d.PNG"></img>

<div>
	<p>If the array is unsorted, a duplicate can occur anywhere in the array. So, in this possible solution, every integer has to be compared with every other integer. Two pointers are used, i and j, where j is the fast-running pointer, and i is the slow-running pointer. Since arrays or lists in python are mutable, the duplicates can actually be removed in this approach so the array mutates during execution, and after execution finishes, the length of the resulting array is returned. For every iteration of pointer i, pointer j compares all integers (greater than i and less than length of array) to i and removes any duplicates. After each iteration of i (before the while loop), the array could have shrunk, so pointer j has to be reset (reinitialized) to the last index of the array at the time.</p>
</div>

<hr>

<div style="font-family: Arial, Verdana, Sans-serif;">
	<h3>Sorted Array Two Pointer technique in Java – O(n)</h3>
	<p>If the array is sorted, we exploit the fact that the duplicates only appear consecutively. The goal is to use the two pointer technique to get the result in O(n) time. Arrays are immutable in Java so the input array cannot be changed without allocating memory for a new one; which is not allowed! The method has to return the desired result in constant memory.</p>
</div>

<div style="font-family: Arial, Verdana, Sans-serif;">
	<h3 style="color: gray">Solution 1</h3>
	<p>In this possible solution, pointers i and j are incremented indiscriminately where they form the edges of a 2 digit window which is slid across the array in each iteration to check for duplicates. Since these pointers both run at the same speed, instead of one being a fast-running or a slow-running pointer, this might not be categorized as a true two pointer technique. The number of duplicates are counted and subtracted from the length of the original array. This gives the length of the array if the duplicates were removed.</p>
</div>

<img src="https://cloud.githubusercontent.com/assets/5385065/11949831/1e639a44-a851-11e5-8342-30ebc39f542a.PNG"></img>

<div style="font-family: Arial, Verdana, Sans-serif;">
	<h3 style="color: gray">Solution 2</h3>
	<p>In this solution, the array is mutated such that the list of integers with duplicates removed ends up in the front of the array while duplicates are pushed toward the back. i is the slow-running pointer, and j is the fast-running pointer. j is incremented on each iteration while i is only conditionally incremented, subject to the condition that nums[i] != nums[j]. In other words, if an integer has a number of duplicates, say, in the array […,3, 3, 3, 3, 7,...], then i will stay with the first occurrence of the duplicate (the second 3) while j increments and skips over every other occurrence of that integer until it comes across the next new integer (7) in the array, at which point, the second 3 will be replaced by the value of 7, and i will be incremented to the third 3. </p>
</div>

<img src="https://cloud.githubusercontent.com/assets/5385065/11949833/207c7814-a851-11e5-9abf-560ae5d87268.PNG"></img>

