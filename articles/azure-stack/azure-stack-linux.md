---
title: "Invités aaaLinux sur la pile de Azure | Documents Microsoft"
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
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="bb4cb-103">Déployer des machines virtuelles Linux sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bb4cb-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="bb4cb-104">Vous pouvez déployer des ordinateurs virtuels Linux sur hello Kit de développement de pile Azure en ajoutant une image Linux hello Azure Marketplace de pile.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-104">You can deploy Linux virtual machines on hello Azure Stack Development Kit by adding a Linux-based image into hello Azure Stack Marketplace.</span></span> <span data-ttu-id="bb4cb-105">Plusieurs fournisseurs Linux proposent des images qui peuvent être ajoutées à un Kit de développement Azure Stack, mais vous pouvez aussi générer votre propre image.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="bb4cb-106">Télécharger une image</span><span class="sxs-lookup"><span data-stu-id="bb4cb-106">Download an image</span></span>
1. <span data-ttu-id="bb4cb-107">Télécharger et extraire une image de la pile compatibles Azure hello suivant liens ou préparer votre propre :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-107">Download and extract an Azure Stack-compatible image from hello following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="bb4cb-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="bb4cb-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="bb4cb-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="bb4cb-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="bb4cb-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="bb4cb-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="bb4cb-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="bb4cb-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="bb4cb-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="bb4cb-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="bb4cb-113">Extraire l’image du disque dur virtuel hello si nécessaire et [ajouter hello image toohello Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="bb4cb-113">Extract hello image VHD if necessary and [add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="bb4cb-114">Vérifiez que hello `OSType` paramètre est défini trop`Linux`.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-114">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
3. <span data-ttu-id="bb4cb-115">Une fois que vous avez ajouté hello image toohello Marketplace, un élément de Marketplace est créé et vous pouvez déployer une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-115">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="bb4cb-116">Préparer votre propre image</span><span class="sxs-lookup"><span data-stu-id="bb4cb-116">Prepare your own image</span></span>
1. <span data-ttu-id="bb4cb-117">Préparez votre propre image de Linux à l’aide de hello suivant les instructions :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-117">Prepare your own Linux image using one of hello following instructions:</span></span>
   
   * [<span data-ttu-id="bb4cb-118">Distributions CentOS</span><span class="sxs-lookup"><span data-stu-id="bb4cb-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="bb4cb-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="bb4cb-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="bb4cb-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="bb4cb-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="bb4cb-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="bb4cb-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="bb4cb-122">SLES et openSUSE</span><span class="sxs-lookup"><span data-stu-id="bb4cb-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="bb4cb-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bb4cb-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="bb4cb-124">Téléchargez et installez hello [Linux Agent Azure](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="bb4cb-124">Download and install hello [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="bb4cb-125">Hello version de le Linux Agent Azure 2.1.3 ou supérieure est requise tooprovision votre VM Linux sur Azure pile.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-125">hello Azure Linux Agent version 2.1.3 or higher is required tooprovision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="bb4cb-126">La plupart des distributions hello répertoriées ci-dessus déjà comprennent cette version de l’agent de hello ou supérieure sous forme de package dans leurs référentiels (généralement appelé `WALinuxAgent` ou `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="bb4cb-126">Many of hello distributions listed above already include this version of hello agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="bb4cb-127">Toutefois, si hello version du package de l’agent Windows Azure hello est inférieur à 2.1.3 (2.0.18 ou inférieur), vous devez installer manuellement l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-127">However, if hello version of hello Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install hello agent manually.</span></span> <span data-ttu-id="bb4cb-128">version de Hello installé peut être déterminée à partir du nom du package hello ou en exécutant `/usr/sbin/waagent -version` sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-128">hello installed version can be determined either from hello package name or by running `/usr/sbin/waagent -version` on hello VM.</span></span>
   
    <span data-ttu-id="bb4cb-129">Suivez les instructions de hello sous l’agent Azure Linux de hello tooinstall manuellement :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-129">Follow hello instructions below tooinstall hello Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="bb4cb-130">Commencez par télécharger hello dernière Azure agent Linux à partir de [GitHub](https://github.com/Azure/WALinuxAgent/releases), exemple :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-130">First, download hello latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="bb4cb-131">Décompresser hello agent Azure :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-131">Unpack hello Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="bb4cb-132">Installez python-setuptools :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="bb4cb-133">**Debian / Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="bb4cb-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="bb4cb-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="bb4cb-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="bb4cb-135">**RHEL / CentOS / Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="bb4cb-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="bb4cb-136">Installez hello agent Azure :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-136">Install hello Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="bb4cb-137">Systèmes avec Python 2.x et 3.x installé Python côte à côte doivent hello toorun commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bb4cb-137">Systems with Python 2.x and Python 3.x installed side-by-side may need toorun hello following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="bb4cb-138">Pour plus d’informations, consultez hello Linux Agent Azure [Lisez-moi](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="bb4cb-138">For more information, see hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="bb4cb-139">[Ajouter l’image de hello toohello Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="bb4cb-139">[Add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="bb4cb-140">Vérifiez que hello `OSType` paramètre est défini trop`Linux`.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-140">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
4. <span data-ttu-id="bb4cb-141">Une fois que vous avez ajouté hello image toohello Marketplace, un élément de Marketplace est créé et vous pouvez déployer une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="bb4cb-141">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb4cb-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb4cb-142">Next steps</span></span>
[<span data-ttu-id="bb4cb-143">Forum aux questions sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bb4cb-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

