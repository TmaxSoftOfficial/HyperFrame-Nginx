### 빌드 환경

- CentOS Linux release 7.7.1908

### 파일 등록 내역
등록된 nginx_1.20_build.tar.gz는 아래의 라이브러리들이 컴파일된 빌드가 포함된 바이너리 파일

- openssl-1.1.1k
- pcre-8.45
- zlib-1.2.11

압축파일의 빌드된 경로는 아래를 참고

    $ tar -xzvf nginx1.20_build.tar.gz
    $ cd ${NGINX_HOME}
    
    # nginx 1.20을 설치하면 conf, html, logs, sbin 폴더가 기본적으로 설치되나, nginx1.20 폴더 아래에 src 폴더를 별도로 생성하여 필요한 라이브러리 위치시킴
    $ cd ${NGINX_HOME}/src
    $ ls -al
     drwxrwxr-x  7 hfnginx hfnginx   97  9월 29 11:30 .
     drwxrwxr-x  7 hfnginx hfnginx   65  9월 29 11:29 ..
     drwxrwxr-x  5 hfnginx hfnginx   45  9월 29 11:23 build
     drwxr-xr-x  9 hfnginx hfnginx  186  9월 29 11:27 nginx-1.20.1
     drwxrwxr-x 20 hfnginx hfnginx 4096  9월 29 11:29 openssl-1.1.1k
     drwxr-xr-x  9 hfnginx hfnginx 8192  9월 29 11:29 pcre-8.45
     drwxr-xr-x 14 hfnginx hfnginx 4096  9월 29 11:29 zlib-1.2.11
     
    # openssl, pcre, zlib 등 빌드한 파일은 아래의 경로로 위치
    $ cd ${NGINX_HOME}/src/build
    $ ls -al
     drwxrwxr-x 5 hfnginx hfnginx 45  9월 29 11:23 .
     drwxrwxr-x 7 hfnginx hfnginx 97  9월 29 11:30 ..
     drwxrwxr-x 7 hfnginx hfnginx 67  9월 29 11:19 openssl
     drwxrwxr-x 6 hfnginx hfnginx 56  9월 29 11:21 pcre
     drwxrwxr-x 5 hfnginx hfnginx 45  9월 29 11:23 zlib
    
### 빌드 파일 실행
등록된 빌드 파일을 실행 시 최초 빌드된 Path가 /home/hfnginx/nginx1.20로 fix되어 있으며, 아래와 같이 실행

    $ ./nginx -p ${NGINX_HOME}

