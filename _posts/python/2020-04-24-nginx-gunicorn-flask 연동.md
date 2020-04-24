# git clone

# python 설정
```
//0. python3 version check
python3 --version

//1. venv 설치
sudo apt python3-venv
python3 -m venv [가상환경명]
source [가상환경경로]/bin/activate

//2. pip 설치(in venv)
sudo apt python3-pip

//3. requirements(in venv)
pip3 install -r [requirements.txt path]

//4. install cryptography 
```

# gunicorn 설정
### 1. gunicorn 설치(in venv)
```
pip3 install gunicorn
```

### 2. wsgi 생성
* app.py와 같은 directory/wsgi.py 생성
```
from app import app

if __name__ == '__main__':
    app.run()
```

### 3. service로 등록
* path : /etc/systemd/system/[서비스명.service]

```
[Unit]
Description=Run toy project with gunicorn
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=[project path : /home/ubuntu/project...]
Environment="PATH=[project path]"
ExecStart=[gunicorn path in venv] --bind unix:[프로젝트명].sock wsgi:app

[Install]
WantedBy=multi-user.target
```

### 4. 서비스 체크
```
systemctl start [서비스명]
systemctl status [서비스명]
systemctl daemon-reload
```

# nginx 설정
### 1. nginx 설치
```
sudo apt nginx
```

### 2. proxy 파일 설정
* path : /etc/nginx/sites-available/[파일명]
```
server {
        listen 80;
        server_name [domain or ip];

        location / {
                include proxy_params;
                proxy_pass http://[gunicorn - .sock file path];
        }
}
```

### 3. enable 에 링크 생성
```
ln -s [proxy config path] /etc/nginx/sites-enabled
```

### 4. service 테스트
```
nginx -t
sudo service nginx start
sudo service nginx status
```

### 5. service 등록
```
[Unit]
Description=Run NginX Proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

# test
* 변경사항 발생시 git pull & gunicorn만 재구동
