---
title: aaaUsing Azure PowerShell avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello applets de commande Azure PowerShell pour Azure Storage toocreate et gérer les comptes de stockage ; travailler avec des objets BLOB, les tables, les files d’attente et les fichiers ; configurer et de requête analytique de stockage et créent des signatures d’accès partagé."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="54f74-103">Utilisation d'Azure PowerShell avec Azure Storage</span><span class="sxs-lookup"><span data-stu-id="54f74-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="54f74-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="54f74-104">Overview</span></span>
<span data-ttu-id="54f74-105">Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="54f74-106">Il s'agit d'un interpréteur de ligne de commande et d'un langage de script basé sur des tâches, conçu spécialement pour l'administration système.</span><span class="sxs-lookup"><span data-stu-id="54f74-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="54f74-107">Avec PowerShell, vous pouvez facilement contrôler et automatiser l’administration hello de vos services et applications Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="54f74-108">Par exemple, vous pouvez utiliser Bonjour applets de commande tooperform Bonjour même tâches que vous pouvez effectuer via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54f74-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="54f74-109">Dans ce guide, nous allons examiner comment toouse hello [applets de commande de stockage Azure](/powershell/module/azurerm.storage/#storage) tooperform diverses tâches de développement et d’administration avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="54f74-110">Ce guide part du principe que vous avez une certaine expérience en tant qu’utilisateur d’[Azure Storage](https://azure.microsoft.com/documentation/services/storage/) et de [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="54f74-111">guide de Hello fournit un nombre de scripts hello de toodemonstrate l’utilisation de PowerShell avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="54f74-112">Vous devez mettre à jour les variables de script hello en fonction de votre configuration avant d’exécuter chaque script.</span><span class="sxs-lookup"><span data-stu-id="54f74-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="54f74-113">Hello première section de ce guide fournit un aperçu rapide au stockage Azure et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="54f74-114">Pour plus d’informations et des instructions, démarrer à partir de hello [conditions préalables à l’aide d’Azure PowerShell avec le stockage Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="54f74-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="54f74-115">Prise en main d'Azure Storage et de PowerShell en 5 minutes</span><span class="sxs-lookup"><span data-stu-id="54f74-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="54f74-116">Cette section vous montre comment tooaccess le stockage Azure via PowerShell dans 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="54f74-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="54f74-117">**Nouvelle tooAzure :** obtenir un abonnement Microsoft Azure et un compte Microsoft associé à cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="54f74-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="54f74-118">Pour en savoir plus sur les options d’achat de Microsoft Azure, voir [Essai gratuit](https://azure.microsoft.com/pricing/free-trial/), [Options d’achat](https://azure.microsoft.com/pricing/purchase-options/) et [Offres spéciales membres](https://azure.microsoft.com/pricing/member-offers/) (pour les membres de MSDN, Microsoft Partner Network et BizSpark, ainsi que d’autres programmes Microsoft).</span><span class="sxs-lookup"><span data-stu-id="54f74-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="54f74-119">Pour plus d’informations sur les abonnements Azure, consultez la section [Attribution de rôles d’administrateur dans Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="54f74-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="54f74-120">**Une fois le compte et l’abonnement à Microsoft Azure créés :**</span><span class="sxs-lookup"><span data-stu-id="54f74-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="54f74-121">Télécharger et installer les dernières hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="54f74-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="54f74-122">Démarrer Windows PowerShell Scripting environnement intégré (ISE) : Sur votre ordinateur local, accédez à toohello **Démarrer** menu.</span><span class="sxs-lookup"><span data-stu-id="54f74-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="54f74-123">Type **outils d’administration** sur toorun il.</span><span class="sxs-lookup"><span data-stu-id="54f74-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="54f74-124">Bonjour **outils d’administration** fenêtre, avec le bouton droit **Windows PowerShell ISE**, cliquez sur **exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="54f74-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="54f74-125">Dans **Windows PowerShell ISE**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="54f74-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="54f74-126">Maintenant, nous donnons un script simple qui montre la base tooaccess de commandes PowerShell Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="54f74-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="54f74-127">script de Hello sera tout d’abord demander à votre tooadd d’informations d’identification de compte Azure votre environnement PowerShell local de compte Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="54f74-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="54f74-128">Ensuite, hello script définir la valeur par défaut de hello abonnement Azure et créez un compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="54f74-129">Ensuite, hello script créer un conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant.</span><span class="sxs-lookup"><span data-stu-id="54f74-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="54f74-130">Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle crée un nouveau répertoire de destination dans votre ordinateur local et télécharger le fichier d’image hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="54f74-131">Bonjour suivant la section de code, sélectionnez le script de hello entre la section Notes hello **#begin** et **#end**.</span><span class="sxs-lookup"><span data-stu-id="54f74-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="54f74-132">Appuyez sur CTRL + C toocopy il toohello Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="54f74-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="54f74-133">Dans **Windows PowerShell ISE**, appuyez sur le script de hello toocopy CTRL + V.</span><span class="sxs-lookup"><span data-stu-id="54f74-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="54f74-134">Cliquez sur **Fichier** > **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="54f74-134">Click **File** > **Save**.</span></span> <span data-ttu-id="54f74-135">Bonjour **Enregistrer sous** boîte de dialogue, entrez un nom hello du fichier de script hello, tels que « mystoragescript ».</span><span class="sxs-lookup"><span data-stu-id="54f74-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="54f74-136">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="54f74-136">Click **Save**.</span></span>
7. <span data-ttu-id="54f74-137">Maintenant, vous devez les variables de script tooupdate hello en fonction de vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="54f74-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="54f74-138">Vous devez mettre à jour hello **$SubscriptionName** variable avec votre propre abonnement.</span><span class="sxs-lookup"><span data-stu-id="54f74-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="54f74-139">Vous pouvez conserver les autres variables comme spécifié dans le script de hello hello ou les mettre à jour que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="54f74-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="54f74-140">**$SubscriptionName :** vous devez mettre à jour cette variable avec le nom de votre propre abonnement.</span><span class="sxs-lookup"><span data-stu-id="54f74-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="54f74-141">Suivez l’une des hello suivant trois nom hello toolocate de façons de votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="54f74-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="54f74-142">a.</span><span class="sxs-lookup"><span data-stu-id="54f74-142">a.</span></span> <span data-ttu-id="54f74-143">Dans **Windows PowerShell ISE**, cliquez sur **fichier** > **nouveau** toocreate un fichier de script.</span><span class="sxs-lookup"><span data-stu-id="54f74-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="54f74-144">Suivant de hello copie toohello nouveau fichier de script de script et cliquez sur **déboguer** > **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="54f74-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="54f74-145">Hello script suivant sera tout d’abord demander votre tooadd d’informations d’identification de compte Azure à votre environnement PowerShell local de compte Azure toohello et présentent ensuite tous les abonnements hello session PowerShell locale de toohello connecté.</span><span class="sxs-lookup"><span data-stu-id="54f74-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="54f74-146">Notez une hello nom d’abonnement de hello que vous souhaitez toouse en suivant ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="54f74-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="54f74-147">b.</span><span class="sxs-lookup"><span data-stu-id="54f74-147">b.</span></span> <span data-ttu-id="54f74-148">toolocate et copiez votre abonnement nom Bonjour [portail Azure](https://portal.azure.com)hello menu Hub sur hello gauche, cliquez sur dans **abonnements**.</span><span class="sxs-lookup"><span data-stu-id="54f74-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="54f74-149">Copiez hello nom de l’abonnement que vous souhaitez toouse lors de l’exécution des scripts de hello dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="54f74-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Portail Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="54f74-151">c.</span><span class="sxs-lookup"><span data-stu-id="54f74-151">c.</span></span> <span data-ttu-id="54f74-152">toolocate et copiez votre abonnement nom Bonjour [portail classique Azure](https://manage.windowsazure.com/), faites défiler la liste et cliquez sur **paramètres** sur hello gauche du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="54f74-153">Cliquez sur **abonnements** toosee une liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="54f74-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="54f74-154">Nom de hello copie d’abonnement que vous souhaitez toouse lors de l’exécution des scripts hello donnés dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="54f74-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![portail Azure Classic](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="54f74-156">**$StorageAccountName :** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="54f74-157">**Important :** nom hello hello du compte de stockage doit être unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="54f74-158">Il doit également inclure des minuscules uniquement.</span><span class="sxs-lookup"><span data-stu-id="54f74-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="54f74-159">**$Location :** hello donné « Ouest des États-Unis » dans le script de hello ou sélectionnez d’autres emplacements de Azure, tels que les États-Unis, Europe du Nord et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="54f74-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="54f74-160">**$ContainerName :** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="54f74-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="54f74-161">**$ImageToUpload :** saisir une image de tooa de chemin d’accès sur votre ordinateur local, tel que : « C:\Images\HelloWorld.png ».</span><span class="sxs-lookup"><span data-stu-id="54f74-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="54f74-162">**$DestinationFolder :** Entrez un chemin d’accès tooa répertoire local toostore les fichiers téléchargés depuis le stockage Azure, telles que : « C:\DownloadImages ».</span><span class="sxs-lookup"><span data-stu-id="54f74-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="54f74-163">Après la mise à jour les variables de script hello dans le fichier de « mystoragescript.ps1 » hello, cliquez sur **fichier** > **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="54f74-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="54f74-164">Ensuite, cliquez sur **déboguer** > **exécuter** ou appuyez sur **F5** script de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="54f74-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="54f74-165">Après l’exécution du script de hello, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="54f74-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="54f74-166">Hello suivant capture d’écran montre un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="54f74-166">hello following screenshot shows an example output:</span></span>

![Téléchargement d'objets blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="54f74-168">Hello section « Mise en route avec le stockage Azure et de PowerShell dans 5 minutes » fourni une brève introduction sur la façon de toouse Azure PowerShell avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="54f74-169">Pour plus d’informations et des instructions, nous vous encourageons hello tooread les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="54f74-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="54f74-170">Conditions préalables à l’utilisation d’Azure PowerShell avec Azure Storage</span><span class="sxs-lookup"><span data-stu-id="54f74-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="54f74-171">Vous avez besoin d’un abonnement et compte toorun hello PowerShell applets de commande Azure donné dans ce guide, comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="54f74-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="54f74-172">Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="54f74-173">Pour plus d’informations sur l’installation et configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54f74-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="54f74-174">Nous vous recommandons de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent avant d’utiliser ce guide.</span><span class="sxs-lookup"><span data-stu-id="54f74-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="54f74-175">Vous pouvez exécuter les applets de commande hello dans la console Windows PowerShell standard de hello ou hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="54f74-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="54f74-176">Par exemple, tooopen **Windows PowerShell ISE**atteindre le menu Démarrer de toohello, tapez outils d’administration, cliquez sur toorun il.</span><span class="sxs-lookup"><span data-stu-id="54f74-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="54f74-177">Dans la fenêtre Outils d’administration de hello, avec le bouton droit de Windows PowerShell ISE, cliquez sur Exécuter en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="54f74-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="54f74-178">Le mode de stockage de toomanage comptes dans Azure</span><span class="sxs-lookup"><span data-stu-id="54f74-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="54f74-179">Commençons par étudier la gestion des comptes de stockage dans Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f74-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="54f74-180">Comment tooset un abonnement Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="54f74-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="54f74-181">toomanage le stockage Azure à l’aide d’Azure PowerShell, vous devez tooauthenticate votre environnement de client avec Azure via l’authentification Azure Active Directory ou l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="54f74-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="54f74-182">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="54f74-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="54f74-183">Ce guide utilise l’authentification Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="54f74-184">Dans Windows PowerShell ISE, tapez Bonjour suivant commande tooadd votre environnement PowerShell local de compte Azure toohello :</span><span class="sxs-lookup"><span data-stu-id="54f74-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="54f74-185">Dans la fenêtre de hello « Connexion tooMicrosoft Azure », adresse de messagerie de type hello et mot de passe associé à votre compte.</span><span class="sxs-lookup"><span data-stu-id="54f74-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="54f74-186">Azure authentifie et enregistre les informations d’identification de hello, puis ferme la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="54f74-187">Ensuite, exécutez hello suivant commande tooview hello Azure des comptes dans votre environnement PowerShell local et vérifiez que votre compte est répertorié :</span><span class="sxs-lookup"><span data-stu-id="54f74-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="54f74-188">Ensuite, exécutez hello suivant tooview de l’applet de commande tous les abonnements hello session PowerShell locale de toohello connecté et vérifiez que votre abonnement est répertorié :</span><span class="sxs-lookup"><span data-stu-id="54f74-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="54f74-189">tooset un abonnement Azure, par défaut, exécutez l’applet de commande hello Select-AzureSubscription :</span><span class="sxs-lookup"><span data-stu-id="54f74-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="54f74-190">Vérifiez le nom hello d’abonnement par défaut de hello en exécutant l’applet de commande Get-AzureSubscription hello :</span><span class="sxs-lookup"><span data-stu-id="54f74-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="54f74-191">toosee que tous hello applets de commande PowerShell disponibles pour le stockage Azure, exécutez :</span><span class="sxs-lookup"><span data-stu-id="54f74-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="54f74-192">Comment toocreate un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="54f74-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="54f74-193">Vous devrez toouse le stockage Azure, un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="54f74-194">Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre abonnement de tooyour tooconnect ordinateur.</span><span class="sxs-lookup"><span data-stu-id="54f74-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="54f74-195">Exécutez toofind d’applet de commande Get-AzureLocation hello tous les emplacements de centres de données disponibles hello :</span><span class="sxs-lookup"><span data-stu-id="54f74-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="54f74-196">Ensuite, exécutez toocreate d’applet de commande New-AzureStorageAccount hello pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="54f74-197">Hello exemple suivant crée un nouveau compte de stockage dans le centre de données hello « Ouest des États-Unis ».</span><span class="sxs-lookup"><span data-stu-id="54f74-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="54f74-198">nom de Hello de votre compte de stockage doit être unique dans Azure et doit être en minuscule.</span><span class="sxs-lookup"><span data-stu-id="54f74-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="54f74-199">Pour connaître les conventions d’affectation de noms et les restrictions, consultez les pages [À propos des comptes de stockage Azure](../storage-create-storage-account.md) et [Affectation de noms et références aux conteneurs, objets blob et métadonnées](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="54f74-200">Comment tooset un compte de stockage Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="54f74-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="54f74-201">Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="54f74-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="54f74-202">Vous pouvez choisir un d’eux et définissez-le comme compte de stockage par défaut hello pour tous les hello stockage commandes Bonjour même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="54f74-203">Cela vous permet commandes de stockage Azure PowerShell toorun hello sans spécifier le contexte de stockage hello explicitement.</span><span class="sxs-lookup"><span data-stu-id="54f74-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="54f74-204">tooset un compte de stockage par défaut pour votre abonnement, vous pouvez exécuter l’applet de commande Set-AzureSubscription hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="54f74-205">Ensuite, exécutez tooverify d’applet de commande Get-AzureSubscription de hello que le compte de stockage hello est associé à votre compte d’abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="54f74-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="54f74-206">Cette commande retourne les propriétés de l’abonnement hello sur abonnement hello, y compris son compte de stockage actuel.</span><span class="sxs-lookup"><span data-stu-id="54f74-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="54f74-207">Le mode toolist tout le stockage Azure de comptes dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="54f74-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="54f74-208">Chaque abonnement Azure peut avoir des comptes de stockage too100.</span><span class="sxs-lookup"><span data-stu-id="54f74-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="54f74-209">Pour hello dernières informations sur les limites, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="54f74-210">Exécutez hello suivant toofind d’applet de commande out nom de hello et l’état hello de comptes de stockage dans l’abonnement actif de hello :</span><span class="sxs-lookup"><span data-stu-id="54f74-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="54f74-211">Comment toocreate un contexte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="54f74-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="54f74-212">Contexte de stockage Azure est un objet d’informations d’identification du stockage hello tooencapsulate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="54f74-213">À l’aide d’un contexte de stockage lors de l’exécution d’une applet de commande suivante permet de vous tooauthenticate votre demande sans spécification explicite de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="54f74-214">Vous pouvez créer un contexte de stockage de plusieurs façons, par exemple à l'aide du nom du compte et de la clé d'accès, du jeton de signature d'accès partagé (SAS), de la chaîne de connexion ou de façon anonyme.</span><span class="sxs-lookup"><span data-stu-id="54f74-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="54f74-215">Pour plus d’informations, consultez la page [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="54f74-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="54f74-216">Utilisez une des hello suivant de trois façons toocreate d’un contexte de stockage :</span><span class="sxs-lookup"><span data-stu-id="54f74-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="54f74-217">Exécutez hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind d’applet de commande à la clé d’accès de stockage principal hello pour votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="54f74-218">Ensuite, appelez hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) toocreate de l’applet de commande un contexte de stockage :</span><span class="sxs-lookup"><span data-stu-id="54f74-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="54f74-219">Générer un jeton de signature d’accès partagé pour un conteneur de stockage Azure et l’utiliser toocreate un contexte de stockage :</span><span class="sxs-lookup"><span data-stu-id="54f74-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="54f74-220">Pour plus d’informations, consultez [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) et [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="54f74-221">Dans certains cas, vous pouvez vouloir points de terminaison de service toospecify hello lorsque vous créez un nouveau contexte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="54f74-222">Cela peut être nécessaire lorsque vous avez enregistré un nom de domaine personnalisé pour votre compte de stockage avec service d’objets Blob hello ou toouse une signature d’accès partagé pour l’accès aux ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="54f74-223">Définir des points de terminaison de service hello dans une chaîne de connexion et utilisez toocreate un nouveau contexte de stockage comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="54f74-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="54f74-224">Pour plus d’informations sur la façon de tooconfigure une chaîne de connexion de stockage, consultez [configuration des chaînes de connexion](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="54f74-225">Maintenant que vous avez configuré votre ordinateur et appris comment toomanage abonnements et les comptes de stockage à l’aide d’Azure PowerShell, accédez toohello toolearn de section suivant comment toomanage Azure BLOB et instantanés d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="54f74-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="54f74-226">Comment tooretrieve et régénérer les clés de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="54f74-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="54f74-227">Un compte Azure Storage est fourni avec deux clés de compte.</span><span class="sxs-lookup"><span data-stu-id="54f74-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="54f74-228">Vous pouvez utiliser hello suivant l’applet de commande tooretrieve vos clés.</span><span class="sxs-lookup"><span data-stu-id="54f74-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="54f74-229">Utilisez hello suivant l’applet de commande tooretrieve une clé spécifique.</span><span class="sxs-lookup"><span data-stu-id="54f74-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="54f74-230">Les valeurs valides sont : Primaire et Secondaire.</span><span class="sxs-lookup"><span data-stu-id="54f74-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="54f74-231">Si vous souhaitez que tooregenerate vos clés, utilisez hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="54f74-232">Les valeurs valides pour -KeyType sont « Primaire » et « Secondaire »</span><span class="sxs-lookup"><span data-stu-id="54f74-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="54f74-233">Comment toomanage Azure BLOB</span><span class="sxs-lookup"><span data-stu-id="54f74-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="54f74-234">Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54f74-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="54f74-235">Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage d’objets Blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="54f74-236">Pour obtenir des informations détaillées, consultez [Prise en main du stockage d’objets blob à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md) et [Concepts du service BLOB](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="54f74-237">Comment toocreate un conteneur</span><span class="sxs-lookup"><span data-stu-id="54f74-237">How toocreate a container</span></span>
<span data-ttu-id="54f74-238">Chaque objet blob du stockage Azure doit se trouver dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="54f74-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="54f74-239">Vous pouvez créer un conteneur privé à l’aide d’applet de commande New-AzureStorageContainer de hello :</span><span class="sxs-lookup"><span data-stu-id="54f74-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="54f74-240">Il existe trois niveaux d’accès en lecture anonyme : **Désactivé**, **Blob** et **Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="54f74-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="54f74-241">tooprevent anonyme accéder à tooblobs, le paramètre d’autorisation ensemble hello**hors**.</span><span class="sxs-lookup"><span data-stu-id="54f74-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="54f74-242">Par défaut, hello nouveau conteneur est privé et sont accessibles uniquement par le propriétaire du compte hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="54f74-243">public anonyme de tooallow lire tooblob d’accéder aux ressources, mais pas toocontainer métadonnées ou toohello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**Blob**.</span><span class="sxs-lookup"><span data-stu-id="54f74-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="54f74-244">public complet de tooallow lire tooblob d’accéder aux ressources, les métadonnées de conteneur et hello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**conteneur**.</span><span class="sxs-lookup"><span data-stu-id="54f74-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="54f74-245">Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="54f74-246">Comment tooupload un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="54f74-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="54f74-247">Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page.</span><span class="sxs-lookup"><span data-stu-id="54f74-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="54f74-248">Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="54f74-249">tooupload objets BLOB dans tooa conteneur, vous pouvez utiliser hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="54f74-250">Par défaut, cette commande télécharge le blob de blocs tooa hello fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="54f74-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="54f74-251">type de hello toospecify pour l’objet blob de hello, vous pouvez utiliser le paramètre - BlobType de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="54f74-252">exemple Hello exécute hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) tooget d’applet de commande hello tous les fichiers dans le dossier spécifié de hello et les transmet toohello applet de commande suivante en utilisant l’opérateur de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="54f74-253">Hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) applet de commande télécharge le conteneur de tooyour hello fichiers locaux :</span><span class="sxs-lookup"><span data-stu-id="54f74-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="54f74-254">Comment toodownload les objets BLOB à partir d’un conteneur</span><span class="sxs-lookup"><span data-stu-id="54f74-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="54f74-255">Bonjour à l’exemple suivant montre comment toodownload les objets BLOB à partir d’un conteneur.</span><span class="sxs-lookup"><span data-stu-id="54f74-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="54f74-256">exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès primaire.</span><span class="sxs-lookup"><span data-stu-id="54f74-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="54f74-257">Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="54f74-258">Ensuite, hello utilise hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs de toodownload d’applet de commande dans le dossier de destination local hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="54f74-259">Comment toocopy les objets BLOB à partir d’un tooanother de conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="54f74-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="54f74-260">Vous pouvez également copier des objets blob entre les comptes de stockage et les régions de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="54f74-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="54f74-261">Hello exemple suivant montre comment les objets BLOB toocopy de tooanother de conteneur de stockage dans les deux comptes de stockage différents.</span><span class="sxs-lookup"><span data-stu-id="54f74-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="54f74-262">exemple de Hello définit les variables pour les comptes de stockage source et de destination et crée ensuite un contexte de stockage pour chaque compte.</span><span class="sxs-lookup"><span data-stu-id="54f74-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="54f74-263">Ensuite, hello exemple copie les objets BLOB à partir du conteneur hello source conteneur toohello destination à l’aide de hello [AzureStorageBlobCopy de début](/powershell/module/azure.storage/start-azurestorageblobcopy) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="54f74-264">Hello suppose que les conteneurs et les comptes de stockage source et de destination hello existent déjà.</span><span class="sxs-lookup"><span data-stu-id="54f74-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="54f74-265">Notez que cet exemple effectue une copie asynchrone.</span><span class="sxs-lookup"><span data-stu-id="54f74-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="54f74-266">Vous pouvez surveiller l’état de hello de chaque copie en exécutant hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="54f74-267">Comment toocopy les objets BLOB à partir d’un emplacement secondaire</span><span class="sxs-lookup"><span data-stu-id="54f74-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="54f74-268">Vous pouvez copier des objets BLOB à partir de l’emplacement secondaire de hello d’un compte activé RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="54f74-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="54f74-269">Comment toodelete un objet blob</span><span class="sxs-lookup"><span data-stu-id="54f74-269">How toodelete a blob</span></span>
<span data-ttu-id="54f74-270">toodelete un objet blob, commencez par obtenir une référence d’objet blob, puis appelez applet de commande Remove-AzureStorageBlob hello sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="54f74-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="54f74-271">Bonjour à l’exemple suivant supprime tous les objets BLOB de hello dans un conteneur donné.</span><span class="sxs-lookup"><span data-stu-id="54f74-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="54f74-272">exemple de Hello définit les variables pour un compte de stockage et crée ensuite un contexte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="54f74-273">Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) blobs de tooremove d’applet de commande à partir d’un conteneur dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="54f74-274">Comment toomanage Azure instantanés d’objets blob</span><span class="sxs-lookup"><span data-stu-id="54f74-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="54f74-275">Azure vous permet de créer l'instantané d'un objet blob.</span><span class="sxs-lookup"><span data-stu-id="54f74-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="54f74-276">Un instantané est une version en lecture seule d'un objet blob capturé à un instant donné.</span><span class="sxs-lookup"><span data-stu-id="54f74-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="54f74-277">Un instantané peut être lu, copié ou supprimé, mais pas modifié.</span><span class="sxs-lookup"><span data-stu-id="54f74-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="54f74-278">Instantanés fournissent un tooback moyen d’un objet blob, tel qu’il apparaît à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="54f74-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="54f74-279">Pour plus d’informations, consultez [Création d’un instantané d’objet blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="54f74-280">Comment toocreate un instantané d’objet blob</span><span class="sxs-lookup"><span data-stu-id="54f74-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="54f74-281">tout d’abord obtenir une référence d’objet blob de toocreate un instantané d’un objet blob et ensuite appeler hello `ICloudBlob.CreateSnapshot` méthode dessus.</span><span class="sxs-lookup"><span data-stu-id="54f74-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="54f74-282">Bonjour exemple suivant définit les variables pour un compte de stockage et crée ensuite un contexte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="54f74-283">Ensuite, hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) méthode toocreate un instantané.</span><span class="sxs-lookup"><span data-stu-id="54f74-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="54f74-284">Comment les instantanés de toolist un objet blob</span><span class="sxs-lookup"><span data-stu-id="54f74-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="54f74-285">Vous pouvez créer autant d'instantanés que vous le souhaitez pour un objet blob.</span><span class="sxs-lookup"><span data-stu-id="54f74-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="54f74-286">Vous pouvez répertorier les instantanés hello associés à votre tootrack blob vos instantanés actuels.</span><span class="sxs-lookup"><span data-stu-id="54f74-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="54f74-287">Hello exemple suivant utilise un prédéfinis Bonjour blob et les appels [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) applet de commande toolist hello des instantanés de cet objet blob.</span><span class="sxs-lookup"><span data-stu-id="54f74-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="54f74-288">Comment toocopy un instantané d’un objet blob</span><span class="sxs-lookup"><span data-stu-id="54f74-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="54f74-289">Vous pouvez copier un instantané d’un instantané de hello toorestore blob.</span><span class="sxs-lookup"><span data-stu-id="54f74-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="54f74-290">Pour plus d’informations et d’autres informations sur les restrictions, consultez [Création d’un instantané d’objet blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="54f74-291">Bonjour exemple suivant définit les variables pour un compte de stockage et crée ensuite un contexte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="54f74-292">Ensuite, hello exemple définit des variables de nom de conteneur et d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="54f74-293">Hello exemple récupère une référence d’objet blob à l’aide de hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) hello applet de commande et exécute [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) méthode toocreate un instantané.</span><span class="sxs-lookup"><span data-stu-id="54f74-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="54f74-294">Exemple de hello exécute ensuite hello [AzureStorageBlobCopy de début](/powershell/module/azure.storage/start-azurestorageblobcopy) instantané de hello toocopy applet de commande d’un objet blob à l’aide d’objet de ICloudBlob hello pour l’objet blob source de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="54f74-295">Que les variables hello tooupdate reposer sur votre configuration avant d’exemple hello en cours.</span><span class="sxs-lookup"><span data-stu-id="54f74-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="54f74-296">Notez que hello l’exemple suivant suppose que la source de hello et conteneurs de destination et hello source blob existent déjà.</span><span class="sxs-lookup"><span data-stu-id="54f74-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="54f74-297">Maintenant que vous avez appris comment toomanage Azure BLOB et instantanés avec Azure PowerShell d’objets blob, accédez à toohello suivant section toolearn comment toomanage tables, files d’attente et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="54f74-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="54f74-298">Comment toomanage Azure tables et entités de table</span><span class="sxs-lookup"><span data-stu-id="54f74-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="54f74-299">Service de stockage de Table Azure est une banque de données NoSQL, que vous pouvez utiliser des jeux d’énorme toostore et requête de données structurées et non relationnelles.</span><span class="sxs-lookup"><span data-stu-id="54f74-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="54f74-300">Hello principaux composants du service de hello sont des tables, des entités et propriétés.</span><span class="sxs-lookup"><span data-stu-id="54f74-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="54f74-301">une table est une collection d’entités.</span><span class="sxs-lookup"><span data-stu-id="54f74-301">A table is a collection of entities.</span></span> <span data-ttu-id="54f74-302">Une entité est un ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="54f74-302">An entity is a set of properties.</span></span> <span data-ttu-id="54f74-303">Chaque entité peut avoir les propriétés too252, qui sont toutes les paires nom-valeur.</span><span class="sxs-lookup"><span data-stu-id="54f74-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="54f74-304">Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage de Table Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="54f74-305">Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx) et [prise en main le stockage de Table Azure à l’aide de .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="54f74-306">Bonjour suivant sous-sections, vous allez apprendre comment toomanage stockage de Table Azure de service à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="54f74-307">Hello scénarios abordés incluent **création**, **suppression**, et **récupération** **tables**, ainsi que **ajout**, **interrogation**, et **la suppression des entités de table**.</span><span class="sxs-lookup"><span data-stu-id="54f74-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="54f74-308">Comment toocreate une table</span><span class="sxs-lookup"><span data-stu-id="54f74-308">How toocreate a table</span></span>
<span data-ttu-id="54f74-309">Toutes les tables doivent se trouver dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="54f74-310">Hello exemple suivant montre comment toocreate une table dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="54f74-311">exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-312">Ensuite, il utilise hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) toocreate de l’applet de commande une table dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="54f74-313">Comment tooretrieve une table</span><span class="sxs-lookup"><span data-stu-id="54f74-313">How tooretrieve a table</span></span>
<span data-ttu-id="54f74-314">Vous pouvez interroger et récupérer une des tables ou toutes les tables dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="54f74-315">Hello exemple suivant montre comment une table donnée à l’aide de tooretrieve hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="54f74-316">Si vous appelez hello applet de commande Get-AzureStorageTable sans aucun paramètre, il obtient toutes les tables de stockage pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="54f74-317">Comment toodelete une table</span><span class="sxs-lookup"><span data-stu-id="54f74-317">How toodelete a table</span></span>
<span data-ttu-id="54f74-318">Vous pouvez supprimer une table à partir d’un compte de stockage à l’aide de hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="54f74-319">Comment toomanage table des entités</span><span class="sxs-lookup"><span data-stu-id="54f74-319">How toomanage table entities</span></span>
<span data-ttu-id="54f74-320">Actuellement, Azure PowerShell ne fournit pas directement des entités de table toomanage applets de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="54f74-321">tooperform des opérations sur les entités de table, vous pouvez utiliser les classes de hello figurant hello [bibliothèque cliente de stockage Azure pour .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="54f74-322">Comment tooadd table des entités</span><span class="sxs-lookup"><span data-stu-id="54f74-322">How tooadd table entities</span></span>
<span data-ttu-id="54f74-323">tooadd une table tooa d’entité, d’abord créer un objet qui définit les propriétés de l’entité.</span><span class="sxs-lookup"><span data-stu-id="54f74-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="54f74-324">Une entité peut avoir les propriétés too255, y compris 3 Propriétés système : **PartitionKey**, **RowKey**, et **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="54f74-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="54f74-325">Vous êtes chargé d’insertion et de mise à jour des valeurs hello de **PartitionKey** et **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="54f74-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="54f74-326">valeur hello gère Hello server **Timestamp**, qui ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="54f74-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="54f74-327">Ensemble hello **PartitionKey** et **RowKey** identifier de façon unique chaque entité d’une table.</span><span class="sxs-lookup"><span data-stu-id="54f74-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="54f74-328">**PartitionKey**: détermine la partition hello stockées dans les entités hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="54f74-329">**RowKey**: identifie de façon unique entité hello au sein de la partition de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="54f74-330">Vous pouvez définir les propriétés personnalisées de too252 pour une entité.</span><span class="sxs-lookup"><span data-stu-id="54f74-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="54f74-331">Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="54f74-332">Hello exemple suivant montre la table de tooa tooadd entités.</span><span class="sxs-lookup"><span data-stu-id="54f74-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="54f74-333">Hello montre comment tooretrieve hello table employee et comment ajouter plusieurs entités dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="54f74-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="54f74-334">Tout d’abord, il établit une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-335">Ensuite, il récupère hello fonction table à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="54f74-336">Si la table de hello n’existe pas, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) applet de commande est utilisée toocreate une table dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="54f74-337">Ensuite, hello exemple définit une fonction personnalisée table de toohello-ajouter une entité tooadd entités en spécifiant la partition de chaque entité et la clé de ligne.</span><span class="sxs-lookup"><span data-stu-id="54f74-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="54f74-338">Hello ajouter une entité fonction appels hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) applet de commande hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) classe toocreate un objet entité.</span><span class="sxs-lookup"><span data-stu-id="54f74-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="54f74-339">Une version ultérieure, hello exemple appelle hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) méthode sur cette tooadd d’objet entité il tooa table.</span><span class="sxs-lookup"><span data-stu-id="54f74-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="54f74-340">Comment tooquery table des entités</span><span class="sxs-lookup"><span data-stu-id="54f74-340">How tooquery table entities</span></span>
<span data-ttu-id="54f74-341">tooquery une table, utilisez hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="54f74-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="54f74-342">Hello exemple suivant suppose que vous avez déjà exécuté le script hello figurant hello la section d’entités tooadd de ce guide.</span><span class="sxs-lookup"><span data-stu-id="54f74-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="54f74-343">exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-344">Ensuite, il tente de table de hello créé précédemment « employés » tooretrieve à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="54f74-345">Appel hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) hello Microsoft.WindowsAzure.Storage.Table.TableQuery classe applet de commande crée un nouvel objet de requête.</span><span class="sxs-lookup"><span data-stu-id="54f74-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="54f74-346">exemple de Hello recherche entités hello qui possèdent une colonne « ID » dont la valeur est 1, comme spécifié dans un filtre de chaîne.</span><span class="sxs-lookup"><span data-stu-id="54f74-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="54f74-347">Pour plus d’informations, consultez [Interrogation de tables et d’entités](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="54f74-348">Lorsque vous exécutez cette requête, il retourne toutes les entités qui correspondent aux critères de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="54f74-349">Comment toodelete table des entités</span><span class="sxs-lookup"><span data-stu-id="54f74-349">How toodelete table entities</span></span>
<span data-ttu-id="54f74-350">Vous pouvez supprimer une entité en utilisant ses clés de partition et de ligne.</span><span class="sxs-lookup"><span data-stu-id="54f74-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="54f74-351">Hello exemple suivant suppose que vous avez déjà exécuté le script hello figurant hello la section d’entités tooadd de ce guide.</span><span class="sxs-lookup"><span data-stu-id="54f74-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="54f74-352">exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-353">Ensuite, il tente de table de hello créé précédemment « employés » tooretrieve à l’aide de hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="54f74-354">Si la table de hello existe, hello exemple appelle hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve méthode une entité en fonction de ses valeurs de clé de partition et de ligne.</span><span class="sxs-lookup"><span data-stu-id="54f74-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="54f74-355">Ensuite, passez hello entité toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de méthode.</span><span class="sxs-lookup"><span data-stu-id="54f74-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="54f74-356">Comment toomanage Azure files d’attente et file d’attente de messages</span><span class="sxs-lookup"><span data-stu-id="54f74-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="54f74-357">Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54f74-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="54f74-358">Cette section part du principe que vous êtes déjà familiarisé avec les concepts de Service de stockage de file d’attente Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="54f74-359">Pour obtenir des informations détaillées, consultez [Prise en main d’Azure Queue Storage à l’aide de .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="54f74-360">Cette section vous indiquera comment toomanage stockage de file d’attente Azure service à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="54f74-361">Hello scénarios abordés incluent **insertion** et **suppression** file d’attente de messages, ainsi que **création**, **suppression**et **la récupération des files d’attente**.</span><span class="sxs-lookup"><span data-stu-id="54f74-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="54f74-362">Comment toocreate une file d’attente</span><span class="sxs-lookup"><span data-stu-id="54f74-362">How toocreate a queue</span></span>
<span data-ttu-id="54f74-363">Hello exemple suivant établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-364">Ensuite, il appelle [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) toocreate de l’applet de commande une file d’attente nommée 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="54f74-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="54f74-365">Pour plus d’informations sur les conventions d’affectation de noms pour le service de File d’attente Azure, consultez la page [Affectation de noms pour les files d’attente et les métadonnées](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="54f74-366">Comment tooretrieve une file d’attente</span><span class="sxs-lookup"><span data-stu-id="54f74-366">How tooretrieve a queue</span></span>
<span data-ttu-id="54f74-367">Vous pouvez interroger et extraire une file d’attente spécifique ou une liste de toutes les files d’attente de hello dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="54f74-368">Hello exemple suivant montre comment une file d’attente spécifiée à l’aide de tooretrieve hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="54f74-369">Si vous appelez hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) applet de commande sans aucun paramètre, il obtient une liste de toutes les files d’attente de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="54f74-370">Comment toodelete une file d’attente</span><span class="sxs-lookup"><span data-stu-id="54f74-370">How toodelete a queue</span></span>
<span data-ttu-id="54f74-371">toodelete une file d’attente et tous les messages hello qu’il contient, applet de commande Remove-AzureStorageQueue de hello appel.</span><span class="sxs-lookup"><span data-stu-id="54f74-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="54f74-372">Bonjour à l’exemple suivant montre comment une file d’attente spécifiée à l’aide de toodelete hello applet de commande Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="54f74-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="54f74-373">Comment tooinsert un message dans une file d’attente</span><span class="sxs-lookup"><span data-stu-id="54f74-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="54f74-374">tooinsert un message dans une file d’attente existante, commencez par créer une nouvelle instance de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="54f74-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="54f74-375">Ensuite, appelez hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="54f74-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="54f74-376">Un CloudQueueMessage peut être créé à partir d'une chaîne (au format UTF-8) ou d'un tableau d'octets.</span><span class="sxs-lookup"><span data-stu-id="54f74-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="54f74-377">Hello, l’exemple suivant montre comment la file d’attente de tooa de message tooadd.</span><span class="sxs-lookup"><span data-stu-id="54f74-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="54f74-378">exemple de Hello établit d’abord une connexion de tooAzure stockage à l’aide du contexte de compte de stockage hello, qui inclut le nom de compte de stockage hello et sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="54f74-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="54f74-379">Ensuite, il récupère la file d’attente spécifiée hello à l’aide de hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="54f74-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="54f74-380">Si la file d’attente hello existe, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) toocreate utilisé une instance de hello est [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="54f74-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="54f74-381">Une version ultérieure, hello exemple appelle hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) méthode sur cette tooadd d’objet de message il file d’attente tooa.</span><span class="sxs-lookup"><span data-stu-id="54f74-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="54f74-382">Voici le code qui Récupère une file d’attente et insère le message de type hello 'MessageInfo' :</span><span class="sxs-lookup"><span data-stu-id="54f74-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="54f74-383">Comment toode la file d’attente à hello message suivant</span><span class="sxs-lookup"><span data-stu-id="54f74-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="54f74-384">Votre code enlève un message d'une file d'attente en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="54f74-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="54f74-385">Lorsque vous appelez hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) (méthode), vous obtenez message de type hello suivante dans une file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54f74-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="54f74-386">Un message retourné à partir de **GetMessage** devient invisible tooany tout autre code de la lecture de messages à partir de cette file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54f74-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="54f74-387">toofinish lors de la suppression du message de salutation à partir de la file d’attente hello, vous devez également appeler hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="54f74-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="54f74-388">Ce processus en deux étapes de la suppression d’un message garantit que si votre code échoue tooprocess qu'un message en raison de la défaillance toohardware ou logiciel, une autre instance de votre code peut obtenir hello même message puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="54f74-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="54f74-389">Votre code appelle **DeleteMessage** juste après le message de salutation a été traité.</span><span class="sxs-lookup"><span data-stu-id="54f74-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="54f74-390">Comment toomanage fichier Azure et les fichiers</span><span class="sxs-lookup"><span data-stu-id="54f74-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="54f74-391">Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole SMB standard de hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="54f74-392">Machines virtuelles Microsoft Azure et les services de cloud computing peuvent partager des données de fichier entre les composants d’application via des partages montés, et des applications locales peuvent accéder à des données de fichier dans un partage via l’API de stockage de fichier hello ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="54f74-393">Pour plus d’informations sur le stockage de fichiers Azure, consultez [Prise en main du stockage de fichiers Azure sous Windows](../storage-dotnet-how-to-use-files.md) et [API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="54f74-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="54f74-394">Comment tooset et la requête analytique de stockage</span><span class="sxs-lookup"><span data-stu-id="54f74-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="54f74-395">Vous pouvez utiliser [Analytique de stockage Azure](../storage-analytics.md) métriques toocollect pour vos comptes de stockage Azure et les données du journal sur les demandes envoyées de compte de stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="54f74-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="54f74-396">Vous pouvez utiliser des mesures toomonitor hello l’intégrité du stockage d’un compte de stockage et le stockage journalisation toodiagnose et résoudre les problèmes avec votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="54f74-397">Vous pouvez configurer la surveillance à l’aide de hello portail Azure ou Windows PowerShell, ou par programme à l’aide de la bibliothèque cliente de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="54f74-398">Stockage de la journalisation produit côté serveur et vous permet de toorecord les détails pour les demandes réussies et échouées dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54f74-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="54f74-399">Ces journaux vous permettent de toosee les détails de la lecture, écriture et les opérations de suppression sur vos tables, files d’attente et objets BLOB ainsi que raisons hello pour les demandes ayant échouées.</span><span class="sxs-lookup"><span data-stu-id="54f74-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="54f74-400">toolearn tooenable et afficher les données des métriques de stockage à l’aide de PowerShell, voir [comment tooenable Storage Metrics à l’aide de PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="54f74-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="54f74-401">toolearn tooenable et récupérer l’enregistrement de stockage des données à l’aide de PowerShell, voir [comment tooenable Storage Logging à l’aide de PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) et [recherche de vos données de journal Storage Logging](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="54f74-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="54f74-402">Pour plus d’informations sur l’utilisation des indicateurs de stockage et les problèmes de stockage tootroubleshoot de journalisation du stockage, consultez [surveillance, diagnostic et résolution des problèmes Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="54f74-403">Mode de partage toomanage Signature d’accès (SAP) et la stratégie d’accès stockée</span><span class="sxs-lookup"><span data-stu-id="54f74-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="54f74-404">Signatures d’accès partagé sont une partie importante de modèle de sécurité hello pour les applications qui utilisent le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="54f74-405">Ils sont utiles pour fournir des autorisations limitées tooyour tooclients stockage compte que vous ne devez pas de clé de compte hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="54f74-406">Par défaut, seul propriétaire du hello hello du compte de stockage peut accéder aux objets BLOB, tables et files d’attente dans ce compte.</span><span class="sxs-lookup"><span data-stu-id="54f74-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="54f74-407">Si votre service ou application doit toomake ces clients disponibles tooother de ressources sans partager votre clé d’accès, vous disposez de trois options :</span><span class="sxs-lookup"><span data-stu-id="54f74-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="54f74-408">Définissez le conteneur toohello l’accès en lecture anonyme d’un conteneur autorisations toopermit et ses objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="54f74-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="54f74-409">Cela n’est pas autorisé pour les tables ou les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="54f74-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="54f74-410">Utiliser une signature d’accès partagé qui accorde toocontainers de droits d’accès restreint, les objets BLOB, les files d’attente et les tables pour un intervalle de temps spécifique.</span><span class="sxs-lookup"><span data-stu-id="54f74-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="54f74-411">Utilisez un tooobtain de stratégie d’accès stockée un niveau supplémentaire de contrôle de signatures d’accès partagé pour un conteneur ou ses objets BLOB, pour une file d’attente ou pour une table.</span><span class="sxs-lookup"><span data-stu-id="54f74-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="54f74-412">Hello stratégie d’accès stockée vous permet de l’heure de début toochange hello, délai d’expiration ou des autorisations pour une signature, ou toorevoke après qu’il a été émise.</span><span class="sxs-lookup"><span data-stu-id="54f74-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="54f74-413">Une signature d’accès partagé peut prendre deux formes :</span><span class="sxs-lookup"><span data-stu-id="54f74-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="54f74-414">**SAS ad hoc**: lorsque vous créez un SAS ad hoc, l’heure de début hello, la durée d’expiration et les autorisations pour hello SAS sont toutes spécifiées sur hello URI SAS.</span><span class="sxs-lookup"><span data-stu-id="54f74-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="54f74-415">Ce type de signature d'accès partagé peut être créé sur un conteneur, un objet blob, une table ou une file d'attente, et il ne peut pas être révoqué.</span><span class="sxs-lookup"><span data-stu-id="54f74-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="54f74-416">**Associations de sécurité avec la stratégie d’accès stockée**: une stratégie d’accès stockée est définie sur un conteneur de ressources un conteneur d’objets blob, une table ou une file d’attente - et vous pouvez l’utiliser toomanage contraintes pour une ou plusieurs signatures d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="54f74-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="54f74-417">Lorsque vous associez un SAS avec une stratégie d’accès stockée, hello SAS hérite des contraintes de hello - hello heure de début, date d’expiration et autorisations - définies pour la stratégie d’accès stockée hello.</span><span class="sxs-lookup"><span data-stu-id="54f74-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="54f74-418">Ce type de signature d'accès partagé peut être révoqué.</span><span class="sxs-lookup"><span data-stu-id="54f74-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="54f74-419">Pour plus d’informations, consultez [à l’aide de Signatures SAP (accès partagé)](../storage-dotnet-shared-access-signature-part-1.md) et [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="54f74-420">Dans les sections suivantes de hello, vous allez apprendre comment toocreate une stratégie d’accès stockée et de jeton de signature accès partagé pour les tables Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="54f74-421">PowerShell Azure fournit aussi des applets de commande semblables pour les conteneurs, les objets blob et les files d'attente.</span><span class="sxs-lookup"><span data-stu-id="54f74-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="54f74-422">scripts de hello toorun dans cette section, télécharger hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="54f74-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="54f74-423">Comment jeton de Signature d’accès partagé toocreate basée sur des stratégies</span><span class="sxs-lookup"><span data-stu-id="54f74-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="54f74-424">Utilisez toocreate d’applet de commande New-AzureStorageTableStoredAccessPolicy hello une stratégie d’accès stockée.</span><span class="sxs-lookup"><span data-stu-id="54f74-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="54f74-425">Ensuite, appelez hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate de l’applet de commande un nouveau jeton de signature basée sur des stratégies d’accès partagé pour une table de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54f74-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="54f74-426">Comment toocreate un jeton de Signature d’accès partagé ad hoc (non révocables)</span><span class="sxs-lookup"><span data-stu-id="54f74-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="54f74-427">Hello d’utilisation [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) toocreate de l’applet de commande un nouveau jeton de Signature d’accès partagé de (non révocables) ad hoc pour une table de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="54f74-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="54f74-428">Comment toocreate une stratégie d’accès stockée</span><span class="sxs-lookup"><span data-stu-id="54f74-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="54f74-429">Utilisez toocreate d’applet de commande hello AzureStorageTableStoredAccessPolicy de nouveau une stratégie d’accès stockée pour une table de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="54f74-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="54f74-430">Comment tooupdate une stratégie d’accès stockée</span><span class="sxs-lookup"><span data-stu-id="54f74-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="54f74-431">Utilisez tooupdate d’applet de commande Set-AzureStorageTableStoredAccessPolicy hello une stratégie d’accès stockée existante pour une table de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="54f74-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="54f74-432">Comment toodelete une stratégie d’accès stockée</span><span class="sxs-lookup"><span data-stu-id="54f74-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="54f74-433">Utilisez toodelete d’applet de commande hello AzureStorageTableStoredAccessPolicy de supprimer une stratégie d’accès stockée sur une table de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="54f74-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="54f74-434">Comment toouse le stockage Azure pour le gouvernement des États-Unis et Azure Chine</span><span class="sxs-lookup"><span data-stu-id="54f74-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="54f74-435">Un environnement Azure est un déploiement indépendant de Microsoft Azure, par exemple [Azure Government pour le gouvernement des États-Unis](https://azure.microsoft.com/features/gov/), [AzureCloud pour Azure global](https://portal.azure.com) et [AzureChinaCloud pour Azure exploité par 21Vianet en Chine](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="54f74-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="54f74-436">Vous pouvez déployer de nouveaux environnements Azure pour le gouvernement des États-Unis et Azure en Chine.</span><span class="sxs-lookup"><span data-stu-id="54f74-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="54f74-437">toouse le stockage Azure avec AzureChinaCloud, vous devez toocreate un contexte de stockage qui est associé à AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="54f74-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="54f74-438">Suivez ces tooget étapes que vous avez démarré :</span><span class="sxs-lookup"><span data-stu-id="54f74-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="54f74-439">Exécutez hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee de l’applet de commande hello environnements Azure disponibles :</span><span class="sxs-lookup"><span data-stu-id="54f74-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="54f74-440">Ajouter un tooWindows de compte Azure Chine PowerShell :</span><span class="sxs-lookup"><span data-stu-id="54f74-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="54f74-441">Créez un contexte de stockage pour un compte AzureChinaCloud :</span><span class="sxs-lookup"><span data-stu-id="54f74-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="54f74-442">toouse Azure Storage avec [des États-Unis pour le gouvernement des États-Unis](https://azure.microsoft.com/features/gov/), vous devez définir un nouvel environnement, puis créer un contexte de stockage avec cet environnement :</span><span class="sxs-lookup"><span data-stu-id="54f74-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="54f74-443">Exécutez hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee de l’applet de commande hello environnements Azure disponibles :</span><span class="sxs-lookup"><span data-stu-id="54f74-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="54f74-444">Ajouter un tooWindows de compte Azure du gouvernement PowerShell :</span><span class="sxs-lookup"><span data-stu-id="54f74-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="54f74-445">Créez un contexte de stockage pour un compte Azure pour le gouvernement américain :</span><span class="sxs-lookup"><span data-stu-id="54f74-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="54f74-446">Pour plus d'informations, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="54f74-446">For more information, see:</span></span>

* <span data-ttu-id="54f74-447">[Guide du développeur Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="54f74-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="54f74-448">Vue d'ensemble des différences lors de la création d'une application sur le service Chine</span><span class="sxs-lookup"><span data-stu-id="54f74-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="54f74-449">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54f74-449">Next Steps</span></span>
<span data-ttu-id="54f74-450">Dans ce guide, vous avez appris comment toomanage le stockage Azure avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f74-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="54f74-451">Pour en savoir plus, consultez les articles et ressources suivants :</span><span class="sxs-lookup"><span data-stu-id="54f74-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="54f74-452">Documentation d'Azure Storage</span><span class="sxs-lookup"><span data-stu-id="54f74-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="54f74-453">Applets de commande Azure Storage PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f74-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="54f74-454">Référence Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="54f74-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
