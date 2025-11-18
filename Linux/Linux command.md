### ls

⇒ list의 약자로 Windows 명령 프롬포트에서 dir 명령과 같은 역할이다. 해당 디렉토리에 있는 파일을 나열한다.

### cd

⇒ Change Directory의 약자로 디렉터리를 이동하는 명령어이다.

```bash
cd ~ # 내 홈 디렉토리로 이동
cd ~rocky rocky # 다른 사용자의 파일로 이동
cd / # 제일 상위 루트로 이동
```

다른 사용자의 파일에 접근할 때 퍼미션 조건이 맞아야 함

### ., ..

⇒ ‘.’는 현재 디렉토리, ‘..’는 현재 디렉토리의 상위 디렉토리

### pwd

⇒ Print Working Directory의 약자로 현재 디렉토리의 전체 경로를 화면에 표시한다

### rm

⇒ ReMove의 약자로 파일이나 디렉터리를 삭제한다. 당연히 권한이 있어야 삭제할 수 있다. 단 root 사용자는 모든 권한이 있으므로 rm 명령 사용에 제약이 없다.

```bash
rm -i abc.txt # 삭제 시 정말 삭제할 지 경고
rm -r abc # 해당 디렉터리 삭제
rm -rf abc # abc 디렉터리와 하위 디렉터리 모두 삭제
```

### cp

⇒ Copy의 약자로 디렉터리를 복사한다. 새로 복사한 파일은 복사한 사용자의 소유가 된다. 그러므로 명령 실행자는 파일의  읽기 권한이 필요하다.

### touch

⇒ 크기가 0인 새 파일을 생성하거나 생성된 파일이 존재한다면 파일의 최종 수정 시간을 변경한다

```bash
touch abc # 파일이 없다면 빈 파일 생성, 있다면 수정 시각이 현재
```

### mv

⇒ Move의 약자로 파일이나 디렉터리의 이름을 변경하거나 다른 디렉터리로 옮길 때 사용한다

```bash
mv abc /ex/sys # abc를 ex/sys/ 디렉터리로 이동
mv abc cba # abc를 cba로 바꾼다
```

### mkdir

⇒ Make directory의 약자로 새로운 디렉터리를 생성한다. 생성된 디렉토리는 명령을 실행한 사용자의 소유가 된다

### rmdir

⇒  Remove directory의 약자로 파일을 지우는데, 안에 파일 있으면 있으면 못 지운다

```bash
rmdir abc 
rmdir -r abc # 안에 있는 하위 파일도 삭제
```

### cat

⇒ Concatenate의 약자로 파일 내용을 화면에 출력합니다

### head, tail

⇒ 텍스트 형식으로 작성된 파일의 앞 10행 또는 마지막 10행만 화면에 출력한다

```bash
	head abc.txt
	tail -5 abc.txt # 마지막 5 행만 출력
```

### more

⇒ 텍스트 형식으로 작성된 파일을 페이지 단위로 화면에 출력한다. space를 누르면 다음 페이지, B는 앞, Q는 명령 종료

```bash
more abc.txt
more +30 abc.txt # 30행부터
```

### less

⇒ more 명령과 용도가 비슷하지만, 기능이 더 확장되었다. more에서 사용하는 키와 더불어 화살표 키나 PageUp, PageDown 도 사용할 수 있다

### file

⇒ 파일의 종류를 표시한다

### clear

⇒ 현재 사용 중인 터미널 화면을 깨끗하게 지운다

### explorer.exe .

⇒ 현재 우분투 파일로 나가진다

### vi  abc.txt

⇒ abc.txt를 열고 수정할 수 있다

```bash
vi abc.txt # 메모 생성
(Esc)
:wq # 저장하고 종료
:q! # 저장 안 하고 종료
:w # 저장 후 계속 편집
```

### rm

⇒ 파일을 지우는 명령어

### su, sudo

⇒ Switch User, SuperUser Do의 약자로 일반 사용자가 root 권한을 사용할 때 사용한다

```bash
su root 
# 현재 계정을 로그아웃 하지 않고 다른 계정으로 전환
# root 사용자의 비밀번호를 요구한다
```

```bash
sudo [command] #root의 권한 만을 빌린다
# sudo는 권한만을 빌려서 쓴다
```

### option

**ls**

- -a : 숨김파일까지 표시
- -l : 자세히 표시
- -h : 사람이 읽기 쉽게
- -R : 하위 폴더까지 재귀적으로
- -t : 최근 수정순 정렬

**All**

- - a : 모두 all
- -l : 상세히 long
- -h : 읽기 쉽게 human-readable
- -i : ignore case
- -v : 자세히 or 반대로 verbose or invert
- -f : 강제 force
- -n : 숫자 관련 limit/number

### echo

⇒ 출력문을 담당한다

```bash
echo hi # 따옴표 없이 출력
echo "Sehyeon_" # 특수 문자 사용 시 큰 따옴표
echo "hello" > abc.txt # abc파일에 문자를 덮어씀
echo "linux" >> abc.txt # 이어쓰기함
```

### grep

⇒ 문자 찾기

```bash
grep 문자 abc.txt
grep -i 문자 abc.txt # 대소문자 무시
```

### chmod

⇒ change mode의 약자로 파일의 권한을 변경할 수 있게 만들어주는 명령어

```bash
chmod [option][mode][file]
chmod +w abc.txt # 수정 권한
chmod +x abc.txt # 실행 권한 추가
```

- 옵션
    - -R : 하위 파일과 디렉토리의 모든 권한 변경
    - -v : 실행되고 있는 모든 파일 나열
    - -c : 권한이 변경된 파일 내용 출력
    
- 모드
    - reference(대상) :
    - u : user의 권한 (사용자의 권한)
    - g : group의 권한 (파일의 group 멤버인 사용자의 권한)
    - o : other의 권한 (user, group의 멤버가 아닌 사용자의 권한)
    - a : all의 권한 (위의 셋을 포함하는 모든 사용자의 권한)
    - operator :
        - ＋ : 해당 권한을 추가한다.
        - － : 해당 권한을 제거한다.
        - = : 해당 권한을 설정한데로 변경한다.
    - modes :
        - r : read 권한 (읽기)
        - w : write 권한 (쓰기)
        - x : excute 권한 (실행)
        - － : 사용권한없음
- 파일
    - 변경 설정을 할 파일이나 디렉토리

### ./

⇒ 파일을 실행할 수 있다

```bash
./abc.txt
./abc.txt & # 백그라운드로 실행한다
```

### $

⇒ 명령어를 실핸한다

```bash
abc=$(2+2) # $() 괄호 안에 오는 명령어를 실행
```

### ps

⇒ 실행중인 프로세스 표시

```powershell
ps -Wal
# W : window프로세스까지 표시
# a : 나뿐만 아니라 모든 사용자 프로세스 표시
# l : 자세한 정보 
```

### apt

⇒ 프로그램을 설치/업데이트/삭제 하는 명령어

```powershell
sudo apt tree # tree 다운로드
```

### export

⇒ 환경변수를 저장하는 명령어

```powershell
export WEBAPP_VAR=ilfpns # WEBAPP_VAR 환경변수에 값 지정
```

### alias

⇒ 명령어를 단축어로 지정하는 명령어

```powershell
 alias mktar='tar -cvf' # tar을 mktar이라는 명령어로 저장할 수 있게 함 
```

### vi ~/.bashrc

⇒ 환경변수/단축 명령어 등을 계속 저장할 수 있다

```powershell
vi ~/.bashrc # bash환경에서 수정
```
