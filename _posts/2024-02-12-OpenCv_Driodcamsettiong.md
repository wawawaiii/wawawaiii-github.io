---
layout: post
title:  "Welcome to Jekyll!"
---


Python과 OpenCV를 활용한 웹캠 비디오 스트리밍
이 포스트에서는 Python과 OpenCV를 사용하여 웹캠에서 비디오 스트리밍을 가져오는 방법을 소개합니다.


import cv2

# 비디오 캡처 객체를 생성합니다. 
# 이 예제에서는 'http://192.168.45.192:4747/mjpegfeed' URL에서 MJPEG 비디오 스트림을 캡처합니다.
video = cv2.VideoCapture('http://192.168.45.192:4747/mjpegfeed')

# 비디오의 프레임 크기를 가져와서 `frame_size`에 저장합니다.
frame_size = (int(video.get(cv2.CAP_PROP_FRAME_WIDTH)), int(video.get(cv2.CAP_PROP_FRAME_HEIGHT)))

while True:
    # video.read() 함수는 비디오의 한 프레임을 읽어옵니다. 
    # ret는 프레임 읽기 성공 여부를 나타내고, frame은 읽어온 프레임의 데이터입니다.
    ret, frame = video.read()

    # 만약 프레임 읽기가 실패하면 (ret가 False라면) 루프를 종료합니다.
    if not ret:
        break

    # cv2.imshow() 함수로 프레임을 화면에 출력합니다.
    cv2.imshow('frame', frame)

    # cv2.waitKey(25)는 키보드 입력을 기다리는 함수입니다. 
    # 여기서는 25ms 동안 기다립니다. 'Esc' 키가 눌리면 (아스키 코드 27), 루프를 종료합니다.
    key = cv2.waitKey(25)
    if key == 27:
        break

# 만약 비디오 캡처 객체가 아직 열려있다면, video.release()를 통해 자원을 해제해줍니다.
if video.isOpened():
    video.release()

# 마지막으로 cv2.destroyAllWindows()를 통해 모든 OpenCV 윈도우를 닫습니다.
cv2.destroyAllWindows()
