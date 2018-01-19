# Leetcode: Implement Trie (Prefix Tree)     :BLOG:Basic:


---

Implement Trie (Prefix Tree)  

---

Implement a trie with insert, search, and startsWith methods.  

Note:  
You may assume that all inputs are consist of lowercase letters a-z.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/implement-trie-prefix-tree)  

Credits To: [Leetcode.com](https://leetcode.com/problems/implement-trie-prefix-tree/description/)  

Leave me comments, if you know how to solve.  

    ## Basic Ideas: TrieNode: is_word(bool), children(dict)
    ##             For the root node, we don't store any characters. Only in children
    ## Assumption: If one word in the Trie tree, we also treat it starts with the word.
    ## Complexity:
    class TrieNode(object):
        def __init__(self):
            self.children = {}
            self.is_word = False
    
    class Trie(object):
    
        def __init__(self):
            """
            Initialize your data structure here.
            """
            self.root = TrieNode()
    
        def insert(self, word):
            """
            Inserts a word into the trie.
            :type word: str
            :rtype: void
            """
            node = self.root
            # check character by character
            for ch in word:
                children = node.children
                # find which child
                if ch not in children:
                    new_child = TrieNode()
                    children[ch] = new_child
                node = children[ch]
            node.is_word = True
    
        def search(self, word):
            """
            Returns if the word is in the trie.
            :type word: str
            :rtype: bool
            """
            node = self.root
            for ch in word:
                children = node.children
                if ch not in children:
                    return False
                node = children[ch]
            return node.is_word
    
        def startsWith(self, prefix):
            """
            Returns if there is any word in the trie that starts with the given prefix.
            :type prefix: str
            :rtype: bool
            """
            node = self.root
            for ch in prefix:
                children = node.children
                if ch not in children:
                    return False
                node = children[ch]
            return True
    
    # Your Trie object will be instantiated and called as such:
    # obj = Trie()
    # obj.insert(word)
    # param_2 = obj.search(word)
    # param_3 = obj.startsWith(prefix)