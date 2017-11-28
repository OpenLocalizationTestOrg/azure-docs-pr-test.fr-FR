---
title: "Invités Linux sur Azure Stack | Microsoft Docs"
description: "Découvrez comment créer des machines virtuelles Linux sur Azure Stack."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="2ed50-103">Déployer des machines virtuelles Linux sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2ed50-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="2ed50-104">Vous pouvez déployer des machines virtuelles Linux sur le Kit de développement Azure Stack en ajoutant une image Linux dans la Place de Marché Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2ed50-104">You can deploy Linux virtual machines on the Azure Stack Development Kit by adding a Linux-based image into the Azure Stack Marketplace.</span></span> <span data-ttu-id="2ed50-105">Plusieurs fournisseurs Linux proposent des images qui peuvent être ajoutées à un Kit de développement Azure Stack, mais vous pouvez aussi générer votre propre image.</span><span class="sxs-lookup"><span data-stu-id="2ed50-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="2ed50-106">Télécharger une image</span><span class="sxs-lookup"><span data-stu-id="2ed50-106">Download an image</span></span>
1. <span data-ttu-id="2ed50-107">Téléchargez et extrayez une image compatible avec Azure Stack à partir des liens suivants, ou préparez votre propre image :</span><span class="sxs-lookup"><span data-stu-id="2ed50-107">Download and extract an Azure Stack-compatible image from the following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="2ed50-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="2ed50-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="2ed50-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="2ed50-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="2ed50-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2ed50-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="2ed50-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="2ed50-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="2ed50-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="2ed50-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="2ed50-113">Extrayez le disque dur virtuel d’image si nécessaire et [ajoutez l’image à la Place de Marché](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="2ed50-113">Extract the image VHD if necessary and [add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="2ed50-114">Vérifiez que le paramètre `OSType` a la valeur `Linux`.</span><span class="sxs-lookup"><span data-stu-id="2ed50-114">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
3. <span data-ttu-id="2ed50-115">Une fois que vous avez ajouté l’image à la Place de Marché, un élément de Place de Marché est créé et vous pouvez déployer une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="2ed50-115">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="2ed50-116">Préparer votre propre image</span><span class="sxs-lookup"><span data-stu-id="2ed50-116">Prepare your own image</span></span>
1. <span data-ttu-id="2ed50-117">Préparez votre propre image Linux en appliquant l’une des instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ed50-117">Prepare your own Linux image using one of the following instructions:</span></span>
   
   * [<span data-ttu-id="2ed50-118">Distributions CentOS</span><span class="sxs-lookup"><span data-stu-id="2ed50-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="2ed50-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="2ed50-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="2ed50-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="2ed50-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="2ed50-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="2ed50-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="2ed50-122">SLES et openSUSE</span><span class="sxs-lookup"><span data-stu-id="2ed50-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="2ed50-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2ed50-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="2ed50-124">Téléchargez et installez l’[agent Linux Azure](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="2ed50-124">Download and install the [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="2ed50-125">L’agent Linux Azure version 2.1.3 ou ultérieure est nécessaire pour approvisionner votre machine virtuelle Linux sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2ed50-125">The Azure Linux Agent version 2.1.3 or higher is required to provision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="2ed50-126">La plupart des distributions répertoriées ci-dessus incluent déjà cette version de l’agent ou une version ultérieure en tant que package dans leurs dépôts (généralement nommé `WALinuxAgent` ou `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="2ed50-126">Many of the distributions listed above already include this version of the agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="2ed50-127">Toutefois, si la version du package de l’agent Azure est inférieure à la version 2.1.3 (autrement dit, 2.0.18 ou inférieure), vous devez installer l’agent manuellement.</span><span class="sxs-lookup"><span data-stu-id="2ed50-127">However, if the version of the Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install the agent manually.</span></span> <span data-ttu-id="2ed50-128">Vous pouvez déterminer la version installée à partir du nom de package ou en exécutant `/usr/sbin/waagent -version` sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2ed50-128">The installed version can be determined either from the package name or by running `/usr/sbin/waagent -version` on the VM.</span></span>
   
    <span data-ttu-id="2ed50-129">Pour installer l’agent Linux Azure manuellement, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2ed50-129">Follow the instructions below to install the Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="2ed50-130">Commencez par télécharger l’agent Linux Azure le plus récent à partir de [GitHub](https://github.com/Azure/WALinuxAgent/releases), par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ed50-130">First, download the latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="2ed50-131">Décompressez l’agent Azure :</span><span class="sxs-lookup"><span data-stu-id="2ed50-131">Unpack the Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="2ed50-132">Installez python-setuptools :</span><span class="sxs-lookup"><span data-stu-id="2ed50-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="2ed50-133">**Debian / Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2ed50-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="2ed50-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="2ed50-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="2ed50-135">**RHEL / CentOS / Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="2ed50-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="2ed50-136">Installez l’agent Azure :</span><span class="sxs-lookup"><span data-stu-id="2ed50-136">Install the Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="2ed50-137">Les systèmes sur lesquels Python 2.x et Python 3.x sont installés côte à côte devront peut-être exécuter la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2ed50-137">Systems with Python 2.x and Python 3.x installed side-by-side may need to run the following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="2ed50-138">Pour plus d’informations, consultez le [fichier LISEZMOI](https://github.com/Azure/WALinuxAgent/blob/master/README.md) de l’agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="2ed50-138">For more information, see the Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="2ed50-139">[Ajoutez l’image à la Place de Marché](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="2ed50-139">[Add the image to the Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="2ed50-140">Vérifiez que le paramètre `OSType` a la valeur `Linux`.</span><span class="sxs-lookup"><span data-stu-id="2ed50-140">Make sure that the `OSType` parameter is set to `Linux`.</span></span>
4. <span data-ttu-id="2ed50-141">Une fois que vous avez ajouté l’image à la Place de Marché, un élément de Place de Marché est créé et vous pouvez déployer une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="2ed50-141">After you've added the image to the Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ed50-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ed50-142">Next steps</span></span>
[<span data-ttu-id="2ed50-143">Forum aux questions sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2ed50-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

