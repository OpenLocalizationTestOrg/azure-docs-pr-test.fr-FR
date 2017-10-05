---
title: "Mettre des applications web, mobiles et API à la disposition de vos utilisateurs Azure Stack | Microsoft Docs"
description: "Didacticiel pour installer le fournisseur de ressources App Service et créer des offres qui donnent à vos utilisateurs Azure Stack la possibilité de créer des applications web, mobiles et API."
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
ms.openlocfilehash: 11ecaa8ec017a9eb1285928e3d3d367ddfc43022
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="make-web-mobile-and-api-apps-available-to-your-azure-stack-users"></a><span data-ttu-id="ab7ae-103">Mettre des applications web, mobiles et API à la disposition de vos utilisateurs Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ab7ae-103">Make web, mobile, and API apps available to your Azure Stack users</span></span>

<span data-ttu-id="ab7ae-104">En tant qu’un administrateur de cloud Azure Stack, vous pouvez créer des offres qui permettent à vos utilisateurs (locataires) de créer des applications Azure Functions, web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create Azure Functions and web, mobile, and API applications.</span></span> <span data-ttu-id="ab7ae-105">En permettant à vos utilisateurs d’accéder à ces applications cloud à la demande, vous pouvez leur faire gagner du temps et économiser des ressources.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-105">By providing access to these on-demand, cloud-based apps to your users, you can save them time and resources.</span></span> <span data-ttu-id="ab7ae-106">Pour effectuer cette configuration, vous allez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab7ae-106">To set this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab7ae-107">Déployer le fournisseur de ressources App Service</span><span class="sxs-lookup"><span data-stu-id="ab7ae-107">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="ab7ae-108">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-108">Create an offer</span></span>
> * <span data-ttu-id="ab7ae-109">Tester l’offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-109">Test the offer</span></span>

## <a name="deploy-the-app-service-resource-provider"></a><span data-ttu-id="ab7ae-110">Déployer le fournisseur de ressources App Service</span><span class="sxs-lookup"><span data-stu-id="ab7ae-110">Deploy the App Service resource provider</span></span>

1. <span data-ttu-id="ab7ae-111">[Préparez l’hôte du Kit de développement Azure Stack](azure-stack-app-service-before-you-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab7ae-111">[Prepare the Azure Stack Development Kit host](azure-stack-app-service-before-you-get-started.md).</span></span> <span data-ttu-id="ab7ae-112">Cette opération inclut le déploiement du fournisseur de ressources SQL Server, qui est nécessaire pour la création de certaines applications.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-112">This includes deploying the SQL Server resource provider, which is required for creating some apps.</span></span>
2. <span data-ttu-id="ab7ae-113">[Téléchargez le programme d’installation et les scripts d’assistance](azure-stack-app-service-deploy.md#download-the-required-components).</span><span class="sxs-lookup"><span data-stu-id="ab7ae-113">[Download the installer and helper scripts](azure-stack-app-service-deploy.md#download-the-required-components).</span></span>
3. <span data-ttu-id="ab7ae-114">[Exécutez le script d’assistance pour créer des certificats nécessaires](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span><span class="sxs-lookup"><span data-stu-id="ab7ae-114">[Run the helper script to create required certificates](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack).</span></span>
4. <span data-ttu-id="ab7ae-115">[Installez le fournisseur de ressources App Service](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack). (Plusieurs heures sont nécessaires pour effectuer l’installation et afficher tous les rôles de travail.)</span><span class="sxs-lookup"><span data-stu-id="ab7ae-115">[Install the App Service resource provider](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (it will take a couple hours to install and for all the worker roles to appear).</span></span>
5. <span data-ttu-id="ab7ae-116">[Validez l’installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span><span class="sxs-lookup"><span data-stu-id="ab7ae-116">[Validate the installation](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="ab7ae-117">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-117">Create an offer</span></span>

<span data-ttu-id="ab7ae-118">Vous pouvez créer une offre qui, par exemple, permet aux utilisateurs de créer des systèmes de gestion de contenu web DNN.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-118">As an example, you can create an offer that lets users create DNN web content management systems.</span></span> <span data-ttu-id="ab7ae-119">Cette opération nécessite le service SQL Server que vous est déjà activé en installant le fournisseur de ressources SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-119">It requires the SQL Server service which you already enabled by installing the SQL Server resource provider.</span></span>

1.  <span data-ttu-id="ab7ae-120">[Définissez un quota](azure-stack-setting-quotas.md) et nommez-le *AppServiceQuota*.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-120">[Set a quota](azure-stack-setting-quotas.md) and name it *AppServiceQuota*.</span></span> <span data-ttu-id="ab7ae-121">Sélectionnez **Microsoft.Web** pour le champ **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-121">Select **Microsoft.Web** for the **Namespace** field.</span></span>
2.  <span data-ttu-id="ab7ae-122">[Créez un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="ab7ae-122">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="ab7ae-123">Nommez-le *TestAppServicePlan*, puis sélectionnez le service **Microsoft.SQL** et le quota **AppService Quota**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-123">Name it *TestAppServicePlan*, select the the **Microsoft.SQL** service, and **AppService Quota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab7ae-124">Pour permettre aux utilisateurs de créer d’autres applications, il est possible que d’autres services soient exigés dans le plan.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-124">To let users create other apps, other services might be required in the plan.</span></span> <span data-ttu-id="ab7ae-125">Par exemple, Azure Functions exige que le plan inclue le service **Microsoft.Storage**, tandis que Wordpress exige **Microsoft.MySQL**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-125">For example, Azure Functions requires that the plan     include the **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQL**.</span></span>
    > 
    >

3.  <span data-ttu-id="ab7ae-126">[Créez une offre](azure-stack-create-offer.md), nommez-la **TestAppServiceOffer**, puis sélectionnez le plan **TestAppServicePlan**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-126">[Create an offer](azure-stack-create-offer.md), name it **TestAppServiceOffer** and select the **TestAppServicePlan** plan.</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="ab7ae-127">Tester l’offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-127">Test the offer</span></span>

<span data-ttu-id="ab7ae-128">Maintenant que vous avez déployé le fournisseur de ressources App Service et créé une offre, vous pouvez vous connecter en tant qu’utilisateur, vous abonner à l’offre, puis créer une application.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-128">Now that you've deployed the App Service resource provider and created an offer, you can sign in as a user, subscribe to the offer, and create an app.</span></span> <span data-ttu-id="ab7ae-129">Pour cet exemple, nous allons créer un système de gestion de contenu de plateforme DNN.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-129">For this example, we'll create a DNN Platform content management system.</span></span> <span data-ttu-id="ab7ae-130">Vous devez d’abord créer une base de données SQL, puis l’application web DNN.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-130">You must first create a SQL database and then the DNN web app.</span></span>

### <a name="subscribe-to-the-offer"></a><span data-ttu-id="ab7ae-131">S’abonner à l’offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-131">Subscribe to the offer</span></span>
1. <span data-ttu-id="ab7ae-132">Connectez-vous au portail Azure Stack (https://portal.local.azurestack.external) en tant que locataire.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-132">Sign in to the Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="ab7ae-133">Cliquez sur **Prendre un abonnement** > tapez **TestAppServiceSubscription** sous **’** > **Sélectionner une offre** > **TestAppServiceOffer** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-133">Click **Get a subscription** > type **TestAppServiceSubscription** under **Display Name** > **Select an offer** > **TestAppServiceOffer** > **Create**.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="ab7ae-134">Créer une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ab7ae-134">Create a SQL database</span></span>

1. <span data-ttu-id="ab7ae-135">Cliquez sur **+** > **Données et stockage** > **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-135">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="ab7ae-136">Conservez les valeurs par défaut pour les champs, sauf pour ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ab7ae-136">Leave the defaults for the fields, except as follows:</span></span>
    - <span data-ttu-id="ab7ae-137">**Nom de la base de données** : DNNdb</span><span class="sxs-lookup"><span data-stu-id="ab7ae-137">**Database Name**: DNNdb</span></span>
    - <span data-ttu-id="ab7ae-138">**Taille maximale (en Mo)** : 100</span><span class="sxs-lookup"><span data-stu-id="ab7ae-138">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="ab7ae-139">**Abonnement**: TestAppServiceOffer</span><span class="sxs-lookup"><span data-stu-id="ab7ae-139">**Subscription**: TestAppServiceOffer</span></span>
    - <span data-ttu-id="ab7ae-140">**Groupe de ressources** : DNN-RG</span><span class="sxs-lookup"><span data-stu-id="ab7ae-140">**Resource Group**: DNN-RG</span></span>
3. <span data-ttu-id="ab7ae-141">Cliquez sur **Paramètres de connexion**, entrez les informations d’identification pour la base de données, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-141">Click **Login Settings**, enter credentials for the database, and then click **OK**.</span></span> <span data-ttu-id="ab7ae-142">Vous allez utiliser ces informations d’identification plus tard dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-142">You'll use these credentials later in these steps.</span></span>
4. <span data-ttu-id="ab7ae-143">Cliquez sur **Référence** > sélectionnez le SKU SQL que vous avez créé pour le serveur d’hébergement SQL > **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-143">Click **SKU** > select the SQL SKU that you created for the SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="ab7ae-144">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-144">Click **Create**.</span></span>

### <a name="create-a-dnn-app"></a><span data-ttu-id="ab7ae-145">Créer une application DNN</span><span class="sxs-lookup"><span data-stu-id="ab7ae-145">Create a DNN app</span></span>    

1. <span data-ttu-id="ab7ae-146">Cliquez sur **+** > **Afficher tout** > **Aperçu de la plateforme DNN** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-146">Click **+** > **See all** > **DNN Platform preview** > **Create**.</span></span>
2. <span data-ttu-id="ab7ae-147">Tapez *DNNapp* sous **Nom de l’application**, puis sélectionnez **TestAppServiceOffer** sous **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-147">Type *DNNapp* under **App name** and select **TestAppServiceOffer** under **Subscription**.</span></span>
3. <span data-ttu-id="ab7ae-148">Cliquez sur **Configurer les paramètres obligatoires** > **Créer** > tapez un nom de**Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-148">Click **Configure required settings** > **Create New** > type an **App Service plan** name.</span></span>
4. <span data-ttu-id="ab7ae-149">Cliquez sur **Niveau tarifaire** > **F1 Gratuit** > **Sélectionner** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-149">Click **Pricing tier** > **F1 Free** > **Select** > **OK**.</span></span>
5. <span data-ttu-id="ab7ae-150">Cliquez sur **Base de données**, puis entrez les informations relatives à la base de données SQL créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-150">Click **Database** and enter the information for the SQL database you created earlier.</span></span>
6. <span data-ttu-id="ab7ae-151">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ab7ae-151">Click **Create**.</span></span>

<span data-ttu-id="ab7ae-152">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="ab7ae-152">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab7ae-153">Déployer le fournisseur de ressources App Service</span><span class="sxs-lookup"><span data-stu-id="ab7ae-153">Deploy the App Service resource provider</span></span>
> * <span data-ttu-id="ab7ae-154">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-154">Create an offer</span></span>
> * <span data-ttu-id="ab7ae-155">Tester l’offre</span><span class="sxs-lookup"><span data-stu-id="ab7ae-155">Test the offer</span></span>

<span data-ttu-id="ab7ae-156">Passez au didacticiel suivant pour savoir comment :</span><span class="sxs-lookup"><span data-stu-id="ab7ae-156">Advance to the next tutorial to learn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab7ae-157">Déployer des applications sur Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ab7ae-157">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
