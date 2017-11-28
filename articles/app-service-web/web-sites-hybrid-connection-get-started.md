---
title: "Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="bdfd7-103">Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="bdfd7-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="bdfd7-104">Vous pouvez connecter une application Azure App Service à n’importe quelle ressource locale utilisant un port TCP statique, par exemple, SQL Server, MySQL, les API web HTTP et la plupart des services web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="bdfd7-105">Cet article vous explique comment créer une connexion hybride entre une application App Service et une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="bdfd7-106">La partie Web Apps de la fonctionnalité Connexions hybrides n’est disponible que dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="bdfd7-107">Pour créer une connexion dans BizTalk Services, consultez la page [Connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="bdfd7-108">Ce contenu s'applique également aux applications mobiles dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bdfd7-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bdfd7-109">Prerequisites</span></span>
* <span data-ttu-id="bdfd7-110">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-110">An Azure subscription.</span></span> <span data-ttu-id="bdfd7-111">Pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="bdfd7-112">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="bdfd7-113">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="bdfd7-114">Pour utiliser une base de données SQL Server ou SQL Server Express locale avec une connexion hybride, TCP/IP doit être activé sur un port statique.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="bdfd7-115">L’utilisation d’une instance par défaut sur SQL Server est recommandée, car elle utilise le port statique 1433.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="bdfd7-116">Pour plus d’informations sur l’installation et la configuration de SQL Server Express en vue de son utilisation avec des connexions hybrides, consultez la page [Connexion à une instance SQL Server locale à partir d’un site Web Azure au moyen de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="bdfd7-117">L'ordinateur sur lequel vous installez l'agent Gestionnaire de connexions hybrides local décrit plus loin dans cet article :</span><span class="sxs-lookup"><span data-stu-id="bdfd7-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="bdfd7-118">doit être capable de se connecter à Azure sur le port 5671 ;</span><span class="sxs-lookup"><span data-stu-id="bdfd7-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="bdfd7-119">doit être capable d'accéder au *hostname*:*numéro_de_port* de votre ressource locale.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="bdfd7-120">Les étapes décrites dans cet article partent du principe que vous utilisez le navigateur à partir de l'ordinateur qui hébergera l'agent de connexion hybride local.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="bdfd7-121">Créer une application web dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="bdfd7-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="bdfd7-122">Si vous avez déjà créé dans le portail Azure une application web ou un backend d’application mobile que vous voulez utiliser pour ce didacticiel, passez directement à la section [Création d’une connexion hybride et d’un service BizTalk](#CreateHC) .</span><span class="sxs-lookup"><span data-stu-id="bdfd7-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="bdfd7-123">Dans le coin supérieur gauche du [portail Azure](https://portal.azure.com), cliquez sur **Nouveau**  > **Web + mobile** > **Application web**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![New web app][NewWebsite]
2. <span data-ttu-id="bdfd7-125">Dans le panneau **Application web**, indiquez une URL et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="bdfd7-127">Après quelques instants, l’application web est créée et son panneau apparaît.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="bdfd7-128">Le volet est un tableau de bord vertical qu'il est possible de faire défiler et qui vous permet de gérer votre site.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="bdfd7-130">Pour vérifier que le site est actif, cliquez sur l'icône **Parcourir** afin d'afficher la page par défaut.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Click browse to see your web app][Browse]
   
    ![Default web app page][DefaultWebSitePage]

<span data-ttu-id="bdfd7-133">Vous allez ensuite créer une connexion hybride et un service BizTalk pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="bdfd7-134">Création d’une connexion hybride et d’un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="bdfd7-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="bdfd7-135">Dans le panneau Application web, cliquez sur **Tous les paramètres** > **Mise en réseau** > **Configurer vos points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connexions hybrides][CreateHCHCIcon]
2. <span data-ttu-id="bdfd7-137">Dans le volet Connexions hybrides, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="bdfd7-138">Le volet **Ajouter une connexion hybride** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="bdfd7-139">Comme il s'agit de votre première connexion hybride, l'option **Nouvelle connexion hybride** est présélectionnée, et le volet **Créer une connexion hybride** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Create a hybrid connection][TwinCreateHCBlades]
   
    <span data-ttu-id="bdfd7-141">Dans le volet **Créer une connexion hybride**:</span><span class="sxs-lookup"><span data-stu-id="bdfd7-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="bdfd7-142">Sous **Nom**, entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="bdfd7-143">Sous **Nom d'hôte**, entrez le nom de l'ordinateur local qui héberge votre ressource.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="bdfd7-144">Sous **Port**, entrez le numéro du port utilisé par votre ressource locale (1433 pour une instance par défaut SQL Server).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="bdfd7-145">Cliquez sur **Service BizTalk**</span><span class="sxs-lookup"><span data-stu-id="bdfd7-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="bdfd7-146">Le panneau **Créer un service BizTalk** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="bdfd7-147">Entrez un nom pour le service BizTalk, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Créer un service BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="bdfd7-149">Le panneau **Créer un service BizTalk** se ferme et vous revenez au panneau **Créer une connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="bdfd7-150">Dans le volet Créer une connexion hybride, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Click OK][CreateBTScomplete]
6. <span data-ttu-id="bdfd7-152">Une fois le processus terminé, la zone des notifications du portail vous informe que la connexion a été créée.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="bdfd7-153">Dans le panneau de l’application web, l’icône **Connexions hybrides** indique à présent qu’une connexion hybride a été créée.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="bdfd7-155">À ce stade, vous avez terminé une partie importante de l'infrastructure de connexion hybride cloud.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="bdfd7-156">Vous allez ensuite créer un élément local.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="bdfd7-157">Installation du Gestionnaire de connexions hybrides local pour terminer la connexion</span><span class="sxs-lookup"><span data-stu-id="bdfd7-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="bdfd7-158">Dans le panneau Application web, cliquez sur **Tous les paramètres** > **Mise en réseau** > **Configurer vos points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="bdfd7-160">Dans le volet **Connexions hybrides**, la colonne **Statut** correspondant au point de terminaison ajouté récemment indique **Non connecté**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="bdfd7-161">Cliquez sur la connexion pour la configurer.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-161">Click the connection to configure it.</span></span>
   
    ![Non connecté][NotConnected]
   
    <span data-ttu-id="bdfd7-163">Le volet Connexion hybride s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="bdfd7-165">Dans le volet, cliquez sur **Configuration de l'écouteur**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="bdfd7-167">Le volet **Propriétés de la connexion hybride** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="bdfd7-168">Sous **Gestionnaire de connexions hybrides local**, cliquez sur **Cliquez ici pour l'installer**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Cliquez ici pour l'installer][ClickToInstallHCM]
5. <span data-ttu-id="bdfd7-170">Dans la boîte de dialogue Exécution de l'application - Avertissement de sécurité, cliquez sur **Exécuter** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Choose Run to continue][ApplicationRunWarning]
6. <span data-ttu-id="bdfd7-172">Dans la boîte de dialogue **Contrôle de compte d'utilisateur**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="bdfd7-174">Le Gestionnaire de connexion hybride est téléchargé et installé pour vous.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installation][HCMInstalling]
8. <span data-ttu-id="bdfd7-176">Une fois l'installation terminée, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-176">When the install completes, click **Close**.</span></span>
   
    ![Click Close][HCMInstallComplete]
   
    <span data-ttu-id="bdfd7-178">Dans le panneau **Connexions hybrides**, la colonne **Statut** indique à présent **Connecté**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status][HCStatusConnected]

<span data-ttu-id="bdfd7-180">Maintenant que l'infrastructure de connexion hybride est terminée, vous pouvez créer une application hybride qui l'utilise.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="bdfd7-181">Les sections suivantes vous montrent comment utiliser une connexion hybride avec un projet de backend d'applications mobiles .NET.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="bdfd7-182">Configuration du projet principal d'application mobile .NET pour la connexion à la base de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="bdfd7-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="bdfd7-183">Dans App Service, un projet de backend d’applications mobiles .NET. est simplement une application web ASP.NET comportant un SDK d'applications Mobile supplémentaire installé et initialisé.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="bdfd7-184">Pour utiliser votre application web comme backend d'applications mobiles, vous devez [télécharger et initialiser le SDK du backend d’applications mobiles .NET](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="bdfd7-185">Pour Mobile Apps, vous devez également définir une chaîne de connexion pour la base de données locale et modifier le serveur principal afin d'utiliser cette connexion.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="bdfd7-186">Dans l'Explorateur de solutions de Visual Studio, ouvrez le fichier Web.config pour votre backend d'application mobile .NET, recherchez la section **connectionStrings** , ajoutez une nouvelle entrée SqlClient comme suit, pointant vers la base de données SQL Server locale :</span><span class="sxs-lookup"><span data-stu-id="bdfd7-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="bdfd7-187">N’oubliez pas de remplacer `<**secure_password**>` dans cette chaîne par le mot de passe que vous avez créé pour *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="bdfd7-188">Cliquez sur **Enregistrer** dans Visual Studio pour enregistrer le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bdfd7-189">Ce paramètre de connexion est utilisé lors de l'exécution sur l'ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="bdfd7-190">Lors de l'exécution dans Azure, ce paramètre est remplacé par le paramètre de connexion défini dans le portail.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="bdfd7-191">Développez le dossier **Modèles** et ouvrez le fichier de modèle de données, se terminant par *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="bdfd7-192">Modifiez le constructeur d'instance **DbContext** pour transmettre la valeur `OnPremisesDBConnection` au constructeur **DbContext** de base, similaire à l'extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="bdfd7-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="bdfd7-193">Le service utilise désormais la nouvelle connexion à la base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="bdfd7-194">Mise à jour du backend d’application mobile pour utiliser la chaîne de connexion en local</span><span class="sxs-lookup"><span data-stu-id="bdfd7-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="bdfd7-195">À présent, vous devez ajouter un paramètre d'application pour cette nouvelle chaîne de connexion afin qu'elle puisse être utilisée à partir d'Azure.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="bdfd7-196">Dans le [portail Azure](https://portal.azure.com) dans le code principal d’application web de votre application mobile, cliquez sur **Tous les paramètres**, puis sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="bdfd7-197">Dans le panneau **Paramètres d'application web**, faites défiler jusqu'à **Chaînes de connexion** et ajoutez une chaîne de connexion **SQL Server** nommée `OnPremisesDBConnection` avec une valeur telle que `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="bdfd7-198">Remplacez `<**secure_password**>` par le mot de passe sécurisé de votre base de données locale.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Chaîne de connexion pour la base de données locale](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="bdfd7-200">Appuyez sur **Enregistrer** pour enregistrer la connexion hybride et la chaîne de connexion que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="bdfd7-201">À ce stade, vous pouvez republier le projet de serveur et tester la nouvelle connexion avec vos clients mobiles actuels.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="bdfd7-202">Les données seront lues et écrites dans la base de données locale à l'aide de la connexion hybride.</span><span class="sxs-lookup"><span data-stu-id="bdfd7-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="bdfd7-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bdfd7-203">Next Steps</span></span>
* <span data-ttu-id="bdfd7-204">Pour des informations sur la création d'une application web ASP.NET utilisant une connexion hybride, consultez la page [Connexion à une instance SQL Server locale à partir d'un site web Azure au moyen de connexions hybrides](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="bdfd7-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="bdfd7-205">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bdfd7-205">Additional Resources</span></span>
[<span data-ttu-id="bdfd7-206">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="bdfd7-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="bdfd7-207">Josh Twist présente les connexions hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="bdfd7-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="bdfd7-208">Site web des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="bdfd7-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="bdfd7-209">BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride</span><span class="sxs-lookup"><span data-stu-id="bdfd7-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="bdfd7-210">Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="bdfd7-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="bdfd7-211">Connexion à une instance SQL Server locale à partir d’Azure Mobile Services au moyen de connexions hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="bdfd7-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="bdfd7-212">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="bdfd7-212">What's changed</span></span>
* <span data-ttu-id="bdfd7-213">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="bdfd7-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
