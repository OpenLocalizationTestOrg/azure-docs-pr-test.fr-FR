---
title: "Gérer vos machines virtuelles à l’aide d’Azure PowerShell | Microsoft Docs"
description: "Découvrez les commandes que vous pouvez utiliser pour automatiser les tâches de gestion des machines virtuelles."
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
ms.openlocfilehash: fd2df7e1029ced11974d0b832258bed2cf3bbb27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="66023-103">Gérer vos machines virtuelles à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="66023-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="66023-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66023-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66023-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="66023-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="66023-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="66023-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="66023-107">Pour connaître les commandes PowerShell courantes avec le modèle Resource Manager, consultez [cet article](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66023-107">For common PowerShell commands using the Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="66023-108">Il est possible d’automatiser les nombreuses tâches quotidiennes liées à la gestion de vos machines virtuelles en utilisant les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66023-108">Many tasks you do each day to manage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="66023-109">Cet article donne des exemples de commandes pour réaliser des tâches simples et contient des liens vers des articles indiquant les commandes à utiliser pour des tâches plus complexes.</span><span class="sxs-lookup"><span data-stu-id="66023-109">This article gives you example commands for simpler tasks, and links to articles that show the commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="66023-110">Si vous n’avez pas installé et configuré Azure PowerShell, vous pouvez obtenir des instructions dans l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66023-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-to-use-the-example-commands"></a><span data-ttu-id="66023-111">Utilisation des exemples de commandes</span><span class="sxs-lookup"><span data-stu-id="66023-111">How to use the example commands</span></span>
<span data-ttu-id="66023-112">Vous devrez remplacer une partie du texte des commandes par un texte approprié à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="66023-112">You'll need to replace some of the text in the commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="66023-113">Les symboles < et > indiquent le texte à remplacer.</span><span class="sxs-lookup"><span data-stu-id="66023-113">The < and > symbols indicate text you need to replace.</span></span> <span data-ttu-id="66023-114">Lorsque vous remplacez le texte, supprimez les symboles, mais laissez les guillemets en place.</span><span class="sxs-lookup"><span data-stu-id="66023-114">When you replace the text, remove the symbols but leave the quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="66023-115">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="66023-115">Get a VM</span></span>
<span data-ttu-id="66023-116">Il s’agit d’une tâche de base que vous utiliserez souvent.</span><span class="sxs-lookup"><span data-stu-id="66023-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="66023-117">Utilisez-la pour obtenir des informations sur une machine virtuelle, effectuer des tâches sur cette dernière ou pour obtenir un résultat à stocker dans une variable.</span><span class="sxs-lookup"><span data-stu-id="66023-117">Use it to get information about a VM, perform tasks on a VM, or get output to store in a variable.</span></span>

<span data-ttu-id="66023-118">Pour obtenir des informations sur la machine virtuelle, exécutez cette commande en remplaçant tous les éléments entre guillemets notamment les caractères < et > :</span><span class="sxs-lookup"><span data-stu-id="66023-118">To get information about the VM, run this command, replacing everything in the quotes, including the < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="66023-119">Pour stocker le résultat dans une variable $vm, exécutez :</span><span class="sxs-lookup"><span data-stu-id="66023-119">To store the output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-to-a-windows-based-vm"></a><span data-ttu-id="66023-120">Ouvrir une session sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="66023-120">Log on to a Windows-based VM</span></span>
<span data-ttu-id="66023-121">Exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="66023-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="66023-122">Vous pouvez obtenir le nom du service cloud et de la machine virtuelle à partir de l’affichage de la commande **Get-AzureVM** .</span><span class="sxs-lookup"><span data-stu-id="66023-122">You can get the virtual machine and cloud service name from the display of the **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="66023-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<emplacement du lecteur et du dossier pour stocker le fichier RDP téléchargé, par exemple : C:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span><span class="sxs-lookup"><span data-stu-id="66023-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location to store the downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="66023-124">Arrêter une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="66023-124">Stop a VM</span></span>
<span data-ttu-id="66023-125">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="66023-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="66023-126">Utilisez ce paramètre pour conserver l’adresse IP virtuelle du service cloud s’il s’agit de la dernière machine virtuelle de ce service.</span><span class="sxs-lookup"><span data-stu-id="66023-126">Use this parameter to keep the virtual IP (VIP) of the cloud service in case it's the last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="66023-127">Si vous utilisez le paramètre StayProvisioned, vous êtes toujours facturé pour cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66023-127">If you use the StayProvisioned parameter, you'll still be billed for the VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="66023-128">Démarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="66023-128">Start a VM</span></span>
<span data-ttu-id="66023-129">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="66023-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="66023-130">Association d’un disque de données</span><span class="sxs-lookup"><span data-stu-id="66023-130">Attach a data disk</span></span>
<span data-ttu-id="66023-131">Cette tâche nécessite de réaliser quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="66023-131">This task requires a few steps.</span></span> <span data-ttu-id="66023-132">Tout d’abord, utilisez l’applet de commande ****Add-AzureDataDisk**** pour ajouter le disque à l’objet $vm.</span><span class="sxs-lookup"><span data-stu-id="66023-132">First, you use the ****Add-AzureDataDisk**** cmdlet to add the disk to the $vm object.</span></span> <span data-ttu-id="66023-133">Utilisez ensuite l’applet de commande **Update-AzureVM** pour mettre à jour la configuration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66023-133">Then, you use **Update-AzureVM** cmdlet to update the configuration of the VM.</span></span>

<span data-ttu-id="66023-134">Vous devez également décider d’associer un nouveau disque ou un disque existant, qui contient des données.</span><span class="sxs-lookup"><span data-stu-id="66023-134">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="66023-135">Dans le cas d’un nouveau disque, la commande entraîne la création du fichier .vhd et son association.</span><span class="sxs-lookup"><span data-stu-id="66023-135">For a new disk, the command creates the .vhd file and attaches it.</span></span>

<span data-ttu-id="66023-136">Pour associer un nouveau disque, exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="66023-136">To attach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="66023-137">Pour associer un disque existant, exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="66023-137">To attach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="66023-138">Pour attacher des disques de données à partir d’un fichier .vhd existant dans le stockage d’objets blob, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="66023-138">To attach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="66023-139">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="66023-139">Create a Windows-based VM</span></span>
<span data-ttu-id="66023-140">Pour créer une nouvelle machine virtuelle Windows dans Azure, consultez [Utilisation d’Azure PowerShell pour créer et préconfigurer des machines virtuelles Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="66023-140">To create a new Windows-based virtual machine in Azure, use the instructions in [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="66023-141">Cette rubrique vous guide lors de la création d’un jeu de commandes Azure PowerShell permettant de créer une machine virtuelle Windows pouvant être préconfigurée avec :</span><span class="sxs-lookup"><span data-stu-id="66023-141">This topic steps you through the creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="66023-142">une appartenance au domaine Active Directory ;</span><span class="sxs-lookup"><span data-stu-id="66023-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="66023-143">des disques supplémentaires ;</span><span class="sxs-lookup"><span data-stu-id="66023-143">With additional disks.</span></span>
* <span data-ttu-id="66023-144">une appartenance à un jeu d’équilibrage de la charge ;</span><span class="sxs-lookup"><span data-stu-id="66023-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="66023-145">une adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="66023-145">With a static IP address.</span></span>

