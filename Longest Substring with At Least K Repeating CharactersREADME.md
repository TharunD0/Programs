class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        if not s or len(s) == 0:
            return 0
        if k == 1:
            return len(s)
        max_len = 0
        for i in range(26):
            start = 0
            end = 0
            unique = 0
            count = [0] * 26
            while end < len(s):
                if unique <= i:
                    idx = ord(s[end]) - ord('a')
                    if count[idx] == 0:
                        unique += 1
                    count[idx] += 1
                    end += 1
                else:
                    idx = ord(s[start]) - ord('a')
                    if count[idx] == 1:
                        unique -= 1
                    count[idx] -= 1
                    start += 1
                if unique == i:
                    valid = True
                    for j in range(26):
                        if count[j] > 0 and count[j] < k:
                            valid = False
                            break
                    if valid:
                        max_len = max(max_len, end - start)
        return max_len
