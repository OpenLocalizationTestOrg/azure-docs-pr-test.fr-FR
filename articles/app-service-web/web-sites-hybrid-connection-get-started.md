---
title: "aaaAccess des ressources locales à l’aide de connexions hybrides dans Azure App Service"
description: "Créer une connexion entre une application web dans Azure App Service et une ressource locale utilisant un port TCP statique"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a>Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service
Vous pouvez connecter une ressource locale tooany application Azure App Service qui utilise un port TCP statique, telles que SQL Server, MySQL, API Web de HTTP et la plupart des Services Web personnalisés. Cet article vous montre comment toocreate une connexion hybride entre le Service d’applications et une base de données SQL Server locale.

> [!NOTE]
> partie des applications Web Hello de fonctionnalité de connexions hybrides hello est uniquement disponible dans hello [Azure Portal](https://portal.azure.com). toocreate une connexion dans les Services BizTalk, consultez [connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274). 
> 
> Ce contenu s’applique également à tooMobile des applications dans Azure App Service. 
> 
> 

## <a name="prerequisites"></a>Composants requis
* Un abonnement Azure. Pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
  
    Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
* toouse un local SQL Server ou la base de données SQL Server Express avec une connexion hybride, TCP/IP doit toobe activé sur un port statique. L’utilisation d’une instance par défaut sur SQL Server est recommandée, car elle utilise le port statique 1433. Pour plus d’informations sur l’installation et configuration de SQL Server Express pour une utilisation avec les connexions hybrides, consultez [tooan de se connecter localement SQL Server à partir d’un site web Azure à l’aide de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979).
* ordinateur Hello sur lequel vous installez l’agent Gestionnaire de connexions hybrides hello local décrite plus loin dans cet article :
  
  * Doit être en mesure de tooconnect tooAzure sur le port 5671
  * Doit être en mesure de tooreach hello *nom d’hôte*:*numéro_port* de votre ressource locale. 

> [!NOTE]
> Hello dans cet article suppose que vous utilisez le navigateur hello à partir de l’ordinateur hello qui hébergera l’agent de connexion hybride hello localement.
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Créer une application web Bonjour portail Azure
> [!NOTE]
> Si vous avez déjà créé une application web ou le principal de l’application Mobile Bonjour portail Azure que vous souhaitez toouse pour ce didacticiel, vous pouvez passer trop[créer une connexion hybride et un BizTalk Service](#CreateHC) et démarrer à partir de là.
> 
> 

1. Dans le coin supérieur gauche hello Hello [Azure Portal](https://portal.azure.com), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.
   
    ![New web app][NewWebsite]
2. Sur hello **application Web** panneau, fournir une URL et cliquez sur **créer**. 
   
    ![Website name][WebsiteCreationBlade]
3. Après quelques instants, l’application hello web est créée et son panneau de l’application web s’affiche. Panneau de Hello est un tableau de bord permettant le défilement vertical qui vous permet de gérer votre site.
   
    ![Website running][WebSiteRunningBlade]
4. tooverify hello site est en ligne, vous pouvez cliquer sur hello **Parcourir** page par défaut d’icône toodisplay hello.
   
    ![Cliquez sur Parcourir toosee votre application web][Browse]
   
    ![Default web app page][DefaultWebSitePage]

Ensuite, vous allez créer une connexion hybride et un service BizTalk pour l’application web de hello.

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a>Création d’une connexion hybride et d’un service BizTalk
1. Dans le panneau Application web, cliquez sur **Tous les paramètres** > **Mise en réseau** > **Configurer vos points de terminaison de connexion hybride**.
   
    ![Connexions hybrides][CreateHCHCIcon]
2. Dans le panneau de connexions hybrides hello, cliquez sur **ajouter**.
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. Hello **ajouter une connexion hybride** panneau s’ouvre.  Dans la mesure où il s’agit de votre première connexion hybride, hello **connexion hybride** option est présélectionnée et hello **créer la connexion hybride** panneau s’ouvre pour vous.
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    Sur hello **Panneau de connexion hybride créer**:
   
   * Pour **nom**, fournissez un nom pour la connexion de hello.
   * Pour **nom d’hôte**, entrez le nom hello de l’ordinateur local hello qui héberge votre ressource.
   * Pour **Port**, entrez le numéro de port hello que votre ressource locale utilise (1433 pour une instance par défaut de SQL Server).
   * Cliquez sur **Service BizTalk**
4. Hello **créer un BizTalk Service** panneau s’ouvre. Entrez un nom pour hello service BizTalk, puis cliquez sur **OK**.
   
    ![Créer un service BizTalk][CreateHCCreateBTS]
   
    Hello **créer un BizTalk Service** panneau se ferme et vous revenez toohello **créer la connexion hybride** panneau.
5. Dans le panneau de connexion hybride hello créer, cliquez sur **OK**. 
   
    ![Cliquez sur OK][CreateBTScomplete]
6. Lors de la fin du processus de hello, zone de notification hello Bonjour portail vous informe que les connexions hello a été créée avec succès.
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. Sur le panneau de l’application hello web, hello **connexions hybrides** icône indique maintenant que la connexion hybride 1 a été créée.
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

À ce stade, vous avez terminé une partie importante de l’infrastructure de connexion hello cloud hybride. Vous allez ensuite créer un élément local.

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a>Installer la fonctionnalité connexion hello toocomplete hello local gestionnaire de connexions hybrides
1. Dans le panneau de l’application hello web, cliquez sur **tous les paramètres** > **réseau** > **configurer vos points de terminaison de connexion hybride**. 
   
    ![Hybrid connections icon][HCIcon]
2. Sur hello **connexions hybrides** panneau, hello **état** colonne hello récemment ajouté montre de point de terminaison **non connecté**. Cliquez sur hello connexion tooconfigure il.
   
    ![Non connecté][NotConnected]
   
    Panneau de connexion hybride Hello s’ouvre.
   
    ![NotConnectedBlade][NotConnectedBlade]
3. Dans le panneau de hello, cliquez sur **écouteur le programme d’installation**.
   
    ![Click Listener Setup][ClickListenerSetup]
4. Hello **propriétés de connexion hybride** panneau s’ouvre. Sous **Gestionnaire de connexions hybrides local**, choisissez **cliquez ici tooinstall**.
   
    ![Cliquez ici tooinstall][ClickToInstallHCM]
5. Dans hello Application sécurité avertissement boîte de dialogue Exécuter, choisissez **exécuter** toocontinue.
   
    ![Choisissez d’exécuter toocontinue][ApplicationRunWarning]
6. Bonjour **contrôle de compte d’utilisateur** boîte de dialogue, choisissez **Oui**.
   
   ![Choose Yes][UAC]
7. Gestionnaire de connexions hybrides de Hello est téléchargé et installé pour vous. 
   
    ![Installation][HCMInstalling]
8. Fin de l’installation de hello, cliquez sur **fermer**.
   
    ![Click Close][HCMInstallComplete]
   
    Sur hello **connexions hybrides** panneau, hello **état** colonne affiche à présent **connecté**. 
   
    ![Connected Status][HCStatusConnected]

Cette infrastructure de connexion hybride hello est terminée, vous pouvez créer une application hybride qui l’utilise. 

> [!NOTE]
> Hello sections suivantes vous montrent comment toouse une connexion hybride avec un projet de service principal .NET des applications mobiles.
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a>Configurer hello Mobile application .NET principal projet tooconnect toohello base de données SQL
Dans App Service, un projet de backend d’applications mobiles .NET. est simplement une application web ASP.NET comportant un SDK d'applications Mobile supplémentaire installé et initialisé. toouse votre application web en tant qu’un serveur principal d’applications mobiles, vous devez [télécharger et initialiser hello Kit de développement logiciel de serveur principal .NET des applications mobiles](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).  

Pour les applications mobiles, vous devez toodefine une chaîne de connexion de base de données locale hello et modifiez hello principal toouse cette connexion. 

1. Dans l’Explorateur de solutions dans Visual Studio, le fichier Web.config de hello ouvert pour votre serveur principal Mobile application .NET, recherchez hello **connectionStrings** section, ajoutez une nouvelle entrée SqlClient hello suivants, les points de toohello SQL local Base de données du serveur :
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    N’oubliez pas de tooreplace `<**secure_password**>` dans cette chaîne avec le mot de passe hello créé pour *HybridConnectionLogin*.
2. Cliquez sur **enregistrer** dans le fichier Web.config de Visual Studio toosave hello.
   
   > [!NOTE]
   > Ce paramètre de connexion est utilisé lors de l’exécution sur l’ordinateur local de hello. Lors de l’exécution dans Azure, ce paramètre est remplacé par le paramètre de connexion hello défini dans le portail de hello.
   > 
   > 
3. Développez hello **modèles** dossier et le fichier de modèle de données ouvert hello, qui se termine par *Context.cs*.
4. Modifier hello **DbContext** toopass de constructeur d’instance hello valeur `OnPremisesDBConnection` toohello base **DbContext** constructeur, toohello similaire suivant extrait de code :
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    service de Hello utiliseront hello nouvelle connexion toohello base de données SQL.

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a>Jour toouse principal de hello application Mobile hello locale une chaîne de connexion
Ensuite, vous devez tooadd un paramètre d’application pour cette nouvelle chaîne de connexion afin qu’elle peut être utilisée à partir d’Azure.  

1. Dans hello [portail Azure](https://portal.azure.com) dans le code hello web application principale pour votre application Mobile, cliquez sur **tous les paramètres**, puis **paramètres de l’Application**.
2. Bonjour **paramètres d’application Web** panneau, faites défiler trop**les chaînes de connexion** et ajouter un nouveau **SQL Server** chaîne de connexion nommée `OnPremisesDBConnection` avec une valeur telle que `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.
   
    Remplacez `<**secure_password**>` avec le mot de passe sécurisé hello pour votre base de données locale.
   
    ![Chaîne de connexion pour la base de données locale](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. Appuyez sur **enregistrer** toosave la connexion hybride hello et la chaîne de connexion vous venez de créer.

À ce stade, vous pouvez republier le projet de serveur hello et tester une nouvelle connexion hello avec vos clients d’applications mobiles existants. Données seront être lues et écrites de base de données sur site toohello à l’aide de la connexion hybride hello.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la création d’une application web ASP.NET qui utilise une connexion hybride, consultez [tooan de se connecter localement SQL Server à partir d’un site web Azure à l’aide de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979). 

### <a name="additional-resources"></a>Ressources supplémentaires
[Aperçu des connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[Josh Twist présente les connexions hybrides (vidéo Channel 9)](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[Site web des connexions hybrides](https://azure.microsoft.com/services/biztalk-services/)

[BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[Se connecter tooan local SQL Server à partir d’Azure Mobile Services à l’aide de connexions de hybrides (vidéo Channel 9)](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
