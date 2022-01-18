## harbor에 docker 이미지 올리기

```
# 만약 이용하려는 이미지가 없다면 docker image에서 확인하고 없다면 docker pull한 상태에서
docker tag busybox:latest 192.168.50.160:8888/test/busybox:v1
docker push 192.168.50.160:8888/test/busybox:v1 # 올바르게 올라갔다면 다음과 같은 출력을 확인 가능
The push refers to repository [192.168.50.160:8888/test/busybox]
d94c78be1352: Pushed
v1: digest: sha256:34efe68cca33507682b1673c851700ec66839ecf94d19b928176e20d20e02413 size: 527
```

#### 참고 사이트
- https://waspro.tistory.com/631
