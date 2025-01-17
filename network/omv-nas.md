NAS 설치하기


![ddd](https://user-images.githubusercontent.com/44438752/63148284-b1cb3980-c03b-11e9-93b6-3592c166ba2c.jpeg)

![d](https://user-images.githubusercontent.com/44438752/63148326-d0c9cb80-c03b-11e9-81e9-9f868d600383.jpeg)

login: root password:앞에서 설정한 비밀번호

root@아이디:~# 
화면이 뜰것임.
ip address 입력하여 ip주소 알아내기.

ip주소 접속.


<br/><br/>
## 1. 네트워크 설정
1-1. 고정ip 등록하기
![62423911-49f32580-b702-11e9-8fe9-08f8b220e481](https://user-images.githubusercontent.com/44438752/62628366-1f090b80-b966-11e9-8dc4-bb7cebbdf87f.png)

<br/><br/><br/><br/>

## 2. HDD 설정
2-1. 저장소 - 디스크 클릭,하드디스크 4개가 인식된걸 확인할 수 있음
<br/><br/>
![스크린샷 2019-08-07 오후 10 54 03](https://user-images.githubusercontent.com/44438752/62628442-4e1f7d00-b966-11e9-9534-4d5413b86163.png)

<br/><br/>
2-2. 파티션 생성을 위해 저장소 -파일시스템 클릭. 마운트 시키기. 혹 생성이 되어 있지 않으면 생성 버튼을 눌러 장치와 레이블(별명), 파일시스템은 ext4로 설정

![스크린샷 2019-08-04 오후 9 52 11](https://user-images.githubusercontent.com/44438752/62423946-d0a80280-b702-11e9-99cf-14696d7a914f.png)

<br/><br/><br/><br/>

## 3. 사용자 생성

3-1. 그룹에 ssh 추가
![스크린샷 2019-08-04 오후 10 04 36](https://user-images.githubusercontent.com/44438752/62424058-7e67e100-b704-11e9-905c-5f8689216458.png)\

<br/><br/>
3-2. 위치 지정
![스크린샷 2019-08-04 오후 10 06 32](https://user-images.githubusercontent.com/44438752/62424064-8758b280-b704-11e9-9780-6bac0d394f32.png)

<br/><br/>
3-3. 상대경로도 설정(seongsil/)
![스크린샷 2019-08-04 오후 10 06 32](https://user-images.githubusercontent.com/44438752/62618884-553b9080-b950-11e9-8f3f-b536a80417f8.png)


<br/><br/>
3-4. 공유폴더 권한 설정
![스크린샷 2019-08-04 오후 10 07 11](https://user-images.githubusercontent.com/44438752/62424075-ac4d2580-b704-11e9-93fc-25784a9d572b.png)


<br/><br/><br/><br/>

## 4. ssh 설정 (ftp 설정도 마찬가지)
4-1. 포트번호 설정 및 활성화시키기
![62424153-c63b3800-b705-11e9-8d7b-7a1152292621](https://user-images.githubusercontent.com/44438752/62628653-a5bde880-b966-11e9-9249-bba3c1fb3daa.png)

<br/><br/>
4-2. 클라이언트 접속
sftp -oPort=<포트번호> <아이디>@<ip주소>
<br/>
![hy](https://user-images.githubusercontent.com/44438752/62629256-cc305380-b967-11e9-89b0-0b33d0bba92c.png)



## 6. Ubuntu Linux Samba 공유 폴더 Mount 하기 
6-1. smb 활성화
![스크린샷 2019-08-04 오후 10 17 06](https://user-images.githubusercontent.com/44438752/62620499-6e464080-b954-11e9-94fc-685fc349084c.png)

<br/><br/>
6-2. 공유 폴더 설정
![스크린샷 2019-08-04 오후 10 17 06](https://user-images.githubusercontent.com/44438752/62620486-6ab2b980-b954-11e9-9b6d-826fb7086e1f.png)

<br/><br/>
6-3. 클라이언트 환경에서 samba설치 안되 있을 경우, sudo apt-get install samba-common
![Screenshot from 2019-08-07 21-06-37](https://user-images.githubusercontent.com/44438752/62622674-dea39080-b959-11e9-9b51-b15adb1c591c.png)

6-4. 삼바 서버 확인 smbclient -L <ip주소>
<br/>
![62623249-5d4cfd80-b95b-11e9-80c8-bf221986423b (1)](https://user-images.githubusercontent.com/44438752/62628787-f0d7fb80-b966-11e9-8fda-d3b7b1906478.png)

smbclient 

<br/><br/>

6-4. 클라이언트 환경에 폴더 생성
vi seongsil

<br/><br/>
![aa](https://user-images.githubusercontent.com/44438752/62623485-ec5a1580-b95b-11e9-8ee9-31c8285cbaba.png)
6-5. 마운트 하기
sudo mount -t cifs -o username='사용자이름',password='패스워드' //서버주소/공유폴더 마운트경로  (파일의 권한 설정을 위해서는 다음과  옵션을  추가하면 됨.uid=seongsil,gid=master,file_mode=0775,dir_mode=0775)

![dde](https://user-images.githubusercontent.com/44438752/62629107-85425e00-b967-11e9-86d2-8b12259d0e4d.png)
<br/><br/>

6-6. 마운트 잘 되었는지 확인

![aa](https://user-images.githubusercontent.com/44438752/62629144-94291080-b967-11e9-8102-2fe968f09885.png)

6-7. 마운트 고정시키기 위해서는,

    sudo nano /etc/fstab

에서 다음을 추가

    //[ip주소]/마운트 시킬omv의 폴더 경로  /mount point file type
    //192.168.0.1/master  /mnt/master-file cifs username=mifile,password=12345,uid=seongsil,gid=master,file_mode=0775,dir_mode=0775 0 0

 
 sudo mount -al
 했을 때 오류 없다면 reboot해서도 제대로 마운트 될것임.
 
 df  -h  명령어로 mount된  
