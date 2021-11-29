# Docker
Docker Ubuntu18-Opencv4.2


in Raspberry Pi4 (armV7l_32bit) os use Docker .
this project for job use so if Encounter difficulties issue you can Ask 

-----
Remark 
Mainly use python3 、Opencv、Python3-dev、Python-numpy

------

Provide raspberry Pi image .but didn't havd CMD["/bin/bash"]
you should add "/bin/bash" in the docker build .

------

Add docker image of raspberry 32 (armv7l)


1.Raspberrypi4-opencv3.4.3-Auto   kneron 520


2.720Raspberrypi4-opencv3.4.3-Auto   kneron 720


-----
docker push tpeswumedia/ri_pi_520_64bit:tagname

latest 為初始版 僅有opencv 4.x  + python3.9
v2  則是 加入YoLov3 and Kneron 520 (old version)
v3  延續v2 做些調整修正刪除不需要的檔案


latest Note 需要下載Kneron 520 host_lib , 重新進行cmake && make -j 
先執行一次autoRun 即可看到error mesg 的路徑,將產生的src / libxxxx.so 複製貼上取代 即可
