---
title: "Passerelle de gestion des données pour Data Factory | Microsoft Docs"
description: "Mettez en place une passerelle de données pour déplacer vos données entre un emplacement local et le cloud. Utilisez la passerelle de gestion des données dans Azure Data Factory pour déplacer vos données."
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
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a>Passerelle de gestion de données
La passerelle de gestion des données est un agent client que vous devez installer dans votre environnement local pour permettre la copie des données entre les magasins de données cloud et locaux. Les magasins de données locaux pris en charge par Data Factory sont répertoriés dans la section [Sources de données prises en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .

Cet article vient compléter la procédure pas à pas de l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) . Dans cette procédure pas à pas, vous créez un pipeline qui utilise la passerelle qui déplace les données d’une base de données SQL Server locale vers un objet blob Azure. Cet article fournit des informations détaillées sur la passerelle de gestion des données. 

Vous pouvez augmenter le nombre des instances d’une passerelle de gestion des données en associant plusieurs machines locales avec la passerelle. Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud. Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique. Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.

> [!NOTE]
> Actuellement, la passerelle prend en charge uniquement l’activité de copie et l’activité de procédure stockée dans Data Factory. Il n’est pas possible d’utiliser la passerelle à partir d’une activité personnalisée pour accéder à des sources de données locales.      

## <a name="overview"></a>Vue d'ensemble
### <a name="capabilities-of-data-management-gateway"></a>Fonctionnalités de la passerelle de gestion des données
La passerelle de gestion des données offre les fonctionnalités suivantes :

* Modélisation des sources de données locales et des sources de données sur le cloud au sein de la même fabrique de données, et déplacement des données.
* Un point unique de surveillance et de gestion avec une visibilité de l’état de la passerelle à partir de la page Data Factory.
* Gestion sécurisée de l’accès aux sources de données locales.
  * Aucune modification du pare-feu d’entreprise n’est requise. La passerelle établit uniquement des connexions HTTP sortantes pour l’accès à Internet.
  * Chiffrement des informations d’identification pour vos magasins de données locaux à l’aide de votre certificat.
* Déplacer les données efficacement : les données sont transférées en parallèle et résistent aux problèmes intermittents du réseau, grâce à la logique de nouvelle tentative automatique.

### <a name="command-flow-and-data-flow"></a>Flux de commandes et flux de données
Lorsque vous utilisez une activité de copie pour copier des données entre des machines locales et cloud, l’activité utilise une passerelle pour transférer les données à partir de la source de données locale vers le cloud et vice versa.

Voici un flux de données global et un résumé des étapes pour la copie à l’aide de la passerelle de données : ![Flux de données à l’aide de la passerelle](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Le développeur des données crée une passerelle pour une fabrique de données Azure à l’aide du [portail Azure](https://portal.azure.com)ou d’une [applet de commande PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).
2. Le développeur de données crée un service lié pour un magasin de données local en spécifiant la passerelle. Dans le cadre de la configuration du service lié, le développeur des données utilise l’application de configuration des informations d’identification pour spécifier les types d’authentification et les informations d’identification.  La boîte de dialogue de l’application de configuration des informations d’identification communique avec le magasin de données pour tester la connexion et la passerelle afin d’enregistrer les informations d’identification.
3. La passerelle chiffre les informations d’identification avec le certificat associé à la passerelle (fourni par le développeur des données) avant d’enregistrer les informations d’identification dans le cloud.
4. Le service Data Factory communique avec la passerelle pour la planification et la gestion des tâches via un canal de contrôle qui utilise une file d’attente Azure Service Bus partagée. Lorsqu’une tâche de l’activité de copie doit être lancée, Data Factory place en file d’attente la requête ainsi que les informations d’identification. La passerelle lance la tâche après avoir interrogé la file d'attente.
5. La passerelle déchiffre les informations d’identification avec le même certificat puis se connecte au magasin de données local avec le type d’authentification et les informations d’identification appropriés.
6. La passerelle copie les données d’un magasin local vers un stockage cloud, ou vice versa selon la configuration de l'activité de copie dans le pipeline de données. Pour cette étape, la passerelle communique directement avec le service de stockage basé sur le cloud comme le stockage d'objets blob Azure via un canal sécurisé (HTTPS).

### <a name="considerations-for-using-gateway"></a>Considérations relatives à l’utilisation de la passerelle
* Une seule instance de passerelle de gestion des données peut être utilisée pour plusieurs sources de données locales. Toutefois, **une seule instance de passerelle est liée à une instance d’Azure Data Factory** et ne peut pas être partagée avec une autre instance d’Azure Data Factory.
* Vous ne pouvez installer qu’**une seule instance de la passerelle de gestion de données** sur un même ordinateur. Si deux fabriques de données doivent accéder aux sources de données locales, vous devez installer des passerelles sur deux ordinateurs locaux. En d’autres termes, une passerelle est liée à une instance d’Azure Data Factory spécifique
* La **passerelle n’a pas besoin d’être sur la même machine que la source de données**. Toutefois, avoir une passerelle plus proche de la source de données réduit le temps de connexion de la passerelle à la source de données. Nous vous recommandons d’installer la passerelle sur un ordinateur différent de celui qui héberge la source de données locale. Lorsque la source de données et la passerelle se trouvent sur des machines différentes, la passerelle ne demande pas de ressources de la source de données.
* Vous pouvez avoir **plusieurs passerelles sur différents ordinateurs connectés à la même source de données locale**. Par exemple, vous pouvez avoir deux passerelles desservant deux fabriques de données, alors que la même source de données locale est enregistrée auprès des deux fabriques de données.
* Si une passerelle est déjà installée sur votre ordinateur desservant un scénario **Power BI**, installez une **passerelle distincte pour Azure Data Factory** sur un autre ordinateur.
* Vous devez utiliser la passerelle même lorsque vous utilisez **ExpressRoute**.
* Considérez votre source de données comme une source de données locale (derrière un pare-feu), même lorsque vous utilisez **ExpressRoute**. Utilisez la passerelle pour établir la connectivité entre le service et la source de données.
* Vous devez **utiliser la passerelle** même si la banque de données se trouve dans le cloud sur une **machine virtuelle IaaS Azure**.

## <a name="installation"></a>Installation
### <a name="prerequisites"></a>Prérequis
* Les versions de **système d’exploitation** prises en charge sont Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2. L’installation de la passerelle de gestion des données sur un contrôleur de domaine n’est pas prise en charge.
* .NET framework 4.5.1 ou version ultérieure est requis. Si vous installez la passerelle sur un ordinateur Windows 7, installez .NET Framework 4.5 ou une version ultérieure. Consultez [Configuration système requise pour .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) pour plus d’informations.
* La **configuration** recommandée pour l’ordinateur de passerelle est la suivante : au moins 2 GHz, 4 cœurs, 8 Go de RAM et 80 Go d’espace disque.
* Si l’ordinateur hôte est en veille prolongée, la passerelle ne répond pas à la demande de données. Vous devez donc configurer un **plan de gestion de l’alimentation** approprié sur l’ordinateur avant d’installer la passerelle. L’installation de la passerelle ouvre un message si l’ordinateur est configuré pour la mise en veille prolongée.
* Vous devez être administrateur sur la machine pour installer et configurer la passerelle de gestion des données avec succès. Vous pouvez ajouter des utilisateurs supplémentaires au groupe Windows local **Utilisateurs de la passerelle de gestion des données**. Les membres de ce groupe sont en mesure d’utiliser l’outil **Gestionnaire de configuration de passerelle de gestion des données** pour configurer la passerelle.

Étant donné que l’activité de copie s’exécute selon une fréquence spécifique, l’utilisation des ressources (processeur, mémoire) sur l’ordinateur suit également le même modèle avec des pics et des baisses d’inactivité. L'utilisation des ressources dépend également en grande partie de la quantité de données déplacées. Lorsque plusieurs travaux sont en cours, vous constaterez une augmentation des ressources utilisées pendant les heures de pointe.

### <a name="installation-options"></a>Options d’installation
La passerelle de gestion des données peut être installée comme suit :

* En téléchargeant un package d’installation MSI à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).  Le fichier MSI peut également servir à mettre à niveau la passerelle de gestion des données existante vers la version la plus récente, en conservant tous les paramètres.
* En cliquant sur le lien **Télécharger et installer la passerelle de données** sous INSTALLATION MANUELLE ou **Installer directement sur cet ordinateur** sous INSTALLATION RAPIDE. Pour des instructions pas à pas sur l’utilisation de l’installation rapide, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) . L’étape manuelle vous amène au centre de téléchargement.  Les instructions pour télécharger et installer la passerelle à partir du centre de téléchargement se trouvent dans la section suivante.

### <a name="installation-best-practices"></a>Meilleures pratiques d’installation :
1. Définissez un plan d'alimentation sur l'ordinateur hôte de la passerelle afin d’empêcher la mise en veille prolongée. Si l’ordinateur hôte est en veille prolongée, la passerelle ne répond pas à la demande de données.
2. Sauvegardez le certificat associé à la passerelle.

### <a name="install-the-gateway-from-download-center"></a>Installer la passerelle à partir du Centre de téléchargement
1. Accédez à la [page de téléchargement de la passerelle de gestion des données Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).
2. Cliquez sur **Télécharger**, sélectionnez la version appropriée (**32 bits** ou **64 bits**), puis cliquez sur **Suivant**.
3. Exécutez le **MSI** directement ou enregistrez-le sur votre disque dur avant de l’exécuter.
4. Dans la page **Bienvenue**, sélectionnez une **langue** et cliquez sur **Suivant**.
5. **Acceptez** le Contrat de Licence Utilisateur Final et cliquez sur **Suivant**.
6. Sélectionnez le **dossier** d’installation de la passerelle, puis cliquez sur **Suivant**.
7. Dans la page **Prêt pour l’installation**, cliquez sur **Installer**.
8. Cliquez sur **Terminer** pour terminer l’installation.
9. Obtenez la clé à partir du portail Azure. Pour des instructions pas à pas, consultez la section suivante.
10. Sur la page **Enregistrer la passerelle** du **Gestionnaire de configuration de passerelle de gestion de données** en cours d’exécution sur votre machine, procédez comme suit :
    1. Collez la clé dans le texte.
    2. Éventuellement, cliquez sur **Afficher la clé de passerelle** pour afficher le texte de la clé.
    3. Cliquez sur **S'inscrire**.

### <a name="register-gateway-using-key"></a>Inscrire la passerelle à l’aide de la clé
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a>Si vous n’avez pas déjà créé une passerelle logique dans le portail
Pour créer une passerelle dans le portail et obtenir la clé à partir de la page **Configurer**, suivez les étapes de la procédure pas à pas de l’article [Déplacement de données entre des sources locales et le cloud](data-factory-move-data-between-onprem-and-cloud.md).    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a>Si vous avez déjà créé la passerelle logique dans le portail
1. Dans le portail Azure, accédez à la page **Data Factory**, puis cliquez sur la vignette **Services liés**.

    ![Page Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Dans la page **Services liés**, sélectionnez la **passerelle** logique que vous avez créée dans le portail.

    ![passerelle logique](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Dans la page **Passerelle de données**, cliquez sur **Télécharger et installer la passerelle de données**.

    ![Lien de téléchargement dans le portail](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Dans la page **Configurer**, cliquez sur **Recréer une clé**. Dans le message d’avertissement, cliquez sur Oui après l’avoir lu attentivement.

    ![Recréer une clé](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Cliquez sur le bouton Copier en regard de la clé. La clé est copiée dans le Presse-papiers.

    ![Copier la clé](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Icônes de la barre d’état système/notifications
L’illustration suivante représente certaines des icônes de barre d’état qui s’affichent.

![Icônes de la barre d’état système](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Si vous déplacez le curseur sur les icônes/messages de notification de la barre d’état système, vous afficherez des informations supplémentaires sur l’état d’opération de la passerelle/la progression de la mise à jour dans une fenêtre contextuelle.

### <a name="ports-and-firewall"></a>Ports et pare-feu
Vous devez porter votre attention sur deux pare-feu : le **pare-feu d’entreprise**, exécuté sur le routeur central de l’organisation et le **Pare-feu Windows**, configuré en tant que démon sur l’ordinateur local sur lequel la passerelle est installée.  

![Pare-feu](./media/data-factory-data-management-gateway/firewalls2.png)

Au niveau du pare-feu d’entreprise, vous devez configurer les domaines et ports de sortie suivants :

| Noms de domaine | Ports | Description |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Utilisé pour la communication avec le serveur principal du service Déplacement des données |
| *.core.windows.net |443 |Utilisé pour une copie intermédiaire à l’aide d’objets Blob Azure (si configuré)|
| *.frontend.clouddatahub.net |443 |Utilisé pour la communication avec le serveur principal du service Déplacement des données |


Au niveau du pare-feu Windows, ces ports de sortie sont normalement activés. Sinon, vous pouvez configurer en conséquence les domaines et les ports sur l’ordinateur de passerelle.

> [!NOTE]
> 1. Selon votre source/vos récepteurs, vous devrez peut-être ajouter des domaines et des ports de sortie supplémentaires à la liste verte de votre pare-feu d’entreprise/Windows.
> 2. Pour certaines bases de données cloud (par exemple : [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), vous devrez peut-être ajouter l’adresse IP de l’ordinateur de la passerelle à la liste verte dans la configuration du pare-feu.
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a>Copier des données d’une banque de données source vers une banque de données de récepteur
Assurez-vous que les règles de pare-feu sont correctement activées sur le pare-feu d’entreprise, sur le pare-feu Windows de l’ordinateur de passerelle, ainsi que sur le magasin de données lui-même. Activer ces règles permet à la passerelle de se connecter correctement à la source et au récepteur. Activez les règles pour chaque magasin de données impliqué dans l’opération de copie.

Par exemple, pour copier à partir d’une **banque de données locale vers un récepteur Azure SQL Database ou un récepteur Azure SQL Data Warehouse**, effectuez les opérations suivantes :

* Autorisez le trafic **TCP** sortant sur le port **1433** pour le pare-feu Windows et le pare-feu d’entreprise.
* Configurez les paramètres de pare-feu du serveur SQL Azure pour ajouter l’adresse IP de l’ordinateur de passerelle à la liste d’adresses IP autorisées.

> [!NOTE]
> Si votre pare-feu n’autorise pas le port de sortie 1433, la passerelle ne peut pas accéder directement à Azure SQL. Dans ce cas, vous pouvez utiliser la [copie intermédiaire](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) sur SQL Azure Database/SQL Azure DW. Dans ce scénario, vous auriez uniquement besoin du protocole HTTPS (port 443) pour le déplacement des données.
>
>


### <a name="proxy-server-considerations"></a>Considérations relatives aux serveurs proxy
Si votre environnement de réseau d’entreprise utilise un serveur proxy pour accéder à Internet, configurez la passerelle de gestion des données pour utiliser les bons paramètres de proxy. Vous pouvez définir le proxy lors de la phase initiale de l’enregistrement.

![Définir le serveur proxy lors de l’inscription](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

La passerelle utilise le serveur proxy pour se connecter au service cloud. Cliquez sur le lien **Modifier** pendant l’installation initiale. La boîte de dialogue **Paramètre proxy** s’affiche.

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxySettings.png)

Il existe trois options de configuration :

* **Ne pas utiliser de proxy**: la passerelle n’utilise pas explicitement de proxy pour se connecter aux services cloud.
* **Utiliser le proxy système** : la passerelle utilise le paramètre de proxy configuré dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est configuré dans diahost.exe.config et diawp.exe.config, la passerelle se connecte au service cloud directement sans passer par le proxy.
* **Utiliser un proxy personnalisé** : configurez les paramètres du proxy HTTP à utiliser pour la passerelle, au lieu d’utiliser les configurations dans diahost.exe.config et diawp.exe.config.  L’adresse et le port sont requis.  Le nom d’utilisateur et le mot de passe sont facultatifs selon le paramètre d’authentification de votre proxy.  Tous les paramètres sont chiffrés avec le certificat d’informations d’identification de la passerelle et stockés localement sur la machine hôte de passerelle.

Le service hôte de la passerelle de gestion des données redémarre automatiquement après avoir enregistré les paramètres de proxy mis à jour.

Une fois la passerelle enregistrée avec succès, si vous souhaitez afficher ou mettre à jour les paramètres de proxy, utilisez le gestionnaire de configuration de la passerelle de gestion des données.

1. Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**.
2. Basculez vers l’onglet **Paramètres** .
3. Cliquez sur le lien **Modifier** dans la section **Serveur proxy HTTP** pour lancer la boîte de dialogue **Définir le proxy HTTP**.  
4. Après avoir cliqué sur le bouton **Suivant** , vous verrez une boîte de dialogue d’avertissement demandant l’autorisation d’enregistrer les paramètres de proxy et de redémarrer le service hôte de la passerelle.

Vous pouvez afficher et mettre à jour le proxy HTTP à l’aide de l’outil Gestionnaire de Configuration.

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Si vous configurez un serveur proxy avec l’authentification NTLM, le service hôte de la passerelle s’exécute sous le compte du domaine. Si vous modifiez le mot de passe du compte du domaine ultérieurement, veillez à mettre à jour les paramètres de configuration pour le service et à redémarrer ce dernier en conséquence. En raison de cette exigence, nous vous conseillons d’utiliser un compte de domaine dédié qui ne nécessite pas de mettre à jour le mot de passe fréquemment pour accéder au serveur proxy.
>
>

### <a name="configure-proxy-server-settings"></a>Configurer les paramètres du serveur proxy
Si vous sélectionnez le paramètre **Utiliser le proxy système** pour le proxy HTTP, la passerelle utilise le paramètre du proxy dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est spécifié dans diahost.exe.config et diawp.exe.config, la passerelle se connecte au service cloud directement sans passer par le proxy. La procédure suivante fournit des instructions pour mettre à jour le fichier de configuration diahost.exe.config.  

1. Dans l’Explorateur de fichiers, effectuez une copie de sauvegarde de C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config pour sauvegarder le fichier d’origine.
2. Lancez Notepad.exe en tant qu’administrateur, puis ouvrez le fichier texte C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. La balise par défaut pour system.net apparaît dans le code suivant :

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Vous pouvez ensuite ajouter les détails du serveur proxy comme illustré dans l’exemple suivant :

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Vous pouvez ajouter des propriétés supplémentaires à l’intérieur de la balise de proxy pour spécifier les paramètres requis comme scriptLocation. Reportez-vous à la page de syntaxe [proxy, élément (paramètres réseau)](https://msdn.microsoft.com/library/sa91de1e.aspx).

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Enregistrez le fichier de configuration à l’emplacement d’origine, puis redémarrez le service hôte de passerelle de gestion des données, qui relève les modifications. Pour redémarrer le service, utilisez l’applet de services du panneau de configuration, ou allez dans le **Gestionnaire de configuration de passerelle de gestion des données**, cliquez sur le bouton **Arrêter le service**, puis sur **Démarrer le service**. Si le service ne démarre pas, il est probable qu’une syntaxe de balise XML incorrecte ait été ajoutée dans le fichier de configuration d’application que vous avez modifié.

> [!IMPORTANT]
> N’oubliez pas de mettre à jour diahost.exe.config **et** diawp.exe.config.  


Outre ces points, vous devez également vous assurer que Microsoft Azure figure dans la liste d’autorisation de votre entreprise. Vous pouvez télécharger la liste des adresses IP Microsoft Azure valides à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Symptômes possibles des erreurs liées au pare-feu et au serveur proxy
Si vous rencontrez l’une des erreurs suivantes, cela signifie que vous avez probablement mal configuré le serveur proxy ou le pare-feu, et que la passerelle ne peut pas se connecter à Data Factory pour s’authentifier. Reportez-vous à la section précédente pour vous assurer que votre pare-feu et votre serveur proxy sont correctement configurés.

1. Lorsque vous tentez d’inscrire la passerelle, vous recevez le message d’erreur suivant : « Nous n’avons pas pu enregistrer la clé de passerelle. Avant de réessayer d’enregistrer la clé de passerelle, vérifiez que la passerelle de gestion des données est connectée et que le service d’hébergement de la passerelle de gestion des données est en cours d’exécution. »
2. Lorsque vous ouvrez le Gestionnaire de configuration, l’état indiqué est « Déconnecté » ou « En cours de connexion ». Lorsque vous affichez les journaux des événements Windows, sous « Observateur d’événements » > « Journaux des applications et services » > « Passerelle de gestion des données », des messages d’erreur tels que le suivant s’affichent : `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Ouvrir le port 8050 pour le chiffrement des informations d’identification
Le port de trafic entrant **8050** est utilisé par l’application **Définition des informations d’identification** pour relayer les informations d’identification à la passerelle lorsque vous configurez un service lié local dans le portail Azure. Lors de l’installation de la passerelle, l’installation de la passerelle ouvre cette dernière par défaut sur l’ordinateur de passerelle.

Si vous utilisez un pare-feu tiers, vous pouvez ouvrir manuellement le port 8050. Si vous rencontrez des problèmes de pare-feu lors de l’installation de la passerelle, vous pouvez essayer d’utiliser la commande suivante pour installer la passerelle sans configurer le pare-feu.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Si vous préférez ne pas ouvrir le port 8050 sur l’ordinateur passerelle, utilisez d’autres mécanismes que l’application **Définition des informations d’identification** pour configurer les informations d’identification de la banque de données. Vous pouvez par exemple utiliser l’applet de commande PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) . Consultez la section [Configuration des informations d’identification et de la sécurité](#set-credentials-and-securityy) pour savoir comment configurer les informations d’identification de la banque de données.

## <a name="update"></a>Mettre à jour
Par défaut, la passerelle de gestion des données est automatiquement mise à jour lorsqu’une version plus récente est disponible. La passerelle n’est pas mise à jour tant que toutes les tâches planifiées ne sont pas terminées. Aucune autre tâche n’est traitée par la passerelle avant la fin de l’opération de mise à jour. Si la mise à jour échoue, la passerelle est restaurée vers son ancienne version.

L’heure de mise à jour planifiée s’affiche aux emplacements suivants :

* Page Propriétés de la passerelle dans le portail Azure.
* Page d’accueil du gestionnaire de configuration de la passerelle de gestion des données
* Message de notification de la barre d’état du système.

L’onglet Accueil du Gestionnaire de configuration de passerelle de gestion des données affiche la planification de la mise à jour, ainsi que la date de la dernière mise à jour/installation de la passerelle.

![Planifier les mises à jour](media/data-factory-data-management-gateway/UpdateSection.png)

Vous pouvez installer la mise à jour immédiatement ou attendre que la passerelle soit mise à jour automatiquement à l’heure planifiée. Par exemple, l’image suivante montre le message de notification affiché dans le Gestionnaire de configuration de passerelle, ainsi que le bouton de mise à jour qui vous permet d’installer cette dernière immédiatement.

![Mise à jour dans DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

Le message de notification dans la barre d’état système se présenterait comme l’image suivante :

![Message de barre d’état système](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Vous voyez s’afficher la progression de l’opération de mise à jour (manuelle ou automatique) dans la barre d’état système. À la prochaine ouverture du Gestionnaire de configuration de passerelle, un message s’affiche dans la barre de notification, vous indiquant que la passerelle a été mise à jour, et contenant un lien vers la rubrique relative aux [nouveautés](data-factory-gateway-release-notes.md).

### <a name="to-disableenable-auto-update-feature"></a>Pour activer/désactiver une fonctionnalité de mise à jour automatique
Vous pouvez désactiver/activer la fonctionnalité de mise à jour automatique comme suit :

[Pour une passerelle à nœud unique]
1. Lancez Windows PowerShell sur l’ordinateur de passerelle.
2. Accédez au dossier C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.
3. Exécutez la commande suivante pour désactiver la fonctionnalité de mise à jour automatique.   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. Pour la réactiver :

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Pour une passerelle hautement disponible et évolutive à plusieurs nœuds (version préliminaire)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Lancez Windows PowerShell sur l’ordinateur de passerelle.
2. Accédez au dossier C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.
3. Exécutez la commande suivante pour désactiver la fonctionnalité de mise à jour automatique.   

    Pour une passerelle avec une fonctionnalité de haute disponibilité (version préliminaire), un paramètre AuthKey supplémentaire est requis.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. Pour la réactiver :

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

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
Si vous accédez au portail à partir d’un ordinateur différent de l’ordinateur de passerelle, vous devrez peut-être vous assurer que l’application Gestionnaire d’informations d’identification peut se connecter à l’ordinateur de passerelle. Sinon, vous ne pourrez pas définir les informations d’identification de la source de données, ni tester la connexion à la source de données.  

Quand vous utilisez l’application **Définition des informations d’identification**, le portail chiffre les informations d’identification avec le certificat que vous avez spécifié dans l’onglet **Certificat** du **Gestionnaire de configuration de passerelle** sur l’ordinateur de passerelle.

Si vous recherchez une approche basée sur une API pour chiffrer les informations d’identification, vous pouvez utiliser l’applet de commande PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) pour chiffrer les informations d’identification. L'applet de commande utilise le certificat qui a servi à configurer la passerelle pour chiffrer les informations d'identification. Vous ajoutez des informations d’identification chiffrées pour l’élément **EncryptedCredential** de **connectionString** dans JSON. Vous utilisez JSON avec l’applet de commande [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) ou dans Data Factory Editor.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Il existe une autre approche pour définir les informations d’identification à l’aide de Data Factory Editor. Si vous créez un service SQL Server lié à l’aide de l’éditeur et entrez les informations d’identification en texte brut, ces informations d’identification sont chiffrées à l’aide d’un certificat appartenant au service Data Factory. Il n’utilise PAS le certificat que passerelle est configurée pour utiliser. Bien que cette approche puisse être un peu plus rapide dans certains cas, elle reste moins sécurisée. Par conséquent, nous vous recommandons de suivre cette approche uniquement à des fins de développement/test.

## <a name="powershell-cmdlets"></a>Applets de commande PowerShell
Cette section décrit comment créer et enregistrer une passerelle à l’aide des applets de commande Azure PowerShell.

1. Lancez **Azure PowerShell** en mode administrateur.
2. Connectez-vous à votre compte Azure en exécutant la commande suivante et en entrant vos informations d’identification Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Utilisez l’applet de commande **New-AzureRmDataFactoryGateway** pour créer une passerelle logique, comme suit :

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

1. Dans Azure PowerShell, accédez au dossier **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**. Exécutez le script **RegisterGateway.ps1** associé à la variable locale **$Key**, comme indiqué dans la commande suivante. Ce script enregistre l’agent client installé sur votre ordinateur avec la passerelle logique que vous avez créée précédemment.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Vous pouvez inscrire la passerelle sur un ordinateur distant en utilisant le paramètre IsRegisterOnRemoteMachine. Exemple :

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Vous pouvez utiliser l’applet de commande **Get-AzureRmDataFactoryGateway** pour obtenir la liste des passerelles dans votre fabrique de données. Lorsque **l’état** est **online**, cela signifie que votre passerelle est prête.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Vous pouvez supprimer une passerelle à l’aide de l’applet de commande **Remove-AzureRmDataFactoryGateway** et mettre à jour la description de la passerelle en utilisant les applets de commande **Set-AzureRmDataFactoryGateway**. Pour obtenir la syntaxe et d’autres détails sur ces applets de commande, consultez la rubrique Référence des applets de commande Azure Data Factory.  

### <a name="list-gateways-using-powershell"></a>Répertorier les passerelles à l’aide de PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Supprimer une passerelle à l’aide de PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Étapes suivantes
* Consultez la page [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) . Dans cette procédure pas à pas, vous créez un pipeline qui utilise la passerelle qui déplace les données d’une base de données SQL Server locale vers un objet blob Azure.  
