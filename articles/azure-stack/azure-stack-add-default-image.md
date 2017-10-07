---
title: "marketplace Azure pile toohello de la machine virtuelle par défaut aaaAdd hello image | Documents Microsoft"
description: "Ajoutez le marketplace de la pile de Azure hello machine virtuelle de Windows Server 2016 par défaut image toohello."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a><span data-ttu-id="bc2cc-103">Ajouter le marketplace Azure pile toohello hello Windows Server 2016 VM image</span><span class="sxs-lookup"><span data-stu-id="bc2cc-103">Add hello Windows Server 2016 VM image toohello Azure Stack marketplace</span></span>

<span data-ttu-id="bc2cc-104">Par défaut, il ne sont pas toutes les images de machine virtuelle disponibles dans le marketplace d’Azure pile hello.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-104">By default, there aren’t any virtual machine images available in hello Azure Stack marketplace.</span></span> <span data-ttu-id="bc2cc-105">administrateur du cloud Azure pile Hello doit ajouter un marketplace toohello d’image avant que les utilisateurs peuvent les utiliser.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-105">hello Azure Stack cloud administrator must add an image toohello marketplace before users can use them.</span></span> <span data-ttu-id="bc2cc-106">Vous pouvez ajouter le marketplace d’Azure pile hello Windows Server 2016 image toohello à l’aide d’une des deux méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-106">You can add hello Windows Server 2016 image toohello Azure Stack marketplace by using one of hello following two methods:</span></span>

* <span data-ttu-id="bc2cc-107">[Ajouter l’image de hello en le téléchargeant à partir d’Azure Marketplace de hello](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -Utilisez cette option si vous opérez dans un scénario connecté et si vous avez enregistré votre instance de la pile d’Azure avec Azure.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-107">[Add hello image by downloading it from hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="bc2cc-108">[Ajouter l’image de hello à l’aide de PowerShell](#add-the-image-by-using-powershell) -Utilisez cette option si vous avez déployé Azure pile dans un scénario déconnecté ou dans des scénarios avec une connectivité limitée.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-108">[Add hello image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a><span data-ttu-id="bc2cc-109">Ajouter l’image de hello en le téléchargeant à partir de hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="bc2cc-109">Add hello image by downloading it from hello Azure Marketplace</span></span>

1. <span data-ttu-id="bc2cc-110">Après avoir déployé la pile d’Azure, connectez-vous tooyour Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-110">After deploying Azure Stack, sign in tooyour Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="bc2cc-111">Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure**</span><span class="sxs-lookup"><span data-stu-id="bc2cc-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="bc2cc-112">Rechercher ou pour hello **Windows Server Datacenter 2016 – Eval** image > cliquez sur **télécharger**</span><span class="sxs-lookup"><span data-stu-id="bc2cc-112">Find or search for hello **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Télécharger l’image à partir d’Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="bc2cc-114">Une fois le téléchargement de hello terminé, hello image ajoutée toohello **Marketplace gestion** lame et il est également accessible à partir de hello **virtuels** panneau.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-114">After hello download completes, hello image is added toohello **Marketplace Management** blade and it is also made available from hello **Virtual Machines** blade.</span></span>

## <a name="add-hello-image-by-using-powershell"></a><span data-ttu-id="bc2cc-115">Ajouter l’image de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc2cc-115">Add hello image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bc2cc-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bc2cc-116">Prerequisites</span></span> 

<span data-ttu-id="bc2cc-117">Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="bc2cc-117">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="bc2cc-118">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="bc2cc-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="bc2cc-119">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="bc2cc-119">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="bc2cc-120">Accédez toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 et télécharger version d’évaluation de Windows Server 2016 de hello.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-120">Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download hello Windows Server 2016 evaluation.</span></span> <span data-ttu-id="bc2cc-121">Lorsque vous y êtes invité, sélectionnez hello **ISO** version du téléchargement de hello.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-121">When prompted, select hello **ISO** version of hello download.</span></span> <span data-ttu-id="bc2cc-122">Toohello de chemin d’accès d’enregistrement hello téléchargement, qui est utilisé ultérieurement dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-122">Record hello path toohello download location, which is used later in these steps.</span></span> <span data-ttu-id="bc2cc-123">Cette étape nécessite une connectivité Internet.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="bc2cc-124">Maintenant, exécutez hello suivant marketplace de la pile de Azure étapes tooadd hello image toohello :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-124">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="bc2cc-125">Importez les modules Azure Connect de pile et ComputeAdmin hello à l’aide de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-125">Import hello Azure Stack Connect and ComputeAdmin modules by using hello following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="bc2cc-126">Se connecter tooyour environnement Azure pile.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-126">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="bc2cc-127">De script suivante d’exécution hello selon si votre environnement Azure pile est déployé à l’aide d’AAD ou ADFS (Assurez-vous que tooreplace hello AAD nom_client) :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-127">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span>  

   <span data-ttu-id="bc2cc-128">a.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-128">a.</span></span> <span data-ttu-id="bc2cc-129">**Azure Active Directory**, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-129">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="bc2cc-130">b.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-130">b.</span></span> <span data-ttu-id="bc2cc-131">**Active Directory Federation Services**, utilisez hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-131">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="bc2cc-132">Ajouter le marketplace d’Azure pile hello Windows Server 2016 image toohello (Assurez-vous que tooreplace hello *Path_to_ISO* avec le chemin d’accès de hello toohello ISO WS2016 vous avez téléchargé) :</span><span class="sxs-lookup"><span data-stu-id="bc2cc-132">Add hello Windows Server 2016 image toohello Azure Stack marketplace (Make sure tooreplace hello *Path_to_ISO* with hello path toohello WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="bc2cc-133">tooensure qui hello image de machine virtuelle de Windows Server 2016 a hello dernière mise à jour cumulative, inclure hello `IncludeLatestCU` paramètre lors de l’exécution hello `New-AzsServer2016VMImage` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-133">tooensure that hello Windows Server 2016 VM image has hello latest cumulative update, include hello `IncludeLatestCU` parameter when running hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="bc2cc-134">Consultez hello [paramètres](#parameters) section pour plus d’informations sur les paramètres autorisés pour hello `New-AzsServer2016VMImage` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-134">See hello [Parameters](#parameters) section for information about allowed parameters for hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="bc2cc-135">Cela prend environ un marketplace d’Azure pile toohello image heure toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-135">It takes about an hour toopublish hello image toohello Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="bc2cc-136">Paramètres</span><span class="sxs-lookup"><span data-stu-id="bc2cc-136">Parameters</span></span>

|<span data-ttu-id="bc2cc-137">Paramètres New-AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="bc2cc-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="bc2cc-138">Requis ?</span><span class="sxs-lookup"><span data-stu-id="bc2cc-138">Required?</span></span>|<span data-ttu-id="bc2cc-139">Description</span><span class="sxs-lookup"><span data-stu-id="bc2cc-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="bc2cc-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="bc2cc-140">ISOPath</span></span>|<span data-ttu-id="bc2cc-141">Oui</span><span class="sxs-lookup"><span data-stu-id="bc2cc-141">Yes</span></span>|<span data-ttu-id="bc2cc-142">Hello toohello de chemin d’accès complet de télécharger Windows Server 2016 ISO.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-142">hello fully qualified path toohello downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="bc2cc-143">Net35</span><span class="sxs-lookup"><span data-stu-id="bc2cc-143">Net35</span></span>|<span data-ttu-id="bc2cc-144">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-144">No</span></span>|<span data-ttu-id="bc2cc-145">Ce paramètre vous permet de runtime de .NET 3.5 hello tooinstall sur l’image de Windows Server 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-145">This parameter allows you tooinstall hello .NET 3.5 runtime on hello Windows Server 2016 image.</span></span> <span data-ttu-id="bc2cc-146">Par défaut, cette valeur est définie à tootrue.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-146">By default, this value is set tootrue.</span></span> <span data-ttu-id="bc2cc-147">Il est obligatoire de que cette image hello contient hello .NET 3.5 runtime tooinstall hello SQL et MYSQL fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-147">It is mandatory that hello image contains hello .NET 3.5 runtime tooinstall hello SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="bc2cc-148">Version</span><span class="sxs-lookup"><span data-stu-id="bc2cc-148">Version</span></span>|<span data-ttu-id="bc2cc-149">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-149">No</span></span>|<span data-ttu-id="bc2cc-150">Ce paramètre vous permet de toochoose si tooadd un **Core** ou **complète** ou **les deux** les images Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-150">This parameter allows you toochoose whether tooadd a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="bc2cc-151">Par défaut, cette valeur est définie trop « Full ».</span><span class="sxs-lookup"><span data-stu-id="bc2cc-151">By default, this value is set too"Full."</span></span>|
|<span data-ttu-id="bc2cc-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="bc2cc-152">VHDSizeInMB</span></span>|<span data-ttu-id="bc2cc-153">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-153">No</span></span>|<span data-ttu-id="bc2cc-154">Hello taille taille (en Mo) de hello VHD image toobe ajouté environnement de Azure pile tooyour.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-154">Sets hello size (in MB) of hello VHD image toobe added tooyour Azure Stack environment.</span></span> <span data-ttu-id="bc2cc-155">Par défaut, cette valeur est définie à too40960 Mo.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-155">By default, this value is set too40960 MB.</span></span>|
|<span data-ttu-id="bc2cc-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="bc2cc-156">CreateGalleryItem</span></span>|<span data-ttu-id="bc2cc-157">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-157">No</span></span>|<span data-ttu-id="bc2cc-158">Spécifie si un élément du Marketplace doit être créé pour l’image de hello Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-158">Specifies if a Marketplace item should be created for hello Windows Server 2016 image.</span></span> <span data-ttu-id="bc2cc-159">Par défaut, cette valeur est définie à tootrue.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-159">By default, this value is set tootrue.</span></span>|
|<span data-ttu-id="bc2cc-160">location</span><span class="sxs-lookup"><span data-stu-id="bc2cc-160">location</span></span> |<span data-ttu-id="bc2cc-161">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-161">No</span></span> |<span data-ttu-id="bc2cc-162">Spécifie l’image de Windows Server 2016 hello emplacement toowhich hello doit être publiée.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-162">Specifies hello location toowhich hello Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="bc2cc-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="bc2cc-163">IncludeLatestCU</span></span>|<span data-ttu-id="bc2cc-164">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-164">No</span></span>|<span data-ttu-id="bc2cc-165">Définissez cette toohello mise à jour cumulative de Windows Server 2016 plus récente de commutateur tooapply hello nouveau disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-165">Set this switch tooapply hello latest Windows Server 2016 cumulative update toohello new VHD.</span></span>|
|<span data-ttu-id="bc2cc-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="bc2cc-166">CUUri</span></span> |<span data-ttu-id="bc2cc-167">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-167">No</span></span> |<span data-ttu-id="bc2cc-168">Définissez cette mise à jour cumulative valeur toochoose hello Windows Server 2016 à partir d’un URI spécifique.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-168">Set this value toochoose hello Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="bc2cc-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="bc2cc-169">CUPath</span></span> |<span data-ttu-id="bc2cc-170">Non</span><span class="sxs-lookup"><span data-stu-id="bc2cc-170">No</span></span> |<span data-ttu-id="bc2cc-171">Définissez cette mise à jour cumulative valeur toochoose hello Windows Server 2016 à partir d’un chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-171">Set this value toochoose hello Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="bc2cc-172">Cette option est utile si vous avez déployé instance d’Azure pile hello dans un environnement déconnecté.</span><span class="sxs-lookup"><span data-stu-id="bc2cc-172">This option is helpful if you have deployed hello Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="bc2cc-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc2cc-173">Next steps</span></span>

[<span data-ttu-id="bc2cc-174">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bc2cc-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
