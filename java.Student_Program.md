# 📘 학생 관리 프로젝트 (Java)

## 📑 목차
- [프로젝트 개요](#-프로젝트-개요)  
- [STEP 1: Student 클래스 구현](#-step-1-student-클래스-구현)  
- [STEP 2: StudentRepository 클래스 구현](#-step-2-studentrepository-클래스-구현)  
- [STEP 3: 테스트 코드 작성 & 실행 결과](#-step-3-테스트-코드-작성--실행-결과)  
- [작성자/환경](#-작성자환경)  

---

## 📑 프로젝트 개요
- **목표**: 학생(Student) 객체를 생성하고, 이를 저장/조회/검증할 수 있는 저장소(StudentRepository)를 구현한다.  
- **구성**  
  - `Student.java` → 학생 클래스  
  - `StudentRepository.java` → 학생 저장소  
  - `StudentRepositoryTest.java` → 테스트 실행 파일  

---

## 🔹 STEP 1: Student 클래스 구현
```java
public class Student {
    private String name;
    private int age;
    private String StudentId;

    public Student() {
        this("이름없음", 0, "알수없음");
    }

    public Student(String name, int age, String StudentId) {
        if(name == null) name = " ";
        if(age < 0) age = 0;
        if(StudentId == null) StudentId = " ";

        this.name = name;
        this.age = age;
        this.StudentId = StudentId;
    }

    public String getName() { return name; }
    public void setName(String name) { this.name = (name == null) ? "" : name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = Math.max(0, age); }
    public String getStudentId() { return StudentId; }
    public void setStudentId(String StudentId) { this.StudentId = (StudentId == null) ? "" : StudentId; }

    @Override
    public String toString() {
        return "Student {name='" + name + "', age=" + age + ", StudentId='" + StudentId + "'}";
    }
}
```

---

## 🔹 STEP 2: StudentRepository 클래스 구현
```java
import java.util.ArrayList;
import java.util.List;

public class StudentRepository {
    private final List<Student> students = new ArrayList<>();

    public boolean add(Student s) {
        if(s == null) return false;
        for(Student st : students) {
            if(st.getStudentId().equals(s.getStudentId())) {
                return false;
            }
        }
        students.add(s);
        return true;
    }

    public List<Student> findAll() {
        return new ArrayList<>(students);
    }

    public Student findById(String studentId) {
        if(studentId == null) return null;
        for(Student st : students) {
            if(st.getStudentId().equals(studentId)) {
                return st;
            }
        }
        return null;
    }
}
```

---

## 🔹 STEP 3: 테스트 코드 작성 & 실행 결과
```java
public class StudentRepositoryTest {
    public static void main(String[] args) {
        StudentRepository repo = new StudentRepository();

        Student s1 = new Student("지안", 20, "2025001");
        Student s2 = new Student("태은", 21, "2025002");
        Student s3 = new Student("중복아이디", 22, "2025001");

        System.out.println("s1 추가: " + repo.add(s1));
        System.out.println("s2 추가: " + repo.add(s2));
        System.out.println("s3 추가(중복): " + repo.add(s3));

        System.out.println("저장된 전체 학생: ");
        for (Student st : repo.findAll()) {
            System.out.println(st);
        }

        System.out.println("학번 2025001 검색: " + repo.findById("2025001"));
        System.out.println("없는 학번 검색: " + repo.findById("9999999"));
    }
}
```

---

## 🖥️ 실행 결과
```java
s1 추가: true
s2 추가: true
s3 추가(중복): false
저장된 전체 학생: 
Student {name='지안', age=20, StudentId='2025001'}
Student {name='태은', age=21, StudentId='2025002'}
학번 2025001 검색: Student {name='지안', age=20, StudentId='2025001'}
없는 학번 검색: null
```

---

##### ✍️작성자: 박지안
##### 🐧실습 환경: IntelliJ IDEA 2025.2
##### 🗓️ 작업일: 2025-08-31
