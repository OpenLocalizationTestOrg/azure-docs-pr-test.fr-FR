---
title: "serveur d’applications Java aaaRun sur une machine virtuelle de Azure classic | Documents Microsoft"
description: "Ce didacticiel utilise des ressources créées avec le modèle de déploiement classique hello et montre comment toocreate une machine virtuelle Windows de l’ordinateur et configurer le serveur d’applications toorun Apache Tomcat."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Comment toorun un serveur d’applications Java sur un ordinateur virtuel créé avec le modèle de déploiement classique de hello
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour un toodeploy de modèle du Gestionnaire de ressources une application Web avec Java 8 et Tomcat, consultez [ici](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Avec Azure, vous pouvez utiliser une capacité serveur tooprovide l’ordinateur virtuel. Par exemple, un ordinateur virtuel en cours d’exécution sur Azure peuvent être toohost configuré un serveur d’applications Java, tels que Apache Tomcat.

À l’issue de ce guide, vous comprendrez de façon toocreate une machine virtuelle s’exécutant sur Azure et configurez-le toorun un serveur d’applications Java. Vous allez en savoir plus et effectuer hello tâches suivantes :

* Comment toocreate une machine virtuelle, l’ordinateur qui a un Kit de développement Java (JDK) déjà installé.
* Comment tooremotely connecter tooyour virtual machine.
* Comment tooinstall un serveur d’applications Java--Apache Tomcat--sur votre machine virtuelle.
* Comment toocreate un point de terminaison pour votre machine virtuelle.
* Comment tooopen hello un port de pare-feu pour votre serveur d’applications.

Hello terminer les résultats de l’installation de Tomcat en cours d’exécution sur un ordinateur virtuel.

![Machine virtuelle exécutant Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate une machine virtuelle
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).  
2. Cliquez sur **nouveau**, cliquez sur **de calcul**, puis cliquez sur **afficher tous les** Bonjour **applications proposées**.
3. Cliquez sur **JDK**, cliquez sur **JDK 8** Bonjour **JDK** volet.  
   Qui prennent en charge de l’image de machine virtuelle **JDK 6** et **JDK 7** sont disponibles si vous avez des applications héritées qui ne sont pas prêt toorun JDK 8.
4. Dans le volet de hello JDK 8, sélectionnez **classique**, puis cliquez sur **créer**.
5. Bonjour **notions de base** panneau :
   1. Spécifiez un nom pour la machine virtuelle de hello.
   2. Entrez un nom pour l’administrateur de hello dans hello **nom d’utilisateur** champ. N’oubliez pas ce nom et hello de mot de passe associé qui suit dans le champ suivant de hello. Vous avez besoin lorsque vous vous connectez à distance dans la machine virtuelle de toohello.
   3. Entrez un mot de passe Bonjour **nouveau mot de passe** champ, puis entrez-le Bonjour **confirmer le mot de passe** champ. Ce mot de passe est pourquoi le compte d’administrateur.
   4. Sélectionnez hello approprié **abonnement**.
   5. Pourquoi **groupe de ressources**, cliquez sur **nouvel** et entrez le nom hello d’un nouveau groupe de ressources. Ou, cliquez sur **utiliser l’existante** et sélectionnez un des groupes de ressources disponibles hello.
   6. Sélectionnez un emplacement de la machine virtuelle de hello, tel que **Amérique du Sud**.
6. Cliquez sur **Suivant**.
7. Bonjour **taille d’image de machine virtuelle** panneau, sélectionnez **A1 Standard** ou une autre image appropriée.
8. Cliquez sur **Sélectionner**.

9. Bonjour **paramètres** panneau, cliquez sur **OK**. Vous pouvez utiliser les valeurs par défaut de hello fournies par Azure.  
10. Bonjour **Résumé** panneau, cliquez sur **OK**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>connexion tooremotely tooyour virtuels
1. Ouvrez une session sur toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Machines virtuelles (classiques)**. Si nécessaire, cliquez sur **davantage de services** en hello en bas à gauche sous les catégories de services hello. Hello **machines virtuelles (classiques)** entrée est répertoriée dans hello **de calcul** groupe.
3. Cliquez sur nom hello hello virtuels que vous souhaitez toosign dans.
4. Après démarrage de la machine virtuelle de hello, un menu en haut de hello du volet de hello autorise les connexions.
5. Cliquez sur **Connecter**.
6. Répondre toohello invites en tant que machine virtuelle de toohello tooconnect nécessaires. En règle générale, vous enregistrerez ou ouvrez le fichier .rdp hello qui contient les détails de la connexion hello. Vous pouvez avoir des url de hello toocopy : port cadre hello dernière hello première ligne du fichier .rdp de hello et collez-le dans une application de connexion à distance.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall un serveur d’applications Java sur votre machine virtuelle
Vous pouvez copier une machine virtuelle de Java application server tooyour, ou vous pouvez installer un serveur d’applications Java via un programme d’installation.

Ce didacticiel utilise Tomcat comme hello Java application server tooinstall.

1. Quand vous êtes connecté dans la machine virtuelle de tooyour, ouvrez une session de navigateur trop[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Double-cliquez sur le lien hello pour **32-bits/64 bits d’installation du Service Windows**. Cette procédure installe Tomcat en tant que service Windows.
3. Lorsque vous y êtes invité, choisissez le programme d’installation de toorun hello.
4. Au sein de hello **le programme d’installation de Apache Tomcat** invites de l’Assistant, suivez hello tooinstall Tomcat. Pour des raisons de hello de ce didacticiel, en acceptant les valeurs par défaut hello convient. Quand vous atteignez hello **fin hello Apache Tomcat Assistant** boîte de dialogue, vous pouvez éventuellement vérifier **exécuter Apache Tomcat** toohave maintenant démarrer de Tomcat. Cliquez sur **Terminer** toocomplete hello processus d’installation de Tomcat.

## <a name="toostart-tomcat"></a>toostart Tomcat

Vous pouvez démarrer manuellement Tomcat en ouvrant une invite de commandes sur votre ordinateur virtuel et l’exécution de la commande hello **net&nbsp;Démarrer&nbsp;Tomcat8**.

Une fois que Tomcat est en cours d’exécution, vous pouvez accéder à Tomcat en entrant l’URL de hello <http://localhost : 8080> dans le navigateur de l’ordinateur virtuel de hello.

toosee Tomcat en cours d’exécution à partir des ordinateurs externes, que vous avez besoin de toocreate un point de terminaison et ouvrez un port.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate un point de terminaison pour votre machine virtuelle
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **Machines virtuelles (classiques)**.
3. Cliquez sur nom hello hello virtual machine qui exécute votre serveur d’applications Java.
4. Cliquez sur **Endpoints**.
5. Cliquez sur **Add**.
6. Bonjour **ajouter le point de terminaison** boîte de dialogue :
   1. Spécifiez un nom pour le point de terminaison hello ; par exemple, **HttpIn**.
   2. Sélectionnez **TCP** pour le protocole hello.
   3. Spécifiez **80** pour le port public de hello.
   4. Spécifiez **8080** pour un port privé hello.
   5. Sélectionnez **désactivé** pour hello flottante d’adresse IP.
   6. Laissez la liste de contrôle d’accès hello en l’état.
   7. Cliquez sur hello **OK** bouton boîte de dialogue tooclose hello et créer le point de terminaison hello.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen un port dans le pare-feu hello pour votre machine virtuelle
1. Machine virtuelle de tooyour vous connecter.
2. Cliquez sur le menu **Démarrage de Windows**.
3. Cliquez sur **Panneau de configuration**.
4. Cliquez sur **Système et sécurité**, sur **Pare-feu Windows**, puis sur **Paramètres avancés**.
5. Cliquez sur **Règles de trafic entrant**, puis sur **Nouvelle règle**.  
   ![Nouvelle règle de trafic entrant][NewIBRule]
6. Pourquoi **le Type de règle**, sélectionnez **Port**, puis cliquez sur **suivant**.  
   ![Porte de nouvelle règle de trafic entrant][NewRulePort]
7. Sur hello **protocole et Ports** écran, sélectionnez **TCP**, spécifiez **8080** comme hello **port local spécifique**, puis cliquez sur **Suivant**.  
  ![Nouvelle règle de trafic entrant][NewRuleProtocol]
8. Sur hello **Action** écran, sélectionnez **autoriser la connexion hello**, puis cliquez sur **suivant**.
   ![Action de nouvelle règle de trafic entrant][NewRuleAction]
9. Sur hello **profil** écran, vérifiez que **domaine**, **privé**, et **Public** sont sélectionnées, puis cliquez sur **suivant** .
   ![Profil de nouvelle règle de trafic entrant][NewRuleProfile]
10. Sur hello **nom** écran, spécifiez un nom pour la règle de hello, tel que **HttpIn** (nom de la règle hello est pas nom de point de terminaison requis toomatch hello, toutefois), puis cliquez sur **Terminer**.  
    ![Nom de nouvelle règle de trafic entrant][NewRuleName]

À ce stade, votre site web Tomcat doit être visible à partir d’un navigateur externe. Dans la fenêtre d’adresse du navigateur hello, tapez une URL sous forme de hello  **http://*votre\_DNS\_nom*. cloudapp.net**, où ***votre\_DNS\_nom*** désigne hello DNS vous avez spécifié lors de la création d’ordinateur virtuel de hello.

## <a name="application-lifecycle-considerations"></a>Considérations relatives au cycle de vie de l'application
* Vous pouvez créer vos propres archive d’application web (WAR) et ajoutez-le toohello **webapps** dossier. Par exemple, créez un projet web dynamique Java Service Page (JSP) de base et exportez-le sous forme de fichier WAR. Ensuite, copiez hello WAR toohello Apache Tomcat **webapps** dossier sur l’ordinateur virtuel de hello, puis l’exécuter dans un navigateur.
* Par défaut lorsque hello service Tomcat est installé, il a la valeur toostart manuellement. Vous pouvez activer cette toostart automatiquement en utilisant le composant logiciel enfichable Services hello. Démarrez le composant logiciel enfichable Services hello en cliquant sur **Démarrer de Windows**, **outils d’administration**, puis **Services**. Double-cliquez sur hello **Apache Tomcat** de service et définissez **type de démarrage** trop**automatique**.

    ![Configuration automatique d’un toostart de service][service_automatic_startup]

    Hello avantage d’avoir Tomcat démarrer automatiquement est qu’il démarre l’exécution lors du redémarrage de machine virtuelle de hello (par exemple, une fois que les mises à jour logicielles nécessitant un redémarrage sont installés).

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez en savoir plus sur les autres services (tels que le stockage Azure, service bus et base de données SQL) que vous pouvez tooinclude avec vos applications Java. Afficher les informations de hello disponibles à hello [centre de développement Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
