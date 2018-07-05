
# Leetcode: Replace Words     :BLOG:Medium:

---

Replace Words  

---

Similar Problems:  

-   [Review: Trie Tree Problems](https://code.dennyzhang.com/review-trie)
-   Tag: [#trie](https://code.dennyzhang.com/tag/trie)

---

In English, we have a concept called root, which can be followed by some other words to form another longer word - let's call this word successor. For example, the root an, followed by other, which can form another word another.  

Now, given a dictionary consisting of many roots and a sentence. You need to replace all the successor in the sentence with the root forming it. If a successor has many roots can form it, replace it with the root with the shortest length.  

You need to output the sentence after the replacement.  

    Example 1:
    Input: dict = ["cat", "bat", "rat"]
    sentence = "the cattle was rattled by the battery"
    Output: "the cat was rat by the bat"

Note:  

1.  The input will only have lower-case letters.
2.  1 <= dict words number <= 1000
3.  1 <= sentence words number <= 1000
4.  1 <= root length <= 100
5.  1 <= sentence words length <= 1000

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/replace-words)  

Credits To: [leetcode.com](https://leetcode.com/problems/replace-words/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/replace-words
    ## Basic Ideas: Trie Tree
    ##              Build a Trie Tree from dict
    ##              For each word in sentence, find the shortest prefix
    ## Complexity: O(1), Space O(1). Because all variables have upper limits.
    class TrieNode(object):
        def __init__(self):
    	self.children = collections.defaultdict(TrieNode)
    	self.is_word = False
    
    class Solution(object):
        def replaceWords(self, dict, sentence):
    	"""
    	:type dict: List[str]
    	:type sentence: str
    	:rtype: str
    	"""
    	root = TrieNode()
    	for word in dict:
    	    node = root
    	    for ch in word:
    		node = node.children[ch]
    	    node.is_word = True
    
    	# replace word by word
    	res = []
    	for word in sentence.split(' '):
    	    node, prefix = root, ''
    	    # check word
    	    for ch in word:
    		# If ch not in the children or children is empty, quit
    		if ch not in node.children:
    		    # mark previous result as invalid
    		    prefix = ''
    		    break
    		# match some prefix
    		prefix = '%s%s' % (prefix, ch)
    		# quit for the shortest path. Notice we shouldn't check node.is_word
    		if node.children[ch].is_word:
    		    break
    		# go further
    		node = node.children[ch]
    
    	    # insert the modified word
    	    if prefix != '':
    		res.append(prefix)
    	    else:
    		res.append(word)
    	return ' '.join(res)
    
    # s = Solution()
    # print s.replaceWords(["a", "aa", "aaa", "aaaa"], "a aa") # a a
    # print s.replaceWords(["a", "aa", "aaa", "aaaa"], "a aa a aaaa aaa aaa aaa aaaaaa bbb baba ababa") # a a a, bbb, baba, a
