# CLOAK OF INVISIBILITY

```python
import numpy as np
import cv2 
import time

```


```python
cap=cv2.VideoCapture(0)

time.sleep(3)

background=0

for i in range(1,30):
    ret,background=cap.read()

background=np.flip(background,axis=1)


while(cap.isOpened()):
    ret,frame=cap.read()
    
    frame=np.flip(frame,axis=1)
    
    hsv=cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
    
    lower_red = np.array([0,120,70])
    upper_red = np.array([10,255,255])

    mask1 = cv2.inRange(hsv, lower_red, upper_red) 
      
    lower_red = np.array([170,120,70])
    upper_red = np.array([180,255,255])

    mask2 = cv2.inRange(hsv, lower_red, upper_red) 
    
    
    mask1=mask1+mask2
    
    
    mask1=cv2.morphologyEx(mask1,cv2.MORPH_OPEN,np.ones((3,3),np.uint8),iterations=3)
    mask1=cv2.morphologyEx(mask1,cv2.MORPH_DILATE,np.ones((3,3),np.uint8),iterations=3)
    
    
    mask2=cv2.bitwise_not(mask1)
    
    res1=cv2.bitwise_and(frame,frame,mask=mask2)
    
    res2=cv2.bitwise_and(background,background,mask=mask1)
    
    final_res=cv2.addWeighted(res1,1,res2,1,0)
    
    cv2.imshow("CLOAK OF INVISIBILITY  :)", final_res) 
    
    if cv2.waitKey(20) & 0xFF == ord('q'):
            
            break
    
cap.release()

cv2.destroyAllWindows()
```


```python

```



# FINAL RESULT
(click on the picture below)</br>
<a href="https://drive.google.com/file/d/16MtdguJuNogReNHb_p-D_A3sWHAwF5Hu/view?usp=sharing" target="_blank"><img src="DATA\images.jpg" 
alt="IMAGE ALT TEXT HERE" width="400" height="300" border="5" /></a>