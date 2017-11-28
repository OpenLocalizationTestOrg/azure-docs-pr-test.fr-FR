---
title: "Comprendre les adresses IP partagées dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment Azure DevTest Labs utilise les adresses IP partagées afin de limiter les adresses IP publiques requises pour accéder aux machines virtuelles de votre laboratoire."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="a4402-103">Comprendre les adresses IP partagées dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4402-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="a4402-104">Azure DevTest Labs permet aux machines virtuelles de laboratoire de partager la même adresse IP publique afin de limiter le nombre d’adresses IP publiques requises pour accéder aux machines virtuelles de votre laboratoire individuel.</span><span class="sxs-lookup"><span data-stu-id="a4402-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="a4402-105">Cet article décrit le fonctionnement des adresses IP partagées et les options de configuration qui leur sont associées.</span><span class="sxs-lookup"><span data-stu-id="a4402-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="a4402-106">Paramètre d’adresse IP partagée</span><span class="sxs-lookup"><span data-stu-id="a4402-106">Shared IP setting</span></span>

<span data-ttu-id="a4402-107">Lorsque vous créez un laboratoire, il se trouve dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="a4402-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="a4402-108">Par défaut, ce sous-réseau est créé avec le paramètre **Enable shared public IP** (Activer l’adresse IP publique partagée) défini sur *Oui*.</span><span class="sxs-lookup"><span data-stu-id="a4402-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="a4402-109">Cette configuration crée une adresse IP publique pour le sous-réseau dans son ensemble.</span><span class="sxs-lookup"><span data-stu-id="a4402-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="a4402-110">Pour plus d’informations sur la configuration des réseaux virtuels et des sous-réseaux, consultez [Configurer un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="a4402-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nouveau sous-réseau de laboratoire](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="a4402-112">Pour les laboratoires existants, vous pouvez activer cette option en sélectionnant **Configuration et stratégies > réseaux virtuels**.</span><span class="sxs-lookup"><span data-stu-id="a4402-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="a4402-113">Puis, sélectionnez un réseau virtuel dans la liste et choisissez **ACTIVER L’ADRESSE IP PUBLIQUE PARTAGÉE** pour un sous-réseau sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a4402-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="a4402-114">Vous pouvez également désactiver cette option dans un laboratoire si vous ne souhaitez pas partager une adresse IP publique entre les machines virtuelles du laboratoire.</span><span class="sxs-lookup"><span data-stu-id="a4402-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="a4402-115">Les machines virtuelles créées dans ce laboratoire utilisent par défaut une adresse IP partagée.</span><span class="sxs-lookup"><span data-stu-id="a4402-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="a4402-116">Lorsque vous créez la machine virtuelle, ce paramètre peut être observé dans le panneau **Paramètres avancés** sous **Configuration de l’adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="a4402-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Nouvelle machine virtuelle](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="a4402-118">**Partagé :** toutes les machines virtuelles créées en mode **Partagé** sont placées dans un groupe de ressources (GR).</span><span class="sxs-lookup"><span data-stu-id="a4402-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="a4402-119">Une seule adresse IP est affectée à ce GR et toutes les machines virtuelles de ce GR utilisent cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="a4402-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="a4402-120">**Public :** chaque machine virtuelle que vous créez possède sa propre adresse IP et est créée dans son propre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a4402-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="a4402-121">**Privé :** chaque machine virtuelle que vous créez utilise une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="a4402-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="a4402-122">Vous ne pourrez pas vous connecter directement à cette machine virtuelle depuis Internet avec le bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="a4402-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="a4402-123">Chaque fois qu’une machine virtuelle dotée une adresse IP partagée activée est ajoutée au sous-réseau, DevTest Labs ajoute automatiquement la machine virtuelle à un équilibreur de charge et attribue un numéro de port TCP à l’adresse IP publique, pour le transfert vers le port RDP sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a4402-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="a4402-124">Utilisation de l’adresse IP partagée</span><span class="sxs-lookup"><span data-stu-id="a4402-124">Using the shared IP</span></span>

- <span data-ttu-id="a4402-125">**Utilisateurs Linux :** SSH vers la machine virtuelle à l’aide de l’adresse IP ou du nom de domaine complet, suivis du signe deux-points et du port.</span><span class="sxs-lookup"><span data-stu-id="a4402-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="a4402-126">Par exemple, dans l’image ci-dessous, l’adresse RDP pour se connecter à la machine virtuelle est `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="a4402-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Exemple de machine virtuelle](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="a4402-128">**Utilisateurs Windows :** sélectionnez **Se connecter** sur le portail Azure pour télécharger un fichier RDP préconfiguré et accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a4402-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4402-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4402-129">Next steps</span></span>

* [<span data-ttu-id="a4402-130">Définir des stratégies de laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4402-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="a4402-131">Configuration d’un réseau virtuel dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4402-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





