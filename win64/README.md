# HyperFrame Nginx for Win64 설치방법

## 순서
- 설치 전 확인 사항
- 설치
- 기동 및 종료

## 설치 전 확인사항

### 확인사항
- http://nginx.org/en/docs/windows.html
- Nginx for Windows의 경우, native Win32 API를 사용하여 높은 성능과 확장성이 나오지 않아 해당 이슈로 베타 버전에 머물러 있다.(version 1.21.5)

## 설치

### 설치 파일 다운로드 및 압축해제
- http://nginx.org/en/download.html
- 설치 파일: nginx-$(버전).zip

  ![image](https://user-images.githubusercontent.com/96853118/148350490-14a77209-c267-41a4-9d65-cb65a94c5c17.png)

- Nginx 를 설치할 경로에서 내려받은 nginx 설치파일 압축 해제

  ![image](https://user-images.githubusercontent.com/96853118/148354630-560ed0fc-7b35-4030-a93d-846718a4b6bd.png)


### Windows 환경변수 등록
- 환경 변수 등록 : PATH 에 nginx.exe 가 포함된 경로 등록
- Windows 시스템 속성 > 환경변수(N)... > 시스템 변수(S) > Path선택 > 편집(I)... > 새로 만들기(N) > [설치경로] 입력 > 확인


### Nginx 설정
- Nginx설치경로/conf/nginx.conf 에서 수정
- Listen 포트 변경 : http { server { listen  80(기본값)에서 원하는 포트로 변경

### Windows 서비스 등록
- Nginx에서 공식적으로 제공 하고 있지 않음
- winsw, nssm와 같이 oss sw를 사용하여 등록
- Nginx는 기본 background 동작이기 CMD 에서 관리가 가능함



## 기동 및 종료

### cmd 를 이용한 기동 / 종료

#### cmd 를 이용한 기동
- 명령프롬프트(cmd) 를 관리자모드로 실행
- Nginx 설치경로로 이동
- nginx.exe 실행
- Nginx 가 D:\hyperframe\nginx-1.21.5 에 설치된 경우, 아래와 같이 실행
  ```
  Microsoft Windows [Version 10.0.19042.867]
  (c) 2020 Microsoft Corporation. All rights reserved.
  
  C:\WINDOWS\system32>d:
  
  D:\>cd hyperframe
  
  D:\hyperframe>cd nginx-1.21.5
  
  D:\hyperframe\nginx-1.21.5>nginx.exe
  ```

#### 기동 확인
- 작업관리자 > 세부정보 에서 nginx.exe 프로세스 확인
  : 실행 중 상태의 nginx.exe 프로세스 확인
- cmd 창에 다음 명령으로 nginx.exe 프로세스 및 PID 확인
  ```
  tasklist | findstr nginx.exe
  ```

#### cmd 를 이용한 종료
- 명령프롬프트(cmd) 를 관리자모드로 실행하고 Nginx 설치경로로 이동
- 아래와 같이 실행
  ```
  Microsoft Windows [Version 10.0.19042.867]
  (c) 2020 Microsoft Corporation. All rights reserved.
  
  C:\WINDOWS\system32>d:
  
  D:\>cd hyperframe
  
  D:\hyperframe>cd nginx-1.21.5
  
  D:\hyperframe\nginx-1.21.5>nginx.exe -s stop
  ```

#### 종료 확인
- 작업관리자 > 세부정보 에서 nginx.exe 프로세스 확인
- cmd 창에 다음 명령으로 nginx.exe 프로세스 및 PID 확인
  ```
  tasklist | findstr nginx.exe
  ```

### Windows service를 이용한 기동 / 종료
Windows 서비스를 등록한 경우에만 사용할 수 있다.

#### Windows service를 이용한 기동
- Windows 서비스 목록에서 nginx 선택
- 상단 메뉴바 또는 좌상단 설명란에서 "서비스 시작" 메뉴 선택

#### 기동 확인
- 작업관리자 > 세부정보 에서 nginx.exe 프로세스 확인
  : 실행 중 상태의 nginx.exe 프로세스 확인
- cmd 창에 다음 명령으로 nginx.exe 프로세스 및 PID 확인
  ```
  tasklist | findstr nginx.exe
  ```

#### Windows service를 이용한 종료
- Windows 서비스 목록에서 nginx 선택
- 상단 메뉴바 또는 좌상단 설명란에서 "서비스 중지" 메뉴 선택

#### 종료 확인
- 작업관리자 > 세부정보 에서 nginx.exe 프로세스가 제거된 것 확인
- cmd 창에 다음 명령으로 nginx.exe 프로세스가 제거되었는지 확인
  ```
  tasklist | findstr nginx.exe
  ```

## 기본 페이지 호출
- http://[서버IP]:80/
- Nginx설치경로/html/index.html 호출

![image](https://user-images.githubusercontent.com/96853118/148363820-dd9de436-9752-4b63-9815-ece12b97c39b.png)







HyperFrame Nginx for Win64
nginx/Windows-1.21.5
