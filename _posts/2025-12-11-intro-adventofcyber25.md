---
title: "🎄 [INTRO] Advent of Cyber 2025 - Try Hack Me"
date: 2025-12-11 18:30:00 -0300
categories: [write-up,ctf]
tags: [ctf,tryhackme,intro]
---
> Este room es la introduccion al CTF.
{: .prompt-tip }

## 1. Advent of Cyber Prep Track
### Challenge 1: Password Pandemonium
Objective:
Create a password that passes all system checks and isn’t found in the leaked password list.

<img width="898" height="373" alt="image" src="https://github.com/user-attachments/assets/275b1c77-5bf6-4719-8f06-950bc43b9049" />
Ñ0k1s_coNk3s01!

La primera flag de este reto es: THM{StrongStart}

### Challenge 2: The Suspicious Chocolate.exe
Objective:
Determine if chocolate.exe is safe or infected.
<img width="927" height="765" alt="image" src="https://github.com/user-attachments/assets/9dc01bfe-59b2-445b-bff4-eeec0d97a68c" />

En la screenshot se puede ver que este archivo es maliocioso, un vendor de muchos lo reconoce y lo tiene catalogado como trojano.

THM{NotSoSweet}



### Challenge 3: Welcome to the AttackBox!
<img width="713" height="548" alt="image" src="https://github.com/user-attachments/assets/4c716b47-cadc-4114-bb17-118be61b0aaf" />
Vemos un simulador de consola linux y bueno este no es dificil.

THM{Ready2Hack}

### Challenge 4: The CMD Conundrum
Este es lo mismo pero con Windows.

Find the hidden flag file using Windows commands.
Lo unico que cambia es que en este tenemos que usar dir /a para ver archivos ocultos. Este es sinonimo de ls -la.

THM{WhereIsMcSkidy}


### Challenge 5: Linux Lore
<img width="779" height="580" alt="image" src="https://github.com/user-attachments/assets/94df2236-6d2a-4228-b1e8-63f236d5c821" />

Hicimos lo mismo que en la anterior pero simplemente en esta usamos la infraestructura real de una distro Linux.

THM{TrustNoBunny}

### Challenge 6: The Leak in the List
Objective:
Check if McSkidy’s email has appeared in a breach.
<img width="727" height="806" alt="image" src="https://github.com/user-attachments/assets/55f32958-d51b-4589-80ec-b0be79a26d52" />

Este esta bueno porque hace referencia a paginas como https://haveibeenpwned.com o https://breachdetective.com/

THM{LeakedAndFound}


### Challenge 7: WiFi Woes in Wareville
Hay que crear una contrasena que cumpla con esos requisitos.
<img width="946" height="622" alt="image" src="https://github.com/user-attachments/assets/ce3c0138-4037-48d3-9014-d2a21602ba96" />

TraiJa_km3(((

THM{NoMoreDefault}

### Challenge 8: The App Trap
Objective:
Find and remove the malicious connected app.
<img width="442" height="510" alt="image" src="https://github.com/user-attachments/assets/3f5798e9-33c1-4711-906d-90a11f669bf0" />


Hay una app sospechosa que tenemos que investigar.
<img width="416" height="578" alt="image" src="https://github.com/user-attachments/assets/b45c99c4-10bd-4056-bbc5-50586cdb0a4a" />

Es Easmas is coming la app sospechosa.

THM{AppTrapped}


### Challenge 9: The Chatbot Confession
TBFC’s AI assistant, FestiveBot, was meant to help write cheerful emails, but it’s been spilling secrets.
Some messages reveal internal URLs and even passwords.

AI tools can be powerful, but defenders must know how to prevent them from oversharing.


Objective:
Identify which chatbot messages contain sensitive information.

<img width="885" height="827" alt="image" src="https://github.com/user-attachments/assets/b7673ff1-5856-4500-9861-ffacd4a47bc3" />

THM{DontFeedTheBot}

### Challenge 10: The Bunny’s Browser Trail

SOCMAS web servers are showing heavy traffic, but one log entry stands out:

“User Agent: BunnyOS/1.0 (HopSecBot)”

Someone or something has infiltrated the system.
User Agent strings help defenders spot automated or suspicious visitors in network logs.

Objective:
Find the unusual User Agent in the HTTP log.

Steps:
* Read the provided web log entries.
* Compare them to common browsers (Chrome, Firefox, Edge).
* Identify and select the suspicious entry.

Este es uno de los mas complicados hasta ahora es una introduccion al analisis de trafico.

<img width="923" height="621" alt="image" src="https://github.com/user-attachments/assets/df3c8e5d-8f40-40e8-8984-a39246500d51" />
THM{EastmasIsComing}





