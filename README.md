# HyperFrameOE-Nginx
업로드된 바이너리는 HyperFrame Open Edition Nginx 제품 설치를 위한 파일
# 사전에 필요한 설치 파일
1) Nginx/
       - Version : nginx-1.20.1.tar.gz
       - Install : http://nginx.org/download/nginx-1.20.1.tar.gz
   
2) PCRE
       - Version : pcre-8.45.tar.gz
       - Install : https://ftp.pcre.org/pub/pcre/pcre-8.45.tar.gz

3) Zlib
       - Version : zlib-1.2.11.tar.gz
       - Install : https://www.zlib.net/zlib-1.2.11.tar.gz
4) Openssl
       - Version : openssl-1.1.1g.tar.gz
       - Install : https://www.openssl.org/source/openssl-1.1.1g.tar.gz

# 설치 및 실행

1) Nginx 압축 풀기

      $ cd /home/
      
      $ tar -zxf nginx-1.20.1.tar.gz
      

2) PCRE 설치

      $ cd /home/nginx-1.20.1
      
      $ tar -zxf pcre-8.45.tar.gz
      
      $ cd /home/nginx-1.20.1/pcre-8.45/
      
      $ ./configure --prefix=${PCRE_HOME}
      
      $ make && make install
      

3) zlib 설치

      $ cd /home/nginx-1.20.1
      
      $ tar -zxf zlib-1.2.11.tar.gz
      
      $ cd /home/nginx-1.20.1/zlib-1.2.11/
      
      $ ./configure --prefix=${ZLIB_HOME}
      
      $ make && make install
      

4) OpenSSL 설치

      $ cd /home/nginx-1.20.1
      
      $ tar -zxf openssl-1.1.1g.tar.gz
      
      $ cd /home/nginx-1.20.1/openssl-1.1.1g/
      
      $ ./config shared zlib --prefix=${OPENSSL_HOME}
      
      $ make && make install
      

5) Nginx 컴파일 설치

      $ cd /home/nignx-1.20.1/
      
      $ ./configure --prefix=/home/username/nginx_server_1 --with-zlib=${ZLIB_HOME} --with-pcre=${PCRE_HOME} --with-openssl=${OPENSSL_HOME} --with-http_ssl_module --with-http_stub_status_module
      
make install


6) Nginx 실행

      $ cd /home/username/nginx_server_1/sbin/
      
      $ ./nginx
      

7) Nginx 종료

      - 강제 종료
      - 
        $ ./nginx -s stop
        

      - Request 처리 후 종료
      - 
        $ ./nginx -s quit
        

8) Nginx 재기동

      $ ./nginx -s reload
      
      
# 디렉토리 구조

$ cd /home/username/nginx_server_1/
   
   nginx_server_1
   
   ├── conf
   
   │   ├── fastcgi.conf <----------------------- FastCGI 환경설정 파일
   
   │   ├── fastcgi.conf.default
   
   │   ├── fastcgi_params
   
   │   ├── fastcgi_params.default
   
   │   ├── koi-utf
   
   │   ├── koi-win
   
   │   ├── mime.types
   
   │   ├── mime.types.default
   
   │   ├── nginx.conf <------------------------ 프로세스 개수, 접속사 수 등 Nginx 퍼포먼스 설정 파일
   
   │   ├── nginx.conf.default
   
   │   ├── scgi_params
   
   │   ├── scgi_params.default
   
   │   ├── uwsgi_params
   
   │   ├── uwsgi_params.default
   
   │   └── win-utf
   
   ├── html
   
   │   ├── 50x.html
   
   │   └── index.html
   
   ├── sbin
   
   │   └── nignx <------------------------ 기동 및 종료, 재기동을 위한 명령 파일
   
   └── logs
   
# 버전 체크
  $ cd /home/username/nginx_server_1/sbin/
  
  $ ./nginx -v
  
    nginx version: nginx/1.20.1
    
# 컴파일 옵션 체크
$ cd /home/username/nginx_server_1/sbin/

$ ./nginx -V

  nginx version: nginx/1.20.1
  
  built by gcc 4.8.5 20150623 (Red Hat 4.8.5-44) (GCC)
  
  built with OpenSSL 1.1.1g  21 Apr 2020
  
  TLS SNI support enabled
  
configure arguments: --prefix=/home/parkminjun/nginx_server_1 --with-zlib=./zlib-1.2.11 --with-pcre=./pcre-8.45 --with-openssl=./openssl-1.1.1g --with-http_ssl_module --with-http_stub_status_module

# 설정 파일 지정 Nginx 실행
$ cd /home/username/nginx_server_1/sbin/

$ ./nginx -c [설정파일]

   (에러 내용 없을 시 정상 실행)
   
   
# 설정 파일 타당성 체크
1) 타당성 체크 후 에러 메세지만 출력 (nginx 정지 후 실행 가능)

   $ cd /home/username/nginx_server_1/sbin/
       
   $ ./nginx -q
   
     (에러 내용 없을 시 출력되는 내용 없음)

   2) 타당성 체크 후 정상, 에러 메세지 출력 (nginx 정지 후 실행 가능)
   
   $ cd /home/username/nginx_server_1/sbin/
       
   $ ./nginx -t
       
     (설정 파일 타당성 정상일 경우)
         
     nginx: the configuration file /home/parkminjun/nginx_server_1/conf/nginx.conf syntax is ok
         
     nginx: configuration file /home/parkminjun/nginx_server_1/conf/nginx.conf test is successful
         
