---
title: python实现前缀树（Trie树）
date: 2020-07-30 11:01:00
tags: 
- python
- 算法
description: 介绍并使用python实现前缀树算法。
---



#### 前缀树的一些应用

- 搜索补全
- IP路由的最长前缀补全

#### python实现

```python
class Node:
    def __init__(self, val=None, next=[], isEnd=False):
        self.val = val
        self.next = {i.val: i for i in next}
        self.isEnd = isEnd

class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.node = Node()

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        tmp = self.node
        for c in word:
            if c not in tmp.next:
                tmp.next[c] = Node(val=c)
            tmp = tmp.next[c]
        tmp.isEnd = True


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        tmp = self.node
        for c in word[:-1]:
            if c not in tmp.next:
                return False
            tmp = tmp.next[c]
        return word[-1] in tmp.next and tmp.next[word[-1]].isEnd


    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        tmp = self.node
        for c in prefix:
            if c not in tmp.next:
                return False
            tmp = tmp.next[c]
        return True



# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

