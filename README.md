## HyperFrameOE-Nginx
업로드된 바이너리는 HyperFrame Open Edition Nginx 제품 설치를 위한 파일  

## 사전에 필요한 설치 파일

### Nginx
* Version : nginx-1.20.1  
* Note : http://nginx.org/download/
   
### PCRE
* Version : pcre-8.45
* Note : https://ftp.pcre.org/pub/pcre/

## 설치 및 실행

### 1) Nginx 압축 풀기

    $ tar -zxf nginx-1.20.1.tar.gz

### 2) PCRE 설치

    $ cd ${NGINX_HOME}
    $ tar -zxf pcre-8.45.tar.gz
    $ cd ${NGINX_HOME}/pcre-8.45/
    $ ./configure --prefix=${PCRE_HOME}
    $ make && make install

### 3) Nginx 컴파일 설치

    $ cd ${NGINX_HOME}
    $ ./configure --prefix=${NGINX_HOME} --with-pcre=${PCRE_HOME} --with-http_ssl_module --with-http_stub_status_module make install

### 4) Nginx 실행

    $ cd ${NGINX_HOME}/sbin/
    $ ./nginx

### 5) Nginx 종료

* 강제 종료

      $ ./nginx -s stop      

* Request 처리 후 종료
      
      $ ./nginx -s quit      

### 6) Nginx 재기동

    $ ./nginx -s reload

## 디렉토리 구조

    # nginx_server_1
    ├── conf
    │    ├── fastcgi.conf <----------------------- FastCGI 환경설정 파일
    │    ├── fastcgi.conf.default
    │    ├── fastcgi_params
    │    ├── fastcgi_params.default
    │    ├── koi-utf
    │    ├── koi-win
    │    ├── mime.types
    │    ├── mime.types.default
    │    ├── nginx.conf <------------------------ 프로세스 개수, 접속사 수 등 Nginx 퍼포먼스 설정 파일
    │    ├── nginx.conf.default
    │    ├── scgi_params
    │    ├── scgi_params.default
    │    ├── uwsgi_params
    │    ├── uwsgi_params.default
    │    └── win-utf
    ├── html
    │    ├── 50x.html
    │    └── index.html
    ├── sbin
    │    └── nignx <------------------------ 기동 및 종료, 재기동을 위한 명령 파일
    └── logs
      
## 버전 확인

    $ cd /home/username/nginx_server_1/sbin/
    $ ./nginx -v
    nginx version: nginx/1.20.1

## 로그 정보

### 1) 로그 경로

    ${NGINX_HOME}/logs/
    
### 2) 로그 정보

* Error.log

      ${NGINX_HOME}/logs/error.log
  
* Access 로그

      ${NGINX_HOME}/logs/access.log

### 2) 로그 설정 변경

* Log Level 설정

      $ vi ${NGINX_HOME}/conf/nginx.conf
      # Log Level [ debug / info / notic / warn / error / crit ]
      error_log ${NGINX_HOME}/logs/error.log error;
      
* Access Log 끄기

      $ vi ${NGINX_HOME}/conf/nginx.conf
      http {
          ...
          access_log off;
          ...
      }
      
* Critical Logging 켜기

      $ vi ${NGINX_HOME}/conf/nginx.conf
      http {
          ...
          error_log <Log 저장 Path> crit;
          ...
      }
            
* Error Log 끄기

      $ vi ${NGINX_HOME}/conf/nginx.conf
      ...
      http {
          ...
          error_log off;
          ...
      }
      
## 환경 설정 파일 정보

### 1) 환경 설정 파일 경로

    ${NGINX_HOME}/conf/nginx.conf/
    
### 2) 환경 설정
    
* Port 변경 
      
      ...
      http {
          ...
          server {
              listen    8080;
              ...
          }
      }
      
* Header Nginx 버전 숨김 
      
      ...
      http {
          ...
          server tokens    off;
      }
      
## Nginx 명령

### 1) Nginx 컴파일 정보 확인

    $ cd ${NGINX_HOME}/sbin/
    $ ./nginx -V
    nginx version: nginx/1.20.1
    built by gcc 4.8.5 20150623 (Red Hat 4.8.5-44) (GCC)
    built with OpenSSL 1.1.1g  21 Apr 2020
    TLS SNI support enabled
    configure arguments: --prefix=${NGINX_HOME} --with-pcre=./pcre-8.45 --with-http_ssl_module --with-http_stub_status_module

### 2) 설정 파일 지정 Nginx 실행

    $ cd /home/username/nginx_server_1/sbin/
    $ ./nginx -c [설정파일]                              
   
   
### 3) 설정 파일 타당성 체크

* 타당성 체크 후 에러 메세지만 출력 (nginx 정지 후 실행 가능)

      $ cd /home/username/nginx_server_1/sbin/
      $ ./nginx -q                                           

* 타당성 체크 후 정상, 에러 메세지 출력 (nginx 정지 후 실행 가능)

      $ cd /home/username/nginx_server_1/sbin/
      $ ./nginx -t
      nginx: the configuration file /home/parkminjun/nginx_server_1/conf/nginx.conf syntax is ok
      nginx: configuration file /home/parkminjun/nginx_server_1/conf/nginx.conf test is successful
