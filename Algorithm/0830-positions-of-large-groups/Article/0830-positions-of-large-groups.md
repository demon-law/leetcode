# 830. 较大分组的位置

---

题目来源：力扣（LeetCode）[https://leetcode-cn.com/problems/positions-of-large-groups/](https://leetcode-cn.com/problems/positions-of-large-groups/)

## 题目

---

在一个由小写字母构成的字符串 `s` 中，包含由一些连续的相同字符所构成的分组。

例如，在字符串 `s = "abbxxxxzyy"` 中，就含有 `"a"`, `"bb"`, `"xxxx"`, `"z"` 和 `"yy"` 这样的一些分组。

分组可以用区间 `[start, end]` 表示，其中 `start` 和 `end` 分别表示该分组的起始和终止位置的下标。上例中的 `"xxxx"` 分组用区间表示为 `[3,6]` 。

我们称所有包含大于或等于三个连续字符的分组为 **较大分组** 。

找到每一个 **较大分组** 的区间，**按起始位置下标递增顺序排序后**，返回结果。

 

**示例 1：**

```
输入：s = "abbxxxxzzy"
输出：[[3,6]]
解释："xxxx" 是一个起始于 3 且终止于 6 的较大分组。
```

**示例 2：**

```
输入：s = "abc"
输出：[]
解释："a","b" 和 "c" 均不是符合要求的较大分组。
```

**示例 3：**

```
输入：s = "abcdddeeeeaabbbcd"
输出：[[3,5],[6,9],[12,14]]
解释：较大分组为 "ddd", "eeee" 和 "bbb"
```

**示例 4：**

```
输入：s = "aba"
输出：[]
```

**提示：**

- `1 <= s.length <= 1000`
- `s` 仅含小写英文字母

## 解题思路

---

### 思路：双指针

先审题，题目中给定一个字符串（仅包含小写字母），要求返回较大分组的区间，按照起始位置下标递增顺序排序返回结果。

其中涉及的分组概念为：字符串中连续相同字符构成分组。

**较大分组**：表示分组中连续相同字符的个数大于或等于 3，称为较大分组。

题目后面提示中说明，给定字符串的数组长度范围为 $[1, 1000]$。

在这里，我们使用双指针的方法来解答这个问题，具体的思路如下：

- 首先声明双指针 $left、right$，初始化 $left = 0、right = 1$（因为字符串长度至少为 $1$，这里直接初始化 $right$ 为 $1$，那么计算相同字符个数 $right - left$ 至少为 $1$）；
- 开始遍历，移动 $right$，进行判断；
- 如果 $left$ 和 $right$ 指针所对应的字符相同时，继续移动 $right$ 指针；
- 如果 $left$ 和 $right$ 指针所对应的字符不相同时，计算前面相同字符的个数，判断是否大于或等于 $3$：
  - 当满足条件时，将对应的起始索引位置添加到结果列表中，维护更新 $left$，令 $left=right$；
  - 否则，直接更新 $left=right$。
- 注意，$right$ 会越界，当越界时，按照上面的步骤进行处理。
- 最终返回结果列表 $ans$。

具体代码实现如下。

```python
class Solution:
    def largeGroupPositions(self, s: str) -> List[List[int]]:
        left = 0
        right = 1

        ans = []
        n = len(s)
        
        while right <= n:
            # right 越界或 s[left] != s[right] 时的处理
            if right == n or s[left] != s[right]:
                if right - left >= 3:
                    ans.append([left, right - 1])
                # 注意维护更新 left
                left = right
            right += 1
        return ans
```

## 欢迎关注

---

公众号 【[书所集录](https://i.loli.net/2020/07/09/sNEGeV8g6fmW5Ub.jpg)】

---

**如有错误，烦请指正，欢迎指点交流。如果觉得写得还可以，麻烦点个赞👍，谢谢。**

