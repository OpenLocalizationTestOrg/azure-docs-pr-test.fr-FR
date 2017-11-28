---
title: "aaaMake web, mobiles et utilisateurs d’Azure pile API apps tooyour disponible | Documents Microsoft"
description: "Didacticiel tooinstall hello du fournisseur de ressources du Service d’applications et créer des offres donnent votre Azure pile utilisateurs hello capacité toocreate, mobile, applications web et API."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a><span data-ttu-id="4e716-103">Rendre web, mobiles et utilisateurs d’Azure pile API apps tooyour disponibles</span><span class="sxs-lookup"><span data-stu-id="4e716-103">Make web, mobile, and API apps available tooyour Azure Stack users</span></span>

<span data-ttu-id="4e716-104">En tant qu’un administrateur de cloud Azure Stack, vous pouvez créer des offres qui permettent à vos utilisateurs (locataires) de créer des applications Azure Functions, web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="4e716-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="4e716-105">En fournissant un accès aux utilisateurs de tooyour toothese applications cloud à la demande, vous pouvez enregistrer les temps et des ressources.</span><span class="sxs-lookup"><span data-stu-id="4e716-105">By providing access toothese on-demand, cloud-based apps tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="4e716-106">tooset cet accès, vous allez :</span><span class="sxs-lookup"><span data-stu-id="4e716-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e716-107">Déployer hello fournisseur de ressources du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="4e716-107">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="4e716-108">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="4e716-108">Create an offer</span></span>
> * <span data-ttu-id="4e716-109">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="4e716-109">Test hello offer</span></span>

## <a name="deploy-hello-app-service-resource-provider"></a><span data-ttu-id="4e716-110">Déployer hello fournisseur de ressources du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="4e716-110">Deploy hello App Service resource provider</span></span>

1. <span data-ttu-id="4e716-111">[Préparer l’hôte du Kit de développement de pile Azure hello](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4e716-111">[Prepare hello Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="4e716-112">Cela inclut le déploiement de fournisseur de ressources SQL Server hello, qui est requis pour la création des applications.</span><span class="sxs-lookup"><span data-stu-id="4e716-112">This includes deploying hello SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="4e716-113">[Télécharger les scripts d’installation et d’assistance hello](azure-stack-app-service-deploy.md#download-the-required-components).</span><span class="sxs-lookup"><span data-stu-id="4e716-113">[Download hello installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="4e716-114">[Exécuter script du programme d’assistance hello toocreate requis certificats](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="4e716-114">[Run hello helper script toocreate required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="4e716-115">[Installer hello fournisseur de ressources du Service d’applications](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (prendra quelques heures tooinstall et, pour tous les hello tooappear des rôles de travail).</span><span class="sxs-lookup"><span data-stu-id="4e716-115">[Install hello App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours tooinstall and for all hello worker roles tooappear).</span></span>
5. <span data-ttu-id="4e716-116">[Valider l’installation de hello](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="4e716-116">[Validate hello installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="4e716-117">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="4e716-117">Create an offer</span></span>

<span data-ttu-id="4e716-118">Vous pouvez créer une offre qui, par exemple, permet aux utilisateurs de créer des systèmes de gestion de contenu web DNN.</span><span class="sxs-lookup"><span data-stu-id="4e716-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="4e716-119">Il requiert le service de SQL Server hello qui vous est déjà activé en installant le fournisseur de ressources SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="4e716-119">It requires hello SQL Server service which you already enabled by installing hello SQL Server resource provider.</span></span>

1.  <span data-ttu-id="4e716-120">[Définissez un quota](azure-stack-setting-quotas.md) et nommez-le *AppServiceQuota*.</span><span class="sxs-lookup"><span data-stu-id="4e716-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="4e716-121">Sélectionnez **Microsoft.Web** pour hello **Namespace** champ.</span><span class="sxs-lookup"><span data-stu-id="4e716-121">Select **Microsoft.Web** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="4e716-122">[Créer un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="4e716-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="4e716-123">Nommez-le *TestAppServicePlan*, sélectionnez Bonjour Bonjour **Microsoft.SQL** service, et **AppService Quota** quota.</span><span class="sxs-lookup"><span data-stu-id="4e716-123">Name it *TestAppServicePlan*, select hello hello **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4e716-124">toolet utilisateurs créer d’autres applications, d’autres services peuvent être nécessaires dans le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="4e716-124">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="4e716-125">Par exemple, les fonctions Azure requiert ce plan hello inclure hello **Microsoft.Storage** de service, tandis que Wordpress requiert **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="4e716-125">For example, Azure Functions requires that hello plan     include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="4e716-126">[Créer une offre](azure-stack-create-offer.md), nommez-le **TestAppServiceOffer** et sélectionnez hello **TestAppServicePlan** plan.</span><span class="sxs-lookup"><span data-stu-id="4e716-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select hello **TestAppServicePlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="4e716-127">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="4e716-127">Test hello offer</span></span>

<span data-ttu-id="4e716-128">Maintenant que vous avez déployé hello fournisseur de ressources du Service d’applications et créé une offre, vous pouvez vous connecter en tant qu’utilisateur, s’abonner toohello offre et créer une application.</span><span class="sxs-lookup"><span data-stu-id="4e716-128">Now that you've deployed hello App Service resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create an app.</span></span> <span data-ttu-id="4e716-129">Pour cet exemple, nous allons créer un système de gestion de contenu de plateforme DNN.</span><span class="sxs-lookup"><span data-stu-id="4e716-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="4e716-130">Vous devez d’abord créer une base de données SQL, puis l’application hello profonds DNN web.</span><span class="sxs-lookup"><span data-stu-id="4e716-130">You must first create a SQL database and then hello DNN web app.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="4e716-131">S’abonner toohello offre</span><span class="sxs-lookup"><span data-stu-id="4e716-131">Subscribe toohello offer</span></span>
1. <span data-ttu-id="4e716-132">Se connecter toohello le portail Azure pile (https://portal.local.azurestack.external) en tant que client.</span><span class="sxs-lookup"><span data-stu-id="4e716-132">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="4e716-133">Cliquez sur **Prendre un abonnement** > tapez **TestAppServiceSubscription** sous **’** > **Sélectionner une offre** > **TestAppServiceOffer** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e716-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="4e716-134">Créer une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="4e716-134">Create a SQL database</span></span>

1. <span data-ttu-id="4e716-135">Cliquez sur **+** > **Données et stockage** > **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="4e716-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="4e716-136">Conservez les valeurs par défaut de la hello pour les champs de hello, sauf comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e716-136">Leave hello defaults for hello fields, except as follows:</span></span>
    - <span data-ttu-id="4e716-137">**Nom de la base de données** : DNNdb</span><span class="sxs-lookup"><span data-stu-id="4e716-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="4e716-138">**Taille maximale (en Mo)** : 100</span><span class="sxs-lookup"><span data-stu-id="4e716-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="4e716-139">**Abonnement**: TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="4e716-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="4e716-140">**Groupe de ressources** : DNN-RG</span><span class="sxs-lookup"><span data-stu-id="4e716-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="4e716-141">Cliquez sur **les paramètres de connexion**, entrez les informations d’identification pour la base de données hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e716-141">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span> <span data-ttu-id="4e716-142">Vous allez utiliser ces informations d’identification plus tard dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="4e716-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="4e716-143">Cliquez sur **référence (SKU)** > sélectionnez hello SKU SQL que vous avez créé pour le serveur d’hébergement SQL de hello > **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e716-143">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="4e716-144">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e716-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="4e716-145">Créer une application DNN</span><span class="sxs-lookup"><span data-stu-id="4e716-145">Create a DNN app</span></span>    

1. <span data-ttu-id="4e716-146">Cliquez sur **+** > **Afficher tout** > **Aperçu de la plateforme DNN** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e716-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="4e716-147">Tapez *DNNapp* sous **Nom de l’application**, puis sélectionnez **TestAppServiceOffer** sous **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4e716-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="4e716-148">Cliquez sur **Configurer les paramètres obligatoires** > **Créer** > tapez un nom de**Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="4e716-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="4e716-149">Cliquez sur **Niveau tarifaire** > **F1 Gratuit** > **Sélectionner** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="4e716-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="4e716-150">Cliquez sur **base de données** et entrez les informations de hello pour la base de données SQL hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4e716-150">Click **Database** and enter hello information for hello SQL database you created earlier.</span></span>
6. <span data-ttu-id="4e716-151">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4e716-151">Click **Create**.</span></span>

<span data-ttu-id="4e716-152">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="4e716-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e716-153">Déployer hello fournisseur de ressources du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="4e716-153">Deploy hello App Service resource provider</span></span>
> * <span data-ttu-id="4e716-154">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="4e716-154">Create an offer</span></span>
> * <span data-ttu-id="4e716-155">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="4e716-155">Test hello offer</span></span>

<span data-ttu-id="4e716-156">Comment toolearn de didacticiel suivant toohello d’avance pour :</span><span class="sxs-lookup"><span data-stu-id="4e716-156">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e716-157">Déployer des applications tooAzure et la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="4e716-157">Deploy apps tooAzure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
