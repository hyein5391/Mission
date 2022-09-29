# Mission

# Student class를 작성하세요
  Person class 와 score class를 작성하고 이를 이용하여 Student class를 완성하세요.
  KBD 혹은 File을 이용하여 학생의 이름과 학번, 성적 정보를 입력하고 이를 출력하세요


person 에 이름 전번
stdent 에 person을 상속 시킨다 [student 에 학번 학년 반 작성]
scora 에 student를 상속 시킨다


class person :
    name = ""    #name이 스트링 문자열이라 인식
    age = -1    #선언은 되어있지만 아무 값도 들어가있지 않음
    phone = ""
  
    def __init__(self, n, a, p) : #생성자를 넣어준다 매소드가 주어져야한다
    self.name = n
    self.age = a
    self.phone = p
while True :
    n = input("Name :")
    a = input("나이 : ")
    p = input("번호: ")
 
#---------------------------------------------------------------------------------------------------------------------------------------------------------
class 를 이용하여
이름 성적 성적에대한 평균을 나타내시오



import pickle
 
class Student:
    def __init__(self,name,kor,eng,mat):
        self.name = name
        self.kor = kor
        self.eng = eng
        self.mat = mat
        self.total = kor+eng+mat
        self.avg = self.total/3
    def student_print(self):
        print(self.name,"\t",self.kor,"\t",self.eng,"\t",self.mat,"\t",self.total,"\t%.3f"%self.avg);
 
 
    def student_name(self):
        return self.name
    def student_avg(self):
        return self.avg
 
    def __lt__(self, other):
        return self.avg > other.avg
 
    def student_reply(self,kor,eng,mat):
        self.kor = kor
        self.eng = eng
        self.mat = mat
        self.total = kor+eng+mat
        self.avg = self.total/3
 
 
class File_IO:
    def __init__(self,data):
        self.student_list = []
        self.data=data
 
    def file_read(self):
        try:
            with open(self.data,"rb") as file:
                while(True):
                    try:
                        self.student_list=pickle.load(file)
                    except EOFError:
                        break
        except FileNotFoundError:
            pass
    
    def file_write(self):
        with open(self.data,"wb") as file:
            pickle.dump(self.student_list,file)
 
 
class Function(File_IO):
    def input_info(self):
        name = input("이름:")
        korea = int(input("국어:"))
        english = int(input("영어:"))
        math = int(input("수학:"))
        tmp_student = Student(name,korea,english,math)
        
        super().file_read()
        self.student_list.append(tmp_student)
        super().file_write()
        
    def print_all(self):
        super().file_read()
        print("이름\t국어\t영어\t수학\t총점\t평균")
        for i in self.student_list:
            i.student_print()
            
    def search_name(self):
        name = input("이름:")
        super().file_read()
        print("이름\t국어\t영어\t수학\t총점\t평균")
        for i in self.student_list:
            if i.student_name() == name:
                i.student_print()
                
    def search_avg(self):
        avg = float(input("점수:"))
        super().file_read()
        print("이름\t국어\t영어\t수학\t총점\t평균")
        sorted_mylist = sorted(self.student_list)
        for i in sorted_mylist:
            if i.student_avg() >=avg:
                i.student_print()
 
    def insert(self):
        name = input("이름:")
        num=-1
        super().file_read()
        for i in range(len(self.student_list)):
            if self.student_list[i].student_name() == name:
                num = i
                break;
        if(num!=-1):
            korea = int(input("국어:"))
            english = int(input("영어:"))
            math = int(input("수학:"))
            self.student_list[i].student_reply(korea,english,math)
        super().file_write()
        
    def delete(self):
        name = input("이름:")
        num=-1
        super().file_read()
        for i in range(len(self.student_list)):
            if self.student_list[i].student_name() == name:
                num = i
                break;
        if(num!=-1):
            del self.student_list[i]
        super().file_write()
 
def main():
    score_list = Function("test.txt")
    while(True):
        num = int(input("기능선택(1.입력 2.전체출력 3.이름검색 4.평균검색 5.수정 6.삭제 (0.끝))"))
        if num==0:
            break
        elif num==1:
            score_list.input_info()
        elif num==2:
            score_list.print_all()
        elif num==3:
            score_list.search_name()
        elif num==4:
            score_list.search_avg()
        elif num==5:
            score_list.insert()
        elif num==6:
            score_list.delete()
 
 
main()




# ===========================================================================================================================================

class point : # 2D point (2차원 포인트) x 와 y 축을 나타
    x = 0
    y = 0

    def __init__(self,x=0 , y=0):
        self.x = x
        self.y = y

    def __add__(self, p) : #p : point class 객채
        x1 = self.x + p.x
        y1 = self.y + p.y
        return (point(x1,y1))
    
    def Scalar(self, m) : #m : 실수
        x1 = self.x * m
        y1 = self.y * m
        return(point(x1,y1))
    
    def __mul__(self, p) :
        x1 = self.x * p.x
        y1 = self.y * p.y
        return(point(x1,y1))

p1 = point(10,10)
p2 = point(20,20)
p3 = p1+p2
p4 = p1*p2
p5 = p1.Scalar(50)
print(f"(10,10) + (20,20) = ({p3.x},{p3.y})")
print(f"(10,10) * (20,20) = ({p4.x},{p4.y})")
print(f"(10,10) * 50        = ({p5.x},{p5.y})")
print(f"(10,10) + (20,20) = ({p3.x},{p3.y})")





==================================================================================================================================
# Q2 수학 함수를 이용하여 그리기 -> sin/ 원 / 원 안의 sin

import math as m

str = "●"

# sin 그래프
# sin = m.sin(m.pi*(degree/180))

sin_lst = [0] * 46                  # sin 수치 값이 담길 리스트
sin_cnt = [0] * 19                  # sin 수치 값의 빈도수가 담길 리스트

for i in range(1, 46):              

    s = int ( m.sin(m.pi * ( i * 8 / 180 )) * 10 )
                                    # 간소화를 위해 0도부터 360도까지, 361개를
                                    # (0 * 8)도부터 (45 * 8)도까지, 46개로 표시하고
                                    # 소수점 1자리 까지를 정수로 표현
    sin_lst[i] = s + 9              # -9 ~ 9 이지만 표현하기 쉽게 하기위해
    sin_cnt[s + 9] += 1             # +9 를 해서 전부 양수화



for i in range(19):                 # cnt의 수만큼 반복

    i = 18 - i                      # 제일 위쪽부터 출력해야하기에 i = 18-i
    n = sin_cnt[i]                  # n에는 i의 빈도수

    a = 1                           
    lst = sin_lst[a: ]              

    while n != 0:                   # 반복이 진행될때마다 n은 1씩 줄어든다.

        ind = lst.index(i)          # ind에는 lst에서의 i의 인덱스번호

        print(f"{'  ' * ind}{str}", end = "")
                                    # 인덱스 번호만큼의 공백을 넣어주고 문자 출력
                                    # 같은 i끼리는 한줄에 쓰여야 하기 때문에 end = ""
        n -= 1
        a = ind + 1                 # ind는 이미 쓰였기때문에 a = ind+1
        lst = lst[a: ]              # 그리고 lst는 lst의 a부터 시작한다.

    print("")                       # 다른 i끼리는 다른 줄에 쓰기 위해 줄바꿈


# 원 그리기
# 원 위의 점 (x,y)
# 원 중앙의 점 (a,b)
# x = a + r * cos(dgr)
# y = b + r * sin(dgr)
# sin 그래프의 길이가 45
# == r = 22.5
# a == b == r

r = 22.5

x_t_lst = []                        # 위 반원
x_b_lst = []

y_t_lst = []                        # 아래 반원
y_b_lst = []

for i in range(46):

    s = m.sin(m.pi * ( i * 8 / 180 ))
    c = m.cos(m.pi * ( i * 8 / 180 ))
                                    # 간편하게 표현 하기 위해 올림
    if i < 23:                      # 위 반원
        x_t_lst.append(int(22.5 + r * c))
        y_t_lst.append(m.ceil(22.5 + r * s))
    else:                           # 아래 반원
        x_b_lst.append(int(22.5 + r * c))
        y_b_lst.append(m.ceil(22.5 + r * s))

check_t = list(set(y_t_lst))        # 중복 없는 체크 리스트
check_b = list(set(y_b_lst))

check_t.sort()                      # 가장 위부터 출력하기 위해 정렬
check_b.sort()

for i in range(len(check_t)):       # 위 체크리스트 갯수만큼

    i = len(check_t) - i - 1        # 리스트의 맨 뒤 요소부터
    n = y_t_lst.count(check_t[i])   # 요소의 빈도수 체크

    a = 0                           
    lst = y_t_lst[a: ]

    while n != 0:

        ind = lst.index(check_t[i]) # 요소의 인덱스
        if a == 0: print(f"{'  ' * x_t_lst[ind]}{str}", end = "")
                                    # 처음에는 해당 인덱스의 x요소만큼 공백추가
        else: print(f"{str}", end="")
                                    # 빈도수 만큼 출력
        n -= 1                      # n이 1씩 줄어들고 0이 되면 break
        a = ind + 1                 # 같은 부분을 다시 출력하지 않기 위해
        lst = lst[a: ]              

    print("")


for i in range(len(check_b)):       # 나머지 반원

    i = len(check_b) - i - 1
    n = y_b_lst.count(check_b[i])

    a = 0                           
    lst = y_b_lst[a: ]              

    while n != 0:

        ind = lst.index(check_b[i])
        if a == 0: print(f"{'  ' * x_b_lst[ind]}{str}", end = "")
        else: print(f"{str}", end="")

        n -= 1
        a = ind + 1
        lst = lst[a: ]

    print("")


# 원 안의 sin 그래프 (태극)
# 문자열로 구현하는 것은 포기

import matplotlib.pyplot as p
import numpy as n

a = n.arange(0, 360)                # 0부터 360까지
y = n.sin(n.radians(a)) * 60        # sin그래프는 -1부터 1까지 이므로 *60을 해서 y범위를 늘려줌

cx = [0] * 361
sy = [0] * 361

for i in range(1,361):              # 원 그리기
    cx[i] = 180 + 180 * m.cos(m.pi * i / 180)
    sy[i] = 0 + 180 * m.sin(m.pi * i / 180)

p.plot(cx, sy)
p.plot(y)

p.show()

==============================================================================================================================
# Q3 임의로 주어진 문자열에 회문이 있는 경우 최대 회문의 길이 출력

def is_p(lst):                  # 함수 선언

    return lst == lst[ : : -1]  # 리스트와 거꾸로 리스트가 같은지 T/F 반환

str = input()                   # 입력된 단어 저장 
lst = []                        # 회문일 경우 단어의 길이가 들어갈 리스트

for i in range(len(str)):       # 단어의 길이만큼 반복

    for j in range(i+2, len(str)+1):
                                # i + 1 부터 단어의 길이 + 1 만큼 반복
        if is_p(str[i:j]): lst.append(len(str[i:j]))
                                # i부터 j까지의 문자열이 회문일 경우
                                # 길이를 리스트에 저장

try: print(max(lst))            # 최고 길이 출력
except: print("회문이 없습니다.")  # 회문이 없어서 오류가 날 경우 회문이 없다고 출력
==============================================================================================================================
# Q4 두가지 수를 입력 받아 최대공약수 출력

a, b = map(int, input("a b\n").split())     # a, b에 두 수를 정수로 저장

lst_a = []                                  # a의 약수
lst_b = []                                  # b의 약수

lst_comb = []                               # a와 b의 공약수

for i in range(1, a+1):                     # a의 약수 뽑기

    if i == 1 | i == a: lst_a.append(i)
    elif a%i == 0: lst_a.append(i)

for i in range(1, b+1):                     # b의 약수 뽑기

    if i == 1 | i == b: lst_b.append(i)
    elif b%i == 0: lst_b.append(i)

for i in lst_a:                             # 공약수 뽑기

    if i in lst_b:

        lst_comb.append(i)

print(f"{a}과(와) {b}의 최대공약수는 {max(lst_comb)} 입니다.")
                                            # 최대공약수 출력

==============================================================================================================================
# Q5 입력받은 알파벳보다 하위 알파벳들 모두 출력

a = input().lower()

start = ord("a")                    # 알파벳 시작인 a의 아스키코드번호
end = ord(a)                        # 입력받은 알파벳의 아스키코드번호

uni = []                            # 필요한 아스키번호를 받을 리스트

for i in range(start, end+1):

    uni.append(i)                   # a 부터 입력까지 리스트에 저장

for i in range(len(uni)):

    i = len(uni) - i                # i는 len(uni) 부터 1까지

    for j in range(i):              # j는 1부터 i-1까지

        print(chr(uni[j]), end = "")# 줄바꿈이나 공백없이 uni[j]를 문자로 변환

    print("")                       # 줄바꿈

==============================================================================================================================
# Q6 홀수를 입력받아 * 피라미드 완성 ex) 5 -> 1층 * 2충 *** 3층 *****

n = int(input())                    # 입력 받은 홀수
b = int(n/2) + 1                    # 가운데 위치
cnt = 0                             # 줄 카운트

for i in range(1, n+1):             # 1부터 n까지 반복
    if i%2 == 1:                    # i가 홀수 일 때
        cnt += 1                    # 줄 카운트 +1
        print(" "*(b-cnt), "*"*i, sep="")
                                    # 공백을 넣어서 가운데까지,
                                    # *을 i만큼 출력

==============================================================================================================================
a = input().upper()

start = ord("A")                    # 알파벳 시작인 a의 아스키코드번호
end = ord(a)                        # 입력받은 알파벳의 아스키코드번호

uni = []                            # 필요한 아스키번호를 받을 리스트

for i in range(start, end+1):

    uni.append(i)                   # a 부터 입력까지 리스트에 저장

for i in range(len(uni)):           # uni의 갯수만큼 반복

    j = len(uni) - i                # 갯수에서 i를 빼서 j에 저장

    print(' ' * (len(uni)-j), chr(uni[i]) * j, sep = "")
                                    # 문자가 j 만큼 출력이 되기에
                                    # 전체 길이에서 j 만큼 빼서 공백 추가 후 출력

==============================================================================================================================
# Q8 임의의 파일을 이용해서 이름, 과목, 점수를 입력 받고 합계와 평균을 계산해서 석차를 구한 후 저장
# 1번의 파일 활용

f = open("./result/score.csv", "r")
                                # 파일을 열고

header = []                     # 파일이 가지고 있는 헤더가 들어갈 리스트

name = []                       # 이름 리스트
k = []                          # 국어 점수 리스트
m = []                          # 수학 점수 리스트
e = []                          # 영어 점수 리스트
c = []                          # 컴퓨터 점수 리스트

m_num = []                      # 평균과 학생의 INDEX가 들어갈 리스트

total = []                      # 점수 합계 리스트

cnt = 0                         # 인덱스 대용

for i in f:

    if cnt == 0:

        header = i.split("\n")[0].split(",")
        cnt += 1                # cnt가 0이라면 헤더에 헤더들을 넣고 cnt + 1

    else:

        temp = i.split("\n")[0].split(",")
                                # 임시 변수에 불러온 값 리스트를 넣고
        name.append(temp[0])    # 이름
        k.append(int(temp[1]))  # 국어점수
        m.append(int(temp[2]))  # 수학점수
        e.append(int(temp[3]))  # 영어점수
        c.append(int(temp[4]))  # 컴퓨터점수 입력

        total.append(k[cnt-1]+m[cnt-1]+e[cnt-1]+c[cnt-1])
                                # 각 점수 리스트에 들어간 값들을 더해 합계 입력
        m_num.append([total[cnt-1]/4, cnt-1])
                                # 합계리스트에 들어간 값으로 평균 계산
                                # 해당 학생의 INDEX를 입력
        cnt += 1

f.close()                       # 데이터 파일 닫기

header.append("합계")            # 헤더 리스트에 추가로 입력할 헤더들 추가
header.append("평균")
header.append("석차")

m_num.sort(reverse = True)      # 석차 계산을 위해 내림차순으로 평균 sort

f = open("./result/score_total_mean.csv", "w")
                                # 데이터들을 반환할 파일을 쓰기모드로 열고
for i in header:
                                # 첫 줄에 헤더들을 , 로 구분하여 입력
    f.write(f"{i},")


cnt = []

for i in range(len(name)):      # 데이터 수 만큼 반복

    f.write("\n")               # 줄바꿈 해주고

    mean = 0                    # 사용할 평균과 석차 변수를 미리 선언
    n = 0

    for j in m_num:             # 1등부터 꼴등까지 순서대로 정렬된 m_num에서
                                # 하나씩 꺼내와서
        if i == j[1]:           # i와 INDEX가 같을 때
            mean = j[0]         # 평균은 해당 j의 평균 값이고
            n = m_num.index(j)  # 석차는 해당 j의 인덱스 값 + 1
                                # 학생을 INDEX로 구분하기에 동명이인이 있어도 중복 안됨.

    f.write(f"{name[i]},{k[i]},{m[i]},{e[i]},{c[i]},{total[i]},{mean},{n + 1}")
                                # 데이터를 원하는 순서대로 ,로 구분하여 입력
f.close()                       # 모두 입력이 되었으면 파일 닫기

print("완료되었습니다.")

==============================================================================================================================
# Q9 음식 이름과 가격이 표시된 메뉴판에서 정해진 금액으로 가능한 모든 2가지 주문 조합을 나열

# 떡 이름 데이터와 random 함수로 가격을 뽑아 사용
# 가격 범위는 1000 ~ 5000 사이, step은 500
# 정해진 금액은 입력 받아 사용

import random as r                  # 가격설정을 위해 random import

f = open("./source/메뉴.txt")        # 메뉴 이름 불러오기

for i in f: food = i.split("\n")[0].split(",")
                                     # food로 저장
price = []                           # 가격 리스트 생성

for i in range(len(food)): price.append(r.randrange(1000, 5000, 500))
                                     # 1000에서 5000 까지 500단위로 랜덤 생성
money = int(input("얼마 있으세요?\n")) # 손님이 가지고 계신 돈 입력 받기

for i in range(len(food)):           # food의 길이 만큼 반복

    a = price[i]                     # a는 food[i] 가격이고

    for j in range(len(food)):       # 또 food 길이만큼 반복하지만

        if i != j:                   # i랑 j가 같지 않을때

            if a + price[j] < money: # 그리고 a에 food[j]의 가격을 더해도 가진 돈을 넘지 않을 때 

                a = a + price[j]     # a에 food[j]의 가격을 더하고

                print(f"{food[i]} + {food[j]} = {a}")
                                     # 조합과 가격 출력

==============================================================================================================================
# Q9 음식 이름과 가격이 표시된 메뉴판에서 정해진 금액으로 가능한 모든 주문 조합을 나열

# 떡 이름 데이터와 random 함수로 가격을 뽑아 사용
# 가격 범위는 1000 ~ 5000 사이, step은 500
# 정해진 금액은 입력 받아 사용

import random as r                  # 가격설정을 위해 random import

f = open("./source/메뉴1.txt")         # 메뉴 이름 불러오기

for i in f: food = i.split("\n")[0].split(",")
                                     # food로 저장
price = []                           # 가격 리스트 생성

for i in range(len(food)): price.append(r.randrange(1000, 5000, 500))
                                     # 1000에서 5000 까지 500단위로 랜덤 생성
money = int(input("얼마 있으세요?\n")) # 손님이 가지고 계신 돈 입력 받기

for i in range(len(food)):          # 메뉴의 갯수만큼 반복

    for j in range(i+1, len(food)): # i의 다음부터 메뉴의 갯수만큼 반복

        if sum(price[i:j+1]) < money:
                                    # i 부터 j+1, 즉, j까지 가격을 더해서 가진 돈과 비교
            for k in range(len(price[i:j])):
                                    # 조건에 맞을 i부터 j-1까지를 하나씩 출력
                print(f"{food[i:j][k]} + ", end = "")

            print(f"{food[j]} = {sum(price[i:j+1])}") 
                                    # 마지막 요소와 총 가격까지 출력

==============================================================================================================================
# Q10 입력받은 선택에 따라 다른 기능을 수행하는 프로그램 작성 ( 기능은 3가지 이상 )


def is_p(lst):

    return lst == lst[ : : -1]



while 1:
    select = input("모드를 선택하세요.:\n\n1) 회문\n2) 최대공약수\n3) 피라미드\n4) 구구단표\n그외의 입력) 종료\n\n> ")

    print("\n")

    if select == "1":

        str = input("단어를 입력해주세요.\n단어에 포함된 가장 긴 회문을 알려드릴게요.\n> ")    
        lst = []
        p_lst = []

        for i in range(len(str)):

            for j in range(i+2, len(str)+1):

                if is_p(str[i:j]):

                    lst.append(len(str[i:j]))                                                                  
                    p_lst.append(str[i:j])

        print("\n")

        try: print(f'가장 긴 회문은 " {max(lst)} " 자의 " {p_lst[lst.index(max(lst))]} " 입니다!')
        except: print("회문이 없습니다.")

        print("\n")

    elif select == "2":

        a, b = map(int, input("두 수 a와 b를 입력하세요.\n> ").split())     

        lst_a = []                                  
        lst_b = []                                  

        lst_comb = []                               

        for i in range(1, a+1):                     

            if i == 1 | i == a: lst_a.append(i)
            elif a%i == 0: lst_a.append(i)

        for i in range(1, b+1):                     

            if i == 1 | i == b: lst_b.append(i)
            elif b%i == 0: lst_b.append(i)

        for i in lst_a:                             

            if i in lst_b:

                lst_comb.append(i)

        print(f"{a}과(와) {b}의 최대공약수는 {max(lst_comb)} 입니다.")

        print("\n")

    elif select == "3":

        n = int(input("홀수를 입력하세요.\n> "))
        symbol = input("어떤 걸로 쌓을까요? 1 글자 이상 입력시 피라미드가 삐뚤어집니다.\n> ")

        b = int(n/2) + 1

        cnt = 0                             

        for i in range(1, n+1):             
            if i%2 == 1:                    
                cnt += 1                    
                print(" "*(b-cnt), f"{symbol*i}", sep="")

        print("\n")

    elif select == "4":

        n = int(input("몇 단을 출력할까요? 0 을 입력하면 모두 출력됩니다.\n> "))

        if n == 0:

            for i in range(2, 10):

                for j in range(1, 10):

                    print(f"{i} * {j} = {i*j}")

                print("")
        else:

            for i in range(1, 10):

                print(f"{n} * {i} = {n*i}")

        print("\n")


    else:
        break

==============================================================================================================================
# Q11 임의의 텍스트 파일에 대해 파일명, 찾을 단어, 바꿀 단어를 입력받아 해당 파일에서 단어를 변환하여 다른 파일로 출력

path = input("경로를 입력해주세요.\n> ")     # 경로
name = input("파일명을 입력해주세요.\n> ")    # 파일명

file = path + "\\" + name               # 전체 경로

f = open(file)                          # 해당 파일 열기

txt = []                                # 파일 내용이 저장될 리스트

for i in f: txt.append(i.split("\n")[0])

f.close()                               # 파일 닫기

print("")

old = input("find : ")                  # 찾을 단어
new = input("replace : ")               # 바꿀 단어

name = name.split(".")                  # 이름과 확장자 분리
file = path + "\\" + name[0] + "_replace." + name[1]
                                        # 저장될 파일의 전체 경로
cnt = 0                                 # 변경 횟수 카운트

f = open(file, "w")                     # 저장될 파일 열기

for i in txt:                           # txt에서 하나씩 빼와서

    if old in i:                        # 찾을 단어가 i 안에 있다면

        i = i.replace(old, new)         # i에서 찾아 바꾸어서
        cnt += 1                        # 변경 횟수 + 1

    f.write(f"{i}\n")                   # 파일에 쓰기

f.close()                               # 파일 닫고


print(f"\n저장 경로 > {file}\n\n{cnt}번 변경되었고,\n성공적으로 저장 되었습니다.")
                                        # 저장된 전체경로, 변경횟수 출력

