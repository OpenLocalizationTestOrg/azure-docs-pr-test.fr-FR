---
title: "Configuration d’un réseau virtuel dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment configurer un réseau virtuel et un sous-réseau existants, puis les utiliser dans une machine virtuelle avec Azure DevTest Labs"
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
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="f46dd-103">Configuration d’un réseau virtuel dans Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f46dd-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="f46dd-104">Comme expliqué dans l’article [Ajouter une machine virtuelle avec des artefacts à un laboratoire](devtest-lab-add-vm-with-artifacts.md), quand vous créez une machine virtuelle dans un laboratoire, vous pouvez spécifier un réseau virtuel configuré.</span><span class="sxs-lookup"><span data-stu-id="f46dd-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="f46dd-105">Voici l’un des scénarios de cette opération : vous devez être en mesure d'accéder aux ressources de votre réseau d'entreprise à partir de vos machines virtuelles à l'aide du réseau virtuel configuré avec ExpressRoute ou un VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="f46dd-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="f46dd-106">Les sections suivantes montrent comment ajouter votre réseau virtuel existant aux paramètres de réseau virtuel d’un labo afin qu'il puisse être sélectionné lors de la création de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f46dd-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="f46dd-107">Configurer un réseau virtuel pour un laboratoire en utilisant le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f46dd-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="f46dd-108">Les étapes suivantes vous montrent comment ajouter un réseau virtuel (et sous-réseau) existant à un laboratoire pour qu’il puisse être utilisé lors de la création d’une machine virtuelle dans le même laboratoire.</span><span class="sxs-lookup"><span data-stu-id="f46dd-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="f46dd-109">Connectez-vous au [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f46dd-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="f46dd-110">Sélectionnez **Autres services**, puis **DevTest Labs** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="f46dd-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="f46dd-111">Sélectionnez le laboratoire souhaité dans la liste des laboratoires.</span><span class="sxs-lookup"><span data-stu-id="f46dd-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="f46dd-112">Dans le panneau du laboratoire, sélectionnez **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="f46dd-113">Dans le panneau **Configuration** du laboratoire, sélectionnez **Réseaux virtuels**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="f46dd-114">Sur le panneau **Réseaux virtuels** , vous verrez une liste de réseaux virtuels configurés pour le labo actuel ainsi que le réseau virtuel par défaut créé pour votre labo.</span><span class="sxs-lookup"><span data-stu-id="f46dd-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="f46dd-115">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-115">Select **+ Add**.</span></span>
   
    ![Ajout d’un réseau virtuel existant à votre labo](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="f46dd-117">Sur le panneau **Réseau virtuel**, sélectionnez **[Sélectionner un réseau virtuel]**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![Sélection d’un réseau virtuel existant](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="f46dd-119">Sur le panneau **Choisissez un réseau virtuel** , sélectionnez le réseau virtuel souhaité.</span><span class="sxs-lookup"><span data-stu-id="f46dd-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="f46dd-120">Le panneau affiche tous les réseaux virtuels sous la même région de l'abonnement que le labo.</span><span class="sxs-lookup"><span data-stu-id="f46dd-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="f46dd-121">Après avoir sélectionné un réseau virtuel, vous êtes redirigé vers le **Réseau virtuel**. Cliquez sur le sous-réseau dans la liste située en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="f46dd-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![Liste des sous-réseaux](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="f46dd-123">Le panneau Lab Subnet (Sous-réseau de laboratoire) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f46dd-123">The Lab Subnet blade is displayed.</span></span>

    ![Panneau Lab Subnet (Sous-réseau de laboratoire)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="f46dd-125">Spécifiez un **nom de sous-réseau de laboratoire**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="f46dd-126">Pour permettre l’utilisation d’un sous-réseau dans le laboratoire de création de machines virtuelles, sélectionnez **Utiliser dans la création de machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="f46dd-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="f46dd-127">Pour activer une [adresse IP publique partagée](devtest-lab-shared-ip.md), sélectionnez **Enable shared public IP** (Activer l’adresse IP publique partagée).</span><span class="sxs-lookup"><span data-stu-id="f46dd-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="f46dd-128">Pour autoriser les adresses IP publiques dans un sous-réseau, sélectionnez **Allow public IP creation** (Autoriser la création d’adresses IP publiques).</span><span class="sxs-lookup"><span data-stu-id="f46dd-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="f46dd-129">Dans le champ **Nombre maximal de machines virtuelles par utilisateur**, spécifiez le nombre maximal de machines virtuelles par utilisateur pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f46dd-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="f46dd-130">Si vous souhaitez un nombre illimité de machines virtuelles, laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="f46dd-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="f46dd-131">Cliquez sur **OK** pour fermer le panneau Lab Subnet (Sous-réseau de laboratoire).</span><span class="sxs-lookup"><span data-stu-id="f46dd-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="f46dd-132">Sélectionnez **Enregistrer** pour fermer le panneau Réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f46dd-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="f46dd-133">Maintenant que le réseau virtuel est configuré, il peut être sélectionné lors de la création d'une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f46dd-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="f46dd-134">Pour voir comment créer une machine virtuelle et spécifier un réseau virtuel, consultez l’article [Ajouter une machine virtuelle avec des artefacts à un laboratoire](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f46dd-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="f46dd-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f46dd-135">Next steps</span></span>
<span data-ttu-id="f46dd-136">Une fois que vous avez ajouté le réseau virtuel souhaité à votre laboratoire, l’étape suivante consiste à [ajouter une machine virtuelle à votre laboratoire](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="f46dd-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

