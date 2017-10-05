---
title: "Présentation d’Azure Web App sur Linux | Microsoft Docs"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a><span data-ttu-id="9156f-104">Présentation d’Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-104">Introduction to Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="9156f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9156f-105">Overview</span></span>
<span data-ttu-id="9156f-106">Les clients peuvent utiliser Web App sur Linux pour héberger des applications web en mode natif sur Linux pour les piles d’applications prises en charge.</span><span class="sxs-lookup"><span data-stu-id="9156f-106">Customers can use Web App on Linux to host web apps natively on Linux for supported application stacks.</span></span> <span data-ttu-id="9156f-107">La section suivante répertorie les piles d’applications qui sont actuellement prises en charge.</span><span class="sxs-lookup"><span data-stu-id="9156f-107">The following section lists the application stacks that are currently supported.</span></span> 

## <a name="features"></a><span data-ttu-id="9156f-108">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="9156f-108">Features</span></span>
<span data-ttu-id="9156f-109">Web App sur Linux prend actuellement en charge les piles d’applications suivantes :</span><span class="sxs-lookup"><span data-stu-id="9156f-109">Web App on Linux currently supports the following application stacks:</span></span>

* <span data-ttu-id="9156f-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9156f-110">Node.js</span></span>
    * <span data-ttu-id="9156f-111">4.4</span><span class="sxs-lookup"><span data-stu-id="9156f-111">4.4</span></span>
    * <span data-ttu-id="9156f-112">4.5</span><span class="sxs-lookup"><span data-stu-id="9156f-112">4.5</span></span>
    * <span data-ttu-id="9156f-113">6.2</span><span class="sxs-lookup"><span data-stu-id="9156f-113">6.2</span></span>
    * <span data-ttu-id="9156f-114">6.6</span><span class="sxs-lookup"><span data-stu-id="9156f-114">6.6</span></span>
    * <span data-ttu-id="9156f-115">6.9</span><span class="sxs-lookup"><span data-stu-id="9156f-115">6.9</span></span>
    * <span data-ttu-id="9156f-116">6.10</span><span class="sxs-lookup"><span data-stu-id="9156f-116">6.10</span></span>
    * <span data-ttu-id="9156f-117">6.11</span><span class="sxs-lookup"><span data-stu-id="9156f-117">6.11</span></span>
    * <span data-ttu-id="9156f-118">8.0</span><span class="sxs-lookup"><span data-stu-id="9156f-118">8.0</span></span>
    * <span data-ttu-id="9156f-119">8.1</span><span class="sxs-lookup"><span data-stu-id="9156f-119">8.1</span></span>
* <span data-ttu-id="9156f-120">PHP</span><span class="sxs-lookup"><span data-stu-id="9156f-120">PHP</span></span>
    * <span data-ttu-id="9156f-121">5.6</span><span class="sxs-lookup"><span data-stu-id="9156f-121">5.6</span></span>
    * <span data-ttu-id="9156f-122">7.0</span><span class="sxs-lookup"><span data-stu-id="9156f-122">7.0</span></span>
* <span data-ttu-id="9156f-123">.Net Core</span><span class="sxs-lookup"><span data-stu-id="9156f-123">.Net Core</span></span>
    * <span data-ttu-id="9156f-124">1.0</span><span class="sxs-lookup"><span data-stu-id="9156f-124">1.0</span></span>
    * <span data-ttu-id="9156f-125">1.1</span><span class="sxs-lookup"><span data-stu-id="9156f-125">1.1</span></span>
* <span data-ttu-id="9156f-126">Ruby</span><span class="sxs-lookup"><span data-stu-id="9156f-126">Ruby</span></span>
    * <span data-ttu-id="9156f-127">2.3</span><span class="sxs-lookup"><span data-stu-id="9156f-127">2.3</span></span>

<span data-ttu-id="9156f-128">Les clients peuvent déployer leurs applications à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="9156f-128">Customers can deploy their applications by using:</span></span>

* <span data-ttu-id="9156f-129">FTP</span><span class="sxs-lookup"><span data-stu-id="9156f-129">FTP</span></span>
* <span data-ttu-id="9156f-130">Git local</span><span class="sxs-lookup"><span data-stu-id="9156f-130">Local Git</span></span>
* <span data-ttu-id="9156f-131">GitHub</span><span class="sxs-lookup"><span data-stu-id="9156f-131">GitHub</span></span>
* <span data-ttu-id="9156f-132">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="9156f-132">Bitbucket</span></span>

<span data-ttu-id="9156f-133">Pour la mise à l’échelle des applications :</span><span class="sxs-lookup"><span data-stu-id="9156f-133">For application scaling:</span></span>

* <span data-ttu-id="9156f-134">Les clients peuvent faire monter ou descendre en puissance les applications web en modifiant le niveau dans leur plan App Service</span><span class="sxs-lookup"><span data-stu-id="9156f-134">Customers can scale web apps up and down by changing the tier of their App Service plan</span></span>
* <span data-ttu-id="9156f-135">Les clients peuvent augmenter la taille des instances de leurs applications et en exécuter plusieurs instances, dans les limites de leur référence (SKU)</span><span class="sxs-lookup"><span data-stu-id="9156f-135">Customers can scale out applications and run multiple app instances within the confines of their SKU</span></span>

<span data-ttu-id="9156f-136">Pour Kudu, certaines fonctionnalités de base sont :</span><span class="sxs-lookup"><span data-stu-id="9156f-136">For Kudu, some of the basic functionality:</span></span>

* <span data-ttu-id="9156f-137">Environnements</span><span class="sxs-lookup"><span data-stu-id="9156f-137">Environments</span></span>
* <span data-ttu-id="9156f-138">Déploiements</span><span class="sxs-lookup"><span data-stu-id="9156f-138">Deployments</span></span>
* <span data-ttu-id="9156f-139">Console de base</span><span class="sxs-lookup"><span data-stu-id="9156f-139">Basic console</span></span>
* <span data-ttu-id="9156f-140">SSH</span><span class="sxs-lookup"><span data-stu-id="9156f-140">SSH</span></span>

<span data-ttu-id="9156f-141">Pour DevOps :</span><span class="sxs-lookup"><span data-stu-id="9156f-141">For devops:</span></span>

* <span data-ttu-id="9156f-142">Environnements intermédiaires</span><span class="sxs-lookup"><span data-stu-id="9156f-142">Staging environments</span></span>
* <span data-ttu-id="9156f-143">ACR et DockerHub CI/CD</span><span class="sxs-lookup"><span data-stu-id="9156f-143">ACR and DockerHub CI/CD</span></span>

## <a name="limitations"></a><span data-ttu-id="9156f-144">Limites</span><span class="sxs-lookup"><span data-stu-id="9156f-144">Limitations</span></span>
<span data-ttu-id="9156f-145">Le portail Azure affiche uniquement les fonctionnalités actuellement compatibles avec Web App sur Linux, et masque les autres.</span><span class="sxs-lookup"><span data-stu-id="9156f-145">The Azure portal shows only features that currently work for Web App on Linux and hides the rest.</span></span> <span data-ttu-id="9156f-146">Les fonctionnalités seront visibles sur le portail au fur et à mesure de leur activation.</span><span class="sxs-lookup"><span data-stu-id="9156f-146">As we enable more features, they will be visible on the portal.</span></span>

<span data-ttu-id="9156f-147">Certaines fonctionnalités, telles que l’intégration de réseau virtuel, l’authentification Azure Active Directory/tierce, ou les extensions de site Kudu, ne sont pas encore disponibles.</span><span class="sxs-lookup"><span data-stu-id="9156f-147">Some features, such as virtual network integration, Azure Active Directory/third-party authentication, or Kudu site extensions, are not available yet.</span></span> <span data-ttu-id="9156f-148">Dès qu’elles le seront, nous mettrons à jour notre documentation et nous annoncerons les modifications sur notre blog.</span><span class="sxs-lookup"><span data-stu-id="9156f-148">Once these features are available, we will update our documentation and blog about the changes.</span></span>

<span data-ttu-id="9156f-149">Cette version préliminaire publique est actuellement disponible uniquement dans les régions suivantes :</span><span class="sxs-lookup"><span data-stu-id="9156f-149">This public preview is currently only available in the following regions:</span></span>

* <span data-ttu-id="9156f-150">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="9156f-150">West US</span></span>
* <span data-ttu-id="9156f-151">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="9156f-151">East US</span></span>
* <span data-ttu-id="9156f-152">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="9156f-152">West Europe</span></span>
* <span data-ttu-id="9156f-153">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="9156f-153">North Europe</span></span>
* <span data-ttu-id="9156f-154">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="9156f-154">South Central US</span></span>
* <span data-ttu-id="9156f-155">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="9156f-155">North Central US</span></span>
* <span data-ttu-id="9156f-156">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="9156f-156">Southeast Asia</span></span>
* <span data-ttu-id="9156f-157">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="9156f-157">East Asia</span></span>
* <span data-ttu-id="9156f-158">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="9156f-158">Australia East</span></span>
* <span data-ttu-id="9156f-159">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="9156f-159">Japan East</span></span>
* <span data-ttu-id="9156f-160">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="9156f-160">Brazil South</span></span>
* <span data-ttu-id="9156f-161">Inde du Sud</span><span class="sxs-lookup"><span data-stu-id="9156f-161">South India</span></span>

<span data-ttu-id="9156f-162">Web Apps sur Linux est uniquement pris en charge dans les plans App Service dédiés et ne dispose pas d’un niveau Gratuit ou Partagé.</span><span class="sxs-lookup"><span data-stu-id="9156f-162">Web Apps on Linux is only supported in the Dedicated app service plans and does not have a Free or Shared tier.</span></span> <span data-ttu-id="9156f-163">En outre, les plans App Service pour les applications web standards et Linux s’excluent mutuellement : vous ne pouvez pas créer une application web Linux dans un plan App Service non Linux.</span><span class="sxs-lookup"><span data-stu-id="9156f-163">Also, App Service plans for regular and Linux web apps are mutually exclusive, so you cannot create a Linux web app in a non-Linux app service plan.</span></span>

<span data-ttu-id="9156f-164">Sous Linux, les applications web doivent être créées dans un groupe de ressources qui ne contient pas d’applications web non Linux dans la même région.</span><span class="sxs-lookup"><span data-stu-id="9156f-164">Web Apps on Linux must be created in a resource group that does not contain non-Linux web apps in the same region.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9156f-165">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9156f-165">Troubleshooting</span></span> ##

<span data-ttu-id="9156f-166">Lorsque votre application ne démarre pas ou que vous souhaitez vérifier la journalisation à partir de votre application, consultez les journaux Docker dans le répertoire LogFiles.</span><span class="sxs-lookup"><span data-stu-id="9156f-166">When your application fails to start or you want to check the logging from your app, check the Docker logs in the LogFiles directory.</span></span> <span data-ttu-id="9156f-167">Vous pouvez accéder à ce répertoire par le biais de votre site SCM ou d’un FTP.</span><span class="sxs-lookup"><span data-stu-id="9156f-167">You can access this directory either through your SCM site or via FTP.</span></span>
<span data-ttu-id="9156f-168">Pour journaliser `stdout` et `stderr` à partir de votre conteneur, vous devez activer **Journalisation de conteneur Docker** sous **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="9156f-168">To log the `stdout` and `stderr` from your container, you need to enable **Docker Container logging** under **Diagnostics Logs**.</span></span>

![Activation de la journalisation][2]

![Affichage des journaux Docker avec Kudu][1]

<span data-ttu-id="9156f-171">Vous pouvez accéder au site SCM à partir d’**Outils avancés** dans le menu **Outils de développement**.</span><span class="sxs-lookup"><span data-stu-id="9156f-171">You can access the SCM site from **Advanced Tools** in the **Development Tools** menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9156f-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9156f-172">Next steps</span></span>
<span data-ttu-id="9156f-173">Consultez les liens ci-dessous pour vous familiariser avec App Service sur Linux.</span><span class="sxs-lookup"><span data-stu-id="9156f-173">See the following links to get started with App Service on Linux.</span></span> <span data-ttu-id="9156f-174">Vous pouvez poser des questions et signaler vos préoccupations sur [notre forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="9156f-174">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="9156f-175">Comment utiliser une image Docker personnalisé pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-175">How to use a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="9156f-176">Utiliser la configuration PM2 pour Node.js dans Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-176">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="9156f-177">Utiliser .NET Core dans Web App d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-177">Using .NET Core in Azure App Service Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="9156f-178">Utiliser Ruby dans Web Apps d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-178">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="9156f-179">FAQ de Web App d’Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-179">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="9156f-180">Prise en charge SSH pour Azure Web App sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-180">SSH support for Azure Web App on Linux</span></span>](./app-service-linux-ssh-support.md)
* [<span data-ttu-id="9156f-181">Configurer des environnements intermédiaires dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9156f-181">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="9156f-182">Déploiement continu Docker Hub avec l’application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="9156f-182">Docker Hub Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png