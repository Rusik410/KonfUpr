## Задача 1

grep '.*' /etc/passwd | cut -d: -f1 | sort

adm
at
bin
cron
cyrus
daemon
dhcp
ftp
games
guest
halt
lp
mail
man
news
nobody
ntp
operator
postmaster
root
shutdown
smmsp
squid
sshd
svn
sync
uucp
vpopmail
xfs

## Задача 2

cat /etc/protocols | sort -n -r -k 2 | head -n 5 | awk '{print $2" "$1}'

142 rohc
141 wesp
140 shim6
139 hip
138 manet






























