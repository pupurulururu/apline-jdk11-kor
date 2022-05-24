# apline-jdk11-kor


ubuntu는 크기가 크기 떄문에 jdk11에서 timezone과 locale을 kor로 변경

https://ssaru.github.io/2021/05/09/20210509-til_set_locale_in_alpine_linux/

위 사이트에 있는 내용을 사용하려 했으나 


executor failed running [/bin/sh -c apk --no-cache add ca-certificates wget &&     wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub &&     wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk &&     apk add glibc-2.25-r0.apk]: exit code: 8

에러가 발생하여 docker build가 되지 않았음

alpine image의 /bin/sh 로 들어가서 위의 명령을 실행하였으나 /usr/glibc는 설치되지 않았다.


https://stackoverflow.com/questions/37818831/is-there-a-best-practice-on-setting-up-glibc-on-docker-alpine-linux-base-image

위의 사이트에 있는 내용을 실행해보니 되서 

wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
    
->

wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \

로만 바꿨다.

...

.pub 파일 주는 링크가 바뀐건가 
