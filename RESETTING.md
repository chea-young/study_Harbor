## 설치 이후 설정 변경 및 적용하기
```
update-ca-trust extract
systemctl restart docker
docker-compose down -v 
./prepare # 변경사항 적용
docker-compose up -d
```

## https 적용하기

https.certificate: {server.cert로 수정 (예시, /etc/docker/certs.d/server/server.cert)
https.private_key: {server.key로 수정 (예시, /etc/docker/certs.d/server/server.key)

## update-ca-certificates
```
yum install ca-certificates
update-ca-trust force-enable
update-ca-trust extract
```

openssl x509 -req -sha512 -days 3650 \
-extfile v3ext.cnf \
-CA ca.crt -CAkey ca.key -CAcreateserial \
-in server.csr \
-out server.crt

openssl req -x509 -new -nodes -sha512 -days 3650 \
-key ca.key \
-out ca.crt

#### 참고 사이트
+ https://wookiist.dev/126
+ https://docs.vmware.com/kr/VMware-vSphere/7.0/vmware-vsphere-with-tanzu/GUID-F98E7DAF-7AFF-4E3F-AB98-A026236CE5C8.html
+ https://docs.vmware.com/kr/VMware-vSphere/7.0/vmware-vsphere-with-tanzu/GUID-963A4FFC-88F5-4916-B12C-F834F519D0C2.html