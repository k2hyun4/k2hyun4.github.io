## 설치
```bash
sudo curl -OL https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb
sudo apt update
sudo apt install mysql-server
```
- deb : debian 패키지라는 뜻
### dpkg
- deb package
- -P : 패키지 제거
- -i : install
- -l : list
- -S : 파일의 패키지명 알아내기
