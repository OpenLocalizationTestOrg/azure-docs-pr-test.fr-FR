---
title: "Connexion à un serveur SQL Server local à partir d’une application web dans Azure App Service au moyen de connexions hybrides"
description: "Créer une application web sur Microsoft Azure et la connecter à une base de données SQL Server locale"
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
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="ca669-103">Connexion à un serveur SQL Server local à partir d’une application web dans Azure App Service au moyen de connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="ca669-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="ca669-104">Les connexions hybrides permettent de connecter des applications web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) à des ressources locales qui utilisent un port TCP statique.</span><span class="sxs-lookup"><span data-stu-id="ca669-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="ca669-105">Les ressources prises en charge incluent Microsoft SQL Server, MySQL, les API web HTTP, App Service et la plupart des services web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ca669-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="ca669-106">Dans ce didacticiel, vous allez apprendre à créer une application web App Service dans le [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715), à la connecter à votre base de données SQL Server locale à l’aide de la nouvelle fonctionnalité de connexion hybride, à créer une application ASP.NET simple qui utilisera la connexion hybride et à déployer l’application sur l’application web App Service.</span><span class="sxs-lookup"><span data-stu-id="ca669-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="ca669-107">L’application web finalisée sur Azure stocke les informations d’identification des membres dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="ca669-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="ca669-108">Ce didacticiel ne requiert aucune d'expérience préalable dans l'utilisation d'Azure ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ca669-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="ca669-109">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="ca669-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ca669-110">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="ca669-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="ca669-111">La partie Web Apps de la fonctionnalité Connexions hybrides n’est disponible que dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca669-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="ca669-112">Pour créer une connexion dans BizTalk Services, consultez la page [Connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="ca669-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ca669-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="ca669-113">Prerequisites</span></span>
<span data-ttu-id="ca669-114">Pour réaliser ce didacticiel, vous avez besoin des produits suivants.</span><span class="sxs-lookup"><span data-stu-id="ca669-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="ca669-115">Tous sont disponibles gratuitement, de sorte que vous pouvez commencer à développer gratuitement pour Azure.</span><span class="sxs-lookup"><span data-stu-id="ca669-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="ca669-116">**Abonnement Azure** : pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ca669-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="ca669-117">**Visual Studio 2013** - Pour télécharger une version d'évaluation gratuite de Visual Studio 2013, consultez la page [Téléchargements Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="ca669-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="ca669-118">Installez ceci avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="ca669-118">Install this before continuing.</span></span>
* <span data-ttu-id="ca669-119">**Microsoft .NET Framework 3.5 Service Pack 1** : si votre système d'exploitation est Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 ou Windows Server 2008 R2, vous pouvez activer cette mise à jour dans Panneau de configuration > Programmes et fonctionnalités > Activer ou désactiver des fonctionnalités Windows.</span><span class="sxs-lookup"><span data-stu-id="ca669-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="ca669-120">Sinon, vous pouvez la télécharger depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="ca669-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="ca669-121">**SQL Server 2014 Express with Tools** - Téléchargez gratuitement Microsoft SQL Server Express sur la [page des bases de données Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca669-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="ca669-122">Choisissez la version **Express** (pas LocalDB).</span><span class="sxs-lookup"><span data-stu-id="ca669-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="ca669-123">La version **Express with Tools** inclut SQL Server Management Studio, que vous utiliserez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ca669-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="ca669-124">**SQL Server Management Studio Express** : cet outil est inclus dans le téléchargement de SQL Server 2014 Express with Tools mentionné plus haut, mais si vous avez besoin de l'installer séparément, vous pouvez le télécharger et l'installer à partir de la [page de téléchargement de SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca669-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="ca669-125">Ce didacticiel part du principe que vous possédez un abonnement Azure, que vous avez installé Visual Studio 2013 et que vous avez installé ou activé .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="ca669-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="ca669-126">Il explique comment installer SQL Server 2014 Express dans une configuration adaptée à la fonctionnalité Connexions hybrides d'Azure (une instance par défaut avec un port IP statique).</span><span class="sxs-lookup"><span data-stu-id="ca669-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="ca669-127">Avant de commencer ce didacticiel, téléchargez SQL Server 2014 Express with Tools depuis l'emplacement mentionné ci-dessus si vous n'avez pas installé SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ca669-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="ca669-128">Remarques</span><span class="sxs-lookup"><span data-stu-id="ca669-128">Notes</span></span>
<span data-ttu-id="ca669-129">Pour utiliser une base de données SQL Server ou SQL Server Express locale avec une connexion hybride, TCP/IP doit être activé sur un port statique.</span><span class="sxs-lookup"><span data-stu-id="ca669-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="ca669-130">Les instances par défaut dans SQL Server utilisent le port statique 1433, mais pas les instances nommées.</span><span class="sxs-lookup"><span data-stu-id="ca669-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="ca669-131">L'ordinateur sur lequel vous installez l'agent Gestionnaire de connexion hybride local :</span><span class="sxs-lookup"><span data-stu-id="ca669-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="ca669-132">doit disposer d'une connectivité à Azure via :</span><span class="sxs-lookup"><span data-stu-id="ca669-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="ca669-133">Port</span><span class="sxs-lookup"><span data-stu-id="ca669-133">Port</span></span> | <span data-ttu-id="ca669-134">Pourquoi</span><span class="sxs-lookup"><span data-stu-id="ca669-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="ca669-135">80</span><span class="sxs-lookup"><span data-stu-id="ca669-135">80</span></span> |<span data-ttu-id="ca669-136">**Obligatoire** pour le port HTTP pour la validation du certificat et éventuellement la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="ca669-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="ca669-137">443</span><span class="sxs-lookup"><span data-stu-id="ca669-137">443</span></span> |<span data-ttu-id="ca669-138">**Facultatif** pour la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="ca669-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="ca669-139">Si la connectivité sortante à 443 n'est pas disponible, le port TCP 80 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ca669-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="ca669-140">5671 et 9352</span><span class="sxs-lookup"><span data-stu-id="ca669-140">5671 and 9352</span></span> |<span data-ttu-id="ca669-141">**Recommandé** mais facultatif pour la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="ca669-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="ca669-142">Notez que ce mode entraîne habituellement un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="ca669-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="ca669-143">Si la connectivité sortante à ces ports n'est pas disponible, le port TCP 443 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ca669-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="ca669-144">doit être capable d'accéder au *hostname*:*numéro_de_port* de votre ressource locale.</span><span class="sxs-lookup"><span data-stu-id="ca669-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="ca669-145">Les étapes décrites dans cet article partent du principe que vous utilisez le navigateur à partir de l'ordinateur qui hébergera l'agent de connexion hybride local.</span><span class="sxs-lookup"><span data-stu-id="ca669-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="ca669-146">Si vous avez déjà installé SQL Server dans une configuration et dans un environnement qui répondent aux conditions décrites ci-dessus, vous pouvez passer directement à [Création d'une base de données SQL Server en local](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="ca669-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="ca669-147">A.</span><span class="sxs-lookup"><span data-stu-id="ca669-147">A.</span></span> <span data-ttu-id="ca669-148">Installation de SQL Server Express, activation de TCP/IP et création d'une base de données SQL Server en local</span><span class="sxs-lookup"><span data-stu-id="ca669-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="ca669-149">Cette section explique comment installer SQL Server Express, activer TCP/IP et créer une base de données de telle sorte que votre application web fonctionne avec l'environnement du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca669-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="ca669-150">Installation de SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="ca669-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="ca669-151">Pour installer SQL Server Express, exécutez le fichier **SQLEXPRWT_x64_ENU.exe** ou **SQLEXPR_x86_ENU.exe** que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="ca669-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="ca669-152">Le Centre d'installation SQL Server s'affiche.</span><span class="sxs-lookup"><span data-stu-id="ca669-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="ca669-154">Choisissez **Nouvelle installation autonome SQL Server ou ajout de fonctionnalités à une installation existante**.</span><span class="sxs-lookup"><span data-stu-id="ca669-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="ca669-155">Suivez les instructions, en acceptant les options et les paramètres par défaut, jusqu'à l'affichage de la page **Configuration de l'instance** .</span><span class="sxs-lookup"><span data-stu-id="ca669-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="ca669-156">Sur la page **Configuration de l'instance**, choisissez **Instance par défaut**.</span><span class="sxs-lookup"><span data-stu-id="ca669-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="ca669-158">Par défaut, l'instance par défaut de SQL Server écoute les demandes des clients SQL Server sur le port statique 1433. C'est une exigence de la fonctionnalité Connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="ca669-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="ca669-159">Les instances nommées utilisent des ports dynamiques et UDP, qui ne sont pas pris en charge par Connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="ca669-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="ca669-160">Acceptez les valeurs par défaut sur la page **Configuration du serveur** .</span><span class="sxs-lookup"><span data-stu-id="ca669-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="ca669-161">Sur la page **Configuration du moteur de base de données**, sous **Mode d'authentification**, choisissez **Mode mixte (authentification SQL Server et authentification Windows)** et fournissez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ca669-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="ca669-163">Dans ce didacticiel, vous allez utiliser l'authentification SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ca669-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="ca669-164">N'oubliez pas votre mot de passe, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ca669-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="ca669-165">Parcourez les autres étapes de l'Assistant pour terminer l'installation.</span><span class="sxs-lookup"><span data-stu-id="ca669-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="ca669-166">Activation de TCP/IP</span><span class="sxs-lookup"><span data-stu-id="ca669-166">Enable TCP/IP</span></span>
<span data-ttu-id="ca669-167">Pour activer TCP/IP, vous allez utiliser le Gestionnaire de configuration SQL Server, qui a été installé en même temps que SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="ca669-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="ca669-168">Suivez la procédure décrite à la page [Activation du protocole réseau TCP/IP pour SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ca669-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="ca669-169">Création d'une base de données SQL Server en local</span><span class="sxs-lookup"><span data-stu-id="ca669-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="ca669-170">Votre application Visual Studio nécessite une base de données d'appartenance à laquelle Azure puisse accéder.</span><span class="sxs-lookup"><span data-stu-id="ca669-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="ca669-171">Il doit s'agir d'une base de données SQL Server ou SQL Server Express (et non de la base de données LocalDB utilisée par défaut par le modèle MVC). Vous allez donc créer ensuite la base de données d'appartenance.</span><span class="sxs-lookup"><span data-stu-id="ca669-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="ca669-172">Dans SQL Server Management Studio, connectez-vous à l'instance SQL Server que vous venez d'installer.</span><span class="sxs-lookup"><span data-stu-id="ca669-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="ca669-173">(Si la boîte de dialogue **Se connecter au serveur** ne s’affiche pas automatiquement, accédez à **l’Explorateur d’objets** dans le volet gauche, cliquez sur **Se connecter**, puis sur **Moteur de base de données**.)  ![Se connecter au serveur][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="ca669-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="ca669-174">Dans la zone **Type de serveur**, choisissez **Moteur de base de données**.</span><span class="sxs-lookup"><span data-stu-id="ca669-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="ca669-175">Dans la zone **Nom du serveur**, vous pouvez utiliser **localhost** ou le nom de l'ordinateur dont vous servez.</span><span class="sxs-lookup"><span data-stu-id="ca669-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="ca669-176">Choisissez **Authentification SQL Server**, puis ouvrez une session avec le nom d'utilisateur sa et le mot de passe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ca669-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="ca669-177">Pour créer une base de données avec SQL Server Management Studio, cliquez avec le bouton droit sur **Bases de données** dans l'Explorateur d'objets, puis cliquez sur **Nouvelle base de données**.</span><span class="sxs-lookup"><span data-stu-id="ca669-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="ca669-179">Dans la boîte de dialogue **Nouvelle base de données**, entrez MembershipDB comme nom de base de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca669-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="ca669-181">Notez qu'à ce stade, vous n'apportez aucune modification à la base de données.</span><span class="sxs-lookup"><span data-stu-id="ca669-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="ca669-182">Les informations d'appartenance seront ajoutées automatiquement plus tard par votre application web, lorsque vous l'exécuterez.</span><span class="sxs-lookup"><span data-stu-id="ca669-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="ca669-183">Dans l'Explorateur d'objets, si vous développez **Bases de données**, vous pouvez constater que la base de données d'appartenance a été créée.</span><span class="sxs-lookup"><span data-stu-id="ca669-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="ca669-185">B.</span><span class="sxs-lookup"><span data-stu-id="ca669-185">B.</span></span> <span data-ttu-id="ca669-186">Créer une application web dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ca669-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="ca669-187">Si vous avez déjà créé dans le portail Azure une application Web que vous voulez utiliser pour ce didacticiel, passez directement à la section [Création d’une connexion hybride et d’un service BizTalk](#CreateHC) .</span><span class="sxs-lookup"><span data-stu-id="ca669-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="ca669-188">Dans le [Portail Azure](https://portal.azure.com), cliquez sur **Nouveau** > **Web + mobile** > **Application web**.</span><span class="sxs-lookup"><span data-stu-id="ca669-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Bouton Nouveau][New]
2. <span data-ttu-id="ca669-190">Configurez votre application web, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ca669-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="ca669-192">Après quelques instants, l’application web est créée et son panneau apparaît.</span><span class="sxs-lookup"><span data-stu-id="ca669-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="ca669-193">Le panneau est un tableau de bord à défilement vertical, qui vous permet de gérer votre application web.</span><span class="sxs-lookup"><span data-stu-id="ca669-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="ca669-195">Pour vérifier que l’application est active, cliquez sur l’icône **Parcourir** afin d’afficher la page par défaut.</span><span class="sxs-lookup"><span data-stu-id="ca669-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="ca669-196">Vous allez ensuite créer une connexion hybride et un service BizTalk pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="ca669-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="ca669-197">C.</span><span class="sxs-lookup"><span data-stu-id="ca669-197">C.</span></span> <span data-ttu-id="ca669-198">Création d’une connexion hybride et d’un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="ca669-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="ca669-199">De retour dans le portail, accédez aux paramètres et cliquez sur **Mise en réseau** > **Configurer les points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="ca669-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connexions hybrides][CreateHCHCIcon]
2. <span data-ttu-id="ca669-201">Dans le panneau Connexions hybrides, cliquez sur **Ajouter** > **Nouvelle connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="ca669-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="ca669-202">Dans le panneau **Créer une connexion hybride** :</span><span class="sxs-lookup"><span data-stu-id="ca669-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="ca669-203">Sous **Nom**, entrez un nom pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="ca669-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="ca669-204">Sous **Nom d'hôte**, entrez le nom de votre ordinateur hôte SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ca669-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="ca669-205">Sous **Port**, entrez 1433 (le port par défaut pour SQL Server).</span><span class="sxs-lookup"><span data-stu-id="ca669-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="ca669-206">Cliquez sur **Service BizTalk** > **Nouveau service BizTalk** et entrez un nom pour le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ca669-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="ca669-208">Cliquez sur **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="ca669-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="ca669-209">Lorsque le processus est terminé, la zone **Notifications** affiche la mention **SUCCÈS** en vert clignotant et le panneau **Connexion hybride** affiche la nouvelle connexion hybride dans l’état **Non connecté**.</span><span class="sxs-lookup"><span data-stu-id="ca669-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="ca669-211">À ce stade, vous avez terminé une partie importante de l'infrastructure de connexion hybride cloud.</span><span class="sxs-lookup"><span data-stu-id="ca669-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="ca669-212">Vous allez ensuite créer un élément local.</span><span class="sxs-lookup"><span data-stu-id="ca669-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="ca669-213">D.</span><span class="sxs-lookup"><span data-stu-id="ca669-213">D.</span></span> <span data-ttu-id="ca669-214">Installation du Gestionnaire de connexions hybrides local pour terminer la connexion</span><span class="sxs-lookup"><span data-stu-id="ca669-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="ca669-215">Maintenant que l’infrastructure de connexion hybride est terminée, vous pouvez créer une application web qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="ca669-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="ca669-216">E.</span><span class="sxs-lookup"><span data-stu-id="ca669-216">E.</span></span> <span data-ttu-id="ca669-217">Création d’un projet web ASP.NET de base, modification de la chaîne de connexion à la base de données et exécution locale du projet</span><span class="sxs-lookup"><span data-stu-id="ca669-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="ca669-218">Création d'un projet ASP.NET de base</span><span class="sxs-lookup"><span data-stu-id="ca669-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="ca669-219">À partir du menu **Fichier** de Visual Studio, créez un nouveau projet :</span><span class="sxs-lookup"><span data-stu-id="ca669-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="ca669-221">Dans la section **Modèles** de la boîte de dialogue **Nouveau projet**, sélectionnez **Web** et choisissez **Application Web ASP.NET**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca669-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="ca669-223">Dans la boîte de dialogue **Nouveau projet ASP.NET**, choisissez **MVC**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca669-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="ca669-225">Lorsque le projet a été créé, la page lisezmoi (readme) de l'application s'affiche.</span><span class="sxs-lookup"><span data-stu-id="ca669-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="ca669-226">N'exécutez pas le projet web immédiatement.</span><span class="sxs-lookup"><span data-stu-id="ca669-226">Do not run the web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="ca669-228">Modification de la chaîne de connexion à la base de données pour l'application</span><span class="sxs-lookup"><span data-stu-id="ca669-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="ca669-229">Au cours de cette étape, vous allez modifier la chaîne de connexion qui indique à votre application où se trouve votre base de données SQL Server Express locale.</span><span class="sxs-lookup"><span data-stu-id="ca669-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="ca669-230">La chaîne de connexion se trouve dans le fichier Web.config de l'application, qui contient les informations de configuration pour l'application.</span><span class="sxs-lookup"><span data-stu-id="ca669-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ca669-231">Pour vous assurer que votre application utilise la base de données que vous avez créée dans SQL Server Express, et non la base de données LocalDB par défaut de Visual Studio, il est important d'effectuer cette opération avant d'exécuter votre projet.</span><span class="sxs-lookup"><span data-stu-id="ca669-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="ca669-232">Dans l'Explorateur de solutions, double-cliquez sur le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="ca669-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="ca669-234">Modifiez la section **connectionStrings** pour pointer vers la base de données SQL Server sur votre ordinateur local, en utilisant la syntaxe de l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ca669-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Chaîne de connexion][HCVSConnectionString]
   
    <span data-ttu-id="ca669-236">Lors de la composition de la chaîne de connexion, gardez à l'esprit ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ca669-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="ca669-237">Si vous vous connectez à une instance nommée plutôt qu'à une instance par défaut (par exemple, VotreServeur\SQLEXPRESS), vous devez configurer votre instance SQL Server de manière à ce qu'elle utilise des ports statiques.</span><span class="sxs-lookup"><span data-stu-id="ca669-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="ca669-238">Pour des informations sur la configuration des ports statiques, consultez la page [Configuration de SQL Server pour qu'il écoute sur un port spécifique](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="ca669-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="ca669-239">Par défaut, les instances nommées utilisent UDP et des ports dynamiques, qui ne sont pas pris en charge par Connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="ca669-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="ca669-240">Il est recommandé de spécifier le port (1433 par défaut, comme indiqué dans l'exemple) dans la chaîne de connexion pour pouvoir être sûr que TCP est activé sur votre instance SQL Server locale et que cette dernière utilise le port correct.</span><span class="sxs-lookup"><span data-stu-id="ca669-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="ca669-241">Pensez à utiliser Authentification SQL Server pour la connexion, en indiquant l'ID utilisateur et le mot de passe dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="ca669-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="ca669-242">Cliquez sur **Enregistrer** dans Visual Studio pour enregistrer le fichier Web.config.</span><span class="sxs-lookup"><span data-stu-id="ca669-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="ca669-243">Exécution du projet localement et inscription d'un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="ca669-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="ca669-244">Exécutez maintenant votre nouveau projet web localement en cliquant sur le bouton Parcourir sous Débogage.</span><span class="sxs-lookup"><span data-stu-id="ca669-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="ca669-245">Cet exemple utilise Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ca669-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="ca669-247">En haut à droite de la page web par défaut, choisissez **Inscription** pour enregistrer un nouveau compte :</span><span class="sxs-lookup"><span data-stu-id="ca669-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="ca669-249">Entrez un nom d'utilisateur et un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="ca669-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="ca669-251">Ceci crée automatiquement sur votre instance SQL Server locale une base de données qui contient les informations d'appartenance pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ca669-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="ca669-252">L’une des tables (**dbo.AspNetUsers**) contient les informations d’identification des utilisateurs de l’application web, comme celles que vous venez d’entrer.</span><span class="sxs-lookup"><span data-stu-id="ca669-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="ca669-253">Cette table sera abordée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ca669-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="ca669-254">Fermez la fenêtre de navigateur de la page web par défaut.</span><span class="sxs-lookup"><span data-stu-id="ca669-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="ca669-255">L'application est alors arrêtée dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca669-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="ca669-256">Vous êtes prêt à passer à l'étape suivante, qui consiste à publier l'application sur Azure et à la tester.</span><span class="sxs-lookup"><span data-stu-id="ca669-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="ca669-257">F.</span><span class="sxs-lookup"><span data-stu-id="ca669-257">F.</span></span> <span data-ttu-id="ca669-258">Publication de l’application web dans Azure et test de l’application</span><span class="sxs-lookup"><span data-stu-id="ca669-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="ca669-259">Vous allez maintenant publier votre application dans votre application web App Service, puis la tester pour voir comment la connexion hybride configurée précédemment connecte votre application web à la base de données sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ca669-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="ca669-260">Publication de l'application web</span><span class="sxs-lookup"><span data-stu-id="ca669-260">Publish the web application</span></span>
1. <span data-ttu-id="ca669-261">Vous pouvez télécharger votre profil de publication de l’application web App Service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ca669-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="ca669-262">Dans le panneau de votre application web, cliquez sur **Obtenir le profil de publication**, puis enregistrez le fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ca669-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Télécharger le profil de publication][PortalDownloadPublishProfile]
   
    <span data-ttu-id="ca669-264">Vous allez ensuite importer ce fichier dans votre application web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca669-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="ca669-265">Dans Visual Studio, cliquez avec le bouton droit sur le nom du projet dans l'Explorateur de solutions et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ca669-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="ca669-267">Dans la boîte de dialogue **Publier le site Web**, sous l'onglet **Profil**, choisissez **Importer**.</span><span class="sxs-lookup"><span data-stu-id="ca669-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Importer][HCVSPublishWebDialogImport]
4. <span data-ttu-id="ca669-269">Recherchez votre profil de publication téléchargé, sélectionnez-le, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca669-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Browse to profile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="ca669-271">Vos informations de publication sont importées et s'affichent sous l'onglet **Connexion** de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ca669-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Cliquer sur Publier][HCVSClickPublish]
   
    <span data-ttu-id="ca669-273">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ca669-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="ca669-274">Lorsque la publication est terminée, votre navigateur démarre et affiche votre application ASP.NET qui est maintenant active dans le cloud Azure !</span><span class="sxs-lookup"><span data-stu-id="ca669-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="ca669-275">Vous allez ensuite utiliser votre application web active pour voir sa connexion hybride en action.</span><span class="sxs-lookup"><span data-stu-id="ca669-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="ca669-276">Test de l'application web terminée sur Azure</span><span class="sxs-lookup"><span data-stu-id="ca669-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="ca669-277">En haut à droite de votre page web sur Azure, choisissez **Ouvrir une session**.</span><span class="sxs-lookup"><span data-stu-id="ca669-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="ca669-279">Votre application web App Service est maintenant connectée à la base de données des membres de votre application web sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ca669-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="ca669-280">Pour le vérifier, ouvrez une session avec les mêmes informations d'identification que celles entrées préalablement dans la base de données locale.</span><span class="sxs-lookup"><span data-stu-id="ca669-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="ca669-282">Pour tester davantage votre nouvelle connexion hybride, déconnectez-vous de votre application web Azure et inscrivez-vous avec d'autres informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="ca669-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="ca669-283">Fournissez un nouveau nom d'utilisateur et un nouveau mot de passe, puis cliquez sur **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="ca669-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="ca669-285">Pour vérifier que les informations d'identification du nouvel utilisateur ont été stockées dans votre base de données locale par l'intermédiaire de votre connexion hybride, ouvrez SQL Management Studio sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ca669-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="ca669-286">Dans l'Explorateur d'objets, développez la base de données **MembershipDB**, puis développez **Tables**.</span><span class="sxs-lookup"><span data-stu-id="ca669-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="ca669-287">Cliquez avec le bouton droit sur la table d'appartenance **dbo.AspNetUsers** et choisissez **Sélectionner les 1 000 premières lignes** pour afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="ca669-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![View the results][HCTestSSMSTree]
5. <span data-ttu-id="ca669-289">Votre table d'appartenance locale indique à présent les deux comptes : celui que vous avez créé localement et celui que vous avez créé dans le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="ca669-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="ca669-290">Celui que vous avez créé dans le cloud a été enregistré dans votre base de données locale par le biais de la fonctionnalité Connexions hybrides d'Azure.</span><span class="sxs-lookup"><span data-stu-id="ca669-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="ca669-292">Vous venez de créer et déployer une application web ASP.NET qui utilise une connexion hybride entre une application web dans le cloud Azure et une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="ca669-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="ca669-293">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ca669-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="ca669-294">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ca669-294">See Also</span></span>
[<span data-ttu-id="ca669-295">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="ca669-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="ca669-296">Josh Twist présente les connexions hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ca669-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="ca669-297">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="ca669-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="ca669-298">BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride</span><span class="sxs-lookup"><span data-stu-id="ca669-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="ca669-299">Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ca669-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="ca669-300">Accéder aux ressources locales à l’aide de connexions hybrides dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ca669-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="ca669-301">Vue d’ensemble d’ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="ca669-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
