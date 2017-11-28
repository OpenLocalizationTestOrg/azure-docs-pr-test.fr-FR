---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)"
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
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="6125f-103">Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)</span><span class="sxs-lookup"><span data-stu-id="6125f-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="6125f-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6125f-104">Before you begin</span></span>
<span data-ttu-id="6125f-105">Consultez trop[considérations relatives à la mise en réseau pour les Services de domaine Active Directory Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="6125f-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="6125f-106">Tâche 2 : Configurer les paramètres réseau</span><span class="sxs-lookup"><span data-stu-id="6125f-106">Task 2: configure network settings</span></span>
<span data-ttu-id="6125f-107">tâche de configuration suivante Hello est toocreate un réseau virtuel Azure et un sous-réseau dédié qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="6125f-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="6125f-108">Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6125f-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="6125f-109">Vous pouvez également sélectionner un réseau virtuel existant et créer des sous-réseaux hello dédié qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="6125f-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="6125f-110">Cliquez sur **réseau virtuel** tooselect un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6125f-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="6125f-111">Sur hello **réseau virtuel de choisir** panneau, vous voyez tous les réseaux virtuels existants.</span><span class="sxs-lookup"><span data-stu-id="6125f-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="6125f-112">Vous voyez uniquement hello réseaux virtuels qui font partie de groupe de ressources toohello et l’emplacement Azure que vous avez sélectionné sur hello **notions de base** page de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="6125f-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="6125f-113">Choisissez hello de réseau virtuel dans lequel les Services de domaine Active Directory de Azure doivent être activées.</span><span class="sxs-lookup"><span data-stu-id="6125f-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="6125f-114">Cliquez sur **nouvel**, si vous préférez toocreate un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6125f-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="6125f-115">Nous vous recommandons vivement d’utiliser un sous-réseau dédié pour Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6125f-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="6125f-116">Si vous sélectionnez un réseau virtuel existant, [créer un sous-réseau dédié à l’aide d’extension de réseaux virtuels hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) et choisir ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6125f-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Sélectionner un réseau virtuel](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="6125f-118">Cliquez sur **sous-réseau** toopick hello sous-réseau dédié dans ce réseau virtuel, dans quel tooenable votre nouvelle gérés domaine.</span><span class="sxs-lookup"><span data-stu-id="6125f-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="6125f-119">Bonjour **créer sous-réseau** panneau, spécifiez un nom pour le sous-réseau de hello, puis cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="6125f-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="6125f-120">Par exemple, créer un sous-réseau portant le nom hello 'DomainServices', ce qui facilite d’autres administrateurs toounderstand ce qui est déployé dans le sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="6125f-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Choisissez le sous-réseau au sein du réseau virtuel de hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="6125f-122">**Indications pour la sélection d’un sous-réseau**</span><span class="sxs-lookup"><span data-stu-id="6125f-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="6125f-123">Utilisez un sous-réseau dédié pour Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="6125f-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="6125f-124">Ne déployez pas un autre sous-réseau toothis de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6125f-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="6125f-125">Cette configuration permet de tooconfigure les groupes de sécurité réseau (NSG) pour vos ordinateurs virtuels ou les charges de travail sans interrompre votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="6125f-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="6125f-126">Pour plus de détails, consultez [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="6125f-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="6125f-127">Ne sélectionnez pas de sous-réseau de passerelle hello pour le déploiement des Services de domaine Active Directory de Azure, car il n’est pas une configuration prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6125f-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="6125f-128">Assurez-vous que vous avez sélectionné le sous-réseau hello possède suffisamment d’espace disponible adresse - les adresses IP disponibles au moins de 3 à 5.</span><span class="sxs-lookup"><span data-stu-id="6125f-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="6125f-129">Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **groupe administrateur** page d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="6125f-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="6125f-130">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="6125f-130">Next step</span></span>
[<span data-ttu-id="6125f-131">Tâche 3 : Configurer le groupe d’administration et activer Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="6125f-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
