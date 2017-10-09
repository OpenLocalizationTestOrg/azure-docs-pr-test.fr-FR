---
title: "aaaUnderstand partagé des adresses IP dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment Azure DevTest Labs utilise partagé IP adresses toominimize hello publique IP adresses requis tooaccess votre laboratoire de machines virtuelles."
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
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="ebcff-103">Comprendre les adresses IP partagées dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ebcff-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="ebcff-104">Lab de permet de Azure DevTest Labs partage des machines virtuelles hello publique IP adresse toominimize hello autant de public tooaccess de requis d’adresses IP de votre laboratoire des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ebcff-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="ebcff-105">Cet article décrit le fonctionnement des adresses IP partagées et les options de configuration qui leur sont associées.</span><span class="sxs-lookup"><span data-stu-id="ebcff-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="ebcff-106">Paramètre d’adresse IP partagée</span><span class="sxs-lookup"><span data-stu-id="ebcff-106">Shared IP setting</span></span>

<span data-ttu-id="ebcff-107">Lorsque vous créez un laboratoire, il se trouve dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ebcff-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="ebcff-108">Par défaut, ce sous-réseau est créé avec **activer partagée d’adresse IP publique** défini trop*Oui*.</span><span class="sxs-lookup"><span data-stu-id="ebcff-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="ebcff-109">Cette configuration crée une adresse IP publique pour le sous-réseau en entier hello.</span><span class="sxs-lookup"><span data-stu-id="ebcff-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="ebcff-110">Pour plus d’informations sur la configuration des réseaux virtuels et des sous-réseaux, consultez [Configurer un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ebcff-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nouveau sous-réseau de laboratoire](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="ebcff-112">Pour les laboratoires existants, vous pouvez activer cette option en sélectionnant **Configuration et stratégies > réseaux virtuels**.</span><span class="sxs-lookup"><span data-stu-id="ebcff-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="ebcff-113">Ensuite, sélectionnez un réseau virtuel à partir de la liste de hello et choisissez **activer partagé adresse IP publique** pour un sous-réseau sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ebcff-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="ebcff-114">Vous pouvez également désactiver cette option dans un laboratoire si vous ne souhaitez pas tooshare une adresse IP publique entre les ordinateurs virtuels de lab.</span><span class="sxs-lookup"><span data-stu-id="ebcff-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="ebcff-115">Les ordinateurs virtuels créés dans cette toousing par défaut de laboratoire une adresse IP partagée.</span><span class="sxs-lookup"><span data-stu-id="ebcff-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="ebcff-116">Lorsque vous créez hello machine virtuelle, ce paramètre peut être observé dans hello **paramètres avancés** panneau sous **configuration d’adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="ebcff-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nouvelle machine virtuelle](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="ebcff-118">**Partagé :** toutes les machines virtuelles créées en mode **Partagé** sont placées dans un groupe de ressources (GR).</span><span class="sxs-lookup"><span data-stu-id="ebcff-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="ebcff-119">Une seule adresse IP est affectée pour ce groupe de routage et de toutes les machines virtuelles dans hello RG utilisera cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="ebcff-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="ebcff-120">**Public :** chaque machine virtuelle que vous créez possède sa propre adresse IP et est créée dans son propre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ebcff-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="ebcff-121">**Privé :** chaque machine virtuelle que vous créez utilise une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="ebcff-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="ebcff-122">Vous ne serez pas en mesure de tooconnect toothis machine virtuelle directement à partir de hello internet avec le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="ebcff-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="ebcff-123">Chaque fois qu’une machine virtuelle avec l’adresse IP partagée activée est ajoutée toohello sous-réseau, DevTest Labs ajoute l’équilibrage de charge hello VM tooa automatiquement et affecte un numéro de port TCP sur l’adresse IP publique hello transfert toohello port RDP sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ebcff-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="ebcff-124">À l’aide de hello partagé IP</span><span class="sxs-lookup"><span data-stu-id="ebcff-124">Using hello shared IP</span></span>

- <span data-ttu-id="ebcff-125">**Les utilisateurs Linux :** SSH toohello machine virtuelle en utilisant l’adresse IP de hello ou nom de domaine complet, suivie du signe deux-points, suivi de port de hello.</span><span class="sxs-lookup"><span data-stu-id="ebcff-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="ebcff-126">Par exemple, dans l’image hello ci-dessous, hello RDP adresses toohello tooconnect machine virtuelle est `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="ebcff-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Exemple de machine virtuelle](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="ebcff-128">**Les utilisateurs Windows :** hello sélectionnez **Connect** bouton un fichier RDP préconfiguré hello toodownload portail Azure et accéder hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ebcff-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebcff-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebcff-129">Next steps</span></span>

* [<span data-ttu-id="ebcff-130">Définir des stratégies de laboratoire dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ebcff-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="ebcff-131">Configuration d’un réseau virtuel dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ebcff-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





