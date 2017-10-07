---
title: "aaaSet d’Apache Tomcat sur une machine virtuelle Linux | Documents Microsoft"
description: "Découvrez comment tooset d’Apache Tomcat7 à l’aide de Machines virtuelles Azure exécutant Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>Configurer Tomcat7 sur une machine virtuelle Linux avec Azure
Apache Tomcat (ou simplement Tomcat, également anciennement appelé Jakarta Tomcat) est un serveur web open source et un conteneur de servlet développé par hello Apache Software Foundation ASF (). Tomcat implémente hello Servlet Java et les spécifications de Java Server Pages (JSP) hello de Sun Microsystems. Tomcat fournit un environnement de serveur web HTTP de Java pur dans le code Java toorun. Dans la configuration la plus simple de hello, Tomcat s’exécute dans un processus de système d’exploitation unique. Ce processus exécute une machine virtuelle Java (JVM). Toutes les demandes HTTP à partir d’un navigateur de tooTomcat sont traité comme un thread distinct dans le processus de Tomcat hello.  

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../../../resource-manager-deployment-model.md). Cet article décrit comment toouse hello modèle de déploiement classique. Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello. toouse un toodeploy de modèle de gestionnaire de ressources une VM Ubuntu avec Open JDK et Tomcat, consultez [cet article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).

Dans cet article, vous installerez Tomcat7 sur une image Linux et le déploierez dans Azure.  

Vous apprendrez à effectuer les opérations suivantes :  

* Comment toocreate une machine virtuelle dans Azure.
* Comment tooprepare hello machine virtuelle pour Tomcat7.
* Comment tooinstall Tomcat7.

Nous partons du principe que vous possédez déjà un abonnement Azure.  Si non, vous pouvez vous inscrire pour une évaluation gratuite à [hello site Web Azure](https://azure.microsoft.com/). Si vous disposez d’un abonnement MSDN, consultez la page présentant les [tarifs préférentiels Microsoft Azure : avantages MSDN, MPN et BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39). toolearn en savoir plus sur Azure, consultez [Nouveautés Azure ?](https://azure.microsoft.com/overview/what-is-azure/).

Cet article suppose que vous avez des connaissances de base relatives à Tomcat et Linux.  

## <a name="phase-1-create-an-image"></a>Phase 1 : Création d’une image
Lors de cette phase, vous allez créer une machine virtuelle à l’aide d’une image Linux dans Azure.  

### <a name="step-1-generate-an-ssh-authentication-key"></a>Étape 1 : Générer une clé d’authentification SSH
SSH est un outil important pour les administrateurs système. Toutefois, une configuration de la sécurité d’accès basée sur un mot de passe déterminé par l’homme n’est pas recommandée. Les utilisateurs malveillants peuvent s’introduire dans votre système si vous disposez d’un nom d’utilisateur et d’un mot de passe faibles.

excellente Hello est qu’il existe un moyen de l’accès à distance tooleave ouvrir et ne vous inquiétez pas sur les mots de passe. Cette méthode se compose d’une authentification avec chiffrement asymétrique. Hello clé privée de l’utilisateur est hello qui accorde l’authentification hello. Vous pouvez verrouiller même compte d’utilisateur hello toonot autoriser l’authentification du mot de passe.

Un autre avantage de cette méthode est que vous n’avez pas besoin de toosign de mots de passe différents dans les serveurs toodifferent. Vous pouvez vous authentifier à l’aide de clé privée personnelle de hello sur tous les serveurs, ce qui vous évite d’avoir tooremember plusieurs mots de passe.



Suivez ces étapes toogenerate hello authentification code SSH.

1. Téléchargez et installez PuTTYgen hello l’emplacement suivant : [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Exécutez Puttygen.exe.
3. Cliquez sur **générer** toogenerate les clés hello. Dans le processus de hello, vous pouvez augmenter le caractère aléatoire par déplacement de la souris hello sur une zone vide de hello dans la fenêtre hello.  
   ![PuTTY Générateur de clés capture d’écran hello générer de nouveau bouton clé][1]
4. Une fois hello générer un processus, Puttygen.exe présentent votre nouvelle clé publique.  
   ![Capture d’écran Générateur de clé puTTY qui affiche la clé publique hello et hello enregistrer bouton clé privée][2]
5. Sélectionnez et copiez la clé publique de hello et enregistrez-le dans un fichier nommé publicKey.pem. Ne cliquez pas sur **clé publique d’enregistrement**, car hello enregistré le format de fichier de la clé publique est différent de la clé publique hello nous voulons.
6. Cliquez sur **Save private key** et enregistrez-la dans un fichier nommé privateKey.ppk.

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>Étape 2 : Créer l’image de hello Bonjour portail Azure
1. Bonjour [portal](https://portal.azure.com/), cliquez sur **nouveau** Bonjour barre des tâches toocreate une image. Choisissez ensuite l’image Linux hello selon vos besoins. Hello exemple suivant utilise hello Ubuntu 14.04 image.
![Capture d’écran du portail hello qui montre le bouton nouvelle de hello][3]

2. Pour **nom d’hôte**, spécifiez nom hello pour hello les URL que vous et les clients Internet utilisera tooaccess cet ordinateur virtuel. Définissez hello dernière partie du nom DNS de hello, par exemple, tomcatdemo. Azure génèrera hello URL en tant que tomcatdemo.cloudapp.net.  

3. Pour **clé d’authentification SSH**, copiez la valeur de clé de hello à partir du fichier hello publicKey.pem, qui contient la clé publique de hello généré par PuTTYgen.  
![Clé d’authentification SSH zone dans le portail de hello][4]

4. Configurez d’autres paramètres selon les besoins, puis cliquez sur **Créer**.  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>Phase 2 : Préparation de la machine virtuelle pour Tomcat7
Dans cette phase, vous configurerez un point de terminaison pour le trafic de Tomcat et puis connectez-vous tooyour machine virtuelle.

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>Étape 1 : Ouvrir l’accès web hello HTTP port tooallow
Les points de terminaison dans Azure se composent d’un protocole TCP ou UDP et d’un port public et privé. Hello privé hello port est que hello écoutent tooon hello virtual machine. port public de Hello est le port hello hello service cloud Azure écoute tooexternally pour le trafic entrant, basés sur Internet.  

Le port TCP 8080 est le numéro de port par défaut hello que Tomcat utilise toolisten. Si ce port est ouvert avec un point de terminaison Azure, vous pouvez (vous et d’autres clients Internet) accéder aux pages Tomcat.  

1. Dans le portail de hello, cliquez sur **Parcourir** > **virtuels**, puis cliquez sur la machine virtuelle hello que vous avez créé.  
   ![Capture d’écran du répertoire des ordinateurs virtuels hello][5]
2. tooadd une machine virtuelle de tooyour de point de terminaison, cliquez sur hello **points de terminaison** boîte.
   ![Capture d’écran qui affiche la boîte de points de terminaison hello][6]
3. Cliquez sur **Add**.  

   1. Pour le point de terminaison hello, entrez un nom pour le point de terminaison hello dans **point de terminaison**, puis entrez 80 dans **Port Public**.  

      Si vous lui affectez too80, vous n’avez pas besoin numéro de port tooinclude hello dans URL hello utilisé tooaccess Tomcat. Par exemple, http://tomcatdemo.cloudapp.net.    

      Si vous lui affectez la valeur tooanother, telles que 81, vous devez tooadd hello port numéro toohello URL tooaccess Tomcat. Par exemple, http://tomcatdemo.cloudapp.net:81/.
   2. Tapez 8080 dans **Port privé**. Par défaut, Tomcat écoute sur le port TCP 8080. Si vous avez modifié le port hello par défaut d’écoute de Tomcat, vous devez mettre à jour **Port privé** toobe hello identique hello du port d’écoute de Tomcat.  
      ![Capture d’écran de l’interface utilisateur montrant la commande Ajouter, Port public et Port privé][7]
4. Cliquez sur **OK** tooadd hello point de terminaison tooyour virtual machine.

### <a name="step-2-connect-toohello-image-you-created"></a>Étape 2 : Connexion image toohello que vous avez créé
Vous pouvez choisir n’importe quel ordinateur virtuel SSH outil tooconnect tooyour. Dans cet exemple, nous utilisons PuTTY.  

1. Obtenir le nom DNS de hello de votre machine virtuelle à partir du portail de hello.
    1. Cliquez sur **Parcourir** > **Machines virtuelles**.
    2. Sélectionnez le nom hello de votre machine virtuelle, puis cliquez sur **propriétés**.
    3. Bonjour **propriétés** vignette, regardez dans hello **nom de domaine** nom DNS de boîte tooget hello.  

2. Obtenir le numéro de port hello pour les connexions SSH à partir de hello **SSH** boîte.  
![Capture d’écran qui affiche le numéro de port de connexion SSH hello][8]

3. Téléchargez [PuTTY](http://www.putty.org/).  

4. Après avoir téléchargé, cliquez sur le fichier exécutable de hello Putty.exe. Dans la configuration de PuTTY, configurer les options de base hello avec le nom d’hôte hello et le port de nombre est obtenu à partir des propriétés hello de votre machine virtuelle.   
![Capture d’écran qui affiche des options de nom et le ports hôte configuration PuTTY de hello][9]

5. Dans le volet gauche de hello, cliquez sur **connexion** > **SSH** > **Auth**, puis cliquez sur **Parcourir** toospecify emplacement Hello du fichier de privateKey.ppk hello. fichier de privateKey.ppk de Hello contient la clé privée hello qui est généré par PuTTYgen plus haut dans hello « Phase 1 : créer une image « section de cet article.  
![Capture d’écran qui affiche la hiérarchie de répertoires de connexion hello et le bouton Parcourir][10]

6. Cliquez sur **Ouvrir**. Une boîte de message peut s’afficher. Si vous avez configuré nom DNS de hello et numéro de port correctement, cliquez sur **Oui**.
![Capture d’écran qui affiche la notification de hello][11]

7. Vous est demandée tooenter votre nom d’utilisateur.  
![Capture d’écran de qui indique où le nom d’utilisateur tooenter][12]

8. Entrez le nom d’utilisateur hello que vous avez utilisé un ordinateur virtuel de hello toocreate Bonjour « Phase 1 : créer une image » plus haut dans cet article. Vous verrez hello suivant :  
![Capture d’écran qui affiche la confirmation de l’authentification de hello][13]

## <a name="phase-3-install-software"></a>Phase 3 : Installation du logiciel
Dans cette phase, vous installez hello Java runtime environment, Tomcat7 et autres composants Tomcat7.  

### <a name="java-runtime-environment"></a>Environnement d’exécution Java
Tomcat est écrit en Java. Il existe deux types de Kits de développement Java (JDK), OpenJDK et JDK Oracle. Vous pouvez choisir hello celui que vous souhaitez.  

> [!NOTE]
> À la fois JDK ont pratiquement les hello même code pour les classes hello Bonjour API Java, mais le code hello pour la machine virtuelle de hello est différent. OpenJDK a tendance à toouse les bibliothèques open, tandis que le JDK Oracle tend toouse fermé celles. Le JDK Oracle a plus de classes et quelques correctifs et il est plus stable qu’OpenJDK.

#### <a name="install-openjdk"></a>Installer OpenJDK  

Utilisez hello suivant toodownload de commande OpenJDK.   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate un toocontain directory hello des fichiers JDK :  

        sudo mkdir /usr/lib/jvm  
* fichiers de JDK tooextract hello dans le répertoire/usr/lib/jvm/hello :  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>Installer JDK Oracle


Utilisez hello suivant toodownload de commande JDK Oracle à partir du site Web de Oracle hello.  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate un toocontain directory hello des fichiers JDK :  

        sudo mkdir /usr/lib/jvm  
* fichiers de JDK tooextract hello dans le répertoire/usr/lib/jvm/hello :  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset JDK Oracle comme hello par défaut machine virtuelle :  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>Confirmer que l’installation de Java a réussi
Vous pouvez utiliser une commande telle que hello suivant tootest si l’environnement d’exécution Java hello est correctement installé :  

    java -version  

Si vous avez installé OpenJDK, vous devez voir un message hello suivante : ![message OpenJDK réussie de l’installation][14]

Si vous avez installé le JDK Oracle, vous devez voir un message hello suivante : ![message d’installation réussie JDK Oracle][15]

### <a name="install-tomcat7"></a>Installer Tomcat7
Utilisez hello suivant commande tooinstall Tomcat7.  

    sudo apt-get install tomcat7  

Si vous n’utilisez pas Tomcat7, conservez hello approprié de cette commande.  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>Confirmer que l’installation de Tomcat7 a réussi
toocheck si Tomcat7 est installé avec succès, parcourir le nom DNS du serveur tooyour Tomcat. Dans cet article, exemple d’URL hello est http://tomcatexample.cloudapp.net/. Si vous voyez un message comme hello suivant, Tomcat7 est correctement installé.
![Message d’installation réussie de Tomcat7][16]

### <a name="install-other-tomcat7-components"></a>Installer d’autres composants de Tomcat7
Il existe d’autres composants facultatifs de Tomcat que vous pouvez installer.  

Hello d’utilisation **sudo apt-cache recherche tomcat7** commande toosee tous les composants disponibles hello. Utilisez hello suivant de commandes tooinstall certains composants utiles.  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>Phase 4 : Configuration de Tomcat7
Dans cette phase, vous administrez Tomcat.

### <a name="start-and-stop-tomcat7"></a>Démarrage et arrêt de Tomcat7
serveur de Tomcat7 Hello démarre automatiquement lorsque vous l’installez. Vous pouvez également le démarrer avec hello de commande suivante :   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7 :

    sudo /etc/init.d/tomcat7 stop

état de hello tooview de Tomcat7 :

    sudo /etc/init.d/tomcat7 status

services de Tomcat toorestart : 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Administration de Tomcat7
Vous pouvez modifier hello Tomcat utilisateur configuration fichier tooset de vos informations d’identification d’administrateur. Utilisez hello de commande suivante :  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

Voici un exemple :  
![Capture d’écran qui affiche la sortie de la commande hello sudo vi][17]  

> [!NOTE]
> Créer un mot de passe fort pour le nom d’utilisateur administrateur de hello.  

Après avoir modifié ce fichier, vous devez redémarrer les services Tomcat7 par hello suivant tooensure commande que hello modifications prennent effet :  

    sudo /etc/init.d/tomcat7 restart  

Ouvrez votre navigateur et entrez **http://<your tomcat server DNS name>/manager/html** comme hello URL. Par exemple hello dans cet article, les URL de hello est http://tomcatexample.cloudapp.net/manager/html.  

Une fois connecté, vous devez voir s’afficher quelque chose de similaire toohello :  
![Capture d’écran de hello Gestionnaire d’applications Web Tomcat][18]

## <a name="common-issues"></a>Problèmes courants
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>Impossible d’accéder à machine virtuelle hello Tomcat et Moodle de hello Internet
#### <a name="symptom"></a>Symptôme  
  Tomcat est en cours d’exécution, mais vous ne voyez pas la page par défaut hello Tomcat avec votre navigateur.
#### <a name="possible-root-cause"></a>Cause principale possible   

  * port d’écoute Tomcat Hello n’est pas hello identique au port privé de hello du point de terminaison de votre machine virtuelle pour le trafic de Tomcat.  

     Vérifiez votre port public et la privée des paramètres de point de terminaison de port, assurez-vous que le port privé de hello est hello identique hello Tomcat port d’écoute. Consultez la section « Phase 1 : Création d’une image » de cet article pour obtenir des instructions sur la configuration des points de terminaison pour votre machine virtuelle.  

     toodetermine hello Tomcat port d’écoute, ouvrez /etc/httpd/conf/httpd.conf (version Red Hat) ou /etc/tomcat7/server.xml (version Debian). Par défaut, hello port d’écoute de Tomcat est 8080. Voici un exemple :  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     Si vous utilisez un ordinateur virtuel comme Debian ou Ubuntu et que vous souhaitez toochange hello par défaut port de Tomcat écouter (par exemple 8081), vous devez également ouvrir le port hello hello système d’exploitation. Tout d’abord, ouvrez le profil de hello :  

        sudo vi /etc/default/tomcat7  

     Puis supprimez les commentaires de la dernière ligne de hello et modifiez « non » trop « Oui ».  

        AUTHBIND=yes
  2. les pare-feu Hello a désactivé hello port d’écoute de Tomcat.

     Vous pouvez page ne s’affiche hello Tomcat par défaut à partir de l’hôte local de hello. problème de Hello est très probable que le port hello, qui est la bonne tooby Tomcat, est bloqué par le pare-feu hello. Vous pouvez utiliser la page Web de hello w3m outil toobrowse hello. Hello commandes suivantes installer w3m et parcourir la page par défaut de Tomcat toohello :  


        sudo yum  install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>Solution

  * Si hello port d’écoute de Tomcat est même hello pas en tant que port privé de hello du point de terminaison hello pour la machine virtuelle de toohello le trafic, vous devez modifier un port privé hello toobe hello identique hello du port d’écoute de Tomcat.   
  2. Si le problème de hello est provoqué par un pare-feu/iptables, ajoutez hello suivant lignes trop/etc/sysconfig/iptables. deuxième ligne de Hello est nécessaire uniquement pour le trafic https :  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > Assurez-vous que les lignes précédentes hello sont positionnées au-dessus de toutes les lignes qui seraient globalement restreindre l’accès, telles que les éléments suivants de hello : - A -j rejeter--rejeter avec icmp-hôte-interdit d’entrée



tooreload hello iptables, exécutez hello de commande suivante :

    service iptables restart

Cela a été testé sur CentOS 6.3.

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>Autorisation refusée lorsque vous téléchargez le projet fichiers trop/var/lib/tomcat7/WebApp /
#### <a name="symptom"></a>Symptôme
  Lorsque vous utilisez un ordinateur virtuel SFTP client (par exemple, FileZilla) tooconnect tooyour et accédez trop/var/lib/tomcat7/WebApp/toopublish votre site, vous obtenez un suivant de toohello erreur message similaire :  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>Cause principale possible
  Vous ne disposez d’aucun dossier de /var/lib/tomcat7/webapps autorisations tooaccess hello.  
#### <a name="solution"></a>Solution  
  Vous devez avoir l’autorisation de tooget à partir du compte root hello. Vous pouvez modifier la propriété de hello de ce dossier à partir du nom d’utilisateur du toohello racine que vous avez utilisé lorsque vous avez configuré l’ordinateur de hello. Voici un exemple avec le nom du compte azureuser hello :  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  Utiliser des autorisations hello tooapply hello -R option pour tous les fichiers à l’intérieur d’un répertoire.  

  Cette commande fonctionne également pour les répertoires. modifications de l’option -R Hello hello des autorisations pour tous les fichiers et répertoires à l’intérieur du répertoire de hello. Voici un exemple :  

     sudo chown -R username:group directory  

  Cette commande modifie la propriété (utilisateur et groupe) pour tous les fichiers et répertoires à l’intérieur des hello active.  

  Hello commande suivante modifie uniquement autorisation hello du répertoire du dossier hello. les fichiers Hello et dossiers contenus dans le répertoire de hello ne sont pas modifiés.  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
