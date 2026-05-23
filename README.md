# LAB-11-Bypass-de-la-Detection-de-Root-Android-avec-Frida
Ce lab porte sur le contournement de la détection de root d'une application Android à l'aide de Frida, un framework d'instrumentation dynamique. L'application cible est OWASP UnCrackable Level 1, conçue spécifiquement pour résister à l'analyse — ce qui en fait un excellent terrain d'entraînement.
L'idée est simple : plutôt que de modifier l'APK ou de patcher le binaire statiquement, Frida injecte un script JavaScript directement dans le processus en cours d'exécution pour intercepter et modifier le comportement des fonctions de sécurité à la volée.

Étape 1 — Vérification de la connexion ADB
Avant de commencer, on s'assure que l'émulateur est bien reconnu par l'ordinateur via ADB :
bashadb devices
<img width="1165" height="88" alt="Connexion ADB - première vérification" src="https://github.com/user-attachments/assets/bdb1ddae-656d-4a7e-8457-c494edc49103" />
Une deuxième vérification confirme que la connexion est stable et que l'émulateur répond correctement :
<img width="1132" height="56" alt="Connexion ADB - confirmation" src="https://github.com/user-attachments/assets/03dfda47-eff1-45f8-be5a-cad972a1d668" />

Étape 2 — Lancement du serveur Frida sur l'émulateur
Le serveur Frida est déployé et lancé en arrière-plan sur l'émulateur Android. On vérifie ensuite sa présence dans la liste des processus actifs pour s'assurer qu'il tourne correctement avant d'aller plus loin.
<img width="1377" height="77" alt="Serveur Frida actif" src="https://github.com/user-attachments/assets/e71377ea-3c5d-411e-be31-8d9818853fd5" />

Étape 3 — Injection du script et bypass des protections
C'est le cœur du lab. Frida injecte le script bypass.js directement dans le processus de l'application cible. Le script intercepte les fonctions responsables de la détection de root et modifie leurs valeurs de retour pour que l'application croie tourner dans un environnement sain.
Les logs confirment que les hooks sont chargés et que les fonctions de sécurité ont bien été neutralisées.
<img width="1396" height="417" alt="Injection Frida et bypass actif" src="https://github.com/user-attachments/assets/5a2d77be-391f-4ef0-b7d9-4b3df923daca" />

Étape 4 — Application déverrouillée
Avec le bypass en place, l'application UnCrackable Level 1 se lance normalement sans se fermer. L'écran de vérification de la chaîne secrète est maintenant accessible — ce qui n'était pas possible avant l'injection.
<img width="377" height="791" alt="Application déverrouillée" src="https://github.com/user-attachments/assets/8a59575a-08cd-4d9d-ba37-135d286e6255" />
