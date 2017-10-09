---
title: "aaaGet a démarré avec l’Explorateur de stockage (version préliminaire) | Documents Microsoft"
description: "Gérer les ressources de stockage Azure avec l’Explorateur de stockage (version préliminaire)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="19f99-103">Prise en main de l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="19f99-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="19f99-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="19f99-104">Overview</span></span>
<span data-ttu-id="19f99-105">Explorateur de stockage Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="19f99-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="19f99-106">Dans cet article, vous découvrez hello différentes manières de se connecter tooand gestion de vos comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Explorateur de stockage Microsoft Azure (version préliminaire)][15]

## <a name="prerequisites"></a><span data-ttu-id="19f99-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="19f99-108">Prerequisites</span></span>
* [<span data-ttu-id="19f99-109">Télécharger et installer l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="19f99-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="19f99-110">Connexion de compte de stockage tooa ou service</span><span class="sxs-lookup"><span data-stu-id="19f99-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="19f99-111">Explorateur de stockage (version préliminaire) offre plusieurs moyens tooconnect toostorage comptes.</span><span class="sxs-lookup"><span data-stu-id="19f99-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="19f99-112">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="19f99-112">For example, you can:</span></span>
* <span data-ttu-id="19f99-113">Se connecter toostorage les comptes associés à vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="19f99-114">Se connecter toostorage comptes et les services qui sont partagés à partir d’autres abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="19f99-115">Se connecter tooand gérer le stockage local à l’aide de hello émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="19f99-116">En outre, vous pouvez utiliser des comptes de stockage Azure à l’échelle internationale et nationale :</span><span class="sxs-lookup"><span data-stu-id="19f99-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="19f99-117">[Se connecter tooan abonnement Azure](#connect-to-an-azure-subscription): gérer les ressources de stockage qui appartiennent tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="19f99-118">[Utilisez un stockage de développement local](#work-with-local-development-storage): gérer le stockage local à l’aide de hello émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="19f99-119">[Attacher tooexternal stockage](#attach-or-detach-an-external-storage-account): gérer les ressources de stockage qui appartiennent tooanother abonnement Azure ou qui sont sous nationales clouds Azure à l’aide du compte de stockage hello nom, clé et points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="19f99-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="19f99-120">[Attacher un compte de stockage à l’aide d’un SAS](#attach-storage-account-using-sas): gérer les ressources de stockage qui appartiennent tooanother abonnement Azure à l’aide d’une signature d’accès partagé (SAS).</span><span class="sxs-lookup"><span data-stu-id="19f99-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="19f99-121">[Attachez un service à l’aide d’un SAS](#attach-service-using-sas): gérer un service de stockage spécifique (conteneur d’objets blob, file d’attente ou table) qui appartient tooanother abonnement Azure à l’aide d’un SAS.</span><span class="sxs-lookup"><span data-stu-id="19f99-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="19f99-122">Se connecter tooan abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="19f99-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="19f99-123">Si vous ne possédez pas de compte Azure, vous pouvez [vous inscrire à un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="19f99-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="19f99-124">Dans l’Explorateur de stockage (version préliminaire), sélectionnez les **paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="19f99-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![paramètres de compte Azure][0]

2. <span data-ttu-id="19f99-126">volet de gauche de Hello affiche tous les comptes de Microsoft hello que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="19f99-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="19f99-127">tooconnect tooanother compte, sélectionnez **ajouter un compte**, puis suivez toosign d’instructions hello avec un compte Microsoft associé au moins un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="19f99-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="19f99-128">Connexion toonational Azure (par exemple, Azure situés en Allemagne, Azure Government et en Chine Azure via la connexion) n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="19f99-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="19f99-129">Consultez hello » attacher ou détacher d’un compte de stockage externe « section sur la manière de tooconnect toonational des comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="19f99-130">Après avoir correctement connectez-vous avec un compte Microsoft, hello gauche volet est rempli avec hello Azure abonnements associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="19f99-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="19f99-131">Sélectionnez hello abonnements Azure que vous souhaitez toowork avec, puis sélectionnez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="19f99-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="19f99-132">(En sélectionnant **tous les abonnements** bascule en sélectionnant la totalité ou aucun de hello répertoriés abonnements Azure.)</span><span class="sxs-lookup"><span data-stu-id="19f99-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Sélectionner les abonnements Azure][3]  
    <span data-ttu-id="19f99-134">volet de gauche Hello affiche les comptes de stockage hello associées aux abonnements Azure de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="19f99-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Abonnements Azure sélectionnés][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="19f99-136">Connecter tooan Azure pile abonnement</span><span class="sxs-lookup"><span data-stu-id="19f99-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="19f99-137">Pour plus d’informations sur l’abonnement de Azure pile tooan connexion, consultez [connecter l’Explorateur de stockage tooan abonnement de Azure pile](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="19f99-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="19f99-138">Utilisation du stockage de développement local</span><span class="sxs-lookup"><span data-stu-id="19f99-138">Work with local development storage</span></span>
<span data-ttu-id="19f99-139">Avec l’Explorateur de stockage (version préliminaire), vous pouvez travailler sur le stockage local à l’aide de hello émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="19f99-140">Cette approche vous permet d’écrire du code par rapport à et stockage de test sans nécessairement disposer d’un compte de stockage déployé sur Azure, car le compte de stockage hello est émulé par hello émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="19f99-141">Hello émulateur de stockage Azure est actuellement pris en charge uniquement pour Windows.</span><span class="sxs-lookup"><span data-stu-id="19f99-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="19f99-142">Dans hello du volet de gauche de l’Explorateur de stockage (version préliminaire), développez hello **(locale et associés)** > **comptes de stockage** > **(développement)** nœud.</span><span class="sxs-lookup"><span data-stu-id="19f99-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nœud de développement local][21]

2. <span data-ttu-id="19f99-144">Si vous n’avez pas encore installé hello émulateur de stockage Azure, vous êtes invité à toodo ce via une barre d’informations.</span><span class="sxs-lookup"><span data-stu-id="19f99-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="19f99-145">Si la barre d’informations hello s’affiche, sélectionnez **version la plus récente hello téléchargement**, puis installez les émulateur hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Invite de téléchargement de l’émulateur de stockage Azure][22]

3. <span data-ttu-id="19f99-147">Une fois que l’émulateur de hello est installé, vous pouvez créer et travailler avec des objets BLOB local, les files d’attente et les tables.</span><span class="sxs-lookup"><span data-stu-id="19f99-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="19f99-148">toolearn comment toowork avec chaque compte de stockage de type, consultez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="19f99-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="19f99-149">Manage Azure blob storage resources (Gérer les ressources Azure Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="19f99-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="19f99-150">Manage Azure file share storage resources (Gérer les ressources de stockage de partage de fichiers Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="19f99-151">Manage Azure queue storage resources (Gérer les ressources de stockage File d’attente Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="19f99-152">Manage Azure table storage resources (Gérer les ressources de stockage Table Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="19f99-153">Attacher ou détacher un compte de stockage externe</span><span class="sxs-lookup"><span data-stu-id="19f99-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="19f99-154">Avec l’Explorateur de stockage (version préliminaire), vous pouvez joindre des comptes de stockage tooexternal afin que les comptes de stockage peuvent être facilement partagées.</span><span class="sxs-lookup"><span data-stu-id="19f99-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="19f99-155">Cette section explique comment tooattach too(and detach from) comptes de stockage externe.</span><span class="sxs-lookup"><span data-stu-id="19f99-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="19f99-156">Obtenir des informations d’identification de compte de stockage hello</span><span class="sxs-lookup"><span data-stu-id="19f99-156">Get hello storage account credentials</span></span>
<span data-ttu-id="19f99-157">tooshare un compte de stockage externe, propriétaire hello de ce compte doit tout d’abord obtenir les informations d’identification hello (nom de compte et de la clé) pour le compte de la hello et ensuite partager ces informations avec personne hello qui souhaite tooattach toothat (externe) compte.</span><span class="sxs-lookup"><span data-stu-id="19f99-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="19f99-158">Vous pouvez obtenir des informations d’identification du compte de stockage hello via hello portail Azure en effectuant hello des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="19f99-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="19f99-159">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19f99-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="19f99-160">Sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="19f99-160">Select **Browse**.</span></span>

3. <span data-ttu-id="19f99-161">Sélectionnez **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="19f99-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="19f99-162">Sur hello **comptes de stockage** panneau, le compte de stockage hello sélectionnez souhaité.</span><span class="sxs-lookup"><span data-stu-id="19f99-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="19f99-163">Sur hello **paramètres** panneau pour hello sélectionné compte de stockage, sélectionnez **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="19f99-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Option Clés d’accès][5]

6. <span data-ttu-id="19f99-165">Sur hello **clés d’accès** panneau, hello de copie **nom de compte de stockage** et **key1** valeurs à utiliser lors de l’attachement du compte de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="19f99-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Clés d’accès][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="19f99-167">Attacher le compte de stockage externe tooan</span><span class="sxs-lookup"><span data-stu-id="19f99-167">Attach tooan external storage account</span></span>
<span data-ttu-id="19f99-168">compte de stockage externe tooattach tooan, vous devez nom et la clé du compte hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="19f99-169">Hello « Get hello stockage compte informations d’identification » section explique comment ces valeurs à partir de tooobtain hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="19f99-170">Toutefois, dans le portail hello, clé de compte hello est appelé **key1**.</span><span class="sxs-lookup"><span data-stu-id="19f99-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="19f99-171">Par conséquent, lorsque l’Explorateur de stockage (version préliminaire) demande une clé de compte, vous entrez hello **key1** valeur.</span><span class="sxs-lookup"><span data-stu-id="19f99-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="19f99-172">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="19f99-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Option de stockage tooAzure de connexion][23]

2. <span data-ttu-id="19f99-174">Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez la clé de compte hello (hello **key1** valeur hello portail Azure), puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19f99-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="19f99-175">Vous pouvez entrer la chaîne de connexion de stockage hello à partir d’un compte de stockage sur Azure national.</span><span class="sxs-lookup"><span data-stu-id="19f99-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="19f99-176">Par exemple, comptes de stockage tooconnect tooAzure Allemagne, entrez connexion chaînes similaires toohello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="19f99-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="19f99-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="19f99-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="19f99-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="19f99-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="19f99-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="19f99-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="19f99-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="19f99-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="19f99-181">Vous pouvez obtenir la chaîne de connexion hello de hello Azure portail Bonjour même façon comme décrit dans hello section de « Obtenir les informations d’identification de compte de stockage hello ».</span><span class="sxs-lookup"><span data-stu-id="19f99-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. <span data-ttu-id="19f99-183">Bonjour **attacher un stockage externe** la boîte de dialogue hello **nom de compte** zone, entrez le nom de compte de stockage hello, spécifiez les autres paramètres de votre choisis, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19f99-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Boîte de dialogue Attacher un stockage externe][8]

4. <span data-ttu-id="19f99-185">Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="19f99-186">Si vous souhaitez toochange n’est pas défini, sélectionnez **nouveau** et réentrer les paramètres de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="19f99-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="19f99-187">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="19f99-187">Select **Connect**.</span></span>

6. <span data-ttu-id="19f99-188">Une fois connecté, le compte de stockage externe hello s’affiche avec **(externe)** ajouté toohello nom de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="19f99-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Résultat de la connexion de compte de stockage externe tooan][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="19f99-190">Détachement d’un compte de stockage externe</span><span class="sxs-lookup"><span data-stu-id="19f99-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="19f99-191">Cliquez sur le compte de stockage externe hello que vous souhaitez toodetach, puis sélectionnez **détachement**.</span><span class="sxs-lookup"><span data-stu-id="19f99-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Option Détacher d’un compte de stockage][10]

2. <span data-ttu-id="19f99-193">Dans le message de confirmation hello, sélectionnez **Oui** le détachement de hello tooconfirm à partir du compte de stockage externe hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="19f99-194">Attachement d’un compte de stockage à l’aide d’une SAP</span><span class="sxs-lookup"><span data-stu-id="19f99-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="19f99-195">Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) admin hello d’un abonnement Azure vous permet d’accorder le compte de stockage d’un accès temporaire tooa sans avoir les informations d’identification de tooprovide abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="19f99-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="19f99-196">tooillustrate ce scénario, nous allons dire que l’UtilisateurA est un administrateur d’un abonnement Azure et l’UtilisateurA veut tooallow UserB tooaccess est un stockage de compte pour une durée limitée avec certaines autorisations :</span><span class="sxs-lookup"><span data-stu-id="19f99-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="19f99-197">UserA génère un SAS (composé de chaîne de connexion de hello pour le compte de stockage hello) pour une heure spécifique période et avec des autorisations hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="19f99-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="19f99-198">L’UtilisateurA partages hello SAS hello personne (utilisateur b, dans notre exemple) souhaite que le compte de stockage toohello accès.</span><span class="sxs-lookup"><span data-stu-id="19f99-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="19f99-199">UserB utilise l’Explorateur de stockage (version préliminaire) tooattach toohello compte appartenant tooUserA à l’aide de hello fourni SAS.</span><span class="sxs-lookup"><span data-stu-id="19f99-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="19f99-200">Obtenir un SAS pour le compte hello tooshare</span><span class="sxs-lookup"><span data-stu-id="19f99-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="19f99-201">Dans l’Explorateur de stockage (version préliminaire), cliquez sur le compte de stockage hello vous souhaitez partager, puis sélectionnez **obtenir une Signature d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="19f99-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Option de menu contextuel Obtenir une signature d’accès partagé][13]

2. <span data-ttu-id="19f99-203">Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez un intervalle de temps hello et les autorisations que vous souhaitez pour le compte de hello, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="19f99-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="19f99-204">![Boîte de dialogue Obtenir une signature d’accès partagé][14]</span><span class="sxs-lookup"><span data-stu-id="19f99-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="19f99-205">Hello **Signature d’accès partagé** boîte de dialogue s’ouvre et affiche hello SAS.</span><span class="sxs-lookup"><span data-stu-id="19f99-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="19f99-206">Toohello suivant **chaîne de connexion**, sélectionnez **copie** toocopy il toohello Presse-papiers, puis sélectionnez **fermer**.</span><span class="sxs-lookup"><span data-stu-id="19f99-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="19f99-207">Attacher toohello partagé compte à l’aide de hello SAS</span><span class="sxs-lookup"><span data-stu-id="19f99-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="19f99-208">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="19f99-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Option de stockage tooAzure de connexion][23]

2. <span data-ttu-id="19f99-210">Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez la chaîne de connexion hello et sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19f99-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. <span data-ttu-id="19f99-212">Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="19f99-213">toomake change, sélectionnez **dans**, puis entrez les paramètres hello souhaités.</span><span class="sxs-lookup"><span data-stu-id="19f99-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="19f99-214">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="19f99-214">Select **Connect**.</span></span>

5. <span data-ttu-id="19f99-215">Une fois qu’il est associé, le compte de stockage hello s’affiche avec **(SAS)** ajouté toohello nom du compte que vous avez fournies.</span><span class="sxs-lookup"><span data-stu-id="19f99-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Résultat du compte tooan attaché à l’aide de SAP][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="19f99-217">Attacher un service à l’aide d’une SAP</span><span class="sxs-lookup"><span data-stu-id="19f99-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="19f99-218">section de « Liaison » un compte de stockage à l’aide d’un SAS Hello explique comment un administrateur d’abonnement Azure peut accorder le compte de stockage d’un accès temporaire tooa en générant et en partage un SAS pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="19f99-219">De la même façon, une SAP peut être générée pour un service spécifique (conteneur de blobs, file d’attente ou table) dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="19f99-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="19f99-220">Générer une SAP pour le service hello que vous souhaitez tooshare</span><span class="sxs-lookup"><span data-stu-id="19f99-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="19f99-221">Dans ce contexte, un service peut être un conteneur d’objets blob, une file d’attente ou une table.</span><span class="sxs-lookup"><span data-stu-id="19f99-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="19f99-222">toogenerate hello SAS pour un service de liste, consultez :</span><span class="sxs-lookup"><span data-stu-id="19f99-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="19f99-223">Obtenir hello SAS pour un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="19f99-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="19f99-224">Obtenir hello SAS pour un partage de fichiers : *sera bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="19f99-225">Obtenir hello SAS pour une file d’attente : *sera bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="19f99-226">Obtenir hello SAS pour une table : *sera bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="19f99-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="19f99-227">Attacher le compte toohello partagé service à l’aide de hello SAS</span><span class="sxs-lookup"><span data-stu-id="19f99-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="19f99-228">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="19f99-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Option de stockage tooAzure de connexion][23]

2. <span data-ttu-id="19f99-230">Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez hello URI SAS, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="19f99-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. <span data-ttu-id="19f99-232">Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="19f99-233">toomake change, sélectionnez **dans**, puis entrez les paramètres hello souhaités.</span><span class="sxs-lookup"><span data-stu-id="19f99-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="19f99-234">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="19f99-234">Select **Connect**.</span></span>

5. <span data-ttu-id="19f99-235">Une fois qu’il est associé, hello service récemment attachée est affiché sous hello **(Service SAP)** nœud.</span><span class="sxs-lookup"><span data-stu-id="19f99-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Résultat de l’attachement tooa partagé service à l’aide d’un SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="19f99-237">Recherche de comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="19f99-237">Search for storage accounts</span></span>
<span data-ttu-id="19f99-238">Si vous avez une longue liste des comptes de stockage, un toolocate rapidement un compte de stockage spécifique est zone de recherche toouse hello haut hello du volet de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="19f99-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="19f99-239">Lorsque vous tapez dans la zone de recherche hello, hello volet gauche affiche les comptes de stockage hello qui correspondent à valeur de recherche hello saisis toothat point.</span><span class="sxs-lookup"><span data-stu-id="19f99-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="19f99-240">Par exemple, une recherche de tous les comptes de stockage dont le nom contient **tarcher** figure dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="19f99-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Recherche de compte de stockage][11]

## <a name="next-steps"></a><span data-ttu-id="19f99-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19f99-242">Next steps</span></span>
* [<span data-ttu-id="19f99-243">Gérer les ressources de Stockage Blob Azure avec l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="19f99-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
