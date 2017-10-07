---
title: "aaaCreate et gérer des connexions hybrides | Documents Microsoft"
description: "Découvrez comment toocreate une connexion hybride, gérer les connexion hello et installer le Gestionnaire de connexions hybrides de hello. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Création et gestion des connexions hybrides

> [!IMPORTANT]
> Les connexions hybrides BizTalk ont été supprimées et remplacées par les connexions hybrides App Service. Pour plus d’informations, y compris comment toomanage vos connexions hybrides BizTalk existant, consultez [connexions hybrides de Azure App Service](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Vue d’ensemble des étapes de hello
1. Créer une connexion hybride en entrant hello **nom d’hôte** ou **nom de domaine complet** de ressource locale de hello dans votre réseau privé.
2. Liez votre applications web Azure ou applications mobiles Azure toohello connexion hybride.
3. Installer hello Gestionnaire de connexions hybrides sur votre ressource locale et se connecter toohello connexion hybride spécifique. Hello portail Azure fournit une expérience de clic de tooinstall et se connecter.
4. Gestion des connexions hybrides et de leurs clés de connexion.

Cette rubrique répertorie ces étapes. 

> [!IMPORTANT]
> Il est possible de tooset une adresse IP de la connexion hybride point de terminaison tooan. Si vous utilisez une adresse IP, vous pouvez ou pouvez atteindre pas la ressource locale de hello, en fonction de votre client. Hello connexion hybride dépend du client hello effectuant une recherche DNS. Dans la plupart des cas, hello **client** est votre code d’application. Si hello client n’effectue pas une recherche DNS, (il ne tente pas adresse IP de hello tooresolve, comme s’il s’agissait d’un nom de domaine (x.x.x.x)), puis le trafic n’est pas envoyé via hello connexion hybride.
> 
> Par exemple (pseudo-code), vous définissez **10.4.5.6** comme hôte local :
> 
> **Hello suivant fonctionne de scénario :**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **Hello scénario ne fonctionne pas :**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Création d’une connexion hybride
Une connexion hybride peuvent être créée dans hello portail Azure à l’aide de Web Apps **ou** à l’aide de BizTalk Services. 

**toocreate connexions hybrides à l’aide de Web Apps**, consultez [connecter Azure Web Apps tooan ressource locale](../app-service-web/web-sites-hybrid-connection-get-started.md). Vous pouvez également installer hello Gestionnaire de connexion hybride (HCM) à partir de votre application web, qui est la méthode hello préféré. 

**toocreate connexions hybrides dans BizTalk Services**:

1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation gauche hello, sélectionnez **BizTalk Services** , puis sélectionnez votre BizTalk Service. 
   
    Si vous n’avez pas de service BizTalk, vous pouvez en [créer un](biztalk-provision-services.md).
3. Sélectionnez hello **connexions hybrides** onglet :  
   ![Onglet Connexions hybrides][HybridConnectionTab]
4. Sélectionnez **créer une connexion hybride** ou sélectionnez hello **ajouter** bouton dans la barre des tâches hello. Entrez hello suivantes :
   
   | Propriété | Description |
   | --- | --- |
   | Nom |Hello hybride nom doit être unique et ne peut pas être hello même nom de la connexion en tant que hello BizTalk Service. Vous pouvez entrer n’importe quel nom, mais soyez précis quant à son objet. Voici quelques exemples : <br/><br/>FichePaie*SQLServer*<br/>ListeFournitures*SharepointServer*<br/>Customers*OracleServer* |
   | Nom d’hôte |Entrez le nom d’hôte complet hello, seul nom d’hôte hello, ou hello adresse IPv4 de la ressource locale de hello. Voici quelques exemples :<br/><br/>monSQLServer<br/>*mySQLServer*.*Domaine*.corp.*votreSociété*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*votreSociété*.com<br/>10.100.10.10<br/><br/>Si vous utilisez des adresses IPv4 de hello, notez que votre code client ou une application peut résoudre l’adresse IP de hello. Consultez hello Important note au début de hello de cette rubrique. |
   | Port |Entrez le numéro de port hello de ressource locale de hello. Par exemple, si vous utilisez des applications web, entrez le port 80 ou 443. Si vous utilisez SQL Server, entrez le port 1433. |
5. Sélectionnez le programme d’installation de hello coche toocomplete hello. 

#### <a name="additional"></a>Informations complémentaires
* Il est possible de créer plusieurs connexions hybrides. Consultez hello [Services BizTalk : tableau comparatif des éditions](biztalk-editions-feature-chart.md) pour nombre hello de connexions autorisées. 
* Chaque connexion hybride est créée avec une paire de chaînes de connexion : des clés Application qui envoient (SEND) et des clés locales qui écoutent (LISTEN). Chaque paire possède une clé primaire et une clé secondaire. 

## <a name="LinkWebSite"></a>Liaison de votre application mobile ou web Azure App Service
toolink une application Web ou une application Mobile dans tooan Azure App Service existant de la connexion hybride, sélectionnez **utiliser une connexion hybride existante** dans le panneau de connexions hybrides hello. Consultez [Accéder aux ressources locales à l’aide de connexions hybrides dans Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Installer hello le Gestionnaire de connexions hybrides local
Après la création d’une connexion hybride, installez hello Gestionnaire de connexions hybrides sur la ressource locale de hello. Vous pouvez le télécharger par le biais de vos applications web Azure ou à partir de votre service BizTalk. Procédure pour BizTalk Services : 

1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation gauche hello, sélectionnez **BizTalk Services** , puis sélectionnez votre BizTalk Service. 
3. Sélectionnez hello **connexions hybrides** onglet :  
   ![Onglet Connexions hybrides][HybridConnectionTab]
4. Dans la barre des tâches hello, sélectionnez **le programme d’installation sur site**:  
   ![Installation locale][HCOnPremSetup]
5. Sélectionnez **installer et configurer** toorun ou téléchargement hello Gestionnaire de connexions hybrides sur hello local system. 
6. Sélectionnez installation de hello toostart hello case à cocher. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Informations complémentaires
* Gestionnaire de connexions hybrides peut être installé sur hello suivant des systèmes d’exploitation :
  
  * Windows Server 2008 R2 (.NET Framework 4.5 et version ultérieures et Windows Management Framework 4.0 et version ultérieures requis)
  * Windows Server 2012 (Windows Management Framework 4.0 et version ultérieures requis)
  * Windows Server 2012 R2
* Après avoir installé le Gestionnaire de connexions hybrides de hello, hello événements suivants se produisent : 
  
  * Hello connexion hybride hébergé sur Azure est automatiquement configuré toouse hello chaîne de connexion d’Application principal. 
  * ressource locale de Hello est automatiquement configuré toouse hello principal chaîne de connexion locale.
* Hello Gestionnaire de connexions hybrides doit utiliser une chaîne de connexion local valide pour l’autorisation. Bonjour Azure Web Apps ou des applications mobiles doivent utiliser une chaîne de connexion d’application valide pour l’autorisation.
* Vous pouvez adapter les connexions hybrides en installant une autre instance du Gestionnaire de connexions hybrides de hello sur un autre serveur. Configurer hello de toouse hello local écouteur même adresse en tant qu’écouteur local de la première hello. Dans ce cas, le trafic de hello est distribuée de manière aléatoire (round robin) entre hello active écouteurs locaux. 

## <a name="ManageHybridConnection"></a>Gestion des connexions hybrides
toomanage vos connexions hybrides, vous pouvez :

* Utilisez hello portail Azure et accédez tooyour BizTalk Service. 
* utiliser les [API REST](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Copiez/régénérez hello des chaînes de connexion hybride
1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Dans le volet de navigation gauche hello, sélectionnez **BizTalk Services** , puis sélectionnez votre BizTalk Service. 
3. Sélectionnez hello **connexions hybrides** onglet :  
   ![Onglet Connexions hybrides][HybridConnectionTab]
4. Sélectionnez hello connexion hybride. Dans la barre des tâches hello, sélectionnez **gérer la connexion**:  
   ![Gérer les options][HCManageConnection]
   
    **Gérer les connexion** listes hello Application locaux et sur les chaînes de connexion. Vous pouvez copier hello les chaînes de connexion ou régénérer hello que clé d’accès utilisée dans la chaîne de connexion hello. 
   
    **Si vous sélectionnez régénérer**, hello clé d’accès partagé utilisée dans hello chaîne de connexion est modifiée. Hello suivant :
   
   * Bonjour portail Azure classic, sélectionnez **synchroniser les clés** Bonjour application Windows Azure.
   * Exécutez de nouveau hello **le programme d’installation local**. Lorsque vous exécutez de nouveau hello localement le programme d’installation, hello ressource locale est automatiquement configuré de chaîne de connexion principale toouse hello mis à jour.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Hello de toocontrol stratégie de groupe de l’utilisation locale les ressources utilisées par une connexion hybride
1. Télécharger hello [modèles d’administration Gestionnaire de connexions hybrides](http://www.microsoft.com/download/details.aspx?id=42963).
2. Extrayez les fichiers hello.
3. Sur l’ordinateur hello qui modifie la stratégie de groupe, hello suivant :  
   
   * Copiez hello. Toohello des fichiers ADMX *%WINROOT%\PolicyDefinitions* dossier.
   * Copiez hello. ADML fichiers toohello *%WINROOT%\PolicyDefinitions\en-us* dossier.

Une fois copiées, vous pouvez utiliser la stratégie d’éditeur de stratégie de groupe toochange hello.

## <a name="next"></a>Suivant
[Connecter des applications Web Azure tooan ressource locale](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Se connecter tooon local SQL Server à partir d’applications Web Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Aperçu des connexions hybrides](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Voir aussi
[API REST pour gérer BizTalk Services sur Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md)  
[Créer un BizTalk Service à l'aide du portail Azure Classic](biztalk-provision-services.md)  
[Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
