
# Leetcode: Construct Binary Tree from Inorder and Postorder Traversal     :BLOG:Basic:

---

Construct Binary Tree from Inorder and Postorder Traversal  

---

Similar Problems:  

-   Tag: [#treetraversal](https://code.dennyzhang.com/tag/treetraversal)

---

Given inorder and postorder traversal of a tree, construct the binary tree.  

Note:  
You may assume that duplicates do not exist in the tree.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/construct-binary-tree-from-inorder-and-postorder-traversal)  

Credits To: [leetcode.com](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/construct-binary-tree-from-inorder-and-postorder-traversal
    ## Basic Ideas:
    ##         Inorder:    L M R
    ##         Postorder:  L R M
    ##       Take the last in postorder as root
    ##       Find root in inorder
    ##       Then locate left sub-tree and right sub-tree
    ## Complexity: Time O(n), Space O(n)
    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution(object):
        def buildTree(self, inorder, postorder):
    	"""
    	:type inorder: List[int]
    	:type postorder: List[int]
    	:rtype: TreeNode
    	"""
    	if len(inorder) == 0:
    	    return None
    	root_val = postorder[-1]
    	ltree_index = inorder.index(root_val)
    	left_node = self.buildTree(inorder[0:ltree_index], postorder[0:ltree_index])
    	right_node = self.buildTree(inorder[ltree_index+1:], postorder[ltree_index:-1])
    
    	node = TreeNode(root_val)
    	node.left, node.right = left_node, right_node
    	return node
