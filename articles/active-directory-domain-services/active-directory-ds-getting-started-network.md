---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="1de1d-103">Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)</span><span class="sxs-lookup"><span data-stu-id="1de1d-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="1de1d-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1de1d-104">Before you begin</span></span>
<span data-ttu-id="1de1d-105">Reportez-vous à [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="1de1d-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="1de1d-106">Tâche 2 : Configurer les paramètres réseau</span><span class="sxs-lookup"><span data-stu-id="1de1d-106">Task 2: configure network settings</span></span>
<span data-ttu-id="1de1d-107">La tâche de configuration suivante consiste à créer un réseau virtuel Azure et un sous-réseau dédié à l’intérieur de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1de1d-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="1de1d-108">Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1de1d-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="1de1d-109">Vous pouvez également sélectionner un réseau virtuel actuel et créez le sous-réseau dédié à l’intérieur de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="1de1d-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="1de1d-110">Cliquez sur **Réseau virtuel** pour choisir un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1de1d-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="1de1d-111">Dans le panneau **Choisir un réseau virtuel**, vous voyez tous les réseaux virtuels actuels.</span><span class="sxs-lookup"><span data-stu-id="1de1d-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="1de1d-112">Vous voyez uniquement les réseaux virtuels qui appartiennent au groupe de ressources et à l’emplacement Azure que vous avez sélectionnés dans la page **Fonctions de base** de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="1de1d-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="1de1d-113">Choisissez le réseau virtuel dans lequel Azure AD Domain Services doit être activé.</span><span class="sxs-lookup"><span data-stu-id="1de1d-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="1de1d-114">Si vous préférez créer un réseau virtuel, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1de1d-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="1de1d-115">Nous vous recommandons vivement d’utiliser un sous-réseau dédié pour Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="1de1d-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="1de1d-116">Si vous sélectionnez un réseau virtuel existant, [créez un sous-réseau dédié à l’aide de l’extension de réseaux virtuels](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), puis choisissez ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="1de1d-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Sélectionner un réseau virtuel](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="1de1d-118">Cliquez sur **Sous-réseau** pour sélectionner le sous-réseau dédié dans ce réseau virtuel, dans lequel activer votre nouveau domaine managé.</span><span class="sxs-lookup"><span data-stu-id="1de1d-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="1de1d-119">Dans le panneau **Créer un sous-réseau**, spécifiez un nom pour le sous-réseau, puis cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="1de1d-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="1de1d-120">Par exemple, créez un sous-réseau nommé « DomainServices », de façon à aider les autres administrateurs à comprendre ce qui est déployé au sein du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="1de1d-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Sélectionner un sous-réseau au sein du réseau virtuel](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="1de1d-122">**Indications pour la sélection d’un sous-réseau**</span><span class="sxs-lookup"><span data-stu-id="1de1d-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="1de1d-123">Utilisez un sous-réseau dédié pour Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="1de1d-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="1de1d-124">Ne déployez pas d’autres machines virtuelles sur ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="1de1d-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="1de1d-125">Cette configuration vous permet de configurer des groupes de sécurité réseau (NSG) pour vos charges de travail ou machines virtuelles sans perturber votre domaine managé.</span><span class="sxs-lookup"><span data-stu-id="1de1d-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="1de1d-126">Pour plus de détails, consultez [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="1de1d-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="1de1d-127">Ne sélectionnez pas le sous-réseau de passerelle pour déployer Azure AD Domain Services, car cette configuration n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1de1d-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="1de1d-128">Vérifiez que le sous-réseau que vous avez sélectionné dispose d’un espace suffisant, comprenant entre 3 et 5 adresses IP disponibles.</span><span class="sxs-lookup"><span data-stu-id="1de1d-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="1de1d-129">Lorsque vous avez terminé, cliquez sur **OK** pour accéder à la page **Groupe des administrateurs** de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="1de1d-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="1de1d-130">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1de1d-130">Next step</span></span>
[<span data-ttu-id="1de1d-131">Tâche 3 : Configurer le groupe d’administration et activer Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="1de1d-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
