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
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="5bf12-103">Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5bf12-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="5bf12-104">Vous pouvez connecter une ressource locale tooany application Azure App Service qui utilise un port TCP statique, telles que SQL Server, MySQL, API Web de HTTP et la plupart des Services Web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="5bf12-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="5bf12-105">Cet article vous montre comment toocreate une connexion hybride entre le Service d’applications et une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="5bf12-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="5bf12-106">partie des applications Web Hello de fonctionnalité de connexions hybrides hello est uniquement disponible dans hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5bf12-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="5bf12-107">toocreate une connexion dans les Services BizTalk, consultez [connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="5bf12-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="5bf12-108">Ce contenu s’applique également à tooMobile des applications dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5bf12-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5bf12-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5bf12-109">Prerequisites</span></span>
* <span data-ttu-id="5bf12-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf12-110">An Azure subscription.</span></span> <span data-ttu-id="5bf12-111">Pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bf12-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="5bf12-112">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="5bf12-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5bf12-113">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="5bf12-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="5bf12-114">toouse un local SQL Server ou la base de données SQL Server Express avec une connexion hybride, TCP/IP doit toobe activé sur un port statique.</span><span class="sxs-lookup"><span data-stu-id="5bf12-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="5bf12-115">L’utilisation d’une instance par défaut sur SQL Server est recommandée, car elle utilise le port statique 1433.</span><span class="sxs-lookup"><span data-stu-id="5bf12-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="5bf12-116">Pour plus d’informations sur l’installation et configuration de SQL Server Express pour une utilisation avec les connexions hybrides, consultez [tooan de se connecter localement SQL Server à partir d’un site web Azure à l’aide de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="5bf12-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="5bf12-117">ordinateur Hello sur lequel vous installez l’agent Gestionnaire de connexions hybrides hello local décrite plus loin dans cet article :</span><span class="sxs-lookup"><span data-stu-id="5bf12-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="5bf12-118">Doit être en mesure de tooconnect tooAzure sur le port 5671</span><span class="sxs-lookup"><span data-stu-id="5bf12-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="5bf12-119">Doit être en mesure de tooreach hello *nom d’hôte*:*numéro_port* de votre ressource locale.</span><span class="sxs-lookup"><span data-stu-id="5bf12-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="5bf12-120">Hello dans cet article suppose que vous utilisez le navigateur hello à partir de l’ordinateur hello qui hébergera l’agent de connexion hybride hello localement.</span><span class="sxs-lookup"><span data-stu-id="5bf12-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="5bf12-121">Créer une application web Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="5bf12-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="5bf12-122">Si vous avez déjà créé une application web ou le principal de l’application Mobile Bonjour portail Azure que vous souhaitez toouse pour ce didacticiel, vous pouvez passer trop[créer une connexion hybride et un BizTalk Service](#CreateHC) et démarrer à partir de là.</span><span class="sxs-lookup"><span data-stu-id="5bf12-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="5bf12-123">Dans le coin supérieur gauche hello Hello [Azure Portal](https://portal.azure.com), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![New web app][NewWebsite]
2. <span data-ttu-id="5bf12-125">Sur hello **application Web** panneau, fournir une URL et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="5bf12-127">Après quelques instants, l’application hello web est créée et son panneau de l’application web s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5bf12-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="5bf12-128">Panneau de Hello est un tableau de bord permettant le défilement vertical qui vous permet de gérer votre site.</span><span class="sxs-lookup"><span data-stu-id="5bf12-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="5bf12-130">tooverify hello site est en ligne, vous pouvez cliquer sur hello **Parcourir** page par défaut d’icône toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Cliquez sur Parcourir toosee votre application web][Browse]
   
    ![Default web app page][DefaultWebSitePage]

<span data-ttu-id="5bf12-133">Ensuite, vous allez créer une connexion hybride et un service BizTalk pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="5bf12-134">Création d’une connexion hybride et d’un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="5bf12-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="5bf12-135">Dans le panneau Application web, cliquez sur **Tous les paramètres** > **Mise en réseau** > **Configurer vos points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connexions hybrides][CreateHCHCIcon]
2. <span data-ttu-id="5bf12-137">Dans le panneau de connexions hybrides hello, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="5bf12-138">Hello **ajouter une connexion hybride** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5bf12-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="5bf12-139">Dans la mesure où il s’agit de votre première connexion hybride, hello **connexion hybride** option est présélectionnée et hello **créer la connexion hybride** panneau s’ouvre pour vous.</span><span class="sxs-lookup"><span data-stu-id="5bf12-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="5bf12-141">Sur hello **Panneau de connexion hybride créer**:</span><span class="sxs-lookup"><span data-stu-id="5bf12-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="5bf12-142">Pour **nom**, fournissez un nom pour la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="5bf12-143">Pour **nom d’hôte**, entrez le nom hello de l’ordinateur local hello qui héberge votre ressource.</span><span class="sxs-lookup"><span data-stu-id="5bf12-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="5bf12-144">Pour **Port**, entrez le numéro de port hello que votre ressource locale utilise (1433 pour une instance par défaut de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="5bf12-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="5bf12-145">Cliquez sur **Service BizTalk**</span><span class="sxs-lookup"><span data-stu-id="5bf12-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="5bf12-146">Hello **créer un BizTalk Service** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5bf12-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="5bf12-147">Entrez un nom pour hello service BizTalk, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Créer un service BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="5bf12-149">Hello **créer un BizTalk Service** panneau se ferme et vous revenez toohello **créer la connexion hybride** panneau.</span><span class="sxs-lookup"><span data-stu-id="5bf12-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="5bf12-150">Dans le panneau de connexion hybride hello créer, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Cliquez sur OK][CreateBTScomplete]
6. <span data-ttu-id="5bf12-152">Lors de la fin du processus de hello, zone de notification hello Bonjour portail vous informe que les connexions hello a été créée avec succès.</span><span class="sxs-lookup"><span data-stu-id="5bf12-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
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
7. <span data-ttu-id="5bf12-153">Sur le panneau de l’application hello web, hello **connexions hybrides** icône indique maintenant que la connexion hybride 1 a été créée.</span><span class="sxs-lookup"><span data-stu-id="5bf12-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="5bf12-155">À ce stade, vous avez terminé une partie importante de l’infrastructure de connexion hello cloud hybride.</span><span class="sxs-lookup"><span data-stu-id="5bf12-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="5bf12-156">Vous allez ensuite créer un élément local.</span><span class="sxs-lookup"><span data-stu-id="5bf12-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="5bf12-157">Installer la fonctionnalité connexion hello toocomplete hello local gestionnaire de connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="5bf12-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="5bf12-158">Dans le panneau de l’application hello web, cliquez sur **tous les paramètres** > **réseau** > **configurer vos points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="5bf12-160">Sur hello **connexions hybrides** panneau, hello **état** colonne hello récemment ajouté montre de point de terminaison **non connecté**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="5bf12-161">Cliquez sur hello connexion tooconfigure il.</span><span class="sxs-lookup"><span data-stu-id="5bf12-161">Click hello connection tooconfigure it.</span></span>
   
    ![Non connecté][NotConnected]
   
    <span data-ttu-id="5bf12-163">Panneau de connexion hybride Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5bf12-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="5bf12-165">Dans le panneau de hello, cliquez sur **écouteur le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="5bf12-167">Hello **propriétés de connexion hybride** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5bf12-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="5bf12-168">Sous **Gestionnaire de connexions hybrides local**, choisissez **cliquez ici tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Cliquez ici tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="5bf12-170">Dans hello Application sécurité avertissement boîte de dialogue Exécuter, choisissez **exécuter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5bf12-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Choisissez d’exécuter toocontinue][ApplicationRunWarning]
6. <span data-ttu-id="5bf12-172">Bonjour **contrôle de compte d’utilisateur** boîte de dialogue, choisissez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="5bf12-174">Gestionnaire de connexions hybrides de Hello est téléchargé et installé pour vous.</span><span class="sxs-lookup"><span data-stu-id="5bf12-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installation][HCMInstalling]
8. <span data-ttu-id="5bf12-176">Fin de l’installation de hello, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-176">When hello install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="5bf12-178">Sur hello **connexions hybrides** panneau, hello **état** colonne affiche à présent **connecté**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="5bf12-180">Cette infrastructure de connexion hybride hello est terminée, vous pouvez créer une application hybride qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="5bf12-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="5bf12-181">Hello sections suivantes vous montrent comment toouse une connexion hybride avec un projet de service principal .NET des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="5bf12-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="5bf12-182">Configurer hello Mobile application .NET principal projet tooconnect toohello base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5bf12-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="5bf12-183">Dans App Service, un projet de backend d’applications mobiles .NET. est simplement une application web ASP.NET comportant un SDK d'applications Mobile supplémentaire installé et initialisé.</span><span class="sxs-lookup"><span data-stu-id="5bf12-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="5bf12-184">toouse votre application web en tant qu’un serveur principal d’applications mobiles, vous devez [télécharger et initialiser hello Kit de développement logiciel de serveur principal .NET des applications mobiles](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="5bf12-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="5bf12-185">Pour les applications mobiles, vous devez toodefine une chaîne de connexion de base de données locale hello et modifiez hello principal toouse cette connexion.</span><span class="sxs-lookup"><span data-stu-id="5bf12-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="5bf12-186">Dans l’Explorateur de solutions dans Visual Studio, le fichier Web.config de hello ouvert pour votre serveur principal Mobile application .NET, recherchez hello **connectionStrings** section, ajoutez une nouvelle entrée SqlClient hello suivants, les points de toohello SQL local Base de données du serveur :</span><span class="sxs-lookup"><span data-stu-id="5bf12-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="5bf12-187">N’oubliez pas de tooreplace `<**secure_password**>` dans cette chaîne avec le mot de passe hello créé pour *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="5bf12-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="5bf12-188">Cliquez sur **enregistrer** dans le fichier Web.config de Visual Studio toosave hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5bf12-189">Ce paramètre de connexion est utilisé lors de l’exécution sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="5bf12-190">Lors de l’exécution dans Azure, ce paramètre est remplacé par le paramètre de connexion hello défini dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="5bf12-191">Développez hello **modèles** dossier et le fichier de modèle de données ouvert hello, qui se termine par *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="5bf12-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="5bf12-192">Modifier hello **DbContext** toopass de constructeur d’instance hello valeur `OnPremisesDBConnection` toohello base **DbContext** constructeur, toohello similaire suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="5bf12-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="5bf12-193">service de Hello utiliseront hello nouvelle connexion toohello base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5bf12-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="5bf12-194">Jour toouse principal de hello application Mobile hello locale une chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="5bf12-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="5bf12-195">Ensuite, vous devez tooadd un paramètre d’application pour cette nouvelle chaîne de connexion afin qu’elle peut être utilisée à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5bf12-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="5bf12-196">Dans hello [portail Azure](https://portal.azure.com) dans le code hello web application principale pour votre application Mobile, cliquez sur **tous les paramètres**, puis **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="5bf12-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="5bf12-197">Bonjour **paramètres d’application Web** panneau, faites défiler trop**les chaînes de connexion** et ajouter un nouveau **SQL Server** chaîne de connexion nommée `OnPremisesDBConnection` avec une valeur telle que `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="5bf12-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="5bf12-198">Remplacez `<**secure_password**>` avec le mot de passe sécurisé hello pour votre base de données locale.</span><span class="sxs-lookup"><span data-stu-id="5bf12-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Chaîne de connexion pour la base de données locale](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="5bf12-200">Appuyez sur **enregistrer** toosave la connexion hybride hello et la chaîne de connexion vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="5bf12-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="5bf12-201">À ce stade, vous pouvez republier le projet de serveur hello et tester une nouvelle connexion hello avec vos clients d’applications mobiles existants.</span><span class="sxs-lookup"><span data-stu-id="5bf12-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="5bf12-202">Données seront être lues et écrites de base de données sur site toohello à l’aide de la connexion hybride hello.</span><span class="sxs-lookup"><span data-stu-id="5bf12-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="5bf12-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5bf12-203">Next Steps</span></span>
* <span data-ttu-id="5bf12-204">Pour plus d’informations sur la création d’une application web ASP.NET qui utilise une connexion hybride, consultez [tooan de se connecter localement SQL Server à partir d’un site web Azure à l’aide de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="5bf12-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="5bf12-205">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5bf12-205">Additional Resources</span></span>
[<span data-ttu-id="5bf12-206">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="5bf12-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="5bf12-207">Josh Twist présente les connexions hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5bf12-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="5bf12-208">Site web des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="5bf12-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="5bf12-209">BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride</span><span class="sxs-lookup"><span data-stu-id="5bf12-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="5bf12-210">Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5bf12-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="5bf12-211">Se connecter tooan local SQL Server à partir d’Azure Mobile Services à l’aide de connexions de hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="5bf12-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="5bf12-212">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="5bf12-212">What's changed</span></span>
* <span data-ttu-id="5bf12-213">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5bf12-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
