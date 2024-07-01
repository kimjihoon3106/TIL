## 경진대회pka
### 1. 기본 구성
1. 모든 라우터의 이름을 토폴로지를 참고하여, 변경하도록 합니다.

ex)
```bash
R2> en
R2# conf t
R2(config)#hostname R2
```
2. 다음과 같이 IP 주소를 할당합니다.
-PC는 해당 서브넷의 첫 번째 IP 할당
-Server는 해당 서브넷의 10번째 IP 할당
-Gateway는 해당 서브넷의 마지막 IP 할당

```bash
// pc0
IP Address : 10.0.0.1
Subnet Mask : 255.255.255.0
Default Gateway : 10.0.0.254
```

```bash
// pc1
IP Address : 10.0.1.1
Subnet Mask : 255.255.255.128
Default Gateway : 10.0.1.126
```

```bash
// pc2
IP Address : 10.0.1.129
Subnet Mask : 255.255.255.192
Default Gateway : 10.0.1.190
```

```bash
// pc3
IP Address : 10.0.1.193
Subnet Mask : 255.255.255.240
Default Gateway : 10.0.1.206
```

```bash
// pc4
IP Address : 1.1.1.5
Subnet Mask : 255.255.255.252
Default Gateway : 1.1.1.6
```

```bash
// pc5
IP Address : 11.11.0.1
Subnet Mask : 255.255.255.128
Default Gateway : 11.11.0.126
```

```bash
// pc6
IP Address : 11.11.0.129
Subnet Mask : 255.255.255.224
Default Gateway : 11.11.0.158
```

```bash
// pc7
IP Address : 11.11.0.2
Subnet Mask : 255.255.255.128
Default Gateway : 11.11.0.126
```

```bash
// pc8
IP Address : 11.11.0.130
Subnet Mask : 255.255.255.224
Default Gateway : 11.11.0.158
```

```bash
// pc9
IP Address : 5.5.5.1
Subnet Mask : 255.255.255.0
Default Gateway : 5.5.5.254
```

```bash
// pc10
IP Address : 5.5.5.2
Subnet Mask : 255.255.255.0
Default Gateway : 5.5.5.254
```
