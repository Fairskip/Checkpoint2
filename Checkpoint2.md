# Checkpoint 2


# 🤓 Contexte de ce checkpoint

Tu travailles dans le service SI de la société **SweetCakes**.  
Tu dois reprendre en urgence le travail de l'un de tes collègues.

# 💻 Outils mis à disposition

Tu as 1 VM que tu trouveras [ici](https://odyssey.wildcodeschool.com/expeditions/9793/quests/2862).  
Il faut l'importer dans VirtualBox.

Voici leurs caracteristiques :

- Serveur DC :
    - OS : **Windows Server 2019**
    - RAM : 2 Go
    - Processeurs : 2
    - Compte d'administration : **Administrateur/Azerty123!**
    - Domaine : **checkpoint.lan**
    - Rôles installés : **AD, DHCP, DNS**
    - Configuration IP : **172.16.0.250 /24**

---

# Challenge

## Exercice 1 : Script Powershell

Tu trouveras des fichiers (users.ps1 & users.csv) dans le dossier **Documents** du serveur.

Voici les fonctionnalités de ce script :

- Entrée : fichier csv contenant des nouveaux utilisateurs
- Sortie : création des utilisateurs

Tu trouveras ci-dessous les remarques des utilisateurs RH qui ont commencé à utiliser ce script.  
Tu dois faire fonctionner ce script correctement avec la correction de tous les points.

Les points à corriger sont indépendant donc tu n'est pas obligé de suivre l'ordre.

1. La création d'un utilisateurs nommé "`prenom nom`" est systématique et amène une erreur. C'est à corriger.

```
$SamAccountName = "$($User.prenom $User.nom)"
```


2. Le mot de passe par défaut des utilisateurs est toujours le même car il est statique dans le script. Ton collègue a prévu une fonction `Random-Password` mais elle n'est pas utilisée. Tu dois t'en servir pour avoir des mots de passe dynamiques. Il faut que ce mot de passe comporte au moins **12 caractères**. (Effectué en dehors du timing)


3. Le mot de passe des utilisateurs n'est pas affiché à la fin. A la place on a `System.Security.SecureString`. Il faut qu'il apparaisse en clair. (Effectué en dehors du timing)


4. Le nom de la société (`Sweetcakes`) est statique. On doit pouvoir le modifier par une variable car ce script doit pouvoir servir pour d'autres sociétés. (Effectué en dehors du timing)


5. Quelques fois les utilisateurs qui ont des accents dans leur nom ou leur prénom sont mal entré dans l'AD. C'est à corriger. (Effectué en dehors du timing)


6. Les utilisateurs des services **Marketing** et **Comptabilité** ne sont pas créée. Il faut voir pourquoi. (Effectué en dehors du timing)


7. Les numéros de téléphone de bureau et de mobile des utilisateurs sont inversé, c'est à corrigé.

```
$MobilePhone = $User.mobile

$OfficePhone = $User.telephoneNumber

```

8. Le script n'est pas du tout commenté. Tu dois mettre des commentaires à chaque `###`.

>### Scripte permettant de créer des utilisateurs à partir d'un fichier CSV
>### Full Path du fichier csv à importer et filtrer le fichier pour récupérer les colonnes voulues.
>### Création de comptes d'users de l'entreprise.
>###Titre de la tache à accomplir.
>###List des éléments qu'on veut afficher.
>### Output en plus propre
>### Si compte existe déjà: 
 

9. Ton collègue a oublié de mettre le mail des utilisateurs. Tu dois ajouter cette information dans la création.

```
-Email $Email
```

10. L'information indiquant que le compte xxx est déjà créée donne toujours le même nom. C'est à corriger. (Effectué en dehors du timing)



11. L'information indiquant que le compte a été crée doit apparaître en **vert** et si le compte existe déjà cela doit apparaître en **rouge**.

```
Write-Host "Le compte $Name a été crée`nLe mot de passe est $password" -ForegroundColor Green

Write-Host "Le compte $Name est déja crée" -ForegroundColor Red
```


<br>

## Exercice 2 : Réseaux et domaine

- Serveur DC à télécharger :
    - OS : **Windows Server 2019**
    - RAM : 2 Go
    - Processeurs : 2
    - Compte d'administration : **Administrateur/Azerty123!**
    - Domaine : **checkpoint.lan**
    - Rôles installés : **AD, DHCP, DNS**
    - Configuration IP : **172.16.0.250 /24**

 [Toute la partie de l'exo qui necessite d'être fait avec le serveur DC => Effectué en dehors du timing car durant le jour du checkpoint, mon internet est instable, lente et après 5 essaies/coupures via wifi et point d'acces wifi mobile, ça ne se fait toujours pas.]


> Tu va devoir créer une deuxième VM **Client1** avec les caractéristiques suivantes :

> - Client
> - OS : Windows 10
> - Disque : 50 Go (1 partition pour le système de 35 Go et 1 partition Data de 15 Go)
> - RAM : 1 Go

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Caracteristiques%201.png width = "550" height = "300">

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/DD.png width = "700" height = "80">

<br>
  
> - Compte utilisateur : wilder/Azerty123!

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/wilder.png width = "300" height = "350">

<br>

> - Configuration IP : DHCP

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/IP%20Dynamic.png width = "300" height = "350">

<br>

> - Hostname : Change le hostname en Client1

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Client1.png width = "350" height = "300">

<br>

> - Rejoindre le domaine : 

  <img src = https://github.com/Fairskip/Checkpoint2/blob/main/Client1%20a%20join%20domaine%202.png width = "500" height = "200">


<br>

#### Sur la VM **Client1** :

> 1. Entre le PC **Client1** et le serveur **DC**, le ping ne fonctionne pas. Pourquoi ?  

Client1 | Server
:---: | :---:
169.254.124.220/16 | Serveur : 172.16.0.250 /24

Ils n'ont pas le même réseau d'adresse Ip ou de masque sous-réseau. Donc ils ne sont pas dans le même réseau.

<br>

> Change le paramétrage des machines pour que cela soit possible.  
> Explique ce que tu as fait sur les 2 machines.

Essayer un config release et renew sur Client1 ne marche pas. Et sur le server, je ne vois pas de plage d'adresse disponible dans le DHCP. Cependant, lorsque je regard le service DNS, il y a un Host1 avec une adresse IP déterminé (172.16.0.10). 

Dans le serveur, je crée donc une nouvelle étendu vu dans le point 5 de l'exercice et je réserve l'IP 172.16.0.10 pour Client1.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Etendue.png width = "650" height = "150">

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Release%20et%20renew%20Client1.png width = "500" height = "300">

<br>

Dans le pc Client1, pour être sur que le system trouve le serveur, j'entre dans le dns préféré l'IP du serveur. 

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/DNS%20au%20client1.png width = "300" height = "350">

<br>

Pour être tranquille, j'ai même créer une règle entrante pour le firewall permettant le ping.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Regle%20ping.png width = "400" height = "350">

<br>

Une fois faites, je fais un ipconfig release et renew et obtiens ainsi une adresse IP dans le même réseau que celui du serveur pour mon Client1. 

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Release%20et%20renew%20Client1.png width = "450" height = "550">

<br>

Et ça ping dans les deux sens.

Server au Client :   

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Ping%20Client%202.png width = "500" height = "400">

Client au Serveur :   

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Ping%20server%202.png width = "500" height = "400">


<br>

2. Tente de te connecter avec l'utilisateur john.doe/Azerty123! sur Client1.
3. Tente de te connecter avec l'utilisateur jane.doe/Azerty123! sur Client1.  
    Quel est la différence entre les deux utilisateurs ?


Lors de ma première connection avec John, ça me demande de changer le mot de passe.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/John1.png width = "400" height = "450">

Pour Jane.doe, le compte a été désactivé.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Jane.png width = "400" height = "450">

<br>

4. Que dois-tu faire pour pouvoir te connecter avec le comtpe de John Doe sur le Client1 ?  
    Explique et fais l'action.
   
En me déconnectant de la session de **wilder**, j'arrive à une page de présentation qui me permet de choisir entre la session de **wilder** et de **Autre utilisateur**. 

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/sessions.png width = "250" height = "200">


Je choisis **Autre utilisateur**.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Autre%20utilisateur.png width = "450" height = "450">


J'entre l'ID **john.doe** dans la case du **Nom d'utilisateur** puis **Azerty123!** dans la case **mot de passe**. Une fois faite, ça me dit que le mot de passe doit être changé avant la première connexion. 

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/John1.png width = "400" height = "450">


Je clique sur **Ok**.

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/John2.png width = "400" height = "450">

Je remplis les cases et crée le nouveau mot de mot sur la troisième case et quatrième case. Puis je valide en appuyant sur la petite flèche qui part vers la droite sur la dernière case ou en appuyant sur la touche **Entrée**. 



<br>

#### Sur la VM **DC** :

> 5. Configure le serveur DHCP pour adresser entre **172.16.0.10** et **172.16.0.199**

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Etendue.png width = "600" height = "100">

<br>

> 6. Fait un enregistrement de type A pointant vers **172.16.0.254** nommé **pfsense**.
> 7. Fait un alias sur l'enregistrement de type A qui s'appelle **firewall** (172.16.0.254).

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/a%20et%20cname.png width = "600" height = "100">

<br>

> 8. Tu vas devoir créer des GPO qui s'appliquera aux utilisateurs.
>    * Les utilisateurs n'ont pas accès à l'invite de commande et au powershell. 
>    * Les utilisateurs ont un fond d'écran imposé par l'entreprise [Télécharge l'image ici](https://drive.google.com/file/d/1dekvQBWvbXaougv3t2ournK5L92od1ex/view?usp=drive_link)

![gpo3](https://github.com/Fairskip/Checkpoint2/blob/main/GPO3.png)
![gpo2](https://github.com/Fairskip/Checkpoint2/blob/main/GPO2.png)

<br>
    
>    * Les utilisateurs du domaine peuvent se connecter sur le poste **Client1 uniquement entre 9h et 17h**.

Sur le terminal en manuel et/ou avec un script : 

```
net Username /Times:M-F,09:00-17:00;Sa-Su,00:00-23:59
```


  

