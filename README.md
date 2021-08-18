## docker alpine

### search

```bash
$ docker search alpine -f is-official=true -f stars=1
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
alpine    A minimal Docker image based on Alpine Linux…   7752      [OK]
```

### pull

```bash
$ docker pull alpine

```

### ash シェル

```bash
docker run -it --name AL02 alpine:latest /bin/ash

/ # ash --help
BusyBox v1.33.1 () multi-call binary.

Usage: ash [-/+OPTIONS] [-/+o OPT]... [-c 'SCRIPT' [ARG0 [ARGS]] / FILE [ARGS] / -s [ARGS]]

Unix shell interpreter
```

### 一般ユーザー作成

ユーザー作成後、ユーザーリストにあるか確認

adduser コマンドで自動でホームディレクトリが作成される

```bash
/ # adduser alpine
Changing password for alpine
New password:
Bad password: too short
Retype password:
passwd: password for alpine changed by root

/ # cat /etc/passwd
root:x:0:0:root:/root:/bin/ash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/mail:/sbin/nologin
news:x:9:13:news:/usr/lib/news:/sbin/nologin
uucp:x:10:14:uucp:/var/spool/uucppublic:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
man:x:13:15:man:/usr/man:/sbin/nologin
postmaster:x:14:12:postmaster:/var/mail:/sbin/nologin
cron:x:16:16:cron:/var/spool/cron:/sbin/nologin
ftp:x:21:21::/var/lib/ftp:/sbin/nologin
sshd:x:22:22:sshd:/dev/null:/sbin/nologin
at:x:25:25:at:/var/spool/cron/atjobs:/sbin/nologin
squid:x:31:31:Squid:/var/cache/squid:/sbin/nologin
xfs:x:33:33:X Font Server:/etc/X11/fs:/sbin/nologin
games:x:35:35:games:/usr/games:/sbin/nologin
cyrus:x:85:12::/usr/cyrus:/sbin/nologin
vpopmail:x:89:89::/var/vpopmail:/sbin/nologin
ntp:x:123:123:NTP:/var/empty:/sbin/nologin
smmsp:x:209:209:smmsp:/var/spool/mqueue:/sbin/nologin
guest:x:405:100:guest:/dev/null:/sbin/nologin
nobody:x:65534:65534:nobody:/:/sbin/nologin
alpine:x:1000:1000:Linux User,,,:/home/alpine:/bin/ash
```

### 一般ユーザー切り替え

```bash
/ # su - alpine
188b92de8384:~$
```

### パッケージ検索

1. vi エディタ

```bash
188b92de8384:~$ which vim
188b92de8384:~$ which vi
/usr/bin/vi

188b92de8384:~$ ls /usr/bin/vi -l
lrwxrwxrwx    1 root     root            12 Aug  5 12:25 /usr/bin/vi -> /bin/busybox
```

### ネットワーク情報

```bash
188b92de8384:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: sit0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN qlen 1000
    link/sit 0.0.0.0 brd 0.0.0.0
20: eth0@if21: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue state UP
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever

```

```bash
188b92de8384:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:16 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:1256 (1.2 KiB)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

### ファイルシステム構造

```bash
188b92de8384:~$ ls -1 /
bin
dev
etc
home
lib
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

```bash
188b92de8384:~$ ls /bin -F
arch@          cp@            egrep@         gzip@          linux64@       more@          ping6@         run-parts@     sync@
ash@           date@          false@         hostname@      ln@            mount@         pipe_progress@ sed@           tar@
base64@        dd@            fatattr@       ionice@        login@         mountpoint@    printenv@      setpriv@       touch@
bbconfig@      df@            fdflush@       iostat@        ls@            mpstat@        ps@            setserial@     true@
busybox*       dmesg@         fgrep@         ipcalc@        lzop@          mv@            pwd@           sh@            umount@
cat@           dnsdomainname@ fsync@         kbd_mode@      makemime@      netstat@       reformime@     sleep@         uname@
chgrp@         dumpkmap@      getopt@        kill@          mkdir@         nice@          rev@           stat@          usleep@
chmod@         echo@          grep@          link@          mknod@         pidof@         rm@            stty@          watch@
chown@         ed@            gunzip@        linux32@       mktemp@        ping@          rmdir@         su@            zcat@

```

名前の最後@記号がついているものは、シンボリックリンク

### パケージ管理コマンド

1. コンテナにインストールされているパッケージ一覧表示

```bash
188b92de8384:~$ apk info -a
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/main: No such file or directory
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/community: No such file or directory
musl
busybox
alpine-baselayout
alpine-keys
libcrypto1.1
libssl1.1
ca-certificates-bundle
libretls
ssl_client
zlib
apk-tools
scanelf
musl-utils
libc-utils

```

### ユーザー切り替え

1. 元のユーザーに戻す場合

```bash
188b92de8384:~$ exit
/ # apk info -a
```

### パケージ更新

```bash
/ # apk search samba
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/main: No such file or directory
WARNING: Ignoring https://dl-cdn.alpinelinux.org/alpine/v3.14/community: No such file or directory
/ # apk update
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/community/x86_64/APKINDEX.tar.gz
v3.14.1-26-g1460b8f70f [https://dl-cdn.alpinelinux.org/alpine/v3.14/main]
v3.14.1-43-gbd086f4217 [https://dl-cdn.alpinelinux.org/alpine/v3.14/community]
OK: 14934 distinct packages available
/ # apk search samba
samba-libs-4.14.5-r0
samba-util-libs-4.14.5-r0
py3-impacket-0.9.22-r1
samba-client-libs-4.14.5-r0
samba-dc-libs-4.14.5-r0
samba-winbind-clients-4.14.5-r0
samba-test-4.14.5-r0
samba-server-openrc-4.14.5-r0
samba-server-4.14.5-r0
samba-dc-4.14.5-r0
samba-libs-py3-4.14.5-r0
samba-server-libs-4.14.5-r0
samba-libnss-winbind-4.14.5-r0
samba-dev-4.14.5-r0
samba-common-tools-4.14.5-r0
samba-common-server-libs-4.14.5-r0
samba-client-4.14.5-r0
samba-4.14.5-r0
libwbclient-4.14.5-r0
samba-pidl-4.14.5-r0
samba-winbind-krb5-locator-4.14.5-r0
samba-doc-4.14.5-r0
samba-winbind-4.14.5-r0
py3-samba-4.14.5-r0
samba-common-4.14.5-r0
acf-samba-0.10.0-r4
```

- apk update
  利用可能パッケージのインデックスを更新

  - これを実行しても、インストールされたパッケージは更新されない
  - これから取ってくるパッケージの参照先を最新にする
  - Docker で使う場合、最初の方に書く

- apk upgrade
  現在インストールされているパッケージをアップグレード

  - 別のパッケージ管理システムの話ではあるが、 Docker ではなるべく使わずに、親 image に upgrade を依頼することを推奨している

### パッケージ Install

```bash
/ # apk -U add bash
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.14/community/x86_64/APKINDEX.tar.gz
(1/4) Installing ncurses-terminfo-base (6.2_p20210612-r0)
(2/4) Installing ncurses-libs (6.2_p20210612-r0)
(3/4) Installing readline (8.1.0-r0)
(4/4) Installing bash (5.1.4-r0)
Executing bash-5.1.4-r0.post-install
Executing busybox-1.33.1-r3.trigger
OK: 8 MiB in 18 packages

/ # apk info bash
bash-5.1.4-r0 description:
The GNU Bourne Again shell

bash-5.1.4-r0 webpage:
https://www.gnu.org/software/bash/bash.html

bash-5.1.4-r0 installed size:
1296 KiB

```

## linux

### 基礎

1. ファイル名
   使える文字は以下の通り

- アルファベット
- 数字
- 記号（「\_」[-]「.」）

  「\*」「!」「?」のような記号（メタキャラクタ）はファイル名やディレクトリに使用してはいけない。
  「.」で始まるファイルは隠しファイル（ユーザー環境やアプリケーションの設定ファイルでよく使用される

2. ファイルの種類

- 通常ファイル
- ディレクトリ
- リンクファイル
  - ファイル名とファイルの実態を紐づけたファイル
  - シンボリックリンクとハードリンクがある
- 特殊ファイル
  - あらゆるデバイスをファイルとして抽象かして扱う
  - プリンタに対応するデバイスファイルにデータを書き込むとプリンタから出力されるなど、ファイルを通じてデバイスを扱える

3. ファイル一覧

```bash
/tmp # ls -l
total 0
-rw-r--r--    1 root     root             0 Aug 18 14:56 test.txt
```

ls コマンドで表示された項目は以下の通り。

| 項目         | 意味                   |
| ------------ | ---------------------- |
| -rw-r--r--   | ファイルモード         |
| 1            | リンク数               |
| root         | ファイルの所有者       |
| root         | ファイルの所有グループ |
| 0            | ファイルサイズ         |
| Aug 18 14:56 | 最終更新日時           |
| test.txt     | ファイル名             |

ファイルモードの左端の１文字目はファイルの種類
| 文字 | 説明 |
| ------------ | ---------------------- |
|-|通常ファイル|
|d|ディレクトリ|
|l|リンクファイル|
|c|特殊ファイル（キャラクデバイスファイル|
|b|特殊ファイル（ブロックデバイスファイル|

3. 相対パス
   | 記号 | 説明 |
   | ------------ | ---------------------- |
   |.|ドット カレントディレクトリ|
   |..|１つ上のディレクトリ|
   |~|ホームディレクトリ|

4. ディレクトリ構成

| ディレクトリ | 説明                                           |
| ------------ | ---------------------------------------------- |
| bin          | 一般ユーザーが使える基本コマンド               |
| boot         | Linux カーネルなど軌道に必要なファイル         |
| dev          | デバイスファイル                               |
| etc          | システム設定ファイルやサービス起動ファイル     |
| home         | ユーザーのホームディレクトリ                   |
| lib          | ライブラリファイル                             |
| lost+found   | 破損ファイルの断片を格納                       |
| media        | 外付けストレージやメディア用のマウントポイント |
| mnt          | 一時的に使われるマウントポイント               |
| opt          | オプション的なソフトウェアのインストール先     |
| proc         | プロセス情報を扱う特殊ディレクトリ             |
| root         | root ユーザーのホームディレクトリ              |
| run          | 実行中のプログラムやシステム情報のデータ       |
| sbin         | システム管理者が利用する基本コマンド           |
| srv          | ホスト固有のサービス情報データ                 |
| swap         | スワップ用                                     |
| sys          | システム情報を扱う特殊なディレクトリ           |
| tmp          | 一時ファイル置き場                             |
| usr          | プログラムやライブラリなど                     |
| var          | ログファイルなど頻繁に更新されるファイル       |

5. ファイル表示

- cat(conCATenate) コマンド

  - text ファイルの内容を表示する

  ```bash
  / # cat etc/motd
  Welcome to Alpine!

  The Alpine Wiki contains a large amount of how-to guides and general
  information about administrating Alpine systems.
  See <http://wiki.alpinelinux.org/>.

  You can setup the system with the command: setup-alpine

  You may change this message by editing /etc/motd.

  ```

- less
  - 1 画面では収まりきらない大きなファイルを表示する場合使用する
  - テキストファイルの内容を１ページずつ表示
    ```bash
      /# less /etc/services
    ```
  - コマンドのキー操作
    - ↓ :1 行下にスクロール
    - ↑:1 行 ↑ にスクロール
    - スペース :1 画面下方向に進める
    - ctrl + b :1 画面 ↑ 方向に進める
    - q :less 終了
