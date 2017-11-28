---
title: "aaaConfigure un réseau virtuel dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooconfigure un réseau virtuel existant et un sous-réseau et les utiliser dans une machine virtuelle avec Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="e8d8e-103">Configuration d’un réseau virtuel dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e8d8e-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="e8d8e-104">Comme expliqué dans l’article hello, [ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md), lorsque vous créez une machine virtuelle dans un laboratoire, vous pouvez spécifier un réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="e8d8e-105">Un scénario pour cette opération est que si vous avez besoin de tooaccess vos ressources réseau d’entreprise à partir de vos machines virtuelles à l’aide de hello réseau virtuel qui a été configuré avec ExpressRoute ou VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="e8d8e-106">Hello sections suivantes illustrent comment tooadd votre réseau virtuel existant dans les paramètres de réseau virtuel d’un laboratoire afin qu’il soit toochoose disponible lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="e8d8e-107">Configurer un réseau virtuel pour un laboratoire à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e8d8e-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="e8d8e-108">Hello étapes suivantes vous guident tout ajout d’un laboratoire de tooa réseau (et de sous-réseau) virtuel existant afin qu’il peut être utilisé lors de la création d’une machine virtuelle Bonjour même laboratoire.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="e8d8e-109">Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e8d8e-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="e8d8e-110">Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="e8d8e-111">Dans liste hello labs, sélectionnez lab souhaité de hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="e8d8e-112">Dans le panneau de hello lab, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="e8d8e-113">Sur du laboratoire hello **Configuration** panneau, sélectionnez **réseaux virtuels**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="e8d8e-114">Sur hello **réseaux virtuels** panneau, vous voyez une liste de réseaux virtuels configurés pour pratiques hello ainsi que de réseau virtuel hello par défaut qui est créé pour votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="e8d8e-115">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-115">Select **+ Add**.</span></span>
   
    ![Ajouter un laboratoire tooyour de réseau virtuel existant](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="e8d8e-117">Sur hello **réseau virtuel** panneau, sélectionnez **[réseau virtuel]**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Sélection d’un réseau virtuel existant](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="e8d8e-119">Sur hello **réseau virtuel de choisir** panneau, le réseau virtuel auquel vous souhaitez hello select.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="e8d8e-120">panneau Hello affiche tous les réseaux virtuels hello qui sont sous hello même région dans l’abonnement hello comme lab de hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="e8d8e-121">Après avoir sélectionné un réseau virtuel, vous êtes renvoyé toohello **réseau virtuel** cliquez sur le sous-réseau hello dans liste hello bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![Liste des sous-réseaux](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="e8d8e-123">Panneau de sous-réseau d’atelier Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-123">hello Lab Subnet blade is displayed.</span></span>

    ![Panneau Lab Subnet (Sous-réseau de laboratoire)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="e8d8e-125">Spécifiez un **nom de sous-réseau de laboratoire**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="e8d8e-126">tooallow un toobe de sous-réseau utilisé dans le laboratoire de la création d’ordinateurs virtuels, sélectionnez **utilisé dans la création de la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="e8d8e-127">tooenable un [partagé d’adresse IP publique](devtest-lab-shared-ip.md), sélectionnez **activer partagée d’adresse IP publique**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="e8d8e-128">les adresses IP publiques tooallow dans un sous-réseau, sélectionnez **permettre la création d’IP publique**.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="e8d8e-129">Bonjour **virtuels Maximum par utilisateur** indiquez hello maximales machines virtuelles par utilisateur pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="e8d8e-130">Si vous souhaitez un nombre illimité de machines virtuelles, laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="e8d8e-131">Sélectionnez **OK** Panneau de sous-réseau de l’atelier tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="e8d8e-132">Sélectionnez **enregistrer** Panneau de réseau virtuel tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="e8d8e-133">Maintenant que hello réseau virtuel est configuré, il peut être sélectionné lors de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e8d8e-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="e8d8e-134">toosee comment toocreate une machine virtuelle et spécifier un réseau virtuel, consultez l’article toohello [ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8d8e-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="e8d8e-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8d8e-135">Next steps</span></span>
<span data-ttu-id="e8d8e-136">Lorsque vous avez ajouté hello souhaité lab tooyour de réseau virtuel, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="e8d8e-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

