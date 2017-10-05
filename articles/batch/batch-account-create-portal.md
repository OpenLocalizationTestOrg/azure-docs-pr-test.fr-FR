---
title: "Créer un compte Batch dans le portail Azure | Microsoft Docs"
description: "Apprenez à créer un compte Azure Batch dans le portail Azure pour exécuter des charges de travail parallèles à grande échelle dans le cloud"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 520d1d42d35b25db1a35d4317e9eb616cf5de565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="e6e99-103">Créer un compte Batch avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e6e99-103">Create a Batch account with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6e99-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e6e99-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="e6e99-105">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="e6e99-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="e6e99-106">Apprenez à créer un compte Azure Batch dans le [portail Azure][azure_portal] et choisissez les propriétés du compte qui correspondent à votre scénario de calcul.</span><span class="sxs-lookup"><span data-stu-id="e6e99-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="e6e99-107">Découvrez où se trouvent les propriétés du compte importantes, telles que les clés d’accès et les URL du compte.</span><span class="sxs-lookup"><span data-stu-id="e6e99-107">Learn where to find important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="e6e99-108">Pour plus d’informations sur les comptes et les scénarios Batch, consultez la [présentation des fonctionnalités](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e6e99-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="e6e99-109">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-109">Create a Batch account</span></span>

<span data-ttu-id="e6e99-110">Utilisez le portail pour créer un compte Batch dans l’un des deux *modes d’allocation de pool* : le mode**Service Batch** ou le mode plus récent **Abonnement utilisateur**, qui requiert davantage de configuration.</span><span class="sxs-lookup"><span data-stu-id="e6e99-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="e6e99-111">Pour plus d’informations sur ces deux modes, consultez la [présentation des fonctionnalités](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="e6e99-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="e6e99-112">Pour les fonctionnalités du mode Abonnement utilisateur, consultez également le [billet de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="e6e99-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="e6e99-113">Mode service Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-113">Batch service mode</span></span>



1. <span data-ttu-id="e6e99-114">Connectez-vous au [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e6e99-114">Sign in to the [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="e6e99-115">Cliquez sur **Nouveau** > **Calcul** > **Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch dans Marketplace][marketplace_portal]
3. <span data-ttu-id="e6e99-117">Le panneau **Nouveau compte Batch** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e6e99-117">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e6e99-118">Consultez les descriptions ci-dessous de chaque élément du panneau.</span><span class="sxs-lookup"><span data-stu-id="e6e99-118">See the descriptions below of each blade element.</span></span>

    ![Création d’un compte Batch][account_portal]

    <span data-ttu-id="e6e99-120">a.</span><span class="sxs-lookup"><span data-stu-id="e6e99-120">a.</span></span> <span data-ttu-id="e6e99-121">**Nom du compte** : le nom du compte Batch que vous choisissez doit être unique dans la région Azure dans laquelle le compte est créé (voir **Emplacement** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="e6e99-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="e6e99-122">Le nom de compte peut contenir uniquement des caractères minuscules ou des chiffres et doit comporter 3 à 24 caractères.</span><span class="sxs-lookup"><span data-stu-id="e6e99-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e6e99-123">b.</span><span class="sxs-lookup"><span data-stu-id="e6e99-123">b.</span></span> <span data-ttu-id="e6e99-124">**Abonnement** : l’abonnement dans lequel créer le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-124">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="e6e99-125">Si vous n’avez qu’un seul abonnement, il est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="e6e99-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="e6e99-126">c.</span><span class="sxs-lookup"><span data-stu-id="e6e99-126">c.</span></span> <span data-ttu-id="e6e99-127">**Mode d’allocation de pool** : sélectionnez **Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="e6e99-128">c.</span><span class="sxs-lookup"><span data-stu-id="e6e99-128">c.</span></span> <span data-ttu-id="e6e99-129">**Groupe de ressources** : sélectionnez un groupe de ressources pour votre nouveau compte Batch (vous pouvez également en créer un).</span><span class="sxs-lookup"><span data-stu-id="e6e99-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="e6e99-130">d.</span><span class="sxs-lookup"><span data-stu-id="e6e99-130">d.</span></span> <span data-ttu-id="e6e99-131">**Emplacement** : la région Azure dans laquelle créer le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-131">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="e6e99-132">Seules les régions prises en charge par votre abonnement et votre groupe de ressources sont affichées.</span><span class="sxs-lookup"><span data-stu-id="e6e99-132">Only the regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="e6e99-133">e.</span><span class="sxs-lookup"><span data-stu-id="e6e99-133">e.</span></span> <span data-ttu-id="e6e99-134">**Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e6e99-135">Cela est recommandé pour la plupart des comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e6e99-136">Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) disponible plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e6e99-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="e6e99-137">Cliquez sur **Créer** pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="e6e99-137">Click **Create** to create the account.</span></span>

   <span data-ttu-id="e6e99-138">Le portail indique que le déploiement est en cours.</span><span class="sxs-lookup"><span data-stu-id="e6e99-138">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="e6e99-139">Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="e6e99-140">Mode Abonnement utilisateur</span><span class="sxs-lookup"><span data-stu-id="e6e99-140">User subscription mode</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="e6e99-141">Autoriser Azure Batch à accéder à l’abonnement (opération ponctuelle)</span><span class="sxs-lookup"><span data-stu-id="e6e99-141">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="e6e99-142">Lorsque vous créez votre premier compte Batch en mode Abonnement utilisateur, procédez comme suit pour inscrire votre abonnement auprès de Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span></span> <span data-ttu-id="e6e99-143">(Si vous l’avez déjà fait, passez à la section suivante.)</span><span class="sxs-lookup"><span data-stu-id="e6e99-143">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="e6e99-144">Connectez-vous au [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="e6e99-144">Sign in to the [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="e6e99-145">Cliquez sur **Plus de services** > **Abonnements**, puis cliquez sur l’abonnement que vous souhaitez utiliser pour le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span></span>

3. <span data-ttu-id="e6e99-146">Dans le panneau **Abonnement**, cliquez sur **Contrôle d’accès (IAM)** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Contrôle d’accès à l’abonnement][subscription_access]

4. <span data-ttu-id="e6e99-148">Dans le panneau **Ajouter des autorisations**, sélectionnez le rôle **Collaborateur** et recherchez l’API Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-148">On the **Add permissions** blade, select the **Contributor** role, search for the Batch API.</span></span> <span data-ttu-id="e6e99-149">Recherchez chacune de ces chaînes, jusqu’à ce que vous trouviez l’API :</span><span class="sxs-lookup"><span data-stu-id="e6e99-149">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="e6e99-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="e6e99-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="e6e99-152">Les locataires Azure AD les plus récents peuvent utiliser ce nom.</span><span class="sxs-lookup"><span data-stu-id="e6e99-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="e6e99-153">La chaîne **ddbf3205-c6bd-46ae-8127-60eb93363864** correspond à l’ID de l’API Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 

5. <span data-ttu-id="e6e99-154">Une fois que vous avez trouvé l’API Batch, sélectionnez-la, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-154">Once you find the Batch API, select it and click **Save**.</span></span>

    ![Ajouter des autorisations Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="e6e99-156">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e6e99-156">Create a key vault</span></span>
<span data-ttu-id="e6e99-157">En mode Abonnement utilisateur, un coffre de clés Azure appartenant au même groupe de ressources que le compte Batch est requis.</span><span class="sxs-lookup"><span data-stu-id="e6e99-157">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="e6e99-158">Assurez-vous que le groupe de ressources se trouve dans une région prise en charge par votre abonnement et dans laquelle Batch est [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="e6e99-158">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="e6e99-159">Dans le [portail Azure][azure_portal], cliquez sur **Nouveau** > **Sécurité et identité** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-159">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="e6e99-160">Dans le panneau **Création d’un coffre de clés**, entrez un nom pour le coffre de clés et créez un groupe de ressources dans la région souhaitée pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-160">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="e6e99-161">Conservez les autres paramètres par défaut, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-161">Leave the remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="e6e99-162">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-162">Create a Batch account</span></span>

1. <span data-ttu-id="e6e99-163">Dans le [portail Azure][azure_portal], cliquez sur **Nouveau** > **Calcul** > **Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-163">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Batch dans Marketplace][marketplace_portal]
3. <span data-ttu-id="e6e99-165">Le panneau **Nouveau compte Batch** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e6e99-165">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="e6e99-166">Consultez les descriptions ci-dessous de chaque élément du panneau.</span><span class="sxs-lookup"><span data-stu-id="e6e99-166">See the descriptions below of each blade element.</span></span>

    ![Création d’un compte Batch][account_portal_byos]

    <span data-ttu-id="e6e99-168">a.</span><span class="sxs-lookup"><span data-stu-id="e6e99-168">a.</span></span> <span data-ttu-id="e6e99-169">**Nom du compte** : le nom du compte Batch que vous choisissez doit être unique dans la région Azure dans laquelle le compte est créé (voir **Emplacement** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="e6e99-169">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="e6e99-170">Le nom de compte peut contenir uniquement des caractères minuscules ou des chiffres et doit comporter 3 à 24 caractères.</span><span class="sxs-lookup"><span data-stu-id="e6e99-170">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="e6e99-171">b.</span><span class="sxs-lookup"><span data-stu-id="e6e99-171">b.</span></span> <span data-ttu-id="e6e99-172">**Abonnement** : si vous avez plusieurs abonnements, sélectionnez celui que vous avez inscrit auprès du service Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-172">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span></span>

    <span data-ttu-id="e6e99-173">c.</span><span class="sxs-lookup"><span data-stu-id="e6e99-173">c.</span></span> <span data-ttu-id="e6e99-174">**Mode d’allocation de pool** : sélectionnez **Abonnement utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="e6e99-175">d.</span><span class="sxs-lookup"><span data-stu-id="e6e99-175">d.</span></span> <span data-ttu-id="e6e99-176">**Coffre de clés** : sélectionnez le coffre de clés que vous avez créé pour votre compte Batch dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="e6e99-176">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span></span> <span data-ttu-id="e6e99-177">Vous pouvez éventuellement créer un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e99-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="e6e99-178">Après avoir sélectionné le coffre, activez la case à cocher pour accorder l’accès Azure Batch au coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e99-178">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span></span>

    <span data-ttu-id="e6e99-179">c.</span><span class="sxs-lookup"><span data-stu-id="e6e99-179">c.</span></span> <span data-ttu-id="e6e99-180">**Groupe de ressources** : sélectionnez le groupe de ressources dans lequel vous avez créé le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="e6e99-180">**Resource group**: Select the resource group in which you  created the key vault.</span></span>

    <span data-ttu-id="e6e99-181">d.</span><span class="sxs-lookup"><span data-stu-id="e6e99-181">d.</span></span> <span data-ttu-id="e6e99-182">**Emplacement** : région Azure dans laquelle vous avez créé le coffre de clés pour le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-182">**Location**: The Azure region in which you created the key vault for the Batch account.</span></span>

    <span data-ttu-id="e6e99-183">e.</span><span class="sxs-lookup"><span data-stu-id="e6e99-183">e.</span></span> <span data-ttu-id="e6e99-184">**Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="e6e99-185">Cela est recommandé pour la plupart des comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="e6e99-186">Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e6e99-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="e6e99-187">Cliquez sur **Créer** pour créer le compte.</span><span class="sxs-lookup"><span data-stu-id="e6e99-187">Click **Create** to create the account.</span></span>

   <span data-ttu-id="e6e99-188">Le portail indique que le déploiement est en cours.</span><span class="sxs-lookup"><span data-stu-id="e6e99-188">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="e6e99-189">Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="e6e99-190">Afficher les propriétés du compte Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-190">View Batch account properties</span></span>
<span data-ttu-id="e6e99-191">Une fois le compte créé, vous pouvez ouvrir le **Panneau du compte Batch** pour accéder à ses propriétés et paramètres.</span><span class="sxs-lookup"><span data-stu-id="e6e99-191">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span></span> <span data-ttu-id="e6e99-192">Vous avez accès à tous les paramètres et propriétés du compte dans le menu de gauche du panneau du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-192">You can access all account settings and properties by using the left menu of the Batch account blade.</span></span>

![Panneau de compte Batch dans le portail Azure][account_blade]

* <span data-ttu-id="e6e99-194">**URL de compte Batch** : lorsque vous développez une application avec des [API Batch](batch-apis-tools.md#azure-accounts-for-batch-development), vous avez besoin d’une URL de compte pour accéder aux ressources de votre Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-194">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL to access your Batch resources.</span></span> <span data-ttu-id="e6e99-195">Une URL de compte Batch a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="e6e99-195">A Batch account URL has the following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL de compte Batch dans le portail][account_url]

* <span data-ttu-id="e6e99-197">**Clés d’accès** (mode Service Batch) : pour authentifier l’accès à votre compte Batch à partir de votre application, vous avez besoin d’une clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="e6e99-197">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="e6e99-198">(Ce paramètre n’est pas disponible en mode Abonnement utilisateur, dans lequel vous utilisez l’authentification Azure Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="e6e99-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="e6e99-199">Pour afficher ou régénérer les clés d’accès de votre compte Batch, entrez `keys` dans la zone **Recherche** du menu de gauche dans le volet du compte Batch, puis sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="e6e99-199">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span></span>

    ![Clés de compte Batch dans le portail Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="e6e99-201">Compte Azure Storage lié</span><span class="sxs-lookup"><span data-stu-id="e6e99-201">Linked Azure Storage account</span></span>

<span data-ttu-id="e6e99-202">Vous pouvez éventuellement lier un compte de stockage à usage général à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-202">You can optionally link a general-purpose Azure Storage account to your Batch account.</span></span> <span data-ttu-id="e6e99-203">La fonctionnalité de [packages d’application](batch-application-packages.md) de Batch utilise le stockage Azure Blob Azure comme la bibliothèque [Batch File Conventions .NET](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="e6e99-203">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="e6e99-204">Ces fonctionnalités facultatives vous aident à déployer les applications exécutées par vos tâches Batch et à conserver les données qu’elles produisent.</span><span class="sxs-lookup"><span data-stu-id="e6e99-204">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="e6e99-205">Nous vous recommandons de créer un compte de stockage dédié à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Créer un compte de stockage à usage général][storage_account]

> [!NOTE]
> <span data-ttu-id="e6e99-207">Azure Batch prend actuellement en charge uniquement le type de compte de stockage à usage général.</span><span class="sxs-lookup"><span data-stu-id="e6e99-207">Azure Batch currently supports only the general-purpose Storage account type.</span></span> <span data-ttu-id="e6e99-208">Ce type de compte est décrit à l’étape 5, [Créer un compte de stockage] (../storage/storage-create-storage-account.md#create-a-storage-account), dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e6e99-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="e6e99-209">Soyez prudent lorsque vous régénérez les clés d’accès d’un compte de stockage lié.</span><span class="sxs-lookup"><span data-stu-id="e6e99-209">Be careful when regenerating the access keys of a linked Storage account.</span></span> <span data-ttu-id="e6e99-210">Ne régénérez qu’une clé du compte de stockage et cliquez sur **Synchroniser les clés** dans le panneau du compte de stockage lié.</span><span class="sxs-lookup"><span data-stu-id="e6e99-210">Regenerate only one Storage account key and click **Sync Keys** on the linked Storage account blade.</span></span> <span data-ttu-id="e6e99-211">Attendez cinq minutes que les clés se propagent aux nœuds de calcul de vos pools, puis régénérez et synchronisez l’autre clé si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e6e99-211">Wait five minutes to allow the keys to propagate to the compute nodes in your pools, then regenerate and synchronize the other key if necessary.</span></span> <span data-ttu-id="e6e99-212">Si vous régénérez les deux clés en même temps, les nœuds de calcul ne pourront pas les synchroniser, car elles perdront l’accès au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e6e99-212">If you regenerate both keys at the same time, your compute nodes will not be able to synchronize either key, and they will lose access to the Storage account.</span></span>
>
>

<span data-ttu-id="e6e99-213">![Régénération de clés de compte de stockage][4]</span><span class="sxs-lookup"><span data-stu-id="e6e99-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="e6e99-214">Quotas et limites du service Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-214">Batch service quotas and limits</span></span>
<span data-ttu-id="e6e99-215">Sachez qu’à l’image de votre abonnement Azure et d’autres services Azure, certains [quotas et limites](batch-quota-limit.md) s’appliquent aux comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e6e99-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span></span> <span data-ttu-id="e6e99-216">Les quotas actuels d’un compte Batch sont indiqués dans les **propriétés**du compte sur le portail.</span><span class="sxs-lookup"><span data-stu-id="e6e99-216">Current quotas for a Batch account appear in the portal in the account **Properties**.</span></span>

![Quotas de compte Batch dans le portail Azure][quotas]



<span data-ttu-id="e6e99-218">De plus, il est possible de relever la plupart de ces quotas simplement en envoyant une demande de support produit gratuit dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e99-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span></span> <span data-ttu-id="e6e99-219">Pour plus d’informations sur les demandes d’augmentation de quotas, consultez [Quotas et limites pour le service Azure Batch](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="e6e99-219">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="e6e99-220">Autres options de gestion de comptes Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-220">Other Batch account management options</span></span>
<span data-ttu-id="e6e99-221">Vous pouvez créer et gérer des comptes Batch à l’aide du portail Azure, mais aussi avec les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e6e99-221">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span></span>

* [<span data-ttu-id="e6e99-222">Applets de commande PowerShell pour Batch</span><span class="sxs-lookup"><span data-stu-id="e6e99-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="e6e99-223">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e6e99-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="e6e99-224">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="e6e99-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="e6e99-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6e99-225">Next steps</span></span>
* <span data-ttu-id="e6e99-226">Pour en savoir plus sur les concepts et fonctionnalités du service Batch, consultez [Présentation des fonctionnalités du service Batch pour les développeurs](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e6e99-226">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="e6e99-227">L’article traite des principales ressources Batch, notamment des pools, des nœuds de calcul, des travaux et des tâches et fournit une vue d’ensemble des fonctionnalités du service qui permettent l’exécution de la charge de travail de calcul à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="e6e99-227">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="e6e99-228">Découvrez les bases du développement d’une application Batch à l’aide de la [bibliothèque Azure Batch pour .NET](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e6e99-228">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="e6e99-229">Cette présentation vous décrit la création d’une application opérationnelle qui utilise le service Batch pour exécuter une charge de travail sur plusieurs nœuds de calcul, et inclut l’utilisation d’Azure Storage pour la mise en attente et la récupération de fichiers de la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="e6e99-229">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Régénération de clés de compte de stockage"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
