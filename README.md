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
 
