# function
function 컨셉 + 문제  
이번 강의에서는 positional argument(위치 인자)만 다룸


## argument, parameter, return
> : def func(parameter1, parameter2, ..)    -> 받을 때, parameter(매개변수)  
> : func(argument1, argument2, ..)          -> 보낼 때, argument(인자)  
> : return val                              -> val값 리턴, 없을 시 생략 가능  

~~~
def func():
    print('기본함수')
func()

>> 기본함수
~~~
~~~
def func2(a,b):
    print(a+b)
func2(3,5)

>> 8
~~~
~~~
def func3(a,b):
    return a+b
print(func3(3,5))

>> 8
~~~
~~~
num = 10        # 전역변수
li = [1,2,3]

# 전달시, 같은 객체를 가리킴
def func4(a,b):
    print(id(a), id(b))
func4(num,li)

>> 4553380880 4532554112
~~~
~~~
def func44(a,b):
    print(id(a), id(b))
    a += 10                 # 새로운 객체에 할당
    b.append(4)             # 기존 객체에 수정(li 수정 적용)
    b += [5]                # 기존 객체에 수정(li 수정 적용, 동일 id가 유지
    b = b + [6]             # 새로운 객체에 할당, 다른 id를 사용
    print(id(a), id(b))
    print(a,b)
func44(num, li)

>> 4419765264 4398942592
>> 4419765584 4404772288
>> 20 [1, 2, 3, 4, 5, 6]
~~~
~~~
print(num, li)

>> 10 [1, 2, 3, 4, 5]
~~~
~~~
print(id(num), id(li))

>> 44419765264 4398942592
~~~
## global 변수
>  : 함수 내에서 전역변수 사용함을 지칭  
>  : 명시 되지 않으면 지역변수 우선 접근, 없으면 전역변수 접근  

### global 없이 전역변수 접근, 멤버 함수 사용
~~~
def func5():
    li.append(6)
    print(num, li)
func5()

>> 10 [1, 2, 3, 4, 5, 6]
~~~
~~~
def func6():
    # global num, li        # num, li 가 전역변수임을 명시
    # num += 20             # global 없으면 지역변수 변경(생성 전이므로 에러)
    # li = li + [5]         # global 없으면 지역변수 변경(생성 전이므로 에러)
    num = 10                # global 없으면 지역변수 생성, 있으면 전역변수에 할당
    li = [10,11,12]         # global 없으면 지역변수 생성, 있으면 전역변수에 할당
    print(num, li)
func6()
print(num, li)

>> 10 [10, 11, 12]
>> 10 [1, 2, 3, 4, 5, 6]
~~~

## default argument value
>  : 인자가 개수에 맞지 않게 전달될 때, 순서에 맞게 기본값으로 설정된다.  
>  : default argument 이후는 전부 default argument 이어야 한다.  

~~~
def func7(a, b=10):
    print(a,b)
func7(20, 30)
func7(20)

>> 20 30
>> 20 10
~~~

## arbitrary (positional) argument  
> : 위치 가변 인자  
> : 매칭되고 남은 모든 인자들을 tuple로 받는다.  
> : positional argument 마지막에 온다.  

~~~
def func8(*args):
    print(args)
func8(1,2,3,4,5)

def func9(a=1, *args):
    print(a, args)
func9(1, 2, 3, 4, 5)
func9(10)
func9()

>> 1 (2, 3, 4, 5)
>> 10 ()
>> 1 ()
~~~

## unpacking argument
>  : iterable 객체를 원소 낱개로 전달한다.  

~~~
print(*[1,2,3])

def func10(a,b,c):
    print(a,b,c)
func10(*'abc')

>> a b c
~~~

~~~
def func11(a,b,*args):
    print(a,b,args)
func11(*'abcdeftg')

>> a b ('c', 'd', 'e', 'f', 't', 'g')
~~~

## lambda
>  : 익명 함수
>  : 주로 map, sorted 등 함수를 인자로 하는 고차함수에서 사용
>  : lambda 매개변수 : 표현식(반환값)

~~~
f = lambda a,b : a+b
print(f(3,5))

>> 8
~~~

~~~
print((lambda a, b : a +b)(3,5))

>> 8
~~~

## map(func, iterable)
~~~
print(*map(int, '12345'))

>> 1 2 3 4 5
~~~
~~~
print(*map(lambda x : int(x), '12345'))

>> 1 2 3 4 5
~~~
~~~
print(*map(lambda x : int(x)**2, '12345'))

>> 1 4 9 16 25
~~~
~~~
print(*map(abs,[1,-5,-10,3,7]))

>> 1 5 10 3 7
~~~
~~~
print(*map(lambda x : abs(x) + 10 ,[1,-5,-10,3,7]))

>> 11 15 20 13 17
~~~


## sorted (iterable, key[func], reverse[True/False])
~~~
print(sorted([5,4,3,2,1]))

>> [1, 2, 3, 4, 5]
~~~
~~~
print(sorted([5,4,3,2,1], key=lambda x : -x))

>> [5, 4, 3, 2, 1]
~~~
~~~
print(sorted([-5,-4,-3,-2,-1]))

>> [-5, -4, -3, -2, -1]
~~~
~~~
print(sorted([-5,-4,-3,-2,-1], key=abs))

>> [-1, -2, -3, -4, -5]
~~~
~~~
print(sorted([-5,-4,-3,-2,-1], key=lambda x : abs(x)))
>> [-1, -2, -3, -4, -5]
~~~


# List

### sequence common

operation|Result|Time|Example|result
--|--|--|--|--
x in s|s에 x값이 있으면 True|O(n)|1 in [1,2,3]|True
x not in s|s에 x값이 없으면 True|O(n)|4 not in [1,2,3]|True
s + t|s와 t를 연결|O(n)|[1,2,3] + [4,5,6]|[1,2,3,4,5,6]
s\*k or k*s|s를 n번 반복|O(n*k)|[1,2,3]*3|[1,2,3,1,2,3,1,2,3]
x[i]|i 위치의 값|O(1)|'abc'[1]|'b'
x[i:j]|[i:j] 범위로 슬라이싱|O(m)|'abcdef'[2:4]|'cd'
x[i:j:k]|[i:j] 범위를 k 단위로 슬라이싱|O(n)|'abcdefg'[1:6:2]|'bdf'
len(s)|s의 길이|O(1)|len['abcdef']|6
min(s)|s에서 가장 작은 값|O(n)|min[5,4,2,6,1]|1
max(s)|s에서 가장 큰 값|O(n)|max[5,4,2,6,1]|6
s.index(x[,i[,j]])|x가 등장하는 가장 앞선 index (i, j 설정시 [i:j]로 검색 범위 제한)|O(n)|[2,3,1,3].index(3)|1
s.count(x)|x가 등장하는 횟수|O(n)|[2,3,1,3].count(3)|2
s==t|모든 원소가 같으면 True|O(n)|[1,2,3]==[1,2,3]|True
s\<t|s의 앞에 원소가 작으면 True|O(n)|[1,2,3]<[2,1,1]|True
s\>t|s의 앞에 원소가 크면 True|O(n)|[2,2,2]<[1,5,5]|True

## sequence mutable only (s=[0,1,2,3])

operation|Result|Time|Example|result
--|--|--|--|--
s[i]=x|s[i]를 x로 변경|O(1)|s[2]=0|[0,1,0,3]
s[i:j]=t|s[i:j]를 iterable t로 변경|O(n)|s[1:]=[5,5]|[0,5,5]
del s[i:j]|s[i:j] 삭제|O(n)|del s[1:]|[0]
s[i:j:k]=t|s[i:j:k]의 각 위치 값을 iterable t의 원소로 순서대로 변경|O(n)|s[1::2]=[5:5]|[0,5,2,5]
del s[i:j:k]|s[i:j:k] 삭제|O(n)|del s[::2]|[1,3]
