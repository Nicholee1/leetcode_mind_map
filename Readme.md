# Hot 100 解题思路

![mind_map](lc_hot100_mind_map_v1.png)
- [回溯](#%E5%9B%9E%E6%BA%AF)
- [二分搜索](#%E4%BA%8C%E5%88%86%E6%90%9C%E7%B4%A2)
- [二叉树](#%E4%BA%8C%E5%8F%89%E6%A0%91)
	- [前序获取父节点信息，遍历二叉树得到答案（回溯）](#%E5%89%8D%E5%BA%8F%E8%8E%B7%E5%8F%96%E7%88%B6%E8%8A%82%E7%82%B9%E4%BF%A1%E6%81%AF%EF%BC%8C%E9%81%8D%E5%8E%86%E4%BA%8C%E5%8F%89%E6%A0%91%E5%BE%97%E5%88%B0%E7%AD%94%E6%A1%88%EF%BC%88%E5%9B%9E%E6%BA%AF%EF%BC%89)
	- [中序处理BST问题](#%E4%B8%AD%E5%BA%8F%E5%A4%84%E7%90%86BST%E9%97%AE%E9%A2%98)
	- [后序利用好返回值获取子树返回的信息，拆解问题得到答案（动态规划）](#%E5%90%8E%E5%BA%8F%E5%88%A9%E7%94%A8%E5%A5%BD%E8%BF%94%E5%9B%9E%E5%80%BC%E8%8E%B7%E5%8F%96%E5%AD%90%E6%A0%91%E8%BF%94%E5%9B%9E%E7%9A%84%E4%BF%A1%E6%81%AF%EF%BC%8C%E6%8B%86%E8%A7%A3%E9%97%AE%E9%A2%98%E5%BE%97%E5%88%B0%E7%AD%94%E6%A1%88%EF%BC%88%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%89)
	- [二叉树构造](#%E4%BA%8C%E5%8F%89%E6%A0%91%E6%9E%84%E9%80%A0)
	- [层序遍历](#%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86)
	- [二叉树递归](#%E4%BA%8C%E5%8F%89%E6%A0%91%E9%80%92%E5%BD%92)
- [链表](#%E9%93%BE%E8%A1%A8)
	- [双指针](#%E5%8F%8C%E6%8C%87%E9%92%88)
	- [快慢指针](#%E5%BF%AB%E6%85%A2%E6%8C%87%E9%92%88)
	- [递归](#%E9%80%92%E5%BD%92)
- [排序](#%E6%8E%92%E5%BA%8F)
	- [冒泡排序](#%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F)
	- [选择排序](#%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F)
	- [插入排序](#%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)
	- [归并排序](#%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F)
	- [快速排序](#%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)
- [动态规划](#%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
	- [一维动态规划：](#%E4%B8%80%E7%BB%B4%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%9A)
	- [二维动态规划：](#%E4%BA%8C%E7%BB%B4%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92%EF%BC%9A)
		- [二维数组遍历](#%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E9%81%8D%E5%8E%86)
		- [子串问题：](#%E5%AD%90%E4%B8%B2%E9%97%AE%E9%A2%98%EF%BC%9A)
		- [序列问题](#%E5%BA%8F%E5%88%97%E9%97%AE%E9%A2%98)
		- [背包问题：](#%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%98%EF%BC%9A)
- [贪心](#%E8%B4%AA%E5%BF%83)
- [双指针](#%E5%8F%8C%E6%8C%87%E9%92%88)
- [哈希](#%E5%93%88%E5%B8%8C)
- [技巧](#%E6%8A%80%E5%B7%A7)
- [堆栈](#%E5%A0%86%E6%A0%88)
- [二维矩阵](#%E4%BA%8C%E7%BB%B4%E7%9F%A9%E9%98%B5)

## 回溯
Template：
```python
def backTracking(path, choice_list):
    if(meet finish condition): #终止条件
        result.add(path)
        return

    for(choice in choice_list): #选择列表
        make a choice
        backTracking(path, choice_list) # 选择路径
        undo the choice
```

* 手机数字建枚举[17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)一个list维护数字键的对应关系，套用模板，对每一个数字键进行枚举
* 枚举括号[22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) 除了枚举，还需要满足括号的规则，所以需要剪枝，右括号不能出现在左括号前。所以需要两个变量left right记录左右括号使用情况
* 候选数组能够拼凑target的所有结果[39. Combination Sum](https://leetcode.com/problems/combination-sum/)数字可以重用，所以选择列表每次从i=index本身算起，注意剪枝以及返回list时深拷贝结果，否则引用的list会持续被修改
* 全排列[46. Permutations](https://leetcode.com/problems/permutations/)数组的全排列，因为是全排列，所以每个元素都可能出现在任一位置上，所以需要一个**used[i]数组**记录有没有使用过，boolean used[n]默认就都是false的
* 全子集[78. Subsets](https://leetcode.com/problems/subsets/)与全排列不同，只要求子集，所以会更贴切模板，添加结果要在终止条件之前，for循环从index开始，但注意选择路径时用i+1而不是index+1
* 单词搜索[79. Word Search](https://leetcode.com/problems/word-search/)很恶心，上下左右遍历，重要一点不能走回头路，所以要对刚走的值进行修改，以免走回去。
* **找出所有回文的子串**[131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/) 由于每组返回结果都是一组子串，所以当index== s.length时，一块返回一个List < String>, 回溯时，先判断**index到i是不是回文**，如果是，就把s.substring(index,i+1)存入结果，然后回溯判断，回溯完记得删除最后的元素。

## 二分搜索

Template：
```java
int binarySearch(int[] nums, int target){
	int left=0, right=nums.length-1;
	while(left<=right){
		int mid=left+(right-left)/2;
		if(nums[mid]==target){
			return mid;
		}else if(nums[mid]<target){
			left=mid+1;
		}else if(nums[mid]>target){
			right=mid-1;
		}
	}
	return -1;
}
```

* 寻找target应该存在列表中的位置[35. Search Insert Position](https://leetcode.com/problems/search-insert-position/)比较常规的二分搜索
* 找到旋转数组中的最小值[153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)用最后一个值进行二分判断，注意边界，nums[mid]<=nums[length-1]时，right=mid避免把最小值过滤出去了，大于时则可以安心left=mid+1，while条件是left < right避免死循环
* 在一个旋转数组中搜索[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) 有序数组被旋转过一次，在这种数组里搜索一个元素。主要思路是用数组最后一个元素二分搜索找出最小值的位置（153.），这样就切开了两个单调有序的数组，然后target如果大于等于最后一个值就在前边的数组找，小于就在后边的数组找
* 有序数组找target的左右边界 [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) 二分搜索的nums[mid]== target条件中用两个指针探测边界即可
* 在有序二维数组中搜索target[74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/) 先对第一列进行二分，找到对应行后再横向二分搜索，注意！！！！while(left<right)和**left=mid搭配时需要向上取整**，也就是mid=left+(right-left+1)/2;
## 二叉树
### 前序获取父节点信息，遍历二叉树得到答案（回溯）
* 反转二叉树[226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)在前序位置调转左右子树
* **二叉树右视角** [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)和114拉平二叉树成链表类似，要求右子树的值，所以前序遍历时需要右在先，左在后。当从0开始的currDepth等于res.size时，说明刚到下一层，插入结果
* 有序数组构建BST[108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/) 二分找一个中点作为root，左子树就是left～mid-1，右子树就是mid+1～right
### 中序处理BST问题
* 验证是否是BST树[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) 一个long型pre记录前一个值，中序遍历，pre应该一直比root的值小
* 中序遍历 [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
* 第k个最小值在BST树[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)限定是BST树，中序遍历即可
### 后序利用好**返回值**获取子树返回的信息，拆解问题得到答案（动态规划）
* 反转二叉树 [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/) 利用好返回值，后序位置每个节点左右子树对调
* 树的深度[104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)  return Math.max(left,right)+1
*  **拉平二叉树成链表** [114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/) 由于拉成右节点连接，所以要按照右节点，根，左节点顺序连接，需要调转左右子树遍历顺序，然后维护一个全局的pre初始为空记录上一个被连接的节点，在后序位置root.left=null/root.right=pre/pre=root
* **最近公共祖先**：[236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) 就是找某个root节点它的左右子树是否包含了给定的两个值。在前序位置，如果值相等直接返回，覆盖了根节点就是给定值的情况。在后序位置，递归的左右子树都不为空，则返回root，即是祖先。否则就返回左子树或右子树.
* 二叉树中的最长距离：[543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)利用树的深度，在深度计算的代码中，在后序位置比较maxLength和left+right中最大的，因为left和right已经是左右子树各自的最长距离了
### 二叉树构造
* 前序+中序：map存储中序值和索引，用来计算边界leftSize=index-instart，preStart>preEnd 作为终止条件，根节点创建后，左右节点分别为root.left=build(preorder,preStart+1,preStart+leftSize,inorder,inStart,index-1)
  root.right=build(preorder,preStart+leftSize+1,preEnd,inorder,index+1,inEnd)
* 后序+中序：map存储中序值和索引，用来计算边界leftSize=index-instart，inStart>inEnd 作为终止条件，根节点创建后，左右节点分别为，roo.left=build(inorder,inStart,index-1,postorder,postStart,postStart+leftSize-1)，build(inorder,index+1,inEnd,postorder,postStart+leftSize,postEnd-1)
* 前序+后序：map存储后序值和索引，用来计算边界leftSize=index-postStart+1; preStart>preEnd 作为终止条件，根节点创建后，*还需用前序第二个元素作为左子树根节点* 左右节点分别为roo.left=build(preorder,preStart+1,preStart+leftSize,postorder,postStart,index)，build(preorder,preStart+leftSize+1,preEnd,postorder,jndex+1,postEnd-1)
### 层序遍历
``` java
void traverse (TreeNode root)}{
	if(root==null) return;
	queue=new LinkList<TreeNode>();
	queue.add(root);
	while(!queue.isEmpty()){
		size=queue.size()
		for(int i=0;i<size;++i){
			node=queue.poll()
			if(!node.left==null){
				queue.add(node.left)
			}
			if(!node.right==null){
				queue.add(node.right)
			}
		}
		
	}
}
```
### 二叉树递归
* [101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)判断树是不是对称的，就是判断左右子树是不是对称的，以左右节点为参数构建辅助函数isSym(left,right),  isSym(left.left,right.right)&&isSym(left.right,right.left)都为真是才是对称的
* **路径和**[437. Path Sum III](https://leetcode.com/problems/path-sum-iii/) 找出树中所有和为sum的可能。拆解问题，所有可能就是包含root节点的可能+包含左右子节点的可能,这里左右子节点必须是父函数，否则只能探测到紧挨着根节点的左右子树。针对某一个节点开始的可能数量，则是自身等于target的count+左子树等于target- root.val的count+右子树等于target- root.val的count
## 链表

### 双指针
* 合并双链表，拉链法，注意dummy头节点预防空指针[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
* 合并K个链表，借助最小堆存放k个链表的头 [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
* 相加两个链表的值[2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) 要考虑进位的问题，所以有一个int型的carry记录进位情况。主要需要注意双指针的判空
* 带随机指针的链表深拷贝[138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/) 链表的完全深拷贝，但是每个节点都有一个随机指针。使用map存储每一个节点和new出来的新节点。然后根据map再循环一遍，这样每次的随机random也能找到对应的指向

### 快慢指针
* 删除倒数第n个节点，快指针先走n步 [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
*   判断链表有没有环，快慢指针二倍速终会相遇 [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)
*  找到环的起点，当快慢指针相遇时一个指针回到起点，再次相遇[142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)
* 判断两个链表是否相交，a走完走b，b走完走a，相等即是交点 [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)
* 排序链表：[148. Sort List](https://leetcode.com/problems/sort-list/) 归并排序，终止条件是空指针或仅剩一个节点。每次先快慢指针找到链表中点，快指针要先移到下一个点。并且每次找到中点后进行mid.next的**断链**。然后后序位置对递归的结果进行合并。
### 递归
* 反转链表，递归一直返回最后一个节点作为头指针，依次反转 [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
* **%反转部分链表**，一个suss标注反转部分的下一个节点，head.next从指空改成指suss [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)
* 判断链表是否回文，递归就是栈，一个全局的指针从头开始走，递归方法到最后开始判断，之前的返回值是true和当前层与全局指针值相等就是回文[234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
* **成对的转换节点**[24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/) 每两个节点转换，最后返回这个链表。递归调用时传入的是head.next.next来跳对。返回值是每一对转换后的头节点，所以需要一个p指针指向head.next, p.next=head;head.next=node; return p

## 排序

### 冒泡排序
双层循环，内部每次循环前n-i个，两两比较交换，这样每次都会将一个最大的放到最后
### 选择排序
双层循环，每次循环选择一个最大/最小的放到最后/最前面的位置
### 插入排序
双层循环，每次循环默认前i个已经有序，将第i个元素在前i个中从后向前找插入的位置
### 归并排序
二叉树后序思想，不断二分数组递归调用，后序位置merge两个有序数组. 一个全局的tmp列表用于临时存储数据，merge时先对范围内的数据传到tmp上，然后三个指针分别指向两个left，mid+1，left。用tmp里面的数据对比后存入num数组中
``` java
void sort(int[] nums,int lo, int hi){
	if(lo== hi) return
	 int mid= (lo+hi)/2
	 sort(nums,lo,mid)
	 sort(nums.mid+1,hi)
	 merge(nums,lo,mid,hi)	
}
```

### 快速排序

二叉树前序思想，选取pivot，对数组排序，使得左边都比pivot小，右边都比它大，可以二分出一个pivot并在比较前交换到left位置，然后双指针一个遍历，一个记录比pivot大的元素的第一个位置，比较后再将left位置和这个指针的值调回来，返回pivot的位置，再左右递归调用函数拆解排序。

```java
private void quickSort(int[] nums, int left, int right) {
    if (left>=right) return;
    int cur = left + 1;                   // 从左侧第二个元素开始
    int lo = left;                        // 分界点为第一个元素
    while (cur <= right) {
        if (nums[cur] <= nums[left]) {    // 交换位置保证lo的左侧都是小于num[left]
            swap(nums, lo+1, cur);
            lo ++;
        }
        cur++;
    }
    swap(nums, left, lo);                 // 把分界点元素移动到新的分界位置
    quickSort(nums, left, lo-1);
    quickSort(nums, lo+1, right);
}
```

## 动态规划
### 一维动态规划：
通常状态可以用一个变量表示（位置，长度，容量）
一维数组：
  1. 一般只会依赖更小的i，dp[i-1] dp[i-2]
  2. 有时需要依赖更前面的状态，这时需要遍历0～i之间去获得最优值（如最长递增子序列）

* **最长递增子序列** [300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) 子序列不连续。dp[i]代表着以i结尾的最长子序列长度,初始值dp【i】=1，以每个i为终点，遍历前0～i-1的值，当nums[i]>nums[j]时，dp[i]=Math.max(dp[i],dp[j]+1)，然后再对dp[i]取最大值即可
* 打家劫舍[198. House Robber](https://leetcode.com/problems/house-robber/)  小偷只能隔着偷，每个家的价值不一样，问最大价值多少。状态转移 ``dp[i]=Math.max(dp[i-2]+nums[i-1],dp[i-1]);`` 要么偷了就是前前个值加当前的价值，要么没偷，就保留i-1的结果
* **最大乘积子数组**：[152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) 如果是最大和。直接比较Math.max(nums[i],nums[i]+dp[i-1])即可。但是最大乘积会有负数变正数的可能。所以需要维护两个状态转移值，minN和maxN，当nums[i] 是负数时swap这两个值。并不断比较maxN和minN乘以当前num和只保留num的最大最小值，代表要前面的乘积值或者不要。
* **单词划分** [139. Word Break](https://leetcode.com/problems/word-break/) ，返回一个字符串能否被提供的字典拼凑出来。如果``boolean dp[i]`` 代表以i结尾能否拼凑，状态转移方程就是 需要遍历前面的节点，找到前j是在字典里同时j～i也是的情况， ``dp[j]&&s.substring(j,i)`` .因为依赖前面字符串的状态，所以是两层循环。
*  最大子数组和[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)： dp【i】表示以i结尾的最大子数组和，``dp[i] = Math.max(dp[i-1]+nums[i],nums[i]);`` 或者用前缀和，然后类似最大股票差值的方式求也可以
* 杨辉三角：[118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/) 按照思路正常做即可，注意先new出来指定长度的list，它的cur.size()还是0，因为即使预先分配了，它的size返回的是当前有多少元素。

### 二维动态规划：
状态通常需要两个变量才能完全描述问题
  1. 背包问题：前i个元素和背包容量为j（0/1背包，完全背包）
  2. 序列问题：A[0...i]和B[0....j]之间某种关系的最优解（最长公共子序列，编辑距离）
  3. 从（i，j）位置出发或到达（i，j）位置的最优解 （最小路径和，不同路径）
  4. 字符串本身子串s[i...j]的性质（回文子串，回文子序列）
     
二维数组：
* 通常依赖于相邻行或列：如``dp[i-1][j],dp[i][j-1],dp[i-1][j-1]``
* 同一行或列中更小的索引 如 ``dp[i][k] (k<j)``
* 多个状态组合的极值 ``max(dp[i-1][j],dp[i-1][j-weight[i]+value[i]])``

#### 二维数组遍历
* 最小路径和：[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) 从左上角只能向右或向下移动，求最小路径和。状态方程比较好写，只跟两个方向有关。这题不需要建m+1,n+1的dp数组，因为不需要``dp[0][j]和dp[i][0]``的含义
*  所有路径：[62. Unique Paths](https://leetcode.com/problems/unique-paths/) 和上一题很像，寻找左上到右下的所有可能，状态转移方程改为``dp[i][j]=dp[i-1][j]+dp[i][j-1]``
* 俄罗斯信封套娃，判断以二维数组表示长宽的信封能嵌套的个数。最长递增序列的变种，先对宽度进行升序排列，由于相同的长度不能嵌套，所以对长度相同的降序排列。然后对长度进行最长递增子序列进行查找。
#### 子串问题：
* **最长回文子串** [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) ， 由于需要返回的是String，所以不是记录长度了，而是boolean dp二维数组，只有当 ``i,j位置的值相等且dp[i+1][j-1]是true或者`` j-i<=2 因为没有这个条件无法判断长度为2的字符串。
*  最长回文子序列[516. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)  回文也是用二维dp数组，表示i-j之间最大的子序列长度。所以最后的结果在``dp[0][n-1]``, basecase 是 ``dp[i][i]`` =1, 如果string的i 和 j相等那么长度将增加到``dp[i+1][j-1]+2`` , 否则就保留``dp[i+1][j]或dp[i][j-1]``中最长的一个。由于每次判断需要i+1和j-1的位置已经确认好，所以需要调整循环顺序，主要就是i这倒序查询

#### 序列问题
* 最长公共子序列：[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) 不是公共子串。两个字符串比较所以需要二维dp。当两个字符相等时``dp[i][j]=dp[i-1][j-1]+1`` ，否则就是留``dp[i-1][j]和dp[i][j-1]``二者中最大的。不加1，因为没有匹配上。
*  编辑距离[72. Edit Distance](https://leetcode.com/problems/edit-distance/)，两个字符串经过最少增删改步骤达到一致。设置dp【i】【j】代表0～i-1和0～j-1 字符串之间一致的最小步骤，base case dp[i][0 和 dp[0][j 】都代表从空字符串到另一个字符串的距离，然后 如果s1[i== s2[j], dp[i] [j] = dp[i-1] [j-1], 不相等就是 dp[i-1][j],dp[i][jj-1],dp[i-1][j-1] 三者之间的最小值+1
#### 背包问题：
* **凑零钱**[322. Coin Change](https://leetcode.com/problems/coin-change/) ，完全背包问题，求凑到target的**最小硬币数量**。dp[i]表示amount是i时需要的最小硬币个数，dp【0】【i】是amount+1代表凑不了，状态转移方程就是dp[i]=Math.min(dp[i-coin]+1,dp[i])， 可以用二维做，但是状态转移只跟```
dp[i-1][j],dp[i][j-coins[i-1]]+1``  有关，比较容易降到1维。
*  0-1背包 ：经典的01背包问题需要找出这个背包**最多可以装多少价值**的物品。``dp[i][j]``表示前i个物品装到j空间的背包内的最大价值， 那么每次选择时的状态转移方程分两种，一个是装不下，那么只能不装``dp[i][j]=dp[i-1][j]`` ，要么就是 可装可不装，那么就取``dp[i-1][j]和dp[i-1][j-val[i-1]]+val[i-1]``的最大值
* **完全背包问题**[518. Coin Change II](https://leetcode.com/problems/coin-change-ii/) 硬币可以重复使用，问凑到钱数有几种方式。 ``dp[i][j]``表示 i个物品放入j容量的背包里有几种方式。初始值dp【i】【0】=1表示0不用凑，。那么放得下，``dp[i][j]=dp[i-1][j]+dp[i][j-coins[i-1]]`` 就是不放当前硬币的选项+放之后的选项，由于硬币可以重复，所以不是i-1。放不下那就是``dp[i][j]=dp[i-1][j]`` 
* **分割等和子集**：[416. Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) 0-1背包的变种，要求判断能否将一个子集分成两个，并且元素和相等。可以理解为n个物品能否凑到sum/2的价值，所以用``boolean[][] dp``来维持状态，装不下，那么只能不装``dp[i][j]=dp[i-1][j]``，dp【i】【0】代表能分割所以是true ，要么就是 可装可不装，那么就取``dp[i-1][j]||dp[i-1][j-val[i-1]]`` 的布尔值
* **完全平方数**[279. Perfect Squares](https://leetcode.com/problems/perfect-squares/) 完全背包。求一个数n最少可以由多少个平方数相加得到。可以转换成完全背包，``t*t`` 小于n的都存到list里，作为硬币，n就是需要凑的钱，硬币可以重复使用。dp[0]应该是0因为0不用凑，其他位置应该初始化为max 因为你要进行最小值的比较。然后当coin比当前容量大的时候``dp[i]=Math.min(dp[i],dp[i-coin]+1);``

## 贪心

* 跳跃游戏[55. Jump Game](https://leetcode.com/problems/jump-game/) 可以沿用动态规划的思想，pre代表可以跳跃的最大距离。base 0位置就是nums【0】，状态转移就是````
pre=Math.max(pre,i+nums[i]);,前一位可跳位置和当前能跳的最远距离。当然，需要确保前面可以跳到这来，也就是pre >当前位置。
* **跳跃游戏2**：[45. Jump Game II](https://leetcode.com/problems/jump-game-ii/) 需要从判断能不能走到最后改成返回走到最后的最小步数。所以需要加个变量维护当前步骤内能走到的最远距离cur，和原先的最大距离maxDic，当cur== i 时说明不得不加一步了。加一步后再把maxDic替换给cur。
* 买股票的最佳时机[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  顺序遍历，记录最小值，同时计算当前值和当前记录最小值的差额，最大的即是结果。
* **划分字符区间**[763. Partition Labels](https://leetcode.com/problems/partition-labels/)： 返回一个长度划分的list，保证每个字母只在一个区间内出现 。先用list统计 每个字符出现的最后位置。然后再二次遍历这个list，用一个变量维护遍历过程中每个字符出现位置的最大值，当val== i的时候，说明有字符已经不得不分割了，就把结果存入，以此类推。

## 双指针

* 3数之和：建立在两数之和之上。首先对数组进行排序，然后对每个nums【i】，找有没有和为-nums【i】的结果。两数之和就是有序数组上的双指针。注意剪枝，如如果数字有正负，那么排序后，数字大于0的就不用找了。 两数之和里，如果相等了，需要把和当前两个相等的都剪枝。 如果不能，在移动左右指针时，也是需要将相等的都剪枝出去。
* 盛水最多的容器[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)：一串数字代表高度。 左右指针，每次算面积，保留最大值，然后移动更短的那一条指针
* 最长无重复子串[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)： 滑动窗口，一个map维护窗口内有没有这个字符，不断移动双指针，找出最长无重复子串
*  找到字符串中所有字母的异位词[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)： 一个字符串去另一个字符串中找有没有跟他字母长度都一样，只有顺序不一样的结果。先存储两个字符串前代匹配字符串长度的各个字符出现的次数，也就是26长的int【】，然后每次减小一个位置，增加后一个位置，再依次比较
* 移动零[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/) 思路就是如果你把所有非0值都移到前面了，那么剩下的自然就是0了。快慢指针，快指针非0，就和慢指针交换值，慢指针++；

## 哈希
* 单词分组  [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)，相同字母的字符串放到一个list里。运用hash ``Map<String, List<String>> map`` , 对每个字符串排序后，存入对应的队列，
* **最长连续序列**： [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)  找出一串数字中最长的连续序列。set存储所有数字。然后遍历这个set。而且只从set没有num-1的情况开始计算，因为这样会最长。
* **%找出所有子数组和为k**[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) 由于数组里有正有负，所以不能用滑动窗口，所以先求出前缀和，并同时将前缀和存入map中，value是出现的次数,map需要一个默认值（0，1）用来比较最前的prefix，同时判断sum【i】-k的值有几个，就代表能有几个子数组。

## 技巧
* 合并区间[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)： 若干个区间块进行合并，重叠的合并在一起。 先对区间块进行正序排列，然后遍历区间块，当前结果集为空或者最后一个结果的末位要大于等于当前区间块的头部，那么就可以合并。否则直接存入结果集
* **轮转数组**[189. Rotate Array](https://leetcode.com/problems/rotate-array/)：将数组向右轮转k个位置，即[1,2,3,4,5]->[4,5,1,2,3]。 先调转整个数组，[5,4,3,2,1].再调转前k个， 【4，5，3，2，1】。再调转后面的，【4，5，1，2，3】.注意k 可能超过数组长度，所以要预先取模
* **除自身以外数组的乘积**[238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)，维护 两个数组，一个记录从0到i-1的每次的乘积，一个记录i+1到最后的乘积，这样通过这两个数组就可以得出每个位置除自身以外的乘积。
* **寻找重复数**[287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)：1～n+1的范围内存在着1～n个数字，那么肯定会有一个重复的。找出重复的数。二分思路，对1，n-1进行二分，也就是n/2向下取整，并统计所有小于等于mid元素。当个数严格大于mid时，说明肯定有重复的，right=mid继续查找。否则肯定不是mid，left=mid+1
* **下一个排列** [31. Next Permutation](https://leetcode.com/problems/next-permutation/) 返回数字的下一个排列1373842-》1374238。恶心。主要知道规则，首先要倒序找挨着的两个正序的数，如果没有，说明整体是降序的，直接翻转即可。然后倒序找有没有比i大的，如果有，互换，然后再对i+1区域正序排列。
* **最大子数组和**[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) 求和最大子数组，有正有负，使用前缀和，转换为买股票的最佳时机，记录最小值，同时记录当前前缀和和最小值的差额。注意最小值初始化为0，可以包含第一个前缀和，否则初始化为第一个前缀和然后下标从1开始就会默认不带第一个值。
* **%颜色排序**[75. Sort Colors](https://leetcode.com/problems/sort-colors/) ：荷兰国旗问题，一组0，1，2按照顺序排列。l指向0的位置，r指向2的位置，idx进行遍历。nums[idx] 是0时与l互换后都++，是2时跟r互换后，只有r--，因为不知道换过来的是什么。是1时直接idx++；
* 只出现一次的数字 [136. Single Number](https://leetcode.com/problems/single-number/) 一个数组里只有一个数字出现了一次，安位异或（res^=num），剩下的值就是单个的
## 堆栈

* 有效的括号[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)： 利用一个map维护不同种类括号之间的对应关系，右括号作为key，左括号作为value。然后用栈进行遍历，左括号直接进。否则如果是右括号，栈顶的元素跟当前括号不匹配或者栈为空，即返回false
* 最小栈[155. Min Stack](https://leetcode.com/problems/min-stack/)：构建一个最小栈的类，除了push/pop/top/以外，还可以返回栈内最小值 getMin（）。维护两个栈，一个用来正常存储，一个只在栈为空或者当前值小于等于栈最小值时才压入。压出时，如果正常栈压出的值等于最小栈的栈顶值，那么也跟着抛出
* 每日温度[739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)：求每个位置对应下一个比他大的温度出现在几天后。用单调栈，只维护比栈顶小的。当当前值小于栈顶时直接入栈。大于时while循环弹出所有比当前值小的，存储的是下标所以直接相减就行了
* 数组中第k个最大元素[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)：维护一个k大小的最小堆，因为堆顶是最小的，然后放入前k个元素，当后续的元素比当前堆内大的时候，就弹出堆顶的元素，插入新值，这样最后堆顶最小的就是第k大的。
* **数组中前k个高频元素**[347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) 返回前k高频的元素本身。一个map统计每个数字出现的次数，然后维护一个小根堆，注意比较方式应该是比较map.get(key)。大于堆顶元素的频次就替换，剩下的就是前k高频的``PriorityQueue<Integer> heap=new PriorityQueue<>(k,(a,b)->map.get(a)-map.get(b));``
* **字符串解码**[394. Decode String](https://leetcode.com/problems/decode-string/) ：细节，``3[a2[c]]``解码成accaccacc。两个栈，一个存数字，一个存字符串。如果是数字则num=num* 10+(c-'0'); 如果是字母则 cur.append(c); 如果是左括号，则将两个参数分别压入各自的栈，并置0置空。如果是右括号，则弹出两个栈顶的值s_num,s_str, 手里的cur执行s_num遍，并和s_str进行拼接。 

## 二维矩阵
* 旋转输出矩阵[54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) l,r,u,d分别定义四个边界，旋转打印矩阵。然后每次打完一行或一列后，判断是否已经到边界值，终止循环。
* 二维数组置零 [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/) 如果不强调O（1），可以两遍循环，第一遍用set 记录下那行那列有0，第二遍遍历的时候置零。如果强调O（1），可以用第一行第一列做一个标志列，首先遍历下第一行第一列，用两个flag去存第一行第一列本身有没有0.然后遍历的时候将有0的位置投影到第一行第一列。第二次循环时置零。
* 搜索二维矩阵2 [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) 跟1相比 不保证前一行的数比下一行都小。只保证行内增序，列向增序。暴力法就是每行二分。或者模拟成二叉树，在右上角的位置，左边的数都比自己小，下边的数都比自己大。从右上角的值和target进行比较小的话就减列，大的话就增行。
* 岛屿数量[200. Number of Islands](https://leetcode.com/problems/number-of-islands/) 1代表岛屿，0代表海洋。双层循环找是1的位置开始dfs遍历，然后有一个isArea函数判断是否超出边界，当该位置是1是，四个方向dfs。每遍历到一个位置就把该位置改成2，表示已经遍历过了。岛屿数量就是每一个递归函数调用了就加1. 岛屿最大面积就是改成1+dfs（）四个方向。
* **腐烂的橘子**[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) 0 代表空，1代表新鲜的橘子，2代表腐烂的橘子。问橘子全部腐烂需要几分钟。每分钟腐烂的橘子会向四周扩散。如果有腐烂不到的，返回-1. 沿用岛屿数量的思路，从2位置开始，多传一个time的参数，从2开始，每次dfs的时候就加1。dfs如果超出边界，或者不是新鲜的橘子且覆盖的腐烂时间小于当前时间的，直接返回。最后再双循环统计一遍，如果有还是1的，直接-1，要不遍历完，如果res还是初始值0，说明没有腐烂的路径，结果还是0，要不就是最大时间-2
