---
layout: post
title: 剑指Offer题目总结
category: 技术
tags: 数据结构 算法 面试
keywords: 
description:
---


### 说明

最近在准备面试，这里总结一下剑指Offer里面的题目。
	
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
{% highlight java linenos %}
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

#### 6. 栈和队列：用两个栈实现队列
###### 题目描述：用两个栈实现一个队列

	

