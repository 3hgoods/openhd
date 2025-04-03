

https://learn.microsoft.com/ko-kr/windows/wsl/#try-wsl-preview-features-by-joining-the-windows-insiders-program
WSL 데모

WSL2: Linux용 Windows 하위 시스템에 더 빠르게 코딩합니다. | 탭과 공백(13:42)
WSL: Linux GUI Apps 실행 | 탭과 공백(17:16)
WSL 2: USB 디바이스 연결 | 탭과 공백(10:08)
WSL 2 사용하여 GPU 가속 Machine Learning | 탭과 공백(16:28)
Visual Studio Code: SSH, VM 및 WSL 사용하여 원격 개발 | 탭과 공백(29:33)
Windows 개발자 도구 업데이트: WSL, 터미널, 패키지 관리자 및 기타 | 탭 및 공백(20:46)
WSL 사용하여 Node.JS 앱 빌드 | 강조 표시(3:15)
WSL 2 새 메모리 회수 기능 | 데모(6:01)
Windows에서 웹 개발 (2019년) | 데모(10:39)

WSL 2: USB 디바이스 연결
https://youtu.be/I2jOuLU4o8E

https://github.com/dorssel/usbipd-win/releases 설치

퍼워셀 관리자 권한 실행
usbipd list
usbipd bind --busid 1-6
usbipd attach --busid 1-2 --wsl
usbipd detach --busid 1-6

