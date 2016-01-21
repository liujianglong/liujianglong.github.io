---
layout: post
title: 剑指Offer题目总结
tags: 数据结构 算法 面试
keywords: 
description:
---


### 说明

最近在看剑指Offer准备面试，里面的算法都是用C实现的，这里总结了一下剑指Offer里面的题目，并用Java实现了。
	
##

###1. 数组：二维数组中的查找
###### 题目描述：在一个二维数组中，每一行都按照从左到右递增的顺序排列，每一列都按照从上到下递增的顺序排列。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

	public boolean find(int nums[][], int target){
		if(nums==null) return false;
		int rows=nums.length;
		int cols=nums[0].length;
		int row=0, col=cols-1;
		while(row<rows && col>=0){
			if(nums[row][col]==target)
				return true;
			else if(nums[row][col]>target)
				col--;
			else
				row++;
		}
		return false;
	}

####2. 字符串：替换空格
###### 题目描述：请实现一个函数，把字符串中的每个空格替换成“%20”。例如输入“We are happy.”，则输出“We%20are%20happy.”。

	    public String replaceSpace(String str) {
    	StringBuilder sb=new StringBuilder();
        for(int i=0; i<str.length(); i++){
            char ch=str.charAt(i);
            if(ch==' ')
                sb.append("%20");
            else
                sb.append(ch);
        }
        return sb.toString();
    }

####3. 链表：从尾到头打印链表
###### 题目描述：输入一个链表的头结点，从尾到头反过来打印出每个结点的值。
	public void printListFromTailToHead(ListNode listNode) {
        if(listNode==null) return;
		Stack<Integer> stack=new Stack<Integer>();
        ListNode head=listNode;
        while(head!=null){
			stack.push(head.val);
            head=head.next;
        }
		while(!stack.isEmpty()){
			System.out.print(stack.pop());
		}
    }

#### 4. 树：重建二叉树
###### 题目描述：输入某个二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果都不含重复的数字。例如输入的前序遍历序列{1，2，4，7，3，5，6，8}和中序遍历序列{4，7，2，1，5，3，8，6}，则重建出该二叉树并输出它的头结点。
	class BinaryTree{
		int val;
		BinaryTree left;
		BinaryTree right;
	}

	    public TreeNode construct(int [] pre,int [] in) {
        	if(pre.length==0 || in.length==0) return null;
        
        	int rootIndex=0;
        	for(int i=0; i<in.length; i++){
          	  if(in[i]==pre[0])
          	      rootIndex=i;
       		}
       		int[] pre1=new int[rootIndex];
      		int[] in1=new int[rootIndex];
      		int[] pre2=new int[in.length-rootIndex-1];
     		int[] in2=new int[in.length-rootIndex-1];
    		   
      		for(int i=0; i<pre1.length; i++){
      			pre1[i]=pre[i+1];
    		}
    		for(int i=0; i<in1.length; i++){
            	in1[i]=in[i];
        	}
        
        	for(int i=0; i<pre2.length; i++){
         	   pre2[i]=pre[pre1.length+1+i];
      		}
        
     	   for(int i=0; i<in2.length; i++){
        	   in2[i]=in[rootIndex+1+i];
       	    }
        	TreeNode root=new TreeNode(pre[0]);
        	root.left=construct(pre1,in1);
        	root.right=construct(pre2,in2);
        	return root;
    }

#### 5. 栈和队列：用两个栈实现队列
###### 题目描述：用两个栈实现一个队列。队列的声明如下，请实现它的两个函数appendTail和deleteHead，分别完成在队列尾部插入结点和在队列头部删除结点的功能。
	public class Queue{
		private Stack<Integer> stack1=new Stack<Integer>();
		private Stack<Integer> stack2=new Stack<Integer>();
		
		private void appendTail(int item){
			stack1.push(item);
		}

		private int deleteHead(){
			if(!stack2.isEmpty())
				return stack2.pop();
			else{
				while(!stack1.isEmpty())
					stack2.push(stack1.pop());
				return stack2.pop();
			}
		}
	}

#### 8. 查找和排序：旋转数组的最小数字
###### 题目描述：把一个数组最开始的若干元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的旋转，输出旋转数组的最小元素。例如数组{3，4，5，1，2}为{1，2，3，4，5}的一个旋转，该数组的最小值为1。

	public int minNum(int[] array, int fromIndex){
        if(array==null || array.length==0)
            return 0;
        if(array.length==1)
            return array[0];

        int left=fromIndex;
        int right=array.length-1;
        if(array[left]<array[right])
            return array[left];
        
        while(array[left]>=array[right]){
            if(right-left==1)
                return array[right];
            int mid=(left+right)/2;
            if(array[mid]>array[left])
                left=mid;
            else if(array[mid]<array[right])
                right=mid;
            else
               return minNum(array, fromIndex+1);
        }
        return array[right];
    }


#### 9. 递归和循环：斐波那契数列(1)
###### 题目描述：写一个函数，输入n，求斐波那契数列的第n项。

	//循环解法：
	public int fib(int n){
		if(n<=1)
			return n;
		int fib_1=1, fib_2=0;
		int fibN=0;
		for(int i=2; i<=n; i++){
			fibN=fib_1+fib_2;
			fib_2=fib_1;
			fib_1=fibN;
		}
		return fibN;
	}

#### 10. 递归和循环：斐波那契数列(2)-跳台阶
###### 题目描述：一个青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少跳法。

	//递归解法（效率较低，可改用上面循环解法）
	 public int jumpFloor(int n) {
		if(n<=2)
            return n;
        return jumpFloor(n-1)+jumpFloor(n-2);
    }

#### 11. 递归和循环：斐波那契数列(3)-矩形覆盖
###### 题目描述：我们可以用2\*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2\*1的小矩形无重叠地覆盖一个2\*n的大矩形，总共有多少种方法？

	//递归解法（效率较低，可改用上面循环解法）
	 public int rectCover(int n) {
		if(n<=2)
            return n;
        return rectCover(n-1)+rectCover(n-2);
    }

#### 12. 位运算：二进制中1的个数
###### 题目描述：请实现一个函数，输入一个整数，输出该数二进制表示中1的个数。例如把9表示成二进制位1001，有2位是1.因此输入9，该函数输出2。

	public int numOf1(int n){
		int count=0;
		while(n!=0){
			n&=n-1;
			count++;
		}
		return count;
	}

	//举一反三1：如何判断一个数是否是2的整数次方？
	public boolean isPowerOf2(int n){
		if(n&(n-1)==0)	
			return true;
		return false;
	}
	
	//举一反三2：给定两个整数m和n，计算需要改动m的二进制表示中的多少位才能得到n，比如10的二进制表示为1010, 13的二进制表示为1101，则需要3位。
	public int numOfBitToChange(int m, int n){
		int temp=n^m;
		int count =0;
		while(temp!=0){
			temp&=temp-1;
			count++;
		}
		return count;
	}

#### 13. 代码的完整性：数值的整数次方
###### 题目描述：实现函数 double power(double base, int exponent), 求base的 exponent次方。 不得使用库函数， 同时不需要考虑大数问题。

	//注意base是否为零； 注意exponent是否为负数
	public double power(double base, int exponent){
		if(Math.abs(base-0.0)<0.000001)
			return 0;
		int result=1.0;
		int e=Math.abs(exponent);
		for(int i=0; i<e; i++)
			result*=base;
		if(exponent<0)
			result=1.0/result;
		return result;
	}

#### 14. 代码的完整性：打印1到最大的n位数
###### 题目描述：输入数字n，按顺序打印出从1到最大n位十进制数。比如输入3，则打印1，2，3一直到999。


#### 15. 代码的完整性：在O(1)时间删除链表结点
###### 题目描述： 给定单向链表的头结点和一个结点指针，定义一个函数在O(1)时间删除该结点。

	class ListNode{
		int val;
		ListNode next;
		public ListNode(int x){val=x;}
	}

	public  ListNode deleteNode(ListNode head, ListNode target) {
		if (head == null || target == null)
			return head;
		//target不是尾结点
		if(target.next!=null){
			target.val = target.next.val;
			target.next = target.next.next;
		}
		//target是尾结点，而且链表只有一个结点
		else if (head == target)
				return head.next;
		//target是尾结点，而且链表有多个结点
		else{
			ListNode node = head;
			while (node.next != target)
				node = node.next;
			node.next = null;
		}
		return head;
	}

#### 16. 代码的完整性：调整数组顺序使奇数位于偶数前面
###### 题目描述： 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

	public void reOrderArray(int[] array) {
		int odd = 0;
		int even = array.length - 1;
		while (odd < even) {
			while (array[odd] % 2 == 1)
				odd++;
			while (array[even] % 2 == 0)
				even--;
			if (odd < even) {
				int temp = array[odd];
				array[odd] = array[even];
				array[even] = temp;
			}
		}
		for (int i = 0; i < array.length; i++)
			System.out.println(array[i]);
	}

#### 17. 代码的鲁棒性：链表中倒数第K个结点
###### 题目描述： 输入一个链表，输出该链表中倒数第K个结点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾结点是倒数第1个结点。例如一个链表有6个结点，从头结点开始它们的值依次是1，2，3，4，5，6。这个链表的倒数第3个结点是值为4的结点。

	public ListNode findKthToTail(ListNode head,int k) {
        if(head==null || k<=0)
            return null;

		ListNode fast = head, slow = head;
		for (int i = 0; i < k - 1; i++) {
			if (fast.next != null)
				fast = fast.next;
            else
                return null;
		}

		while (fast.next != null) {
			slow = slow.next;
			fast = fast.next;
		}
		return slow;
    }
	
#### 18. 代码的鲁棒性：反转链表
###### 题目描述： 定义一个函数，输入一个链表的头结点，反转该链表并输出反转后链表的头结点。

	 public ListNode reverseList(ListNode head) {
        if(head==null) return null;
		ListNode newHead=new ListNode(head.val);
        while(head.next!=null){
            head=head.next;
            ListNode node=new ListNode(head.val);
            node.next=newHead;
            newHead=node;
        }
        return newHead;
    }

#### 19. 代码的鲁棒性：合并两个排序的列表
###### 题目描述： 输入两个递增排序的链表，合并这两个链表并使新链表中的结点仍然是按照递增排序的。链表结点的定义如下：
	
	class ListNode{
		int val;
		ListNode next;
	}
	
	//解法一：常规解法
	public ListNode Merge(ListNode list1,ListNode list2) {
        if(list1==null) return list2;
        if(list2==null) return list1;
        ListNode node=new ListNode(0);
        ListNode head=node;
        while(list1!=null && list2!=null){
            if(list1.val<=list2.val){
                node.next=list1;
                list1=list1.next;
            }else{
                node.next=list2;
                list2=list2.next;
            }
            node=node.next;
        }
        
        while(list1!=null){
            node.next=list1;
            list1=list1.next;
            node=node.next;
        }
        
         while(list2!=null){
            node.next=list2;
            list2=list2.next;
            node=node.next;
        }
        return head.next;
    }

	//解法二：递归解法

    public ListNode Merge(ListNode list1,ListNode list2) {
        if(list1==null) return list2;
        if(list2==null) return list1;
		ListNode head=null;
        if(list1.val<=list2.val){
            head=list1;
            head.next=Merge(list1.next, list2);
        }else{
            head=list2;
            head.next=Merge(list1,list2.next);
        }
        return head;
    }

#### 19. 代码的鲁棒性：树的子结构
###### 题目描述： 输入两棵二叉树A和B，判断B是不是A的子结构。二叉树结点的定义如下：

	class BinaryTreeNode{
		int val;
		BinaryTreeNode left;
		BinaryTreeNode right;
	}

    public boolean hasSubtree(TreeNode root1,TreeNode root2) {
        if(root2==null || root1==null) return false;
		boolean result=false;
        if(root1.val==root2.val)
            result= isBPartOfA(root1, root2);
        if(!result)
            result= hasSubtree(root1.left, root2);
        if(!result)
            result= hasSubtree(root1.right, root2);
        return result;
    }
    
    private boolean isBPartOfA(TreeNode a, TreeNode b){
        if(b==null)
            return true;
        if(a==null)
            return false;
        if(a.val!=b.val)
            return false;
        return isBPartOfA(a.left, b.left) && isBPartOfA(a.right, b.right);
    }

#### 20. 解决面试题的思路：二叉树的镜像
###### 题目描述： 请完成一个函数，输入一个二叉树，该函数输出它的镜像。

	class TreeNode{
		int val;
		TreeNode left;
		TreeNode right;
		TreeNode(int val){this.val=val;}
	}

    public void Mirror(TreeNode root) {
        if(root==null) return;
        if(root.left==null && root.right==null) return;
        
        TreeNode temp=root.left;
        root.left=root.right;
        root.right=temp;
        
        Mirror(root.left);
        Mirror(root.right);
    }

#### 21. 解决面试题的思路：顺时针打印矩阵
###### 题目描述： 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

    public ArrayList<Integer> printMatrix(int [][] matrix) {
		ArrayList<Integer> list=new ArrayList<Integer>();
		if(matrix==null || matrix.length==0) return list;
        
        int rows=matrix.length, cols=matrix[0].length;
        int start=0;
        while(rows>start*2 && cols>start*2){
            list.addAll(printMatrixCircle(matrix, rows, cols, start));
            start++;
        }
        return list;
    }
    
    //打印某一圈
    private ArrayList<Integer> printMatrixCircle(int [][] matrix, int rows, int cols, int start){
        ArrayList<Integer> list=new ArrayList<Integer>();
        int endX=cols-1-start;
        int endY=rows-1-start;
        //从左向右打印
        for(int i=start; i<=endX; i++){
            list.add(matrix[start][i]);
        }
        //从上到下打印
        if(start<endY){
            for(int i=start+1; i<=endY; i++){
                list.add(matrix[i][endX]);
            }
        }
        //从右到左打印
        if(start<endX && start<endY){
            for(int i=endX-1; i>=start;i--){
                list.add(matrix[endY][i]);
            }
        }
        //从下到上打印
        if(start<endX && start<endY-1){
            for(int i=endY-1; i>=start+1; i--){
                list.add(matrix[i][start]);
            }
        }
        return list;
    }

#### 22. 解决面试题的思路：包含min函数的栈
###### 题目描述： 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的min函数。在该栈中，调用min、push及pop的时间复杂度都是O(1)。

		public class MinStack {
			Stack<Integer> stack=new Stack<Integer>();
    		Stack<Integer> minStack=new Stack<Integer>();
    	
    		public void push(int value) {
    		    stack.push(value);
    		    if(minStack.size()==0 || value< minStack.peek())
    		        minStack.push(value);
    		    else
    		        minStack.push(minStack.peek());
    		}
    
    		public void pop() {
    		    stack.pop();
    		    minStack.pop();
    		}
    
    		public int top() {
    		    return stack.peek();
    		}
    
    		public int min() {
    		    return minStack.peek();
    	}
	}

#### 23. 解决面试题的思路：栈的压入、弹出序列
###### 题目描述： 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出序列。加入压入栈的所有数字均不相等。

	public boolean IsPopOrder(int [] pushA,int [] popA) {
        if(pushA==null || popA==null || pushA.length==0 || popA.length==0) 
            return false;
        
        if(pushA.length!=popA.length) 
            return false;
        
        Stack<Integer> stack=new Stack<Integer>();
      	int popIndex=0;
        int pushIndex=0;
        
        while(popIndex<popA.length && pushIndex<pushA.length){
            while(pushIndex<pushA.length && (stack.empty() || stack.peek()!=popA[popIndex]))
                stack.push(pushA[pushIndex++]);
             while((!stack.empty() && popIndex<popA.length)&& stack.peek()==popA[popIndex]){
                stack.pop();
                popIndex++;
            }
        }
        if(popIndex==popA.length)
        	return true;
        return false;
    }

#### 24. 解决面试题的思路：从上往下打印二叉树
###### 题目描述： 从上往下打印出二叉树的每个结点，同一层的结点按照从左到右的顺序打印。

    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> list=new ArrayList<Integer>();
        if(root==null) return list;
        
        Queue<TreeNode> queue=new ArrayDeque<TreeNode>();
        queue.add(root);
        
        while(queue.size()!=0){
            if(queue.peek().left!=null)
                queue.add(queue.peek().left);
            if(queue.peek().right!=null)
                queue.add(queue.peek().right);
            list.add(queue.remove().val);
        }
        return list;
    }

#### 24. 解决面试题的思路：二叉搜索树的后序遍历序列
###### 题目描述： 输入一个整数数组，判断该数组是不是某二叉搜索树的后续遍历的结果。如果是则返回true，否则返回false。假设输入的数组的任意两个数字都互不相同。

    public boolean VerifySquenceOfBST(int [] sequence) {
		int n = sequence.length;
		if (sequence == null || n == 0)
			return false;
		int last = sequence[n - 1];
		int i = 0;
		for (; i < n - 1; i++) {
			if (sequence[i] > last)
				break;
		}
		for (int j = i; j < n - 1; j++) {
			if (sequence[j] < last) 
				return false;
		}
		boolean left = true, right = true;
		if (i > 0)
			left = VerifySquenceOfBST(Arrays.copyOfRange(sequence, 0, i));
		if (n - 1 - i > 0)
			right = VerifySquenceOfBST(Arrays.copyOfRange(sequence, i, n - 1));
		return left && right;
    }



