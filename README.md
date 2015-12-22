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

<!-- HTML generated using hilite.me --><div style="background: #272822; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; color: gray; line-height: 125%"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #66d9ef">def</span> <span style="color: #a6e22e">removeDuplicates</span><span style="color: #f8f8f2">(nums):</span>
    <span style="color: #e6db74">&quot;&quot;&quot;</span>
<span style="color: #e6db74">    :type nums: List[int]</span>
<span style="color: #e6db74">    :rtype: int</span>
<span style="color: #e6db74">    &quot;&quot;&quot;</span>
    
    <span style="color: #66d9ef">for</span> <span style="color: #f8f8f2">i</span> <span style="color: #f92672">in</span> <span style="color: #f8f8f2">range(</span><span style="color: #ae81ff">0</span><span style="color: #f8f8f2">,</span> <span style="color: #f8f8f2">len(nums)):</span>
        
        <span style="color: #f8f8f2">j</span> <span style="color: #f92672">=</span> <span style="color: #f8f8f2">len(nums)</span><span style="color: #f92672">-</span><span style="color: #ae81ff">1</span>
        
        <span style="color: #66d9ef">while</span> <span style="color: #f8f8f2">j</span> <span style="color: #f92672">&gt;</span> <span style="color: #f8f8f2">i:</span>
            <span style="color: #66d9ef">if</span> <span style="color: #f8f8f2">nums[i]</span> <span style="color: #f92672">==</span> <span style="color: #f8f8f2">nums[j]:</span>
                <span style="color: #f8f8f2">nums</span><span style="color: #f92672">.</span><span style="color: #f8f8f2">remove(nums[j])</span>
            <span style="color: #f8f8f2">j</span><span style="color: #f92672">-=</span><span style="color: #ae81ff">1</span>
    
    <span style="color: #66d9ef">return</span> <span style="color: #f8f8f2">len(nums)</span>
</pre></td></tr></table></div>

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
<!-- HTML generated using hilite.me --><div style="background: #272822; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><table><tr><td><pre style="margin: 0; color: gray; line-height: 125%"> 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15</pre></td><td><pre style="margin: 0; line-height: 125%"><span style="color: #f8f8f2">public</span> <span style="color: #f8f8f2">static</span> <span style="color: #f8f8f2">int</span> <span style="color: #f8f8f2">removeDuplicates(int[]</span> <span style="color: #f8f8f2">nums)</span> <span style="color: #f8f8f2">{</span>
    
    <span style="color: #66d9ef">if</span> <span style="color: #f8f8f2">(nums</span><span style="color: #f92672">.</span><span style="color: #f8f8f2">length</span> <span style="color: #f92672">==</span> <span style="color: #ae81ff">0</span><span style="color: #f8f8f2">)</span> <span style="color: #66d9ef">return</span> <span style="color: #ae81ff">0</span><span style="color: #f8f8f2">;</span>
    
    <span style="color: #f8f8f2">int</span> <span style="color: #f8f8f2">i</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">0</span><span style="color: #f8f8f2">;</span>
    <span style="color: #f8f8f2">int</span> <span style="color: #f8f8f2">duplicateCount</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">0</span><span style="color: #f8f8f2">;</span>

    <span style="color: #66d9ef">for</span> <span style="color: #f8f8f2">(int</span> <span style="color: #f8f8f2">j</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">1</span><span style="color: #f8f8f2">;</span> <span style="color: #f8f8f2">j</span> <span style="color: #f92672">&lt;</span> <span style="color: #f8f8f2">nums</span><span style="color: #f92672">.</span><span style="color: #f8f8f2">length;</span> <span style="color: #f8f8f2">j</span><span style="color: #f92672">++</span><span style="color: #f8f8f2">)</span> <span style="color: #f8f8f2">{</span>
        <span style="color: #66d9ef">if</span> <span style="color: #f8f8f2">(nums[i]</span> <span style="color: #f92672">==</span> <span style="color: #f8f8f2">nums[j])</span> <span style="color: #f8f8f2">{</span>
            <span style="color: #f8f8f2">duplicateCount</span><span style="color: #f92672">++</span><span style="color: #f8f8f2">;</span>
        <span style="color: #f8f8f2">}</span>
        <span style="color: #f8f8f2">i</span><span style="color: #f92672">++</span><span style="color: #f8f8f2">;</span>
    <span style="color: #f8f8f2">}</span>
    <span style="color: #66d9ef">return</span> <span style="color: #f8f8f2">nums</span><span style="color: #f92672">.</span><span style="color: #f8f8f2">length</span> <span style="color: #f92672">-</span> <span style="color: #f8f8f2">duplicateCount;</span>
<span style="color: #f8f8f2">}</span>
</pre></td></tr></table></div>


<div style="font-family: Arial, Verdana, Sans-serif;">
	<h2 style="color: gray">Solution 2</h2>
	<p>In this solution, the array is mutated such that the list of integers with duplicates removed ends up in the front of the array while duplicates are pushed toward the back. i is the slow-running pointer, and j is the fast-running pointer. j is incremented on each iteration while i is only conditionally incremented, subject to the condition that nums[i] != nums[j]. In other words, if an integer has a number of duplicates, say, in the array […,3, 3, 3, 3, 7,...], then i will stay with the first occurrence of the duplicate (the second 3) while j increments and skips over every other occurrence of that integer until it comes across the next new integer (7) in the array, at which point, the second 3 will be replaced by the value of 7, and i will be incremented to the third 3. </p>
</div>

<div style="background: #272822; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;">
	<pre style="margin: 0; line-height: 125%">
		<span style="color: #f8f8f2">public</span> 
		<span style="color: #f8f8f2">int</span> 
		<span style="color: #f8f8f2">removeDuplicates(int[]</span> 
		<span style="color: #f8f8f2">nums)</span> 
		<span style="color: #f8f8f2">{</span>
    
    <span style="color: #66d9ef">if</span> 
	<span style="color: #f8f8f2">(nums</span>
	<span style="color: #f92672">.</span>
	<span style="color: #f8f8f2">length</span> 
	<span style="color: #f92672">==</span> 
	<span style="color: #ae81ff">0</span>
	<span style="color: #f8f8f2">)</span> 
	<span style="color: #66d9ef">return</span> 
	<span style="color: #ae81ff">0</span><span style="color: #f8f8f2">;</span>
    
    <span style="color: #f8f8f2">int</span> 
	<span style="color: #f8f8f2">i</span> 
	<span style="color: #f92672">=</span> 
	<span style="color: #ae81ff">0</span>
	<span style="color: #f8f8f2">;</span>
    <span style="color: #66d9ef">for</span> 
	<span style="color: #f8f8f2">(int</span> 
	<span style="color: #f8f8f2">j</span> 
	<span style="color: #f92672">=</span> 
	<span style="color: #ae81ff">1</span>
	<span style="color: #f8f8f2">;</span> 
	<span style="color: #f8f8f2">j</span> 
	<span style="color: #f92672">&lt;</span> 
	<span style="color: #f8f8f2">nums</span>
	<span style="color: #f92672">.</span>
	<span style="color: #f8f8f2">length;</span> 
	<span style="color: #f8f8f2">j</span>
	<span style="color: #f92672">++</span>
	<span style="color: #f8f8f2">)</span> 
	<span style="color: #f8f8f2">{</span>
        <span style="color: #66d9ef">if</span> 
		<span style="color: #f8f8f2">(nums[j]</span> 
		<span style="color: #f92672">!=</span> 
		<span style="color: #f8f8f2">nums[i])</span> 
		<span style="color: #f8f8f2">{</span>
            <span style="color: #f8f8f2">i</span>
			<span style="color: #f92672">++</span>
			<span style="color: #f8f8f2">;</span>
            <span style="color: #f8f8f2">nums[i]</span> 
			<span style="color: #f92672">=</span> 
			<span style="color: #f8f8f2">nums[j];</span>
        <span style="color: #f8f8f2">}</span>
    <span style="color: #f8f8f2">}</span>
    <span style="color: #66d9ef">return</span> 
	<span style="color: #f8f8f2">i</span> 
	<span style="color: #f92672">+</span> 
	<span style="color: #ae81ff">1</span>
	<span style="color: #f8f8f2">;</span>
<span style="color: #f8f8f2">}</span>
</pre></div>

