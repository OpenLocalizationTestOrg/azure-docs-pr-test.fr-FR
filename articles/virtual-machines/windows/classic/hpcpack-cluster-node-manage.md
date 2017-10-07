---
title: "nœuds de calcul du cluster de HPC Pack aaaManage | Documents Microsoft"
description: "En savoir plus sur PowerShell script outils tooadd, supprimer, démarrer et arrêter les nœuds de calcul de cluster HPC Pack 2012 R2 dans Azure"
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="b6735-103">Gérer le nombre de hello et de disponibilité de nœuds de calcul dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="b6735-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="b6735-104">Si vous avez créé un cluster HPC Pack 2012 R2 dans des machines virtuelles Azure, vous pourriez façons tooeasily ajouter, supprimer, démarrer (approvisionner) ou arrêter (annuler le déploiement) de certaines machines virtuelles de nœud dans le cluster de calcul.</span><span class="sxs-lookup"><span data-stu-id="b6735-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="b6735-105">toodo ces tâches, exécuter des scripts PowerShell de Azure qui sont installés sur la machine virtuelle du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="b6735-106">Ces scripts vous permettent de contrôler les nombre hello et la disponibilité de vos ressources de cluster HPC Pack afin de contrôler les coûts.</span><span class="sxs-lookup"><span data-stu-id="b6735-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b6735-107">Cet article s’applique uniquement tooHPC Pack 2012 R2 clusters dans Azure créé à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="b6735-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="b6735-109">En outre, les scripts PowerShell de hello décrits dans cet article ne sont pas disponibles dans HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="b6735-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6735-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6735-110">Prerequisites</span></span>
* <span data-ttu-id="b6735-111">**Cluster HPC Pack 2012 R2 dans des machines virtuelles Azure**: créer un cluster HPC Pack 2012 R2 dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="b6735-112">Par exemple, vous pouvez automatiser le déploiement de hello en utilisant une image de machine virtuelle de HPC Pack 2012 R2 hello Bonjour Azure Marketplace et un script Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6735-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="b6735-113">Pour plus d’informations et les conditions préalables requises, consultez [créer un Cluster HPC avec hello script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="b6735-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="b6735-114">Après le déploiement, recherchez des hello nœud Gestion des scripts dans hello % CCP\_dossier Accueil % bin sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="b6735-115">Exécuter chacun des scripts de hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b6735-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="b6735-116">**Certificat de gestion ou le fichier de paramètres de publication Azure**: vous devez toodo hello suivantes sur le nœud principal de hello :</span><span class="sxs-lookup"><span data-stu-id="b6735-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="b6735-117">**Fichier de paramètres de publication de hello d’importation Azure**.</span><span class="sxs-lookup"><span data-stu-id="b6735-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="b6735-118">toodo, hello exécution suivant des applets de commande PowerShell de Azure de nœud principal de hello :</span><span class="sxs-lookup"><span data-stu-id="b6735-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="b6735-119">**Configurer le certificat de gestion Azure hello sur le nœud principal de hello**.</span><span class="sxs-lookup"><span data-stu-id="b6735-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="b6735-120">Si vous disposez de fichier .cer hello, importez-le dans le magasin de certificats CurrentUser\My hello, puis exécutez hello suivant l’applet de commande PowerShell de Azure pour votre environnement Azure (cloud Azure ou AzureChinaCloud) :</span><span class="sxs-lookup"><span data-stu-id="b6735-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="b6735-121">Ajouter des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="b6735-121">Add compute node VMs</span></span>
<span data-ttu-id="b6735-122">Ajouter des nœuds de calcul avec hello **Add-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="b6735-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b6735-123">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b6735-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="b6735-124">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b6735-124">Parameters</span></span>
* <span data-ttu-id="b6735-125">**ServiceName**: nom du service de cloud hello nouvelles machines virtuelles de nœud de calcul sont ajoutés à.</span><span class="sxs-lookup"><span data-stu-id="b6735-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="b6735-126">**ImageName**: nom d’image de machine virtuelle Azure, qui peut être obtenu via hello portail Azure classic ou l’applet de commande Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="b6735-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="b6735-127">image de Hello doit respecter hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="b6735-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="b6735-128">Un système d’exploitation Windows doit être installé.</span><span class="sxs-lookup"><span data-stu-id="b6735-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="b6735-129">HPC Pack doit être installé dans le rôle de nœud de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="b6735-130">image de Hello doit être une image privée dans la catégorie d’utilisateur hello, pas une image de machine virtuelle Azure publique.</span><span class="sxs-lookup"><span data-stu-id="b6735-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="b6735-131">**Quantité**: nombre de toobe de machines virtuelles de nœud de calcul ajouté.</span><span class="sxs-lookup"><span data-stu-id="b6735-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="b6735-132">**InstanceSize**: taille de hello des machines virtuelles de nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="b6735-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="b6735-133">**DomainUserName**: nom d’utilisateur de domaine, qui est utilisé toojoin hello nouvelles machines virtuelles toohello domaine.</span><span class="sxs-lookup"><span data-stu-id="b6735-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="b6735-134">**DomainUserPassword**: mot de passe d’utilisateur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="b6735-135">**NodeNameSeries** (facultatif) : modèle de dénomination hello pour les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="b6735-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="b6735-136">Hello format doit être &lt; *racine\_nom*&gt;&lt;*Démarrer\_nombre*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="b6735-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="b6735-137">Par exemple, MyCN % 10 % signifie une série de hello calcule les noms des nœuds à partir de MyCN11.</span><span class="sxs-lookup"><span data-stu-id="b6735-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="b6735-138">Si non spécifié, hello script utilise hello configuré série d’affectation de noms de nœud dans un cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="b6735-139">Exemple</span><span class="sxs-lookup"><span data-stu-id="b6735-139">Example</span></span>
<span data-ttu-id="b6735-140">Hello exemple suivant ajoute nœud de calcul de grande taille 20 ordinateurs virtuels dans le service cloud hello *hpccnimage1*, en fonction de l’image de machine virtuelle hello *hpcservice1*.</span><span class="sxs-lookup"><span data-stu-id="b6735-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="b6735-141">Supprimer des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="b6735-141">Remove compute node VMs</span></span>
<span data-ttu-id="b6735-142">Supprimer des nœuds de calcul avec hello **Remove-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="b6735-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b6735-143">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b6735-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="b6735-144">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b6735-144">Parameters</span></span>
* <span data-ttu-id="b6735-145">**Nom**: noms des toobe des nœuds de cluster est supprimé.</span><span class="sxs-lookup"><span data-stu-id="b6735-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="b6735-146">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b6735-146">Wildcards are supported.</span></span> <span data-ttu-id="b6735-147">nom de jeu de paramètre Hello est.</span><span class="sxs-lookup"><span data-stu-id="b6735-147">hello parameter set name is Name.</span></span> <span data-ttu-id="b6735-148">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b6735-149">**Nœud**: objet HpcNode hello pour hello nœuds toobe est supprimé, ce qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6735-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b6735-150">nom du jeu de paramètre Hello est un nœud.</span><span class="sxs-lookup"><span data-stu-id="b6735-150">hello parameter set name is Node.</span></span> <span data-ttu-id="b6735-151">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b6735-152">**DeleteVHD** (facultatif) : paramètre toodelete disques hello associé pour hello machines virtuelles qui sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="b6735-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="b6735-153">**Force** (facultatif) : paramètre tooforce nœuds HPC en mode hors connexion avant de les supprimer.</span><span class="sxs-lookup"><span data-stu-id="b6735-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="b6735-154">**Confirmer** (facultatif) : demander confirmation avant d’exécuter la commande hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="b6735-155">**WhatIf**: paramètre toodescribe ce qui se passerait si vous avez exécuté la commande hello sans réellement l’exécuter commande hello.</span><span class="sxs-lookup"><span data-stu-id="b6735-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="b6735-156">Exemple</span><span class="sxs-lookup"><span data-stu-id="b6735-156">Example</span></span>
<span data-ttu-id="b6735-157">Hello exemple suivant force les nœuds hors connexion hello dont le nom commence *HPCNode-CN -* et les supprime les nœuds hello et les disques associés.</span><span class="sxs-lookup"><span data-stu-id="b6735-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="b6735-158">Démarrer des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="b6735-158">Start compute node VMs</span></span>
<span data-ttu-id="b6735-159">Démarrer les nœuds avec hello **Start-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="b6735-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b6735-160">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b6735-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="b6735-161">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b6735-161">Parameters</span></span>
* <span data-ttu-id="b6735-162">**Nom**: noms des toobe de nœuds de cluster hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="b6735-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="b6735-163">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b6735-163">Wildcards are supported.</span></span> <span data-ttu-id="b6735-164">nom de jeu de paramètre Hello est.</span><span class="sxs-lookup"><span data-stu-id="b6735-164">hello parameter set name is Name.</span></span> <span data-ttu-id="b6735-165">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b6735-166">**Nœud**-objet HpcNode hello pour toobe de nœuds hello démarré, qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6735-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b6735-167">nom du jeu de paramètre Hello est un nœud.</span><span class="sxs-lookup"><span data-stu-id="b6735-167">hello parameter set name is Node.</span></span> <span data-ttu-id="b6735-168">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="b6735-169">Exemple</span><span class="sxs-lookup"><span data-stu-id="b6735-169">Example</span></span>
<span data-ttu-id="b6735-170">Hello exemple suivant démarre les nœuds dont le nom commence *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="b6735-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="b6735-171">Arrêter des machines virtuelles à nœud de calcul</span><span class="sxs-lookup"><span data-stu-id="b6735-171">Stop compute node VMs</span></span>
<span data-ttu-id="b6735-172">Arrêter les nœuds de calcul avec hello **Stop-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="b6735-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="b6735-173">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b6735-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="b6735-174">Paramètres</span><span class="sxs-lookup"><span data-stu-id="b6735-174">Parameters</span></span>
* <span data-ttu-id="b6735-175">**Nom**-noms de toobe de nœuds de cluster hello s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="b6735-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="b6735-176">Les caractères génériques sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b6735-176">Wildcards are supported.</span></span> <span data-ttu-id="b6735-177">nom de jeu de paramètre Hello est.</span><span class="sxs-lookup"><span data-stu-id="b6735-177">hello parameter set name is Name.</span></span> <span data-ttu-id="b6735-178">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b6735-179">**Nœud**: objet HpcNode hello pour hello nœuds toobe est arrêté, ce qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6735-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="b6735-180">nom du jeu de paramètre Hello est un nœud.</span><span class="sxs-lookup"><span data-stu-id="b6735-180">hello parameter set name is Node.</span></span> <span data-ttu-id="b6735-181">Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.</span><span class="sxs-lookup"><span data-stu-id="b6735-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="b6735-182">**Force** (facultatif) : paramètre tooforce nœuds HPC en mode hors connexion avant de les arrêter.</span><span class="sxs-lookup"><span data-stu-id="b6735-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="b6735-183">Exemple</span><span class="sxs-lookup"><span data-stu-id="b6735-183">Example</span></span>
<span data-ttu-id="b6735-184">Hello exemple suivant force les nœuds hors connexion dont le nom commence *HPCNode-CN -* et puis s’arrête hello nœuds.</span><span class="sxs-lookup"><span data-stu-id="b6735-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="b6735-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6735-185">Next steps</span></span>
* <span data-ttu-id="b6735-186">tooautomatically augmenter ou réduire les nœuds du cluster en fonction de la charge de travail actuelle hello des tâches et des tâches sur le cluster de hello hello, consultez [croître automatiquement et de réduire les ressources de cluster HPC Pack hello dans Azure conséquente toohello la charge du cluster](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="b6735-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

