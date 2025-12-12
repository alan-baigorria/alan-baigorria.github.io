---
title: "🎄 [Linux CLI + Side Quest 1] Advent of Cyber 2025 - Try Hack Me"
date: 2025-12-11 18:30:00 -0300
categories: [write-up,ctf]
tags: [ctf,tryhackme,intro]
---
> En este room vamos a ver comandos de Linux.
{: .prompt-tip }

# Linux CLI (facil)

<img width="719" height="572" alt="image" src="https://github.com/user-attachments/assets/53f4e7b1-59e0-4406-870d-0d3247dd8db4" />

## Task 1
Nos explica como conectarnos a la MV

## Task 2: Linux CLI

<img width="1160" height="391" alt="image" src="https://github.com/user-attachments/assets/4dc0f9fa-9605-4aba-b0a7-06cff4840579" />

En esta task nos ensenan comandos importantes a la hora de movernos en Linux.
`ls`
Listar archivos/carpetas

`ls -la`
Listar archivos/carpetas ocultas.

`cd`
Moverse entre carpetas

`grep "Failed password" auth.log`
Grep nos permite buscar cadenas de texto dentro de un archivo

`find /home/socmas -name *egg*`
Find nos permite buscar archivos en X ruta que contenga Y nombre, en este caso buscamos en /home/socmas cualquier archivo llamado egg.


Cada uno de estos comandos se puede consultar su documentacion desde cualquier terminal con Linux usando `man` por ejemplo:
man find
<img width="1052" height="639" alt="image" src="https://github.com/user-attachments/assets/593d99aa-afea-41cb-acff-d30246e374b3" />

Nota mental: agregar documentacion de ayuda al script que cree dnscanner.sh

Nos da una breve resena de como usar
`|`
`>`
`&&`
Operadores muy importantes a la hora de manejarse en linux, que se pueden combinar.

System utilities
cat
uptime
sudo
sudo su(ilegal q ensenen este)
whoami



## Task 1: respuestas
Which CLI command would you use to list a directory? 
LS

Which command helped you filter the logs for failed logins?
grep


Which command would you run to switch to the root user?
SUDO SU

Finally, what flag did Sir Carrotbane leave in the root bash history?

<img width="831" height="837" alt="image" src="https://github.com/user-attachments/assets/c959d2d1-b075-4821-be23-84cc8c1633bf" />


sudo su
cd /root/
THM{until-we-meet-again}1


# Side-Quest 1 (para mi dificil)
## Primera Flag
cd /home/mcskidy/Documents/ 

El loco nos dejo una biblia:
```
from: mcskidy
To: whoever finds this

I had a short second when no one was watching. I used it.

I've managed to plant a few clues around the account.
If you can get into the user below and look carefully,
those three little "easter eggs" will combine into a passcode
that unlocks a further message that I encrypted in the
/home/eddi_knapp/Documents/ directory.
I didn't want the wrong eyes to see it.

Access the user account:
username: eddi_knapp
password: S0mething1Sc0ming

There are three hidden easter eggs.
They combine to form the passcode to open my encrypted vault.

Clues (one for each egg):

1)
I ride with your session, not with your chest of files.
Open the little bag your shell carries when you arrive.

2)
The tree shows today; the rings remember yesterday.
Read the ledger’s older pages.

3)
When pixels sleep, their tails sometimes whisper plain words.
Listen to the tail.

Find the fragments, join them in order, and use the resulting passcode
to decrypt the message I left. Be careful — I had to be quick,
and I left only enough to get help.

~ McSkidy
```

Lo primero que voy a hacer es abrir el historial de comandos a ver que nos sale
cd /home/mcskidy
cat .bash_history

<img width="550" height="174" alt="image" src="https://github.com/user-attachments/assets/d78c85d1-d566-4802-91e3-e3adbf7d52c5" />


Hay una guia oculta

<img width="634" height="230" alt="image" src="https://github.com/user-attachments/assets/44eaa6ca-d9dd-428c-b288-1b281f888d68" />

Tenemos nuestra primera flag
THM{learning-linux-cli}

## Segunda flag:
grep "egg" auth.log

<img width="1251" height="465" alt="image" src="https://github.com/user-attachments/assets/f89244c0-729b-4ae8-ac9d-6991d2696e72" />

Si analizamos este registro vemos que se esta intentando conectar por ssh al dominio que sale ahi con ese puerto, nosotros teniamos una credencial asi que lo vamos a intentar.

No funciona el ssh.

Entro a localhost a ver que hay

<img width="1161" height="792" alt="image" src="https://github.com/user-attachments/assets/1220f472-4331-4222-93c9-91fd480c088a" />

Sale error 405

Siendo honesto no estaba leyendo el post, pero resulta que hay un script que tenemos que analizar 

<img width="627" height="526" alt="image" src="https://github.com/user-attachments/assets/e434f819-b274-4b59-96c8-53df4a65e0e6" />

Creia que era complicado pero es entrar y hacer cat solamente

mcskidy@tbfc-web01:~$ cd /home/socmas/2025
mcskidy@tbfc-web01:~$ cat eggstrike.sh

<img width="615" height="330" alt="image" src="https://github.com/user-attachments/assets/e06e1bac-d231-4baa-8ce8-f18e52fd8101" />

THM{sir-carrotbane-attacks}

Vamos a entrar a:
http://10.66.147.161:8080

<img width="1158" height="826" alt="image" src="https://github.com/user-attachments/assets/a09e2413-bc0c-4b5c-9922-a2935bb25ab7" />

Si nos deja ver la pagina web ahora.

<img width="638" height="333" alt="image" src="https://github.com/user-attachments/assets/57abcd34-aa1d-44c5-9f4f-5ba3d0e3d1de" />

Analizamos el codigo vemos que hay un /secret.

Vamos a ver la carpeta del usuario este que sale en los logs de mcskidy

<img width="667" height="339" alt="image" src="https://github.com/user-attachments/assets/cc8e7cae-d577-46f5-8118-d7dc2451b046" />

ls -la

<img width="939" height="752" alt="image" src="https://github.com/user-attachments/assets/ba73d417-bc64-49f5-ad9c-deb9dde658c0" />

Hay muchos archivos ocultos vamos a entrar en la carpeta fix.

```
root@tbfc-web01:/home/eddi_knapp/fix_passfrag_backups_20251111162432$ ls -la
total 28
drwxrwxr-x  2 eddi_knapp eddi_knapp 4096 Nov 11 16:24 .
drwxr-x--- 18 eddi_knapp eddi_knapp 4096 Dec  1 08:52 ..
-rw-r--r--  1 eddi_knapp eddi_knapp 3797 Nov 11 16:19 .bashrc.bak
-rw-r--r--  1 eddi_knapp eddi_knapp 3797 Nov 11 16:19 .bashrc.pre_replace
-rw-------  1 eddi_knapp eddi_knapp   19 Nov 11 16:19 .pam_environment.bak
-rw-r--r--  1 eddi_knapp eddi_knapp  833 Nov 11 16:19 .profile.bak
-rw-r--r--  1 eddi_knapp eddi_knapp  833 Nov 11 16:19 .profile.pre_replace
```

en bash pre replace vemos un pedazo de una flag?
export PASSFRAG1="3ast3r"

en .profile.bak tambien
export PASSFRAG1="3ast3r"

Buscamos la pass con
grep -r "PASSFRAG" 

<img width="1308" height="451" alt="image" src="https://github.com/user-attachments/assets/54a0d13b-d5c0-433f-b9f7-dc82aa67db75" />


Reslta un archivo llamado fix_passfrag.sh

Clickee en la pista porque ando medio perdido, y tengo que buscar un archivo .secret en teoria.


<img width="538" height="142" alt="image" src="https://github.com/user-attachments/assets/2524f762-398f-4e8c-95e4-83ed6fe5c40c" />

dir.tar.gz.gpg

Vamos a intentar desencriptarlo.


<img width="616" height="445" alt="image" src="https://github.com/user-attachments/assets/cb5f16b2-c3b8-4502-aec6-fb6fe5e2d220" />


Necesitamos una contrasena que no tenemos.

Probablemente ahi este la flag final.

Vamos a buscar cualquier archivo o carpeta .secret a ver si encontramos otra pista.

sudo find / \( -type f -o -type d \) -name '*\.secret*' 2>/dev/null

<img width="798" height="196" alt="image" src="https://github.com/user-attachments/assets/e1b778a3-623f-45bb-9764-02e3b1e8e763" />

Encontramos tres.

Nunca en mi vida he usado git asi que le pregunto a mi profesor:

<img width="1110" height="559" alt="image" src="https://github.com/user-attachments/assets/dc7644e3-9577-4498-847f-d3c146bd1607" />

VEmos que hay un dato ahi

<img width="685" height="266" alt="image" src="https://github.com/user-attachments/assets/33b2d666-7e94-44de-b8fd-db5618f341d4" />


Como no tengo ni idea de git le pregunto de nuevo a mi profesor

<img width="1062" height="615" alt="image" src="https://github.com/user-attachments/assets/88d2ddea-d714-4284-af3e-ebbc71ac15ef" />

git show e924698378132991ee08f050251242a092c548fd
<img width="748" height="413" alt="image" src="https://github.com/user-attachments/assets/fe5b2a8b-9853-43b2-b153-d5a89bf75406" />


PASSFRAG2: -1s-

git show d12875c8b62e089320880b9b7e41d6765818af3d

<img width="722" height="417" alt="image" src="https://github.com/user-attachments/assets/562d7d3b-95fa-474e-8fba-8da5c03e18f7" />


Vemos el mismo
PASSFRAG2: -1s

Hasta ahora hay 2 fragmentos. Nos falta uno.

## Tercera flag:

When pixels sleep, their tails sometimes whisper plain words.
Listen to the tail.

pixeles = fotos?

Abro caja(gestor de archivo) como sudo a ver que vemos
<img width="756" height="836" alt="image" src="https://github.com/user-attachments/assets/92acdde7-fcda-436b-9acc-53ad48830c2d" />

Hay uina foto que es diferente llamada easter.png, probablemente sea esa.

La abro con vim a ver si hay algo en texto plano:
vim easter.png
<img width="751" height="528" alt="image" src="https://github.com/user-attachments/assets/7163022b-7cb7-48a5-b449-97e4d32ac032" />

No hay nada, vamos a intentar con exim.
Haciendo ls -la en Pictures vemos unos archivos ocultos.

<img width="759" height="537" alt="image" src="https://github.com/user-attachments/assets/2e29454c-ecf6-4a09-8eac-7f4ccc18523b" />


Encontramos la flag!
```

root@tbfc-web01:/home/eddi_knapp/Pictures$ cat .easter_egg 

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@%%%%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@#+==+*@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@%+=+*++@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@*++**+#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@%%#*====+#%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@#*===-===#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@%*++:-+====*%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@%*===++++===-+*#######%%@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@%*+===+++==::-=========+*#%@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@%%#**+======-:-==--==-==+*%@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@%*+======---=+===------=#%@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@%**+=-=====-==+==-====--=*%@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@%***+++==--=====+=----=-=#@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%#**++=--=====++====----*@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@%*+=-:=++**++**+=-::--*@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@#+=:.+#***=*#=--::-=-=%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@%%*+-:+%#+++=++=:::==--*%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%*+=--*@#++===::::::::=#%@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@%%%##*#%%%####***#*#####%%@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@%%###%%%%%%%%%%##%%##%%@@@@@@@@@@@@

~~ HAPPY EASTER ~~~
PASSFRAG3: c0M1nG
```

Tenemos los tres fragmentos.

3ast3r-1sc0M1nG

Vamos intentar abrir el archivo que nos pedia una contrasena

gpg --batch --passphrase "3ast3r-1s-c0M1nG" -d dir.tar.gz.gpg

<img width="752" height="546" alt="image" src="https://github.com/user-attachments/assets/0d67bfcd-1ffa-4107-9e77-c2bfc560dea1" />


 No funciono.


Busco algun otro archivo como ese con find y me dio esto

/home/eddi_knapp/.secret/dir.tar.gz.gpg
home/eddi_knapp/mcskidy_note.txt.gpg

Vamos a intentar abrir el archivo .gpg con la frase que tenemos.

gpg --batch --passphrase "3ast3r-1s-c0M1nG" -d dir.tar.gz.gpg
```

root@tbfc-web01:/home/eddi_knapp/Documents$ gpg --batch --passphrase "3ast3r-1s-c0M1nG" -d mcskidy_note.txt.gpg 
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
Congrats — you found all fragments and reached this file.

Below is the list that should be live on the site. If you replace the contents of
/home/socmas/2025/wishlist.txt with this exact list (one item per line, no numbering),
the site will recognise it and the takeover glitching will stop. Do it — it will save the site.

Hardware security keys (YubiKey or similar)
Commercial password manager subscriptions (team seats)
Endpoint detection & response (EDR) licenses
Secure remote access appliances (jump boxes)
Cloud workload scanning credits (container/image scanning)
Threat intelligence feed subscription

Secure code review / SAST tool access
Dedicated secure test lab VM pool
Incident response runbook templates and playbooks
Electronic safe drive with encrypted backups

A final note — I don't know exactly where they have me, but there are *lots* of eggs
and I can smell chocolate in the air. Something big is coming.  — McSkidy

---

When the wishlist is corrected, the site will show a block of ciphertext. This ciphertext can be decrypted with the following unlock key:

UNLOCK_KEY: 91J6X7R4FQ9TQPM9JX2Q9X2Z

To decode the ciphertext, use OpenSSL. For instance, if you copied the ciphertext into a file /tmp/website_output.txt you could decode using the following command:

cat > /tmp/website_output.txt
openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 -salt -base64 -in /tmp/website_output.txt -out /tmp/decoded_message.txt -pass pass:'91J6X7R4FQ9TQPM9JX2Q9X2Z'
cat /tmp/decoded_message.txt

Sorry to be so convoluted, I couldn't risk making this easy while King Malhare watches. — McSkidy
```

Tenemos la ultima pista que necesitamos?

Nos da una salt (UNLOCK_KEY)

Tenemos que arreglar la pagina que visitamos antes.

Vamos a reemplazar la wishlist.
Vamos a la carpeta de socmas
nano wishlist.txt


<img width="710" height="456" alt="image" src="https://github.com/user-attachments/assets/0ef1697f-8f09-4605-a93e-ee638643532f" />

<img width="1138" height="799" alt="image" src="https://github.com/user-attachments/assets/76d10d3b-f505-4a29-8787-acd43808a100" />

El sitio nos da un mensaje para decodificar con la salta que teniamos antes:
U2FsdGVkX1/7xkS74RBSFMhpR9Pv0PZrzOVsIzd38sUGzGsDJOB9FbybAWod5HMsa+WIr5HDprvK6aFNYuOGoZ60qI7axX5Qnn1E6D+BPknRgktrZTbMqfJ7wnwCExyU8ek1RxohYBehaDyUWxSNAkARJtjVJEAOA1kEOUOah11iaPGKxrKRV0kVQKpEVnuZMbf0gv1ih421QvmGucErFhnuX+xv63drOTkYy15s9BVCUfKmjMLniusI0tqs236zv4LGbgrcOfgir+P+gWHc2TVW4CYszVXlAZUg07JlLLx1jkF85TIMjQ3B91MQS+btaH2WGWFyakmqYltz6jB5DOSCA6AMQYsqLlx53ORLxy3FfJhZTl9iwlrgEZjJZjDoXBBMdlMCOjKUZfTbt3pnlHWEaGJD7NoTgywFsIw5cz7hkmAMxAIkNn/5hGd/S7mwVp9h6GmBUYDsgHWpRxvnjh0s5kVD8TYjLzVnvaNFS4FXrQCiVIcp1ETqicXRjE4T0MYdnFD8h7og3ZlAFixM3nYpUYgKnqi2o2zJg7fEZ8c=

Le preguntamos al profesor de nuevo:

<img width="1140" height="693" alt="image" src="https://github.com/user-attachments/assets/27cf1d1f-04ba-4b1a-a3c1-a4bdaff0cde0" />

echo 'U2FsdGVkX1/7xkS74RBSFMhpR9Pv0PZrzOVsIzd38sUGzGsDJOB9FbybAWod5HMsa+WIr5HDprvK6aFNYuOGoZ60qI7axX5Qnn1E6D+BPknRgktrZTbMqfJ7wnwCExyU8ek1RxohYBehaDyUWxSNAkARJtjVJEAOA1kEOUOah11iaPGKxrKRV0kVQKpEVnuZMbf0gv1ih421QvmGucErFhnuX+xv63drOTkYy15s9BVCUfKmjMLniusI0tqs236zv4LGbgrcOfgir+P+gWHc2TVW4CYszVXlAZUg07JlLLx1jkF85TIMjQ3B91MQS+btaH2WGWFyakmqYltz6jB5DOSCA6AMQYsqLlx53ORLxy3FfJhZTl9iwlrgEZjJZjDoXBBMdlMCOjKUZfTbt3pnlHWEaGJD7NoTgywFsIw5cz7hkmAMxAIkNn/5hGd/S7mwVp9h6GmBUYDsgHWpRxvnjh0s5kVD8TYjLzVnvaNFS4FXrQCiVIcp1ETqicXRjE4T0MYdnFD8h7og3ZlAFixM3nYpUYgKnqi2o2zJg7fEZ8c=
' | openssl enc -d -a -aes-256-cbc -pbkdf2 -pass pass:'91J6X7R4FQ9TQPM9JX2Q9X2Z'

No funciono.

echo 'U2FsdGVkX1/7xkS74RBSFMhpR9Pv0PZrzOVsIzd38sUGzGsDJOB9FbybAWod5HMsa+WIr5HDprvK6aFNYuOGoZ60qI7axX5Qnn1E6D+BPknRgktrZTbMqfJ7wnwCExyU8ek1RxohYBehaDyUWxSNAkARJtjVJEAOA1kEOUOah11iaPGKxrKRV0kVQKpEVnuZMbf0gv1ih421QvmGucErFhnuX+xv63drOTkYy15s9BVCUfKmjMLniusI0tqs236zv4LGbgrcOfgir+P+| openssl enc -d -a -aes-256-cbc -pbkdf2 -pass pass:'91J6X7R4FQ9TQPM9JX2Q9X2Z'
Tampoco funciono.



echo 'U2FsdGVkX1/7xkS74RBSFMhpR9Pv0PZrzOVsIzd38sUGzGsDJOB9FbybAWod5HMsa+WIr5HDprvK6aFNYuOGoZ60qI7axX5Qnn1E6D+BPknRgktrZTbMqfJ7wnwCExyU8ek1RxohYBehaDyUWxSNAkARJtjVJEAOA1kEOUOah11iaPGKxrKRV0kVQKpEVnuZMbf0gv1ih421QvmGucErFhnuX+xv63drOTkYy15s9BVCUfKmjMLniusI0tqs236zv4LGbgrcOfgir+P+gWHc2TVW4CYszVXlAZUg07JlLLx1jkF85TIMjQ3B91MQS+btaH2WGWFyakmqYltz6jB5DOSCA6AMQYsqLlx53ORLxy3FfJhZTl9iwlrgEZjJZjDoXBBMdlMCOjKUZfTbt3pnlHWEaGJD7NoTgywFsIw5cz7hkmAMxAIkNn/5hGd/S7mwVp9h6GmBUYDsgHWpRxvnjh0s5kVD8TYjLzVnvaNFS4FXrQCiVIcp1ETqicXRjE4T0MYdnFD8h7og3ZlAFixM3nYpUYgKnqi2o2zJg7fEZ8c=' | \
openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 -salt -base64 \
  -pass 'pass:91J6X7R4FQ9TQPM9JX2Q9X2Z'


<img width="1238" height="270" alt="image" src="https://github.com/user-attachments/assets/9500b030-e0dc-4486-bd3d-7d0f8e2419e9" />

Si se pudo!

THM{w3lcome_2_A0c_2025}


Ahora hay que desencriptar el ultimo archivo. Buscando veo q es un archivo comprimido.

gpg --batch --passphrase "THM{w3lcome_2_A0c_2025}" -d dir.tar.gz.gpg > archivito.tar.gz
<img width="1196" height="430" alt="image" src="https://github.com/user-attachments/assets/b017ca70-90b9-436f-bb11-249e7aaa724d" />


Descomprimmos el archivo

sudo caja

<img width="616" height="426" alt="image" src="https://github.com/user-attachments/assets/5ac20f31-2f7a-49bc-b84b-72c840721f6e" />

Finalmente podemos ver la flag final:


<img width="668" height="726" alt="image" src="https://github.com/user-attachments/assets/6216cb5d-266d-4e9b-9bda-1c293d983613" />







