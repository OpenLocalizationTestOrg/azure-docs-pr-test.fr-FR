---
title: "interface réseau Windows Azure VM aaaHow tooreset | Documents Microsoft"
description: "Montre comment tooreset interface réseau pour la machine virtuelle de Windows Azure"
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
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a><span data-ttu-id="9d152-103">Comment tooreset interface réseau pour la machine virtuelle de Windows Azure</span><span class="sxs-lookup"><span data-stu-id="9d152-103">How tooreset network interface for Azure Windows VM</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9d152-104">Vous ne peut pas se connecter à tooMicrosoft Machine virtuelle de Windows Azure (VM) après la désactivation de la valeur par défaut de hello d’Interface réseau (NIC) ou manuellement définit une adresse IP statique pour la carte réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="9d152-104">You cannot connect tooMicrosoft Azure Windows Virtual Machine (VM) after you disable hello default Network Interface (NIC) or manually sets a static IP for hello NIC.</span></span> <span data-ttu-id="9d152-105">Cet article explique comment tooreset hello interface réseau de l’ordinateur virtuel Windows Azure, qui résout le problème de connexion à distance hello.</span><span class="sxs-lookup"><span data-stu-id="9d152-105">This article shows how tooreset hello network interface for Azure Windows VM, which will resolve hello remote connection issue.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a><span data-ttu-id="9d152-106">Réinitialiser l’interface réseau</span><span class="sxs-lookup"><span data-stu-id="9d152-106">Reset network interface</span></span>

### <a name="for-classic-vms"></a><span data-ttu-id="9d152-107">Pour les machines virtuelles Classic</span><span class="sxs-lookup"><span data-stu-id="9d152-107">For Classic VMs</span></span>

<span data-ttu-id="9d152-108">tooreset réseau de l’interface, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d152-108">tooreset network interface, follow these steps:</span></span>

1.  <span data-ttu-id="9d152-109">Accédez toohello [portail Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d152-109">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="9d152-110">Sélectionnez **Machines virtuelles (Classic)**.</span><span class="sxs-lookup"><span data-stu-id="9d152-110">Select **Virtual Machines (Classic)**.</span></span>
3.  <span data-ttu-id="9d152-111">Sélectionnez hello affectées de Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d152-111">Select hello affected Virtual Machine.</span></span>
4.  <span data-ttu-id="9d152-112">Sélectionnez **Adresses IP**.</span><span class="sxs-lookup"><span data-stu-id="9d152-112">Select **IP addresses**.</span></span>
5.  <span data-ttu-id="9d152-113">Si hello **l’attribution IP privé** n’est pas **statique**, modifiez-le trop**statique**.</span><span class="sxs-lookup"><span data-stu-id="9d152-113">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
6.  <span data-ttu-id="9d152-114">Hello de modification **adresse IP** tooanother adresse IP disponible dans hello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9d152-114">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
7.  <span data-ttu-id="9d152-115">Sélectionnez Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="9d152-115">Select Save.</span></span>
8.  <span data-ttu-id="9d152-116">machine virtuelle de Hello redémarre tooinitialize hello nouveau NIC toohello système.</span><span class="sxs-lookup"><span data-stu-id="9d152-116">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
9.  <span data-ttu-id="9d152-117">Essayez tooRDP tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="9d152-117">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="9d152-118">En cas de réussite, vous pouvez modifier hello IP privé adresse arrière toohello d’origine si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9d152-118">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="9d152-119">Sinon, vous pouvez conserver cette adresse.</span><span class="sxs-lookup"><span data-stu-id="9d152-119">Otherwise, you can keep it.</span></span> 

### <a name="for-vms-deployed-in-resource-group-model"></a><span data-ttu-id="9d152-120">Pour les machines virtuelles déployées dans le modèle de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9d152-120">For VMs deployed in Resource group model</span></span>

1.  <span data-ttu-id="9d152-121">Accédez toohello [portail Azure]( https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d152-121">Go toohello [Azure portal]( https://ms.portal.azure.com).</span></span>
2.  <span data-ttu-id="9d152-122">Sélectionnez hello affectées de Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d152-122">Select hello affected Virtual Machine.</span></span>
3.  <span data-ttu-id="9d152-123">Sélectionnez **Interfaces réseau**.</span><span class="sxs-lookup"><span data-stu-id="9d152-123">Select **Network Interfaces**.</span></span>
4.  <span data-ttu-id="9d152-124">Sélectionnez hello Qu'interface réseau associé à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="9d152-124">Select hello Network Interface associated with your machine</span></span>
5.  <span data-ttu-id="9d152-125">Sélectionnez **Configurations IP**.</span><span class="sxs-lookup"><span data-stu-id="9d152-125">Select **IP configurations**.</span></span>
6.  <span data-ttu-id="9d152-126">Sélectionnez adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="9d152-126">Select hello IP.</span></span> 
7.  <span data-ttu-id="9d152-127">Si hello **l’attribution IP privé** n’est pas **statique**, modifiez-le trop**statique**.</span><span class="sxs-lookup"><span data-stu-id="9d152-127">If hello **Private IP assignment**  is not  **Static**, change it too**Static**.</span></span>
8.  <span data-ttu-id="9d152-128">Hello de modification **adresse IP** tooanother adresse IP disponible dans hello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9d152-128">Change hello **IP address** tooanother IP address that is available in hello Subnet.</span></span>
9. <span data-ttu-id="9d152-129">machine virtuelle de Hello redémarre tooinitialize hello nouveau NIC toohello système.</span><span class="sxs-lookup"><span data-stu-id="9d152-129">hello virtual machine will restart tooinitialize hello new NIC toohello system.</span></span>
10. <span data-ttu-id="9d152-130">Essayez tooRDP tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="9d152-130">Try tooRDP tooyour machine.</span></span> <span data-ttu-id="9d152-131">En cas de réussite, vous pouvez modifier hello IP privé adresse arrière toohello d’origine si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="9d152-131">If successful, you can change hello Private IP address back toohello original if you would like.</span></span> <span data-ttu-id="9d152-132">Sinon, vous pouvez conserver cette adresse.</span><span class="sxs-lookup"><span data-stu-id="9d152-132">Otherwise, you can keep it.</span></span> 

## <a name="delete-hello-unavailable-nics"></a><span data-ttu-id="9d152-133">Supprimer hello cartes réseau non disponible</span><span class="sxs-lookup"><span data-stu-id="9d152-133">Delete hello unavailable NICs</span></span>
<span data-ttu-id="9d152-134">Une fois que vous pouvez les ordinateur toohello Bureau à distance, vous devez supprimer le problème potentiel de hello anciennes cartes réseau tooavoid hello :</span><span class="sxs-lookup"><span data-stu-id="9d152-134">After you can remote desktop toohello machine, you must delete hello old NICs tooavoid hello potential problem:</span></span>

1.  <span data-ttu-id="9d152-135">Ouvrez le Gestionnaire de périphériques.</span><span class="sxs-lookup"><span data-stu-id="9d152-135">Open Device Manager.</span></span>
2.  <span data-ttu-id="9d152-136">Sélectionnez **Afficher** > **Afficher les périphériques cachés**.</span><span class="sxs-lookup"><span data-stu-id="9d152-136">Select **View** > **Show hidden devices**.</span></span>
3.  <span data-ttu-id="9d152-137">Sélectionnez **Adaptateurs réseau**.</span><span class="sxs-lookup"><span data-stu-id="9d152-137">Select **Network Adapters**.</span></span> 
4.  <span data-ttu-id="9d152-138">Rechercher les cartes de hello nommés en tant que « Carte de réseau Microsoft Hyper-V ».</span><span class="sxs-lookup"><span data-stu-id="9d152-138">Check for hello adapters named as "Microsoft Hyper-V Network Adapter".</span></span>
5.  <span data-ttu-id="9d152-139">Il se peut qu’un adaptateur non disponible apparaisse grisé. L’adaptateur hello d’avec le bouton droit, puis sélectionnez Désinstaller.</span><span class="sxs-lookup"><span data-stu-id="9d152-139">You might see an unavailable adapter that is grayed out. Right-click hello adapter and then select Uninstall.</span></span>

    ![image Hello Hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > <span data-ttu-id="9d152-141">Désinstaller uniquement les adaptateurs indisponible hello qui portent le nom hello « Carte de réseau Microsoft Hyper-V ».</span><span class="sxs-lookup"><span data-stu-id="9d152-141">Only uninstall hello unavailable adapters that have hello name "Microsoft Hyper-V Network Adapter".</span></span> <span data-ttu-id="9d152-142">Si vous désinstallez des hello autres adaptateurs masquées, elle peut entraîner des problèmes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9d152-142">If you uninstall any of hello other hidden adapters, it could cause additional issues.</span></span>
    >
    >

6.  <span data-ttu-id="9d152-143">À présent, tous les adaptateurs indisponibles ont normalement été nettoyés sur votre système.</span><span class="sxs-lookup"><span data-stu-id="9d152-143">Now all unavailable adapter should be cleared out from your system.</span></span>