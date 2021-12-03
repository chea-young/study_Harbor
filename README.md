# Harbor-
리눅스에 Private Docker Registry Harbor를 설치하고 실습 내용을 정리하는 Repository

## 왜 도입?
- Sonatype nexus를 사용했으나 maven, npm 등 사설 레지스트리로 사용하는데 충분하지만 Docker로 사용하기 위해서는 https 사용할 수 없어 추가적인 설정이 필요했기 때문에 계속해서 사용하기 에는 적합하지 않다고 판단
- Docker Hub는 무료로 사용하기 위해서는 public으로 공개해야 하는 점, private로 사용할 경우 추가적인 비용을 지불해야 한다는 점에서 연구실에서 사용하기에는 부적합


### Harbor
- registry가 아닌 project라는 이름으로 정보 저장소 제공
- 포털로 올리고 내리는 것이 가능
```
docker login https://192.168.50.160:8888
로그인해서 받는 것이 같음.

# 이미지 업로드
docker tag SOURCE_IMAGE[:TAG] [MyDomain.com]:[PORT]/[PROJECT]/IMAGE[:TAG]
#push 
docker push [MyDomain.com]:[PORT]/[PROJECT]/IMAGE[:TAG]

# 이미지 다운로드
docker pull [MyDomain.com]:[PORT]/[PROJECT]/IMAGE[:TAG]
```

## 설치하기
```
#docker-compose 설치 (1.18 버전 이상이여야 한다.)
# ./install.sh 할 때 docker-compose가 필요하다
# 링크: https://dejavuhyo.github.io/posts/install-docker-compose/
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

docker-compose --version # 설치 확인

# 인증서 받기
 yum install epel-release
 yum install certbot -y
 sudo systemctl stop nginx
certbot certonly -d harbor.domain.com
2
/etc/letsencrypt/live/harbor/

#Harbor
# 링크: https://waspro.tistory.com/630
# 2021-12-02 기준으로 v2.3.4가 가장 최신
wget https://github.com/goharbor/harbor/releases/download/v2.3.4/harbor-offline-installer-v2.3.4.tgz

tar -xvf harbor-offline-installer-v2.3.4.tgz

cd harbor
nano harbor.yaml # hostname-> ip로 수정, https-> 주석
mkdir /etc/letsencrypt/live/harbor/ 생성

./install.sh

192.168.50.160:8888 접속
admin/Harbor12345


docker login https://192.168.50.160:8888  -u admin -p Harbor12345
```