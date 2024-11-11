# linux os install 과정에서 구형 노트북 환경설정시 wifi 연결 오류 발생
* 구형 노트북에서 와이파이 모듈의 제조사에 따라 2개로 나뉠수 있슴.
    * intel 와이파이 모듈
    * broadcom 와아파이 모듈
    우선 노트북에 장착된 wifi 모듈을 확인해야함.

    * 레노버 e430 model은 broadcom wifi 모듈이 장착되어 있어서 드라이버 설치가 되어 있어야 동작 함

# 구형 노트북 wifi 연결 해결 방법
* 필요 용품 
    * WIFI usb 수신기
    * linux 버전에 따른 wifi driver install 

*  드라이버 충돌 방지
    * /etc/modprobe.d/blacklist.conf 파일을 수정하여 사용하지 않을 드라이버를 블랙리스트에 추가
    ~~~
    sudo nano /etc/modprobe.d/blacklist.conf
    ~~~
    상기 파일을 열어 아래의 내용을 추가하여 blacklist에 추가
    ~~~
    blacklist b43
    blacklist bcma
    blacklist brcmsmac
    ~~~

* 누락 펌웨어 install

    * Broadcom 드라이버는 종종 펌웨어 파일을 요구하기 때문에 설치 진행
    ~~~
    sudo apt update
    sudo apt install firmware-b43-installer
    ~~~

## 노트북 내부의 wifi 수신기로 수신하는것 보다 usb 수신기로 사용하게 되면 느리기 떄문에 꼭 노트북에 사용된 wifi 수신 모듈로 사용할수 있게 설정하는 것을 추천 드림 
다이소 5000원 리시버 기준 약 100배 정도 차이 나는것으로 보임