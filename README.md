## HyperFrameOE-Nginx
업로드된 바이너리는 HyperFrame Open Edition Nginx 제품 설치를 위한 파일  

## 사전에 필요한 설치 파일

### Nginx
* Version : nginx-1.20.1  
* Note : http://nginx.org/download/
   
### PCRE
* Version : pcre-8.45
* Note : https://ftp.pcre.org/pub/pcre/

## 검증 환경

* CentOS Linux release 7.9.2009 (Core)

## 설치 및 실행

### 1) Nginx 압축 풀기

    $ tar -zxf nginx-1.20.1.tar.gz

### 2) 디렉토리 구조 확인

    # nginx
    ├── conf
    │    ├── fastcgi.conf 
    │    ├── fastcgi.conf.default
    │    ├── fastcgi_params
    │    ├── fastcgi_params.default
    │    ├── koi-utf
    │    ├── koi-win
    │    ├── mime.types
    │    ├── mime.types.default
    │    ├── nginx.conf 
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
    │    └── nignx
    └── logs
    
### 3) PCRE 설치

    $ cd ${NGINX_HOME}
    $ tar -zxf pcre-8.45.tar.gz
    $ cd ${NGINX_HOME}/pcre-8.45/
    $ ./configure --prefix=${PCRE_HOME}
    $ make && make install

### 4) Nginx 컴파일 설치

    $ cd ${NGINX_HOME}
    $ ./configure --prefix=${NGINX_HOME} --with-pcre=${PCRE_HOME} --with-http_ssl_module --with-http_stub_status_module 
    $ make && make install

### 5) Nginx 실행

    # binaries에 등록된 nginx.tar.gz 바이너리의 ${NGINX_HOME}의 기본값은 /home/nginx/.
    # 기본값이 아닌 다른 경로에서 기동 시 옵션 -p을 사용하여, 실제 Nginx Home 경로로 기동.
    
    $ cd ${NGINX_HOME}/sbin/
    $ ./nginx -p ${NGINX_HOME}
    
### 6) Nginx 종료

* 강제 종료

      $ ./nginx -s stop      

* Request 처리 후 종료
      
      $ ./nginx -s quit      

### 7) Nginx 재기동

    $ ./nginx -s reload
    
## 버전 확인

    $ cd ${NGINX_HOME}/sbin/
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
    configure arguments: --prefix=${NGINX_HOME} --with-pcre=./pcre-8.45 --with-http_stub_status_module

### 2) 설정 파일 지정 Nginx 실행

    $ cd ${NGINX_HOME}/sbin/
    $ ./nginx -c [설정파일]                              
   
   
### 3) 설정 파일 타당성 체크

* 타당성 체크 후 에러 메세지만 출력 (nginx 정지 후 실행 가능)

      $ cd ${NGINX_HOME}/sbin/
      $ ./nginx -q                                           

* 타당성 체크 후 정상, 에러 메세지 출력 (nginx 정지 후 실행 가능)

      $ cd ${NGINX_HOME}/sbin/
      $ ./nginx -t
      nginx: the configuration file ${NGINX_HOME}/conf/nginx.conf syntax is ok
      nginx: configuration file ${NGINX_HOME}/conf/nginx.conf test is successful

