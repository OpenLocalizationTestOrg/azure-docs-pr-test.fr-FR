---
title: "Déployer votre application dans Azure App Service avec FTP/S | Microsoft Docs"
description: "Découvrez comment déployer votre application dans Azure App Service avec FTP ou FTPS."
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="71422-103">Déployer votre application dans Azure App Service avec FTP/S</span><span class="sxs-lookup"><span data-stu-id="71422-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="71422-104">Cet article vous explique comment utiliser FTP ou FTPS pour déployer votre application web, votre backend d’applications mobiles ou votre application API dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="71422-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="71422-105">Le point de terminaison FTP/S de votre application est déjà actif.</span><span class="sxs-lookup"><span data-stu-id="71422-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="71422-106">Aucune configuration n’est nécessaire pour activer le déploiement FTP/S.</span><span class="sxs-lookup"><span data-stu-id="71422-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71422-107">Nous prenons en permanence des mesures pour améliorer la sécurité de la plateforme Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="71422-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="71422-108">Dans le cadre de cet effort continu, une mise à niveau des Applications Web est prévue pour les régions d’Allemagne centrale et d’Allemagne du nord-est.</span><span class="sxs-lookup"><span data-stu-id="71422-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="71422-109">L’utilisation du protocole FTP en texte brut pour les déploiements est désactivée pendant cette Web Apps.</span><span class="sxs-lookup"><span data-stu-id="71422-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="71422-110">La recommandation faite à nos clients consiste à basculer vers FTPS pour les déploiements.</span><span class="sxs-lookup"><span data-stu-id="71422-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="71422-111">Aucune interruption de votre service n’aura lieu pendant cette mise à niveau qui est prévue le 5 septembre.</span><span class="sxs-lookup"><span data-stu-id="71422-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="71422-112">Nous vous remercions du soutien apporté à cet effort.</span><span class="sxs-lookup"><span data-stu-id="71422-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="71422-113">Étape 1 : définir les informations d’identification du déploiement</span><span class="sxs-lookup"><span data-stu-id="71422-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="71422-114">Pour accéder au serveur FTP de votre application, vous devez disposer des informations d’identification du déploiement.</span><span class="sxs-lookup"><span data-stu-id="71422-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="71422-115">Pour définir ou réinitialiser vos informations d’identification du déploiement, consultez [Informations d’identification du déploiement d’Azure App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="71422-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="71422-116">Ce didacticiel illustre l’utilisation des informations d’identification de niveau utilisateur.</span><span class="sxs-lookup"><span data-stu-id="71422-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="71422-117">Étape 2 : obtenir les informations de connexion FTP</span><span class="sxs-lookup"><span data-stu-id="71422-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="71422-118">Dans le [portail Azure](https://portal.azure.com), ouvrez le [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) de votre application.</span><span class="sxs-lookup"><span data-stu-id="71422-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="71422-119">Sélectionnez **Vue d’ensemble** dans le menu de gauche, puis notez les valeurs de **Utilisateur FTP/de déploiement**, **Nom de l'hôte FTP** et **Nom de l'hôte FTPS**.</span><span class="sxs-lookup"><span data-stu-id="71422-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Informations de connexion FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="71422-121">Valeur **Utilisateur FTP/de déploiement** affichée par le portail Azure, avec le nom de l’application, afin de fournir le contexte approprié au serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="71422-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="71422-122">Vous pouvez obtenir les mêmes informations en sélectionnant **Propriétés** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="71422-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="71422-123">En outre, le mot de passe du déploiement n’est jamais affiché.</span><span class="sxs-lookup"><span data-stu-id="71422-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="71422-124">Si vous oubliez le mot de passe de votre déploiement, revenez à l’[étape 1](#step1) et réinitialisez-le.</span><span class="sxs-lookup"><span data-stu-id="71422-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="71422-125">Étape 3 : déployer les fichiers sur Azure</span><span class="sxs-lookup"><span data-stu-id="71422-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="71422-126">À partir de votre client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc.), utilisez les informations de connexion que vous avez recueillies pour vous connecter à votre application.</span><span class="sxs-lookup"><span data-stu-id="71422-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="71422-127">Copiez vos fichiers et la structure de répertoire qui leur correspond dans le répertoire [**/site/wwwroot** dans Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) (ou dans le répertoire **/site/wwwroot/App_Data/Jobs/** pour WebJobs).</span><span class="sxs-lookup"><span data-stu-id="71422-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="71422-128">Accédez à l’URL de votre application pour vérifier que l’application s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="71422-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="71422-129">Contrairement aux [déploiements Git](app-service-deploy-local-git.md), un déploiement FTP ne prend pas en charge les automatisations de déploiement suivantes :</span><span class="sxs-lookup"><span data-stu-id="71422-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="71422-130">restauration de dépendances (par exemple, des automatisations NuGet, NPM, PIP et Composer)</span><span class="sxs-lookup"><span data-stu-id="71422-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="71422-131">compilation de fichiers binaires .NET</span><span class="sxs-lookup"><span data-stu-id="71422-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="71422-132">génération du fichier web.config (dont voici un [exemple Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="71422-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="71422-133">Vous devez restaurer, créer, générer ces fichiers requis manuellement sur votre ordinateur local et les déployer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="71422-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="71422-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71422-134">Next steps</span></span>

<span data-ttu-id="71422-135">Pour des scénarios de déploiement plus avancés, consultez [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="71422-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="71422-136">Le déploiement GIT vers Azure autorise le contrôle de version, la restauration du package, MSBuild et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="71422-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="71422-137">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="71422-137">More Resources</span></span>

* <span data-ttu-id="71422-138">[Créer une application Web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP](web-sites-php-mysql-deploy-use-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="71422-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="71422-139">Informations d’identification du déploiement d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="71422-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
