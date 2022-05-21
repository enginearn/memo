# 雑多なメモたち

``` PowerShell
Hyper-VのON / OFF
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All

Enable-VMEventing
Disable-VMEventing
```

``` PowerShell Python
py -3.10 -m pip install -U pip
```

``` PowerShell Python
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
<summary>Pthon3の確認</summary>

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
