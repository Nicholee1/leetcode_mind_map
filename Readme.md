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
