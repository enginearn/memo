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
root@GPD-P2-Max:/mnt/c/Users/nagar#
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
  File "/home/nagar/requests_header_encoding.py", line 5, in <module>
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

$ wget https://repo.mysql.com//mysql-apt-config_0.8.22-1_all.deb
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

$ sudo apt update
$ sudo apt upgrade -y
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

$ sudo service apache2 restart
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
> dbconfig-no-thanks dbconfig-common libjs-bootstrap4 libjs-codemirror libjs-jquery libjs-jquery-mousewheel \> libjs-jquery-timepicker libjs-jquery-ui libjs-openlayers php-mysql php-google-recaptcha php-phpmyadmin-motranslator \
> php-phpmyadmin-shapefile php-phpmyadmin-sql-parser php-twig-i18n-extension php-phpseclib php-symfony-config \
> php-symfony-dependency-injection php-symfony-expression-language php-symfony-yaml php-twig php-mariadb-mysql-kbs \
> libjs-sphinxdoc php-bz2 php-tcpdf php-zip
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
$ sudo apt install php-fpm
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
$ sudo apt install libapache2-mod-php8.0
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  php8.0-cli php8.0-common php8.0-opcache php8.0-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  libapache2-mod-php8.0 php8.0-cli php8.0-common php8.0-opcache php8.0-readline
0 upgraded, 5 newly installed, 0 to remove and 0 not upgraded.
Creating config file /etc/php/8.0/apache2/php.ini with new version
libapache2-mod-php8.0: php7.4 module already enabled, not enabling PHP 8.0
Processing triggers for man-db (2.8.5-2) ...
Processing triggers for php8.0-cli (1:8.0.19-1+0~20220517.33+debian10~1.gbpbb919b) ...
Processing triggers for libapache2-mod-php8.0 (1:8.0.19-1+0~20220517.33+debian10~1.gbpbb919b) ...
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
$ sudo a2enmod php8.0
Considering dependency mpm_prefork for php8.0:
Considering conflict mpm_event for mpm_prefork:
Considering conflict mpm_worker for mpm_prefork:
Module mpm_prefork already enabled
Considering conflict php5 for php8.0:
Enabling module php8.0.
To activate the new configuration, you need to run:
  systemctl restart apache2
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

</details>



## git commands

``` git
git rm --cached -r .
```

``` git
git branch -d origin
```

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

``` docker
docker-compose up -d
docker-compose down --volume
```

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
