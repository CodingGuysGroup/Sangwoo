### `문제 설명`

#### English

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

![image](https://user-images.githubusercontent.com/106041072/227897298-22343a42-4987-48d3-a1d1-8e5570e09e11.png)

For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given an integer, convert it to a roman numeral.

#### Korean

로마 숫자는 일곱 개의 다른 기호로 표현됩니다: I, V, X, L, C, D, M.

![image](https://user-images.githubusercontent.com/106041072/227897305-0460394b-b5b8-4e36-b9d5-0a1d99ebe0f4.png)

예를 들어, 2는 로마 숫자로 II로 쓰여지고, 2는 하나만 더하면 됩니다. 12는 X + II인 XII로 쓰여집니다. 27이라는 숫자는 XXVII로 적혀있는데 XX+V+II입니다.

로마 숫자는 보통 왼쪽에서 오른쪽으로 가장 큰 것부터 가장 작은 것까지 쓰여집니다. 그러나 4의 숫자는 III가 아닙니다. 대신에, 숫자 4는 IV로 쓰여져 있습니다. 왜냐하면 하나는 5보다 앞에 있기 때문에 4를 만드는 것을 뺄 수 있습니다. 같은 원리가 IX로 표기된 숫자 9에도 적용됩니다. 감산이 사용되는 예는 6가지입니다:

V(5)와 X(10) 앞에 배치하여 4와 9를 만들 수 있습니다.
X는 L(50)과 C(100) 앞에 배치하여 40과 90을 만들 수 있습니다.
C는 D(500)와 M(1000) 앞에 배치하여 400과 900을 만들 수 있습니다.
정수를 지정하면 로마 숫자로 변환합니다.

### `제한 사항`

- 1 <= num <= 3999
- 
### `결과`

Given an integer, convert it to a roman numeral.

정수를 지정하면 로마 숫자로 변환합니다.

### `입출력 예`
### Case 1

|Input|output|
|---|---|
|num=3|"III"|

#### Explanation

3 is represented as 3 ones.

### Case 2

|Input|output|
|---|---|
|num=58|"LVIII"|

#### Explanation

L = 50, V = 5, III = 3.

### Case 3

|Input|output|
|---|---|
|num=1994|"MCMXCIV"|

#### Explanation

M = 1000, CM = 900, XC = 90 and IV = 4.

### `ANS`

----

```
class Solution:
    def intToRoman(self, num: int) -> str:
        dic={}
        symbol=['M','D','C','L','X','V','I']
        value=[1000,500,100,50,10,5,1]
        special_symbol=['IV','IX','XL','XC','CD','CM'] #4,9,40,90,400,900은 특별한 수이므로 미리 리스트 만듬
        special_value=[4,9,40,90,400,900]
        ans="" #답을 담아둘 문자열
        num=str(num) #현재 숫자를 문자로 나눔
        num_list=[] #각 자리 수들을 담을 리스트
        for i in range(len(symbol)): #각 로마어에 따라 값을 dic 로 표현 ex){'M':1000 ... }
            dic[symbol[i]]=value[i]
        for i in range(len(special_symbol)): #각 특수한 값에 따라 문자을 dic 로 표현 ex){40:'XL'...}
            dic[special_value[i]]=special_symbol[i]
        for i in range(len(num)): #입력값을 각 자리 수로 나누어 리스트에 저장 ex) num=1994 [4 90 900 1000]
            num_list.append(int(num[len(num)-i-1])*(10**i))
        num_list.reverse() #큰 수부터 처리하기 위해서 역순 정렬
        for i in num_list: 
            if i in dic: #특수한 값이면
                ans+=dic[i] #특수값 먼저 처리 후 continue
                continue
            for j in symbol: #특수한 값이 아니면 1000,500,100 순으로 나눠 몫을 확인하고 처리
                if 0<i//dic[j]<=3: # 이때 몫이 5,6,7,8인 것은 높은 순으로 먼저 나눠 처리했기 때문에 나올 수 없음
                    ans+=j*(i//dic[j]) #현재 문자와 몫을 곱한 것을 ans에 추가 
                    i=i%dic[j] #나눈 나머지로 i 업데이트
        return ans

```

### `Runtime and Memory`

![image](https://user-images.githubusercontent.com/106041072/227915519-a5c5cdf9-2f9a-4a3f-b427-8d8bca6ec110.png)
