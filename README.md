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
