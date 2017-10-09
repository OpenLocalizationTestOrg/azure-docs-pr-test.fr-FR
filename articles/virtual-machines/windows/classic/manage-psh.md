---
title: "aaaManage vos machines virtuelles à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Découvrir les commandes que vous pouvez utiliser des tâches tooautomate dans la gestion de vos machines virtuelles."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="e55f8-103">Gérer vos machines virtuelles à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e55f8-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e55f8-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e55f8-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e55f8-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e55f8-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e55f8-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e55f8-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e55f8-107">Pour les commandes PowerShell communes à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e55f8-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e55f8-108">Plusieurs tâches que vous effectuez chaque toomanage jour vos machines virtuelles peuvent être automatisées à l’aide des applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="e55f8-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e55f8-109">Cet article vous donne des exemples de commandes pour des tâches plus simples et tooarticles des liens qui montrent les commandes hello pour des tâches plus complexes.</span><span class="sxs-lookup"><span data-stu-id="e55f8-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="e55f8-110">Si vous n’avez pas encore installé et configuré Azure PowerShell, vous pouvez obtenir des instructions dans l’article de hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e55f8-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="e55f8-111">Comment toouse hello des exemples de commandes</span><span class="sxs-lookup"><span data-stu-id="e55f8-111">How toouse hello example commands</span></span>
<span data-ttu-id="e55f8-112">Vous devez tooreplace une partie du texte hello dans hello commandes avec le texte qui est approprié pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e55f8-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="e55f8-113">Hello < et > symboles indiquent le texte tooreplace.</span><span class="sxs-lookup"><span data-stu-id="e55f8-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="e55f8-114">Lorsque vous remplacez le texte hello, supprimer les symboles de hello, mais laissez les guillemets hello en place.</span><span class="sxs-lookup"><span data-stu-id="e55f8-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="e55f8-115">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e55f8-115">Get a VM</span></span>
<span data-ttu-id="e55f8-116">Il s’agit d’une tâche de base que vous utiliserez souvent.</span><span class="sxs-lookup"><span data-stu-id="e55f8-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="e55f8-117">Utiliser tooget d’informations sur une machine virtuelle, effectuer des tâches sur une machine virtuelle ou obtenir toostore de sortie dans une variable.</span><span class="sxs-lookup"><span data-stu-id="e55f8-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="e55f8-118">tooget informations hello machine virtuelle, exécutez cette commande, en remplaçant tous les éléments entre guillemets hello, y compris hello < et > :</span><span class="sxs-lookup"><span data-stu-id="e55f8-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="e55f8-119">hello toostore de sortie dans une variable $vm, exécutez :</span><span class="sxs-lookup"><span data-stu-id="e55f8-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="e55f8-120">Ouvrez une session sur tooa ordinateurs virtuels Windows</span><span class="sxs-lookup"><span data-stu-id="e55f8-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="e55f8-121">Exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="e55f8-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="e55f8-122">Vous pouvez obtenir hello virtual machine et le nom du service cloud à partir de l’affichage de hello Hello **Get-AzureVM** commande.</span><span class="sxs-lookup"><span data-stu-id="e55f8-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="e55f8-123">$svcName = «<cloud service name>» $vmName = »<virtual machine name>» $localPath = « < lecteur et le dossier fichier emplacement toostore hello téléchargé RDP, par exemple : c:\temp > « $localFile = $localPath + «\" + $vmname + « .rdp « Get-AzureRemoteDesktopFile - ServiceName $svcName-nom - LocalPath $vmName $localFile-lancement</span><span class="sxs-lookup"><span data-stu-id="e55f8-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="e55f8-124">Arrêter une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e55f8-124">Stop a VM</span></span>
<span data-ttu-id="e55f8-125">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="e55f8-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="e55f8-126">Utilisez cette hello tookeep de paramètre de service IP virtuelle (VIP) du cloud de hello en cas de hello dernier ordinateur virtuel dans ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="e55f8-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="e55f8-127">Si vous utilisez le paramètre de StayProvisioned hello, vous serez toujours facturé pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e55f8-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="e55f8-128">Démarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e55f8-128">Start a VM</span></span>
<span data-ttu-id="e55f8-129">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="e55f8-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="e55f8-130">Association d’un disque de données</span><span class="sxs-lookup"><span data-stu-id="e55f8-130">Attach a data disk</span></span>
<span data-ttu-id="e55f8-131">Cette tâche nécessite de réaliser quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="e55f8-131">This task requires a few steps.</span></span> <span data-ttu-id="e55f8-132">Tout d’abord, vous utilisez hello *** Add-AzureDataDisk *** applet de commande tooadd hello toohello $vm objet de disque.</span><span class="sxs-lookup"><span data-stu-id="e55f8-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="e55f8-133">Ensuite, vous utilisez **Update-AzureVM** configuration hello applet de commande tooupdate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e55f8-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="e55f8-134">Vous devez également toodecide si tooattach un nouveau disque ou un qui contient des données.</span><span class="sxs-lookup"><span data-stu-id="e55f8-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="e55f8-135">Commande hello crée le fichier .vhd de hello pour un nouveau disque et l’attache.</span><span class="sxs-lookup"><span data-stu-id="e55f8-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="e55f8-136">tooattach un nouveau disque, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e55f8-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="e55f8-137">tooattach un disque de données existant, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e55f8-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="e55f8-138">tooattach des disques de données à partir d’un fichier .vhd existant dans le stockage blob, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e55f8-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="e55f8-139">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="e55f8-139">Create a Windows-based VM</span></span>
<span data-ttu-id="e55f8-140">toocreate une basé sur Windows machine virtuelle dans Azure, suivez les instructions du hello [toocreate d’utiliser Azure PowerShell et préconfigurer des machines virtuelles basées sur Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e55f8-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="e55f8-141">Étapes de cette rubrique vous guide dans la création d’une commande que la valeur de Azure PowerShell hello crée un ordinateur virtuel basé sur Windows qui peut être préconfiguré :</span><span class="sxs-lookup"><span data-stu-id="e55f8-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="e55f8-142">une appartenance au domaine Active Directory ;</span><span class="sxs-lookup"><span data-stu-id="e55f8-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="e55f8-143">des disques supplémentaires ;</span><span class="sxs-lookup"><span data-stu-id="e55f8-143">With additional disks.</span></span>
* <span data-ttu-id="e55f8-144">une appartenance à un jeu d’équilibrage de la charge ;</span><span class="sxs-lookup"><span data-stu-id="e55f8-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="e55f8-145">une adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="e55f8-145">With a static IP address.</span></span>

