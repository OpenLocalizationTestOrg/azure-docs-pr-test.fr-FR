---
title: "aaaData passerelle de gestion de fabrique de données | Documents Microsoft"
description: "Configurer une passerelle de données toomove des données entre locaux et hello cloud. Utiliser la passerelle de gestion des données dans Azure Data Factory toomove vos données."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Passerelle de gestion de données
passerelle de gestion des données Hello est un agent de client que vous devez installer dans vos données de toocopy environnement local entre des magasins de données locaux et cloud. Hello des données localement magasins pris en charge par la fabrique de données sont répertoriées dans hello [prise en charge des sources de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.

Cet article vient s’ajouter aux procédure pas à pas de hello Bonjour [déplacement des données entre locaux et cloud banques de données](data-factory-move-data-between-onprem-and-cloud.md) l’article. Hello procédure pas à pas, vous créez un pipeline qui utilise des données de toomove hello passerelle à partir d’un tooan de base de données SQL Server locale blob Azure. Cet article fournit des informations détaillées sur la passerelle de gestion des données hello. 

Vous pouvez faire évoluer une passerelle de gestion des données en associant plusieurs machines locales de la passerelle de hello. Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud. Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique. Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.

> [!NOTE]
> Actuellement, passerelle prend en charge uniquement l’activité de copie hello et l’activité de procédure stockée dans la fabrique de données. Il n’est pas passerelle de hello toouse possible à partir de sources de données sur site tooaccess activité personnalisée.      

## <a name="overview"></a>Vue d'ensemble
### <a name="capabilities-of-data-management-gateway"></a>Fonctionnalités de la passerelle de gestion des données
Passerelle de gestion des données fournit hello suivant de fonctionnalités :

* Modèle des sources de données sur site et les sources de données cloud dans hello même fabrique de données et déplacement des données.
* Avoir un point unique pour la surveillance et la gestion avec visibilité sur l’état de la passerelle à partir de la page de Data Factory hello.
* Gérer les sources de données access tooon local en toute sécurité.
  * Aucune modification requise toocorporate pare-feu. Passerelle effectue uniquement les connexions HTTP sortant tooopen internet.
  * Chiffrement des informations d’identification pour vos magasins de données locaux à l’aide de votre certificat.
* Déplacer efficacement des données : les données sont transférées en parallèle, résilients toointermittent des problèmes de réseau avec la logique de nouvelle tentative automatique.

### <a name="command-flow-and-data-flow"></a>Flux de commandes et flux de données
Lorsque vous utilisez un copier activité toocopy des données entre locaux et cloud, activité hello utilise un passerelle tootransfer de données à partir de toocloud de source de données locale et vice versa.

Voici hello des flux de données de haut niveau pour et un récapitulatif des étapes de la copie avec la passerelle de données : ![des flux de données à l’aide de la passerelle](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Développeur de données crée une passerelle pour une fabrique de données Azure à l’aide soit hello [portail Azure](https://portal.azure.com) ou [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).
2. Développeur de données crée un service lié pour une banque de données locale en spécifiant la passerelle de hello. Comme partie de la configuration de hello le service lié, développeur de données utilise les informations d’identification et les types d’authentification toospecify application hello informations d’identification du paramètre.  informations d’identification du paramètre Hello boîte de dialogue application communique avec les données de salutation stocker tootest connexion et hello toosave d’identification de passerelle.
3. Passerelle chiffre les informations d’identification de l’hello avec certificat hello associé passerelle hello (fourni par le développeur de données), avant d’enregistrer les informations d’identification hello dans le cloud de hello.
4. Service de fabrique de données communique avec la passerelle hello pour la planification et la gestion des travaux via un canal de contrôle qui utilise une file d’attente du bus de service Azure partagé. Lorsqu’un travail d’activité de copie doit toobe lancé, fabrique de données des files d’attente demande hello en même temps que les informations d’identification. Passerelle démarre le travail de hello après interrogation file d’attente hello.
5. passerelle de Hello déchiffre des informations d’identification de hello avec hello même certificat et connecte ensuite banque de données locale toohello avec les informations d’identification et le type d’authentification approprié.
6. passerelle de Hello copie des données à partir d’un stockage en nuage tooa magasin local ou vice versa, selon la configuration dans le pipeline de données hello hello activité de copie. Pour cette étape, la passerelle de hello communique directement avec les services de stockage cloud, tels que le stockage Blob Azure sur un un canal sécurisé (HTTPS).

### <a name="considerations-for-using-gateway"></a>Considérations relatives à l’utilisation de la passerelle
* Une seule instance de passerelle de gestion des données peut être utilisée pour plusieurs sources de données locales. Toutefois, **une seule instance de passerelle est une fabrique de données Azure liée tooonly** et ne peut pas être partagé avec un autre Azure data factory.
* Vous ne pouvez installer qu’**une seule instance de la passerelle de gestion de données** sur un même ordinateur. Supposons que vous avez deux fabriques de données qui doivent tooaccess des sources de données locale, vous devez les passerelles tooinstall sur deux ordinateurs locaux. En d’autres termes, une passerelle est la fabrique de données spécifiques tooa liée
* Hello **passerelle n’a pas besoin toobe sur hello même ordinateur en tant que source de données hello**. Toutefois, source de données toohello plus proche passerelle réduit la durée hello pour la source de données hello passerelle tooconnect toohello. Nous vous recommandons d’installer la passerelle de hello sur un ordinateur différent de hello une source de données hôtes locaux. Lors de la source de données et de la passerelle hello sont sur des ordinateurs différents, passerelle de hello n’est pas en concurrence pour les ressources avec la source de données.
* Vous pouvez avoir **plusieurs passerelles sur différents ordinateurs connexion toohello même source de données locale**. Par exemple, peut avoir deux passerelles desservant les fabriques de deux données mais hello même source de données locale est enregistré avec les fabriques de données hello.
* Si une passerelle est déjà installée sur votre ordinateur desservant un scénario **Power BI**, installez une **passerelle distincte pour Azure Data Factory** sur un autre ordinateur.
* Vous devez utiliser la passerelle même lorsque vous utilisez **ExpressRoute**.
* Considérez votre source de données comme une source de données locale (derrière un pare-feu), même lorsque vous utilisez **ExpressRoute**. Utiliser une connexion de tooestablish hello passerelle entre le service de hello et de la source de données hello.
* Vous devez **utiliser hello passerelle** même si le magasin de données hello est dans le cloud de hello sur un **Azure IaaS VM**.

## <a name="installation"></a>Installation
### <a name="prerequisites"></a>Composants requis
* prise en charge de Hello **système d’exploitation** versions sont Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Installation de la passerelle de gestion des données hello sur un contrôleur de domaine n’est actuellement pas pris en charge.
* .NET framework 4.5.1 ou version ultérieure est requis. Si vous installez la passerelle sur un ordinateur Windows 7, installez .NET Framework 4.5 ou une version ultérieure. Consultez [Configuration système requise pour .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) pour plus d’informations.
* Hello recommandé **configuration** pour ordinateur de passerelle hello est au moins 2 GHz, 4 cœurs, 8 Go de RAM et disque 80 Go.
* Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répond pas les demandes toodata. Par conséquent, configurer un approprié **de l’alimentation** sur ordinateur hello avant d’installer la passerelle de hello. Si la machine de hello est toohibernate configuré, installation de la passerelle hello vous invite à entrer un message.
* Vous devez être administrateur sur hello machine tooinstall et configurer la passerelle de gestion des données hello avec succès. Vous pouvez ajouter des utilisateurs supplémentaires toohello **passerelle de gestion des données utilisateurs** groupe Windows local. membres Hello de ce groupe sont en mesure de toouse hello **Gestionnaire de Configuration de passerelle de gestion de données** passerelle de hello tooconfigure outil.

Comme copier activité se produisent sur une fréquence spécifique, hello l’utilisation des ressources (processeur, mémoire) sur l’ordinateur de hello suit également hello même modèle avec des heures de pointe et les temps d’inactivité. L’utilisation des ressources également dépend fortement hello quantité de données en cours de déplacement. Lorsque plusieurs travaux sont en cours, vous constaterez une augmentation des ressources utilisées pendant les heures de pointe.

### <a name="installation-options"></a>Options d’installation
Passerelle de gestion des données peut être installé dans hello suivant façons :

* En téléchargeant un package d’installation MSI de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Hello MSI peut également être utilisé tooupgrade existant données Gestion passerelle toohello version la plus récente, tous les paramètres sont conservés.
* En cliquant sur le lien **Télécharger et installer la passerelle de données** sous INSTALLATION MANUELLE ou **Installer directement sur cet ordinateur** sous INSTALLATION RAPIDE. Pour des instructions pas à pas sur l’utilisation de l’installation rapide, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) . étape manuelle de Hello prend le centre de téléchargement toohello.  instructions de Hello pour télécharger et installer la passerelle de hello à partir du centre de téléchargement sont fournies dans la section suivante de hello.

### <a name="installation-best-practices"></a>Meilleures pratiques d’installation :
1. Configurer le mode d’alimentation sur l’ordinateur hôte de hello pour la passerelle de hello afin que hello machine ne pas en veille prolongée. Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répond pas les demandes toodata.
2. Sauvegardez le certificat hello associé hello passerelle.

### <a name="install-hello-gateway-from-download-center"></a>Installer la passerelle de hello à partir du centre de téléchargement
1. Accédez trop[page de téléchargement de passerelle de gestion des données Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).
2. Cliquez sur **télécharger**, sélectionnez hello version appropriée (**32 bits** Visual Studio. **64 bits**), puis cliquez sur **Suivant**.
3. Exécutez hello **MSI** directement ou enregistrez-le tooyour disque et les exécuter.
4. Sur hello **Bienvenue** page, sélectionnez un **langage** cliquez sur **suivant**.
5. **Accepter** hello du contrat de licence utilisateur final et cliquez sur **suivant**.
6. Sélectionnez **dossier** tooinstall hello passerelle, puis cliquez sur **suivant**.
7. Sur hello **tooinstall prêt** , cliquez sur **installer**.
8. Cliquez sur **Terminer** toocomplete installation.
9. Obtenir la clé de hello hello portail Azure. Consultez hello la section suivante pour obtenir des instructions pas à pas.
10. Sur hello **Registre passerelle** page de **Gestionnaire de Configuration de passerelle de gestion de données** en cours d’exécution sur votre ordinateur, procédez comme hello comme suit :
    1. Collez la clé de hello texte hello.
    2. Si vous le souhaitez, cliquez sur **afficher la clé de passerelle** texte de la touche toosee hello.
    3. Cliquez sur **S'inscrire**.

### <a name="register-gateway-using-key"></a>Inscrire la passerelle à l’aide de la clé
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Si vous n’avez pas déjà créé une passerelle logique dans le portail de hello
toocreate une passerelle dans hello portal et get hello la clé à partir de hello **configurer** page, suivez les étapes de procédure pas à pas Bonjour [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Si vous avez déjà créé la passerelle logique de hello dans le portail de hello
1. Dans le portail Azure, accédez toohello **Data Factory** page, puis cliquez sur **Services liés** vignette.

    ![Page Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Bonjour **Services liés** page, sélectionnez hello logique **passerelle** vous avez créé dans le portail de hello.

    ![passerelle logique](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Bonjour **passerelle de données** , cliquez sur **télécharger et installer la passerelle de données**.

    ![Télécharger le lien dans le portail de hello](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Bonjour **configurer** , cliquez sur **recréez clé**. Cliquez sur Oui sur le message d’avertissement hello après leur lecture avec soin.

    ![Recréer une clé](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Cliquez sur Copier bouton suivant toohello la clé. clé de Hello est copié toohello Presse-papiers.

    ![Copier la clé](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Icônes de la barre d’état système/notifications
Hello image suivante montre certains des hello des icônes de barre d’état que vous voyez.

![Icônes de la barre d’état système](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Si vous déplacez le curseur sur hello système barre d’état et l’avis de l’icône du message, vous consultez les détails sur l’état de hello d’opération de mise à jour de passerelle/hello dans une fenêtre contextuelle.

### <a name="ports-and-firewall"></a>Ports et pare-feu
Il existe deux pare-feu, vous devez tooconsider : **pare-feu d’entreprise** en cours d’exécution sur le routeur central de hello d’organisation de hello, et **pare-feu Windows** configuré comme un démon sur l’ordinateur local de hello où hello passerelle est installée.  

![Pare-feu](./media/data-factory-data-management-gateway/firewalls2.png)

Au niveau du pare-feu d’entreprise, vous devez configurer les éléments suivants de hello domaines et les ports de sortie :

| Noms de domaine | Ports | Description |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Utilisé pour la communication avec le serveur principal du service Déplacement des données |
| *.core.windows.net |443 |Utilisé pour une copie intermédiaire à l’aide d’objets Blob Azure (si configuré)|
| *.frontend.clouddatahub.net |443 |Utilisé pour la communication avec le serveur principal du service Déplacement des données |


Au niveau du pare-feu Windows, ces ports de sortie sont normalement activés. Si non, vous pouvez configurer les ports et les domaines de hello en conséquence sur l’ordinateur de passerelle.

> [!NOTE]
> 1. En fonction de votre source / récepteurs, vous avez peut-être toowhitelist d’autres domaines et les ports de sortie dans votre pare-feu d’entreprise et Windows.
> 2. Pour certaines bases de données Cloud (par exemple : [base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), vous devrez peut-être adresse toowhitelist de l’ordinateur de passerelle sur leur configuration de pare-feu.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Copier des données à partir d’un magasin de données du magasin tooa récepteur source données
Assurez-vous que les règles de pare-feu de hello sont activées correctement sur le pare-feu d’entreprise hello, le pare-feu Windows sur l’ordinateur de passerelle hello, et du magasin de données de hello lui-même. L’activation de ces règles permet hello source de passerelle tooconnect tooboth et récepteur avec succès. Activer les règles pour chaque magasin de données impliquée dans une opération de copie hello.

Par exemple, toocopy de **un récepteur Azure SQL Database tooan de banque de données locale ou un récepteur d’Azure SQL Data Warehouse**, hello comme suit :

* Autorisez le trafic **TCP** sortant sur le port **1433** pour le pare-feu Windows et le pare-feu d’entreprise.
* Configurez les paramètres de pare-feu hello de SQL Azure tooadd hello adresse IP du serveur de liste de toohello hello passerelle machine d’adresses IP autorisées.

> [!NOTE]
> Si votre pare-feu n’autorise pas le port de sortie 1433, la passerelle ne peut pas accéder directement à Azure SQL. Dans ce cas, vous pouvez utiliser [intermédiaire de copie](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL de la base de données Azure / entrepôt de données SQL Azure. Dans ce scénario, vous nécessiterait HTTPS (port 443) pour le déplacement des données de hello.
>
>


### <a name="proxy-server-considerations"></a>Considérations relatives aux serveurs proxy
Si votre environnement de réseau d’entreprise utilise un proxy serveur tooaccess hello internet, configurer les paramètres de proxy appropriés de données Gestion passerelle toouse. Vous pouvez définir le proxy de hello pendant la phase initiale d’inscription de hello.

![Définir le serveur proxy lors de l’inscription](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

Gateway utilise le service de cloud hello proxy server tooconnect toohello. Cliquez sur le lien **Modifier** pendant l’installation initiale. Vous consultez hello **paramètre proxy** boîte de dialogue.

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxySettings.png)

Il existe trois options de configuration :

* **N’utilisez pas de proxy**: passerelle n’utilise pas explicitement tous les services de toocloud tooconnect proxy.
* **Utiliser le proxy système**: passerelle utilise le proxy hello paramètre qui est configuré dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est configuré dans diahost.exe.config et diawp.exe.config, passerelle connecte toocloud service directement sans passer par le proxy.
* **Utiliser le proxy personnalisé**: configurer hello HTTP proxy paramètre toouse pour la passerelle, au lieu d’utiliser des configurations dans diahost.exe.config et diawp.exe.config.  L’adresse et le port sont requis.  Le nom d’utilisateur et le mot de passe sont facultatifs selon le paramètre d’authentification de votre proxy.  Tous les paramètres sont chiffrés par le certificat d’informations d’identification de hello de passerelle de hello et stockées localement sur l’ordinateur hôte de passerelle hello.

passerelle de gestion des données Hello Service hôte redémarre automatiquement après avoir enregistré les paramètres de proxy hello mis à jour.

Une fois la passerelle a été inscrit avec succès, si vous souhaitez tooview ou mettre à jour les paramètres de proxy, utilisez le Gestionnaire de Configuration de passerelle de gestion de données.

1. Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**.
2. Commutateur toohello **paramètres** onglet.
3. Cliquez sur **modification** lien dans **HTTP Proxy** hello toolaunch de section **définir le Proxy HTTP** boîte de dialogue.  
4. Après avoir cliqué sur hello **suivant** bouton, vous voyez une boîte de dialogue Avertissement demandant pour vos paramètres du proxy autorisation toosave hello et le redémarrage du Service hôte de passerelle de hello.

Vous pouvez afficher et mettre à jour le proxy HTTP à l’aide de l’outil Gestionnaire de Configuration.

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Si vous configurez un serveur proxy avec l’authentification NTLM, le Service hôte de passerelle s’exécute sous un compte de domaine hello. Si vous modifiez le mot de passe hello pour le compte de domaine hello plus tard, n’oubliez pas de tooupdate les paramètres de configuration de service de hello et redémarrez-le en conséquence. En raison de la spécification de toothis, nous vous suggérons de que vous utilisez un serveur dédié domaine compte tooaccess hello proxy qui ne nécessite pas un mot de passe tooupdate hello fréquemment.
>
>

### <a name="configure-proxy-server-settings"></a>Configurer les paramètres du serveur proxy
Si vous sélectionnez **utiliser le proxy système** définition pour le proxy de hello HTTP, la passerelle utilise hello paramètre de proxy dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est spécifié dans diahost.exe.config et diawp.exe.config, passerelle connecte toocloud service directement sans passer par le proxy. Hello procédure suivante fournit des instructions pour mettre à jour le fichier de diahost.exe.config hello.  

1. Dans l’Explorateur de fichiers, constituent une copie de sauvegarde de C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared\diahost.exe.config tooback fichier d’origine de hello.
2. Lancez Notepad.exe en tant qu’administrateur, puis ouvrez le fichier texte C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Vous recherchez balise par défaut de hello system.net comme indiqué dans hello suivant de code :

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Vous pouvez ensuite ajouter les détails du serveur proxy comme indiqué dans hello l’exemple suivant :

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Propriétés supplémentaires sont autorisées dans les paramètres hello proxy balise toospecify hello requis comme scriptLocation. Consultez trop[proxy, élément (paramètres réseau)](https://msdn.microsoft.com/library/sa91de1e.aspx) sur la syntaxe.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Enregistrer le fichier de configuration hello dans l’emplacement d’origine de hello, puis redémarrez hello service hôte de passerelle de gestion de données, qui Récupère les modifications hello. service de hello toorestart : utiliser l’applet services à partir du Panneau de configuration hello ou hello **Gestionnaire de Configuration de passerelle de gestion de données** > cliquez sur hello **arrêter le Service** , puis cliquez sur hello **Démarrer le Service**. Si le service de hello ne démarre pas, il est probable qu’une syntaxe de balise XML incorrecte a été ajoutée dans le fichier de configuration d’application hello qui a été modifié.

> [!IMPORTANT]
> N’oubliez pas de tooupdate **les deux** diahost.exe.config et diawp.exe.config.  


En outre les points toothese, vous devez également toomake que Microsoft Azure se trouve dans la liste blanche d’adresses de votre entreprise. liste Hello des adresses IP de Microsoft Azure valides peut être téléchargée à partir de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Symptômes possibles des erreurs liées au pare-feu et au serveur proxy
Si vous rencontrez des erreurs toohello similaire après ceux, il est probable en raison de la configuration tooimproper de hello pare-feu ou un serveur proxy, qui bloque la passerelle de connexion tooauthenticate de fabrique tooData lui-même. Consultez tooensure de section tooprevious votre serveur proxy et de pare-feu sont configurés correctement.

1. Lorsque vous essayez de passerelle de hello tooregister, vous recevez hello l’erreur suivante : « clé de passerelle n’a pas pu tooregister hello. Avant de réessayer la clé de passerelle tooregister hello, vérifiez que hello passerelle de gestion des données est dans un état connecté et hello Service hôte de passerelle de gestion des données est démarré. »
2. Lorsque vous ouvrez le Gestionnaire de configuration, l’état indiqué est « Déconnecté » ou « En cours de connexion ». Lors de l’affichage des journaux des événements Windows, sous « Observateur d’événements » > « Applications et Services Logs » > « Passerelle de gestion des données », vous voyez des messages d’erreur tels que hello l’erreur suivante :`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Ouvrir le port 8050 pour le chiffrement des informations d’identification
Hello **informations d’identification du paramètre** application utilise hello port entrant **8050** passerelle de toohello toorelay informations d’identification lorsque vous configurez un site local lié à service Bonjour portail Azure. Pendant l’installation de la passerelle, par défaut, installation de la passerelle hello ouvre sur l’ordinateur de passerelle hello.

Si vous utilisez un pare-feu tiers, vous pouvez ouvrir manuellement le port hello 8050. Si vous rencontrez des problème de pare-feu pendant l’installation de la passerelle, vous pouvez essayer d’utiliser hello suivant de passerelle de commande tooinstall hello sans configurer le pare-feu hello.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Si vous ne choisissez pas tooopen port hello 8050 sur l’ordinateur de passerelle hello, utilisent des mécanismes de différent à l’aide de hello **informations d’identification du paramètre** tooconfigure les données d’application stocke des informations d’identification. Vous pouvez par exemple utiliser l’applet de commande PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) . Consultez la section [Configuration des informations d’identification et de la sécurité](#set-credentials-and-securityy) pour savoir comment configurer les informations d’identification de la banque de données.

## <a name="update"></a>Mettre à jour
Par défaut, passerelle de gestion des données est automatiquement mis à jour lorsqu’une version plus récente de la passerelle de hello est disponible. passerelle de Hello n’est pas mis à jour jusqu'à ce que toutes les tâches planifiée de hello sont terminés. Aucune autre tâche n’est traitées par la passerelle de hello avant la fin de l’opération de mise à jour hello. En cas de mise à jour hello, passerelle est restaurée toohello une ancienne version.

Vous consultez heure de mise à jour planifiée de hello Bonjour suivant place :

* page des propriétés passerelle Hello hello portail Azure.
* Page d’accueil du Gestionnaire de Configuration de passerelle de gestion de données de hello
* Message de notification de la barre d’état du système.

onglet Accueil de Hello Hello Gestionnaire de Configuration de passerelle de gestion de données affiche la planification de mise à jour de hello et passerelle de hello hello dernière heure a été installé ou mis à jour.

![Planifier les mises à jour](media/data-factory-data-management-gateway/UpdateSection.png)

Vous pouvez installer les mises à jour hello immédiatement ou attendre hello passerelle toobe est automatiquement mis à jour au moment de hello planifiée. Par exemple, hello ci-dessous illustre image hello de message de notification montrée dans hello Gestionnaire de Configuration de passerelle en même temps que le bouton de mise à jour hello que vous pouvez cliquer sur tooinstall immédiatement.

![Mise à jour dans DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

message de notification Hello dans la barre d’état système hello se présente comme dans hello suivant image :

![Message de barre d’état système](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Vous consultez État hello d’opération de mise à jour (manuelle ou automatique) dans la barre d’état système hello. Lorsque vous lancez le Gestionnaire de Configuration de passerelle prochaine, vous voyez un message de notification hello cette passerelle hello a été mis à jour avec un lien trop[quelle est la nouvelle rubrique](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>fonctionnalité de mise à jour automatique toodisable/activer
Vous pouvez désactiver/activer fonction hello en procédant comme hello comme suit :

[Pour une passerelle à nœud unique]
1. Lancez Windows PowerShell sur l’ordinateur de passerelle hello.
2. Basculez le dossier C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript de toohello.
3. Exécution hello suivant commande tooturn hello-mise à jour automatique des fonctionnalités (désactiver).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn à nouveau sur :

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Pour une passerelle hautement disponible et évolutive à plusieurs nœuds (version préliminaire)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Lancez Windows PowerShell sur l’ordinateur de passerelle hello.
2. Basculez le dossier C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript de toohello.
3. Exécution hello suivant commande tooturn hello-mise à jour automatique des fonctionnalités (désactiver).   

    Pour une passerelle avec une fonctionnalité de haute disponibilité (version préliminaire), un paramètre AuthKey supplémentaire est requis.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn à nouveau sur :

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Si vous accédez à portal de hello à partir d’un ordinateur différent de l’ordinateur de passerelle hello, il se peut que vous devez vous assurer que les applications du Gestionnaire d’informations d’identification hello peuvent se connecter toohello machine de la passerelle. Si l’application hello ne peut pas atteindre l’ordinateur de passerelle hello, il ne vous permet pas tooset les informations d’identification pour la source de données hello et la source de données toohello tootest connexion.  

Lorsque vous utilisez hello **informations d’identification du paramètre** , application de portail de hello chiffre les informations d’identification de l’hello avec certificat hello spécifié dans hello **certificat** onglet Hello **passerelle Gestionnaire de configuration** sur l’ordinateur de passerelle hello.

Si vous recherchez une approche basée sur les API pour le chiffrement des informations d’identification hello, vous pouvez utiliser hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) informations d’identification de tooencrypt d’applet de commande PowerShell. applet de commande Hello utilise un certificat hello que cette passerelle est configurée toouse tooencrypt hello références. Vous ajoutez des informations d’identification chiffrées toohello **EncryptedCredential** élément Hello **connectionString** Bonjour JSON. Vous utilisez hello JSON avec hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) applet de commande ou Bonjour éditeur Data Factory.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Il existe une autre approche pour définir les informations d’identification à l’aide de Data Factory Editor. Si vous créez un serveur SQL Server lié service à l’aide de l’éditeur hello et que vous entrez des informations d’identification en texte brut, les informations d’identification hello sont chiffrées à l’aide d’un certificat qui est propriétaire de service de fabrique de données hello. Il n’utilise pas de certificat hello que cette passerelle est toouse configuré. Bien que cette approche puisse être un peu plus rapide dans certains cas, elle reste moins sécurisée. Par conséquent, nous vous recommandons de suivre cette approche uniquement à des fins de développement/test.

## <a name="powershell-cmdlets"></a>Applets de commande PowerShell
Cette section décrit comment toocreate et inscrire une passerelle à l’aide des applets de commande PowerShell de Azure.

1. Lancez **Azure PowerShell** en mode administrateur.
2. Connectez-vous à tooyour compte Azure en exécutant hello suivant de commande et entrez vos informations d’identification Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Hello d’utilisation **New-AzureRmDataFactoryGateway** toocreate de l’applet de commande une passerelle logique comme suit :

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Exemple de commande et de sortie**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. Dans Azure PowerShell, basculez toohello dossier : **C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript\**. Exécutez **RegisterGateway.ps1** liées à la variable locale de hello **$Key** comme indiqué dans hello commande suivante. Ce script enregistre l’agent du client hello installé sur votre ordinateur avec la passerelle logique de hello que vous créez précédemment.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Vous pouvez inscrire la passerelle hello sur un ordinateur distant à l’aide du paramètre de IsRegisterOnRemoteMachine hello. Exemple :

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Vous pouvez utiliser hello **Get-AzureRmDataFactoryGateway** liste de hello tooget applet de commande de passerelles dans votre fabrique de données. Hello lorsque **état** montre **online**, cela signifie que votre passerelle est toouse prêt.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Vous pouvez supprimer une passerelle à l’aide de hello **Remove-AzureRmDataFactoryGateway** applet de commande et de mise à jour la description d’une passerelle à l’aide de hello **Set-AzureRmDataFactoryGateway** applets de commande. Pour obtenir la syntaxe et d’autres détails sur ces applets de commande, consultez la rubrique Référence des applets de commande Azure Data Factory.  

### <a name="list-gateways-using-powershell"></a>Répertorier les passerelles à l’aide de PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Supprimer une passerelle à l’aide de PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Étapes suivantes
* Consultez la page [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) . Hello procédure pas à pas, vous créez un pipeline qui utilise des données de toomove hello passerelle à partir d’un tooan de base de données SQL Server locale blob Azure.  
