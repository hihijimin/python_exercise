## 아나콘다3 설치(pythhon= 3.6)
참고사이트
https://blog.naver.com/PostView.nhn?blogId=jihu02&logNo=221447248039&from=search&redirect=Log&widgetTypeCall=true&directAccess=false  
아나콘다 다운로드 사이트: https://www.anaconda.com/products/individual  

- 아나콘다 다운로드 후, 설치 실행!
Select installation Type(Just Me(recommended))선택 -> 설칫할 경로는 원하는 경로에! -> Advanced installation Options(Register Anaconda as my default Python 3.7) 선택  

- 설치된 앱 중에서 anaconda prompt 에 들어가서 $ conda install python=3.6 이라 작성한다(python =3.6 설치하기 위해)  
![image](https://user-images.githubusercontent.com/56099627/82296200-cf269d00-99eb-11ea-8d73-32561c5f0ea8.png)  
![image](https://user-images.githubusercontent.com/56099627/82296311-f8dfc400-99eb-11ea-90fe-862479eae4d0.png)  

## opencv 설치
$ pip install opencv-contrib-python  
![image](https://user-images.githubusercontent.com/56099627/82297623-e1a1d600-99ed-11ea-9622-8ce7ad6e490a.png)  

## anaconda 가상환경 만들기
$ conda create -n hrnet_pose python=3.6  
![image](https://user-images.githubusercontent.com/56099627/82298695-778a3080-99ef-11ea-8c0e-5b2019201527.png)  
![image](https://user-images.githubusercontent.com/56099627/82298772-938dd200-99ef-11ea-835e-093d80090346.png)  

## cuda 설치
nvidia 사이트 가서 cuda 9.0 파일 다운로드 하기(링크 없음)  
![image](https://user-images.githubusercontent.com/56099627/82300488-e2d50200-99f1-11ea-9ae5-c18a0f5d5e39.png)  
(참고: 경로를 D 드라이브로 설정해서 설치해도 C 드라이브에 설치 됌)  
+ cudnn 다운로드  
CUDNN 다운로드 사이트: https://developer.nvidia.com/rdp/cudnn-download  
![image](https://user-images.githubusercontent.com/56099627/82305664-e455f880-99f8-11ea-8515-aea2e217f4d3.png)  
- 경로" C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0 " 에 cudnn 다운로드 받은것을 덮어쓰기 해준다.  


