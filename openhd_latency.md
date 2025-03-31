

openHD는 rtl8812au를 이용하는데 wifi 통신과 차이점이 무엇이니?

penHD는 RTL8812AU 칩셋을 사용하여 FPV(First-Person View) 영상 전송을 수행하는데, 일반적인 Wi-Fi 통신과 몇 가지 중요한 차이점이 있습니다.

✅ Wi-Fi 통신 vs. OpenHD (RTL8812AU 기반)
특징	일반 Wi-Fi	OpenHD (RTL8812AU 기반)
목적	데이터 통신 (인터넷, 파일 전송)	저지연(로우 레이턴시) FPV 영상 전송
프로토콜	802.11 표준 Wi-Fi 프로토콜 사용	Wi-Fi PHY 레이어 사용하지만 맞춤형 전송 방식
레이턴시 (지연 시간)	10~100ms 이상 (일반적인 Wi-Fi 영상 스트리밍)	50ms 이하 (실시간 FPV)
대역폭 사용 방식	주파수 공유 및 충돌 방지 기능 포함	고정된 대역폭 사용, 효율적인 전송
비디오 전송 방식	압축된 비디오 (H.264 등)	낮은 지연 시간의 비디오 프레임 전송
재전송 (Retransmission)	패킷 손실 시 재전송 (신뢰성 우선)	재전송 최소화 (실시간 성능 우선)
하드웨어	스마트폰, 노트북 등 일반적인 Wi-Fi 기기	RTL8812AU 칩셋 기반 USB Wi-Fi 모듈
통신 거리	수십~수백 미터 (Wi-Fi 환경에 따라 다름)	수 km까지 가능 (고출력 증폭기 사용 시)

🔹 핵심 차이점
실시간 저지연 전송

일반적인 Wi-Fi는 안정성과 신뢰성을 위해 패킷 손실 시 재전송을 수행하지만, OpenHD는 FPV에 맞춰 지연 시간을 최소화하고 재전송을 줄이는 방식으로 작동합니다.

고정된 주파수 및 대역폭 최적화

OpenHD는 **Wi-Fi의 PHY 레이어(물리 계층)**를 사용하지만, 일반적인 Wi-Fi 네트워크처럼 다양한 장치가 연결되는 구조가 아니라 단일 송수신 간 최적화된 연결을 설정합니다.

더 긴 통신 거리

일반적인 Wi-Fi 모듈은 주로 실내 및 근거리 통신에 적합하지만, OpenHD는 고출력 Wi-Fi 어댑터(예: 2W 이상)를 사용하여 몇 km까지 연결을 확장할 수 있습니다.

고성능 무압축(또는 저압축) 비디오 전송

OpenHD는 H.264/H.265 등의 압축 방식을 사용하지 않거나 최소한의 압축을 적용하여 빠른 화면 전송이 가능합니다.

📌 결론
OpenHD는 일반 Wi-Fi 통신과 달리, Wi-Fi PHY 레이어를 활용하지만 FPV 영상 전송에 최적화된 방식으로 작동합니다.
이로 인해 지연 시간이 낮고, 거리 확장이 가능하며, 실시간성이 중요한 드론 FPV 등에 적합합니다.

openHD를 사용하면서 H.264/H.265 등의 압축 방식을 사용할 수 있니?
네, OpenHD는 H.264/H.265 등의 압축 방식을 사용할 수 있습니다. 하지만 기본적으로 OpenHD는 무압축(또는 저압축) 비디오 전송을 지향하여 저지연(로우 레이턴시) 성능을 극대화합니다.

🔹 OpenHD에서 H.264/H.265 압축 사용 여부
기본 설정

OpenHD는 비디오 프레임을 압축 없이(또는 MJPEG 같은 가벼운 압축 방식으로) 전송하는 것이 기본입니다.

이는 저지연(50ms 이하)을 유지하기 위해서이며, FPV에서 실시간성이 중요하기 때문입니다.

H.264/H.265 사용 가능 여부

일부 사용자는 OpenHD에서 H.264/H.265를 적용하여 더 낮은 대역폭에서 전송할 수 있도록 설정하기도 합니다.

하지만 비디오 인코딩/디코딩 과정에서 추가적인 지연이 발생할 수 있습니다.

특히 H.265는 더 높은 압축률을 제공하지만, 인코딩 시간이 더 길어져 지연이 증가할 가능성이 큽니다.

사용 가능 사례

저대역폭 환경에서 H.264/H.265를 사용하면 더 먼 거리까지 전송 가능합니다.

하지만 **실시간 FPV 성능(저지연)**이 중요하다면, 무압축 또는 경량 압축(MJPEG 등)을 사용하는 것이 더 적합합니다.

✅ 결론
OpenHD는 기본적으로 무압축 또는 저압축 방식을 사용하지만, 필요하면 H.264/H.265를 적용할 수 있습니다.
그러나 지연 시간이 증가할 수 있으므로, FPV 환경에서는 신중하게 고려해야 합니다.
(특히, 하드웨어 가속 인코딩/디코딩 기능이 있는 GPU/FPGA 사용 시 지연을 줄일 수 있음).

옵션을 어떻게 설정해야  H.264/H.265 인코딩/디코딩을 사용할 수 있니?

OpenHD에서 H.264/H.265 인코딩/디코딩을 활성화하려면 몇 가지 설정을 변경해야 합니다. 기본적으로 OpenHD는 저지연 전송을 위해 무압축 또는 경량 압축을 사용하지만, 대역폭 절약과 장거리 전송을 위해 H.264/H.265 코덱을 활용할 수 있습니다.

🔹 1. H.264/H.265 인코딩 활성화
1) 라즈베리파이 (Raspberry Pi)
라즈베리파이에서는 GStreamer를 활용한 하드웨어 인코딩(H.264/H.265)을 활성화할 수 있습니다.

📌 설정 방법 (Raspberry Pi 카메라 사용 시)

config.txt 파일 수정 (/boot/config.txt)
start_x=1
gpu_mem=256
설명: GPU 메모리를 256MB 이상 할당하여 하드웨어 인코딩을 원활하게 수행.

OpenHD 설정 파일 (/etc/openhd/openhd.conf 또는 /boot/openhd_settings.txt)에서 인코딩 옵션 변경:
VIDEO_ENCODING=H264

GStreamer를 이용한 H.264 인코딩 명령어 예시 (Raspberry Pi Camera Module 사용 시)
raspivid -t 0 -w 1280 -h 720 -fps 30 -b 2000000 -o - | gst-launch-1.0 fdsrc ! h264parse ! rtph264pay config-interval=1 pt=96 ! udpsink host=192.168.0.1 port=5600


2) NVIDIA Jetson (하드웨어 가속)
NVIDIA Jetson 보드에서는 **GStreamer + NVENC (NVIDIA Encoder)**를 이용해 H.264/H.265 인코딩을 수행할 수 있습니다.

📌 설정 방법

OpenHD 설정 파일에서 H.264 활성화:
VIDEO_ENCODING=H264

GStreamer를 이용한 Jetson 하드웨어 인코딩 명령어 (H.264)
gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=1280, height=720, format=NV12, framerate=30/1' ! nvv4l2h264enc ! h264parse ! rtph264pay config-interval=1 pt=96 ! udpsink host=192.168.0.1 port=5600
nvarguscamerasrc → Jetson 카메라 입력

nvv4l2h264enc → NVIDIA 하드웨어 가속 H.264 인코더

H.265 인코딩을 사용하려면 nvv4l2h265enc로 변경:
gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=1280, height=720, format=NV12, framerate=30/1' ! nvv4l2h265enc ! h265parse ! rtph265pay config-interval=1 pt=96 ! udpsink host=192.168.0.1 port=5600



 2. H.264/H.265 디코딩 활성화
수신 측(드론 지상국)에서도 H.264/H.265 스트림을 디코딩해야 합니다.

📌 GStreamer를 이용한 H.264/H.265 디코딩 예시

H.264 디코딩
gst-launch-1.0 udpsrc port=5600 caps="application/x-rtp, media=(string)video, encoding-name=(string)H264" ! rtph264depay ! h264parse ! avdec_h264 ! videoconvert ! autovideosink


H.265 디코딩
gst-launch-1.0 udpsrc port=5600 caps="application/x-rtp, media=(string)video, encoding-name=(string)H265" ! rtph265depay ! h265parse ! avdec_h265 ! videoconvert ! autovideosink


✅ 결론
H.264/H.265 인코딩을 활성화하려면 OpenHD 설정 파일에서 VIDEO_ENCODING=H264 또는 VIDEO_ENCODING=H265로 변경.

라즈베리파이에서는 raspivid + GStreamer 조합 사용.

NVIDIA Jetson은 GStreamer + NVENC (하드웨어 가속) 활용 가능.

지상 수신기에서는 GStreamer를 이용한 디코딩 실행.

이 방식으로 OpenHD에서도 H.264/H.265 압축을 활용하여 더 긴 거리에서 안정적인 비디오 전송이 가능합니다. 🚀



















