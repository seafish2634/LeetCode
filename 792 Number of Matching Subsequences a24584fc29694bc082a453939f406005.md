# 792. Number of Matching Subsequences

Given a string `s` and an array of strings `words`, return *the number of* `words[i]` *that is a subsequence of* `s`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

- For example, `"ace"` is a subsequence of `"abcde"`.

**Example 1:**

```
Input: s = "abcde", words = ["a","bb","acd","ace"]
Output: 3
Explanation: There are three strings in words that are a subsequence of s: "a", "acd", "ace".

```

**Example 2:**

```
Input: s = "dsahjpjauf", words = ["ahjpjau","ja","ahbwzgqnuk","tnmlanowax"]
Output: 2
```

**Constraints:**

- `1 <= s.length <= 5 * 104`
- `1 <= words.length <= 5000`
- `1 <= words[i].length <= 50`
- `s` and `words[i]` consist of only lowercase English letters.

### Code:

```cpp
**class Solution {
public:
    int numMatchingSubseq(string s, vector<string>& words) {
        int res=0;
        vector<vector<int>> dic(27);
        for(int i=0;i<s.size();i++)
        {
             dic[s[i]-'a'].push_back(i);
        }
        for(int i=0;i<words.size();i++)
        {
            int fl=1,cur=-1;
            for(int j=0;j<words[i].size();j++)
            {
                if(dic[words[i][j]-'a'].size()==0)
                {
                    fl=0;
                    break;
                }
                else
                {
                    for(int k=0;k<dic[words[i][j]-'a'].size();k++)
                    {
                        if(dic[words[i][j]-'a'][k]>cur)
                        {
                            cur=dic[words[i][j]-'a'][k];
                            break;
                        }
                        else
                        {
                            if(k==dic[words[i][j]-'a'].size()-1)fl=0;
                        }
                    }
                }
            }
            if(fl)res++;
        }  
        return res;
    }
};**
```

## **Solution:**

---

### **if we check every element with every string just by check all of their char**

### **it will TLE!!.**

---

**so we use array to record every  char’s location in s.**

 **by ACII  ⇒ we can transfer char into integer.**

t**hen we can start to check the strings in words.**

---

### if the char of string in words doesn’t exist ⇒ break ⇒ fail.

### if char satisfied but location not ⇒ keep search ⇒ if no one bigger than current one ⇒ fail.

### if both char exist and location bigger than current location ⇒ success ⇒ renew current location.

---