## https 설정하기
```
openssl genrsa -out ca.key 4096

openssl req -x509 -new -nodes -sha512 -days 365 \
> -key ca.key \
> -out ca.crt
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:kr
State or Province Name (full name) []:uilljeonbu
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:

openssl genrsa -out server.key 4096
Generating RSA private key, 4096 bit long modulus (2 primes)
.......++++
......................++++
e is 65537 (0x010001)

openssl req -sha512 -new \
> -key server.key \
> -out server.csr
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:kr
State or Province Name (full name) []:
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:

ls # 생성 확인
ca.crt  ca.key  server.csr  server.key

openssl x509 -req -sha512 -days 365 \
> -extfile v3ext.cnf \
> -CA ca.crt -CAkey ca.key -CAcreateserial \
> -in server.csr \
> -out server.crt

openssl x509 -inform PEM -in server.crt -out server.cert
```

- 이후 server.crt와 server.key가 생성된 위치에 harbor 설정 키를 해당 위치로 변경해서 올리기
```
https.certificate: {server.cert로 수정 (예시, /etc/docker/certs.d/server/server.cert)
https.private_key: {server.key로 수정 (예시, /etc/docker/certs.d/server/server.key)
```

#### 참고사이트
+ https://wookiist.dev/126