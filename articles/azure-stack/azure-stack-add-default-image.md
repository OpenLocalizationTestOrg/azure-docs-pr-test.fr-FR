---
title: "Ajouter l’image de machine virtuelle par défaut sur la Place de marché Azure Stack | Microsoft Docs"
description: "Ajoutez l’image de machine virtuelle Windows Server 2016 par défaut sur la Place de marché Azure Stack."
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
ms.openlocfilehash: 43781cb025865df1d228376f57412f3d482d3ad0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="6ba97-103">Ajouter l’image de machine virtuelle Windows Server 2016 sur la Place de marché Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6ba97-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="6ba97-104">Par défaut, il n’y a pas d’images de machine virtuelle disponibles sur la Place de marché Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6ba97-104">By default, there aren’t any virtual machine images available in the Azure Stack marketplace.</span></span> <span data-ttu-id="6ba97-105">L’opérateur Azure Stack doit ajouter préalablement une image sur la Place de marché pour la mettre à la disposition des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6ba97-105">The Azure Stack operator must add an image to the marketplace before users can use them.</span></span> <span data-ttu-id="6ba97-106">Vous pouvez ajouter l’image Windows Server 2016 sur la Place de marché Azure Stack à l’aide d’une des deux méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ba97-106">You can add the Windows Server 2016 image to the Azure Stack marketplace by using one of the following two methods:</span></span>

* <span data-ttu-id="6ba97-107">[Ajouter l’image en la téléchargeant à partir de la Place de marché Azure](#add-the-image-by-downloading-it-from-the-Azure-marketplace) : choisissez cette méthode si vous êtes dans un scénario connecté et si vous avez inscrit votre instance Azure Stack auprès d’Azure.</span><span class="sxs-lookup"><span data-stu-id="6ba97-107">[Add the image by downloading it from the Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="6ba97-108">[Ajouter l’image à l’aide de PowerShell](#add-the-image-by-using-powershell) : choisissez cette méthode si vous avez déployé Azure Stack dans un scénario déconnecté ou avec une connectivité limitée.</span><span class="sxs-lookup"><span data-stu-id="6ba97-108">[Add the image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a><span data-ttu-id="6ba97-109">Ajouter l’image en la téléchargeant à partir de la Place de marché Azure</span><span class="sxs-lookup"><span data-stu-id="6ba97-109">Add the image by downloading it from the Azure Marketplace</span></span>

1. <span data-ttu-id="6ba97-110">Après avoir déployé Azure Stack, connectez-vous à votre Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6ba97-110">After deploying Azure Stack, sign in to your Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="6ba97-111">Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure**</span><span class="sxs-lookup"><span data-stu-id="6ba97-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="6ba97-112">Localisez ou recherchez l’image **Windows Server Datacenter 2016 – Évaluations** et cliquez sur **Télécharger**</span><span class="sxs-lookup"><span data-stu-id="6ba97-112">Find or search for the **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Télécharger l’image à partir d’Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="6ba97-114">Une fois son téléchargement terminé, l’image est ajoutée au panneau **Gestion de la Place de Marché** et au panneau **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="6ba97-114">After the download completes, the image is added to the **Marketplace Management** blade and it is also made available from the **Virtual Machines** blade.</span></span>

## <a name="add-the-image-by-using-powershell"></a><span data-ttu-id="6ba97-115">Ajouter l’image à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ba97-115">Add the image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6ba97-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6ba97-116">Prerequisites</span></span> 

<span data-ttu-id="6ba97-117">Effectuez les étapes prérequises suivantes à partir du [Kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) ou à partir d’un client externe Windows si vous êtes [connecté par le biais d’un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) :</span><span class="sxs-lookup"><span data-stu-id="6ba97-117">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="6ba97-118">Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="6ba97-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="6ba97-119">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="6ba97-119">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="6ba97-120">Accédez à https://www.microsoft.com/fr-fr/evalcenter/evaluate-windows-server-2016 et téléchargez la version d’évaluation de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ba97-120">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="6ba97-121">Quand vous y êtes invité, sélectionnez la version **ISO** du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="6ba97-121">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="6ba97-122">Enregistrez le chemin d’accès à l’emplacement de téléchargement, car vous en aurez besoin plus tard dans cette procédure.</span><span class="sxs-lookup"><span data-stu-id="6ba97-122">Record the path to the download location, which is used later in these steps.</span></span> <span data-ttu-id="6ba97-123">Cette étape nécessite une connectivité Internet.</span><span class="sxs-lookup"><span data-stu-id="6ba97-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="6ba97-124">Effectuez maintenant les étapes suivantes pour ajouter l’image sur la Place de marché Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="6ba97-124">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="6ba97-125">Importez les modules Azure Stack Connect et ComputeAdmin à l’aide des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ba97-125">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="6ba97-126">Connectez-vous à votre environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6ba97-126">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="6ba97-127">Exécutez le script suivant en fonction du type de déploiement de votre environnement Azure Stack : AAD ou AD FS (veillez à remplacer les valeurs tenantName AAD, le point de terminaison GraphAudience et la valeur ArmEndpoint conformément à la configuration de votre environnement) :</span><span class="sxs-lookup"><span data-stu-id="6ba97-127">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenantName, GraphAudience endpoint and ArmEndpoint values as per your environment configuration):</span></span>  

   <span data-ttu-id="6ba97-128">a.</span><span class="sxs-lookup"><span data-stu-id="6ba97-128">a.</span></span> <span data-ttu-id="6ba97-129">Pour **AAD**, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6ba97-129">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"
   
   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="6ba97-130">b.</span><span class="sxs-lookup"><span data-stu-id="6ba97-130">b.</span></span> <span data-ttu-id="6ba97-131">Pour **AD FS**, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6ba97-131">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="6ba97-132">Ajoutez l’image Windows Server 2016 sur la Place de marché Azure Stack (sans oublier de remplacer la variable *Path_to_ISO* par le chemin d’accès à l’image ISO WS2016 que vous avez téléchargée) :</span><span class="sxs-lookup"><span data-stu-id="6ba97-132">Add the Windows Server 2016 image to the Azure Stack marketplace (Make sure to replace the *Path_to_ISO* with the path to the WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="6ba97-133">Pour vous assurer que l’image de machine virtuelle Windows Server 2016 contient la dernière mise à jour cumulative, incluez le paramètre `IncludeLatestCU` dans l’applet de commande `New-AzsServer2016VMImage` que vous allez exécuter.</span><span class="sxs-lookup"><span data-stu-id="6ba97-133">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the `IncludeLatestCU` parameter when running the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="6ba97-134">Consultez la section [Paramètres](#parameters) pour plus d’informations sur les paramètres autorisés dans l’applet de commande `New-AzsServer2016VMImage`.</span><span class="sxs-lookup"><span data-stu-id="6ba97-134">See the [Parameters](#parameters) section for information about allowed parameters for the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="6ba97-135">La publication de l’image sur la Place de marché Azure Stack prend environ une heure.</span><span class="sxs-lookup"><span data-stu-id="6ba97-135">It takes about an hour to publish the image to the Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="6ba97-136">Paramètres</span><span class="sxs-lookup"><span data-stu-id="6ba97-136">Parameters</span></span>

|<span data-ttu-id="6ba97-137">Paramètres New-AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="6ba97-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="6ba97-138">Requis ?</span><span class="sxs-lookup"><span data-stu-id="6ba97-138">Required?</span></span>|<span data-ttu-id="6ba97-139">Description</span><span class="sxs-lookup"><span data-stu-id="6ba97-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="6ba97-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="6ba97-140">ISOPath</span></span>|<span data-ttu-id="6ba97-141">Oui</span><span class="sxs-lookup"><span data-stu-id="6ba97-141">Yes</span></span>|<span data-ttu-id="6ba97-142">Spécifie le chemin d’accès complet à l’image ISO Windows Server 2016 téléchargée.</span><span class="sxs-lookup"><span data-stu-id="6ba97-142">The fully qualified path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="6ba97-143">Net35</span><span class="sxs-lookup"><span data-stu-id="6ba97-143">Net35</span></span>|<span data-ttu-id="6ba97-144">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-144">No</span></span>|<span data-ttu-id="6ba97-145">Ce paramètre vous permet d’installer le Runtime .NET 3.5 sur l’image Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ba97-145">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="6ba97-146">Par défaut, cette valeur est définie sur true.</span><span class="sxs-lookup"><span data-stu-id="6ba97-146">By default, this value is set to true.</span></span>|
|<span data-ttu-id="6ba97-147">Version</span><span class="sxs-lookup"><span data-stu-id="6ba97-147">Version</span></span>|<span data-ttu-id="6ba97-148">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-148">No</span></span>|<span data-ttu-id="6ba97-149">Ce paramètre vous permet de choisir l’option d’installation des images Windows Server 2016 : **Base**, **Complète** ou **Les deux**.</span><span class="sxs-lookup"><span data-stu-id="6ba97-149">This parameter allows you to choose whether to add a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="6ba97-150">Par défaut, cette valeur est définie sur Complète.</span><span class="sxs-lookup"><span data-stu-id="6ba97-150">By default, this value is set to "Full."</span></span>|
|<span data-ttu-id="6ba97-151">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="6ba97-151">VHDSizeInMB</span></span>|<span data-ttu-id="6ba97-152">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-152">No</span></span>|<span data-ttu-id="6ba97-153">Définit la taille (en Mo) de l’image VHD à ajouter à votre environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6ba97-153">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="6ba97-154">Par défaut, cette valeur est définie sur 40 960 Mo.</span><span class="sxs-lookup"><span data-stu-id="6ba97-154">By default, this value is set to 40960 MB.</span></span>|
|<span data-ttu-id="6ba97-155">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="6ba97-155">CreateGalleryItem</span></span>|<span data-ttu-id="6ba97-156">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-156">No</span></span>|<span data-ttu-id="6ba97-157">Spécifie si un élément de la Place de marché doit être créé pour l’image Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ba97-157">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="6ba97-158">Par défaut, cette valeur est définie sur true.</span><span class="sxs-lookup"><span data-stu-id="6ba97-158">By default, this value is set to true.</span></span>|
|<span data-ttu-id="6ba97-159">location</span><span class="sxs-lookup"><span data-stu-id="6ba97-159">location</span></span> |<span data-ttu-id="6ba97-160">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-160">No</span></span> |<span data-ttu-id="6ba97-161">Spécifie l’emplacement de publication de l’image Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="6ba97-161">Specifies the location to which the Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="6ba97-162">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="6ba97-162">IncludeLatestCU</span></span>|<span data-ttu-id="6ba97-163">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-163">No</span></span>|<span data-ttu-id="6ba97-164">Ce paramètre vous permet d’appliquer la dernière mise à jour cumulative de Windows Server 2016 à la nouvelle image VHD.</span><span class="sxs-lookup"><span data-stu-id="6ba97-164">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="6ba97-165">CUUri</span><span class="sxs-lookup"><span data-stu-id="6ba97-165">CUUri</span></span> |<span data-ttu-id="6ba97-166">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-166">No</span></span> |<span data-ttu-id="6ba97-167">Ce paramètre vous permet de choisir la mise à jour cumulative de Windows Server 2016 à partir d’un URI spécifique.</span><span class="sxs-lookup"><span data-stu-id="6ba97-167">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="6ba97-168">CUPath</span><span class="sxs-lookup"><span data-stu-id="6ba97-168">CUPath</span></span> |<span data-ttu-id="6ba97-169">Non</span><span class="sxs-lookup"><span data-stu-id="6ba97-169">No</span></span> |<span data-ttu-id="6ba97-170">Ce paramètre vous permet de choisir la mise à jour cumulative de Windows Server 2016 à partir d’un chemin d’accès local.</span><span class="sxs-lookup"><span data-stu-id="6ba97-170">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="6ba97-171">Ce paramètre est utile si vous avez déployé l’instance Azure Stack dans un environnement déconnecté.</span><span class="sxs-lookup"><span data-stu-id="6ba97-171">This option is helpful if you have deployed the Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6ba97-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ba97-172">Next steps</span></span>

[<span data-ttu-id="6ba97-173">Approvisionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6ba97-173">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
