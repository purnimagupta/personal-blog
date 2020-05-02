---
title: Implement Binary Search Tree in JavaScript
date: "2020-04-29"
description: We'll discuss what is binary search tree and how to implement it in javascript
cover: ./tree.jpg
photoBy: Frédéric Perez 
tags: data structure, bst, binary search tree, javascript algo
---

# Table of Contents

1. [What is a Binary Tree](#what-is-a-binary-tree)
2. [Properties of binary tree](#types)
3. [Insert a node in Binary Search Tree](#insert)
4. [Find a node](#search)

<div id="what-is-a-binary-tree"></div>

# What is a Binary Tree?

To answer this question, you need to know what is a _tree_.


![](./tree.png)

### No, not that one.

<br>

**Here is the Wikipedia definition of a tree:**

> In computer science, a "tree" is a tree data structure which allows us to represent the hierarchial data in a graphical form. It's named a "tree structure" because it resembles a biological tree, but with the upside down form, with the "root" being at the top and the "leaves" at the bottom.

_Root at the top and leaves like at the bottom._ So like this?

![](./tree_inverted.png)

### Hmm, close enough. It's more like this:

![](./hierarchical-data-structure.png)

So trees are **data structures**. What's more interesting is that, they are also _**recursive** data structures_ - because within a tree is there is another tree (sub-tree), and within that sub-tree is another sub-tree...all the way down!

**There are lots of applications of a tree data structure, and some of them are:**

- operating system(directory structure)
- management(hierarchical organizational structures)
- biology(evolutionary tree)

And when we discuss a tree within the context of programming, we often represent it in this way:

![](./tree-in-cs.png)

Now, in this post, I'll focus on a special kind of tree, called a *Binary Tree*.

> A Binary Tree is a tree data structure in which each node has at the most, 2 children. There can be a child on the left, and a child on the right. 

The tree elements are called nodes. And each node can have atmost 2 children. That means it can have either 0, 1, or 2 children.

Here are some examples:

![1.png](./1.png) 
![2.png](./2.png)  
![3.png](./3.png)

### Binary trees are very useful because they help you store, sort and retrieve data very efficiently.

<div id="types"></div>

## Binary trees can be of many types as well:

- ### Full/Proper/Strict Binary Tree

Every node has exactly two chidren except leaf nodes. Leaf nodes have zero children.

![](./full-binary-tree.png)

![](./not-full-binary-tree.png)

- ### Complete Binary Tree

All levels are completely filled except the last level and last level has nodes as left as possible.

![](./complete-binary-tree.png)
![](./not-complete-binary-tree.png)

- ### Perfect Binary Tree

All the internal nodes have 2 children and all the leaves are at the same level. A Perfect binary tree is also a complete binary tree and full binary tree, but the reverse is not true.

![](./not-perfect-binary-tree.png)

- ### Degenerate Binary Tree

All internal nodes have exactly one node.

![](./degenerate-binary-tree.png)

---

Now that you've seen how different binary trees can look like, let's look at some of their properties

## Properties of a binary tree

1. Maximum number of nodes possible at any level **i = 2<sup>i</sup>**

![](./binary-tree_max-node-level.png)

2. Maximum number of nodes at height h would be **2<sup>h</sup> - 1** nodes if height of the root node
is 1. But if you consider height of root node as 0, then formula would be slightly changed and can be written like this(**2<sup>h+1</sup> - 1**)

![](./binary-tree-max-nodes-height-h.png)

3. Minimum height `h = Math.ceil(log(n+1))`. It can be derived from the equation above.

![](./binary-tree_min-height.png)

4. Minimum number of nodes in Binary tree of height h would be **n = h + 1**. Here, we're considering the height 0 for the root Node.

![](./binary-tree_min-nodes.png)

5. You can easily derive from equation `n=h+1` that maximum height at node n is **h = n-1**

---

# What is a Binary Search Tree?

According to wikipedia, binary search trees (BST), is a data structure that stores "items" (such as numbers, names etc.) in memory. It keeps their keys on sorted order, so that lookup and other can use the principle of binary search.

In simple words, binary search tree is a binary tree that has the following properties:

- The left subtree of a node is less than or equal to it's parent node's key
- The right subtree of a node is greater than or equal to it's parent node's key


### Logical representation of a Binary Search Tree

<p align="center"><img  src="./4.png"></p>

### Let's write some code now!

In the following tutorial, you'll learn to build a binary search tree. You'll learn how to write create and insert integer nodes into the tree, and how to efficiently search for some data value.

> Note: The coding tutorial will be in JavaScript, so some basic knowledge of programming in JS will be useful.

So if you notice carefully in the diagram above, we know that a node would require three fields:
  - a _data_ field to store a value or some information like an integer for example.
  - a _left_ field to store the left subtree 
  - a _right_ field to store the right subtree

So first, create a `class` called `BST`:

```
class BST {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }
}
```
In the beginning, you'll create an instance of this class when you add your first root node. It's a BST with 1 node, and since that node does not have any subtrees below it, its _left_ and _right_ nodes would be `null`.

```
let rootNode = new BST(10);
console.log(rootNode) // Node { val: 10, left: null, right: null }

```

Next, let's write a function to insert a node.
<div id="insert"></div>

### Insert a node

#### Let's visualize it through a flow diagram

![](./bst-insert.png)

This is how the logic of the insert function would look like:
```
insert(val) {
  if(val < this.val && !this.left) {
    this.left = new Node(val);
  }
  else if(val < this.val && this.left) {
    this.left.insert(val)
  }
  else if(val > this.val && !this.right) {
    this.right = new Node(val)
  } 
  else if(val > this.val && this.right) {
    this.right.insert(val)
  }
}

```

Now, if you insert `rootNode.insert(8)`, and print the root node, then the output would be:

```
Node {
  val: 10,
  left: Node { val: 8, left: null, right: null },
  right: null 
}
```

**What happened?**

In the beginning, the value of the root node is `10`. Then, you tried to insert `8`. 8 is less than 10, so the first condition holds true - and it inserts a new Node with a value of `8` to the left of the Node 10.

If we insert again `rootNode.insert(6)` then what do you think will happen? Think for a while and proceed below to
check the output.

```
Node {
  val: 10,
  left:
   Node {
     val: 8,
     left: Node { val: 6, left: null, right: null },
     right: null 
  },
  right: null 
}
```

This time the 2nd condition holds true, because 6 is less than 10 and the left subtree exists (because it already contains 8!) So it'll call the `insert` function again, but this time within the left sub-tree (i.e, the Node that contains `8`). Now the 1st condition will again hold true, and a new Node with the value `6` will be inserted to the left of the Node with the value `8`.

Let's move on now.

<div id="search"></div>

### Search if some value exists in the tree

Think for a moment how we'll write the logic for this bit. Let's divide it into subtasks that we would need.

- if the value is equal to root Node itself then we can return `true` (meaning that the value exists).
- if the value is less than the root Node and the left node exists, then search in the left subtree.
- if the value is bigger than the root Node and the right node exists, then search in the right subtree.

#### Let's visualize it through a flow diagram

![](./Search-in-BST.png)

```
search(element) {
  if(this.val === element) {
    return true
  } else if(this.val > element && this.left){
    return this.left.search(element)
  } else if(this.val < element && this.right) {
    return this.right.search(element)
  }   

  return false // element does not exist in the tree 
}
```

#### And we're done!

## Here is how the final program will look like:

```
class Node {
  constructor(val) {
    this.val = val;
    this.left = null;
    this.right = null;
  }

  insert(val) {
    if(val < this.val && !this.left) {
      // create a new node at the left of the tree
      this.left = new Node(val);
    }
    else if(val < this.val && this.left) {
      this.left.insert(val)
    }
    else if(val > this.val && !this.right) {
      this.right = new Node(val)
    } 
    else if(val > this.val && this.right) {
      this.right.insert(val)
    }
  }

  search(element){   
    if(this.val === element) {
      return true
    } else if(this.val > element && this.left){
      return this.left.search(element)
    } else if(this.val < element && this.right) {
      return this.right.search(element)
    }
    return false
  }
}

// create a bst with 3 nodes. (Root node contains the value 10)
let bst = new Node(10);
bst.insert(9)
bst.insert(6)

console.log(bst)
console.log(bst.search(9)) // prints true
```

## Thank you for reading!
