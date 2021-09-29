### 빌드 환경

- CentOS Linux release 7.7.1908

### 파일 내역
등록된 nginx_1.20_build.tar.gz는 아래의 라이브러리들이 컴파일돼서 빌드되었음

- openssl-1.1.1k
- pcre-8.45
- zlib-1.2.11

압축파일의 빌드된 경로는 아래를 참고

    $ tar -xzvf nginx1.20_build.tar.gz
    $ cd nginx1.20
    # nginx 1.20을 설치하면 conf, html, logs, sbin 폴더가 기본적으로 설치되나, nginx1.20 폴더 아래에 src 폴더를 별도로 생성하여 필요한 라이브러리 위치시킴
    $ cd ${NGINX_HOME}/src
    # openssl, pcre, zlib 등 빌드한 파일은 아래의 경로로 위치
    $ cd ${NGINX_HOME}/src/build
    $ ls -al
     drwxrwxr-x 5 hfnginx hfnginx 45  9월 29 11:23 .
     drwxrwxr-x 7 hfnginx hfnginx 97  9월 29 11:30 ..
     drwxrwxr-x 7 hfnginx hfnginx 67  9월 29 11:19 openssl
     drwxrwxr-x 6 hfnginx hfnginx 56  9월 29 11:21 pcre
     drwxrwxr-x 5 hfnginx hfnginx 45  9월 29 11:23 zlib
    



