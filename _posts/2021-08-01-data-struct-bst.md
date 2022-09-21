---
layout: post
title: Data Structure with python-Binary Search Tree
categories: Dev
tags: [python, data structure]
---

# Introduction

二元搜尋樹（英語：Binary Search Tree），也稱為有序二元樹（ordered binary tree）或排序二元樹（sorted binary tree），是指一棵空樹或者具有下列性質的二元樹：

- 若任意節點的左子樹不空，則左子樹上所有節點的值均小於它的根節點的值

- 若任意節點的右子樹不空，則右子樹上所有節點的值均大於它的根節點的值

- 任意節點的左、右子樹也分別為二元搜尋樹

<!-- more -->

二元搜尋樹相比於其他資料結構的優勢在於尋找、插入的時間複雜度較低。為$$O(\log n)$$。二元搜尋樹是基礎性資料結構，用於構建更為抽象的資料結構，如集合、多重集、關聯陣列等。

<!-- more -->

二元搜尋樹的尋找過程和次優二元樹類似，通常採取二元連結串列作為二元搜尋樹的儲存結構。中序遍歷二元搜尋樹可得到一個關鍵字的有序序列，一個無序序列可以透過建構一棵二元搜尋樹變成一個有序序列，建構樹的過程即為對無序序列進行尋找的過程。每次插入的新的結點都是二元搜尋樹上新的葉子結點，在進行插入操作時，不必移動其它結點，只需改動某個結點的指標，由空變為非空即可。搜尋、插入、刪除的複雜度等於樹高，期望$$O(\log n)$$​，最壞$$O(n)$$（數列有序，樹退化成線性表）。

雖然二元搜尋樹的最壞效率是$$O(n)$$，但它支援動態查詢，且有很多改進版的二元搜尋樹可以使樹高為$$O(\log n)$$，從而將最壞效率降至$$O(\log n)$$，如AVL樹、紅黑樹等。

# Implementation

```python
"""
A binary search Tree
"""


class Node:
    def __init__(self, value, parent):
        self.value = value
        self.parent = parent  # Added in order to delete a node easier
        self.left = None
        self.right = None

    def __repr__(self):
        from pprint import pformat

        if self.left is None and self.right is None:
            return str(self.value)
        return pformat({"%s" % (self.value): (self.left, self.right)}, indent=1)


class BinarySearchTree:
    def __init__(self, root=None):
        self.root = root

    def __str__(self):
        """
        Return a string of all the Nodes using in order traversal
        """
        return str(self.root)

    def __reassign_nodes(self, node, new_children):
        if new_children is not None:  # reset its kids
            new_children.parent = node.parent
        if node.parent is not None:  # reset its parent
            if self.is_right(node):  # If it is the right children
                node.parent.right = new_children
            else:
                node.parent.left = new_children
        else:
            self.root = new_children

    def is_right(self, node):
        return node == node.parent.right

    def empty(self):
        return self.root is None

    def __insert(self, value):
        """
        Insert a new node in Binary Search Tree with value label
        """
        new_node = Node(value, None)  # create a new Node
        if self.empty():  # if Tree is empty
            self.root = new_node  # set its root
        else:  # Tree is not empty
            parent_node = self.root  # from root
            while True:  # While we don't get to a leaf
                if value < parent_node.value:  # We go left
                    if parent_node.left is None:
                        parent_node.left = new_node  # We insert the new node in a leaf
                        break
                    else:
                        parent_node = parent_node.left
                else:
                    if parent_node.right is None:
                        parent_node.right = new_node
                        break
                    else:
                        parent_node = parent_node.right
            new_node.parent = parent_node

    def insert(self, *values):
        for value in values:
            self.__insert(value)
        return self

    def search(self, value):
        if self.empty():
            raise IndexError("Warning: Tree is empty! please use another.")
        else:
            node = self.root
            # use lazy evaluation here to avoid NoneType Attribute error
            while node is not None and node.value is not value:
                node = node.left if value < node.value else node.right
            return node

    def get_max(self, node=None):
        """
        We go deep on the right branch
        """
        if node is None:
            node = self.root
        if not self.empty():
            while node.right is not None:
                node = node.right
        return node

    def get_min(self, node=None):
        """
        We go deep on the left branch
        """
        if node is None:
            node = self.root
        if not self.empty():
            node = self.root
            while node.left is not None:
                node = node.left
        return node

    def remove(self, value):
        node = self.search(value)  # Look for the node with that label
        if node is not None:
            if node.left is None and node.right is None:  # If it has no children
                self.__reassign_nodes(node, None)
            elif node.left is None:  # Has only right children
                self.__reassign_nodes(node, node.right)
            elif node.right is None:  # Has only left children
                self.__reassign_nodes(node, node.left)
            else:
                tmp_node = self.get_max(
                    node.left
                )  # Gets the max value of the left branch
                self.remove(tmp_node.value)
                node.value = (
                    tmp_node.value
                )  # Assigns the value to the node to delete and keep tree structure

    def preorder_traverse(self, node):
        if node is not None:
            yield node  # Preorder Traversal
            yield from self.preorder_traverse(node.left)
            yield from self.preorder_traverse(node.right)

    def traversal_tree(self, traversal_function=None):
        """
        This function traversal the tree.
        You can pass a function to traversal the tree as needed by client code
        """
        if traversal_function is None:
            return self.preorder_traverse(self.root)
        else:
            return traversal_function(self.root)

    def inorder(self, arr: list, node: Node):
        """Perform an inorder traversal and append values of the nodes to
        a list named arr"""
        if node:
            self.inorder(arr, node.left)
            arr.append(node.value)
            self.inorder(arr, node.right)

    def find_kth_smallest(self, k: int, node: Node) -> int:
        """Return the kth smallest element in a binary search tree"""
        arr = []
        self.inorder(arr, node)  # append all values to list using inorder traversal
        return arr[k - 1]


def postorder(curr_node):
    """
    postOrder (left, right, self)
    """
    node_list = list()
    if curr_node is not None:
        node_list = postorder(curr_node.left) + postorder(curr_node.right) + [curr_node]
    return node_list


def binary_search_tree():
    r"""
    Example
                  8
                 / \
                3   10
               / \    \
              1   6    14
                 / \   /
                4   7 13
    >>> t = BinarySearchTree().insert(8, 3, 6, 1, 10, 14, 13, 4, 7)
    >>> print(" ".join(repr(i.value) for i in t.traversal_tree()))
    8 3 1 6 4 7 10 14 13
    >>> print(" ".join(repr(i.value) for i in t.traversal_tree(postorder)))
    1 4 7 6 3 13 14 10 8
    >>> BinarySearchTree().search(6)
    Traceback (most recent call last):
    ...
    IndexError: Warning: Tree is empty! please use another.
    """
    testlist = (8, 3, 6, 1, 10, 14, 13, 4, 7)
    t = BinarySearchTree()
    for i in testlist:
        t.insert(i)

    # Prints all the elements of the list in order traversal
    print(t)

    if t.search(6) is not None:
        print("The value 6 exists")
    else:
        print("The value 6 doesn't exist")

    if t.search(-1) is not None:
        print("The value -1 exists")
    else:
        print("The value -1 doesn't exist")

    if not t.empty():
        print("Max Value: ", t.get_max().value)
        print("Min Value: ", t.get_min().value)

    for i in testlist:
        t.remove(i)
        print(t)


if __name__ == "__main__":
    import doctest

    doctest.testmod()
    # binary_search_tree()
```
# Renference

[Implementation](https://github.com/TheAlgorithms/Python)
