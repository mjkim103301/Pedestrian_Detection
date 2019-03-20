# Pedestrian_Detection_with_python3
import numpy as np
import cv2

def draw_detections(img, rects, thickness=1):
 for x,y, w, h in rects:
  pad_w, pad_h= int(0.15*w), int(0.05*h)
  cv2.rectangle(img, (x+pad_w, y+pad_h), (x+w-pad_w, y+h-pad_h), (0, 255, 0), thickness)

if __name__ == '__main__':

 hog=cv2.HOGDescriptor()
 hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())
 cap=cv2.VideoCapture('/home/pi/Downloads/pede.mp4') 

 while True:
   _, frame=cap.read()
   minisize=(int(frame.shape[1]/1.5), int(frame.shape[0]/1.5))
   miniframe=cv2.resize(frame, minisize)
   found,w=hog.detectMultiScale(miniframe, winStride=(8, 8), padding=(32, 32), scale=1.05)
   draw_detections(miniframe, found)
   cv2.imshow('feed', miniframe)

   if cv2.waitKey(1) & 0xff == ord('q'):
    break

 cv2.destroyAllWindows()


#"https://www.youtube.com/watch?v=1DE-8MIUFWM"에서 결과 영상을 확인하실 수 있습니다.
