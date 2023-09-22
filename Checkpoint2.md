# Checkpoint 2

## Exercice 1 : Script Powershell

<br>

## Exercice 2 : Réseaux et domaine

Tu va devoir créer une deuxième VM **Client1** avec les caractéristiques suivantes :

- Client
- OS : Windows 10
- Disque : 50 Go (1 partition pour le système de 35 Go et 1 partition Data de 15 Go)
- RAM : 1 Go

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/Caracteristiques%201.png width = "550" height = "300">

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/DD.png width = "700" height = "80">

  
- Compte utilisateur : wilder/Azerty123!

<img src = https://github.com/Fairskip/Checkpoint2/blob/main/wilder.png width = "300" height = "350">


- Configuration IP : DHCP
- Hostname : Change le hostname en Client1

<br>

#### Sur la VM **Client1** :

1. Entre le PC **Client1** et le serveur **DC**, le ping ne fonctionne pas. Pourquoi ?  
    Change le paramétrage des machines pour que cela soit possible.  
    Explique ce que tu as fait sur les 2 machines.


2. Tente de te connecter avec l'utilisateur john.doe/Azerty123! sur Client1.


3. Tente de te connecter avec l'utilisateur jane.doe/Azerty123! sur Client1.  
    Quel est la différence entre les deux utilisateurs ?


4. Que dois-tu faire pour pouvoir te connecter avec le comtpe de John Doe sur le Client1 ?  
    Explique et fais l'action.



<br>

#### Sur la VM **DC** :

5. Configure le serveur DHCP pour adresser entre **172.16.0.10** et **172.16.0.199**


6. Fait un enregistrement de type A pointant vers **172.16.0.254** nommé **pfsense**.


7. Fait un alias sur l'enregistrement de type A qui s'appelle **firewall** (172.16.0.254).


8. Tu vas devoir créer des GPO qui s'appliquera aux utilisateurs.
    1. Les utilisateurs n'ont pas accès à l'invite de commande et au powershell.
    
    
    2. Les utilisateurs ont un fond d'écran imposé par l'entreprise [Télécharge l'image ici](https://drive.google.com/file/d/1dekvQBWvbXaougv3t2ournK5L92od1ex/view?usp=drive_link)
    
    
    3. Les utilisateurs du domaine peuvent se connecter sur le poste **Client1 uniquement entre 9h et 17h**.
  
    4. 
