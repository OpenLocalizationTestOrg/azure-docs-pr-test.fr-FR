---
title: aaaCreate un compte Batch Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment toocreate un traitement par lots Azure compte Bonjour toorun portail Azure, les charges de travail parallèles à grande échelle dans le cloud de hello"
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
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a><span data-ttu-id="014e0-103">Créer un compte de traitement par lots avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="014e0-103">Create a Batch account with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="014e0-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="014e0-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="014e0-105">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="014e0-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
>
>

<span data-ttu-id="014e0-106">Découvrez comment toocreate un traitement par lots Azure compte Bonjour [portail Azure][azure_portal], puis choisissez les propriétés de compte hello qui correspondent à votre scénario de calcul.</span><span class="sxs-lookup"><span data-stu-id="014e0-106">Learn how toocreate an Azure Batch account in hello [Azure portal][azure_portal], and choose hello account properties that fit your compute scenario.</span></span> <span data-ttu-id="014e0-107">Découvrez où les propriétés du compte important toofind que les clés d’accès et les URL de compte.</span><span class="sxs-lookup"><span data-stu-id="014e0-107">Learn where toofind important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="014e0-108">Pour plus d’informations sur les comptes de traitement par lots et les scénarios, consultez hello [vue d’ensemble des fonctionnalités](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="014e0-108">For background about Batch accounts and scenarios, see hello [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="014e0-109">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-109">Create a Batch account</span></span>

<span data-ttu-id="014e0-110">Utiliser toocreate de portail hello un compte Batch de hello deux *les modes d’allocation de pool*: **lot service** mode ou plus récente de hello **abonnement utilisateur** mode, ce qui requiert plus de configuration.</span><span class="sxs-lookup"><span data-stu-id="014e0-110">Use hello portal toocreate a Batch account in one of hello two *pool allocation modes*: **Batch service** mode or hello newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="014e0-111">Pour plus d’informations sur ces deux modes, consultez hello [vue d’ensemble des fonctionnalités](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="014e0-111">For information about these two modes, see hello [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="014e0-112">Pour les fonctionnalités du mode d’abonnement utilisateur hello, voir aussi hello [billet de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="014e0-112">For features of hello user subscription mode, see also hello [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="014e0-113">Mode service Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-113">Batch service mode</span></span>



1. <span data-ttu-id="014e0-114">Connectez-vous à toohello [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="014e0-114">Sign in toohello [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="014e0-115">Cliquez sur **Nouveau** > **Calcul** > **Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="014e0-115">Click **New** > **Compute** > **Batch Service**.</span></span>

    ![Traitement par lots dans hello Marketplace][marketplace_portal]
3. <span data-ttu-id="014e0-117">Hello **compte Batch** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="014e0-117">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="014e0-118">Consultez les descriptions de hello ci-dessous de chaque élément du panneau.</span><span class="sxs-lookup"><span data-stu-id="014e0-118">See hello descriptions below of each blade element.</span></span>

    ![Création d’un compte Batch][account_portal]

    <span data-ttu-id="014e0-120">a.</span><span class="sxs-lookup"><span data-stu-id="014e0-120">a.</span></span> <span data-ttu-id="014e0-121">**Nom du compte**: nom du compte Batch hello vous choisissez doit être unique dans hello région Azure où le compte de hello est créée (voir **emplacement** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="014e0-121">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="014e0-122">nom du compte Hello peut contenir uniquement des caractères en minuscules ou des nombres et doit être de longueur 3 et 24 caractères.</span><span class="sxs-lookup"><span data-stu-id="014e0-122">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="014e0-123">b.</span><span class="sxs-lookup"><span data-stu-id="014e0-123">b.</span></span> <span data-ttu-id="014e0-124">**Abonnement**: hello abonnement dans le hello toocreate compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-124">**Subscription**: hello subscription in which toocreate hello Batch account.</span></span> <span data-ttu-id="014e0-125">Si vous n’avez qu’un seul abonnement, il est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="014e0-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="014e0-126">c.</span><span class="sxs-lookup"><span data-stu-id="014e0-126">c.</span></span> <span data-ttu-id="014e0-127">**Mode d’allocation de pool** : sélectionnez **Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="014e0-127">**Pool allocation mode**: Select **Batch service**.</span></span>

    <span data-ttu-id="014e0-128">c.</span><span class="sxs-lookup"><span data-stu-id="014e0-128">c.</span></span> <span data-ttu-id="014e0-129">**Groupe de ressources** : sélectionnez un groupe de ressources pour votre nouveau compte Batch (vous pouvez également en créer un).</span><span class="sxs-lookup"><span data-stu-id="014e0-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="014e0-130">d.</span><span class="sxs-lookup"><span data-stu-id="014e0-130">d.</span></span> <span data-ttu-id="014e0-131">**Emplacement**: hello région Azure dans le hello toocreate compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-131">**Location**: hello Azure region in which toocreate hello Batch account.</span></span> <span data-ttu-id="014e0-132">Seules les régions hello pris en charge par votre abonnement et le groupe de ressources sont affichées en tant qu’options.</span><span class="sxs-lookup"><span data-stu-id="014e0-132">Only hello regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="014e0-133">e.</span><span class="sxs-lookup"><span data-stu-id="014e0-133">e.</span></span> <span data-ttu-id="014e0-134">**Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="014e0-135">Cela est recommandé pour la plupart des comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="014e0-136">Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) disponible plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="014e0-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="014e0-137">Cliquez sur **créer** compte de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="014e0-137">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="014e0-138">portail de Hello indique que le déploiement est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="014e0-138">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="014e0-139">Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="014e0-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>

## <a name="user-subscription-mode"></a><span data-ttu-id="014e0-140">Mode Abonnement utilisateur</span><span class="sxs-lookup"><span data-stu-id="014e0-140">User subscription mode</span></span>

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a><span data-ttu-id="014e0-141">Autoriser Azure Batch tooaccess l’abonnement hello (opération à usage unique)</span><span class="sxs-lookup"><span data-stu-id="014e0-141">Allow Azure Batch tooaccess hello subscription (one-time operation)</span></span>
<span data-ttu-id="014e0-142">Lorsque vous créez votre premier compte Batch en mode d’abonnement utilisateur, effectuer hello suivant les étapes tooregister votre abonnement avec le lot.</span><span class="sxs-lookup"><span data-stu-id="014e0-142">When creating your first Batch account in user subscription mode, perform hello following steps tooregister your subscription with Batch.</span></span> <span data-ttu-id="014e0-143">(Si vous avez effectué précédemment cette, ignorer toohello la prochaine section.)</span><span class="sxs-lookup"><span data-stu-id="014e0-143">(If you previously did this, skip toohello next section.)</span></span>

1. <span data-ttu-id="014e0-144">Connectez-vous à toohello [portail Azure][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="014e0-144">Sign in toohello [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="014e0-145">Cliquez sur **plus Services** > **abonnements**, cliquez sur l’abonnement hello souhaité toouse pour hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-145">Click **More Services** > **Subscriptions**, and click hello subscription you want toouse for hello Batch account.</span></span>

3. <span data-ttu-id="014e0-146">Bonjour **abonnement** panneau, cliquez sur **(IAM) de contrôle d’accès** > **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="014e0-146">In hello **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Contrôle d’accès à l’abonnement][subscription_access]

4. <span data-ttu-id="014e0-148">Sur hello **ajouter des autorisations** panneau, sélectionnez hello **collaborateur** rôle, recherchez hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="014e0-148">On hello **Add permissions** blade, select hello **Contributor** role, search for hello Batch API.</span></span> <span data-ttu-id="014e0-149">Recherche de chacune de ces chaînes jusqu'à ce que vous trouviez hello API :</span><span class="sxs-lookup"><span data-stu-id="014e0-149">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="014e0-150">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="014e0-150">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="014e0-151">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="014e0-151">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="014e0-152">Les locataires Azure AD les plus récents peuvent utiliser ce nom.</span><span class="sxs-lookup"><span data-stu-id="014e0-152">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="014e0-153">**ddbf3205-c6bd-46AE-8127-60eb93363864** ID de hello pour hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="014e0-153">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 

5. <span data-ttu-id="014e0-154">Une fois que vous trouvez hello API de lot, sélectionnez-la, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="014e0-154">Once you find hello Batch API, select it and click **Save**.</span></span>

    ![Ajouter des autorisations Batch][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="014e0-156">Création d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="014e0-156">Create a key vault</span></span>
<span data-ttu-id="014e0-157">Mode d’utilisateur abonnement, un coffre de clés Azure est requis qui appartient toothe même groupe de ressources que hello lot compte toobe est créé.</span><span class="sxs-lookup"><span data-stu-id="014e0-157">In user subscription mode, an Azure key vault is required that belongs toothe same resource group as hello Batch account toobe created.</span></span> <span data-ttu-id="014e0-158">Assurez-vous que le groupe de ressources hello est dans une région où le lot est [disponible](https://azure.microsoft.com/regions/services/) et qui prend en charge de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="014e0-158">Make sure hello resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="014e0-159">Bonjour [portail Azure][azure_portal], cliquez sur **nouveau** > **sécurité + identité** > **le coffre de clés** .</span><span class="sxs-lookup"><span data-stu-id="014e0-159">In hello [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span>

2. <span data-ttu-id="014e0-160">Bonjour **créer un coffre de clés** panneau, entrez un nom pour le coffre de clés hello et créer un groupe de ressources dans la région de hello souhaité pour votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-160">In hello **Create Key Vault** blade, enter a name for hello key vault, and create a resource group in hello region you want for your Batch account.</span></span> <span data-ttu-id="014e0-161">Laissez hello restant les valeurs par défaut des paramètres, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="014e0-161">Leave hello remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="014e0-162">Création d’un compte Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-162">Create a Batch account</span></span>

1. <span data-ttu-id="014e0-163">Bonjour [portail Azure][azure_portal], cliquez sur **nouveau** > **de calcul** > **le Service Batch**.</span><span class="sxs-lookup"><span data-stu-id="014e0-163">In hello [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>

    ![Traitement par lots dans hello Marketplace][marketplace_portal]
3. <span data-ttu-id="014e0-165">Hello **compte Batch** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="014e0-165">hello **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="014e0-166">Consultez les descriptions de hello ci-dessous de chaque élément du panneau.</span><span class="sxs-lookup"><span data-stu-id="014e0-166">See hello descriptions below of each blade element.</span></span>

    ![Création d’un compte Batch][account_portal_byos]

    <span data-ttu-id="014e0-168">a.</span><span class="sxs-lookup"><span data-stu-id="014e0-168">a.</span></span> <span data-ttu-id="014e0-169">**Nom du compte**: nom du compte Batch hello vous choisissez doit être unique dans hello région Azure où le compte de hello est créée (voir **emplacement** ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="014e0-169">**Account name**: hello Batch account name you choose must be unique within hello Azure region where hello account is created (see **Location** below).</span></span> <span data-ttu-id="014e0-170">nom du compte Hello peut contenir uniquement des caractères en minuscules ou des nombres et doit être de longueur 3 et 24 caractères.</span><span class="sxs-lookup"><span data-stu-id="014e0-170">hello account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="014e0-171">b.</span><span class="sxs-lookup"><span data-stu-id="014e0-171">b.</span></span> <span data-ttu-id="014e0-172">**Abonnement**: Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous avez enregistré avec hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-172">**Subscription**: If you have more than one subscription, select hello subscription that you registered with hello Batch service.</span></span>

    <span data-ttu-id="014e0-173">c.</span><span class="sxs-lookup"><span data-stu-id="014e0-173">c.</span></span> <span data-ttu-id="014e0-174">**Mode d’allocation de pool** : sélectionnez **Abonnement utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="014e0-174">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="014e0-175">d.</span><span class="sxs-lookup"><span data-stu-id="014e0-175">d.</span></span> <span data-ttu-id="014e0-176">**Coffre de clés**: coffre de clés hello sélectionnez vous avez créé pour votre compte Batch dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="014e0-176">**Key vault**: Select hello key vault you created for your Batch account in hello previous section.</span></span> <span data-ttu-id="014e0-177">Vous pouvez éventuellement créer un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="014e0-177">Optionally, create a new key vault.</span></span> <span data-ttu-id="014e0-178">Après avoir sélectionné le coffre de hello, sélectionnez hello case à cocher toogrant Azure Batch accès toohello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="014e0-178">After selecting hello vault, select hello checkbox toogrant Azure Batch access toohello key vault.</span></span>

    <span data-ttu-id="014e0-179">c.</span><span class="sxs-lookup"><span data-stu-id="014e0-179">c.</span></span> <span data-ttu-id="014e0-180">**Groupe de ressources**: groupe de ressources sélectionnez hello dans lequel vous avez créé le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="014e0-180">**Resource group**: Select hello resource group in which you  created hello key vault.</span></span>

    <span data-ttu-id="014e0-181">d.</span><span class="sxs-lookup"><span data-stu-id="014e0-181">d.</span></span> <span data-ttu-id="014e0-182">**Emplacement**: hello région Azure dans lequel vous avez créé le coffre de clés hello pour le compte de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="014e0-182">**Location**: hello Azure region in which you created hello key vault for hello Batch account.</span></span>

    <span data-ttu-id="014e0-183">e.</span><span class="sxs-lookup"><span data-stu-id="014e0-183">e.</span></span> <span data-ttu-id="014e0-184">**Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-184">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="014e0-185">Cela est recommandé pour la plupart des comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-185">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="014e0-186">Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="014e0-186">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="014e0-187">Cliquez sur **créer** compte de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="014e0-187">Click **Create** toocreate hello account.</span></span>

   <span data-ttu-id="014e0-188">portail de Hello indique que le déploiement est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="014e0-188">hello portal indicates deployment is in progress.</span></span> <span data-ttu-id="014e0-189">Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="014e0-189">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="014e0-190">Afficher les propriétés du compte Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-190">View Batch account properties</span></span>
<span data-ttu-id="014e0-191">Une fois que le compte de hello a été créé, vous pouvez ouvrir hello **Panneau de compte Batch** tooaccess ses paramètres et les propriétés.</span><span class="sxs-lookup"><span data-stu-id="014e0-191">Once hello account has been created, you can open hello **Batch account blade** tooaccess its settings and properties.</span></span> <span data-ttu-id="014e0-192">Vous pouvez accéder tous les paramètres de compte et les propriétés à l’aide du menu de gauche hello du Panneau de compte de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="014e0-192">You can access all account settings and properties by using hello left menu of hello Batch account blade.</span></span>

![Panneau de compte Batch dans le portail Azure][account_blade]

* <span data-ttu-id="014e0-194">**URL du compte de traitement par lots**: lorsque vous développez une application avec hello [API de lot](batch-apis-tools.md#azure-accounts-for-batch-development), vous aurez besoin de vos ressources de traitement par lots une tooaccess URL de compte.</span><span class="sxs-lookup"><span data-stu-id="014e0-194">**Batch account URL**: When you develop an application with hello [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you'll need an account URL tooaccess your Batch resources.</span></span> <span data-ttu-id="014e0-195">Une URL de compte de traitement par lots a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="014e0-195">A Batch account URL has hello following format:</span></span>

    `https://<account_name>.<region>.batch.azure.com`

![URL de compte Batch dans le portail][account_url]

* <span data-ttu-id="014e0-197">**Clés d’accès** (mode de service de lot) : tooauthenticate accès tooyour compte Batch à partir de votre application, vous aurez besoin d’une clé d’accès de compte.</span><span class="sxs-lookup"><span data-stu-id="014e0-197">**Access keys** (Batch service mode): tooauthenticate access tooyour Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="014e0-198">(Ce paramètre n’est pas disponible en mode Abonnement utilisateur, dans lequel vous utilisez l’authentification Azure Active Directory.)</span><span class="sxs-lookup"><span data-stu-id="014e0-198">(This setting is not available in user subscription mode, where you use Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="014e0-199">tooview ou régénérer les clés d’accès de votre compte de traitement par lots, entrez `keys` dans le menu de gauche hello **recherche** zone sur le panneau de compte de traitement par lots hello, puis sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="014e0-199">tooview or regenerate your Batch account's access keys, enter `keys` in hello left menu **Search** box on hello Batch account blade, then select **Keys**.</span></span>

    ![Clés de compte Batch dans le portail Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="014e0-201">Compte Azure Storage lié</span><span class="sxs-lookup"><span data-stu-id="014e0-201">Linked Azure Storage account</span></span>

<span data-ttu-id="014e0-202">Vous pouvez éventuellement lier un tooyour de compte de stockage Azure à usage général du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-202">You can optionally link a general-purpose Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="014e0-203">Hello [les packages d’applications](batch-application-packages.md) fonctionnalité de traitement par lots utilise le stockage Blob Azure, comme hello [Batch fichier Conventions .NET](batch-task-output.md) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="014e0-203">hello [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does hello [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="014e0-204">Ces fonctionnalités facultatives vous aideront à déployer des applications hello qui s’exécutent de vos tâches de traitement par lots et conserver les données hello qu'elles produisent.</span><span class="sxs-lookup"><span data-stu-id="014e0-204">These optional features assist you in deploying hello applications that your Batch tasks run, and persisting hello data they produce.</span></span>

<span data-ttu-id="014e0-205">Nous vous recommandons de créer un compte de stockage dédié à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="014e0-205">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Créer un compte de stockage à usage général][storage_account]

> [!NOTE]
> <span data-ttu-id="014e0-207">Traitement par lots Azure prend actuellement en charge uniquement hello à usage général compte type de stockage.</span><span class="sxs-lookup"><span data-stu-id="014e0-207">Azure Batch currently supports only hello general-purpose Storage account type.</span></span> <span data-ttu-id="014e0-208">Ce type de compte est décrit à l’étape 5, [Créer un compte de stockage] (../storage/storage-create-storage-account.md#create-a-storage-account), dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="014e0-208">This account type is described in step 5, [Create a storage account] (../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

> [!WARNING]
> <span data-ttu-id="014e0-209">Soyez prudent lors de la régénération de clés d’accès hello d’un compte de stockage lié.</span><span class="sxs-lookup"><span data-stu-id="014e0-209">Be careful when regenerating hello access keys of a linked Storage account.</span></span> <span data-ttu-id="014e0-210">Régénérer la clé qu’un seul compte de stockage, puis cliquez sur **synchroniser les clés** sur hello liés au panneau de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="014e0-210">Regenerate only one Storage account key and click **Sync Keys** on hello linked Storage account blade.</span></span> <span data-ttu-id="014e0-211">Attendez cinq minutes tooallow hello clés toopropagate toohello nœuds de calcul dans vos pools, puis régénérer et synchroniser hello autre clé si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="014e0-211">Wait five minutes tooallow hello keys toopropagate toohello compute nodes in your pools, then regenerate and synchronize hello other key if necessary.</span></span> <span data-ttu-id="014e0-212">Si vous régénérez les clés à hello même temps, vos nœuds de calcul ne sera pas en mesure de toosynchronize sur les clés et compte de stockage toohello accès seront perdues.</span><span class="sxs-lookup"><span data-stu-id="014e0-212">If you regenerate both keys at hello same time, your compute nodes will not be able toosynchronize either key, and they will lose access toohello Storage account.</span></span>
>
>

<span data-ttu-id="014e0-213">![Régénération de clés de compte de stockage][4]</span><span class="sxs-lookup"><span data-stu-id="014e0-213">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="014e0-214">Quotas et limites du service Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-214">Batch service quotas and limits</span></span>
<span data-ttu-id="014e0-215">Soyez conscient que comme avec votre abonnement Azure et autres Azure services, certains [quotas et limites](batch-quota-limit.md) appliquer tooBatch comptes.</span><span class="sxs-lookup"><span data-stu-id="014e0-215">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply tooBatch accounts.</span></span> <span data-ttu-id="014e0-216">Les quotas pour un compte de traitement par lots actuels s’affichent dans le portail hello dans le compte de hello **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="014e0-216">Current quotas for a Batch account appear in hello portal in hello account **Properties**.</span></span>

![Quotas de compte Batch dans le portail Azure][quotas]



<span data-ttu-id="014e0-218">En outre, la plupart de ces quotas peuvent être augmentées simplement avec une demande de support gratuit soumise Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="014e0-218">Additionally, many of these quotas can be increased simply with a free product support request submitted in hello Azure portal.</span></span> <span data-ttu-id="014e0-219">Consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour plus d’informations sur la demande d’augmentation du quota.</span><span class="sxs-lookup"><span data-stu-id="014e0-219">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="014e0-220">Autres options de gestion de comptes Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-220">Other Batch account management options</span></span>
<span data-ttu-id="014e0-221">En outre toousing hello portail Azure, vous pouvez également créer et gérer les comptes de traitement par lots avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="014e0-221">In addition toousing hello Azure portal, you can also create and manage Batch accounts with hello following:</span></span>

* [<span data-ttu-id="014e0-222">Applets de commande PowerShell pour Batch</span><span class="sxs-lookup"><span data-stu-id="014e0-222">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="014e0-223">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="014e0-223">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="014e0-224">Gestion de lots .NET</span><span class="sxs-lookup"><span data-stu-id="014e0-224">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="014e0-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="014e0-225">Next steps</span></span>
* <span data-ttu-id="014e0-226">Consultez hello [vue d’ensemble de lot](batch-api-basics.md) toolearn plus d’informations sur les fonctionnalités et les concepts du service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="014e0-226">See hello [Batch feature overview](batch-api-basics.md) toolearn more about Batch service concepts and features.</span></span> <span data-ttu-id="014e0-227">Hello article traite des ressources de traitement principales hello tels que les pools, les nœuds de calcul, les opérations et les tâches et fournit une vue d’ensemble de hello les fonctionnalités du service qui permettent l’exécution de la charge de travail de calcul à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="014e0-227">hello article discusses hello primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of hello service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="014e0-228">Principes fondamentaux du développement d’une application activée de lot à l’aide de hello hello [bibliothèque cliente .NET de lot](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="014e0-228">Learn hello basics of developing a Batch-enabled application using hello [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="014e0-229">Ces articles d’introduction vous guident dans une application opérationnelle qui utilise hello lot service tooexecute une charge de travail sur plusieurs nœuds de calcul et inclut l’utilisation du stockage Azure pour la récupération et de mise en attente du fichier de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="014e0-229">These introductory articles guide you through a working application that uses hello Batch service tooexecute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

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
