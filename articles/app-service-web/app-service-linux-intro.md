---
title: aaaIntroduction tooAzure application Web sur Linux | Documents Microsoft
description: En savoir plus sur Azure Web App sur Linux.
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a><span data-ttu-id="b2267-104">Introduction tooAzure application Web sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-104">Introduction tooAzure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="b2267-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b2267-105">Overview</span></span>
<span data-ttu-id="b2267-106">Clients peuvent utiliser une application Web sur les applications web Linux toohost en mode natif sur Linux pour les piles d’applications pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b2267-106">Customers can use Web App on Linux toohost web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="b2267-107">Hello section suivante répertorie les piles d’application hello actuellement prises en charge.</span><span class="sxs-lookup"><span data-stu-id="b2267-107">hello following section lists hello application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="b2267-108">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="b2267-108">Features</span></span>
<span data-ttu-id="b2267-109">Web application sur Linux prend actuellement en charge hello suivant des piles d’applications :</span><span class="sxs-lookup"><span data-stu-id="b2267-109">Web App on Linux currently supports hello following application stacks:</span></span>

* <span data-ttu-id="b2267-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="b2267-110">Node.js</span></span>
    * <span data-ttu-id="b2267-111">4.4</span><span class="sxs-lookup"><span data-stu-id="b2267-111">4.4</span></span>
    * <span data-ttu-id="b2267-112">4.5</span><span class="sxs-lookup"><span data-stu-id="b2267-112">4.5</span></span>
    * <span data-ttu-id="b2267-113">6.2</span><span class="sxs-lookup"><span data-stu-id="b2267-113">6.2</span></span>
    * <span data-ttu-id="b2267-114">6.6</span><span class="sxs-lookup"><span data-stu-id="b2267-114">6.6</span></span>
    * <span data-ttu-id="b2267-115">6.9</span><span class="sxs-lookup"><span data-stu-id="b2267-115">6.9</span></span>
    * <span data-ttu-id="b2267-116">6.10</span><span class="sxs-lookup"><span data-stu-id="b2267-116">6.10</span></span>
    * <span data-ttu-id="b2267-117">6.11</span><span class="sxs-lookup"><span data-stu-id="b2267-117">6.11</span></span>
    * <span data-ttu-id="b2267-118">8.0</span><span class="sxs-lookup"><span data-stu-id="b2267-118">8.0</span></span>
    * <span data-ttu-id="b2267-119">8.1</span><span class="sxs-lookup"><span data-stu-id="b2267-119">8.1</span></span>
* <span data-ttu-id="b2267-120">PHP</span><span class="sxs-lookup"><span data-stu-id="b2267-120">PHP</span></span>
    * <span data-ttu-id="b2267-121">5.6</span><span class="sxs-lookup"><span data-stu-id="b2267-121">5.6</span></span>
    * <span data-ttu-id="b2267-122">7.0</span><span class="sxs-lookup"><span data-stu-id="b2267-122">7.0</span></span>
* <span data-ttu-id="b2267-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="b2267-123">.Net Core</span></span>
    * <span data-ttu-id="b2267-124">1.0</span><span class="sxs-lookup"><span data-stu-id="b2267-124">1.0</span></span>
    * <span data-ttu-id="b2267-125">1.1</span><span class="sxs-lookup"><span data-stu-id="b2267-125">1.1</span></span>
* <span data-ttu-id="b2267-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="b2267-126">Ruby</span></span>
    * <span data-ttu-id="b2267-127">2.3</span><span class="sxs-lookup"><span data-stu-id="b2267-127">2.3</span></span>

<span data-ttu-id="b2267-128">Les clients peuvent déployer leurs applications à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="b2267-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="b2267-129">FTP</span><span class="sxs-lookup"><span data-stu-id="b2267-129">FTP</span></span>
* <span data-ttu-id="b2267-130">Git local</span><span class="sxs-lookup"><span data-stu-id="b2267-130">Local Git</span></span>
* <span data-ttu-id="b2267-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="b2267-131">GitHub</span></span>
* <span data-ttu-id="b2267-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="b2267-132">Bitbucket</span></span>

<span data-ttu-id="b2267-133">Pour la mise à l’échelle des applications :</span><span class="sxs-lookup"><span data-stu-id="b2267-133">For application scaling:</span></span>

* <span data-ttu-id="b2267-134">Les clients peuvent évoluer les applications web en modifiant le niveau de hello de leur plan de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="b2267-134">Customers can scale web apps up and down by changing hello tier of their App Service plan</span></span>
* <span data-ttu-id="b2267-135">Clients puissent monter en charge les applications et exécuter plusieurs instances de l’application dans les limites de hello de leur référence (SKU)</span><span class="sxs-lookup"><span data-stu-id="b2267-135">Customers can scale out applications and run multiple app instances within hello confines of their SKU</span></span>

<span data-ttu-id="b2267-136">Pour Kudu, certaines des fonctionnalités de base hello :</span><span class="sxs-lookup"><span data-stu-id="b2267-136">For Kudu, some of hello basic functionality:</span></span>

* <span data-ttu-id="b2267-137">Environnements</span><span class="sxs-lookup"><span data-stu-id="b2267-137">Environments</span></span>
* <span data-ttu-id="b2267-138">Déploiements</span><span class="sxs-lookup"><span data-stu-id="b2267-138">Deployments</span></span>
* <span data-ttu-id="b2267-139">Console de base</span><span class="sxs-lookup"><span data-stu-id="b2267-139">Basic console</span></span>
* <span data-ttu-id="b2267-140">SSH</span><span class="sxs-lookup"><span data-stu-id="b2267-140">SSH</span></span>

<span data-ttu-id="b2267-141">Pour DevOps :</span><span class="sxs-lookup"><span data-stu-id="b2267-141">For devops:</span></span>

* <span data-ttu-id="b2267-142">Environnements intermédiaires</span><span class="sxs-lookup"><span data-stu-id="b2267-142">Staging environments</span></span>
* <span data-ttu-id="b2267-143">ACR et DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="b2267-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="b2267-144">Limites</span><span class="sxs-lookup"><span data-stu-id="b2267-144">Limitations</span></span>
<span data-ttu-id="b2267-145">Hello portail Azure affiche uniquement pour les fonctions qui fonctionnent actuellement pour l’application Web sur Linux et masque les reste hello.</span><span class="sxs-lookup"><span data-stu-id="b2267-145">hello Azure portal shows only features that currently work for Web App on Linux and hides hello rest.</span></span> <span data-ttu-id="b2267-146">Comme nous activer d’autres fonctionnalités, elles seront visibles sur le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="b2267-146">As we enable more features, they will be visible on hello portal.</span></span>

<span data-ttu-id="b2267-147">Certaines fonctionnalités, telles que l’intégration de réseau virtuel, l’authentification Azure Active Directory/tierce, ou les extensions de site Kudu, ne sont pas encore disponibles.</span><span class="sxs-lookup"><span data-stu-id="b2267-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="b2267-148">Une fois que ces fonctionnalités sont disponibles, nous mettrons à jour notre documentation et le blog sur les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="b2267-148">Once these features are available, we will update our documentation and blog about hello changes.</span></span>

<span data-ttu-id="b2267-149">Cette version préliminaire publique est actuellement disponible uniquement dans hello suivant régions :</span><span class="sxs-lookup"><span data-stu-id="b2267-149">This public preview is currently only available in hello following regions:</span></span>

* <span data-ttu-id="b2267-150">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b2267-150">West US</span></span>
* <span data-ttu-id="b2267-151">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b2267-151">East US</span></span>
* <span data-ttu-id="b2267-152">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="b2267-152">West Europe</span></span>
* <span data-ttu-id="b2267-153">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="b2267-153">North Europe</span></span>
* <span data-ttu-id="b2267-154">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b2267-154">South Central US</span></span>
* <span data-ttu-id="b2267-155">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="b2267-155">North Central US</span></span>
* <span data-ttu-id="b2267-156">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="b2267-156">Southeast Asia</span></span>
* <span data-ttu-id="b2267-157">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="b2267-157">East Asia</span></span>
* <span data-ttu-id="b2267-158">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="b2267-158">Australia East</span></span>
* <span data-ttu-id="b2267-159">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="b2267-159">Japan East</span></span>
* <span data-ttu-id="b2267-160">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="b2267-160">Brazil South</span></span>
* <span data-ttu-id="b2267-161">Inde du Sud</span><span class="sxs-lookup"><span data-stu-id="b2267-161">South India</span></span>

<span data-ttu-id="b2267-162">Web Apps sur Linux est uniquement pris en charge dans des plans de service d’application dédiée hello et n’a pas d’un niveau gratuit ou partagé.</span><span class="sxs-lookup"><span data-stu-id="b2267-162">Web Apps on Linux is only supported in hello Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="b2267-163">En outre, les plans App Service pour les applications web standards et Linux s’excluent mutuellement : vous ne pouvez pas créer une application web Linux dans un plan App Service non Linux.</span><span class="sxs-lookup"><span data-stu-id="b2267-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="b2267-164">Web Apps sur Linux doit être créée dans un groupe de ressources qui ne contient-elle pas les applications web non-Linux Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="b2267-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in hello same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b2267-165">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="b2267-165">Troubleshooting</span></span> ##

<span data-ttu-id="b2267-166">Lorsque votre application échoue toostart ou utiliser la journalisation hello toocheck à partir de votre application, vérifiez hello que docker enregistre dans le répertoire des fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="b2267-166">When your application fails toostart or you want toocheck hello logging from your app, check hello Docker logs in hello LogFiles directory.</span></span> <span data-ttu-id="b2267-167">Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.</span><span class="sxs-lookup"><span data-stu-id="b2267-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="b2267-168">toolog hello `stdout` et `stderr` à partir de votre conteneur, vous devez tooenable **journalisation du conteneur Docker** sous **les journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="b2267-168">toolog hello `stdout` and `stderr` from your container, you need tooenable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Activation de la journalisation][2]

![Utilisation des journaux de Kudu tooview Docker][1]

<span data-ttu-id="b2267-171">Vous pouvez accéder à site SCM hello **outils avancés** Bonjour **outils de développement** menu.</span><span class="sxs-lookup"><span data-stu-id="b2267-171">You can access hello SCM site from **Advanced Tools** in hello **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2267-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2267-172">Next steps</span></span>
<span data-ttu-id="b2267-173">Consultez hello suivant tooget liens démarré avec le Service d’application sur Linux.</span><span class="sxs-lookup"><span data-stu-id="b2267-173">See hello following links tooget started with App Service on Linux.</span></span> <span data-ttu-id="b2267-174">Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="b2267-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="b2267-175">Comment toouse une Docker personnalisée de l’image pour l’application Web de Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-175">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="b2267-176">Utilisation de la configuration PM2 pour Node.js dans l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="b2267-177">Utiliser .NET Core dans Web App d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="b2267-178">Utiliser Ruby dans Web Apps d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="b2267-179">FAQ de Web App d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="b2267-180">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="b2267-181">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b2267-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="b2267-182">Déploiement continu Docker Hub avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="b2267-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png