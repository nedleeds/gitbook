---
description: from Samsung SW Expert Academy
---

# 1. 전기버스

## 

### \[ 문제 \]

> 버스는 0번에서 출발해 종점인 N번 정류장까지 이동하고, 한번 충전으로 최대한 이동할 수 있는 정류장 수 K가 정해져 있다.
>
> 충전기가 설치된 M개의 정류장 번호가 주어질 때, 최소한 몇 번의 충전을 해야 종점에 도착할 수 있는지 출력하는 프로그램을 만드시오.
>
> 만약 충전기 설치가 잘못되어 종점에 도착할 수 없는 경우는 0을 출력한다. 출발지에는 항상 충전기가 설치되어 있지만 충전횟수에는 포함하지 않는다.

![](../../.gitbook/assets/samsung_1.jpg)

### \[ 입력 \] ​​​​

> ```python
> 첫 줄에 노선 수 T가 주어진다.  
> ( 1 ≤ T ≤ 50 )
>
> 각 노선별로 K, N, M이 주어지고, 다음줄에 M개의 정류장 번호가 주어진다. 
> ( 1 ≤ K, N, M ≤ 100 )
>
> --------------------------------------------------------
> 3
> 3 10 5
> 1 3 5 7 9
> 3 10 5
> 1 3 7 8 9
> 5 20 5
> 4 7 9 14 17
> --------------------------------------------------------
> ```

###  \[ 출력 \]

> ```python
>
> '#'과 노선번호, 빈칸에 이어 최소 충전횟수 또는 0을 출력한다.
> --------------------------------------------------------
> #1 3
> #2 0
> #3 4
> --------------------------------------------------------
> ```

### \[ 코드 \]

{% tabs %}
{% tab title="문제해석" %}
1. 노선에 따라서 버스가 다닌다.
2. k만큼만 이동할 수 있고 k만큼 움직이면 충전을 해야한다.
3. k : 버스 최대 이동 거리, n: 종착역 위치, m: 충전소 위치
{% endtab %}

{% tab title="핵심파악" %}
> 1. 버스는 충전소를 반드시 지난다.
> 2. 충전소에 도착하면 조건에 따라서 충전여부를 결정한다.
>
>    \[조건\]
>
>    ```python
>    if leftOil>=nxt[idx] : # 남은 기름 >= 다음 충전소까지 거리    
>        pass               # 기름이 있으므로 pass
>    elif nxt[idx]>k:       # 이동할 거리 > 최대 이동가능 거리    
>        return 0           # stop 해야돼
>    else:
>        charge += 1        # 충전횟수 += 1    
>        leftOil = k        # 기름을 가득 채움
>    ```
>
>    * 구현에 사용할 자료구조 :
>      * list
>    * prv = \[ \] : 이전 충전소 &lt;-&gt; 현재 충전소 거리
>    * nxt = \[ \]   :  현재 충전소 &lt;-&gt; 다음 충전소 거리
>    * mList = \[ \] : 충전소 위치 리스트
>
>      +\) 탐색 방법 : 충전소 위치별 완전 탐색.
{% endtab %}

{% tab title="틀" %}
```python
#==============[ getDist ]===============
argument : mList, nreturn prv, nxt
#========================================


#==============[ oilStatus ]=============
argument : mList, prv, nxt, k, nreturn minChargeNum
#========================================


#==============[ getDist ]===============
prv, nxt = getDist(mList, n)
answer = oilStatus(mList, prv, nxt, k, n)
return answer
#========================================
```
{% endtab %}

{% tab title="CODE" %}
```python
def getDist(l, n):
	prv, nxt, p = [], [], 0
	for i in l:
		prv.append(i-p)
		p=i
	nlist = l[1:]
	nlist.append(n)
	p=l[0]
	for j in nlist:
		nxt.append(j-p)
		p=j
	return prv, nxt

def oilCheck(mList, prv, nxt, k):
	leftOil, charge = k, 0
	for idx in range(0, len(mList)):
		leftOil-=prv[idx]
		if(leftOil>=nxt[idx]): pass
		elif(nxt[idx]>k): 		return 0
		else:
			charge+=1
			leftOil = k
	return charge
    
T = int(input())

for test_case in range(1, T + 1):
	k,n,m = map(int, input().split())
	mList = list(map(int, input().split()))
	num = 0

	prv, nxt = getDist(mList,n)
	num = oilCheck(mList, prv, nxt, k)
	print("#%d %d" %(test_case, num))
```
{% endtab %}
{% endtabs %}

