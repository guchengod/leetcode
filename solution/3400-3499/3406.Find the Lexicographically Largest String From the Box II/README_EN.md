---
comments: true
difficulty: Hard
edit_url: https://github.com/doocs/leetcode/edit/main/solution/3400-3499/3406.Find%20the%20Lexicographically%20Largest%20String%20From%20the%20Box%20II/README_EN.md
tags:
    - Two Pointers
    - String
---

<!-- problem:start -->

# [3406. Find the Lexicographically Largest String From the Box II 🔒](https://leetcode.com/problems/find-the-lexicographically-largest-string-from-the-box-ii)

[中文文档](/solution/3400-3499/3406.Find%20the%20Lexicographically%20Largest%20String%20From%20the%20Box%20II/README.md)

## Description

<!-- description:start -->

<p>You are given a string <code>word</code>, and an integer <code>numFriends</code>.</p>

<p>Alice is organizing a game for her <code>numFriends</code> friends. There are multiple rounds in the game, where in each round:</p>

<ul>
	<li><code>word</code> is split into <code>numFriends</code> <strong>non-empty</strong> strings, such that no previous round has had the <strong>exact</strong> same split.</li>
	<li>All the split words are put into a box.</li>
</ul>

<p>Find the <strong>lexicographically largest</strong> string from the box after all the rounds are finished.</p>

<p>A string <code>a</code> is <strong>lexicographically smaller</strong> than a string <code>b</code> if in the first position where <code>a</code> and <code>b</code> differ, string <code>a</code> has a letter that appears earlier in the alphabet than the corresponding letter in <code>b</code>.<br />
If the first <code>min(a.length, b.length)</code> characters do not differ, then the shorter string is the lexicographically smaller one.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">word = &quot;dbca&quot;, numFriends = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">&quot;dbc&quot;</span></p>

<p><strong>Explanation:</strong></p>

<p>All possible splits are:</p>

<ul>
	<li><code>&quot;d&quot;</code> and <code>&quot;bca&quot;</code>.</li>
	<li><code>&quot;db&quot;</code> and <code>&quot;ca&quot;</code>.</li>
	<li><code>&quot;dbc&quot;</code> and <code>&quot;a&quot;</code>.</li>
</ul>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">word = &quot;gggg&quot;, numFriends = 4</span></p>

<p><strong>Output:</strong> <span class="example-io">&quot;g&quot;</span></p>

<p><strong>Explanation:</strong></p>

<p>The only possible split is: <code>&quot;g&quot;</code>, <code>&quot;g&quot;</code>, <code>&quot;g&quot;</code>, and <code>&quot;g&quot;</code>.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>word</code> consists only of lowercase English letters.</li>
	<li><code>1 &lt;= numFriends &lt;= word.length</code></li>
</ul>

<!-- description:end -->

## Solutions

<!-- solution:start -->

### Solution 1

<!-- tabs:start -->

#### Python3

```python
class Solution:
    def answerString(self, word: str, numFriends: int) -> str:
        if numFriends == 1:
            return word
        s = self.lastSubstring(word)
        return s[: len(word) - numFriends + 1]

    def lastSubstring(self, s: str) -> str:
        i, j, k = 0, 1, 0
        while j + k < len(s):
            if s[i + k] == s[j + k]:
                k += 1
            elif s[i + k] < s[j + k]:
                i += k + 1
                k = 0
                if i >= j:
                    j = i + 1
            else:
                j += k + 1
                k = 0
        return s[i:]
```

#### Java

```java
class Solution {
    public String answerString(String word, int numFriends) {
        if (numFriends == 1) {
            return word;
        }
        String s = lastSubstring(word);
        return s.substring(0, Math.min(s.length(), word.length() - numFriends + 1));
    }

    public String lastSubstring(String s) {
        int n = s.length();
        int i = 0, j = 1, k = 0;
        while (j + k < n) {
            int d = s.charAt(i + k) - s.charAt(j + k);
            if (d == 0) {
                ++k;
            } else if (d < 0) {
                i += k + 1;
                k = 0;
                if (i >= j) {
                    j = i + 1;
                }
            } else {
                j += k + 1;
                k = 0;
            }
        }
        return s.substring(i);
    }
}
```

#### C++

```cpp
class Solution {
public:
    string answerString(string word, int numFriends) {
        if (numFriends == 1) {
            return word;
        }
        string s = lastSubstring(word);
        return s.substr(0, min(s.length(), word.length() - numFriends + 1));
    }

    string lastSubstring(string& s) {
        int n = s.size();
        int i = 0, j = 1, k = 0;
        while (j + k < n) {
            if (s[i + k] == s[j + k]) {
                ++k;
            } else if (s[i + k] < s[j + k]) {
                i += k + 1;
                k = 0;
                if (i >= j) {
                    j = i + 1;
                }
            } else {
                j += k + 1;
                k = 0;
            }
        }
        return s.substr(i);
    }
};
```

#### Go

```go
func answerString(word string, numFriends int) string {
	if numFriends == 1 {
		return word
	}
	s := lastSubstring(word)
	return s[:min(len(s), len(word)-numFriends+1)]
}

func lastSubstring(s string) string {
	n := len(s)
	i, j, k := 0, 1, 0
	for j+k < n {
		if s[i+k] == s[j+k] {
			k++
		} else if s[i+k] < s[j+k] {
			i += k + 1
			k = 0
			if i >= j {
				j = i + 1
			}
		} else {
			j += k + 1
			k = 0
		}
	}
	return s[i:]
}
```

#### TypeScript

```ts
function answerString(word: string, numFriends: number): string {
    if (numFriends === 1) {
        return word;
    }
    const s = lastSubstring(word);
    return s.slice(0, word.length - numFriends + 1);
}

function lastSubstring(s: string): string {
    const n = s.length;
    let i = 0;
    for (let j = 1, k = 0; j + k < n; ) {
        if (s[i + k] === s[j + k]) {
            ++k;
        } else if (s[i + k] < s[j + k]) {
            i += k + 1;
            k = 0;
            if (i >= j) {
                j = i + 1;
            }
        } else {
            j += k + 1;
            k = 0;
        }
    }
    return s.slice(i);
}
```

<!-- tabs:end -->

<!-- solution:end -->

<!-- problem:end -->
