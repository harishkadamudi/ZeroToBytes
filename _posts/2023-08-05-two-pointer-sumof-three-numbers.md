---
title: Sum of Three Values
author: harish
date: 2023-08-09 15:32:00 +0530
categories: [golang, dsa, two-pointer]
tags: [two-pointer,someof-three-numbers]
pin: false
---

## Problem statement
Given an array of integers, nums, and an integer value, target, determine if there are any three integers in nums whose sum is equal to the target, that is, nums[i] + nums[j] + nums[k] == target. Return TRUE if three such integers exist in the array. Otherwise, return FALSE.

## Condition

> Note: A valid triplet consists of elements with distinct indexes. This means, for the triplet nums[i], nums[j], and nums[k], i ≠ j, i ≠ k and j ≠ k.

## Code

```golang

package main

import (
	"fmt"
	"sort"
	"strings"
)

// findSumOfThreeNumbers
// return three number which are sums to the target number
// we can return an array, trying to keep it simple and clean
func findSumOfThreeNumbers(target int, nums []int) (first, second, last int) {

	low, sum, high := 0, 0, 0
	// Sort the given array
	sort.Sort(sort.IntSlice(nums))
	for i := 0; i < len(nums)-2; i++ {
		low = i + 1
		high = len(nums) - 1
		// since low and high be same number
		for low < high {
			sum = nums[i] + nums[low] + nums[high]
			// The sum of the triplet equals the target
			if sum == target {
				return nums[i], nums[low], nums[high]
			} else if sum <= target {
				// The sum of the triplet is less than target, so move the low pointer forward
				low += 1
			} else {
				// The sum of the triplet is greater than target, so move the high pointer backward
				high -= 1
			}
		}
	}
	return 0, 0, 0
}

func main() {
	numsLists := [][]int{
		{3, 7, 1, 2, 8, 4, 5},
		{-1, 2, 1, -4, 5, -3},
		{2, 3, 4, 1, 7, 9},
		{1, -1, 0},
		{2, 4, 2, 7, 6, 3, 1},
	}
	tList := []int{10, 7, 20, -1, 8}
	for i, nList := range numsLists {
		fmt.Printf("%d. Input array: %s\n", i+1, strings.Replace(fmt.Sprint(nList), " ", ", ", -1))
		first, second, last := findSumOfThreeNumbers(tList[i], nList)
		if first != 0 {
			fmt.Printf("   Sum for %d exists\n and numbers are %d, %d, %d \n ", tList[i], first, second, last)
		} else {
			fmt.Printf("   Sum for %d does not exist\n", tList[i])
		}
		fmt.Printf("%s\n", strings.Repeat("-", 100))
	}
}


```