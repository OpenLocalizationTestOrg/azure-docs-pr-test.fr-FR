---
title: "aaaDeploy votre tooAzure d’application du Service d’applications à l’aide de FTP/S | Documents Microsoft"
description: "Découvrez comment toodeploy votre tooAzure d’application du Service d’applications à l’aide de FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="4f031-103">Déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S</span><span class="sxs-lookup"><span data-stu-id="4f031-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="4f031-104">Cet article vous montre comment toouse FTP ou FTPS toodeploy votre application web, un principal de l’application mobile ou une application API trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="4f031-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="4f031-105">point de terminaison Hello FTP/S pour votre application est déjà active.</span><span class="sxs-lookup"><span data-stu-id="4f031-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="4f031-106">Aucune configuration n’est un déploiement de FTP/S tooenable nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4f031-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f031-107">Nous prenons en permanence des étapes tooimprove sécurité de la plateforme Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4f031-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="4f031-108">Dans le cadre de cet effort continu, une mise à niveau des Applications Web est prévue pour les régions d’Allemagne centrale et d’Allemagne du nord-est.</span><span class="sxs-lookup"><span data-stu-id="4f031-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="4f031-109">Au cours de cette, applications Web seront désactivation utilisez hello du protocole FTP en texte brut pour les déploiements.</span><span class="sxs-lookup"><span data-stu-id="4f031-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="4f031-110">Nos clients tooour de recommandation est tooFTPS tooswitch pour les déploiements.</span><span class="sxs-lookup"><span data-stu-id="4f031-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="4f031-111">Nous n’attendent pas de n’importe quel service de tooyour interruption pendant cette mise à niveau qui est prévue pour le 9/5.</span><span class="sxs-lookup"><span data-stu-id="4f031-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="4f031-112">Nous vous remercions du soutien apporté à cet effort.</span><span class="sxs-lookup"><span data-stu-id="4f031-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="4f031-113">Étape 1 : définir les informations d’identification du déploiement</span><span class="sxs-lookup"><span data-stu-id="4f031-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="4f031-114">serveur de hello FTP tooaccess pour votre application, vous devez tout d’abord d’informations d’identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="4f031-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="4f031-115">tooset ou réinitialiser vos informations d’identification de déploiement, consultez [informations d’identification du déploiement Azure App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="4f031-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="4f031-116">Ce didacticiel montre l’utilisation hello d’informations d’identification au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4f031-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="4f031-117">Étape 2 : obtenir les informations de connexion FTP</span><span class="sxs-lookup"><span data-stu-id="4f031-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="4f031-118">Bonjour [portail Azure](https://portal.azure.com), ouvrez votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="4f031-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="4f031-119">Sélectionnez **vue d’ensemble** dans le menu de gauche hello, puis notez les valeurs hello pour **utilisateur FTP/déploiement**, **nom d’hôte FTP**, et **nom d’hôte FTPS**.</span><span class="sxs-lookup"><span data-stu-id="4f031-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informations de connexion FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="4f031-121">Hello **utilisateur FTP/déploiement** valeur utilisateur tel qu’affiché par hello portail Azure, y compris le nom de l’application hello dans l’ordre tooprovide bon contexte hello FTP serveur.</span><span class="sxs-lookup"><span data-stu-id="4f031-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="4f031-122">Vous pouvez trouver hello les mêmes informations lorsque vous sélectionnez **propriétés** dans le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4f031-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="4f031-123">En outre, le mot de passe de déploiement hello n’est jamais affichée.</span><span class="sxs-lookup"><span data-stu-id="4f031-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="4f031-124">Si vous oubliez votre mot de passe de déploiement, revenez trop[étape 1](#step1) et réinitialiser votre mot de passe de déploiement.</span><span class="sxs-lookup"><span data-stu-id="4f031-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="4f031-125">Étape 3 : Déployer des fichiers tooAzure</span><span class="sxs-lookup"><span data-stu-id="4f031-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="4f031-126">À partir de votre client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc.), utilisez les informations de connexion hello collectées tooconnect tooyour application.</span><span class="sxs-lookup"><span data-stu-id="4f031-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="4f031-127">Copier vos fichiers et leur toohello de structure de répertoire correspondant [ **/site/wwwroot** active](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) dans Azure (ou hello **/site/wwwroot/App_Data/tâches/** répertoire pour Les tâches Web).</span><span class="sxs-lookup"><span data-stu-id="4f031-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="4f031-128">Application de l’application de navigation tooyour URL tooverify hello s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="4f031-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4f031-129">Contrairement aux [déploiements Git](app-service-deploy-local-git.md), déploiement FTP ne prend pas en charge hello suivant automatisations de déploiement :</span><span class="sxs-lookup"><span data-stu-id="4f031-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="4f031-130">restauration de dépendances (par exemple, des automatisations NuGet, NPM, PIP et Composer)</span><span class="sxs-lookup"><span data-stu-id="4f031-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="4f031-131">compilation de fichiers binaires .NET</span><span class="sxs-lookup"><span data-stu-id="4f031-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="4f031-132">génération du fichier web.config (dont voici un [exemple Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="4f031-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="4f031-133">Vous devez restaurer, créer, générer ces fichiers requis manuellement sur votre ordinateur local et les déployer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="4f031-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4f031-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f031-134">Next steps</span></span>

<span data-ttu-id="4f031-135">Pour les scénarios de déploiement plus avancées, essayez [déploiement tooAzure avec Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="4f031-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="4f031-136">Déploiement GIT tooAzure permet le contrôle de version, la restauration des packages, MSBuild et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="4f031-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="4f031-137">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="4f031-137">More Resources</span></span>

* <span data-ttu-id="4f031-138">[Créer une application Web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="4f031-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="4f031-139">Informations d’identification du déploiement d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4f031-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
