---
title: "Azure Active Directory Domain Services : créer ou sélectionner un réseau virtuel | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
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
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="9ce05-103">Créer ou sélectionner un réseau virtuel pour Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="9ce05-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="9ce05-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9ce05-104">Before you begin</span></span>
<span data-ttu-id="9ce05-105">Consultez trop[considérations relatives à la mise en réseau pour les Services de domaine Active Directory Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="9ce05-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="9ce05-106">Tâche 2 : créer un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="9ce05-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="9ce05-107">tâche de configuration suivante Hello est toocreate un réseau virtuel Azure et un sous-réseau qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="9ce05-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="9ce05-108">Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9ce05-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="9ce05-109">Si vous avez un réseau virtuel existant que vous préférez toouse, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="9ce05-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce05-110">Assurez-vous que ce réseau virtuel Azure que vous créez ou choisissez toouse avec Azure Active Directory Domain Services appartient tooan région Azure qui est pris en charge par les Services de domaine Active Directory Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9ce05-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="9ce05-111">tooascertain hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="9ce05-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="9ce05-112">Notez le nom hello de hello tooensure de réseau virtuel que vous sélectionnez réseau virtuel à droite de hello lorsque vous activez Azure Active Directory Domain Services dans une étape de configuration suivantes.</span><span class="sxs-lookup"><span data-stu-id="9ce05-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="9ce05-113">toocreate un réseau virtuel Azure dans lequel vous souhaitez tooenable Azure Active Directory Domain Services, suivez les instructions de configuration :</span><span class="sxs-lookup"><span data-stu-id="9ce05-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="9ce05-114">Accédez toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9ce05-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9ce05-115">Dans le volet gauche de hello, sélectionnez **réseaux**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="9ce05-116">![Nœud Réseaux](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="9ce05-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="9ce05-117">Hello **réseaux virtuels** fenêtre s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="9ce05-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="9ce05-118">Dans le volet des tâches hello bas hello de fenêtre hello, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Fenêtre Réseaux virtuels](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="9ce05-120">Cliquez sur **Services réseau**, puis sélectionnez **Réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Réseau virtuel : création rapide](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="9ce05-122">toocreate un réseau virtuel, cliquez sur **création rapide**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="9ce05-123">Spécifiez un **nom** pour votre machine virtuelle, réseau et de prendre en compte la manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="9ce05-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="9ce05-124">Vous pouvez choisir tooconfigure **l’espace d’adressage** ou **nombre d’ordinateurs virtuels Maximum** pour ce réseau.</span><span class="sxs-lookup"><span data-stu-id="9ce05-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="9ce05-125">Vous pouvez laisser hello **serveur DNS** définition en tant que **aucun** pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="9ce05-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="9ce05-126">Vous pouvez mettre à jour le paramètre de hello après avoir activé Azure des Services de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9ce05-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="9ce05-127">Bonjour **emplacement** liste déroulante, sélectionnez une région Azure prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9ce05-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="9ce05-128">tooascertain hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible, consultez [des services Azure par région](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="9ce05-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="9ce05-129">toocreate votre réseau virtuel, cliquez sur **créer un réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Créer un réseau virtuel pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="9ce05-131">Une fois que vous avez créé un réseau virtuel, sélectionnez le nom hello du réseau virtuel de hello, puis cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="9ce05-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Créer un sous-réseau](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="9ce05-133">Sous **espaces d’adressage de réseau virtuel**, cliquez sur **ajouter un sous-réseau**, puis spécifiez un sous-réseau nommé hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Créer un sous-réseau pour Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="9ce05-135">toocreate hello sous-réseau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9ce05-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="9ce05-136">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9ce05-136">Next step</span></span>
[<span data-ttu-id="9ce05-137">Tâche 3 : Activer Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="9ce05-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
