---
title: "Création et déploiement d’un service cloud | Microsoft Docs"
description: "Découvrez comment créer et déployer un service cloud à l'aide du portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: e5ce666f1d826c7901c9fd5e7fafe6171139c3ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-deploy-a-cloud-service"></a><span data-ttu-id="decd1-103">Création et déploiement d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="decd1-103">How to create and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="decd1-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="decd1-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="decd1-105">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="decd1-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="decd1-106">Le portail Azure vous permet de créer et de déployer un service cloud de deux manières : *Création rapide* et *Création personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="decd1-106">The Azure portal provides two ways for you to create and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="decd1-107">Cet article explique comment utiliser la méthode Quick Create pour créer un service cloud et comment utiliser ensuite **Upload** pour télécharger et déployer un package de service cloud dans Azure.</span><span class="sxs-lookup"><span data-stu-id="decd1-107">This article explains how to use the Quick Create method to create a new cloud service and then use **Upload** to upload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="decd1-108">Si vous utilisez cette méthode, le portail Azure met à votre disposition tous les liens nécessaires pour remplir les conditions requises au fur et à mesure.</span><span class="sxs-lookup"><span data-stu-id="decd1-108">When you use this method, the Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="decd1-109">Si vous êtes prêt à déployer votre service cloud lorsque vous le créez, vous pouvez effectuer ces deux opérations en même temps à l'aide de Création personnalisée.</span><span class="sxs-lookup"><span data-stu-id="decd1-109">If you're ready to deploy your cloud service when you create it, you can do both at the same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="decd1-110">Si vous prévoyez de publier votre service cloud depuis Visual Studio Team Services (VSTS), utilisez Création rapide, puis configurez la publication VSTS dans l’outil de démarrage rapide Azure ou dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="decd1-110">If you plan to publish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from the Azure Quickstart or the dashboard.</span></span> <span data-ttu-id="decd1-111">Pour plus d’informations, consultez la page [Livraison continue sur Azure au moyen de Visual Studio Team Services][TFSTutorialForCloudService] ou **Démarrage rapide**.</span><span class="sxs-lookup"><span data-stu-id="decd1-111">For more information, see [Continuous Delivery to Azure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for the **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="decd1-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="decd1-112">Concepts</span></span>
<span data-ttu-id="decd1-113">Trois composants sont nécessaires pour déployer une application en tant que service cloud dans Azure :</span><span class="sxs-lookup"><span data-stu-id="decd1-113">Three components are required to deploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="decd1-114">**Définition de service**</span><span class="sxs-lookup"><span data-stu-id="decd1-114">**Service Definition**</span></span>  
  <span data-ttu-id="decd1-115">Le fichier de définition de service cloud (.csdef) définit le modèle de service, notamment le nombre de rôles.</span><span class="sxs-lookup"><span data-stu-id="decd1-115">The cloud service definition file (.csdef) defines the service model, including the number of roles.</span></span>
* <span data-ttu-id="decd1-116">**Configuration de service**</span><span class="sxs-lookup"><span data-stu-id="decd1-116">**Service Configuration**</span></span>  
  <span data-ttu-id="decd1-117">Le fichier de configuration de service cloud (.cscfg) contient les paramètres de configuration du service cloud et des différents rôles, notamment le nombre d’instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="decd1-117">The cloud service configuration file (.cscfg) provides configuration settings for the cloud service and individual roles, including the number of role instances.</span></span>
* <span data-ttu-id="decd1-118">**Package de service**</span><span class="sxs-lookup"><span data-stu-id="decd1-118">**Service Package**</span></span>  
  <span data-ttu-id="decd1-119">Le package de service (.cspkg) contient le code d’application, les configurations et le fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="decd1-119">The service package (.cspkg) contains the application code and configurations and the service definition file.</span></span>

<span data-ttu-id="decd1-120">Pour plus d’informations sur ces composants et sur la création d’un package, cliquez [ici](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-120">You can learn more about these and how to create a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="decd1-121">Préparation de votre application</span><span class="sxs-lookup"><span data-stu-id="decd1-121">Prepare your app</span></span>
<span data-ttu-id="decd1-122">Avant de déployer un service cloud, vous devez créer le package de service cloud (.cspkg) à partir du code de l'application, ainsi que le fichier de configuration de service cloud (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="decd1-122">Before you can deploy a cloud service, you must create the cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="decd1-123">Le Kit de développement logiciel (SDK) Azure fournit les outils nécessaires à la préparation des fichiers de déploiement.</span><span class="sxs-lookup"><span data-stu-id="decd1-123">The Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="decd1-124">Vous pouvez installer le Kit de développement logiciel (SDK) depuis la page des [téléchargements Azure](https://azure.microsoft.com/downloads/) , dans le langage souhaité pour le développement de votre code.</span><span class="sxs-lookup"><span data-stu-id="decd1-124">You can install the SDK from the [Azure Downloads](https://azure.microsoft.com/downloads/) page, in the language in which you prefer to develop your application code.</span></span>

<span data-ttu-id="decd1-125">Trois fonctions du service cloud nécessitent une configuration spécifique avant d'exporter le package de service :</span><span class="sxs-lookup"><span data-stu-id="decd1-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="decd1-126">Si vous souhaitez déployer un service cloud qui utilise le chiffrement de données SSL (Secure Sockets Layer), [configurez votre application](cloud-services-configure-ssl-certificate-portal.md#modify) pour SSL.</span><span class="sxs-lookup"><span data-stu-id="decd1-126">If you want to deploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="decd1-127">Si vous voulez configurer les connexions Bureau à distance aux instances de rôle, [configurez les rôles](cloud-services-role-enable-remote-desktop-new-portal.md) pour le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="decd1-127">If you want to configure Remote Desktop connections to role instances, [configure the roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="decd1-128">Si vous voulez configurer la surveillance détaillée pour votre service cloud, activez Azure Diagnostics pour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="decd1-128">If you want to configure verbose monitoring for your cloud service, enable Azure Diagnostics for the cloud service.</span></span> <span data-ttu-id="decd1-129">*Surveillance minimale* (niveau de surveillance par défaut) utilise des compteurs de performances récupérés sur le système d'exploitation hôte des instances de rôle (machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="decd1-129">*Minimal monitoring* (the default monitoring level) uses performance counters gathered from the host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="decd1-130">*surveillance détaillée* recueille des mesures supplémentaires sur les données de performances dans les instances de rôle, afin de permettre une analyse plus fine des problèmes qui surviennent au cours du traitement de l'application.</span><span class="sxs-lookup"><span data-stu-id="decd1-130">*Verbose monitoring* gathers additional metrics based on performance data within the role instances to enable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="decd1-131">Pour savoir comment activer Azure Diagnostics, consultez la page [Activation des diagnostics dans Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-131">To find out how to enable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="decd1-132">Pour créer un service cloud avec des déploiements de rôles web ou de rôles de travail, vous devez [créer le package de service](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="decd1-132">To create a cloud service with deployments of web roles or worker roles, you must [create the service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="decd1-133">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="decd1-133">Before you begin</span></span>
* <span data-ttu-id="decd1-134">Si vous n'avez pas installé le Kit de développement logiciel (SDK), cliquez sur **Install Azure SDK** pour ouvrir la page des [téléchargements Azure](https://azure.microsoft.com/downloads/), puis téléchargez le Kit de développement logiciel dans le langage souhaité pour le développement de votre code.</span><span class="sxs-lookup"><span data-stu-id="decd1-134">If you haven't installed the Azure SDK, click **Install Azure SDK** to open the [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download the SDK for the language in which you prefer to develop your code.</span></span> <span data-ttu-id="decd1-135">(Vous pourrez le faire ultérieurement.)</span><span class="sxs-lookup"><span data-stu-id="decd1-135">(You'll have an opportunity to do this later.)</span></span>
* <span data-ttu-id="decd1-136">Si des instances de rôle nécessitent des certificats, créez ces certificats.</span><span class="sxs-lookup"><span data-stu-id="decd1-136">If any role instances require a certificate, create the certificates.</span></span> <span data-ttu-id="decd1-137">Les services cloud requièrent un fichier .pfx avec une clé privée.</span><span class="sxs-lookup"><span data-stu-id="decd1-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="decd1-138">Vous pouvez charger les certificats sur Azure quand vous créez et déployez le service cloud.</span><span class="sxs-lookup"><span data-stu-id="decd1-138">You can upload the certificates to Azure as you create and deploy the cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="decd1-139">Création et déploiement</span><span class="sxs-lookup"><span data-stu-id="decd1-139">Create and deploy</span></span>
1. <span data-ttu-id="decd1-140">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="decd1-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="decd1-141">Cliquez sur **Nouveau >Calculer**, faites défiler la page vers le bas, puis cliquez sur **Service cloud**.</span><span class="sxs-lookup"><span data-stu-id="decd1-141">Click **New > Compute**, and then scroll down to and click **Cloud Service**.</span></span>

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="decd1-143">Dans le nouveau panneau **Service cloud**, entrez une valeur pour le **nom DNS**.</span><span class="sxs-lookup"><span data-stu-id="decd1-143">In the new **Cloud Service** blade, enter a value for the **DNS name**.</span></span>
4. <span data-ttu-id="decd1-144">Créez un **groupe de ressources** ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="decd1-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="decd1-145">Sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="decd1-145">Select a **Location**.</span></span>
6. <span data-ttu-id="decd1-146">Cliquez sur **Package**.</span><span class="sxs-lookup"><span data-stu-id="decd1-146">Click **Package**.</span></span> <span data-ttu-id="decd1-147">Le panneau **Télécharger un package** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="decd1-147">This will open the **Upload a package** blade.</span></span> <span data-ttu-id="decd1-148">Renseignez les champs obligatoires.</span><span class="sxs-lookup"><span data-stu-id="decd1-148">Fill in the required fields.</span></span> <span data-ttu-id="decd1-149">Si l’un de vos rôles contient une seule et même instance, vérifiez que l’option **Déployer même si un ou plusieurs rôles ne contiennent qu’une seule et même instance** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="decd1-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="decd1-150">Vérifiez que l’option **Démarrer le déploiement** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="decd1-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="decd1-151">Cliquez sur **OK** pour fermer le panneau **Télécharger un package**.</span><span class="sxs-lookup"><span data-stu-id="decd1-151">Click **OK** which will close the **Upload a package** blade.</span></span>
9. <span data-ttu-id="decd1-152">Si vous n’avez aucun certificat à ajouter, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="decd1-152">If you do not have any certificates to add, click **Create**.</span></span>

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="decd1-154">Téléchargement d'un certificat</span><span class="sxs-lookup"><span data-stu-id="decd1-154">Upload a certificate</span></span>
<span data-ttu-id="decd1-155">Si votre package de déploiement a été [configuré pour utiliser des certificats](cloud-services-configure-ssl-certificate-portal.md#modify), vous pouvez charger le certificat maintenant.</span><span class="sxs-lookup"><span data-stu-id="decd1-155">If your deployment package was [configured to use certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload the certificate now.</span></span>

1. <span data-ttu-id="decd1-156">Sélectionnez **Certificats** et, dans le panneau **Ajouter des certificats**, sélectionnez le fichier .pfx du certificat SSL et indiquez le **mot de passe** pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="decd1-156">Select **Certificates**, and on the **Add certificates** blade, select the SSL certificate .pfx file, and then provide the **Password** for the certificate,</span></span>
2. <span data-ttu-id="decd1-157">Cliquez sur **Joindre un certificat**, puis sur **OK** dans le panneau **Ajouter des certificats**.</span><span class="sxs-lookup"><span data-stu-id="decd1-157">Click **Attach certificate**, and then click **OK** on the **Add certificates** blade.</span></span>
3. <span data-ttu-id="decd1-158">Cliquez sur **Créer** dans le panneau **Service cloud**.</span><span class="sxs-lookup"><span data-stu-id="decd1-158">Click **Create** on the **Cloud Service** blade.</span></span> <span data-ttu-id="decd1-159">Lorsque le déploiement atteint l'état **Ready** , vous pouvez passer aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="decd1-159">When the deployment has reached the **Ready** status, you can proceed to the next steps.</span></span>

    ![Publier votre service cloud](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="decd1-161">Vérifier la réussite du déploiement</span><span class="sxs-lookup"><span data-stu-id="decd1-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="decd1-162">Cliquez sur l’instance de service cloud.</span><span class="sxs-lookup"><span data-stu-id="decd1-162">Click the cloud service instance.</span></span>

    <span data-ttu-id="decd1-163">L'état présente le service comme étant **En cours d'exécution**.</span><span class="sxs-lookup"><span data-stu-id="decd1-163">The status should show that the service is **Running**.</span></span>
2. <span data-ttu-id="decd1-164">Sous **Bases**, cliquez sur l’**URL du site** pour ouvrir le service cloud dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="decd1-164">Under **Essentials**, click the **Site URL** to open your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="decd1-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="decd1-166">Next steps</span></span>
* <span data-ttu-id="decd1-167">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="decd1-168">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="decd1-169">[Gérez votre service cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="decd1-170">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="decd1-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
