---
title: "Procédure de réinitialisation de l’interface réseau pour les machines virtuelles Windows Azure | Microsoft Docs"
description: "Montre comment réinitialiser l’interface réseau pour une machine virtuelle Windows Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 220e426be20086841854d89831f6c9d67529867f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="6c4f0-103">Comment réinitialiser l’interface réseau pour une machine virtuelle Windows Azure</span><span class="sxs-lookup"><span data-stu-id="6c4f0-103">How to reset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="6c4f0-104">Vous ne pouvez pas vous connecter à une machine virtuelle Microsoft Azure Windows après avoir désactivé l’interface réseau (carte réseau) par défaut ou défini manuellement une adresse IP statique pour la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-104">You cannot connect to Microsoft Azure Windows Virtual Machine (VM) after you disable the default Network Interface (NIC) or manually sets a static IP for the NIC.</span></span> <span data-ttu-id="6c4f0-105">Cet article explique comment réinitialiser l’interface réseau pour une machine virtuelle Windows Azure, ce qui résoudra le problème de connexion distante.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-105">This article shows how to reset the network interface for Azure Windows VM, which will resolve the remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="6c4f0-106">Réinitialiser l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="6c4f0-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="6c4f0-107">Pour les machines virtuelles Classic</span><span class="sxs-lookup"><span data-stu-id="6c4f0-107">For Classic VMs</span></span>

<span data-ttu-id="6c4f0-108">Pour réinitialiser l’interface réseau, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c4f0-108">To reset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="6c4f0-109">Accédez au [portail Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c4f0-109">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="6c4f0-110">Sélectionnez **Machines virtuelles (Classic)**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="6c4f0-111">Sélectionnez la machine virtuelle concernée.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-111">Select the affected Virtual Machine.</span></span>
4.  <span data-ttu-id="6c4f0-112">Sélectionnez **Adresses IP**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="6c4f0-113">Si l’**attribution d’adresse IP privée** n’est pas **Statique**, choisissez **Statique**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-113">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
6.  <span data-ttu-id="6c4f0-114">Modifiez l’**adresse IP** pour indiquer une autre adresse IP, disponible dans le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-114">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
7.  <span data-ttu-id="6c4f0-115">Sélectionnez Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-115">Select Save.</span></span>
8.  <span data-ttu-id="6c4f0-116">La machine virtuelle redémarre afin d’initialiser la nouvelle carte réseau pour le système.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-116">The virtual machine will restart to initialize the new NIC to the system.</span></span>
9.  <span data-ttu-id="6c4f0-117">Essayez d’utiliser le protocole RDP sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-117">Try to RDP to your machine.</span></span> <span data-ttu-id="6c4f0-118">En cas de réussite, vous pouvez redéfinir l’adresse IP privée d’origine si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-118">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="6c4f0-119">Sinon, vous pouvez conserver cette adresse.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="6c4f0-120">Pour les machines virtuelles déployées dans le modèle de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="6c4f0-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="6c4f0-121">Accédez au [portail Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c4f0-121">Go to the [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="6c4f0-122">Sélectionnez la machine virtuelle concernée.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-122">Select the affected Virtual Machine.</span></span>
3.  <span data-ttu-id="6c4f0-123">Sélectionnez **Interfaces réseau**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="6c4f0-124">Sélectionnez l’interface réseau associée à votre machine.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-124">Select the Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="6c4f0-125">Sélectionnez **Configurations IP**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="6c4f0-126">Sélectionnez l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-126">Select the IP.</span></span> 
7.  <span data-ttu-id="6c4f0-127">Si l’**attribution d’adresse IP privée** n’est pas **Statique**, choisissez **Statique**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-127">If the **Private IP assignment**  is not  **Static**, change it to **Static**.</span></span>
8.  <span data-ttu-id="6c4f0-128">Modifiez l’**adresse IP** pour indiquer une autre adresse IP, disponible dans le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-128">Change the **IP address** to another IP address that is available in the Subnet.</span></span>
9. <span data-ttu-id="6c4f0-129">La machine virtuelle redémarre afin d’initialiser la nouvelle carte réseau pour le système.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-129">The virtual machine will restart to initialize the new NIC to the system.</span></span>
10. <span data-ttu-id="6c4f0-130">Essayez d’utiliser le protocole RDP sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-130">Try to RDP to your machine.</span></span> <span data-ttu-id="6c4f0-131">En cas de réussite, vous pouvez redéfinir l’adresse IP privée d’origine si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-131">If successful, you can change the Private IP address back to the original if you would like.</span></span> <span data-ttu-id="6c4f0-132">Sinon, vous pouvez conserver cette adresse.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-the-unavailable-nics"></a><span data-ttu-id="6c4f0-133">Supprimer les cartes réseau non disponibles</span><span class="sxs-lookup"><span data-stu-id="6c4f0-133">Delete the unavailable NICs</span></span>
<span data-ttu-id="6c4f0-134">Une fois que vous pouvez vous connecter directement à la machine à l’aide du bureau à distance, vous devez supprimer les anciennes cartes réseau pour éviter tout problème potentiel :</span><span class="sxs-lookup"><span data-stu-id="6c4f0-134">After you can remote desktop to the machine, you must delete the old NICs to avoid the potential problem:</span></span>

1.  <span data-ttu-id="6c4f0-135">Ouvrez le Gestionnaire de périphériques.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="6c4f0-136">Sélectionnez **Afficher** > **Afficher les périphériques cachés**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="6c4f0-137">Sélectionnez **Adaptateurs réseau**.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="6c4f0-138">Recherchez les adaptateurs nommés « Carte réseau de bus Microsoft Hyper-V ».</span><span class="sxs-lookup"><span data-stu-id="6c4f0-138">Check for the adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="6c4f0-139">Il se peut qu’un adaptateur non disponible apparaisse grisé.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-139">You might see an unavailable adapter that is grayed out.</span></span> <span data-ttu-id="6c4f0-140">Cliquez avec le bouton droit sur l’adaptateur, puis sélectionnez Désinstaller.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-140">Right-click the adapter and then select Uninstall.</span></span>

    ![Image de la carte réseau](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="6c4f0-142">Désinstallez uniquement les adaptateurs non disponibles qui portent le nom « Carte réseau de bus Microsoft Hyper-V ».</span><span class="sxs-lookup"><span data-stu-id="6c4f0-142">Only uninstall the unavailable adapters that have the name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="6c4f0-143">Si vous désinstallez un autre adaptateur caché, cela peut entraîner des problèmes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-143">If you uninstall any of the other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="6c4f0-144">À présent, tous les adaptateurs indisponibles ont normalement été nettoyés sur votre système.</span><span class="sxs-lookup"><span data-stu-id="6c4f0-144">Now all unavailable adapter should be cleared out from your system.</span></span>