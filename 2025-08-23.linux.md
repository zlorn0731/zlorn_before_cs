# 🐧 리눅스 프로세스(Process) 학습  

## 📌 목차  
1. [프로세스란?](#-프로세스란)  
2. [프로세스 관리 명령어](#-프로세스-관리-명령어)  
3. [프로세스 제어 (jobs, fg, bg)](#-프로세스-제어-jobs-fg-bg)  
4. [오늘의 실습](#-오늘의-실습)  
5. [오늘 배운 핵심](#-오늘-배운-핵심)  

---

## 🐾 프로세스란?  
- 실행 중인 프로그램을 **프로세스**라 부름  
- 각각의 프로세스는 고유한 **PID(Process ID)**를 가짐  
- 리눅스에서는 **부모-자식 프로세스 구조**로 동작  
- 터미널도 프로세스, 그 안에서 실행하는 `ls`, `cat` 같은 명령도 자식 프로세스  

---

## 🛠️ 프로세스 관리 명령어  

### 🔍 프로세스 확인  
```bash
ps -ef | head -5

- 예시 출력: 
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 Aug22 ?        00:00:01 /sbin/init
root         2     0  0 Aug22 ?        00:00:00 [kthreadd]
root         3     2  0 Aug22 ?        00:00:00 [rcu_gp]
root         4     2  0 Aug22 ?        00:00:00 [rcu_par_gp]
```

### 📊 실시간 모니터링
```bash
top

- 예시 출력 (일부):
top - 20:12:33 up 1 day,  3:45,  2 users,  load average: 0.10, 0.08, 0.09
Tasks: 210 total,   1 running, 209 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.0 us,  1.0 sy,  0.0 ni, 96.5 id,  0.3 wa,  0.0 hi,  0.2 si,  0.0 st
```

### 🔎 특정 프로세스 찾기
```bash
ps aux | grep bash

- 예시 출력:
user     1234  0.0  0.1  12345  5678 pts/0    Ss   20:10   0:00 -bash
user     2345  0.0  0.0   6789   456 pts/0    S+   20:11   0:00 grep bash
```

### 🛑 프로세스 종료
```bash
kill -9 1234
👉 1234는 위에서 확인한 PID
```

### 🎮 프로세스 제어 (jobs, fg, bg)

#### Foreground & Background
```bash
sleep 100 &

- 예시 출력:
[1] 3456
👉 [1]은 작업 번호, 3456은 PID
```

#### jobs
```bash
jobs

- 예시 출력:
[1]+  Running    sleep 100 &
```

#### fg (foreground)
```bash
fg %1
👉 sleep 100이 앞으로 나와서 터미널 입력을 막음.
- Ctrl + Z 누르면 중지됨
[1]+  Stopped    sleep 100
```

#### bg (background)
```bash
bg %1

- 예시 출력:
[1]+ sleep 100 &
```

### 종료
```bash
kill %1
👉 %1은 jobs에서 확인한 작업 번호
```

## 📝 오늘의 실습
### 1. 프로세스 목록 확인
ps -ef | head -5

### 2. top 실행 (q로 종료)
top

### 3. 특정 프로세스 검색
ps aux | grep bash

### 4. 백그라운드 실행
sleep 1000 &

### 5. jobs로 확인
jobs

### 6. fg로 앞으로 가져오기
fg %1

### (Ctrl + Z 로 중지 후)
bg %1   # 다시 백그라운드 실행

### 7. 프로세스 종료
kill %1

## 🌟 오늘 배운 핵심
- 프로세스 = 실행 중인 프로그램, PID로 구분
- ps, top, grep, kill → 프로세스 관리 기본기
- &, Ctrl+Z, jobs, fg, bg → 터미널 안에서 프로세스 제어
- 오늘로써 프로세스 기초 + 제어 완료!
 → 내일은 signal(시그널: SIGTERM, SIGKILL 등) 정리하면 완성됨

##### ✍️작성자: 박지안
##### 🐧실습 환경: Replit
##### 🗓️ 작업일: 2025-08-23
