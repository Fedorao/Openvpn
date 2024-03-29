# **OpenVPN Client 설치 및 설정**

본 Report는 그로윈 ㈜ OSS 사업본부 / Infra 기술팀 에서 제공하는 문서입니다.

운영중인 OpenVPN 시스템에 대한 Client 설정 정보를 포함하고 있습니다.



---
1.    https://openvpn.net/community-downloads/ 에서 " OpenVPN 2.5.8 -- Released 2 November 2022 " 버전을 다운로드.


---

2. 다운로드한 파일을 실행하여 설치 진행  
(윈도우10의 경우 C:\Program Files\OpenVPN에 설치됩니다.)

 ![1](https://user-images.githubusercontent.com/96568963/147732133-bc03b1cc-ce81-4060-8c5d-6ea36788917f.png)  


---

3. 메일에 첨부되어 있는 파일을 C:\Program Files\OpenVPN\config 경로로 복사합니다.

   ca.crt
 
   id.crt
 
   id.key


---

4. C:\Program Files\OpenVPN\config 경로에 client.ovpn 파일 생성해줘야 합니다.  

아래 양식 사용하면 되며, id부분엔 본인의 crt와 key 정보기입.  
[client.ovpn 파일보기](https://github.com/Fedorao/Openvpn/blob/main/client.ovpn)
 

 
---

5. 설정파일과 동일한 경로로 openvpn 경로 설정이 필요합니다.

1 - openvpn 파일을 관리자 권한으로 실행합니다.

![6](https://user-images.githubusercontent.com/96568963/221455910-dc5708c2-7016-4da4-89a4-9284e1f98e89.png)


2 - 숨겨진 아이콘 항목에서 openvpn 을 우클릭하여 설정을 클릭합니다.

![7](https://user-images.githubusercontent.com/96568963/221455914-77323073-31f1-4ffb-a24c-b5201e4bc51a.png)


3 - 상세에서 설정파일 경로와 로그파일 경로를 맞춰주고 확인을 클릭합니다.

![8](https://user-images.githubusercontent.com/96568963/221457238-56335d8b-151e-40c8-becd-24191d760d28.png)


---

6. 모든 client 설정이 끝났습니다.  
OpenVPN 실행파일을 관리자 권환으로 실행하면 작업표시줄에 다음같이 표시되고 Connect를 클릭하여 openvpn 서버에 접속합니다.  
(OpenVPN 실행파일은 반드시 관리자 권환으로 실행해야 합니다.)

![2](https://user-images.githubusercontent.com/96568963/147732139-cbeb18c1-cf75-40e5-a9ab-1aae7618018d.png) 

 
---

7. 접속이 완료되면 10.8.0.x 대역의 IP를 할당 받게 됩니다.
 
![3](https://user-images.githubusercontent.com/96568963/147732140-59262b77-4d6a-4f7a-89e7-ef180aeb4e11.png)

 
---

8. OpenVPN Server IP는 10.8.0.1 입니다.  
OpenVPN에 문제가 없다면 라우팅 확인시 10.8.0.1을 게이트웨이로 가지는 대역이 추가됩니다.  
해당 IP로 PING 테스트시 문제가 없다면 모든 설정이 정상적으로 이루어진 것입니다.  
(접속이 정상적이지 않다면 설정파일점검이나,윈도우방화벽,알약v3등의 확인이 필요합니다.)

 ![4](https://user-images.githubusercontent.com/96568963/147732142-28968002-ec29-4abb-8dc8-a5ffd94ace9c.png)

---

**■ OPENVPN이슈 사항**
 
1. There are no TAP-Windows adapters on this system. You should be able to create a TAP-Windows adapter by going to Start -> All Programs -> TAP-Windows -> Utilities -> Add a new TAP-Windows virtual ethernet adapter.

**조치방법**
 
- 시작메뉴 TAP-Windows 폴더
openvpn을 설치하면 이 가상 어댑터를 관리하는 Tap-windows가 같이 설치됩니다.  
윈도우에서 이 어댑터가 문제가 생겨서 접속실패가 되는 것이므로 초기화 작업이 필요합니다.

- Delete All Tap Virtual ethernet adapters 눌러서 삭제  
- Add a new Tap Virtual ethernet adapters 눌러서 새로 생성

![5](https://user-images.githubusercontent.com/96568963/147732144-c63570cd-9360-4df2-8c31-43ef377868da.png)

---
 
2. write to tun/tap invalid argument (code=22)

**조치방법**
- 설정파일에서 comp-lzo 라인 주석제거

---

3. msi 확장자로 설치시 notepad에서 아래 작업 수행 필요

**조치방법**
- 편집 > 줄끝 문자(EOL) 변환 > Unix (LF) 선택
