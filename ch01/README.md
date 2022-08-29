## 계정관련 명령어

### alias
- `alias [별명='명령어']`
- `alias c='cal'`
```
[root@79861411cd80 /]# alias c='cal'
[root@79861411cd80 /]# c
     August 2022
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```

### unalias
- `unalias [option][단축명령어]`
- 옵션 -a: 설정된 모든 alias 해제
```
[root@79861411cd80 /]# alias c='cal'
[root@79861411cd80 /]# c
     August 2022
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31

[root@79861411cd80 /]# alias d='cal'
[root@79861411cd80 /]# d
     August 2022
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31


[root@79861411cd80 /]# unalias c
[root@79861411cd80 /]# c
bash: c: command not found
[root@79861411cd80 /]# unalias -a
[root@79861411cd80 /]# c
bash: c: command not found
[root@79861411cd80 /]# d
bash: d: command not found
```

### which
- $PATH가 설정되어 있는 경로에서만 해당명령어로 경로 탐색
- $PATH: 실행 파일들의 디렉토리 위치를 저장 해놓은 환경변수
```
[root@79861411cd80 /]# which cal
bash: which: command not found
[root@79861411cd80 /]# yum install which
Loaded plugins: fastestmirror, ovl
Determining fastest mirrors
 * base: mirror.worria.com
 * extras: mirrors.bfsu.edu.cn
 * updates: mirrors.bfsu.edu.cn
base                                         | 3.6 kB     00:00
extras                                       | 2.9 kB     00:00
updates                                      | 2.9 kB     00:00
(1/4): base/7/aarch64/group_gz                 | 153 kB   00:00
(2/4): extras/7/aarch64/primary_db             | 250 kB   00:00
(3/4): base/7/aarch64/primary_db               | 4.9 MB   00:01
(4/4): updates/7/aarch64/primary_db            | 3.3 MB   00:06
Resolving Dependencies
--> Running transaction check
---> Package which.aarch64 0:2.20-7.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================
 Package      Arch           Version              Repository   Size
====================================================================
Installing:
 which        aarch64        2.20-7.el7           base         40 k

Transaction Summary
====================================================================
Install  1 Package

Total download size: 40 k
Installed size: 119 k
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/aarch64/7/base/packages/which-2.20-7.el7.aarch64.rpm: Header V4 RSA/SHA1 Signature, key ID 305d49d6: NOKEY
Public key for which-2.20-7.el7.aarch64.rpm is not installed
which-2.20-7.el7.aarch64.rpm                   |  40 kB   00:00
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-9.2009.0.el7.centos.aarch64 (@instCentOS)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Is this ok [y/N]: y
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7-aarch64
Importing GPG key 0x305D49D6:
 Userid     : "CentOS AltArch SIG - AArch64 (http://wiki.centos.org/SpecialInterestGroup/AltArch/AArch64) <security@centos.org>"
 Fingerprint: ef8f 3ca6 6efd f32b 36cd adf7 6c7c b6ef 305d 49d6
 Package    : centos-release-7-9.2009.0.el7.centos.aarch64 (@instCentOS)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7-aarch64
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : which-2.20-7.el7.aarch64                         1/1
install-info: No such file or directory for /usr/share/info/which.info.gz
  Verifying  : which-2.20-7.el7.aarch64                         1/1

Installed:
  which.aarch64 0:2.20-7.el7

Complete!
```
```
[root@79861411cd80 /]# which cal
/usr/bin/cal
```

### man
- 옵션
    - h: 사용법 출력
    - k: 해당 키워드로 발견되는 모든 매뉴얼의 내용을 검색(apropos와 동일)
    - w: man 명령 실행 시 호출되는 메뉴얼 페이지 파일의 위치를 보여줌
```
[root@79861411cd80 /]# man cal
bash: man: command not found
[root@79861411cd80 /]# yum install man -y
Loaded plugins: fastestmirror, ovl
Loading mirror speeds from cached hostfile
 * base: mirror.worria.com
 * extras: mirrors.bfsu.edu.cn
 * updates: mirrors.bfsu.edu.cn
Resolving Dependencies
--> Running transaction check
---> Package man-db.aarch64 0:2.6.3-11.el7 will be installed
--> Processing Dependency: less for package: man-db-2.6.3-11.el7.aarch64
--> Processing Dependency: groff-base for package: man-db-2.6.3-11.el7.aarch64
--> Processing Dependency: libpipeline.so.1()(64bit) for package: man-db-2.6.3-11.el7.aarch64
--> Running transaction check
---> Package groff-base.aarch64 0:1.22.2-8.el7 will be installed
---> Package less.aarch64 0:458-9.el7 will be installed
---> Package libpipeline.aarch64 0:1.2.3-3.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================
 Package          Arch         Version              Repository
                                                               Size
====================================================================
Installing:
 man-db           aarch64      2.6.3-11.el7         base      826 k
Installing for dependencies:
 groff-base       aarch64      1.22.2-8.el7         base      920 k
 less             aarch64      458-9.el7            base      115 k
 libpipeline      aarch64      1.2.3-3.el7          base       52 k

Transaction Summary
====================================================================
Install  1 Package (+3 Dependent packages)

Total download size: 1.9 M
Installed size: 6.7 M
Downloading packages:
(1/4): less-458-9.el7.aarch64.rpm              | 115 kB   00:00
(2/4): libpipeline-1.2.3-3.el7.aarch64.rpm     |  52 kB   00:00
(3/4): man-db-2.6.3-11.el7.aarch64.rpm         | 826 kB   00:00
(4/4): groff-base-1.22.2-8.el7.aarch64.rpm     | 920 kB   00:06
--------------------------------------------------------------------
Total                                  291 kB/s | 1.9 MB  00:06
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : groff-base-1.22.2-8.el7.aarch64                  1/4
  Installing : less-458-9.el7.aarch64                           2/4
  Installing : libpipeline-1.2.3-3.el7.aarch64                  3/4
  Installing : man-db-2.6.3-11.el7.aarch64                      4/4
  Verifying  : man-db-2.6.3-11.el7.aarch64                      1/4
  Verifying  : libpipeline-1.2.3-3.el7.aarch64                  2/4
  Verifying  : groff-base-1.22.2-8.el7.aarch64                  3/4
  Verifying  : less-458-9.el7.aarch64                           4/4

Installed:
  man-db.aarch64 0:2.6.3-11.el7

Dependency Installed:
  groff-base.aarch64 0:1.22.2-8.el7     less.aarch64 0:458-9.el7
  libpipeline.aarch64 0:1.2.3-3.el7

Complete!
```
```
[root@79861411cd80 /]# man ls
No manual entry for ls
```
- 문제 발생
    - docker를 통해 centos를 실행하면 man page를 찾지 못함
- 원인
    - docker에서 처음 컨테이너를 생성할 때, 기본값으로 문서를 제외함
- 해결
    - docker 컨테이너 실행
    - root 계정
    - vi /etc/yum.conf
    - 14 line tsflags=nodocs 를 주석처리함
    - man page가 필요한 패키지를 재설치해야함
```
yum reinstall which

설치 후 
man which 하면 잘됨
```

### info
- man 처럼 매뉴얼 조회(man 만큼 사용 빈도는 적음)

### whatis
- 명령어에 대한 간략한 기능 설명
```
[root@79861411cd80 /]# whatis which
which: nothing appropriate.
```
- 문제
    - 참조하는 man page가 없기때문
- 해결
```
[root@79861411cd80 /]# mandb
Processing manual pages under /usr/share/man...
Updating index cache for path `/usr/share/man/mann'. Wait...done.
Checking for stray cats under /usr/share/man...
Checking for stray cats under /var/cache/man...
Processing manual pages under /usr/local/share/man...
Updating index cache for path `/usr/local/share/man/mann'. Wait...done.
Checking for stray cats under /usr/local/share/man...
Checking for stray cats under /var/cache/man/local...
41 man subdirectories contained newer manual pages.
1 manual page was added.
0 stray cats were added.
0 old database entries were purged.
```
```
[root@79861411cd80 /]# whatis which
which (1)            - shows the full path of (shell) commands.
```

### manpath
- man 명령이 참조하는 매뉴얼 페이지의 경로 표시
```
[root@79861411cd80 /]# manpath
/usr/local/share/man:/usr/share/man
```

### whereis
- 찾는 명령어의 실행파일 절대경로 소스, 설정파일 및 매뉴얼 페이지 출력
```
[root@79861411cd80 /]# whereis cal
cal: /usr/bin/cal
```

### apropos
- man 페이지 설정에서 지정한 키워드를 포함하고 있는 명령어