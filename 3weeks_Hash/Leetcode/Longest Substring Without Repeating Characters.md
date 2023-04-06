### `문제 설명`

### English

Given a string s, find the length of the longest substring without repeating characters.

### Korea

문자열 s가 지정되면 반복 문자가 없는 가장 긴 하위 문자열의 길이를 찾습니다.

### `제한 사항`

- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces.

### `결과`

Find the length of the longest substring without repeating characters.

문자열 s가 지정되면 반복 문자가 없는 가장 긴 하위 문자열의 길이를 찾습니다.

### `입출력 예`

### Case 1

|input|output|
|---|---|
|"abcabcbb"|3|

#### Explanation

The answer is "abc", with the length of 3.

답은 길이가 3인 "abc"이다.

### Case2

|input|output|
|---|---|
|"bbbbb"|1|

#### Explanation

The answer is "b", with the length of 1.

답은 "b"이고 길이는 1이다.

### Case3

|input|output|
|---|---|
|"pwwkew"|3|

#### Explanation

The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

답은 길이가 3인 "wke"이다.
"pwke"는 하위 문자열이 아니라 하위 문자열이어야 합니다.

----

### `ANS`

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        cnt=0 #substring 길이를 재는 변수
        start=0 #반복이 시작되는 시점을 표시할 변수
        dic={}
        for i in range(len(s)):
            if s[i] not in dic: #dic에 해당 문자가 없으면
                dic[s[i]]=i # dic에 문자 넣음
            else: #문자 있으면
                if dic[s[i]]>=start: #반복 시작 되는 부분 확인 ex) acbebc 경우 앞에 있는 c보다 b가 start 가 되야함
                    start=dic[s[i]]+1 #반복 시작 되는 부분(=start) 선언 이때(+1하는 이유는 문자가 1개 있는 경우 고려해야함)
                dic[s[i]]=i
            cnt=max(cnt,i-start+1) #substring 중 최대 길이 계속 비교
        return cnt
```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/226248595-30882d8d-861b-47a2-acd7-1f612516fdf2.png)
