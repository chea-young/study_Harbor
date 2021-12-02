## 재설정

```
- docker-compose down -v 
- ./prepare --with-clair --with-chartmuseum # 변경사항 적용
- docker-compose up -d 

https.certificate: {server.cert로 수정 (예시, /etc/docker/certs.d/server/server.cert)
https.private_key: {server.key로 수정 (예시, /etc/docker/certs.d/server/server.key)
```