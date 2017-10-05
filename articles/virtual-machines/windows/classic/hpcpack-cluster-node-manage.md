---
title: "Gérer les nœuds de calcul de cluster HPC Pack | Microsoft Docs"
description: "En savoir plus sur les outils de script PowerShell pour ajouter, supprimer, démarrer et arrêter des nœuds de calcul de cluster HPC Pack 2012 R2 dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="2c75a-103">Gérer le nombre et la disponibilité des nœuds de calcul dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="2c75a-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="2c75a-104">Une fois un cluster HPC Pack 2012 R2 créé dans des machines virtuelles Azure, il peut s’avérer utile de pouvoir facilement ajouter, supprimer, démarrer (approvisionner) ou arrêter (annuler l’approvisionnement) certaines machines virtuelles à nœud de calcul dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="2c75a-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="2c75a-105">Pour effectuer ces tâches, exécutez des scripts Azure PowerShell qui sont installés sur la machine virtuelle à nœud principal.</span><span class="sxs-lookup"><span data-stu-id="2c75a-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="2c75a-106">Ces scripts vous aident à contrôler le nombre et la disponibilité de vos ressources de cluster HPC Pack afin de contrôler les coûts.</span><span class="sxs-lookup"><span data-stu-id="2c75a-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2c75a-107">Cet article s’applique uniquement aux clusters HPC Pack 2012 R2 dans Azure créés à l’aide du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="2c75a-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="2c75a-108">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c75a-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="2c75a-109">En outre, les scripts PowerShell décrits dans cet article ne sont pas disponibles dans HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="2c75a-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c75a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2c75a-110">Prerequisites</span></span>
* <span data-ttu-id="2c75a-111">**Cluster HPC Pack 2012 R2 dans des machines virtuelles Azure** : créez un cluster HPC Pack 2012 R2 dans le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="2c75a-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="2c75a-112">Par exemple, vous pouvez automatiser le déploiement à l’aide de l’image de machine virtuelle de HPC Pack 2012 R2 dans Azure Marketplace et un script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c75a-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="2c75a-113">Pour plus d’informations, y compris concernant la configuration requise, consultez [Créer un cluster HPC avec le script de déploiement HPC Pack IaaS](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="2c75a-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="2c75a-114">Après le déploiement, trouvez les scripts de gestion de nœud dans le dossier %CCP\_HOME%bin sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="2c75a-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="2c75a-115">Exécutez chacun des scripts en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2c75a-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="2c75a-116">**Fichier de paramètres de publication ou certificat de gestion Azure** : vous devez effectuer l’une des opérations suivantes sur le nœud principal :</span><span class="sxs-lookup"><span data-stu-id="2c75a-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="2c75a-117">**Importer le fichier de publication de paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="2c75a-118">Pour ce faire, exécutez les applets de commande Azure PowerShell suivantes sur le nœud principal :</span><span class="sxs-lookup"><span data-stu-id="2c75a-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="2c75a-119">**Configurez le certificat de gestion Azure sur le nœud principal**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="2c75a-120">Si vous disposez du fichier .cer, importez-le dans le magasin de certificats CurrentUser\My, puis exécutez l’applet de commande Azure PowerShell suivante pour votre environnement Azure (AzureCloud ou AzureChinaCloud) :</span><span class="sxs-lookup"><span data-stu-id="2c75a-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="2c75a-121">Ajouter des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="2c75a-121">Add compute node VMs</span></span>
<span data-ttu-id="2c75a-122">Ajoutez des nœuds de calcul avec le script **Add-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="2c75a-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2c75a-123">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c75a-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="2c75a-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2c75a-124">Parameters</span></span>
* <span data-ttu-id="2c75a-125">**ServiceName** : nom du service cloud auquel les nouvelles machines virtuelles à nœud de calcul sont ajoutées.</span><span class="sxs-lookup"><span data-stu-id="2c75a-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="2c75a-126">**ImageName** : nom de l’image de machine virtuelle Azure, qui peut être obtenu par le biais du Portail Azure Classic ou de l’applet de commande Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="2c75a-127">L’image doit répondre aux exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="2c75a-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="2c75a-128">Un système d’exploitation Windows doit être installé.</span><span class="sxs-lookup"><span data-stu-id="2c75a-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="2c75a-129">HPC Pack doit être installé dans le rôle de nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="2c75a-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="2c75a-130">L’image doit être une image privée dans la catégorie Utilisateur, et non une image de machine virtuelle Azure publique.</span><span class="sxs-lookup"><span data-stu-id="2c75a-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="2c75a-131">**Quantity** : nombre de machines virtuelles à nœud de calcul à ajouter.</span><span class="sxs-lookup"><span data-stu-id="2c75a-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="2c75a-132">**InstanceSize** : taille des machines virtuelles à nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="2c75a-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="2c75a-133">**DomainUserName** : nom d’utilisateur de domaine utilisé pour joindre les nouvelles machines virtuelles au domaine.</span><span class="sxs-lookup"><span data-stu-id="2c75a-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="2c75a-134">**DomainUserPassword** : mot de passe de l’utilisateur de domaine.</span><span class="sxs-lookup"><span data-stu-id="2c75a-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="2c75a-135">**NodeNameSeries** (facultatif) : modèle d’affectation de noms pour les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="2c75a-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="2c75a-136">Le format doit être le suivant : &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="2c75a-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="2c75a-137">Par exemple, MyCN%10% représente une série de noms de nœud de calcul commençant par MyCN11.</span><span class="sxs-lookup"><span data-stu-id="2c75a-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="2c75a-138">Si ce paramètre n’est pas spécifié, le script utilise la série d’affectation de noms configurée dans le cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="2c75a-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="2c75a-139">Exemple</span><span class="sxs-lookup"><span data-stu-id="2c75a-139">Example</span></span>
<span data-ttu-id="2c75a-140">L’exemple suivant ajoute 20 machines virtuelles à nœud de calcul de grande taille au service cloud *hpcservice1*, en se basant sur l’image de machine virtuelle *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="2c75a-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="2c75a-141">Supprimer des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="2c75a-141">Remove compute node VMs</span></span>
<span data-ttu-id="2c75a-142">Supprimez des nœuds de calcul avec le script **Remove-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="2c75a-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2c75a-143">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c75a-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="2c75a-144">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2c75a-144">Parameters</span></span>
* <span data-ttu-id="2c75a-145">**Name** : noms des nœuds de cluster à supprimer.</span><span class="sxs-lookup"><span data-stu-id="2c75a-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="2c75a-146">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2c75a-146">Wildcards are supported.</span></span> <span data-ttu-id="2c75a-147">Le nom du jeu de paramètres est Name.</span><span class="sxs-lookup"><span data-stu-id="2c75a-147">The parameter set name is Name.</span></span> <span data-ttu-id="2c75a-148">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2c75a-149">**Nœud** : objet HpcNode des nœuds à supprimer, qui peut être obtenu par le biais de l’applet de commande HPC PowerShell [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c75a-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2c75a-150">Le nom du jeu de paramètres est Node.</span><span class="sxs-lookup"><span data-stu-id="2c75a-150">The parameter set name is Node.</span></span> <span data-ttu-id="2c75a-151">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2c75a-152">**DeleteVHD** (facultatif) : permet de supprimer les disques associés aux machines virtuelles qui sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="2c75a-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="2c75a-153">**Force** (facultatif) : permet de mettre les nœuds HPC hors connexion avant de les supprimer.</span><span class="sxs-lookup"><span data-stu-id="2c75a-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="2c75a-154">**Confirm** (facultatif) : permet d’inviter à confirmer avant d’exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="2c75a-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="2c75a-155">**WhatIf** : permet de décrire l’exécution de la commande sans l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="2c75a-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="2c75a-156">Exemple</span><span class="sxs-lookup"><span data-stu-id="2c75a-156">Example</span></span>
<span data-ttu-id="2c75a-157">L’exemple suivant met hors connexion les nœuds dont le nom commence par *HPCNode-CN-* , puis supprime les nœuds et leurs disques associés.</span><span class="sxs-lookup"><span data-stu-id="2c75a-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="2c75a-158">Démarrer des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="2c75a-158">Start compute node VMs</span></span>
<span data-ttu-id="2c75a-159">Démarrez des nœuds de calcul avec le script **Start-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="2c75a-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2c75a-160">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c75a-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="2c75a-161">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2c75a-161">Parameters</span></span>
* <span data-ttu-id="2c75a-162">**Name** : noms des nœuds de cluster à démarrer.</span><span class="sxs-lookup"><span data-stu-id="2c75a-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="2c75a-163">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2c75a-163">Wildcards are supported.</span></span> <span data-ttu-id="2c75a-164">Le nom du jeu de paramètres est Name.</span><span class="sxs-lookup"><span data-stu-id="2c75a-164">The parameter set name is Name.</span></span> <span data-ttu-id="2c75a-165">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2c75a-166">**Nœud**: objet HpcNode des nœuds à démarrer, qui peut être obtenu par le biais de l’applet de commande HPC PowerShell [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c75a-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2c75a-167">Le nom du jeu de paramètres est Node.</span><span class="sxs-lookup"><span data-stu-id="2c75a-167">The parameter set name is Node.</span></span> <span data-ttu-id="2c75a-168">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="2c75a-169">Exemple</span><span class="sxs-lookup"><span data-stu-id="2c75a-169">Example</span></span>
<span data-ttu-id="2c75a-170">L’exemple suivant démarre les nœuds dont le nom commence par *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="2c75a-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="2c75a-171">Arrêter des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="2c75a-171">Stop compute node VMs</span></span>
<span data-ttu-id="2c75a-172">Arrêtez des nœuds de calcul avec le script **Stop-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="2c75a-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="2c75a-173">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c75a-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="2c75a-174">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2c75a-174">Parameters</span></span>
* <span data-ttu-id="2c75a-175">**Name**: noms des nœuds de cluster à arrêter.</span><span class="sxs-lookup"><span data-stu-id="2c75a-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="2c75a-176">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2c75a-176">Wildcards are supported.</span></span> <span data-ttu-id="2c75a-177">Le nom du jeu de paramètres est Name.</span><span class="sxs-lookup"><span data-stu-id="2c75a-177">The parameter set name is Name.</span></span> <span data-ttu-id="2c75a-178">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2c75a-179">**Nœud** : objet HpcNode des nœuds à arrêter, qui peut être obtenu par le biais de l’applet de commande HPC PowerShell [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c75a-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="2c75a-180">Le nom du jeu de paramètres est Node.</span><span class="sxs-lookup"><span data-stu-id="2c75a-180">The parameter set name is Node.</span></span> <span data-ttu-id="2c75a-181">Vous ne pouvez pas spécifier à la fois les paramètres **Name** et **Node**.</span><span class="sxs-lookup"><span data-stu-id="2c75a-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="2c75a-182">**Force** (facultatif) : permet de mettre les nœuds HPC hors connexion avant de les arrêter.</span><span class="sxs-lookup"><span data-stu-id="2c75a-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="2c75a-183">Exemple</span><span class="sxs-lookup"><span data-stu-id="2c75a-183">Example</span></span>
<span data-ttu-id="2c75a-184">L’exemple suivant met hors connexion les nœuds dont le nom commence par *HPCNode-CN-* , puis les arrête.</span><span class="sxs-lookup"><span data-stu-id="2c75a-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="2c75a-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c75a-185">Next steps</span></span>
* <span data-ttu-id="2c75a-186">Pour augmenter ou réduire automatiquement les nœuds de cluster en fonction de la charge de travail actuelle des travaux et des tâches sur le cluster, consultez [Agrandir et réduire automatiquement les ressources de cluster HPC Pack dans Azure en fonction de la charge de travail du cluster](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="2c75a-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

