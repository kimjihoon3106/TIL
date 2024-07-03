## 경진대회pka
### 가. 기본 구성
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
3. R1 라우터의 Gig0/0 포트에 Description 설정을 합니다.
-문구는 "This is Private Network"로 설정합니다.

``` bash
R1(config) #int g0/0
R1(config-if) #description This is Private Network
```

4. R3 라우터에 배너 설정을 합니다.
- 라우터에 접근 시, “Check your access permissions." 문구가 뜨도록 합니다.

```bash
R3(config)# banner motd *Check your access permisssions.
```

5. R2, R3, R4, R7 라우터의 config 모드 접근 시, md5 암호화 알고리즘이 적용된 암호 로 접근하도록 합니다. (암호는 “2017yynet"을 사용합니다.)

```bash
// ex
R2(config)#enable secret 2017yynet
```

6. R1, R4, R8, R9 에 콘솔 접근 시, 로컬 계정 인증을 수행할 수 있도록 합니다.
( username : [자신의 hostname] / password : Skills39@@ )

```bash
// ex
R1(config)#username R1 password Skills39@@
```

7. R5는 잠겨 있습니다. IP 정보를 확인 시, CDP 프로토콜을 사용하여 확인합니다.
```bash
R4(config)# cdp enable
R4(conf-if)#exit
R4(config)#cdp run
R4#exit
R4#show cdp neighbors detail
```
8. 모든 시리얼 링크의 clock rate는 64000으로 설정하도록 합니다.

시계표시가 있는 부분만 설정하면 된다.
```bash
R2(config)# int s0/0/0
R2(config-if)# clock rate 64000
```
---

### 나. 서브넷팅
1. A 와 B 지역에 주어진 기본 주소 대역과 할당 범위를 잘 참고하여 주소를 할당 합니다.
2. PC7과 PC8는 해당 서브넷의 2번째 주소를 할당합니다.

참고 하세요
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

---

다. VLAN 및 이더채널 구성
귀찮지만 잘생긴 나 니까 올려드려요
1. 각 VLAN 설정은 토폴로지를 참고합니다.
```bash
Switch(config)# vlan 10
Swtich(config-vlan)# name chrome
Swtich(config-vlan)# int f0/1
Swtich(config-if)# swtichport access vlan 10
```

```bash
R1(config)# int g0/0.10
R1(config-subif)# encapsulation dot1Q 10
R1(config-subif)# ip address 10.0.0.254 255.255.255.0
```

2. SW3 와 SW4 사이의 이더채널을 설정합니다.
( 이더채널 프로토콜은 시스코 전용 프로토콜을 사용하도록 하며, 적극적인 협상을 하도록 합니다. channel-group은 1을 사용합니다. )

Sw3, Sw4 둘다 해야 함!!
```bash
Switch(config)# int range f0/23-24
Swtich(config-if-range)# channel-protocol pagp
Swtich(config-if-range)# channel-group 1 mode desirable
```
Sw3, Sw4 둘다 해야 함!!
```bash
// 중요!!
Switch(config-if-range)# switchport mode trunk
```
