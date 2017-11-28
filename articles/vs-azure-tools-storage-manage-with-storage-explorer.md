---
title: "Prise en main de l’Explorateur de stockage (version préliminaire) | Microsoft Docs"
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="24b54-103">Prise en main de l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="24b54-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="24b54-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="24b54-104">Overview</span></span>
<span data-ttu-id="24b54-105">L’Explorateur de stockage Azure (version préliminaire) est une application autonome qui vous permet d’utiliser facilement les données Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="24b54-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="24b54-106">Dans cet article, vous découvrez les différentes façons de vous connecter à vos comptes de stockage Azure et de les gérer.</span><span class="sxs-lookup"><span data-stu-id="24b54-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Explorateur de stockage Microsoft Azure (version préliminaire)][15]

## <a name="prerequisites"></a><span data-ttu-id="24b54-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="24b54-108">Prerequisites</span></span>
* [<span data-ttu-id="24b54-109">Télécharger et installer l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="24b54-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="24b54-110">Connexion à un service ou un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="24b54-110">Connect to a storage account or service</span></span>
<span data-ttu-id="24b54-111">L’Explorateur de stockage (version préliminaire) offre de nombreuses façons de se connecter à des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="24b54-112">Vous pouvez par exemple afficher :</span><span class="sxs-lookup"><span data-stu-id="24b54-112">For example, you can:</span></span>
* <span data-ttu-id="24b54-113">Vous connecter à des comptes de stockage associés à vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="24b54-114">Vous connecter à des comptes de stockage et à des services partagés à partir d’autres abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="24b54-115">Vous connecter au stockage local et le gérer à l’aide de l’émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="24b54-116">En outre, vous pouvez utiliser des comptes de stockage Azure à l’échelle internationale et nationale :</span><span class="sxs-lookup"><span data-stu-id="24b54-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="24b54-117">[Connexion à un abonnement Azure](#connect-to-an-azure-subscription) : gérez les ressources de stockage appartenant à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="24b54-118">[Utilisation du stockage de développement local](#work-with-local-development-storage) : gérez le stockage local à l’aide de l’émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="24b54-119">[Attachement au stockage externe](#attach-or-detach-an-external-storage-account) : gérez les ressources de stockage qui appartiennent à un autre abonnement Azure ou qui sont dans des clouds Azure nationaux en utilisant les points de terminaison, la clé et le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="24b54-120">[Attachement d’un compte de stockage à l’aide d’une SAP](#attach-storage-account-using-sas) : gérez les ressources de stockage qui appartiennent à un autre abonnement Azure à l’aide d’une signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="24b54-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="24b54-121">[Attachement d’un service à l’aide d’une SAP](#attach-service-using-sas) : gérez un service de stockage spécifique (conteneur de blobs, file d’attente ou table) qui appartient à un autre abonnement Azure à l’aide d’une SAP.</span><span class="sxs-lookup"><span data-stu-id="24b54-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="24b54-122">Connexion à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="24b54-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="24b54-123">Si vous ne possédez pas de compte Azure, vous pouvez [vous inscrire à un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="24b54-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="24b54-124">Dans l’Explorateur de stockage (version préliminaire), sélectionnez les **paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="24b54-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![paramètres de compte Azure][0]

2. <span data-ttu-id="24b54-126">Le volet gauche affiche tous les comptes Microsoft auxquels vous vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="24b54-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="24b54-127">Pour vous connecter à un autre compte, sélectionnez **Ajouter un compte** et suivez les indications pour vous connecter avec un compte Microsoft associé à un ou plusieurs abonnements Azure actifs.</span><span class="sxs-lookup"><span data-stu-id="24b54-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="24b54-128">La connexion aux comptes de stockage Azure nationaux (Azure Germany, Azure Government et Azure China par le biais d’une connexion) n’est pas prise en charge pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="24b54-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="24b54-129">Pour plus d’informations sur la procédure de connexion aux comptes de stockage Azure nationaux, consultez la section « Attacher ou détacher un compte de stockage externe ».</span><span class="sxs-lookup"><span data-stu-id="24b54-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="24b54-130">Après vous être connecté avec un compte Microsoft, le volet gauche est renseigné avec les abonnements Azure associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="24b54-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="24b54-131">Sélectionnez les abonnements Azure que vous souhaitez utiliser, puis sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="24b54-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="24b54-132">(La case à cocher **Tous les abonnements** permet de sélectionner ou de désélectionner l’ensemble des abonnements Azure répertoriés.)</span><span class="sxs-lookup"><span data-stu-id="24b54-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Sélectionner les abonnements Azure][3]  
    <span data-ttu-id="24b54-134">Le volet gauche affiche les comptes de stockage associés aux abonnements Azure sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="24b54-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Abonnements Azure sélectionnés][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="24b54-136">Connexion à un abonnement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="24b54-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="24b54-137">Pour en savoir plus sur la connexion à un abonnement Azure Stack, consultez [Connecter l’Explorateur de stockage à un abonnement Azure Stack](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="24b54-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="24b54-138">Utilisation du stockage de développement local</span><span class="sxs-lookup"><span data-stu-id="24b54-138">Work with local development storage</span></span>
<span data-ttu-id="24b54-139">Avec l’Explorateur de stockage (version préliminaire), vous pouvez travailler sur le stockage local à l’aide de l’émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="24b54-140">Cette approche vous permet d’écrire du code pour le stockage et de le tester sans nécessairement disposer d’un compte de stockage déployé sur Azure, étant donné que le compte de stockage est émulé par l’émulateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="24b54-141">Actuellement, l’émulateur de stockage Azure est pris en charge uniquement pour Windows.</span><span class="sxs-lookup"><span data-stu-id="24b54-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="24b54-142">Dans le volet gauche de l’Explorateur de stockage (version préliminaire), développez le nœud **(Local et attaché)** > **Comptes de stockage** > **(Développement)**.</span><span class="sxs-lookup"><span data-stu-id="24b54-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nœud de développement local][21]

2. <span data-ttu-id="24b54-144">Si vous n’avez pas encore installé l’émulateur de stockage Azure, vous êtes invité à le faire par le biais d’une barre d’informations.</span><span class="sxs-lookup"><span data-stu-id="24b54-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="24b54-145">Si la barre d’informations s’affiche, sélectionnez **Télécharger la dernière version** et installez l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="24b54-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Invite de téléchargement de l’émulateur de stockage Azure][22]

3. <span data-ttu-id="24b54-147">Une fois que l’émulateur est installé, vous pouvez créer et utiliser des tables, des files d’attente et des blobs locaux.</span><span class="sxs-lookup"><span data-stu-id="24b54-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="24b54-148">Pour apprendre à utiliser chaque type de compte de stockage, consultez l’un des liens suivants :</span><span class="sxs-lookup"><span data-stu-id="24b54-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="24b54-149">Manage Azure blob storage resources (Gérer les ressources Azure Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="24b54-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="24b54-150">Manage Azure file share storage resources (Gérer les ressources de stockage de partage de fichiers Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="24b54-151">Manage Azure queue storage resources (Gérer les ressources de stockage File d’attente Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="24b54-152">Manage Azure table storage resources (Gérer les ressources de stockage Table Azure) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="24b54-153">Attacher ou détacher un compte de stockage externe</span><span class="sxs-lookup"><span data-stu-id="24b54-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="24b54-154">L’Explorateur de stockage (version préliminaire) vous permet d’effectuer un attachement à des comptes de stockage externes, pour un partage simplifié des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="24b54-155">Cette section explique la procédure d’attachement à des comptes de stockage externes (et la procédure de détachement).</span><span class="sxs-lookup"><span data-stu-id="24b54-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="24b54-156">Obtention des informations d’identification du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="24b54-156">Get the storage account credentials</span></span>
<span data-ttu-id="24b54-157">Pour partager un compte de stockage externe, le propriétaire du compte doit d’abord obtenir les informations d’identification du compte (nom et clé du compte), puis les partager avec les personnes souhaitant effectuer un attachement à ce compte (externe).</span><span class="sxs-lookup"><span data-stu-id="24b54-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="24b54-158">Vous pouvez obtenir les informations d’identification du compte de stockage via le portail Azure en suivant ces étapes :</span><span class="sxs-lookup"><span data-stu-id="24b54-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="24b54-159">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24b54-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="24b54-160">Sélectionnez **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="24b54-160">Select **Browse**.</span></span>

3. <span data-ttu-id="24b54-161">Sélectionnez **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="24b54-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="24b54-162">Dans le panneau **Comptes de stockage**, sélectionnez le compte de stockage souhaité.</span><span class="sxs-lookup"><span data-stu-id="24b54-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="24b54-163">Dans le panneau **Paramètres** du compte de stockage sélectionné, sélectionnez **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="24b54-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Option Clés d’accès][5]

6. <span data-ttu-id="24b54-165">Dans le panneau **Clés d’accès**, copiez les valeurs **Nom du compte de stockage** et **key1** à utiliser pour l’attachement au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Clés d’accès][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="24b54-167">Attachement à un compte de stockage externe</span><span class="sxs-lookup"><span data-stu-id="24b54-167">Attach to an external storage account</span></span>
<span data-ttu-id="24b54-168">Pour attacher à un compte de stockage externe, vous avez besoin du nom et de la clé du compte.</span><span class="sxs-lookup"><span data-stu-id="24b54-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="24b54-169">La section « Obtention des informations d’identification du compte de stockage » explique comment obtenir ces valeurs à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="24b54-170">Toutefois, dans le portail, la clé du compte est appelée **key1**.</span><span class="sxs-lookup"><span data-stu-id="24b54-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="24b54-171">Par conséquent, lorsque l’Explorateur de stockage (version préliminaire) demande une clé de compte, vous entrez la valeur **key1**.</span><span class="sxs-lookup"><span data-stu-id="24b54-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="24b54-172">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **Se connecter à Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="24b54-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Option Se connecter à Azure Storage][23]

2. <span data-ttu-id="24b54-174">Dans la boîte de dialogue **Connexion au stockage Azure**, spécifiez la clé de compte (la valeur **key1** du portail Azure), puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="24b54-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="24b54-175">Vous pouvez entrer la chaîne de connexion de stockage appartenant à un compte de stockage Azure national.</span><span class="sxs-lookup"><span data-stu-id="24b54-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="24b54-176">Par exemple, pour vous connecter à des comptes de stockage Azure Germany, entrez des chaînes de connexion semblables à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="24b54-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="24b54-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="24b54-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="24b54-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="24b54-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="24b54-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="24b54-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="24b54-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="24b54-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="24b54-181">Vous pouvez obtenir la chaîne de connexion à partir du portail Azure en suivant les instructions de la section « Obtention des informations d’identification du compte de stockage ».</span><span class="sxs-lookup"><span data-stu-id="24b54-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Boîte de dialogue Connexion au stockage Azure][24]

3. <span data-ttu-id="24b54-183">Dans la boîte de dialogue **Attacher un stockage externe**, entrez le nom du compte de stockage dans la zone **Nom du compte**, spécifiez tout autre paramètre souhaité, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="24b54-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Boîte de dialogue Attacher un stockage externe][8]

4. <span data-ttu-id="24b54-185">Vérifiez les informations de la boîte de dialogue **Résumé de connexion**.</span><span class="sxs-lookup"><span data-stu-id="24b54-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="24b54-186">Si vous souhaitez modifier quoi que ce soit, sélectionnez **Précédent** et saisissez de nouveau les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="24b54-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="24b54-187">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="24b54-187">Select **Connect**.</span></span>

6. <span data-ttu-id="24b54-188">Une fois connecté, le compte de stockage externe s’affiche avec **(Externe)** ajouté au nom.</span><span class="sxs-lookup"><span data-stu-id="24b54-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Résultat de la connexion à un compte de stockage externe][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="24b54-190">Détachement d’un compte de stockage externe</span><span class="sxs-lookup"><span data-stu-id="24b54-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="24b54-191">Cliquez avec le bouton droit sur le compte de stockage externe que vous souhaitez détacher, puis sélectionnez **Détacher**.</span><span class="sxs-lookup"><span data-stu-id="24b54-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Option Détacher d’un compte de stockage][10]

2. <span data-ttu-id="24b54-193">Cliquez sur **Oui** dans le message de confirmation pour confirmer le détachement du compte de stockage externe.</span><span class="sxs-lookup"><span data-stu-id="24b54-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="24b54-194">Attachement d’un compte de stockage à l’aide d’une SAP</span><span class="sxs-lookup"><span data-stu-id="24b54-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="24b54-195">Une [SAP](storage/common/storage-dotnet-shared-access-signature-part-1.md) permet à l’administrateur d’un abonnement Azure d’accorder un accès temporaire à un compte de stockage sans avoir à fournir des informations d’identification pour l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="24b54-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="24b54-196">Pour illustrer ce scénario, supposons que l’utilisateur A est l’administrateur d’un abonnement Azure et qu’il souhaite autoriser l’utilisateur B à accéder à un compte de stockage pour une durée limitée, avec certaines autorisations :</span><span class="sxs-lookup"><span data-stu-id="24b54-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="24b54-197">L’utilisateur A génère une SAP (composée de la chaîne de connexion du compte de stockage) pour une période spécifique, avec les autorisations souhaitées.</span><span class="sxs-lookup"><span data-stu-id="24b54-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="24b54-198">L’utilisateur A partage la SAP avec la personne souhaitant accéder au compte de stockage, en l’occurrence l’utilisateur B.</span><span class="sxs-lookup"><span data-stu-id="24b54-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="24b54-199">L’utilisateur B utilise l’Explorateur de stockage (version préliminaire) pour effectuer l’attachement au compte appartenant à l’utilisateur A à l’aide de la SAP fournie.</span><span class="sxs-lookup"><span data-stu-id="24b54-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="24b54-200">Obtention d’une SAP pour le compte à partager</span><span class="sxs-lookup"><span data-stu-id="24b54-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="24b54-201">Dans l’Explorateur de stockage (version préliminaire), cliquez avec le bouton droit sur le compte de stockage que vous souhaitez partager, puis sélectionnez **Obtenir une signature d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="24b54-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Option de menu contextuel Obtenir une signature d’accès partagé][13]

2. <span data-ttu-id="24b54-203">Dans la boîte de dialogue **Signature d’accès partagé**, spécifiez la période et les autorisations souhaitées pour le compte, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="24b54-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="24b54-204">![Boîte de dialogue Obtenir une signature d’accès partagé][14]</span><span class="sxs-lookup"><span data-stu-id="24b54-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="24b54-205">La seconde boîte de dialogue **Signature d’accès partagé** s’ouvre et affiche la SAP.</span><span class="sxs-lookup"><span data-stu-id="24b54-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="24b54-206">Sélectionnez **Copier** en regard de la **Chaîne de connexion** pour la copier dans le Presse-papiers, puis sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="24b54-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="24b54-207">Attachement au compte partagé à l’aide de la SAP</span><span class="sxs-lookup"><span data-stu-id="24b54-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="24b54-208">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **Se connecter à Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="24b54-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Option Se connecter à Azure Storage][23]

2. <span data-ttu-id="24b54-210">Dans la boîte de dialogue **Connexion au stockage Azure**, spécifiez la chaîne de connexion, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="24b54-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Boîte de dialogue Connexion au stockage Azure][24]

3. <span data-ttu-id="24b54-212">Vérifiez les informations de la boîte de dialogue **Résumé de connexion**.</span><span class="sxs-lookup"><span data-stu-id="24b54-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="24b54-213">Pour apporter des modifications, sélectionnez **Précédent**, puis entrez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="24b54-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="24b54-214">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="24b54-214">Select **Connect**.</span></span>

5. <span data-ttu-id="24b54-215">Une fois attaché, le compte de stockage s’affiche avec **(SAP)** ajouté au nom fourni.</span><span class="sxs-lookup"><span data-stu-id="24b54-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![Résultat de l’attachement à un compte à l’aide d’une SAP][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="24b54-217">Attacher un service à l’aide d’une SAP</span><span class="sxs-lookup"><span data-stu-id="24b54-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="24b54-218">La section « Attachement d’un compte de stockage à l’aide d’une SAP » illustre la façon dont l’administrateur d’un abonnement Azure peut accorder un accès temporaire à un compte de stockage en générant et en partageant une SAP pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="24b54-219">De la même façon, une SAP peut être générée pour un service spécifique (conteneur de blobs, file d’attente ou table) dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="24b54-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="24b54-220">Génération d’une SAP pour le service à partager</span><span class="sxs-lookup"><span data-stu-id="24b54-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="24b54-221">Dans ce contexte, un service peut être un conteneur d’objets blob, une file d’attente ou une table.</span><span class="sxs-lookup"><span data-stu-id="24b54-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="24b54-222">Pour générer la SAP d’un service répertorié, consultez :</span><span class="sxs-lookup"><span data-stu-id="24b54-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="24b54-223">Obtenir la signature d’accès partagé pour un conteneur d’objets blob</span><span class="sxs-lookup"><span data-stu-id="24b54-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="24b54-224">Get the SAS for a file share (Obtenir la signature d’accès partagé pour un partage de fichiers) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="24b54-225">Get the SAS for a queue (Obtenir la signature d’accès partagé pour une file d’attente) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="24b54-226">Get the SAS for a table (Obtenir la signature d’accès partagé pour une table) - *Bientôt disponible*</span><span class="sxs-lookup"><span data-stu-id="24b54-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="24b54-227">Attachement au service de compte partagé à l’aide de la SAP</span><span class="sxs-lookup"><span data-stu-id="24b54-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="24b54-228">Dans l’Explorateur de stockage (version préliminaire), sélectionnez **Se connecter à Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="24b54-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Option Se connecter à Azure Storage][23]

2. <span data-ttu-id="24b54-230">Dans la boîte de dialogue **Connexion au stockage Azure**, spécifiez l’URI de SAP, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="24b54-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Boîte de dialogue Connexion au stockage Azure][24]

3. <span data-ttu-id="24b54-232">Vérifiez les informations de la boîte de dialogue **Résumé de connexion**.</span><span class="sxs-lookup"><span data-stu-id="24b54-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="24b54-233">Pour apporter des modifications, sélectionnez **Précédent**, puis entrez les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="24b54-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="24b54-234">Sélectionnez **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="24b54-234">Select **Connect**.</span></span>

5. <span data-ttu-id="24b54-235">Une fois attaché, le nouveau service s’affiche sous le nœud **(Service SAS)** (SAP de service).</span><span class="sxs-lookup"><span data-stu-id="24b54-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Résultat de l’attachement à un service partagé à l’aide d’une SAP][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="24b54-237">Recherche de comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="24b54-237">Search for storage accounts</span></span>
<span data-ttu-id="24b54-238">Si vous avez une longue liste de comptes de stockage, la zone de recherche située en haut du volet gauche offre un moyen rapide de rechercher un compte spécifique.</span><span class="sxs-lookup"><span data-stu-id="24b54-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="24b54-239">À mesure que vous tapez dans la zone de recherche, le volet gauche affiche les comptes de stockage qui correspondent à la valeur en cours de saisie.</span><span class="sxs-lookup"><span data-stu-id="24b54-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="24b54-240">Par exemple, une recherche de tous les comptes de stockage dont le nom contient **tarcher** est illustrée dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="24b54-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Recherche de compte de stockage][11]

## <a name="next-steps"></a><span data-ttu-id="24b54-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24b54-242">Next steps</span></span>
* [<span data-ttu-id="24b54-243">Gérer les ressources de Stockage Blob Azure avec l’Explorateur de stockage (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="24b54-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
