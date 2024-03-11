---
title: Parallel Programming with C++
published: true
Tags: ["programming","cpp"]
image: /images/cpp-parallel-stl.jpg
date: 2021-07-21
author: Hatim
keywords: C++,cpp,stl,parallel,programming,program,code,execution,vector,standard,template,library,cppreferen,sequence,sequenced,policy,unsequenced,vectorize,c++17
description: A performance optimization lesson will teach you about C++17 parallel algorithms and how to improve C++ code performance using this library and the Intel Parallel STL
---

# C++17 - New Parallel Algorithm of STL

C++17 introduces parallel algorithms. However, there aren't many implementations where the additional functionalities can be used.

The concept is straightforward. More than 100 algorithms are included in the Standard Template (STL) for searching, counting, and manipulating ranges and their constituents. 69 of them are overloaded in C++17, and a few new ones are added. A so-called execution policy can be used to invoke the overloaded and new algorithms. You can specify whether the method should run sequentially, parallelly, or parallel and vectorized by using the execution policy.

## C++ Parallel Algorithm of STL

There are almost 100 algorithms in the Standard Template Library for finding, counting, and manipulating ranges and their elements. C++17 adds new overloads to 69 of them and adds new ones to others. A so-called execution policy can be used to launch overloaded and new algorithms. You can indicate whether the method should run sequentially, in parallel, or in parallel with vectorization using an execution policy. You must add the header `<execution>` if you want to use the execution policy.


## Execution Policy of Parallel Algorithm

**Three execution policies are defined in the C++17 standard:**

- `std::execution::sequenced_policy` : sequential execution
- `std::execution::parallel_policy` : Parallel execution
- `std::execution::parallel_unsequenced_policy` : Parallel and unsequenced execution

The important thing to remember is that the execution policies are permissions rather than obligations. Each library implementation may decide what and how much can be parallelized.

To use parallel algorithms, you need at least forward iterators.

Here is code snippet of `sort` algorithm which applies all execution policies.

```cpp
#include <vector> //for vector
#include <algorithm> // for sort
#include <execution> // for parallel execution


int main() {

std::vector<int> vec  = {21,34,53,98,22,7,244,52,60,72,89,44,57};

//standart sequential sort
std::sort(vec.begin(),vec.end());

// sequential execution
std::sort(std::execution::seq,vec.begin(),vec.end());

// permittin parallel execution
std::sort(std::execution::par,vec.begin(),vec.end());

// permitting parallel and vectorized execution
std::sort(std::execution::par_unseq,vec.begin(),vec.end());

}

```
The example demonstrates that the classic variant of `std::sort` can still be used . Furthermore, in C++17, you can specify whether you want to utilise the **sequential** , **parallel** , or **parallel and vectorized**  versions.


## Exception

If an exception occurs while using an algorithm with an execution policy, the function `std::terminate` is invoked. The installed `std::terminate::handler` is called by `std::terminate`. As a result, the `std::abort` function is invoked by default, resulting in abnormal programme termination. The handling of exceptions distinguishes between the invocation of an algorithm without an execution policy and the invocation of an algorithm with a sequential `std::execution::seq` execution policy. The exception is propagated when the algorithm is invoked without an execution policy, and so the exception can be handled.

With C++17, 69 STL algorithms received new overloads, and new algorithms were introduced.


## Algorithm

The table below shows whether parallel and unsequenced execution are supported by each of the C++17 algorithms that accept execution policies. The use of an unsupported algorithm and execution policy will result in sequential execution.

<table style="width:100%">
<tbody>
<tr >
<th><p>Algorithm</p></th>
<th><p>Implementation</p></th>
</tr>

<tr >
<td><p><code>adjacent_difference</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>adjacent_find</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>all_of</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>any_of</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>copy_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>copy_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>count</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>count_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>destroy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>destroy_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>equal</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>exclusive_scan</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>fill</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>fill_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>find</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>find_end</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>find_first_of</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>find_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>find_if_not</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>for_each</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>for_each_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>generate</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>generate_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>includes</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>inclusive_scan</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>inplace_merge</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>is_heap</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>is_heap_until</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>is_partitioned</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>is_sorted</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>is_sorted_until</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>lexicographical_compare</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>max_element</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>merge</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>min_element</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>minmax_element</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>mismatch</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>move</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>none_of</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>nth_element</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>partial_sort</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>partial_sort_copy</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>partition</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>partition_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>reduce</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>remove</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>remove_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>remove_copy_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>remove_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>replace</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>replace_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>replace_copy_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>replace_if</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>reverse</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>reverse_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>rotate</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>rotate_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>search</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>search_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>set_difference</code></p></td>
<td></td>
<td> </td>
</tr>
<tr >
<td><p><code>set_intersection</code></p></td>
<td></td>
<td> </td>
</tr>
<tr >
<td><p><code>set_symmetric_difference</code></p></td>
<td></td>
<td> </td>
</tr>
<tr >
<td><p><code>set_union</code></p></td>
<td></td>
<td> </td>
</tr>
<tr >
<td><p><code>sort</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>stable_sort</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>stable_partition</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>swap_ranges</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>transform</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>transform_exclusive_scan</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>transform_inclusive_scan</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>transform_reduce</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_copy_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_default_construct</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_default_construct_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_fill</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_fill_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_move</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_move_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_value_construct</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>uninitialized_value_construct_n</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
<tr >
<td><p><code>unique</code></p></td>
<td></td>
<td><p>parallel</p></td>
</tr>
<tr >
<td><p><code>unique_copy</code></p></td>
<td></td>
<td><p>parallel, unsequenced</p></td>
</tr>
</tbody>
</table>


### References
- https://en.cppreference.com/
- https://software.intel.com/content/w/develop/articles/get-started-with-parallel-stl.html
- https://www.modernescpp.com/index.php/c-17-new-algorithm-of-the-standard-template-library