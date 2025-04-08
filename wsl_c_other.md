wsl D 저장

wsl --list --online
다음은 설치할 수 있는 유효한 배포판 목록입니다.
'wsl.exe --install <Distro>'를 사용하여 설치합니다.

NAME                            FRIENDLY NAME
AlmaLinux-8                     AlmaLinux OS 8
AlmaLinux-9                     AlmaLinux OS 9
AlmaLinux-Kitten-10             AlmaLinux OS Kitten 10
Debian                          Debian GNU/Linux
SUSE-Linux-Enterprise-15-SP5    SUSE Linux Enterprise 15 SP5
SUSE-Linux-Enterprise-15-SP6    SUSE Linux Enterprise 15 SP6
Ubuntu                          Ubuntu
Ubuntu-24.04                    Ubuntu 24.04 LTS
kali-linux                      Kali Linux Rolling
openSUSE-Tumbleweed             openSUSE Tumbleweed
openSUSE-Leap-15.6              openSUSE Leap 15.6
Ubuntu-18.04                    Ubuntu 18.04 LTS
Ubuntu-20.04                    Ubuntu 20.04 LTS
Ubuntu-22.04                    Ubuntu 22.04 LTS
OracleLinux_7_9                 Oracle Linux 7.9
OracleLinux_8_7                 Oracle Linux 8.7
OracleLinux_9_1                 Oracle Linux 9.1


wsl --install -d Ubuntu-22.04
기본적으로 wsl --install -d Ubuntu-20.04로 설치하면 Ubuntu는 C드라이브의 기본 위치 (예: %USERPROFILE%\AppData\Local\Packages)에 설치됩니다.
 MS Store에서 설치 후 export → import)

#설치 확인 - 비번까지 셋팅 
wsl --list --verbose

wsl --shutdown 
혹은 wsl --terminate Ubuntu-22.04

d:
mkdir WSL
cd WSL
mkdir Ubuntu-22.04

# 기존 Ubuntu export
wsl --export Ubuntu-22.04 D:\WSL\Ubuntu-22.04\ubuntu.tar
# 원하는 위치로 import
wsl --import Ubuntu-22.04 D:\WSL\Ubuntu-22.04 D:\WSL\Ubuntu-22.04\ubuntu.tar --version 2
제공된 이름의 배포가 이미 있습니다. --name 사용하여 다른 이름을 선택하십시오.
오류 코드: Wsl/Service/RegisterDistro/ERROR_ALREADY_EXISTS
wsl --import Ubuntu-2204 D:\WSL\Ubuntu-22.04 D:\WSL\Ubuntu-22.04\ubuntu.tar --version 2


wsl --list --verbose
  NAME                   STATE           VERSION
* Ubuntu-22.04           Stopped         2
  docker-desktop-data    Stopped         2
  Ubuntu-2204            Stopped         2
  docker-desktop         Stopped         2

wsl --unregister Ubuntu-22.04
# 기존 시스템 제거 import 후에 하는게 더 효과적인거 같음.

c가 53.9G여유 --> 55.1G 여유로 변경됨.

