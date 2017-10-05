---
title: "Azure Active Directory Domain Services : créer ou sélectionner un réseau virtuel | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure Classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="e63e2-103">Créer ou sélectionner un réseau virtuel pour Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="e63e2-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="e63e2-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e63e2-104">Before you begin</span></span>
<span data-ttu-id="e63e2-105">Reportez-vous à [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="e63e2-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="e63e2-106">Tâche 2 : créer un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="e63e2-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="e63e2-107">La tâche de configuration suivante consiste à créer un réseau virtuel Azure et un sous-réseau à l’intérieur de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e63e2-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="e63e2-108">Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e63e2-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="e63e2-109">Si vous souhaitez utiliser un réseau virtuel existant, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="e63e2-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="e63e2-110">Assurez-vous que le réseau virtuel Azure que vous créez ou que vous choisissez d’utiliser avec Azure Active Directory Domain Services appartient à une région Azure qui est prise en charge par Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e63e2-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="e63e2-111">Pour connaître les régions Azure dans lesquelles Azure Active Directory Domain Services est disponible, consultez la page [Services Azure par région](https://azure.microsoft.com/regions/#services/) .</span><span class="sxs-lookup"><span data-stu-id="e63e2-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="e63e2-112">Notez le nom du réseau virtuel, car vous en aurez besoin au cours d’une étape de configuration ultérieure pour sélectionner le réseau virtuel adéquat au moment de l’activation d’Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e63e2-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="e63e2-113">Pour créer un réseau virtuel Azure dans lequel vous souhaitez activer Azure Active Directory Domain Services, suivez les instructions de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="e63e2-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="e63e2-114">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e63e2-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e63e2-115">Dans le volet gauche, sélectionnez **Réseaux**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="e63e2-116">![Nœud Réseaux](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="e63e2-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="e63e2-117">La fenêtre **Réseaux virtuels** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e63e2-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="e63e2-118">Dans le volet des tâches en bas de la fenêtre, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="e63e2-120">Cliquez sur **Services réseau**, puis sélectionnez **Réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Réseau virtuel : création rapide](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="e63e2-122">Pour créer un réseau virtuel, cliquez sur **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="e63e2-123">Spécifiez un **nom** pour votre réseau virtuel, et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e63e2-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="e63e2-124">Vous pouvez choisir de configurer **l’Espace d’adressage** ou le **Nombre maximal de machines virtuelles** pour ce réseau.</span><span class="sxs-lookup"><span data-stu-id="e63e2-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="e63e2-125">Vous pouvez laisser le paramètre du **serveur DNS** sur **Aucun** pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="e63e2-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="e63e2-126">Vous pourrez mettre à jour ce paramètre après avoir activé Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e63e2-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="e63e2-127">Dans la liste déroulante **Emplacement**, sélectionnez une région Azure prise en charge.</span><span class="sxs-lookup"><span data-stu-id="e63e2-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="e63e2-128">Pour connaître les régions Azure dans lesquelles Azure Active Directory Domain Services est disponible, consultez la page [Services Azure par région](https://azure.microsoft.com/regions/#services/) .</span><span class="sxs-lookup"><span data-stu-id="e63e2-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="e63e2-129">Pour créer votre réseau virtuel, cliquez sur **Créer un réseau virtuel** .</span><span class="sxs-lookup"><span data-stu-id="e63e2-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Créer un réseau virtuel pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="e63e2-131">Une fois que vous avez créé un réseau virtuel, sélectionnez son nom, puis cliquez sur l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Créer un sous-réseau](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="e63e2-133">Sous **Espaces d’adressage du réseau virtuel**, cliquez sur **Ajouter un sous-réseau**, puis spécifiez un sous-réseau avec le nom **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Créer un sous-réseau pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="e63e2-135">Pour créer le sous-réseau, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e63e2-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="e63e2-136">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e63e2-136">Next step</span></span>
[<span data-ttu-id="e63e2-137">Tâche 3 : Activer Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="e63e2-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
