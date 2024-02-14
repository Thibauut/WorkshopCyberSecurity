# WorkshopBasicsCyberSecurityEpitech - WorkShop1

## Introduction

Aujourd'hui, nous allons explorer les bases de la cybersécurité. Nous allons commencer par apprendre à utiliser divers outils pour identifier et exploiter des vulnérabilités dans des applications web. Avant de plonger dans l'exploitation des failles, nous devons nous familiariser avec les outils que nous allons utiliser.

## Les outils

Dans ce workshop, nous allons utiliser deux outils essentiels pour les tests de pénétration: **Gobuster** et **JohnTheRipper**.

### Gobuster

<img src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/01c6fdc1-27e4-4af5-9fa9-e7da6fd0ea59" width="30%" height="30%" alt="Gob">

Gobuster aide à découvrir des parties cachées d'un site web, comme des pages secrètes ou des dossiers non répertoriés, en explorant toutes les possibilités. Cela peut être utile pour trouver des vulnérabilités dans une application web.

Pour faire simple:
Imaginez que vous avez une carte au trésor, mais vous ne savez pas exactement où se trouvent les indices. Gobuster, c'est comme un explorateur de cartes au trésor numérique. Il parcourt le terrain (un site web) pour trouver des indices (fichiers et dossiers cachés).

### JohnTheRipper

<img src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/a73d3560-9969-4089-a6f7-e7de1d2e4c5c" width="30%" height="30%" alt="Gob">

John the Ripper est un outil de cracking de mot de passe qui tente de récupérer les mots de passe en utilisant des techniques telles que la force brute et le cracking de hachage. Cet outil peut être employé pour évaluer la robustesse des mots de passe en testant différentes combinaisons.

En d'autres termes:
Imaginez que vous avez un coffre-fort dont vous avez oublié le code. John the Ripper agit comme un spécialiste en ouverture de coffre-fort. Il essaie différentes combinaisons de codes jusqu'à ce qu'il réussisse à déverrouiller le coffre.

## Partie 1: Gobuster (Trouver des fichiers et des dossiers cachés)

Dans cet exercice, nous allons utiliser Gobuster pour trouver des fichiers et des dossiers cachés sur un site web. Cela peut nous aider à découvrir des vulnérabilités potentielles.

### Exercice 1: Installer Gobuster

Pour commencer, nous devons installer Gobuster. Ouvrez un terminal et exécutez la ou les commande suivante:

- Pour Linux (Ubuntu/Debian)
```
sudo apt update
sudo apt install gobuster
```
- Pour Mac OS (Homebrew est requis)
```
brew install gobuster
```
Parfait! Maintenant pour vérifier que **Gobuster** est bien installé utilisons la commande:
```
gobuster --help
```
Vous devriez voir une aide montrant l’utilisation de **Gobuster** avec les commandes et options possibles. Cela indique que l'installation a réussi.

### Exercice 2: Utiliser Gobuster

Maintenant que **Gobuster** est installé, nous allons l'utiliser pour trouver des fichiers et des dossiers cachés sur un site web. Pour ce faire, nous allons utiliser un site web de test (Il sera écrit au tableau au préalable) vous pouvez aller dessus et vous verrez que le site est très simple.

Avant d'utiliser **Gobuster** nous devons télécharger un fichier de wordlist (liste de mots) pour que **Gobuster** puisse l'utiliser pour trouver des fichiers et des dossiers cachés. Vous pouvez télécharger la wordlist [ici](https://drive.google.com/file/d/1geXJQyuSyy342_lPE_8HI6My0h2Rp_fe/view?usp=sharing) (le fichier nomme big.txt)

Ensuite, ouvrez un terminal et exécutez la commande suivante:
```
gobuster dir -u http://exemple.com -w /chemin/vers/big.txt
```

Notez qu'il est important de remplacer **`http://exemple.com`** par l'URL du site web que vous souhaitez scanner (celui qui sera écrit au tableau) et **`/chemin/vers/big.txt`** par le chemin vers le fichier de wordlist que vous avez téléchargé.
Après la commande exécutée et l'analyse de **Gobuster** on doit obtenir cela:

<img width="558" alt="Capture d’écran 2024-02-03 à 03 34 59" src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/cf5235cf-eb43-4815-85c0-0ae7cf668f3e">

### Exercice 3: Analyser les résultats

Après avoir exécuté **Gobuster**, vous devriez voir une liste de fichiers et de dossiers cachés sur le site web. Cela peut inclure des pages secrètes, des dossiers non répertoriés, ou d'autres informations sensibles.

Pour tester ces chemins, vous pouvez les visiter dans un navigateur en ajoutant chacun à la fin de l'URL de la cible, par exemple, `http://exemple.com/home`, `http://exemple.com/login` et `http://exemple.com/secret`.<br/>
Voyez-vous quelque chose d'intéressant? Peut-être un fichier secret a télécharger qui n'était pas censé être visible?

Pour ceux ayant reussi à trouver et télécharger un fichier secret, vous pouvez essayer de l'ouvrir pour voir ce qu'il contient. En revanche, pour ceux qui n'ont pas réussi, revoyez les étapes précédentes et assurez-vous que vous avez bien suivi les instructions. Si vous avez des questions, n'hésitez pas à demander de l'aide.<br/>

Dans le fichier nommé **`secret-folder.zip`** vous devriez trouver.. Ah vous pensez que j'allais vous le dire hein! On va voir si vous arrivez a dechiffer le mot de passe pour pouvoir acceder a mes données :)

Lorsque vous tentez d'ouvrir le fichier .zip on nous demande un mot de passe et pas de bol parce qu'a l'intérieur vous devriez trouver des informations sensibles qui ne devraient pas être accessibles au public.<br/>
Maintenant on va passer à l'exercice suivant.

## Partie 2: JohnTheRipper (Tester les mots de passe pour acceder au secret)

### Exercice 1: Installer JohnTheRipper

Pour commencer, nous devons installer **JohnTheRipper**. Ouvrez un terminal et exécutez la ou les commande suivante:

```
git clone git@github.com:openwall/john.git
```
Rendez vous à l'endroit ou vous avez cloner votre répertoire il doit se nommer "JohnTheRipper", naviguez à l'interieur et tapez cette commande:
```
cd src && ./configure && make
```

Cela va permettre de compiler les différents outils de **JohnTheRipper**. Normalement si tout s'est bien passé il doit être ecrit "Make process completed". Cela signifie que la compilation et l'installation ont été effectuées avec succès.<br/>
Ensuite on se rend dans le dossier "run" en faisant (ne vous inquiétez pas il y a énormément d'outils proposés mais dans notre cas on en utilisera que 2):
```
cd .. && cd run
```

C'est ici que tout les outils compilés se trouvent et sont prêt à être utilisés. Tentez de lancer john ou zip2john ce sont les deux outils que nous allons utiliser qui sont installés avec JohnTheRipper.<br/>
Parfait! Maintenant pour vérifier que les outils sont bien installé utilisons les commandes:
```
./john --help
```
Et 
```
./zip2john --help
```
Vous devriez voir une aide montrant l’utilisation de **john** et **zip2john** avec les commandes et options possibles. Cela indique que l'installation a réussi.

### Exercice 2: Utiliser **zip2john**

**zip2john** est une partie de l'outil JohnTheRipper et est utilisé pour extraire des informations de hachage à partir d'archives ZIP. Expliquons cela de manière simple:

Imaginez une mallette avec un cadenas. Vous voulez savoir ce qu'il y a à l'intérieur, mais vous avez oublié la combinaison du cadenas. zip2john agit comme un inspecteur de cadenas. Il regarde la serrure (le fichier ZIP) et trouve des indices qui pourraient vous aider à trouver la bonne combinaison.

C'est tout simple on va utiliser **zip2john** sur le fichier secret que vous avez téléchargé précédemment pour cela on va utliser la commande suivante:
```
./zip2john secret-folder.zip
```
On obtient le résultat suivant:<br/><br/>
<img width="557" alt="Capture d’écran 2024-02-03 à 18 48 14" src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/cd47091d-23ff-46ac-951f-4ac0e8afa4b0"><br/><br/>
Je sais que c'est incompressible mais ne vous inquiétez pas je vais tout vous expliquer. Sur l'image ci-dessus nous pouvons voir que zip2john a réussi à récuperer toutes les informations et indices permettant de trouver le mot de passe tel que le **hash** de ce dernier (c'est a dire le mot de passe cryptée). Donc tout ce qui nous intéresse ici c'est notre mot de passe hashé:<br/>

<img width="557" alt="Capture d’écran 2024-02-03 à 18 48 14" src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/eb221d97-c419-4178-abea-5148c8e3718f"><br/><br/>

On va ensuite copier et coller notre mot de passe hashé (le contenu qui est souligné en rouge sur l'image ci dessus) dans un fichier.txt que nous allons crée et qui se nommera `hash.txt`. Ce fichier sera ensuite utilisé par l'outil **john** afin de pouvoir decrypter le mot de passe dans l'exercice suivant.<br/>

Notez que vous devez en plus télécharger la wordlist (liste de mots de passe fréquents) [ici](https://drive.google.com/file/d/1vN2cTDknWz-v1-aGW26NDftJh1lRwbij/view?usp=drive_link) (le fichier se nomme rockyou.txt)

### Exercice 3: Utiliser **john** (Exercice final)

Si vous avez bien suivi les étapes et reussi les exercices précédents cela devrait dire que vous devriez avoir en votre possesion les fichiers suivants:
- hash.txt (fichier contenant votre mot de passe crypté récupéré dans l’exercice précédent)
- rockyou.txt (liste des mots de passes les plus fréquemment utilisés)<br/>

Si vous avez ces deux fichiers alors vous êtes prets a utiliser **john**.

Afin de décrypter votre mot de passe vous allez devoir utiliser la commande suivante:
```
john /chemin/vers/votre/fichier/hash.txt --wordlist=/chemin/vers/votre/wordlist/rockyou.txt
```
Attention à bien spécifier vos fichiers car ci-dessus ce sont les chemins vers mes fichiers qui sont spécifiés.<br/>Vous devriez obtenir quelque chose comme cela:<br/>

<img width="562" alt="Capture d’écran 2024-02-03 à 20 17 28" src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/acbf0bcb-fbcd-4698-a8c4-5fc176a7ba39"><br/>

Bingo! Vous voyez le mot de passe ? Il est bel est bien sous vos yeux!<br/>

<img width="562" alt="Capture d’écran 2024-02-03 à 20 17 28" src="https://github.com/Thibauut/WorkshopBasicsCyberSecurityEpitech/assets/91698852/3abebcf5-bd3a-48d7-b6dd-6b939b547765"><br/>

Essayez maintenant d'extraire le fichier .zip et d'en voir son contenu. Vous y verrez normalement des informations confidentielles qui vont vous permettre de vous connecter avec le /login du site web donné au debut.<br/><br/>
Un indice: C'est soit le premier soit le dernier!<br/><br/>
Essayez de vous connecter pour voir ce qu'il se passe. :)
