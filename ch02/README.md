## 사용자 생성 관련 명령어

### useradd
- 새로운 계정의 홈 디렉토리: /home/계정명
- 옵션
    - s: 로그인 시 사용할 기본 쉘 지정
    - d: 사용자의 홈 디렉토리 지정
    - e: 계정만기일 지정
    - f: 계정유효일 지정
    - c: comment
    - G: 2차 그룹의 GID
```
[root@79861411cd80 /]# useradd userA
```

### passwd
- /etc/shadow 파일안에 기록
- 옵션
    - S: 계정 상태표시(PS: 정상, NP: 패스워드 없음, LK: 계정 잠김)
    - d: 패스워드 삭제
    - l: 계정을 lock 상태로 변경
    - u: 계정의 lock 상태 해제
```
[root@79861411cd80 /]# passwd -S userA
userA LK 2022-08-29 0 99999 7 -1 (Password locked.)
```
```
[root@79861411cd80 /]# passwd userA
Changing password for user userA.
New password:
BAD PASSWORD: The password is shorter than 7 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[root@79861411cd80 /]# passwd -S userA
userA PS 2022-08-29 0 99999 7 -1 (Password set, SHA512 crypt.)
```
```
[root@79861411cd80 /]# passwd -d userA
Removing password for user userA.
passwd: Success
[root@79861411cd80 /]# passwd -S userA
userA NP 2022-08-29 0 99999 7 -1 (Empty password.)
```

### whoami
```
[root@79861411cd80 /]# whoami
root
```

### su
- 로그아웃하지 않고 다른 계정으로 로그인하여 사용자 권한을 획득하기 위한 명령어
- switch user | substitute user

### 사용자 관련 파일

#### /etc/default/useradd
- useradd로 추가된 사용자 계정의 정보파일
```
[root@79861411cd80 /]# cat /etc/default/useradd
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```
#### /etc/passwd
- 계정의 정보파일
- 정보의 구분은 : 으로 함
```
[root@79861411cd80 /]# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
userA:x:1000:1000::/home/userA:/bin/bash
```

#### /etc/shadow
- 계정의 패스워드가 암호화 되어있는 파일
```
[root@79861411cd80 /]# cat /etc/shadow
root:locked::0:99999:7:::
bin:*:18353:0:99999:7:::
daemon:*:18353:0:99999:7:::
adm:*:18353:0:99999:7:::
lp:*:18353:0:99999:7:::
sync:*:18353:0:99999:7:::
shutdown:*:18353:0:99999:7:::
halt:*:18353:0:99999:7:::
mail:*:18353:0:99999:7:::
operator:*:18353:0:99999:7:::
games:*:18353:0:99999:7:::
ftp:*:18353:0:99999:7:::
nobody:*:18353:0:99999:7:::
systemd-network:!!:18579::::::
dbus:!!:18579::::::
userA:$6$vThxcYhH$4PgucbWB6RiUnnBdQPI.4JS0oJQWEJnmGCAF//ocjLczJ.NRMl096WSsn3CNf7jTkDeWZGVVuhHoqEkP.ffiu1:19233:0:99999:7:::
```

#### /etc/login.defs
- 사용자 계정 설정과 관련된 기본 값들을 정의한 파일
```
[root@79861411cd80 /]# cat /etc/login.defs
#
# Please note that the parameters in this configuration file control the
# behavior of the tools from the shadow-utils component. None of these
# tools uses the PAM mechanism, and the utilities that use PAM (such as the
# passwd command) should therefore be configured elsewhere. Refer to
# /etc/pam.d/system-auth for more information.
#

# *REQUIRED*
#   Directory where mailboxes reside, _or_ name of file, relative to the
#   home directory.  If you _do_ define both, MAIL_DIR takes precedence.
#   QMAIL_DIR is for Qmail
#
#QMAIL_DIR	Maildir
MAIL_DIR	/var/spool/mail
#MAIL_FILE	.mail

# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password changes.
#	PASS_MIN_LEN	Minimum acceptable password length.
#	PASS_WARN_AGE	Number of days warning given before a password expires.
#
PASS_MAX_DAYS	99999
PASS_MIN_DAYS	0
PASS_MIN_LEN	5
PASS_WARN_AGE	7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN                  1000
UID_MAX                 60000
# System accounts
SYS_UID_MIN               201
SYS_UID_MAX               999

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                  1000
GID_MAX                 60000
# System accounts
SYS_GID_MIN               201
SYS_GID_MAX               999

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD	/usr/sbin/userdel_local

#
# If useradd should create home directories for users by default
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#
CREATE_HOME	yes

# The permission mask is initialized to this value. If not specified,
# the permission mask will be initialized to 022.
UMASK           077

# This enables userdel to remove user groups if no members exist.
#
USERGROUPS_ENAB yes

# Use SHA512 to encrypt password.
ENCRYPT_METHOD SHA512
```

## 사용자 계정 관리 명령어

### usermod
- /home에 위치한 사용자들의 정보를 변경하는 명령어
- 사용자의 홈디렉토리 변경, 그룹변경, 유효기간 병경 등
- root 계정만 가능
- 옵션
    - d 홈디렉토리: 새로운 홈디렉토리 지정, -m 옵션과 같이 쓰면 새로 생성
    - G: 새로운 보조 그룹 지정, 기본 그룹에 포함된 상태에서 새그룹에 추가

### userdel
- 기존의 계정정보를 삭제
- /etc/passwd, /etc/shadow, /etc/group에서 해당 정보를 삭제
```
[root@79861411cd80 /]# cat /etc/passwd | grep userA
userA:x:1000:1000::/home/userA:/bin/bash
[root@79861411cd80 /]# userdel userA
[root@79861411cd80 /]# cat /etc/passwd | grep userA
[root@79861411cd80 /]#
```

### chage
- 패스워드 만료 정보를 변경
```
[root@79861411cd80 /]# adduser abc
[root@79861411cd80 /]# passwd abc
Changing password for user abc.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[root@79861411cd80 /]# passwd -S abc
abc PS 2022-08-29 0 99999 7 -1 (Password set, SHA512 crypt.)
[root@79861411cd80 /]# chage abc -l
Last password change					: Aug 29, 2022
Password expires					: never
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
```


## 그룹관리 명령어

### groupadd
- 새로운 그룹을 생성
- /etc/group 에서 그룹명 확인
    - 그룹명:암호:GID:맴버들
```
[root@79861411cd80 /]# cat /etc/group
root:x:0:
bin:x:1:
daemon:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mem:x:8:
kmem:x:9:
wheel:x:10:
cdrom:x:11:
mail:x:12:
man:x:15:
dialout:x:18:
floppy:x:19:
games:x:20:
tape:x:33:
video:x:39:
ftp:x:50:
lock:x:54:
audio:x:63:
nobody:x:99:
users:x:100:
utmp:x:22:
utempter:x:35:
input:x:999:
systemd-journal:x:190:
systemd-network:x:192:
dbus:x:81:
abc:x:1000:
```
```
[root@79861411cd80 /]# tail -2 /etc/group
dbus:x:81:
abc:x:1000:
```

### groupdel
- 기존 그룹을 삭제

### groupmod
- 그룹의 설정을 변경
- 그룹명, GID를 변경
- 옵션
    - n: 그룹명으로 변경
    - g: 그룹 GID 변경
```
groupmod -n
```