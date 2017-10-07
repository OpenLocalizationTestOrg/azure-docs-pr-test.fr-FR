---
title: "aaaConnect tooon local SQL Server à partir d’une application web dans Azure App Service à l’aide de connexions hybrides"
description: "Créer une application web sur Microsoft Azure et le connecter à base de données SQL Server tooan local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a>Se connecter tooon local SQL Server à partir d’une application web dans Azure App Service à l’aide de connexions hybrides
Connexions hybrides peuvent se connecter [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ressources tooon local des applications Web qui utilisent un port TCP statique. Les ressources prises en charge incluent Microsoft SQL Server, MySQL, les API web HTTP, App Service et la plupart des services web personnalisés.

Dans ce didacticiel, vous allez apprendre comment toocreate un Service d’application web application Bonjour [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connecter hello web application tooyour sur site local SQL Server de base de données à l’aide de la nouvelle fonctionnalité de connexion hybride hello, créer un simple ASP.NET application qui utilise la connexion hybride hello et déployer hello application toohello application Service web d’application. Hello terminé l’application web sur Azure stocke les informations d’identification de l’utilisateur dans une base de données d’appartenance local. Hello est supposé aucune expérience préalable à l’aide de Azure ou ASP.NET.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> partie des applications Web Hello de fonctionnalité de connexions hybrides hello est uniquement disponible dans hello [Azure Portal](https://portal.azure.com). toocreate une connexion dans les Services BizTalk, consultez [connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274).  
> 
> 

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suite de produits. Tous sont disponibles gratuitement, de sorte que vous pouvez commencer à développer gratuitement pour Azure.

* **Abonnement Azure** : pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](/pricing/free-trial/).
* **Visual Studio 2013** -consultez d’une version d’évaluation gratuite de Visual Studio 2013, toodownload [téléchargements Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs). Installez ceci avant de poursuivre.
* **Microsoft .NET Framework 3.5 Service Pack 1** : si votre système d'exploitation est Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 ou Windows Server 2008 R2, vous pouvez activer cette mise à jour dans Panneau de configuration &gt; Programmes et fonctionnalités &gt; Activer ou désactiver des fonctionnalités Windows. Sinon, vous pouvez le télécharger depuis hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).
* **SQL Server 2014 Express with Tools** -télécharger Microsoft SQL Server Express gratuitement sur hello [page de base de données de Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx). Choisissez hello **Express** (pas LocalDB) version. Hello **Express with Tools** version inclut SQL Server Management Studio, que vous utiliserez dans ce didacticiel.
* **SQL Server Management Studio Express** - est incluse avec hello SQL Server 2014 Express avec le téléchargement des outils mentionné ci-dessus, mais si vous avez besoin de tooinstall il séparément, vous pouvez télécharger et l’installer à partir de hello [SQL Server Express page de téléchargement](http://www.microsoft.com/web/platform/database.aspx).

Hello est supposé que vous disposez d’un abonnement Azure, que vous avez installé Visual Studio 2013, et que vous avez installé ou activé le .NET Framework 3.5. didacticiel de Hello vous montre comment tooinstall SQL Server 2014 Express dans une configuration qui fonctionne bien avec les connexions hybrides hello fonctionnalité (une instance par défaut avec un port TCP statique). Avant de commencer le didacticiel de hello, téléchargez SQL Server 2014 Express with Tools à partir de l’emplacement hello mentionné ci-dessus, si vous n’avez pas installé de SQL Server.

### <a name="notes"></a>Remarques
toouse un local SQL Server ou la base de données SQL Server Express avec une connexion hybride, TCP/IP doit toobe activé sur un port statique. Les instances par défaut dans SQL Server utilisent le port statique 1433, mais pas les instances nommées.

ordinateur Hello sur lequel vous installez l’agent de gestionnaire de connexions hybrides hello local :

* Connectivité sortante tooAzure devez sur :

| Port | Pourquoi |
| --- | --- |
| 80 |**Obligatoire** pour le port HTTP pour la validation du certificat et éventuellement la connectivité des données. |
| 443 |**Facultatif** pour la connectivité des données. Si la connectivité sortante too443 n’est pas disponible, le port TCP 80 est utilisé. |
| 5671 et 9352 |**Recommandé** mais facultatif pour la connectivité des données. Notez que ce mode entraîne habituellement un débit plus élevé. Si les ports toothese connexion sortante n’est pas disponible, le port TCP 443 est utilisé. |

* Doit être en mesure de tooreach hello *nom d’hôte*:*numéro_port* de votre ressource locale.

Hello dans cet article suppose que vous utilisez le navigateur hello à partir de l’ordinateur hello qui hébergera l’agent de connexion hybride hello localement.

Si vous avez déjà SQL Server est installé dans une configuration et dans un environnement qui répond aux conditions hello décrites ci-dessus, vous pouvez passer et commencer par [créer une base de données SQL Server sur site](#CreateSQLDB).

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a>R : Installation de SQL Server Express, activation de TCP/IP et création d'une base de données SQL Server en local
Cette section vous montre comment tooinstall SQL Server Express, activez TCP/IP et comment créer une base de données afin que votre application web fonctionne avec hello portail Azure.

### <a name="install-sql-server-express"></a>Installation de SQL Server Express
1. tooinstall SQL Server Express, exécutez hello **SQLEXPRWT_x64_ENU.exe** ou **SQLEXPR_x86_ENU.exe** fichier que vous avez téléchargé. Assistant du centre d’Installation SQL Server Hello s’affiche.
   
    ![SQL Server Install][SQLServerInstall]
2. Choisissez **nouvelle installation SQL Server autonome ou ajoutez l’installation existante de fonctionnalités tooan**. Suivez les instructions de hello, en acceptant les choix par défaut hello et les paramètres, jusqu'à ce que vous atteigniez toohello **Configuration de l’Instance** page.
3. Sur hello **Configuration de l’Instance** choisissez **instance par défaut**.
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    Par défaut, instance par défaut de hello de SQL Server écoute les demandes des clients de SQL Server sur le port statique 1433, c'est-à-dire le connexions hybrides fonctionnalité nécessite hello. Les instances nommées utilisent des ports dynamiques et UDP, qui ne sont pas pris en charge par Connexions hybrides.
4. Accepter les valeurs par défaut hello hello **Configuration du serveur** page.
5. Sur hello **Configuration du moteur de base de données** sous **Mode d’authentification**, choisissez **en Mode mixte (authentification SQL Server et l’authentification Windows)**et fournir un mot de passe.
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    Dans ce didacticiel, vous allez utiliser l'authentification SQL Server. Être tooremember vraiment hello un mot de passe que vous fournissez, car vous en aurez besoin ultérieurement.
6. Parcourez reste hello d’installation de hello Assistant toocomplete hello.

### <a name="enable-tcpip"></a>Activation de TCP/IP
tooenable TCP/IP, vous allez utiliser le Gestionnaire de Configuration SQL Server, qui a été installée lors de l’installation de SQL Server Express. Suivez les étapes de hello dans [activer le protocole réseau TCP/IP pour SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) avant de continuer.

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a>Création d'une base de données SQL Server en local
Votre application Visual Studio nécessite une base de données d'appartenance à laquelle Azure puisse accéder. Cela nécessite une base de données SQL Server ou SQL Server Express (pas hello LocalDB base de données hello utilise du modèle MVC par défaut), donc vous allez ensuite créer de base de données d’appartenance de hello.

1. Dans SQL Server Management Studio, connectez-vous toohello SQL Server, vous venez d’installer. (Si hello **connecter tooServer** boîte de dialogue n’apparaît pas automatiquement, accédez trop**l’Explorateur d’objets** dans le volet gauche de hello, cliquez sur **connexion**, puis cliquez sur **Du moteur de base de données**.) ![Se connecter tooServer][SSMSConnectToServer]
   
    Dans la zone **Type de serveur**, choisissez **Moteur de base de données**. Pour **nom du serveur**, vous pouvez utiliser **localhost** hello nom ou de hello ordinateur que vous utilisez. Choisissez **l’authentification SQL Server**, puis ouvrez une session avec le nom d’utilisateur hello et le mot de passe hello que vous avez créé précédemment.
2. toocreate une base de données à l’aide de SQL Server Management Studio, cliquez sur **bases de données** dans l’Explorateur d’objets, puis cliquez sur **nouvelle base de données**.
   
    ![Create new database][SSMScreateNewDB]
3. Bonjour **nouvelle base de données** boîte de dialogue, entrez MembershipDB pour le nom de base de données hello, puis cliquez sur **OK**.
   
    ![Provide database name][SSMSprovideDBname]
   
    Notez que vous n’apportez pas de toute base de données de toohello de modifications à ce stade. les informations d’appartenance Hello seront ajoutées automatiquement ultérieurement par votre application web lors de son exécution.
4. Dans l’Explorateur d’objets, si vous développez **bases de données**, vous verrez cette base de données d’appartenance hello a été créé.
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a>B. Créer une application web Bonjour portail Azure
> [!NOTE]
> Si vous avez déjà créé une application web dans hello portail Azure que vous souhaitez toouse pour ce didacticiel, vous pouvez passer trop[créer une connexion hybride et un BizTalk Service](#CreateHC) et continuer à partir de là.
> 
> 

1. Bonjour [Azure Portal](https://portal.azure.com), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.
   
    ![Bouton Nouveau][New]
2. Configurez votre application web, puis cliquez sur **Créer**.
   
    ![Website name][WebsiteCreationBlade]
3. Après quelques instants, l’application hello web est créée et son panneau de l’application web s’affiche. Panneau de Hello est un tableau de bord permettant le défilement vertical qui vous permet de gérer votre application web.
   
    ![Website running][WebSiteRunningBlade]
   
    l’application web tooverify hello est dynamique, vous pouvez cliquer sur hello **Parcourir** page par défaut d’icône toodisplay hello.

Ensuite, vous allez créer une connexion hybride et un service BizTalk pour l’application web de hello.

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a>C. Création d’une connexion hybride et d’un service BizTalk
1. Précédent dans hello portail, accédez à toosettings et cliquez sur **réseau** > **configurer vos points de terminaison de connexion hybride**.
   
    ![Connexions hybrides][CreateHCHCIcon]
2. Dans le panneau de connexions hybrides hello, cliquez sur **ajouter** > **connexion hybride**.
3. Sur hello **créer la connexion hybride** panneau :
   
   * Pour **nom**, fournissez un nom pour la connexion de hello.
   * Pour **nom d’hôte**, entrez le nom de l’ordinateur hello de votre ordinateur hôte de SQL Server.
   * Pour **Port**, entrez 1433 (hello port par défaut pour SQL Server).
   * Cliquez sur **BizTalk Service** > **nouveau BizTalk Service** et entrez un nom pour hello service BizTalk.
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. Cliquez sur **OK** deux fois.
   
    Lorsque les processus hello est terminée, hello **Notifications** un vert clignote en zone **réussite** et hello **connexion hybride** panneau affichera hello connexion hybride avec Hello état en tant que **non connecté**.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

À ce stade, vous avez terminé une partie importante de l’infrastructure de connexion hello cloud hybride. Vous allez ensuite créer un élément local.

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>D. Installer la fonctionnalité connexion hello toocomplete hello local gestionnaire de connexions hybrides
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

Cette infrastructure de connexion hybride hello est terminée, vous allez créer une application web qui l’utilise.

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a>E. Créer un projet web de base ASP.NET, modifier la chaîne de connexion de base de données hello et exécuter le projet de hello localement
### <a name="create-a-basic-aspnet-project"></a>Création d'un projet ASP.NET de base
1. Dans Visual Studio, sur hello **fichier** menu, créez un nouveau projet :
   
    ![New Visual Studio project][HCVSNewProject]
2. Bonjour **modèles** section Hello **nouveau projet** boîte de dialogue, sélectionnez **Web** et choisissez **Application Web ASP.NET**, puis cliquez sur  **OK**.
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. Bonjour **nouveau projet ASP.NET** boîte de dialogue, choisissez **MVC**, puis cliquez sur **OK**.
   
    ![Choose MVC][HCVSChooseMVC]
4. Lorsque le projet de hello a été créé, la page du fichier Lisez-moi application hello s’affiche. N’exécutez pas encore projet web de hello.
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a>Modifier la chaîne de connexion de base de données hello pour une application hello
Dans cette étape, vous modifiez la chaîne de connexion hello qui indique à votre application où toofind de votre serveur local SQL Server Express base de données. chaîne de connexion Hello est dans le fichier Web.config de l’application hello, qui contient les informations de configuration de l’application hello.

> [!NOTE]
> tooensure que votre application utilise une base de données hello que vous avez créé dans SQL Server Express et non la hello une dans la valeur par défaut de Visual Studio base de données locale, il est important d’effectuer cette étape avant d’exécuter votre projet.
> 
> 

1. Dans l’Explorateur de solutions, double-cliquez sur le fichier Web.config de hello.
   
    ![Web.config][HCVSChooseWebConfig]
2. Modifier hello **connectionStrings** section toopoint toohello base de données SQL sur votre ordinateur local, la syntaxe hello Bonjour l’exemple suivant :
   
    ![Chaîne de connexion][HCVSConnectionString]
   
    Pour composer la chaîne hello, gardez suivante de hello l’esprit :
   
   * Si vous vous connectez tooa nommé instance au lieu d’une instance par défaut (par exemple, YourServer\SQLEXPRESS), vous devez configurer les ports statiques toouse de SQL Server. Pour plus d’informations sur la configuration des ports statiques, consultez [comment tooconfigure les toolisten de SQL Server sur un port spécifique](http://support.microsoft.com/kb/823938). Par défaut, les instances nommées utilisent UDP et des ports dynamiques, qui ne sont pas pris en charge par Connexions hybrides.
   * Il est recommandé de spécifier hello port (1433 par défaut, comme indiqué dans l’exemple de hello) de chaîne de connexion hello afin que vous pouvez être certain que votre serveur SQL Server local a TCP activé et qu’il utilise le port correct de hello.
   * N’oubliez pas de tooconnect de l’authentification SQL Server toouse, en spécifiant hello ID d’utilisateur et mot de passe dans votre chaîne de connexion.
3. Cliquez sur **enregistrer** dans le fichier Web.config de Visual Studio toosave hello.

### <a name="run-hello-project-locally-and-register-a-new-user"></a>Exécutez le projet de hello localement et inscrire un nouvel utilisateur
1. Maintenant, exécutez localement votre projet web en cliquant sur Parcourir hello sous le débogage. Cet exemple utilise Internet Explorer.
   
    ![Run project][HCVSRunProject]
2. Hello supérieur à droite de la page web de hello par défaut, choisissez **inscrire** tooregister un nouveau compte :
   
    ![Register a new account][HCVSRegisterLocally]
3. Entrez un nom d'utilisateur et un mot de passe :
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    Cela crée automatiquement une base de données sur votre serveur SQL local qui contient les informations d’appartenance hello pour votre application. Une des tables de hello (**dbo. AspNetUsers**) contient web application informations d’identification que celles que vous venez d’entrer hello. Vous verrez cette table plus loin dans le didacticiel de hello.
4. Fermez la fenêtre du navigateur hello de page web de hello par défaut. Cela arrête application hello dans Visual Studio.

Vous êtes maintenant prêt pour l’étape suivante de hello, qui est toopublish hello application tooAzure et le tester.

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a>F. Hello web application tooAzure de publier et de le tester
Maintenant, vous allez publier votre application web App Service de tooyour application et testez-le toosee comment vous avez configuré précédemment la connexion hybride hello est en cours tooconnect utilisé votre base de données web application toohello sur votre ordinateur local.

### <a name="publish-hello-web-application"></a>Publier l’application web de hello
1. Vous pouvez télécharger votre profil de publication pour hello application Service web d’application Bonjour portail Azure. Dans le panneau de hello pour votre application web, cliquez sur **obtenir le profil de publication**, puis enregistrez ordinateur tooyour de fichiers hello.
   
    ![Télécharger le profil de publication][PortalDownloadPublishProfile]
   
    Vous allez ensuite importer ce fichier dans votre application web Visual Studio.
2. Dans Visual Studio, cliquez sur le nom de projet hello dans l’Explorateur de solutions et sélectionnez **publier**.
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. Bonjour **publier le site Web** boîte de dialogue hello **profil** , onglet choisir **importation**.
   
    ![Importer][HCVSPublishWebDialogImport]
4. Parcourir tooyour téléchargé le profil de publication, sélectionnez-le, puis cliquez sur **OK**.
   
    ![Parcourir tooprofile][HCVSBrowseToImportPubProfile]
5. Vos informations de publication est importées et affiche sur hello **connexion** onglet de boîte de dialogue hello.
   
    ![Cliquer sur Publier][HCVSClickPublish]
   
    Cliquez sur **Publier**.
   
    Lorsque la publication est terminée, votre navigateur lancera et afficher votre application ASP.NET maintenant familiarisée--, sauf qu’il est maintenant en ligne Bonjour Azure cloud !

Ensuite, vous allez utiliser votre toosee d’application web dynamique sa connexion hybride en action.

### <a name="test-hello-completed-web-application-on-azure"></a>Hello du test terminé l’application web sur Azure
1. En haut de hello à droite de votre page web sur Azure, choisissez **connecter**.
   
    ![Test log in][HCTestLogIn]
2. Votre Service d’application web application est maintenant connecté de base de données d’appartenance de l’application tooyour web sur votre ordinateur local. tooverify, connectez-vous avec hello mêmes informations d’identification que vous avez entré dans hello local de base de données précédemment.
   
    ![Hello greeting][HCTestHelloContoso]
3. toofurther tester votre connexion hybride, déconnectez-vous de votre application web Azure et inscrire en tant qu’un autre utilisateur. Fournissez un nouveau nom d'utilisateur et un nouveau mot de passe, puis cliquez sur **Inscription**.
   
    ![Test register another user][HCTestRegisterRelecloud]
4. tooverify que les informations d’identification hello du nouvel utilisateur ont été stockées dans votre base de données locale via une connexion hybride, ouvrez SQL Management Studio sur votre ordinateur local. Dans l’Explorateur d’objets, développez hello **MembershipDB** de base de données, puis développez **Tables**. Avec le bouton hello **dbo. AspNetUsers** l’appartenance de table et choisissez **sélectionnez 1000 lignes du haut** des résultats tooview hello.
   
    ![Afficher les résultats de hello][HCTestSSMSTree]
5. Votre table des appartenances local affiche maintenant les deux comptes - hello créé localement et hello créé Bonjour cloud Azure. Hello une que vous avez créé dans le cloud de hello a été enregistré tooyour de la base de données locale via la fonctionnalité de connexion hybride d’Azure.
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

Vous avez maintenant créé et déployé une application web ASP.NET qui utilise une connexion hybride entre une application web Bonjour Azure cloud et une base de données SQL Server locale. Félicitations !

## <a name="see-also"></a>Voir aussi
[Aperçu des connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist présente les connexions hybrides (vidéo Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Aperçu des connexions hybrides](/services/biztalk-services/)

[BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Accéder aux ressources locales à l’aide de connexions hybrides dans Azure App Service](web-sites-hybrid-connection-get-started.md)

[Vue d’ensemble d’ASP.NET Identity](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
