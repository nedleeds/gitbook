# 2. 숫자카드

**※ SW Expert 아카데미의 문제를 무단 복제하는 것을 금지합니다.**  
  
  
0에서 9까지 숫자가 적힌 N장의 카드가 주어진다.  
  
가장 많은 카드에 적힌 숫자와 카드가 몇 장인지 출력하는 프로그램을 만드시오. 카드 장수가 같을 때는 적힌 숫자가 큰 쪽을 출력한다.

**\[입력\]**  
 

첫 줄에 테스트 케이스 개수 T가 주어진다.  \( 1 ≤ T ≤ 50 \)

다음 줄부터 테스트케이스의 첫 줄에 카드 장수 N이 주어진다. \( 5 ≤ N ≤ 100 \)

다음 줄에 N개의 숫자 ai가 여백없이 주어진다. \(0으로 시작할 수도 있다.\)  \( 0 ≤ ai ≤ 9 \) 

**\[출력\]**  
 

각 줄마다 "\#T" \(T는 테스트 케이스 번호\)를 출력한 뒤, 가장 많은 카드의 숫자와 장 수를 차례로 출력한다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Input</th>
      <th style="text-align:left">Output</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">3
        <br />5
        <br />49679
        <br />5
        <br />08271
        <br />10
        <br /><a href="tel:7797946543">7797946543</a>
      </td>
      <td style="text-align:left">
        <p>#1 9 2</p>
        <p>#2 8 1</p>
        <p>#3 7 3</p>
      </td>
    </tr>
  </tbody>
</table>{% tabs %}
{% tab title="myCode" %}
```python
def prevSearch(numbers, now):
	numSame = []
	cnt=0
	idx = []
	for i in range(0, len(numbers)):
		if now == numbers[i]:
			if i==0: # 첫번째 카드면 어차피 같으니깐 패스.
				pass
			else:	# 두번째 카드부터 같으면 cnt + 1
				cnt+=1
				idx.append(i)
		else:		# 카드가 다르면 횟수 세지 않음.
			pass
	return cnt, idx

def findBiggest(table, numbers):
	M = max(table) 							 # table은 각 카드별로 나온 횟수가 중첩된 값들이다. 여기서 제일 큰값이 바로 가장많은 카드수가 된다.
	cnt, idx = prevSearch(table,M)   # M과 비교해서 table에 또 다른 같은수의 최대양이 있는 지 비교한다. 반환 => cnt, index
	pos = 0
	pos = max(idx) 					     	 # 결론 : max(idx)를 하면 최대값을 int형으로 반환하기 때문에 pos = max(idx) 를 하면된다.
	num = numbers[pos]
	amount = M
	return num, amount 
  
def search(numbers, numCard):
	table = []
	for idx in range(0, numCard):
		now = numbers[idx]
		cnt = 1
		numSame, _ = prevSearch(numbers[:idx], now)
		if numSame == 0:
			pass
		else:
			cnt += numSame
		table.append(cnt)    
	num, amount = findBiggest(table, numbers)
	return num, amount 

T = int(input())
for test_case in range(1, T + 1):
	numCard = int(input())
	numbers = list(map(int, input()))
	numbers.sort()
	num, amount = search(numbers, numCard)
	print("#{} {} {}".format(test_case, num, amount))



```
{% endtab %}

{% tab title="other\'s Code" %}

{% endtab %}
{% endtabs %}

