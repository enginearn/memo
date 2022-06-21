# 雑多なメモたち

## WSL2

<details>
<summary>WSL2のDistributionへアクセス</summary>

``` PowerShell
wsl --list
Linux 用 Windows サブシステム ディストリビューション:
Ubuntu (既定)
docker-desktop-data
Ubuntu-22.04
docker-desktop
wsl -d Ubuntu-22.04 -u root
Welcome to Ubuntu 22.04 LTS (GNU/Linux 5.10.102.1-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed May 25 05:59:04 AM JST 2022

  System load:  0.0                Processes:             12
  Usage of /:   0.6% of 250.98GB   Users logged in:       0
  Memory usage: 12%                IPv4 address for eth0: xxx.xxx.xxx.xxx
  Swap usage:   0%

0 updates can be applied immediately.



This message is shown once a day. To disable it please create the
/root/.hushlogin file.
root@GPD-P2-Max:/mnt/c/Users/username#
```

</details>

<details>
<summary>WSL2のカレントフォルダをマウント元のフォルダで開く</summary>

``` WLS2 ubuntu 22.04
$ explorer.exe .
```

</details>


<details>
<summary>WLS2のubuntuでpip3でインストールしたパッケージの追加</summary>

``` WLS ubuntu 22.04
$ python3 requests_header_encoding.py https://gihyo.jp/dp
^C # ここでCtrl + C
Traceback (most recent call last):
  File "/home/path/requests_header_encoding.py", line 5, in <module>
    r = requests.get(url)
  File "/usr/lib/python3/dist-packages/requests/api.py", line 76, in get
    return request('get', url, params=params, **kwargs)
  File "/usr/lib/python3/dist-packages/requests/api.py", line 61, in request
    return session.request(method=method, url=url, **kwargs)
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 542, in request
    resp = self.send(prep, **send_kwargs)
  File "/usr/lib/python3/dist-packages/requests/sessions.py", line 655, in send
    r = adapter.send(request, **kwargs)
  File "/usr/lib/python3/dist-packages/requests/adapters.py", line 439, in send
    resp = conn.urlopen(
  File "/usr/lib/python3/dist-packages/urllib3/connectionpool.py", line 699, in urlopen
    httplib_response = self._make_request(
  File "/usr/lib/python3/dist-packages/urllib3/connectionpool.py", line 382, in _make_request
    self._validate_conn(conn)
  File "/usr/lib/python3/dist-packages/urllib3/connectionpool.py", line 1012, in _validate_conn
    conn.connect()
  File "/usr/lib/python3/dist-packages/urllib3/connection.py", line 353, in connect
    conn = self._new_conn()
  File "/usr/lib/python3/dist-packages/urllib3/connection.py", line 169, in _new_conn
    conn = connection.create_connection(
  File "/usr/lib/python3/dist-packages/urllib3/util/connection.py", line 86, in create_connection
    sock.connect(sa)
KeyboardInterrupt
$ pip3 list
Package                Version
---------------------- -------------
requests               2.25.1
urllib3                1.26.5
```

requestsのインストール先を確認

``` WSL2 ubuntu22.04
$ pip3 show requests
Name: requests
Version: 2.25.1
Summary: Python HTTP for Humans.
Home-page: https://requests.readthedocs.io
Author: Kenneth Reitz
Author-email: me@kennethreitz.org
License: Apache 2.0
Location: /usr/lib/python3/dist-packages
Requires:

Required-by:
```
packageのインストール先を確認

``` WSL2 ubuntu22.04
$ python3 -c "import sys, pprint; pprint.pprint(sys.path)"
['',
 '/usr/lib/python310.zip',
 '/usr/lib/python3.10',
 '/usr/lib/python3.10/lib-dynload',
 '/usr/local/lib/python3.10/dist-packages',
 '/usr/lib/python3/dist-packages']
```

念のため、もう1回追加

``` WSL2 ubuntu22.04
$ python3 -c 'sys.path.append("/usr/lib/python3/dist-packages")'
```

</details>

## SSH

<details>
<summary>ssh-agentを自動起動</summary>

``` Powershell
# PowerShellをAdminDEで起動
Set-Service ssh-agent -StartType Automatic
Start-Service ssh-agent
Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent
```

</details>

## ssh-keygen

<details>
<summary>秘密鍵と公開鍵の作成</summary>

``` PowerShell
mkdir $HOME/.ssh && cd $HOME/.ssh
ssh-keygen -t ed25519 -f github_LENOVO13 -C "yourmail@address.com"
Directory: C:\Users\pathto\.ssh

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---          2022/06/19    11:05            124 config
-a---          2022/06/19    10:42            419 github_LENOVO13
-a---          2022/06/19    10:42            105 github_LENOVO13.pub
```

</details>

## PowerShell

<details>
<summary>Invoke-WebRequestを使う</summary>

``` PowerShell
Invoke-WebRequest -Uri https://ferret-plus.com/4637

StatusCode        : 200
StatusDescription : OK
Content           : <!DOCTYPE html><html lang="ja"><head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb#"><script src="https://securepubads.g.doubleclick.net/tag/js/gpt.js"></script><link crossorigin="" href="//fo…
RawContent        : HTTP/1.1 200 OK
                    Date: Sat, 21 May 2022 12:00:36 GMT
                    Transfer-Encoding: chunked
                    Connection: keep-alive
                    Server: nginx
                    X-Frame-Options: SAMEORIGIN
                    X-XSS-Protection: 1; mode=block
                    X-Content-Type-Op…
Headers           : {[Date, System.String[]], [Transfer-Encoding, System.String[]], [Connection, System.String[]], [Server, System.String[]]…}
Images            : {@{outerHTML=<img loading="lazy" alt="「URIとは？「URL」と「URI」の違いを解説！」の見出し画像" width="800" height="600" src="https://ferret.akamaized.net/uploads/article/4637/eyecatch/default-d51f6b54f653accfe5bf19d2d2d75fb7.jpg" />; tagName=IMG; loading=lazy; alt=「URI 
                    とは？「URL」と「URI」の違いを解説！」の見出し画像; width=800; height=600; src=https://ferret.akamaized.net/uploads/article/4637/eyecatch/default-d51f6b54f653accfe5bf19d2d2d75fb7.jpg}, @{outerHTML=<img src="https://ferret.akamaized.net/images/579073cb69702d514a0a0000/la 
                    rge.jpeg?1469084618" alt="Untitled(3)_(3).png">; tagName=IMG; src=https://ferret.akamaized.net/images/579073cb69702d514a0a0000/large.jpeg?1469084618; alt=Untitled(3)_(3).png}, @{outerHTML=<img class="article-eyecatch" loading="lazy" alt="「市場調査の方法は？3つの手法と  
                    具体的なレポート事例を解説」の見出し画像" width="400" height="300" src="https://ferret.akamaized.net/uploads/article/63461/eyecatch/default-3501af993cf2c87dcd0b5a3ccd2b460d.jpg" />; tagName=IMG; class=article-eyecatch; loading=lazy; alt=「市場調査の方法は？3つの手法と具 
                    体的なレポート事例を解説」の見出し画像; width=400; height=300; src=https://ferret.akamaized.net/uploads/article/63461/eyecatch/default-3501af993cf2c87dcd0b5a3ccd2b460d.jpg}, @{outerHTML=<img class="article-eyecatch" loading="lazy" alt="「顧客管理のやり方間違ってませんか 
                    ？リアル店舗とECにおけるデータ管理の課題と“心地良い購買体験”とは
                    」の見出し画像" width="400" height="300" src="https://ferret.akamaized.net/uploads/article/64210/eyecatch/default-e4f3c25863ba596dbd23c1b9d4e6702c.jpg" />; tagName=IMG; class=article-eyecatch; loading=lazy; alt=「顧客管理のやり方間違ってませんか？リアル店舗とECにおける  
                    データ管理の課題と“心地良い購買体験”とは
                    」の見出し画像; width=400; height=300; src=https://ferret.akamaized.net/uploads/article/64210/eyecatch/default-e4f3c25863ba596dbd23c1b9d4e6702c.jpg}…}
InputFields       : {@{outerHTML=<input class="q-text-field js-search-form-input" required="required" placeholder="キーワードで記事を検索" type="text" name="q" id="q" />; tagName=INPUT; class=q-text-field js-search-form-input; required=required; placeholder=キーワードで記事を検索; type=tex 
                    t; name=q; id=q}}
Links             : {@{outerHTML=<a class="ferret-root-link" href="/"><svg class="ferret-icon"><use xlink:href="https://ferret-plus.com/assets/icons-501a8b6f6002f26fac774ba463aa6c7f39c2cb481106f85e62da592cf4b172ad.svg#ferret"></use></svg></a>; tagName=A; class=ferret-root-link; href=/}, @{ 
                    outerHTML=<a class="main-link is-current" href="/articles">記事</a>; tagName=A; class=main-link is-current; href=/articles}, @{outerHTML=<a class="main-link " href="/useful-items">お役立ち資料</a>; tagName=A; class=main-link ; href=/useful-items}, @{outerHTML=<a class=" 
                    main-link " href="/tools">ツール</a>; tagName=A; class=main-link ; href=/tools}…}
RawContentLength  : 89148
RelationLink      : {}
```

``` PowerShell
Invoke-WebRequest -Uri https://gihyo.jp/feed/rss2 | Out-File rss2.xml
```

[Invoke-WebRequest](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.2)

</details>

<details>
<summary>Hyper-VのON / OFF</summary>

``` PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All

Enable-VMEventing
Disable-VMEventing
```

</details>

<details>
<summary>システム環境変数を編集</summary>

``` PowerShell
# adminでPowerShellを実行
Start C:\Windows\system32\rundll32.exe sysdm.cpl, EditEnvironmentVariables
```

</details>

``` Python 3.10
py -3.10 -m pip install -U pip
```

``` Python 3.10
py -3.10 -m venv venv
```

``` ubuntu
$ localectl list-locales
C.UTF-8
en_US.UTF-8
```

``` ubuntu
$ sudo apt install -y language-pack-ja
$
```

``` ubuntu
$ localectl list-locales
C.UTF-8
en_US.UTF-8
ja_JP.UTF-8
```

``` ubuntu
$ sudo localectl set-locale LANG=ja_JP.UTF-8
$ sudo reboot
$
```

``` vagrant
$ vagrant up --debug 2>&1 | Tee-Object -FilePath ".\vagrant.log"
$
```

`docker run -dp 8000:8000 getting-started`
Remember the `-d` and `-p` flags? We’re running the new container in “detached” mode (in the background) and
creating a mapping between the host’s port 3000 to the container’s port 3000.
Without the port mapping, we wouldn’t be able to access the application.

``` docker
$ docker rmi <IMAGE ID>
<IMAGE ID>
```

``` docker
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED              STATUS              PORTS                            NAMES
e1d3b34e572c   docker/getting-started   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:3000->3000/tcp   heuristic_hypatia
```

``` docker
$ docker run -d --name ubuntu-latest ubuntu:latest
$ docker run --name ubuntu-latest ubuntu "/bin/bash"
$ docker run -it -d --name ubuntu-latest ubuntu
$ docker run -it -d -u sudo_user --name ubuntu-latest-jp ubuntu-latest-jp
$ docker run -it -d --name ubuntu-latest ubuntu "/bin/bash"
$
```

``` docker
docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]
$ docker container exec -it ubuntu-latest bash
$ docker container exec -it ubuntu-latest-jp bash
$ docker container exec -it hopeful_solomon sh
$
```

## Exitedしたコンテナへアクセスする

``` docker
$ docker commit [CONTAINER ID] <temporary_contenaier_name>
$ docker commit 1e18025e3b50 check
$docker run --rm -it check sh
# アクセスできてる
# pwd
/
# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
# exit
$
```

``` Dockerfile
apt-get update && apt-get upgrade -y && \
apt-get install -y sudo vim

USERNAME=sudo_user
GROUPNAME=sudo_user
uid=1000
GID=1000
PASSWRD=sudo_user
groupadd -g $GID $GROUPNAME && \
useradd -m -s /bin/bash -u $uid -g $GID -G sudo $USERNAME && \
echo $USERNAME:$PASSWRD | chpasswd && \
echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
su sudo_user && cd $HOME
```

~~sudo apt-get install -y language-pack-ja-base language-pack-ja~~

``` ubuntu
$ sudo locale-gen ja_JP.UTF-8
Generating locales (this might take a while)...
  ja_JP.UTF-8... done
Generation complete.

$ echo export LANG=ja_JP.UTF-8 >> ~/.bashrc
$ source ~/.bashrc
$
```

``` ubuntu
$ sudo apt-get install -y tzdata
Please select the geographic area in which you live. Subsequent configuration questions will narrow this down by presenting a list of cities, representing the time zones in which they are located.

  1. Africa  2. America  3. Antarctica  4. Australia  5. Arctic  6. Asia  7. Atlantic  8. Europe  9. Indian  10. Pacific  11. US  12. Etc
Geographic area: 6

Please select the city or region corresponding to your time zone.

  1. Aden    7. Ashgabat  13. Barnaul     19. Chongqing  25. Dushanbe     31. Hong_Kong  37. Jerusalem  43. Khandyga      49. Macau     55. Novokuznetsk  61. Pyongyang  67. Sakhalin       73. Taipei    79. Tokyo          85. Vientiane
  2. Almaty  8. Atyrau    14. Beirut      20. Colombo    26. Famagusta    32. Hovd       38. Kabul      44. Kolkata       50. Magadan   56. Novosibirsk   62. Qatar      68. Samarkand      74. Tashkent  80. Tomsk          86. Vladivostok
  3. Amman   9. Baghdad   15. Bishkek     21. Damascus   27. Gaza         33. Irkutsk    39. Kamchatka  45. Krasnoyarsk   51. Makassar  57. Omsk          63. Qostanay   69. Seoul          75. Tbilisi   81. Ujung_Pandang  87. Yakutsk
  4. Anadyr  10. Bahrain  16. Brunei      22. Dhaka      28. Harbin       34. Istanbul   40. Karachi    46. Kuala_Lumpur  52. Manila    58. Oral          64. Qyzylorda  70. Shanghai       76. Tehran    82. Ulaanbaatar    88. Yangon
  5. Aqtau   11. Baku     17. Chita       23. Dili       29. Hebron       35. Jakarta    41. Kashgar    47. Kuching       53. Muscat    59. Phnom_Penh    65. Rangoon    71. Singapore      77. Tel_Aviv  83. Urumqi         89. Yekaterinburg
  6. Aqtobe  12. Bangkok  18. Choibalsan  24. Dubai      30. Ho_Chi_Minh  36. Jayapura   42. Kathmandu  48. Kuwait        54. Nicosia   60. Pontianak     66. Riyadh     72. Srednekolymsk  78. Thimphu   84. Ust-Nera       90. Yerevan
Time zone: 79


Current default time zone: 'Asia/Tokyo'
Local time is now:      Sat May 14 11:45:09 JST 2022.
Universal Time is now:  Sat May 14 02:45:09 UTC 2022.
Run 'dpkg-reconfigure tzdata' if you wish to change it.
```

``` ubuntu
# id
uid=0(root) gid=0(root) groups=0(root)
```

``` docker
docker container commit [IMAGE ID] <user_name>/<repository>[:tag]
$ docker container commit a7310aa433f7 enginearn/ubuntu-latest-jp
```

``` docker
docker push enginearn/ubuntu-latest-jp
```

``` docker
$ docker volume create todo-db
$
```

``` docker
$ docker run -dp 3000:3000 -v todo-db:/etc/todos getting-started
$
```

``` docker
$ docker volume inspect todo-db
[
    {
        "CreatedAt": "2022-05-14T08:17:10Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

``` docker
docker run -dp 3000:3000 `
    -w /app -v "$(pwd):/app" `
    node:12-alpine `
    sh -c "yarn install && yarn run dev"
```

```  docker
docker run -d `
    --network todo-app --network-alias mysql --platform linux/amd64 `
    -v todo-mysql-data:/var/lib/mysql `
    -e MYSQL_ROOT_PASSWORD=secret `
    -e MYSQL_DATABASE=todos `
    mysql:latest
```

``` docker
docker exec -it <mysql-container-id> mysql -p
$ docker exec -it b570b2230839 mysql -p
password:
mysql
```

``` docker
$ docker run -it --network todo-app nicolaka/netshoot

466e743f1fdd  ~  dig mysql

; <<>> DiG 9.16.27 <<>> mysql
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16965
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;mysql.                         IN      A

;; ANSWER SECTION:
mysql.                  600     IN      A       172.19.0.2

;; Query time: 10 msec
;; SERVER: 127.0.0.11#53(127.0.0.11)
;; WHEN: Sat May 14 09:14:11 UTC 2022
;; MSG SIZE  rcvd: 44
```

``` docker
docker run -dp 3000:3000 `
  -w /app -v "$(pwd):/app" `
  --network todo-app `
  -e MYSQL_HOST=mysql `
  -e MYSQL_USER=root `
  -e MYSQL_PASSWORD=secret `
  -e MYSQL_DB=todos `
  node:12-alpine `
  sh -c "yarn install && yarn run dev"
```

``` MySQL
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'secret';
```

``` docker
$ docker container exec -it --user sudo_user fe2dce8820eb "bash"
$
```

## docker/getting-tutorial

``` docker
$ docker run -d -p 80:80 --name docker-getting-started docker/getting-started
$
```

``` docker
$ docker build -t getting-started .
$
```

``` docker
$ docker run -dp 3000:3000 --name todo-app getting-started
$
```

``` docker
$ docker rm -f <CONTAINER ID>
$
```

``` docker
$ docker build -t getting-started .
$
```

``` docker
$ docker run -dp 3000:3000 --name todo-app getting-started
$
```

``` docker
$ docker push enginearn/getting-started:getting-started
$
```

``` docker
$ docker volume ls
DRIVER    VOLUME NAME
local     1ef33fc54d258d8d2e46004f5cae87889a7da156f2dfee87dba0e2a1a5def88b
local     5d402387cfafb4f29368aadf2dec16cdbd2218c3ce63f620f22235096a4b5336
local     todo-db
local     todo-mysql-data
```

``` docker
$ docker volume inspect todo-mysql-data
$
```

``` docker
$ docker vomule rm <VOLUME NAME>
$
```

``` docker
$ docker volume --help

Usage:  docker volume COMMAND

Manage volumes

Commands:
  create      Create a volume
  inspect     Display detailed information on one or more volumes
  ls          List volumes
  prune       Remove all unused local volumes
  rm          Remove one or more volumes

Run 'docker volume COMMAND --help' for more information on a command.
```

``` docker
$ docker volume prune  
WARNING! This will remove all local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Volumes:
5d402387cfafb4f29368aadf2dec16cdbd2218c3ce63f620f22235096a4b5336
todo-db
todo-mysql-data

Total reclaimed space: 215.5MB
```

``` docker
$ docker volume create todo-db
$
```

``` docker
$ docker rm -f <CONTAINER ID>
$
```

``` docker
$ docker run -dp 3000:3000 -v todo-db:/etc/todos --name todo-app getting-started
$
```

``` docker
$ docker volume inspect todo-db
[
    {
        "CreatedAt": "2022-05-15T00:59:24Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/todo-db/_data",
        "Name": "todo-db",
        "Options": {},
        "Scope": "local"
    }
]
```

``` docker
$ docker stop <CONTAINER ID>
$
```

``` docker
$ docker run -dp 3000:3000 `
    -w /app -v "$(pwd):/app" `
    --name todo-app `
    --platform "linux/amd64" `
    node:12-alpine `
    sh -c "yarn install && yarn run dev"
```

``` docker
$ docker network create todo-app
Error response from daemon: network with name todo-app already exists
```

``` docker
$ docker network inspect todo-app
[
    {
        "Name": "todo-app",
        "Id": "c028b4d8e7adc3995056ce7044c349c006580a28a0bcca16307d48419c81772d",
        "Created": "2022-05-14T09:00:13.8373871Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
```

``` docker
$ docker network --help

Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks

Run 'docker network COMMAND --help' for more information on a command.
```

``` docker
$ docker network prune
WARNING! This will remove all custom networks not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Networks:
getting-started_default
todo-app
```

``` docker
$ docker network create network-todo-app
$
```

``` docker
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. 
All files and directories added to build context will have '-rwxr-xr-x' permissions.
It is recommended to double check and reset permissions for sensitive files and directories.
```

``` docker
$ docker logs <CONTAINER ID>
yarn install v1.22.18
[1/4] Resolving packages...
warning Resolution field "ansi-regex@5.0.1" is incompatible with requested version "ansi-regex@^2.0.0"
warning Resolution field "ansi-regex@5.0.1" is incompatible with requested version "ansi-regex@^3.0.0"
[2/4] Fetching packages...
[3/4] Linking dependencies...
```

``` docker
$ docker run -dp 3000:3000 `
    -w /app -v "$(pwd):/app" `
    --name todo-app `
    --platform "linux/amd64" ` # platformを追加
    node:12-alpine `
    sh -c "yarn install && yarn run dev"
```

``` docker
$ docker run -dp 3000:3000 -v todo-db:/etc/todos --name todo-app getting-started
$
```

``` docker
$ docker run -d `
    --name mysql-todo-app `
    --network network-todo-app `
    --network-alias mysql `
    --platform linux/amd64 `
    -v todo-mysql-data:/var/lib/mysql `
    -e MYSQL_ROOT_PASSWORD=secret `
    -e MYSQL_DATABASE=todos `
    mysql:latest
```

``` docker
$ docker exec -it <mysql-container-id> mysql -p
$
```

``` docker
$ docker run -it --network network-todo-app nicolaka/netshoot
$
```

``` docker
$ dig mysql
$
```

``` docker
$ docker run -dp 3000:3000 `
   -w /app -v "$(pwd):/app" `
   --name todo-app `
   --platform "linux/amd64" `
   --network network-todo-app `
   -e MYSQL_HOST=mysql `
   -e MYSQL_USER=root `
   -e MYSQL_PASSWORD=secret `
   -e MYSQL_DB=todos `
   node:12-alpine `
  sh -c "yarn install && yarn run dev"
```

## MySQL8の日本語対応

``` MySQL
SET character_set_client = utf8mb4;
SET character_set_results = utf8mb4;
SET character_set_connection = utf8mb4;
```

``` MySQL
SET CHARACTER SET 'charset_name'
SET CHARACTER SET 'utf8mb4'
```

``` MySQL
SET character_set_client = utf8mb4;
SET character_set_results = utf8mb4;
SET collation_connection = @@collation_database;
```

## GCPのWordPressアップグレード

<details>
<summary>MySQL5.7 -> MySQL8.0</summary>

``` bash
$ mysql --version
mysql  Ver 14.14 Distrib 5.7.38, for Linux (x86_64) using  EditLine wrapper

$ wget https://repo.mysql.com/mysql-apt-config_0.8.22-1_all.deb
--2022-06-09 22:00:39--  https://repo.mysql.com//mysql-apt-config_0.8.22-1_all.deb
Resolving repo.mysql.com (repo.mysql.com)... 23.40.193.17
Connecting to repo.mysql.com (repo.mysql.com)|23.40.193.17|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18012 (18K) [application/x-debian-package]
Saving to: ‘mysql-apt-config_0.8.22-1_all.deb’

mysql-apt-config_0.8.22-1_a 100%[========================================>]  17.59K  --.-KB/s    in 0s      

2022-06-09 22:00:39 (128 MB/s) - ‘mysql-apt-config_0.8.22-1_all.deb’ saved [18012/18012]

$ sudo dpkg -i mysql-apt-config_0.8.22-1_all.deb
(Reading database ... 75925 files and directories currently installed.)
Preparing to unpack mysql-apt-config_0.8.22-1_all.deb ...
Unpacking mysql-apt-config (0.8.22-1) over (0.8.22-1) ...
Setting up mysql-apt-config (0.8.22-1) ...
Warning: apt-key should not be used in scripts (called from postinst maintainerscript of the package mysql-apt-config)
OK

$ sudo apt update && sudo apt upgrade -y
Configuration file '/etc/mysql/mysql.conf.d/mysqld.cnf'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** mysqld.cnf (Y/I/N/O/D/Z) [default=N] ? Y
Installing new version of config file /etc/mysql/mysql.conf.d/mysqld.cnf ...
Setting up mysql-server (8.0.29-1debian10) ...
Processing triggers for man-db (2.8.5-2) ...
Processing triggers for libc-bin (2.28-10+deb10u1) ...

$ mysql --version
mysql  Ver 8.0.29 for Linux on x86_64 (MySQL Community Server - GPL)

$ sudo systemctl restart apache2
```
</details>

<details>
<summary>Install phpMyAdmin</summary>

``` bash
$ sudo apt install phpmyadmin
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 phpmyadmin : Depends: php-twig (> 2.9) but 2.6.2-2 is to be installed
              Recommends: php-bz2
              Recommends: php-tcpdf but it is not going to be installed
              Recommends: php-zip
E: Unable to correct problems, you have held broken packages.

$ sudo apt upgrade phpmyadmin
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 phpmyadmin : Depends: dbconfig-mysql but it is not going to be installed or
                       dbconfig-no-thanks but it is not going to be installed or
                       dbconfig-common (< 2.0.0) but it is not going to be installed
              Depends: libjs-bootstrap4 but it is not going to be installed
              Depends: libjs-codemirror but it is not going to be installed
              Depends: libjs-jquery but it is not going to be installed
              Depends: libjs-jquery-mousewheel but it is not going to be installed
              Depends: libjs-jquery-timepicker but it is not going to be installed
              Depends: libjs-jquery-ui but it is not going to be installed
              Depends: libjs-openlayers but it is not going to be installed
              Depends: php-mysql
              Depends: php-google-recaptcha (>= 1.1) but it is not going to be installed
              Depends: php-google-recaptcha (< 2~~) but it is not going to be installed
              Depends: php-phpmyadmin-motranslator (< 6~~) but it is not going to be installed
              Depends: php-phpmyadmin-shapefile (>= 2.0) but it is not going to be installed
              Depends: php-phpmyadmin-shapefile (< 3~~) but it is not going to be installed
              Depends: php-phpmyadmin-sql-parser (>= 5.0) but it is not going to be installed
              Depends: php-phpmyadmin-sql-parser (< 6~~) but it is not going to be installed
              Depends: php-twig-i18n-extension but it is not going to be installed
              Depends: php-phpseclib (>= 2.0)
              Depends: php-phpseclib (< 3~~)
              Depends: php-symfony-config (< 5~~) but it is not going to be installed
              Depends: php-symfony-dependency-injection (< 5~~) but it is not going to be installed
              Depends: php-symfony-expression-language (< 5~~) but it is not going to be installed
              Depends: php-symfony-yaml (< 5~~) but it is not going to be installed
              Depends: php-twig (> 2.9) but it is not going to be installed
              Depends: php-twig (< 4~~) but it is not going to be installed
              Depends: php-mariadb-mysql-kbs (>= 1.2) but it is not going to be installed
              Depends: php-mariadb-mysql-kbs (< 2~~) but it is not going to be installed
              Depends: libjs-sphinxdoc (>= 1.0) but it is not going to be installed
              Recommends: php-bz2
              Recommends: php-tcpdf but it is not going to be installed
              Recommends: php-zip

$ sudo apt install \
dbconfig-no-thanks dbconfig-common libjs-bootstrap4 libjs-codemirror libjs-jquery libjs-jquery-mousewheel \
libjs-jquery-timepicker libjs-jquery-ui libjs-openlayers php-mysql php-google-recaptcha php-phpmyadmin-motranslator \
php-phpmyadmin-shapefile php-phpmyadmin-sql-parser php-twig-i18n-extension php-phpseclib php-symfony-config \
php-symfony-dependency-injection php-symfony-expression-language php-symfony-yaml php-twig php-mariadb-mysql-kbs \
libjs-sphinxdoc php-bz2 php-tcpdf php-zip
```

``` bash
$ sudo apt install phpmyadmin
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 phpmyadmin : Depends: php-twig (> 2.9) but 2.6.2-2 is to be installed
```

``` bash
$ sudo apt -t buster-backports install php-twig
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  php-twig-doc
The following packages will be upgraded:
  php-twig
1 upgraded, 0 newly installed, 0 to remove and 53 not upgraded.
Need to get 121 kB of archives.
After this operation, 73.7 kB of additional disk space will be used.
Get:1 http://deb.debian.org/debian buster-backports/main amd64 php-twig all 2.14.3-1~bpo10+1 [121 kB]
Fetched 121 kB in 0s (386 kB/s) 
(Reading database ... 79611 files and directories currently installed.)
Preparing to unpack .../php-twig_2.14.3-1~bpo10+1_all.deb ...
Unpacking php-twig (2.14.3-1~bpo10+1) over (2.6.2-2) ...
Setting up php-twig (2.14.3-1~bpo10+1) ...

$ wget https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-all-languages.zip
$ unzip phpMyAdmin-5.2.0-all-languages.zip
$ sudo service mysql stop && sudo service apache2 stop
$ sudo apt install phpmyadmin
$ sudo mv /usr/share/phpmyadmin /usr/share/phpmyadmin_old
$ sudo mv phpMyAdmin-5.2.0-all-languages phpmyadmin
$ sudo cp -r phpmyadmin /usr/share/
$ sudo cp /usr/share/phpmyadmin/config.sample.inc.php /usr/share/phpmyadmin/config.inc.php
$ sudo vim /usr/share/phpmyadmin/config.inc.php # 32文字以上のパスフレーズを設定
$ sudo mkdir /usr/share/phpmyadmin/tmp
$ sudo chown -R www-data:www-data /usr/share/phpmyadmin/tmp
$ sudo service mysql start && sudo service apache2 start
```

</details>

<details>
<summary>Upgrade php</summary>

``` bash
$ sudo apt install php-fpm libapache2-mod-php8.1 php-mbstring
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  php8.1-fpm
Suggested packages:
  php-pear
The following NEW packages will be installed:
  php-fpm php8.1-fpm
0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
Need to get 1679 kB of archives.
After this operation, 5594 kB of additional disk space will be used.
Do you want to continue? [Y/n] 
Get:1 https://packages.sury.org/php buster/main amd64 php8.1-fpm amd64 8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1 [1672 kB]
Get:2 https://packages.sury.org/php buster/main amd64 php-fpm all 2:8.1+92+0~20220117.43+debian10~1.gbpe0d14e [7476 B]
Fetched 1679 kB in 2s (885 kB/s)
Selecting previously unselected package php8.1-fpm.
(Reading database ... 81559 files and directories currently installed.)
Preparing to unpack .../php8.1-fpm_8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1_amd64.deb ...
Unpacking php8.1-fpm (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...
Selecting previously unselected package php-fpm.
Preparing to unpack .../php-fpm_2%3a8.1+92+0~20220117.43+debian10~1.gbpe0d14e_all.deb ...
Unpacking php-fpm (2:8.1+92+0~20220117.43+debian10~1.gbpe0d14e) ...
Setting up php8.1-fpm (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...

Creating config file /etc/php/8.1/fpm/php.ini with new version
NOTICE: Not enabling PHP 8.1 FPM by default.
NOTICE: To enable PHP 8.1 FPM in Apache2 do:
NOTICE: a2enmod proxy_fcgi setenvif
NOTICE: a2enconf php8.1-fpm
NOTICE: You are seeing this message because you have apache2 package installed.
Created symlink /etc/systemd/system/multi-user.target.wants/php8.1-fpm.service → /lib/systemd/system/php8.1-fpm.service.
Setting up php-fpm (2:8.1+92+0~20220117.43+debian10~1.gbpe0d14e) ...
Processing triggers for man-db (2.8.5-2) ...
Processing triggers for systemd (241-7~deb10u8) ...
Processing triggers for php8.1-fpm (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...
NOTICE: Not enabling PHP 8.1 FPM by default.
NOTICE: To enable PHP 8.1 FPM in Apache2 do:
NOTICE: a2enmod proxy_fcgi setenvif
NOTICE: a2enconf php8.1-fpm
NOTICE: You are seeing this message because you have apache2 package installed.
```

``` bash
$ php --version
PHP 8.1.6 (cli) (built: May 17 2022 16:49:19) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.6, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.6, Copyright (c), by Zend Technologies
```

``` bash
$ sudo apt install libapache2-mod-php8.1
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php8.1
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 1603 kB of archives.
After this operation, 5425 kB of additional disk space will be used.
Get:1 https://packages.sury.org/php buster/main amd64 libapache2-mod-php8.1 amd64 8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1 [1603 kB]
Fetched 1603 kB in 2s (903 kB/s)                 
Selecting previously unselected package libapache2-mod-php8.1.
(Reading database ... 81807 files and directories currently installed.)
Preparing to unpack .../libapache2-mod-php8.1_8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1_amd64.deb ...
Unpacking libapache2-mod-php8.1 (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...
Setting up libapache2-mod-php8.1 (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...

Creating config file /etc/php/8.1/apache2/php.ini with new version
libapache2-mod-php8.1: php8.0 module already enabled, not enabling PHP 8.1
Processing triggers for libapache2-mod-php8.1 (8.1.6-1+0~20220517.17+debian10~1.gbp6b3bd1) ...
```

``` bash
$ sudo a2dismod php7.4
Module php7.4 disabled.
To activate the new configuration, you need to run:
  systemctl restart apache2
```

``` bash
$ sudo systemctl restart apache2
```

``` bash
$ php -r "echo phpinfo();" | grep "php.ini"
Configuration File (php.ini) Path => /etc/php/8.1/cli
Loaded Configuration File => /etc/php/8.1/cli/php.ini
```

``` bash
$ sudo update-alternatives --config php
There are 3 choices for the alternative php (providing /usr/bin/php).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/php8.1   81        auto mode
  1            /usr/bin/php7.4   74        manual mode
  2            /usr/bin/php8.0   80        manual mode
  3            /usr/bin/php8.1   81        manual mode

Press <enter> to keep the current choice[*], or type selection number: 0
```

``` bash
sudo cp -r /etc/apache2/conf-available/php8.1-fpm.conf /etc/apache2/conf-enabled/
```

</details>

## SSL証明書とHTTTPS通信有効化

<details>
<summary>Let's EncryptからSSL証明書を取得する準備</summary>

[snap instalation](https://snapcraft.io/docs/installing-snap-on-debian)


``` Debian bash
$ sudo apt update && sudo apt install -y snap snapd python3-certbot-apache ufw
$ sudo snap install core; sudo snap refresh core
$ sudo apt remove certbot
$ sudo snap install --classic certbot
certbot 1.28.0 from Certbot Project (certbot-eff✓) installed
$ sudo ln -s /snap/bin/certbot /usr/bin/certbot
$ sudo certbot --apache -d enginearn.dev
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): enginyaaaaan@gmail.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v02.api.letsencrypt.org/directory
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(A)gree/(C)ancel: A

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: Y
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for enginearn.dev
Waiting for verification...
Cleaning up challenges

We were unable to find a vhost with a ServerName or Address of enginearn.dev.
Which virtual host would you like to choose?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: wordpress-https.conf           |                       | HTTPS | Enabled
2: 000-default.conf               |                       |       | Enabled
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/wordpress-https.conf

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Redirecting vhost in /etc/apache2/sites-enabled/000-default.conf to ssl vhost in /etc/apache2/sites-enabled/wordpress-https.conf

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled https://enginearn.dev

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=enginearn.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/enginearn.dev/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/enginearn.dev/privkey.pem
   Your cert will expire on 2022-09-13. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - Your account credentials have been saved in your Certbot
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Certbot so
   making regular backups of this folder is ideal.
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```

``` Debian bash
$ sudo ufw app list
Available applications:
  AIM
  Bonjour
  CIFS
  DNS
  Deluge
  IMAP
  IMAPS
  IPP
  KTorrent
  Kerberos Admin
  Kerberos Full
  Kerberos KDC
  Kerberos Password
  LDAP
  LDAPS
  LPD
  MSN
  MSN SSL
  Mail submission
  NFS
  OpenSSH
  POP3
  POP3S
  PeopleNearby
  SMTP
  SSH
  Socks
  Telnet
  Transmission
  Transparent Proxy
  VNC
  WWW
  WWW Cache
  WWW Full
  WWW Secure
  XMPP
  Yahoo
  qBittorrent
  svnserve
$ sudo ufw allow "WWW Full"
Rules updated
Rules updated (v6)

# FireWallの状態
$ sudo ufw status
Status: inactive
$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup

$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
WWW Full                   ALLOW       Anywhere
WWW Full (v6)              ALLOW       Anywhere (v6)

$ sudo certbot --apache -d enginearn.dev
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for enginearn.dev
Waiting for verification...
Cleaning up challenges

We were unable to find a vhost with a ServerName or Address of enginearn.dev.
Which virtual host would you like to choose?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: wordpress-https.conf           |                       | HTTPS | Enabled
2: 000-default.conf               |                       |       | Enabled
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Deploying Certificate to VirtualHost /etc/apache2/sites-enabled/wordpress-https.conf

Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
Redirecting vhost in /etc/apache2/sites-enabled/000-default.conf to ssl vhost in /etc/apache2/sites-enabled/wordpress-https.conf

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Congratulations! You have successfully enabled https://enginearn.dev

You should test your configuration at:
https://www.ssllabs.com/ssltest/analyze.html?d=enginearn.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

IMPORTANT NOTES:
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/enginearn.dev/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/enginearn.dev/privkey.pem
   Your cert will expire on 2022-09-13. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - If you like Certbot, please consider supporting our work by:

   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le

$ sudo certbot certonly --apache
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache

Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: enginearn.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel): 1
Cert not yet due for renewal

You have an existing certificate that has exactly the same domains or certificate name you requested and isn't close to expiry.
(ref: /etc/letsencrypt/renewal/enginearn.dev.conf)

What would you like to do?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: Keep the existing certificate for now
2: Renew & replace the cert (limit ~5 per 7 days)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Keeping the existing certificate

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Certificate not yet due for renewal; no action taken.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

${APACHE_LOG_DIR}/error.log

</details>

## PHP Postges NGINX with CentOS stream9 on GCE 環境構築

### CentOS strem9 基本設定

<details>
<summary>レポジトリ追加</summary>

``` bash
$ sudo dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm
$ sudo dnf config-manager --set-enabled remi
$ sudo dnf module list reset php -y
Last metadata expiration check: 0:14:13 ago on Fri 17 Jun 2022 10:00:15 PM JST.
Remi's Modular repository for Enterprise Linux 9 - x86_64
Name             Stream               Profiles                              Summary                          
php              remi-7.4             common [d], devel, minimal            PHP scripting language           
php              remi-8.0             common [d], devel, minimal            PHP scripting language           
php              remi-8.1             common [d], devel, minimal            PHP scripting language           

Hint: [d]efault, [e]nabled, [x]disabled, [i]nstalled
$ sudo dnf module enable php:remi-8.1
Last metadata expiration check: 0:15:38 ago on Fri 17 Jun 2022 10:00:15 PM JST.
Dependencies resolved.
=============================================================================================================
 Package                  Architecture            Version                     Repository                Size
=============================================================================================================
Enabling module streams:
 php                                              remi-8.1                                                  

Transaction Summary
=============================================================================================================

Is this ok [y/N]: y
Complete!
```

</details>

<details>
<summary>パッケージ更新</summary>

``` bash
$ sudo dnf -y groupinstall base
$ sudo dnf -y groupinstall development
$ sudo dnf update -y
```

</details>

<details>
<summary>不要な物を停止 削除</summary>

``` bash
$ sudo systemctl disable atd kdump mdmonitor
$ sudo dnf remove -y cockpit
$ sudo reboot
```

</details>

<details>
<summary>Firewallの設定</summary>

``` bash
$ sudo firewall-cmd --list-all
trusted (active)
  target: ACCEPT
  icmp-block-inversion: no
  interfaces: eth0
  sources: 
  services: 
  ports: 
  protocols: 
  forward: yes
  masquerade: no
  forward-ports: 
  source-ports: 
  icmp-blocks: 
  rich rules:
```

``` bash
$ sudo firewall-cmd --remove-service=cockpit --permanent
Warning: NOT_ENABLED: cockpit
success
$ sudo firewall-cmd --remove-service=dhcpv6-client --permanent
Warning: NOT_ENABLED: dhcpv6-client
success
```

``` bash
$ sudo firewall-cmd --add-port=80/tcp --permanent
success
$ sudo firewall-cmd --add-port=443/tcp --permanent
success
sudo firewall-cmd --add-service=ssh --permanent
success

sudo firewall-cmd --reload
success
```

``` bash
$ sudo firewall-cmd --list-all
trusted (active)
  target: ACCEPT
  icmp-block-inversion: no
  interfaces: eth0
  sources: 
  services: ssh
  ports: 80/tcp 443/tcp
  protocols: 
  forward: yes
  masquerade: no
  forward-ports: 
  source-ports: 
  icmp-blocks: 
  rich rules:
```

</details>

<details>
<summary>Chronyの設定</summary>

``` bash
$ sudo timedatectl set-timezone Asia/Tokyo
$ sudo vim /etc/chrony.conf

> # server metadata.google.internal iburst
> server ntp.nict.jp iburst

$ sudo systemctl restart chronyd
```

``` bash
$ sudo systemctl enable chronyd
[enginyaaaaan@centos-stream9 ~]$ chronyc sources -v

  .-- Source mode  '^' = server, '=' = peer, '#' = local clock.
 / .- Source state '*' = current best, '+' = combined, '-' = not combined,
| /             'x' = may be in error, '~' = too variable, '?' = unusable.
||                                                 .- xxxx [ yyyy ] +/- zzzz
||      Reachability register (octal) -.           |  xxxx = adjusted offset,
||      Log2(Polling interval) --.      |          |  yyyy = measured offset,
||                                \     |          |  zzzz = estimated error.
||                                 |    |           \
MS Name/IP address         Stratum Poll Reach LastRx Last sample               
===============================================================================
^- ntp-b2.nict.go.jp             1   6   177    65   +176us[ +176us] +/- 1329us
^* metadata.google.internal      2   6   177    65  +9151ns[  +24us] +/-  353us
```

</details>

<details>
<summary>postfixでメール送信設定</summary>

``` bash
$ sudo dnf install -y postfix
$ sudo systemctl enable --now postfix
Created symlink /etc/systemd/system/multi-user.target.wants/postfix.service → /usr/lib/systemd/system/postfix.service.
$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/usr/lib/systemd/system/postfix.service; enabled; vendor preset: disabled)
     Active: active (running) since Fri 2022-06-17 20:55:17 JST; 15s ago
    Process: 2754 ExecStartPre=/usr/sbin/restorecon -R /var/spool/postfix/pid/master.pid (code=exited, statu>
    Process: 2755 ExecStartPre=/usr/libexec/postfix/aliasesdb (code=exited, status=0/SUCCESS)
    Process: 2759 ExecStartPre=/usr/libexec/postfix/chroot-update (code=exited, status=0/SUCCESS)
    Process: 2760 ExecStart=/usr/sbin/postfix start (code=exited, status=0/SUCCESS)
   Main PID: 2829 (master)
      Tasks: 3 (limit: 11072)
     Memory: 4.9M
        CPU: 480ms
     CGroup: /system.slice/postfix.service
             ├─2829 /usr/libexec/postfix/master -w
             ├─2830 pickup -l -t unix -u
             └─2831 qmgr -l -t unix -u

$ sudo vim /etc/postfix/gmail # [smtp.gmail.com]:587 enginyaaaaan@gmail.com:PASSWD
$ sudo chmod 600 /etc/postfix/gmail
$ sudo postmap /etc/postfix/gmail
$ sudo vim /etc/postfix/main.cf

relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/gmail
smtp_sasl_security_options = noanonymous
smtp_sasl_tls_security_options = noanonymous
smtp_sasl_mechanism_filter = plain
smtp_use_tls = yes

$ sudo systemctl reload postfix
```

</details>

<details>
<summary>送信テスト</summary>

``` bash
$ echo test | sendmail "test mail" enginyaaaaan@gmail.com
You have new mail in /var/spool/mail/enginyaaaaan # success!
```

</details>

<details>
<summary>PHPをインストール</summary>

``` bash
$ sudo dnf install php
$ php --version
PHP 8.1.7 (cli) (built: Jun  7 2022 18:21:38) (NTS gcc x86_64)
Copyright (c) The PHP Group
Zend Engine v4.1.7, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.7, Copyright (c), by Zend Technologies
```

</details>


<details>
<summary>golangをインストール</summary>

``` bash
$ wget https://go.dev/dl/go1.18.3.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.18.3.linux-amd64.tar.gz
echo 'PATH="$PATH":/usr/local/go/bin' >> ~/.bashrc
$ source .bashrc
$ go version
go version go1.18.3 linux/amd64

```

PATHを通すの挙動

``` bash
$ echo $PATH
/home/enginyaaaaan/.local/bin:/home/enginyaaaaan/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
$ echo $PATH
/home/enginyaaaaan/.local/bin:/home/enginyaaaaan/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/usr/local/go/bin
$ echo $PATH
After logout, PATH: "/usr/local/go/bin" gone!
/home/enginyaaaaan/.local/bin:/home/enginyaaaaan/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```

``` DANGER COMMAND
$ export PATH=$PATH:/usr/local/go/bin
```

</details>

<details>
<summary>Hugoのインストール</summary>

``` bash
$ wget https://github.com/gohugoio/hugo/releases/download/v0.101.0/hugo_0.101.0_Linux-64bit.tar.gz
]$ sudo tar -C /usr/bin -xvzf hugo_0.101.0_Linux-64bit.tar.gz 
LICENSE
README.md
hugo
$ hugo version
hugo v0.101.0-466fa43c16709b4483689930a4f9ac8add5c9f66 linux/amd64 BuildDate=2022-06-16T07:09:16Z VendorInfo=gohugoio
```

</details>

<details>
<summary>PostgreSQLインストール</summary>

``` bash
$ sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
Last metadata expiration check: 2:10:05 ago on Tue 21 Jun 2022 08:55:29 PM JST.
pgdg-redhat-repo-latest.noarch.rpm                                           9.2 kB/s |  12 kB     00:01    
Dependencies resolved.
=============================================================================================================
 Package                        Architecture         Version                Repository                  Size
=============================================================================================================
Installing:
 pgdg-redhat-repo               noarch               42.0-24                @commandline                12 k

Transaction Summary
=============================================================================================================
Install  1 Package

Total size: 12 k
Installed size: 12 k
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                     1/1 
  Installing       : pgdg-redhat-repo-42.0-24.noarch                                                     1/1 
  Verifying        : pgdg-redhat-repo-42.0-24.noarch                                                     1/1 

Installed:
  pgdg-redhat-repo-42.0-24.noarch                                                                            

Complete!
```

``` bash
$ sudo dnf -qy module disable postgresql
Importing GPG key 0x442DF0F8:
 Userid     : "PostgreSQL RPM Building Project <pgsql-pkg-yum@postgresql.org>"
 Fingerprint: 68C9 E2B9 1A37 D136 FE74 D176 1F16 D2E1 442D F0F8
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG
Unable to resolve argument postgresql
Error: Problems in request:
missing groups or modules: postgresql
```

``` bash
$ sudo dnf install -y postgresql14-server
```

``` bash
$ sudo /usr/pgsql-14/bin/postgresql-14-setup initdb
Initializing database ... OK


$ sudo systemctl start postgresql-14
```

``` bash
$ sudo systemctl enable postgresql-14
Created symlink /etc/systemd/system/multi-user.target.wants/postgresql-14.service → /usr/lib/systemd/system/postgresql-14.service.
```

</details>

## git commands

<details>
<summary>git addを取り消す</summary>

``` git
git rm --cached -r .
```

</details>

<details>
<summary>branch削除</summary>

``` git
git branch -d origin
```

</details>

<details>
<summary>まだあんまり理解してないコマンド</summary>

``` git
git revert <commit id>
```

``` git
git reset --hard <commit id>
```

``` git
git status   
On branch master
Your branch and 'origin/main' have diverged,
and have 2 and 6 different commits each, respectively.
(use "git pull" to merge the remote branch into yours)

nothing to commit, working tree clean
```

``` git
git pull  
fatal: refusing to merge unrelated histories
```

``` git
git merge --allow-unrelated-histories --squash main
```

``` git
echo "# docker-getting-started-app" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/enginearn/docker-getting-started-app.git
git push -u origin main
```

</details>

## docker-compose

<details>
<summary></summary>

``` docker
docker-compose up -d
docker-compose down --volume
```

## ubuntu server 初期設定

<details>
<summary>updating packages</summary>

``` bash
sudo apt update && sudo apt upgrade -y
```

</details>

<details>
<summary>set hostname</summary>

``` bash
$ hostname
ubuntu

$ sudo hostnamectl set-hostname ubuntu-server-1
$ hostname
ubuntu-server-1
```

</details>

<details>
<summary>setting timezone</summary>

``` bash
$ timedatectl status
               Local time: Sun 2022-06-19 12:45:45 UTC
           Universal time: Sun 2022-06-19 12:45:45 UTC
                 RTC time: n/a
                Time zone: Etc/UTC (UTC, +0000)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no

$ sudo timedatectl set-timezone "Asia/Tokyo"
$ timedatectl status
               Local time: Sun 2022-06-19 21:46:50 JST
           Universal time: Sun 2022-06-19 12:46:50 UTC
                 RTC time: n/a
                Time zone: Asia/Tokyo (JST, +0900)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no

```

</details>

<details>
<summary>locale</summary>

``` bash
$ localectl list-locales
C.UTF-8
en_US.UTF-8

$ sudo apt install -y language-pack-ja
$ localectl list-locales
C.UTF-8
en_US.UTF-8
ja_JP.UTF-8

$ localectl status
   System Locale: LANG=C.UTF-8
       VC Keymap: n/a
      X11 Layout: us
       X11 Model: pc105

$ sudo localectl set-locale LANG=ja_JP.UTF-8
$ localectl status
   System Locale: LANG=ja_JP.UTF-8
       VC Keymap: n/a
      X11 Layout: us
       X11 Model: pc105
```

</details>

<details>
<summary>Firewall settings</summary>

``` bash
$ sudo apt install -y ufw
$ sudo ufw status
Status: inactive

$ sudo vim /etc/ssh/sshd_config # Port 22
ubuntu@ubuntu:~$ sudo ufw default deny
Default incoming policy changed to 'deny' 
(be sure to update your rules accordingly)

$ sudo ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```

</details>

<details>
<summary>staitc ipの設定</summary>

`/etc/dhcp/dhclient.conf`を以下のように編集

> interface eth0
> static ip_address=xxx.xxx.xxx.xxx/24
> static routers=xxx.xxx.xxx.xxx # デフォルトゲートウェイのIPアドレス
> static domain_name_servers=xxx.xxx.xxx.xxx # DNSのIPアドレス
>
> interface wlan0
> static ip_address=xxx.xxx.xxx.xxx/24
> static routers=xxx.xxx.xxx.xxx # デフォルトゲートウェイのIPアドレス
> static domain_name_servers=xxx.xxx.xxx.xxx # DNSのIPアドレス
</details>


## Python

<details>
<summary>printの出力結果をUTF-8に</summary>

``` 
# printの出力結果をUTF-8に
sys.stdout = io.TextIOWrapper(sys.stdout.buffer, encoding='utf-8')
sys.stderr = io.TextIOWrapper(sys.stderr.buffer, encoding='utf-8')
print('標準出力(stdout)へ、utf-8で出力')
print('標準エラー出力(stderr)へ、utf-8で出力', file=sys.stderr)
```

</details>

## Python仮想環境構築

<details>
<summary>Python 2.7</summary>

``` PowerShell
$ py -2 -m virtualenv venv27
created virtual environment CPython2.7.18.final.0-64 in 5958ms
  creator CPython2Windows(dest=C:\Users\path\to\Python\venv27, clear=False, global=False)
  seeder FromAppData(download=False, pip=latest, setuptools=latest, wheel=latest, via=copy, app_data_dir=C:\Users\pathto\AppData\Local\pypa\virtualenv\seed-app-data\v1.0.1)
  activators PythonActivator,FishActivator,BatchActivator,BashActivator,PowerShellActivator
 .\venv27\Scripts\activate
(venv27) PS C:\Users\pathto\Development\Python>
(venv27) PS C:\Users\pathto\Development\Python> pip list
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Package    Version
---------- -------
pip        20.0.2 
setuptools 44.1.0 
wheel      0.34.2 
WARNING: You are using pip version 20.0.2; however, version 20.3.4 is available.
You should consider upgrading via the 'C:\Users\pathto\Development\Python\venv27\Scripts\python.exe -m pip install --upgrade pip' command.
(venv27) PS C:\Users\pathto\Development\Python> python -m pip install -U pip
DEPRECATION: Python 2.7 reached the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 is no longer maintained. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Collecting pip
  Downloading pip-20.3.4-py2.py3-none-any.whl (1.5 MB)
     |################################| 1.5 MB 2.0 MB/s
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 20.0.2
    Uninstalling pip-20.0.2:
      Successfully uninstalled pip-20.0.2
Successfully installed pip-20.3.4
```

</details>

<details>
<summary>Python 3.x</summary>

``` PowerShell
PS C:\Users\pathto\Development\Python> py -3.10 -m venv venv310 
PS C:\Users\pathto\Development\Python> .\venv310\Scripts\activate
(venv310) PS C:\Users\pathto\Development\Python>
(venv310) PS C:\Users\pathto\Development\Python> pip list
Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0
WARNING: You are using pip version 22.0.4; however, version 22.1 is available.
You should consider upgrading via the 'C:\Users\pathto\Development\Python\venv310\Scripts\python.exe -m pip install --upgrade pip' command.
(venv310) PS C:\Users\pathto\Development> python -m pip install -U pip
Requirement already satisfied: pip in c:\users\pathto\development\python\venv310\lib\site-packages (22.0.4)
Collecting pip
  Using cached pip-22.1-py3-none-any.whl (2.1 MB)
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 22.0.4
    Uninstalling pip-22.0.4:
      Successfully uninstalled pip-22.0.4
Successfully installed pip-22.1
```

</details>

## Shell Script

<details>
<summary>Shell Script</summary>

``` sh
#!/bin/sh

stty -echo
read -p "enter password: " entered
stty echo
echo "what you entered: $entered"

```

</details>

## ubuntu 22.04にPython環境構築

[docker image](https://hub.docker.com/repository/docker/enginearn/ubuntu-latest-jp)からubuntuを用意する

<details>
<summary>Python3の確認</summary>

``` docker container
$ which pythom3
$ # python3が入ってない
```

</details>

<details>
<summary>Python3とpip3をインストール</summary>

``` docker container
$ sudo apt install python3 python3-pip
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています... 完了
状態情報を読み取っています... 完了
以下の追加パッケージがインストールされます:
  binutils binutils-common binutils-x86-64-linux-gnu build-essential bzip2 ca-certificates cpp cpp-11 dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm
  javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan6 libassuan0 libatomic1 libbinutils libbrotli1 libbsd0 libc-dev-bin libc-devtools libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libdeflate0 libdpkg-perl libexpat1-dev libfakeroot     
  libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev libgd3 libgdbm-compat4 libgdbm6 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjs-sphinxdoc libjs-underscore libksba8 libldap-2.5-0 libldap-common liblocale-gettext-perl liblsan0 libmd0 libmpc3   
  libmpfr6 libnpth0 libnsl-dev libperl5.34 libpng16-16 libpython3-dev libpython3-stdlib libpython3.10-dev libquadmath0 libsasl2-2 libsasl2-modules libsasl2-modules-db libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libx11-6 libx11-data libxau6 libxcb1 libxdmcp6 libxpm4   
  linux-libc-dev lto-disabled-list make manpages manpages-dev netbase openssl patch perl perl-modules-5.34 pinentry-curses python3-dev python3-distutils python3-lib2to3 python3-minimal python3-pkg-resources python3-setuptools python3-wheel python3.10 python3.10-dev python3.10-minimal       
  rpcsvc-proto ucf xz-utils zlib1g-dev
提案パッケージ:
  binutils-doc bzip2-doc cpp-doc gcc-11-locales dbus-user-session libpam-systemd pinentry-gnome3 tor debian-keyring g++-multilib g++-11-multilib gcc-11-doc gcc-multilib autoconf automake libtool flex bison gdb gcc-doc gcc-11-multilib parcimonie xloadimage scdaemon apache2 | lighttpd        
  | httpd glibc-doc git bzr libgd-tools gdbm-l10n libsasl2-modules-gssapi-mit | libsasl2-modules-gssapi-heimdal libsasl2-modules-ldap libsasl2-modules-otp libsasl2-modules-sql libstdc++-11-doc make-doc man-browser ed diffutils-doc perl-doc libterm-readline-gnu-perl
  | libterm-readline-perl-perl libtap-harness-archive-perl pinentry-doc python3-doc python3-tk python3-venv python-setuptools-doc python3.10-venv python3.10-doc binfmt-support
以下のパッケージが新たにインストールされます:
  binutils binutils-common binutils-x86-64-linux-gnu build-essential bzip2 ca-certificates cpp cpp-11 dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm
  javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan6 libassuan0 libatomic1 libbinutils libbrotli1 libbsd0 libc-dev-bin libc-devtools libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libdeflate0 libdpkg-perl libexpat1-dev libfakeroot     
  libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev libgd3 libgdbm-compat4 libgdbm6 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjs-sphinxdoc libjs-underscore libksba8 libldap-2.5-0 libldap-common liblocale-gettext-perl liblsan0 libmd0 libmpc3   
  libmpfr6 libnpth0 libnsl-dev libperl5.34 libpng16-16 libpython3-dev libpython3-stdlib libpython3.10-dev libquadmath0 libsasl2-2 libsasl2-modules libsasl2-modules-db libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libx11-6 libx11-data libxau6 libxcb1 libxdmcp6 libxpm4   
  linux-libc-dev lto-disabled-list make manpages manpages-dev netbase openssl patch perl perl-modules-5.34 pinentry-curses python3 python3-dev python3-distutils python3-lib2to3 python3-minimal python3-pip python3-pkg-resources python3-setuptools python3-wheel python3.10 python3.10-dev      
  python3.10-minimal rpcsvc-proto ucf xz-utils zlib1g-dev
アップグレード: 0 個、新規インストール: 122 個、 削除: 0 個、保留: 0 個。
95.0 MB のアーカイブを取得する必要があります。
この操作後に追加で 333 MB のディスク容量が消費されます。
続行しますか? [Y/n] n
中断しました。
```

提案パッケージの中にpython3-venv python3.10-venvがいるので、一旦インストールをキャンセル

提案パッケージも纏めて入れるようにコマンドを追加

``` docker container
$ sudo apt install python3 python3-pip --install-suggests
アップグレード: 0 個、新規インストール: 4730 個、 削除: 0 個、保留: 0 個。
7,119 MB のアーカイブを取得する必要があります。
この操作後に追加で 22.2 GB のディスク容量が消費されます。
続行しますか? [Y/n] n
中断しました。
```

よくわからんのが入りすぎて22GBとかイミフなので、以下でインストール

``` docker container
$ sudo apt install python3 python3-pip python3-venv
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています... 完了
状態情報を読み取っています... 完了
以下の追加パッケージがインストールされます:
  binutils binutils-common binutils-x86-64-linux-gnu build-essential bzip2 ca-certificates cpp cpp-11 dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm       
  javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan6 libassuan0 libatomic1 libbinutils libbrotli1 libbsd0 libc-dev-bin libc-devtools libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libdeflate0 libdpkg-perl libexpat1-dev libfakeroot
  libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev libgd3 libgdbm-compat4 libgdbm6 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjs-sphinxdoc libjs-underscore libksba8 libldap-2.5-0 libldap-common liblocale-gettext-perl liblsan0 libmd0 libmpc3   
  libmpfr6 libnpth0 libnsl-dev libperl5.34 libpng16-16 libpython3-dev libpython3-stdlib libpython3.10-dev libquadmath0 libsasl2-2 libsasl2-modules libsasl2-modules-db libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libx11-6 libx11-data libxau6 libxcb1 libxdmcp6 libxpm4   
  linux-libc-dev lto-disabled-list make manpages manpages-dev netbase openssl patch perl perl-modules-5.34 pinentry-curses python3-dev python3-distutils python3-lib2to3 python3-minimal python3-pip-whl python3-pkg-resources python3-setuptools python3-setuptools-whl python3-wheel python3.10  
  python3.10-dev python3.10-minimal python3.10-venv rpcsvc-proto ucf xz-utils zlib1g-dev
提案パッケージ:
  binutils-doc bzip2-doc cpp-doc gcc-11-locales dbus-user-session libpam-systemd pinentry-gnome3 tor debian-keyring g++-multilib g++-11-multilib gcc-11-doc gcc-multilib autoconf automake libtool flex bison gdb gcc-doc gcc-11-multilib parcimonie xloadimage scdaemon apache2 | lighttpd        
  | httpd glibc-doc git bzr libgd-tools gdbm-l10n libsasl2-modules-gssapi-mit | libsasl2-modules-gssapi-heimdal libsasl2-modules-ldap libsasl2-modules-otp libsasl2-modules-sql libstdc++-11-doc make-doc man-browser ed diffutils-doc perl-doc libterm-readline-gnu-perl
  | libterm-readline-perl-perl libtap-harness-archive-perl pinentry-doc python3-doc python3-tk python-setuptools-doc python3.10-doc binfmt-support
以下のパッケージが新たにインストールされます:
  binutils binutils-common binutils-x86-64-linux-gnu build-essential bzip2 ca-certificates cpp cpp-11 dirmngr dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc gcc-11 gcc-11-base gnupg gnupg-l10n gnupg-utils gpg gpg-agent gpg-wks-client gpg-wks-server gpgconf gpgsm
  javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan6 libassuan0 libatomic1 libbinutils libbrotli1 libbsd0 libc-dev-bin libc-devtools libc6-dev libcc1-0 libcrypt-dev libctf-nobfd0 libctf0 libdeflate0 libdpkg-perl libexpat1-dev libfakeroot     
  libfile-fcntllock-perl libfontconfig1 libfreetype6 libgcc-11-dev libgd3 libgdbm-compat4 libgdbm6 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery libjs-sphinxdoc libjs-underscore libksba8 libldap-2.5-0 libldap-common liblocale-gettext-perl liblsan0 libmd0 libmpc3   
  libmpfr6 libnpth0 libnsl-dev libperl5.34 libpng16-16 libpython3-dev libpython3-stdlib libpython3.10-dev libquadmath0 libsasl2-2 libsasl2-modules libsasl2-modules-db libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libx11-6 libx11-data libxau6 libxcb1 libxdmcp6 libxpm4   
  linux-libc-dev lto-disabled-list make manpages manpages-dev netbase openssl patch perl perl-modules-5.34 pinentry-curses python3 python3-dev python3-distutils python3-lib2to3 python3-minimal python3-pip python3-pip-whl python3-pkg-resources python3-setuptools python3-setuptools-whl       
  python3-venv python3-wheel python3.10 python3.10-dev python3.10-minimal python3.10-venv rpcsvc-proto ucf xz-utils zlib1g-dev
アップグレード: 0 個、新規インストール: 126 個、 削除: 0 個、保留: 0 個。
97.4 MB のアーカイブを取得する必要があります。
この操作後に追加で 336 MB のディスク容量が消費されます。
続行しますか? [Y/n]
```

</details>

<details>
<summary>Python3起動確認</summary>

``` docker container
$ which python3
/usr/bin/python3

$ python3
Python 3.10.4 (main, Apr  2 2022, 09:04:19) [GCC 11.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

</details>

<details>
<summary>Python3でvenv</summary>

``` docker container
redmine-ubuntu-ansible$ python3 -m venv venv
redmine-ubuntu-ansible$ . venv/bin/activate
(venv) redmine-ubuntu-ansible$
```

```
sudo apt install hoge --install-suggests
sudo apt install hoge --install-recommends
```

</details>


<details>
<summary>install postgresql</summary>

``` ubuntu
sudo apt install postgresql postgresql-dev-145 --install-suggests
```

</details>

## winget

<details>
<summary>基本的な使い方</summary>

``` 

```

</details>


## oh-my-posh

<details>
<summary>winget install oh-my-posh</summary>

``` PowerSHell
winget install oh-my-posh
'msstore' ソースを使用するには、使用する前に次の契約を表示する必要があります。
Terms of Transaction: https://aka.ms/microsoft-store-terms-of-transaction
ソースが正常に機能するには、現在のマシンの 2 文字の地理的リージョンをバックエンド サービスに送信する必要があります (例: "US")。

すべてのソース契約条件に同意しますか?
[Y] はい  [N] いいえ: Y
複数のパッケージが入力条件に一致しました。入力内容を修正してください。
名前       ID                      ソース
------------------------------------------
oh-my-posh XP8K0HKJFRXGCK          msstore
Oh My Posh JanDeDobbeleer.OhMyPosh winget
```

``` PowerShell
winget install oh-my-posh --id XP8K0HKJFRXGCK
見つかりました oh-my-posh [XP8K0HKJFRXGCK] バージョン Unknown
このアプリケーションは所有者からライセンス供与されます。
Microsoft はサードパーティのパッケージに対して責任を負わず、ライセンスも付与しません。
バージョン: Unknown
公開元: jandedobbeleer
発行元 URL: https://ohmyposh.dev/
発行元のサポート URL: http://support@ohmyposh.dev/
説明: A prompt theme engine for any shell.
ライセンス: Copyright 2022 Jan De Dobbeleer

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
documentation files (the "Software"), to deal in the Software without restriction, including without limitation
the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software,
and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
著作権: 2022 Jan De Dobbeleer
契約:
Category: Productivity
Pricing: Free
Free Trial: No
Terms of Transaction: https://aka.ms/microsoft-store-terms-of-transaction
Seizure Warning: https://aka.ms/microsoft-store-seizure-warning
Store License Terms: https://aka.ms/microsoft-store-license


発行元は、お客様がインストール前に上記の情報を表示し、契約に同意することを必要としています。
使用条件に同意しますか?
[Y] はい  [N] いいえ: Y
Downloading https://github.com/JanDeDobbeleer/oh-my-posh/releases/download/v7.94.1/install-amd64.exe
  ██████████████████████████████  6.23 MB / 6.23 MB
インストーラーハッシュが正常に検証されました
パッケージのインストールを開始しています...
インストールが完了しました
```

</details>

<details>
<summary>theme</summary>

``` Powershell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH\jandedobbeleer.omp.json"
```

</details>



---

[Docker環境でnodemonがwatchしてくれない問題と対処方法](https://jpdebug.com/p/2477366)

[【node.js】MySQL8.0に接続できない。Error: ER_NOT_SUPPORTED_AUTH_MODE](https://www.chuken-engineer.com/entry/2020/09/04/074216)

[docker上のアプリにlocalhostでアクセスしたらERR_EMPTY_RESPONSEが出る](https://qiita.com/amuyikam/items/01a8c16e3ddbcc734a46)

[bash の初期化ファイル .profile, .bashrc, .bash_profile の使い分けと管理方針](https://blog1.mammb.com/entry/2019/12/01/090000)

[Dockerコンテナに一般ユーザーを追加するときのDockerfileの設定](https://qiita.com/Spritaro/items/602118d946a4383bd2bb)

[Docker 停止中 or 稼働中の Ubuntu コンテナの Bash に入る - docker start attach](https://kei-s-lifehack.hatenablog.com/entry/docker-use-stopped-or-running-ubuntu-container-bash)

[AttributeError: 'str' object has no attribute 'read'](https://yohei-a.hatenablog.jp/entry/20200408/1586291597)

[PythonでJSON 読み込み](https://qiita.com/kikuchiTakuya/items/53990fca06fb9ba1d8a7)

[Pythonで辞書を作成するdict()と波括弧、辞書内包表記](https://note.nkmk.me/python-dict-create/)

[pythonでのcsvファイルの読み込み](https://qiita.com/motoki1990/items/0274d8bcf1a97fe4a869)

[Pythonプログラミング入門](https://utokyo-ipp.github.io/)

[[Python3]printで文字化けするので、文字コードを変更したい](https://www.curict.com/item/c7/c7eaca3.html)

[DockerのMySQLコンテナを日本語対応させる](https://qiita.com/zongxiaojie/items/6b593ec4ce5e85bb342c)

[nerdfonts](https://www.nerdfonts.com/#home)

[Wikimedia Downloads](https://dumps.wikimedia.org/)

[wikipediaを使ったword2vecコーパスの作り方をまとめてみた](https://qiita.com/Zect/items/d106d46fc94eaa2ed361)

[【Docker, Python】MySQL connectorサンプルコード](https://baran-gizagiza.com/docker-python-mysql-connector/)

[MySQL Rejecting Correct Password “Error 1045: Access denied for user (using password: YES)”](https://devanswers.co/mysql-rejecting-correct-password-error-1045-access-denied-for-user-using-password-yes/)

[Pythonで環境変数を活用する](https://www.twilio.com/blog/environment-variables-python-jp)

[mysql-phpmyadmin：依存：php-twig（> = 2.9）ですが、2.6.2-2がインストールされます。何？](https://yaoply.com/items/phpmyadmin-depends-php-twig-2-9-but-2-6-2-2-is-to-be-installed-what)

[How To Install MySQL 8.0 on Debian 11/10 /9](https://computingforgeeks.com/how-to-install-mysql-8-0-on-debian/)

[第26回　【WordPress】　MySQL5.7→MySQL8.0へアップグレード](https://tohyo2020.org/mysql-57-mysql-80/)

[QMK Firmware - All Supported Keyboards](https://qmk.fm/keyboards/)

[https://login.docker.com/u/login/identifier?state=hKFo2SBhWndZdzR1U0hZQmYtQng2cTdWb2V4a2pSdHowUXc2aqFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIDNHLU4xVXFOeUN5S0JZR1FUbThBYzkyaWNVUTF6MTc2o2NpZNkgbHZlOUdHbDhKdFNVcm5lUTFFVnVDMGxiakhkaTluYjk](https://login.docker.com/u/login/identifier?state=hKFo2SBhWndZdzR1U0hZQmYtQng2cTdWb2V4a2pSdHowUXc2aqFur3VuaXZlcnNhbC1sb2dpbqN0aWTZIDNHLU4xVXFOeUN5S0JZR1FUbThBYzkyaWNVUTF6MTc2o2NpZNkgbHZlOUdHbDhKdFNVcm5lUTFFVnVDMGxiakhkaTluYjk)

[Overlay2 について調べてみた - Qiita](https://qiita.com/toshihirock/items/e99889e4a77a76f28455)

[Debian 11.2に「sudo: ufw: command not found」の解決方法 - 最新IT技術情報_arkgame.com](https://arkgame.com/2020/03/29/post-44388/)

[wordpress-1-vm – Compute Engine – My First Project – Google Cloud Platform](https://console.cloud.google.com/compute/instancesDetail/zones/asia-northeast1-a/instances/wordpress-1-vm?authuser=4&project=resolute-fold-352811&pageState=(%22duration%22:(%22groupValue%22:%22PT1H%22,%22customValue%22:null)))
[VM インスタンス – Compute Engine – My First Project – Google Cloud Platform](https://console.cloud.google.com/compute/instances?authuser=4&project=resolute-fold-352811)

[enginearn/memo at dev-lenovo-13](https://github.com/enginearn/memo/tree/dev-lenovo-13)

[接続エラーを解決する - Google Chrome ヘルプ](https://support.google.com/chrome/answer/6098869#-200&zippy=%2C%E3%81%93%E3%81%AE%E6%8E%A5%E7%B6%9A%E3%81%A7%E3%81%AF%E3%83%97%E3%83%A9%E3%82%A4%E3%83%90%E3%82%B7%E3%83%BC%E3%81%8C%E4%BF%9D%E8%AD%B7%E3%81%95%E3%82%8C%E3%81%BE%E3%81%9B%E3%82%93neterr-cert-authority-invaliderr-cert-common-name-invalidneterr-cert-weak-signature-algorithmerr-certificate-transparency-requiredssl-%E8%A8%BC%E6%98%8E%E6%9B%B8%E3%82%A8%E3%83%A9%E3%83%BC)

[ネットワーク タグの構成  |  VPC  |  Google Cloud](https://cloud.google.com/vpc/docs/add-remove-network-tags?authuser=4&_ga=2.41882539.-80309478.1654773236&_gac=1.253379067.1655242528.CjwKCAjw46CVBhB1EiwAgy6M4o52LBfwXR-l-QDwtbYDicEX8zD7yFLH4bXRRJgXKDRBdftlZyVq8xoCDxAQAvD_BwE)

[34.84.110.68 / localhost | phpMyAdmin 5.2.0](http://34.84.110.68/phpmyadmin/index.php?route=/&route=%2F)

[PHP 8.1.7 - phpinfo()](https://enginearn.dev/.phpinfo.php)

[PHPでmbstringを設定して日本語環境に対応する方法を現役エンジニアが解説【初心者向け】 | TechAcademyマガジン](https://techacademy.jp/magazine/39850)

[【Vim】ファイル内で特定の文字列を検索するコマンド一覧 | かわたま.net](http://kawatama.net/web/1341)

[PHP 8.x での php.ini の設定について](https://zenn.dev/ksh2ksk4/articles/3cb75ed89ae662c1352d)

[【CentOS + PHP】「mbstring」を「Httpサーバー」にインストールする方法 - renoji.com](https://renoji.com/IT.php?Contents=OS_CentOS/Server_Http/Install_php_mbstring.html)

[【GCPでWordPress構築】4. https化のためにやること/WebサーバのSSL証明書導入/WordPressのURL変更 | Hello, new World](https://tomorisblog.com/gcp-wordpress-04/)

[Certbot Instructions | Certbot](https://certbot.eff.org/instructions?ws=apache&os=debianbuster)

[Ubuntu 20.04でLet’s Encryptを使用してApacheを保護する方法 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-20-04-ja)

[How To Install the Apache Web Server on Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04)

[How To Install the Apache Web Server on Ubuntu 20.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04#step-5-%E2%80%94-setting-up-virtual-hosts-(recommended))

[やさしいLet’s EncryptでSSL証明書を発行する方法 | Oji-Cloud](https://oji-cloud.net/2020/09/29/post-5570/)

[iptablesが難しいためufwでWEBサーバーのファイアウォール設定 - Qiita](https://qiita.com/shimakaze_soft/items/c3cce2bfb7d584e1fbce)

[DNSのゾーン設定を削除したあとにLet’s Encryptによる認証作業を行ったときに発生するエラーについて – エコテキブログ](https://e-yota.com/infrastructure/free_ssl_lets_encrypt_error/)

[SSL サーバ証明書：Apacheトラブルシューティング｜DigiCert（デジサート）](https://rms.ne.jp/sslserver/install/troubleshoot_apache-html/)

[SSL Server Test: enginearn.dev (Powered by Qualys SSL Labs)](https://www.ssllabs.com/ssltest/analyze.html?d=enginearn.dev)

[[*SSL*] Apache2.4にてSSL化を行う - Qiita](https://qiita.com/cigalecigales/items/63698979c4be452c82ea)

[ファイル認証　トラブルシューティング | さくらのサポート情報](https://help.sakura.ad.jp/rs/2268/?article_anchor=js-nav-3)

[Apache | 設定ファイル(httpd.conf)の初期設定](https://www.javadrive.jp/apache/install/index2.html#section2)

[日本語環境の設定 - mbstring - php.iniの設定 - PHP入門のカルマ](https://webkaru.net/php/mbstring-php-ini/)

[GCEでSSH鍵でログインが出来ない(（Permission denied (publickey,gssapi-keyex,gssapi-with-mic)）の解決方法 - Qiita](https://qiita.com/tab02733/items/f1cbfafd39a06271d7ef)

[[SSH]Permission deniedが出てきた時の対応 – ADACHIN SERVER LABO](https://blog.adachin.me/archives/2054)

[VSCodeとGCPを使ってリモート開発マシン作ってみた](https://zenn.dev/noumi0k/articles/6ee90a47921cc6ee8743)

[【秘密鍵/公開鍵】RSA暗号より強い、Ed25519を用いてSSHキーを作成する - Qiita](https://qiita.com/noumi0k/items/d277331819c9f4af6137)

[ssh_config(5): OpenSSH SSH client config files - Linux man page](https://linux.die.net/man/5/ssh_config)

[パスワード生成 (Passwords Generator)](https://www.graviness.com/app/pwg/)

[Google Compute Engine && VS Code でのremote ssh環境構築｜hgsgtk｜note](https://note.com/hgsgtk/n/nb36465c1ac7f)

[SSH で Permission Denied となる傾向と対策 - Qiita](https://qiita.com/youcune/items/2f427979403771f2e03a)

[公開鍵と秘密鍵のペアの作り方と、秘密鍵から公開鍵を再生成する方法 - Qiita](https://qiita.com/hirohiro77/items/d5970791ebb420759aba)

[Permission denied (publickey) の 対処方法はだいたいこれ | ORM ねこの遊び庭](https://ormcat.net/blog/20210509_github-denied-publickey/)

[SSH接続するための秘密鍵と公開鍵をMacで作る | www.ni4.jp](https://www.ni4.jp/2021/01/31-134600.html)

[実行ユーザーを指定してsshをした時にHost key verification failedが出たときの対処法 - Qiita](https://qiita.com/picapica/items/d4d3c80d8881fc2f279f)

[SSHでPermission deniedが解決しないと思ったらauthorized_keysに"\n"が紛れ込んでいた - Qiita](https://qiita.com/noir_neo/items/60532baaf051f91f3013)

[SSH公開鍵認証で接続するまで - Qiita](https://qiita.com/kazokmr/items/754169cfa996b24fcbf5)

[sshの認証についてまとめ - 技術ブログ](https://nkawamura.hatenablog.com/entry/2018/05/05/120616)

[インフラエンジニアじゃなくても押さえておきたいSSHの基礎知識 - Qiita](https://qiita.com/tag1216/items/5d06bad7468f731f590e)

[VSCodeからGCP(GoogleCloudPlatform)にSSH接続 - FlatKids](https://flat-kids.net/2020/03/09/vscode%E3%81%8B%E3%82%89gcpgooglecloudplatform%E3%81%ABssh%E6%8E%A5%E7%B6%9A/)

[SSHでPermission deniedが解決しないと思ったらauthorized_keysに"\n"が紛れ込んでいた - Qiita](https://qiita.com/noir_neo/items/60532baaf051f91f3013)

[GCP: Compute Engineに対して通常のsshコマンドでSSHできるようにする - nwtgck / Ryo Ota](https://scrapbox.io/nwtgck/GCP:_Compute_Engine%E3%81%AB%E5%AF%BE%E3%81%97%E3%81%A6%E9%80%9A%E5%B8%B8%E3%81%AEssh%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%A7SSH%E3%81%A7%E3%81%8D%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%99%E3%82%8B)

[【設定爆速】VS CodeのRemote Developmentを使ってSSH接続したEC2上のファイルを編集する | DevelopersIO](https://dev.classmethod.jp/articles/vs-code-remote-development-ec2/)

[公開鍵方式のssh接続ログイン時にパスワード入力が求められてしまう。](https://teratail.com/questions/337240)

[How To Configure SSH Key-Based Authentication on a Linux Server | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)

[[秘密鍵/公開鍵]GCPにSSHで接続する方法 | エンジニアの眠れない夜](https://sleepless-se.net/2018/09/15/gcp-ssh/)

[WindowsでSSHの鍵を作る - Qiita](https://qiita.com/digdagdag/items/9e5c061e7d86e0af9a57)

[ssh-keygen（sshキー) - vzの尺なblog](https://vz-shark.hatenablog.com/entry/2018/10/03/164528)

[[小ネタ] キーペアの秘密鍵が新OpenSSH形式であるためにWindows EC2インスタンスのログインパスワード復号に失敗するときの対処法 | DevelopersIO](https://dev.classmethod.jp/articles/windows-openssh-keypair/)

[Debian 10 Buster : システムのタイムゾーンを設定する : Server World](https://www.server-world.info/query?os=Debian_10&p=timezone)

[Debian 10 (buster) - 時刻同期設定(systemd-timesyncd)！ - mk-mode BLOG](https://www.mk-mode.com/blog/2019/10/23/debian-10-systemd-timesyncd/)

[I can't use vault ssh in windows 10](https://groups.google.com/g/vault-tool/c/5IWWpYERupw)

[メモモモモ: Windowsで始める初めてのSSH](http://memomo2.blogspot.com/2018/06/windowsssh.html)

[Win10起動時に仮想デスクトップ番号を指定してアプリを立ち上げる - Qiita](https://qiita.com/piyox2/items/328ca89a6e7effe58ced)

[Linuxのデバイスを確認するコマンド | パソコン工房 NEXMAG](https://www.pc-koubou.jp/magazine/36572)

[【Docker】イメージダウンロードでエラー（Error response from daemon）が発生した場合の対応方法 | インフラエンジニアの技術LOG](https://genchan.net/it/virtualization/docker/2553/)
[linux-tools-5.4.0-77-generic - Google 検索](https://www.google.com/search?q=linux-tools-5.4.0-77-generic&rlz=1C1QABZ_jaJP895JP895&oq=linux-tools-5.4.0-77-generic&aqs=chrome..69i57j0i5i19i30j0i19i30.4073j0j4&sourceid=chrome&ie=UTF-8)

[how can i pass through USB device in docker for windows(Hyper -v ) · Issue #3926 · docker/for-win](https://github.com/docker/for-win/issues/3926)

[How to Use Basler USB Cameras in Docker Container?](https://www.baslerweb.com/jp/sales-support/knowledge-base/frequently-asked-questions/how-to-use-basler-usb-cameras-in-docker-container/588488/)

[Docker - a way to give access to a host USB or serial device? - Stack Overflow](https://stackoverflow.com/questions/24225647/docker-a-way-to-give-access-to-a-host-usb-or-serial-device)

[バインドマウントの利用 | Docker ドキュメント](https://matsuand.github.io/docs.docker.jp.onthefly/storage/bind-mounts/)

[第17回 Dockerで植物が育つ様子を自動録画してみよう――その1：古賀政純の「攻めのITのためのDocker塾」（2/2 ページ） - ITmedia エンタープライズ](https://www.itmedia.co.jp/enterprise/articles/1603/02/news031_2.html)

[Docker run reference | Docker Documentation](https://docs.docker.com/engine/reference/run/)

[第17回 Dockerで植物が育つ様子を自動録画してみよう――その1：古賀政純の「攻めのITのためのDocker塾」（2/2 ページ） - ITmedia エンタープライズ](https://www.itmedia.co.jp/enterprise/articles/1603/02/news031_2.html)

[Windows環境でDockerコンテナにUSBウェブカメラを認識させる | UNITRUST](https://www.unitrust.co.jp/7117)

[USB デバイスを接続する | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/connect-usb)

[Release usbipd-win 2.3.0 · dorssel/usbipd-win](https://github.com/dorssel/usbipd-win/releases/tag/v2.3.0)

[WSL その227 - WSL 2にUSBデバイスを接続し、LinuxディストリビューションからUSBデバイスにアクセスするには - kledgeb](https://kledgeb.blogspot.com/2021/11/wsl-227-wsl-2usblinuxusb.html)

[Connecting USB devices to WSL - Windows Command Line](https://devblogs.microsoft.com/commandline/connecting-usb-devices-to-wsl/)

[macOS Catalinaでavrdudeを使ってProMicroに書き込もうとするとprogrammer is not respondingというエラーが出る - ぽよメモ](https://poyo.hatenablog.jp/entry/2019/11/04/005016)

[Error: The software identifier is not 'CATERIN': ASCII T - Google 検索](https://www.google.com/search?q=Error%3A+The+software+identifier+is+not+%27CATERIN%27%3A+ASCII+T&rlz=1C1QABZ_jaJP895JP895&oq=Error%3A+The+software+identifier+is+not+%27CATERIN%27%3A+ASCII+T&aqs=chrome.0.69i59j69i58.1653j0j7&sourceid=chrome&ie=UTF-8)
[WordPressのログインURLを変更する方法！プラグインを使ってセキュリティ対策を｜ワプ活](https://www.conoha.jp/lets-wp/wp-loginurl/)

[設定 - セキュリティ](chrome://settings/security?q=enhanced)

[gitignore.io - プロジェクトに役立つ.gitignoreファイルを作成しよう](https://www.toptal.com/developers/gitignore)

[WordPress｜コアファイルの処理フロー(管理画面編) - わくわくBank](https://www.wakuwakubank.com/posts/657-wordpress-core-manage-flow/)

[index.htmlとは（indexの優先順位も）【初心者向け】 | エンジニア足立のコーディング日記](https://deep-blog.jp/engineer/index-html-priority/)

[WordPress｜コアファイルの処理フロー(管理画面編) - わくわくBank](https://www.wakuwakubank.com/posts/657-wordpress-core-manage-flow/)

[CentOS Stream 9 LAMPサーバインストールメモ【Apache2.4＋MySQL8.0＋PHP8.0】 | あぱーブログ](https://blog.apar.jp/linux/15791/)

[gohugoio/hugo: The world’s fastest framework for building websites.](https://github.com/gohugoio/hugo)

[CentOS 7 firewalld よく使うコマンド - Qiita](https://qiita.com/kenjjiijjii/items/1057af2dddc34022b09e)

[CentOS7でSSHのポート番号を変更する - Qiita](https://qiita.com/fk_2000/items/019b62818e34be973227)

[【find・grep】特定の文字列を含むファイルのリストを取得する方法。 - Qiita](https://qiita.com/pokari_dz/items/0f14a21e3ca3df025d21)

[Postfixのバージョンを確認する](https://www.linuxmaster.jp/linux_skill/2016/10/postfix.html)

[Download and install - The Go Programming Language](https://go.dev/doc/install)

[centos stream 9 に nginx と php8.1 をインストール - Qiita](https://qiita.com/ma7ma7pipipi/items/90000bce1248a41745f8)

[PostgreSQL: Linux downloads (Red Hat family)](https://www.postgresql.org/download/linux/redhat/)

[Install Hugo | Hugo](https://gohugo.io/getting-started/installing/)

[gohugoio/hugo: The world’s fastest framework for building websites.](https://github.com/gohugoio/hugo)

[インストール](https://garretlab.web.fc2.com/hugo/introduction/installation/)

[ローカルgitリポジトリでリモートのリポジトリURL確認方法 - Qiita](https://qiita.com/zhao-xy/items/a35add58575ef7d9d4dc)

[Options | CopyAllURLs](chrome-extension://djdmadneanknadilpjiknlnanaolmbfk/options.html)

[最低限かつムダのないUbuntuサーバー初期設定【VPS】 | ジコログ](https://self-development.info/%E6%9C%80%E4%BD%8E%E9%99%90%E3%81%8B%E3%81%A4%E3%83%A0%E3%83%80%E3%81%AE%E3%81%AA%E3%81%84ubuntu%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E5%88%9D%E6%9C%9F%E8%A8%AD%E5%AE%9A%E3%80%90vps%E3%80%91/)

[ラズベリーパイで固定IPアドレスを設定する - ムギークのブログ](https://mugeek.hatenablog.com/entry/2019/05/27/230256)

[新しい SSH キーを生成して ssh-agent に追加する - GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

[SSH キーのパスフレーズを使う - GitHub Docs](https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)

[ssh-agentを自動起動する - Qiita](https://qiita.com/fuji44/items/da63086c11c772c9f5fb)

[Visual Studio Code Remote Development Troubleshooting Tips and Tricks](https://code.visualstudio.com/docs/remote/troubleshooting#_setting-up-the-ssh-agent)

[メモモモモ: Windowsで始める初めてのSSH](http://memomo2.blogspot.com/2018/06/windowsssh.html)

[クリップボードに値をコピーする : PowerShell プログラミング | iPentec](https://www.ipentec.com/document/powershell-copy-to-clipboard)

[Raspberry Pi 3用Ubuntu MATEのカーネルのアップデート方法 | Memoteki](https://memoteki.net/archives/1206)

[Raspberry Pi ファームウェアとカーネルをバージョンアップ | MIKI-IE.COM（みきいえMIKIIE）](https://www.miki-ie.com/raspberry-pi/raspberry-pi-upgrade-os-firmware/)

[SDカードのフォーマットできないを解決｜初期化・復元の正しい方法 | bitWave](https://bitwave.showcase-tv.com/sd-microsd-format/)

[diskpartコマンドでディスクのパーティションを操作する (2/3) | 「DORA君」転職](http://51.jpis.co.jp/?p=501)

[Raspberry Pi Documentation - The Linux kernel](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#kernel)

[Raspberry Pi 4にUbuntu Serverを入れて初期設定をするまで【簡単なセキュリティを添えて】 - Qiita](https://qiita.com/quailDegu/items/63114ba1e14416df8040)

[Raspberry Pi のIPアドレスを固定にするには？│FABSHOP.JP -デジタルでものづくり！ ファブショップ ！](https://www.fabshop.jp/raspberry-pi-static-ip/)

[Linux kernel release 5.x <http://kernel.org/> — The Linux Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/README.html)

[VM インスタンス – Compute Engine – My First Project – Google Cloud Console](https://console.cloud.google.com/compute/instances?authuser=4&hl=ja&project=resolute-fold-352811)

[Useful_PowerShell/Useful_PowerShell.ps1 at main · enginearn/Useful_PowerShell](https://github.com/enginearn/Useful_PowerShell/blob/main/Useful_PowerShell.ps1)

[Certbot Instructions | Certbot](https://certbot.eff.org/instructions?ws=other&os=ubuntufocal)

[コマンドの出力を「コピペ」したいなら「 xclip 」を使おう！【pbcopy・pbpaste】 | LFI](https://linuxfan.info/xclip)

[Running a notebook server — Jupyter Notebook 6.4.12 documentation](https://jupyter-notebook.readthedocs.io/en/stable/public_server.html)

[Installing snap on Ubuntu | Snapcraft documentation](https://snapcraft.io/docs/installing-snap-on-ubuntu)

[Snap.d error: cannot communicate with server connection refused - snapd - snapcraft.io](https://forum.snapcraft.io/t/snap-d-error-cannot-communicate-with-server-connection-refused/6093/14)

[boot - System has not been booted with systemd as init system (PID 1). Can't operate - Ask Ubuntu](https://askubuntu.com/questions/1379425/system-has-not-been-booted-with-systemd-as-init-system-pid-1-cant-operate)

[shayne/wsl2-hacks: Useful snippets / tools for using WSL2 as a development environment](https://github.com/shayne/wsl2-hacks)

[GitHubでssh接続する手順~公開鍵・秘密鍵の生成から~ - Qiita](https://qiita.com/shizuma/items/2b2f873a0034839e47ce)

[enginearn/Python_for_Algorithmic_Trading_2nd_ed-978-4873119793](https://github.com/enginearn/Python_for_Algorithmic_Trading_2nd_ed-978-4873119793)

[【git エラー解決策】Permission denied (publickey). fatal: Could not read from remote repository. Please make sure you have the correct access rights and the repository exists. が出た時の解決方法 - " いいね " なライフをつくる。](https://tusukuru.hatenablog.com/entry/2018/08/29/021651)

[Error: Permission denied (publickey) - GitHub Docs](https://docs.github.com/ja/authentication/troubleshooting-ssh/error-permission-denied-publickey)

[【Git】リモートレポジトリ(origin)を変更・削除・上書き・追加する方法｜git remote add, remote -v, set-url, rename, rmの使い方（初心者向け、わかりやすい）](https://prograshi.com/general/git/git-remote-commands/)

[docker - Run a script in Dockerfile - Stack Overflow](https://stackoverflow.com/questions/34549859/run-a-script-in-dockerfile)

[innovation1005/python3-for-system-trade: Python3ではじめるシステムトレードのプログラムコードと学習ガイド](https://github.com/innovation1005/python3-for-system-trade)

[Project Jupyter | Installing Jupyter](https://jupyter.org/install)

[yhilpisch/py4at: Jupyter Notebooks and code for the book Python for Algorithmic Trading (O'Reilly) by Yves Hilpisch.](https://github.com/yhilpisch/py4at)

[複数Quandl アカウントをレプリケーション](https://www.cdata.com/jp/kb/tech/quandl-sync-multiple-accounts.rst)

[data_process… (auto-R : 2) - JupyterLab](http://localhost:8888/lab/workspaces/auto-R/tree/Chapter_03/data_processing.ipynb)

['RM' is not recognized as an internal or external command while using Meteor on Windows - Stack Overflow](https://stackoverflow.com/questions/33188752/rm-is-not-recognized-as-an-internal-or-external-command-while-using-meteor-on)

[WordPressでコメント入力時「Invalid CAPTCHA」と出てしまう時の対処法 | MERIDERI.com](https://merideri.com/comment-invalid-captcha)

[マイドライブ - Google ドライブ](https://drive.google.com/drive/u/4/my-drive)

[Account Activation - enginyaaaaan@gmail.com - Gmail](https://mail.google.com/mail/u/4/?tab=om#inbox/FMfcgzGpGdccPCNBJGshpCZRzrSnzNNr)

[Documentation, Help and Support | Nasdaq Data Link](https://data.nasdaq.com/docs-and-help)

[GETTING STARTED](https://docs.data.nasdaq.com/docs/getting-started)

[Nasdaq Data Link Account Profile | Nasdaq Data Link](https://data.nasdaq.com/account/profile)

[API Keys - Google スプレッドシート](https://docs.google.com/spreadsheets/d/13TrFpXzuYeOMLSr-Tvap6xGoXGpEV-yUcpsqYd6YpBs/edit#gid=0)

[Eikon の仕様とダウンロード | リフィニティブ](https://www.refinitiv.com/ja/products/eikon-trading-software/download-eikon)

