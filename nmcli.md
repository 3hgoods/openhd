
ref https://www.radishlogic.com/linux/how-to-connect-to-wifi-using-nmcli/

https://jangkunstory.tistory.com/156

https://tstigma.tistory.com/112

1.nmtui 명령어 사용하기
# nmtui 
# systemctl start network 
# systemctl restart network 
ifup <장치이름> 및 ifdown <장치이름>
  - 네트워크 장치를 On 또는 Off 시키는 명령어
  - systemctl <start/stop/restart/status> network 적용되지 않을 때 사용

1. 네트워크 장치를 확인해보기 
# ifconfig 

2. 끄기 켜기 
# ifup ens-32 
# ifdow ens-32
