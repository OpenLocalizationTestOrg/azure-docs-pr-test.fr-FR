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
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="1363d-103">Se connecter tooon local SQL Server à partir d’une application web dans Azure App Service à l’aide de connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="1363d-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="1363d-104">Connexions hybrides peuvent se connecter [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ressources tooon local des applications Web qui utilisent un port TCP statique.</span><span class="sxs-lookup"><span data-stu-id="1363d-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="1363d-105">Les ressources prises en charge incluent Microsoft SQL Server, MySQL, les API web HTTP, App Service et la plupart des services web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="1363d-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="1363d-106">Dans ce didacticiel, vous allez apprendre comment toocreate un Service d’application web application Bonjour [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connecter hello web application tooyour sur site local SQL Server de base de données à l’aide de la nouvelle fonctionnalité de connexion hybride hello, créer un simple ASP.NET application qui utilise la connexion hybride hello et déployer hello application toohello application Service web d’application.</span><span class="sxs-lookup"><span data-stu-id="1363d-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="1363d-107">Hello terminé l’application web sur Azure stocke les informations d’identification de l’utilisateur dans une base de données d’appartenance local.</span><span class="sxs-lookup"><span data-stu-id="1363d-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="1363d-108">Hello est supposé aucune expérience préalable à l’aide de Azure ou ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1363d-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="1363d-109">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="1363d-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1363d-110">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="1363d-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="1363d-111">partie des applications Web Hello de fonctionnalité de connexions hybrides hello est uniquement disponible dans hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1363d-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="1363d-112">toocreate une connexion dans les Services BizTalk, consultez [connexions hybrides](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="1363d-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1363d-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1363d-113">Prerequisites</span></span>
<span data-ttu-id="1363d-114">toocomplete ce didacticiel, vous devez hello suite de produits.</span><span class="sxs-lookup"><span data-stu-id="1363d-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="1363d-115">Tous sont disponibles gratuitement, de sorte que vous pouvez commencer à développer gratuitement pour Azure.</span><span class="sxs-lookup"><span data-stu-id="1363d-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="1363d-116">**Abonnement Azure** : pour un abonnement gratuit, consultez la page [Version d'évaluation gratuite d'Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1363d-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="1363d-117">**Visual Studio 2013** -consultez d’une version d’évaluation gratuite de Visual Studio 2013, toodownload [téléchargements Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="1363d-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="1363d-118">Installez ceci avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="1363d-118">Install this before continuing.</span></span>
* <span data-ttu-id="1363d-119">**Microsoft .NET Framework 3.5 Service Pack 1** : si votre système d'exploitation est Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 ou Windows Server 2008 R2, vous pouvez activer cette mise à jour dans Panneau de configuration &gt; Programmes et fonctionnalités &gt; Activer ou désactiver des fonctionnalités Windows.</span><span class="sxs-lookup"><span data-stu-id="1363d-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="1363d-120">Sinon, vous pouvez le télécharger depuis hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="1363d-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="1363d-121">**SQL Server 2014 Express with Tools** -télécharger Microsoft SQL Server Express gratuitement sur hello [page de base de données de Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="1363d-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="1363d-122">Choisissez hello **Express** (pas LocalDB) version.</span><span class="sxs-lookup"><span data-stu-id="1363d-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="1363d-123">Hello **Express with Tools** version inclut SQL Server Management Studio, que vous utiliserez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1363d-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="1363d-124">**SQL Server Management Studio Express** - est incluse avec hello SQL Server 2014 Express avec le téléchargement des outils mentionné ci-dessus, mais si vous avez besoin de tooinstall il séparément, vous pouvez télécharger et l’installer à partir de hello [SQL Server Express page de téléchargement](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="1363d-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="1363d-125">Hello est supposé que vous disposez d’un abonnement Azure, que vous avez installé Visual Studio 2013, et que vous avez installé ou activé le .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="1363d-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="1363d-126">didacticiel de Hello vous montre comment tooinstall SQL Server 2014 Express dans une configuration qui fonctionne bien avec les connexions hybrides hello fonctionnalité (une instance par défaut avec un port TCP statique).</span><span class="sxs-lookup"><span data-stu-id="1363d-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="1363d-127">Avant de commencer le didacticiel de hello, téléchargez SQL Server 2014 Express with Tools à partir de l’emplacement hello mentionné ci-dessus, si vous n’avez pas installé de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1363d-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="1363d-128">Remarques</span><span class="sxs-lookup"><span data-stu-id="1363d-128">Notes</span></span>
<span data-ttu-id="1363d-129">toouse un local SQL Server ou la base de données SQL Server Express avec une connexion hybride, TCP/IP doit toobe activé sur un port statique.</span><span class="sxs-lookup"><span data-stu-id="1363d-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="1363d-130">Les instances par défaut dans SQL Server utilisent le port statique 1433, mais pas les instances nommées.</span><span class="sxs-lookup"><span data-stu-id="1363d-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="1363d-131">ordinateur Hello sur lequel vous installez l’agent de gestionnaire de connexions hybrides hello local :</span><span class="sxs-lookup"><span data-stu-id="1363d-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="1363d-132">Connectivité sortante tooAzure devez sur :</span><span class="sxs-lookup"><span data-stu-id="1363d-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="1363d-133">Port</span><span class="sxs-lookup"><span data-stu-id="1363d-133">Port</span></span> | <span data-ttu-id="1363d-134">Pourquoi</span><span class="sxs-lookup"><span data-stu-id="1363d-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="1363d-135">80</span><span class="sxs-lookup"><span data-stu-id="1363d-135">80</span></span> |<span data-ttu-id="1363d-136">**Obligatoire** pour le port HTTP pour la validation du certificat et éventuellement la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="1363d-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="1363d-137">443</span><span class="sxs-lookup"><span data-stu-id="1363d-137">443</span></span> |<span data-ttu-id="1363d-138">**Facultatif** pour la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="1363d-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="1363d-139">Si la connectivité sortante too443 n’est pas disponible, le port TCP 80 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1363d-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="1363d-140">5671 et 9352</span><span class="sxs-lookup"><span data-stu-id="1363d-140">5671 and 9352</span></span> |<span data-ttu-id="1363d-141">**Recommandé** mais facultatif pour la connectivité des données.</span><span class="sxs-lookup"><span data-stu-id="1363d-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="1363d-142">Notez que ce mode entraîne habituellement un débit plus élevé.</span><span class="sxs-lookup"><span data-stu-id="1363d-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="1363d-143">Si les ports toothese connexion sortante n’est pas disponible, le port TCP 443 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1363d-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="1363d-144">Doit être en mesure de tooreach hello *nom d’hôte*:*numéro_port* de votre ressource locale.</span><span class="sxs-lookup"><span data-stu-id="1363d-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="1363d-145">Hello dans cet article suppose que vous utilisez le navigateur hello à partir de l’ordinateur hello qui hébergera l’agent de connexion hybride hello localement.</span><span class="sxs-lookup"><span data-stu-id="1363d-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="1363d-146">Si vous avez déjà SQL Server est installé dans une configuration et dans un environnement qui répond aux conditions hello décrites ci-dessus, vous pouvez passer et commencer par [créer une base de données SQL Server sur site](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="1363d-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="1363d-147">R :</span><span class="sxs-lookup"><span data-stu-id="1363d-147">A.</span></span> <span data-ttu-id="1363d-148">Installation de SQL Server Express, activation de TCP/IP et création d'une base de données SQL Server en local</span><span class="sxs-lookup"><span data-stu-id="1363d-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="1363d-149">Cette section vous montre comment tooinstall SQL Server Express, activez TCP/IP et comment créer une base de données afin que votre application web fonctionne avec hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1363d-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="1363d-150">Installation de SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="1363d-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="1363d-151">tooinstall SQL Server Express, exécutez hello **SQLEXPRWT_x64_ENU.exe** ou **SQLEXPR_x86_ENU.exe** fichier que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="1363d-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="1363d-152">Assistant du centre d’Installation SQL Server Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1363d-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![SQL Server Install][SQLServerInstall]
2. <span data-ttu-id="1363d-154">Choisissez **nouvelle installation SQL Server autonome ou ajoutez l’installation existante de fonctionnalités tooan**.</span><span class="sxs-lookup"><span data-stu-id="1363d-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="1363d-155">Suivez les instructions de hello, en acceptant les choix par défaut hello et les paramètres, jusqu'à ce que vous atteigniez toohello **Configuration de l’Instance** page.</span><span class="sxs-lookup"><span data-stu-id="1363d-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="1363d-156">Sur hello **Configuration de l’Instance** choisissez **instance par défaut**.</span><span class="sxs-lookup"><span data-stu-id="1363d-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Choose Default Instance][ChooseDefaultInstance]
   
    <span data-ttu-id="1363d-158">Par défaut, instance par défaut de hello de SQL Server écoute les demandes des clients de SQL Server sur le port statique 1433, c'est-à-dire le connexions hybrides fonctionnalité nécessite hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="1363d-159">Les instances nommées utilisent des ports dynamiques et UDP, qui ne sont pas pris en charge par Connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="1363d-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="1363d-160">Accepter les valeurs par défaut hello hello **Configuration du serveur** page.</span><span class="sxs-lookup"><span data-stu-id="1363d-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="1363d-161">Sur hello **Configuration du moteur de base de données** sous **Mode d’authentification**, choisissez **en Mode mixte (authentification SQL Server et l’authentification Windows)**et fournir un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1363d-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Choose Mixed Mode][ChooseMixedMode]
   
    <span data-ttu-id="1363d-163">Dans ce didacticiel, vous allez utiliser l'authentification SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1363d-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="1363d-164">Être tooremember vraiment hello un mot de passe que vous fournissez, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1363d-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="1363d-165">Parcourez reste hello d’installation de hello Assistant toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="1363d-166">Activation de TCP/IP</span><span class="sxs-lookup"><span data-stu-id="1363d-166">Enable TCP/IP</span></span>
<span data-ttu-id="1363d-167">tooenable TCP/IP, vous allez utiliser le Gestionnaire de Configuration SQL Server, qui a été installée lors de l’installation de SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="1363d-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="1363d-168">Suivez les étapes de hello dans [activer le protocole réseau TCP/IP pour SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="1363d-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="1363d-169">Création d'une base de données SQL Server en local</span><span class="sxs-lookup"><span data-stu-id="1363d-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="1363d-170">Votre application Visual Studio nécessite une base de données d'appartenance à laquelle Azure puisse accéder.</span><span class="sxs-lookup"><span data-stu-id="1363d-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="1363d-171">Cela nécessite une base de données SQL Server ou SQL Server Express (pas hello LocalDB base de données hello utilise du modèle MVC par défaut), donc vous allez ensuite créer de base de données d’appartenance de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="1363d-172">Dans SQL Server Management Studio, connectez-vous toohello SQL Server, vous venez d’installer.</span><span class="sxs-lookup"><span data-stu-id="1363d-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="1363d-173">(Si hello **connecter tooServer** boîte de dialogue n’apparaît pas automatiquement, accédez trop**l’Explorateur d’objets** dans le volet gauche de hello, cliquez sur **connexion**, puis cliquez sur **Du moteur de base de données**.) ![Se connecter tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="1363d-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="1363d-174">Dans la zone **Type de serveur**, choisissez **Moteur de base de données**.</span><span class="sxs-lookup"><span data-stu-id="1363d-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="1363d-175">Pour **nom du serveur**, vous pouvez utiliser **localhost** hello nom ou de hello ordinateur que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="1363d-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="1363d-176">Choisissez **l’authentification SQL Server**, puis ouvrez une session avec le nom d’utilisateur hello et le mot de passe hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1363d-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="1363d-177">toocreate une base de données à l’aide de SQL Server Management Studio, cliquez sur **bases de données** dans l’Explorateur d’objets, puis cliquez sur **nouvelle base de données**.</span><span class="sxs-lookup"><span data-stu-id="1363d-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Create new database][SSMScreateNewDB]
3. <span data-ttu-id="1363d-179">Bonjour **nouvelle base de données** boîte de dialogue, entrez MembershipDB pour le nom de base de données hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1363d-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="1363d-181">Notez que vous n’apportez pas de toute base de données de toohello de modifications à ce stade.</span><span class="sxs-lookup"><span data-stu-id="1363d-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="1363d-182">les informations d’appartenance Hello seront ajoutées automatiquement ultérieurement par votre application web lors de son exécution.</span><span class="sxs-lookup"><span data-stu-id="1363d-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="1363d-183">Dans l’Explorateur d’objets, si vous développez **bases de données**, vous verrez cette base de données d’appartenance hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="1363d-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="1363d-185">B.</span><span class="sxs-lookup"><span data-stu-id="1363d-185">B.</span></span> <span data-ttu-id="1363d-186">Créer une application web Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="1363d-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="1363d-187">Si vous avez déjà créé une application web dans hello portail Azure que vous souhaitez toouse pour ce didacticiel, vous pouvez passer trop[créer une connexion hybride et un BizTalk Service](#CreateHC) et continuer à partir de là.</span><span class="sxs-lookup"><span data-stu-id="1363d-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="1363d-188">Bonjour [Azure Portal](https://portal.azure.com), cliquez sur **nouveau** > **Web + Mobile** > **application Web**.</span><span class="sxs-lookup"><span data-stu-id="1363d-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Bouton Nouveau][New]
2. <span data-ttu-id="1363d-190">Configurez votre application web, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1363d-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="1363d-192">Après quelques instants, l’application hello web est créée et son panneau de l’application web s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1363d-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="1363d-193">Panneau de Hello est un tableau de bord permettant le défilement vertical qui vous permet de gérer votre application web.</span><span class="sxs-lookup"><span data-stu-id="1363d-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="1363d-195">l’application web tooverify hello est dynamique, vous pouvez cliquer sur hello **Parcourir** page par défaut d’icône toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="1363d-196">Ensuite, vous allez créer une connexion hybride et un service BizTalk pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="1363d-197">C.</span><span class="sxs-lookup"><span data-stu-id="1363d-197">C.</span></span> <span data-ttu-id="1363d-198">Création d’une connexion hybride et d’un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="1363d-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="1363d-199">Précédent dans hello portail, accédez à toosettings et cliquez sur **réseau** > **configurer vos points de terminaison de connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="1363d-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connexions hybrides][CreateHCHCIcon]
2. <span data-ttu-id="1363d-201">Dans le panneau de connexions hybrides hello, cliquez sur **ajouter** > **connexion hybride**.</span><span class="sxs-lookup"><span data-stu-id="1363d-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="1363d-202">Sur hello **créer la connexion hybride** panneau :</span><span class="sxs-lookup"><span data-stu-id="1363d-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="1363d-203">Pour **nom**, fournissez un nom pour la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="1363d-204">Pour **nom d’hôte**, entrez le nom de l’ordinateur hello de votre ordinateur hôte de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1363d-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="1363d-205">Pour **Port**, entrez 1433 (hello port par défaut pour SQL Server).</span><span class="sxs-lookup"><span data-stu-id="1363d-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="1363d-206">Cliquez sur **BizTalk Service** > **nouveau BizTalk Service** et entrez un nom pour hello service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="1363d-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Create a hybrid connection][TwinCreateHCBlades]
4. <span data-ttu-id="1363d-208">Cliquez sur **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="1363d-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="1363d-209">Lorsque les processus hello est terminée, hello **Notifications** un vert clignote en zone **réussite** et hello **connexion hybride** panneau affichera hello connexion hybride avec Hello état en tant que **non connecté**.</span><span class="sxs-lookup"><span data-stu-id="1363d-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="1363d-211">À ce stade, vous avez terminé une partie importante de l’infrastructure de connexion hello cloud hybride.</span><span class="sxs-lookup"><span data-stu-id="1363d-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="1363d-212">Vous allez ensuite créer un élément local.</span><span class="sxs-lookup"><span data-stu-id="1363d-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="1363d-213">D.</span><span class="sxs-lookup"><span data-stu-id="1363d-213">D.</span></span> <span data-ttu-id="1363d-214">Installer la fonctionnalité connexion hello toocomplete hello local gestionnaire de connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="1363d-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="1363d-215">Cette infrastructure de connexion hybride hello est terminée, vous allez créer une application web qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="1363d-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="1363d-216">E.</span><span class="sxs-lookup"><span data-stu-id="1363d-216">E.</span></span> <span data-ttu-id="1363d-217">Créer un projet web de base ASP.NET, modifier la chaîne de connexion de base de données hello et exécuter le projet de hello localement</span><span class="sxs-lookup"><span data-stu-id="1363d-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="1363d-218">Création d'un projet ASP.NET de base</span><span class="sxs-lookup"><span data-stu-id="1363d-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="1363d-219">Dans Visual Studio, sur hello **fichier** menu, créez un nouveau projet :</span><span class="sxs-lookup"><span data-stu-id="1363d-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="1363d-221">Bonjour **modèles** section Hello **nouveau projet** boîte de dialogue, sélectionnez **Web** et choisissez **Application Web ASP.NET**, puis cliquez sur  **OK**.</span><span class="sxs-lookup"><span data-stu-id="1363d-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="1363d-223">Bonjour **nouveau projet ASP.NET** boîte de dialogue, choisissez **MVC**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1363d-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="1363d-225">Lorsque le projet de hello a été créé, la page du fichier Lisez-moi application hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1363d-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="1363d-226">N’exécutez pas encore projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-226">Do not run hello web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="1363d-228">Modifier la chaîne de connexion de base de données hello pour une application hello</span><span class="sxs-lookup"><span data-stu-id="1363d-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="1363d-229">Dans cette étape, vous modifiez la chaîne de connexion hello qui indique à votre application où toofind de votre serveur local SQL Server Express base de données.</span><span class="sxs-lookup"><span data-stu-id="1363d-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="1363d-230">chaîne de connexion Hello est dans le fichier Web.config de l’application hello, qui contient les informations de configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="1363d-231">tooensure que votre application utilise une base de données hello que vous avez créé dans SQL Server Express et non la hello une dans la valeur par défaut de Visual Studio base de données locale, il est important d’effectuer cette étape avant d’exécuter votre projet.</span><span class="sxs-lookup"><span data-stu-id="1363d-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="1363d-232">Dans l’Explorateur de solutions, double-cliquez sur le fichier Web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="1363d-234">Modifier hello **connectionStrings** section toopoint toohello base de données SQL sur votre ordinateur local, la syntaxe hello Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1363d-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Chaîne de connexion][HCVSConnectionString]
   
    <span data-ttu-id="1363d-236">Pour composer la chaîne hello, gardez suivante de hello l’esprit :</span><span class="sxs-lookup"><span data-stu-id="1363d-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="1363d-237">Si vous vous connectez tooa nommé instance au lieu d’une instance par défaut (par exemple, YourServer\SQLEXPRESS), vous devez configurer les ports statiques toouse de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1363d-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="1363d-238">Pour plus d’informations sur la configuration des ports statiques, consultez [comment tooconfigure les toolisten de SQL Server sur un port spécifique](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="1363d-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="1363d-239">Par défaut, les instances nommées utilisent UDP et des ports dynamiques, qui ne sont pas pris en charge par Connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="1363d-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="1363d-240">Il est recommandé de spécifier hello port (1433 par défaut, comme indiqué dans l’exemple de hello) de chaîne de connexion hello afin que vous pouvez être certain que votre serveur SQL Server local a TCP activé et qu’il utilise le port correct de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="1363d-241">N’oubliez pas de tooconnect de l’authentification SQL Server toouse, en spécifiant hello ID d’utilisateur et mot de passe dans votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="1363d-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="1363d-242">Cliquez sur **enregistrer** dans le fichier Web.config de Visual Studio toosave hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="1363d-243">Exécutez le projet de hello localement et inscrire un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="1363d-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="1363d-244">Maintenant, exécutez localement votre projet web en cliquant sur Parcourir hello sous le débogage.</span><span class="sxs-lookup"><span data-stu-id="1363d-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="1363d-245">Cet exemple utilise Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="1363d-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="1363d-247">Hello supérieur à droite de la page web de hello par défaut, choisissez **inscrire** tooregister un nouveau compte :</span><span class="sxs-lookup"><span data-stu-id="1363d-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="1363d-249">Entrez un nom d'utilisateur et un mot de passe :</span><span class="sxs-lookup"><span data-stu-id="1363d-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="1363d-251">Cela crée automatiquement une base de données sur votre serveur SQL local qui contient les informations d’appartenance hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="1363d-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="1363d-252">Une des tables de hello (**dbo. AspNetUsers**) contient web application informations d’identification que celles que vous venez d’entrer hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="1363d-253">Vous verrez cette table plus loin dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="1363d-254">Fermez la fenêtre du navigateur hello de page web de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="1363d-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="1363d-255">Cela arrête application hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1363d-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="1363d-256">Vous êtes maintenant prêt pour l’étape suivante de hello, qui est toopublish hello application tooAzure et le tester.</span><span class="sxs-lookup"><span data-stu-id="1363d-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="1363d-257">F.</span><span class="sxs-lookup"><span data-stu-id="1363d-257">F.</span></span> <span data-ttu-id="1363d-258">Hello web application tooAzure de publier et de le tester</span><span class="sxs-lookup"><span data-stu-id="1363d-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="1363d-259">Maintenant, vous allez publier votre application web App Service de tooyour application et testez-le toosee comment vous avez configuré précédemment la connexion hybride hello est en cours tooconnect utilisé votre base de données web application toohello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="1363d-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="1363d-260">Publier l’application web de hello</span><span class="sxs-lookup"><span data-stu-id="1363d-260">Publish hello web application</span></span>
1. <span data-ttu-id="1363d-261">Vous pouvez télécharger votre profil de publication pour hello application Service web d’application Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1363d-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="1363d-262">Dans le panneau de hello pour votre application web, cliquez sur **obtenir le profil de publication**, puis enregistrez ordinateur tooyour de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Télécharger le profil de publication][PortalDownloadPublishProfile]
   
    <span data-ttu-id="1363d-264">Vous allez ensuite importer ce fichier dans votre application web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1363d-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="1363d-265">Dans Visual Studio, cliquez sur le nom de projet hello dans l’Explorateur de solutions et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="1363d-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="1363d-267">Bonjour **publier le site Web** boîte de dialogue hello **profil** , onglet choisir **importation**.</span><span class="sxs-lookup"><span data-stu-id="1363d-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Importer][HCVSPublishWebDialogImport]
4. <span data-ttu-id="1363d-269">Parcourir tooyour téléchargé le profil de publication, sélectionnez-le, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1363d-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Parcourir tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="1363d-271">Vos informations de publication est importées et affiche sur hello **connexion** onglet de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Cliquer sur Publier][HCVSClickPublish]
   
    <span data-ttu-id="1363d-273">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="1363d-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="1363d-274">Lorsque la publication est terminée, votre navigateur lancera et afficher votre application ASP.NET maintenant familiarisée--, sauf qu’il est maintenant en ligne Bonjour Azure cloud !</span><span class="sxs-lookup"><span data-stu-id="1363d-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="1363d-275">Ensuite, vous allez utiliser votre toosee d’application web dynamique sa connexion hybride en action.</span><span class="sxs-lookup"><span data-stu-id="1363d-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="1363d-276">Hello du test terminé l’application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="1363d-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="1363d-277">En haut de hello à droite de votre page web sur Azure, choisissez **connecter**.</span><span class="sxs-lookup"><span data-stu-id="1363d-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="1363d-279">Votre Service d’application web application est maintenant connecté de base de données d’appartenance de l’application tooyour web sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="1363d-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="1363d-280">tooverify, connectez-vous avec hello mêmes informations d’identification que vous avez entré dans hello local de base de données précédemment.</span><span class="sxs-lookup"><span data-stu-id="1363d-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="1363d-282">toofurther tester votre connexion hybride, déconnectez-vous de votre application web Azure et inscrire en tant qu’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1363d-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="1363d-283">Fournissez un nouveau nom d'utilisateur et un nouveau mot de passe, puis cliquez sur **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="1363d-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="1363d-285">tooverify que les informations d’identification hello du nouvel utilisateur ont été stockées dans votre base de données locale via une connexion hybride, ouvrez SQL Management Studio sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="1363d-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="1363d-286">Dans l’Explorateur d’objets, développez hello **MembershipDB** de base de données, puis développez **Tables**.</span><span class="sxs-lookup"><span data-stu-id="1363d-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="1363d-287">Avec le bouton hello **dbo. AspNetUsers** l’appartenance de table et choisissez **sélectionnez 1000 lignes du haut** des résultats tooview hello.</span><span class="sxs-lookup"><span data-stu-id="1363d-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Afficher les résultats de hello][HCTestSSMSTree]
5. <span data-ttu-id="1363d-289">Votre table des appartenances local affiche maintenant les deux comptes - hello créé localement et hello créé Bonjour cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="1363d-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="1363d-290">Hello une que vous avez créé dans le cloud de hello a été enregistré tooyour de la base de données locale via la fonctionnalité de connexion hybride d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1363d-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="1363d-292">Vous avez maintenant créé et déployé une application web ASP.NET qui utilise une connexion hybride entre une application web Bonjour Azure cloud et une base de données SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="1363d-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="1363d-293">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="1363d-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="1363d-294">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1363d-294">See Also</span></span>
[<span data-ttu-id="1363d-295">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="1363d-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="1363d-296">Josh Twist présente les connexions hybrides (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="1363d-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="1363d-297">Aperçu des connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="1363d-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="1363d-298">BizTalk Services : Onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride</span><span class="sxs-lookup"><span data-stu-id="1363d-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="1363d-299">Création d’un cloud hybride réel avec la portabilité transparente des applications (vidéo Channel 9)</span><span class="sxs-lookup"><span data-stu-id="1363d-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="1363d-300">Accéder aux ressources locales à l’aide de connexions hybrides dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1363d-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="1363d-301">Vue d’ensemble d’ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="1363d-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
