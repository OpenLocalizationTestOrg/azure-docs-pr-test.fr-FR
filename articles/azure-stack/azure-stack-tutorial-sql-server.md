---
title: "aaaMake SQL des bases de données utilisateurs d’Azure pile disponible tooyour | Documents Microsoft"
description: "Didacticiel tooinstall hello du fournisseur de ressources SQL Server et créer des offres qui permettent de créer des bases de données SQL Azure pile utilisateurs."
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
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a><span data-ttu-id="f7ce8-103">Rendre les bases de données SQL utilisateurs d’Azure pile tooyour disponibles</span><span class="sxs-lookup"><span data-stu-id="f7ce8-103">Make SQL databases available tooyour Azure Stack users</span></span>

<span data-ttu-id="f7ce8-104">En tant qu’administrateur de cloud Azure Stack, vous pouvez créer des offres qui permettent aux utilisateurs de créer des bases de données SQL qu’ils peuvent utiliser avec leurs applications cloud natives, sites web et charges de travail.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-104">As an Azure Stack cloud administrator, you can create offers that let your users (tenants) create SQL databases that they can use with their cloud-native apps, websites, and workloads.</span></span> <span data-ttu-id="f7ce8-105">En fournissant ces personnalisé, à la demande, les utilisateurs de bases de données en nuage tooyour, vous pouvez enregistrer les temps et des ressources.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-105">By providing these custom, on-demand, cloud-based databases tooyour users, you can save them time and resources.</span></span> <span data-ttu-id="f7ce8-106">tooset cet accès, vous allez :</span><span class="sxs-lookup"><span data-stu-id="f7ce8-106">tooset this up, you will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f7ce8-107">Déployer le fournisseur de ressources SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="f7ce8-107">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="f7ce8-108">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="f7ce8-108">Create an offer</span></span>
> * <span data-ttu-id="f7ce8-109">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="f7ce8-109">Test hello offer</span></span>

## <a name="deploy-hello-sql-server-resource-provider"></a><span data-ttu-id="f7ce8-110">Déployer le fournisseur de ressources SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="f7ce8-110">Deploy hello SQL Server resource provider</span></span>

<span data-ttu-id="f7ce8-111">processus de déploiement Hello est décrit en détail dans hello [bases de données SQL d’utilisation sur un article de la pile de Azure](azure-stack-sql-resource-provider-deploy.md)et est composé de hello principal comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7ce8-111">hello deployment process is described in detail in hello [Use SQL databases on Azure Stack article](azure-stack-sql-resource-provider-deploy.md), and is comprised of hello following primary steps:</span></span>

1.  <span data-ttu-id="f7ce8-112">[Déployer le fournisseur de ressources SQL hello]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span><span class="sxs-lookup"><span data-stu-id="f7ce8-112">[Deploy hello SQL resource provider]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider).</span></span>
2.  <span data-ttu-id="f7ce8-113">[Vérifier le déploiement de hello]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span><span class="sxs-lookup"><span data-stu-id="f7ce8-113">[Verify hello deployment]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal).</span></span>
3.  <span data-ttu-id="f7ce8-114">[Fournir une capacité en vous connectant tooa hébergeant SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span><span class="sxs-lookup"><span data-stu-id="f7ce8-114">[Provide capacity by connecting tooa hosting SQL server]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="f7ce8-115">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="f7ce8-115">Create an offer</span></span>

1.  <span data-ttu-id="f7ce8-116">[Définissez un quota](azure-stack-setting-quotas.md) et nommez-le *SQLServerQuota*.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-116">[Set a quota](azure-stack-setting-quotas.md) and name it *SQLServerQuota*.</span></span> <span data-ttu-id="f7ce8-117">Sélectionnez **Microsoft.SQLAdapter** pour hello **Namespace** champ.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-117">Select **Microsoft.SQLAdapter** for hello **Namespace** field.</span></span>
2.  <span data-ttu-id="f7ce8-118">[Créer un plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="f7ce8-118">[Create a plan](azure-stack-create-plan.md).</span></span> <span data-ttu-id="f7ce8-119">Nommez-le *TestSQLServerPlan*, sélectionnez hello **Microsoft.SQLAdapter** service, et **SQLServerQuota** quota.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-119">Name it *TestSQLServerPlan*, select hello **Microsoft.SQLAdapter** service, and **SQLServerQuota** quota.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f7ce8-120">toolet utilisateurs créer d’autres applications, d’autres services peuvent être nécessaires dans le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-120">toolet users create other apps, other services might be required in hello plan.</span></span> <span data-ttu-id="f7ce8-121">Par exemple, les fonctions Azure requiert ce plan hello inclure hello **Microsoft.Storage** de service, tandis que Wordpress requiert **Microsoft.MySQLAdapter**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-121">For example, Azure Functions requires that hello plan include hello **Microsoft.Storage** service, while Wordpress requires **Microsoft.MySQLAdapter**.</span></span>
    > 
    >

3.  <span data-ttu-id="f7ce8-122">[Créer une offre](azure-stack-create-offer.md), nommez-le **TestSQLServerOffer** et sélectionnez hello **TestSQLServerPlan** plan.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-122">[Create an offer](azure-stack-create-offer.md), name it **TestSQLServerOffer** and select hello **TestSQLServerPlan** plan.</span></span>

## <a name="test-hello-offer"></a><span data-ttu-id="f7ce8-123">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="f7ce8-123">Test hello offer</span></span>

<span data-ttu-id="f7ce8-124">Maintenant que vous avez déployé le fournisseur de ressources SQL Server hello et créé une offre, vous pouvez vous connecter en tant qu’utilisateur, s’abonner toohello offre et créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-124">Now that you've deployed hello SQL Server resource provider and created an offer, you can sign in as a user, subscribe toohello offer, and create a database.</span></span>

### <a name="subscribe-toohello-offer"></a><span data-ttu-id="f7ce8-125">S’abonner toohello offre</span><span class="sxs-lookup"><span data-stu-id="f7ce8-125">Subscribe toohello offer</span></span>
1. <span data-ttu-id="f7ce8-126">Se connecter toohello le portail Azure pile (https://portal.local.azurestack.external) en tant que client.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-126">Sign in toohello Azure Stack portal (https://portal.local.azurestack.external) as a tenant.</span></span>
2. <span data-ttu-id="f7ce8-127">Cliquez sur **Prendre un abonnement**, puis tapez **TestSQLServerSubscription** sous **Nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-127">Click **Get a subscription** and then type **TestSQLServerSubscription** under **Display Name**.</span></span>
3. <span data-ttu-id="f7ce8-128">Cliquez sur **Sélectionner une offre** > **TestSQLServerOffer** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-128">Click **Select an offer** > **TestSQLServerOffer** > **Create**.</span></span>
4. <span data-ttu-id="f7ce8-129">Cliquez sur **Plus de services** > **Abonnements** > **TestSQLServerSubscription** > **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-129">Click **More services** > **Subscriptions** > **TestSQLServerSubscription** > **Resource providers**.</span></span>
5. <span data-ttu-id="f7ce8-130">Cliquez sur **inscrire** toohello suivant **Microsoft.SQLAdapter** fournisseur.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-130">Click **Register** next toohello **Microsoft.SQLAdapter** provider.</span></span>

### <a name="create-a-sql-database"></a><span data-ttu-id="f7ce8-131">Créer une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="f7ce8-131">Create a SQL database</span></span>

1. <span data-ttu-id="f7ce8-132">Cliquez sur **+** > **Données et stockage** > **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-132">Click **+** > **Data + Storage** > **SQL Database**.</span></span>
2. <span data-ttu-id="f7ce8-133">Valeurs par défaut de congé hello pour les champs hello, ou vous peuvent utiliser ces exemples :</span><span class="sxs-lookup"><span data-stu-id="f7ce8-133">Leave hello defaults for hello fields, or you can use these examples:</span></span>
    - <span data-ttu-id="f7ce8-134">**Nom de la base de données** : SQLdb</span><span class="sxs-lookup"><span data-stu-id="f7ce8-134">**Database Name**: SQLdb</span></span>
    - <span data-ttu-id="f7ce8-135">**Taille maximale (en Mo)** : 100</span><span class="sxs-lookup"><span data-stu-id="f7ce8-135">**Max Size in MB**: 100</span></span>
    - <span data-ttu-id="f7ce8-136">**Abonnement** : TestSQLOffer</span><span class="sxs-lookup"><span data-stu-id="f7ce8-136">**Subscription**: TestSQLOffer</span></span>
    - <span data-ttu-id="f7ce8-137">**Groupe de ressources** : SQL-RG</span><span class="sxs-lookup"><span data-stu-id="f7ce8-137">**Resource Group**: SQL-RG</span></span>
3. <span data-ttu-id="f7ce8-138">Cliquez sur **les paramètres de connexion**, entrez les informations d’identification pour la base de données hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-138">Click **Login Settings**, enter credentials for hello database, and then click **OK**.</span></span>
4. <span data-ttu-id="f7ce8-139">Cliquez sur **référence (SKU)** > sélectionnez hello SKU SQL que vous avez créé pour le serveur d’hébergement SQL de hello > **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-139">Click **SKU** > select hello SQL SKU that you created for hello SQL Hosting Server > **OK**.</span></span>
5. <span data-ttu-id="f7ce8-140">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f7ce8-140">Click **Create**.</span></span>

<span data-ttu-id="f7ce8-141">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="f7ce8-141">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f7ce8-142">Déployer le fournisseur de ressources SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="f7ce8-142">Deploy hello SQL Server resource provider</span></span>
> * <span data-ttu-id="f7ce8-143">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="f7ce8-143">Create an offer</span></span>
> * <span data-ttu-id="f7ce8-144">Offre de hello de test</span><span class="sxs-lookup"><span data-stu-id="f7ce8-144">Test hello offer</span></span>

<span data-ttu-id="f7ce8-145">Comment toolearn de didacticiel suivant toohello d’avance pour :</span><span class="sxs-lookup"><span data-stu-id="f7ce8-145">Advance toohello next tutorial toolearn how to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7ce8-146">Que web, mobiles et les utilisateurs de API apps tooyour disponibles</span><span class="sxs-lookup"><span data-stu-id="f7ce8-146">Make web, mobile, and API apps available tooyour users</span></span>]( azure-stack-tutorial-app-service.md)

