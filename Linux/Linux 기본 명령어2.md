# Linux 기본 명령어 - 2


### 목차
1. [sort](#sort)
2. [grep](#grep)
3. [find](#find)
4. [which](#which)
5. [whereis](#whereis)
6. [와일드카드](#와일드카드)


### sort
- 파일의 내용을 정렬하며 라인 단위로 동작 (기본적으로 문자열로 인식하여 오름차순 정렬)
- 구문 형태 **`sort [옵션]... [파일]...`**
- 옵션
    - `-r` : 내림차순으로 정렬
    - `-n` : 숫자로 정렬
    - `-k` : 지정한 필드(열)로 정렬
    - `-t` : 필드 구분자를 지정
    - `-u` : 중복된 라인을 제거

```powershell
ubuntu@ip:~$ sort number.txt
1
3
5
6
7
8
ubuntu@ip~$ sort -n number.txt
1
3
5
6
7
8
ubuntu@ip:~$ sort -r number.txt
8
7
6
5
3
1
```

- `sort -k 2 -n number.txt`
    - **-k**  특정 필드로 정렬할 거다
    - **2** 특정 필드 위치 (정렬 기준이 2번째 필드)
    - **-n** number임 (없으면 자동으로 아스키코드)

```powershell
ubuntu@ip:~$ sort -k 2 -n number.txt
Kim 25
Park 27
Choi 29
Lee 30
ubuntu@ip:~$ sort -k 2 -n -r number.txt
Lee 30
Choi 29
Park 27
Kim 25
ubuntu@ip:~$ sort -k 1 number.txt
Choi 29
Kim 25
Lee 30
Park 27
ubuntu@ip:~$ sort -k 1 -r number.txt
Park 27
Lee 30
Kim 25
Choi 29
```

### grep  ⭐
- Global Regular Expression Print
- 텍스트의 패턴을 검색하는데 사용됨
    - 파일에서 **특정 문자열을 찾거나** **표준 입력에서 문자열을 찾는데** 사용됨
- 구문 형태  **`grep [options] pattern [file...]`**
    - options : 명령을 수행하는 방법을 변경하는데 사용됨
    - pattern : 파일에서 찾으려는 문자열
    - file… : 검색할 파일 또는 디렉토리
- 옵션
    - `-i`: 대소문자를 무시하고 검색
    - `-r` 또는 `-R`: 디렉토리 및 하위 디렉토리를 재귀적으로 검색
    - `-v`: 패턴과 일치하지 않는 줄을 출력
    - `-l`: 패턴과 일치하는 줄이 있는 파일 이름만 출력
    - `-n`: 패턴과 일치하는 줄과 함께 해당 줄 번호를 출력

```powershell
vim test.txt
ubuntu@ip:~$ grep "test" test.txt
Hello, this is a test file. It contains several words, including the word test.
ubuntu@ip:~$ grep "word" test.txt
Hello, this is a test file. It contains several words, including the word test.
ubuntu@ip:~$ grep "words" test.txt
Hello, this is a test file. It contains several words, including the word test.
ubuntu@ip:~$ grep "wordsss" test.txt
ubuntu@ip:~$ grep -v "wordsss" test.txt
Hello, this is a test file. It contains several words, including the word test.
ubuntu@ip:~$ grep -v "word" test.txt
ubuntu@ip:~$ grep -v "word1" test.txt
Hello, this is a test file. It contains several words, including the word test.
```

### find
- 파일시스템에서 파일을 찾을 때 사용하는 명령어
- 기본 문법 : `find [경로..] [표현식]`
    - **경로** : 검색을 시작할 디렉토리 지정 (여러 경로 지정 가능)
    - **표현식**은 검색 조건과 검색 결과에 적용할 작업을 지정
        - `-name [파일명]`: 지정된 이름의 파일을 찾음
        - `-iname [파일명]`: 지정된 이름(대소문자를 구분X)의 파일을 찾음
        - `-type [d/f]`: `d`는 디렉토리, `f`는 일반 파일을 찾음
        - `-mtime [일수]`: 지정된 일수만큼 이전에 수정된 파일을 찾음
        - `-exec [명령...] {} \\;`: 검색 결과에 대해 지정된 명령을 실행.  `{}`는 검색 결과를 의미
    - 예시 : `sudo find /var/log -type f -mtime -7`
        
        찾기    루트/var/log 폴더에서   일반 파일을     7일 이내에 수정된 파일
        

```powershell
ubuntu@ip:~$ find . -name example.txt
ubuntu@ip:~$ find . -name test.txt
./test.txt
ubuntu@ip:~$ cp test.txt Test.txt
ubuntu@ip:~$ ls
Test.txt  test.txt
ubuntu@ip:~$ find . -name test.txt
./test.txt
ubuntu@ip:~$ find . -iname test.txt
./test.txt
./Test.txt
ubuntu@ip:~$ sudo find /var/log -type f -mtime -7
/var/log/lastlog
/var/log/journal/ec21e00b65274492b12548b604f67ff1/user-1000.journal
/var/log/journal/ec21e00b65274492b12548b604f67ff1/system.journal
/var/log/dmesg.0
/var/log/landscape/sysinfo.log
/var/log/amazon/ssm/errors.log
/var/log/amazon/ssm/amazon-ssm-agent.log
/var/log/amazon/ssm/audits/amazon-ssm-agent-audit-2024-07-10
/var/log/amazon/ssm/audits/amazon-ssm-agent-audit-2024-07-11
/var/log/syslog
/var/log/dpkg.log
/var/log/kern.log
/var/log/cloud-init-output.log

```

### which
- 특정한 실행 가능 파일의 경로 찾기 **(시스템에 설치된 SW의 위치를 찾을 때 유용함)**
- 사용자의 환경 변수 PATH에 지정된 디렉토리를 검색하여 실행 가능 파일을 찾음
    - 설치되어 있지 않을 경우, 어떠한 출력도 보여주지 않음
- 사용법 : `which [명령어]`   예시: which java

```powershell
ubuntu@ip:~$ which python3
/usr/bin/python3
ubuntu@ip:~$ which gcc
ubuntu@ip:~$ which java
/usr/bin/java
```

### whereis
- 특정 바이너리(executable), 소스, 매뉴얼 페이지 파일의 위치를 찾기
- 사용법 : `whereis [옵션] [파일명]`
    - 옵션
        - `-b` : 바이너리 파일만 찾기
        - `-m` : 매뉴얼 페이지만 찾기
        - `-s` : 소스 파일만 찾기
        - `-u` : 언급한 위치에서 파일을 찾지 못했을 경우 사용

```powershell
ubuntu@ip:~$ whereis ls
ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz
ubuntu@ip:~$ whereis python
python:
ubuntu@ip:~$ whereis java
java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1
```

### 와일드카드
- 리눅스에서 와일드카드는 파일들을 일치시키는데 사용되는 심볼 또는 문자를 의미함
- 가장 많이 사용되는 와일드 카드
    - **`*`**: 모든 문자를 대체할 수 있는 와일드카드. 예:  `*.txt`는 모든 txt 파일 대상으로 함
    - **`?`**: 한 문자를 대체하는 와일드카드. 예: `?.txt`는 한 문자로 된 모든 txt 파일 대상으로 함
    - **`[]`**: 대괄호 안의 어떤 문자든 일치하는 와일드카드. 예: `[abc].txt`는 a.txt, b.txt, c.txt와 일치함
- find 명령어와 함께 많이 사용됨

```powershell
ubuntu@ip:~$ ls
Test.txt  a.pdf   b      c      d  est-backend-5  hello_world.sh  test.txt   testcopy.txt
a         ab.pdf  b.pdf  c.pdf  e  f              study0712.txt   test2.txt
ubuntu@ip:~$ ls *.pdf
a.pdf  ab.pdf  b.pdf  c.pdf
ubuntu@ip:~$ ls ?.pdf
a.pdf  b.pdf  c.pdf
ubuntu@ip:~$ ls ??.pdf
ab.pdf
ubuntu@ip:~$ ls [ab].pdf
a.pdf  b.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "*.pdf"
/home/ubuntu/ab.pdf
/home/ubuntu/b.pdf
/home/ubuntu/a.pdf
/home/ubuntu/c.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "[b].pdf"
/home/ubuntu/b.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "[ab].pdf"
/home/ubuntu/b.pdf
/home/ubuntu/a.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "*[ab].pdf"
/home/ubuntu/ab.pdf
/home/ubuntu/b.pdf
/home/ubuntu/a.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "*b.pdf"
/home/ubuntu/ab.pdf
/home/ubuntu/b.pdf
ubuntu@ip:~$ find /home/ubuntu/ -name "*b*.*"
/home/ubuntu/123b2123.good
/home/ubuntu/ab.pdf
/home/ubuntu/b.pdf
```

한글자인 파일 찾기

`ls ?`  또는 `find . -name "?"`

```powershell
ubuntu@ip:~$ touch a b c d e f
ubuntu@ip:~$ ls
Test.txt  a  b  c  d  e  f  test.txt
ubuntu@ip:~$ ls ?
a  b  c  d  e  f
ubuntu@ip:~$ find . -name "?"
.
./a
./b
./e
./c
./d
./f
```
