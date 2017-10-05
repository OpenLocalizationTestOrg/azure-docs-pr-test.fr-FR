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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 47507096a6245d4f1ba57a652ddf5167b3776ae9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="25159-103">Activer Azure Active Directory Domain Services à l’aide du portail Azure (préversion)</span><span class="sxs-lookup"><span data-stu-id="25159-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>
<span data-ttu-id="25159-104">Cet article explique comment activer Azure Active Directory Domain Services (Azure AD DS) au moyen du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="25159-104">This article shows how to enable Azure Active Directory Domain Services (Azure AD DS) using the Azure portal.</span></span>


<span data-ttu-id="25159-105">Pour lancer l’Assistant **Activer Azure AD Domain Services**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="25159-105">To launch the **Enable Azure AD Domain Services** wizard, complete the following steps:</span></span>

1. <span data-ttu-id="25159-106">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25159-106">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="25159-107">Dans le volet gauche, cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="25159-107">In the left pane, click on **New**.</span></span>
3. <span data-ttu-id="25159-108">Dans le panneau **Nouveau**, tapez **Domain Services** dans la barre de recherche.</span><span class="sxs-lookup"><span data-stu-id="25159-108">In the **New** blade, type **Domain Services** into the search bar.</span></span>

    ![Rechercher Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="25159-110">Dans la liste des suggestions de recherche, cliquez pour sélectionner **Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="25159-110">Click to select **Azure AD Domain Services** from the list of search suggestions.</span></span> <span data-ttu-id="25159-111">Dans le panneau **Azure AD Domain Services**, cliquez sur le bouton **Créer**.</span><span class="sxs-lookup"><span data-stu-id="25159-111">On the **Azure AD Domain Services** blade, click the **Create** button.</span></span>

    ![Panneau Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="25159-113">L’Assistant **Activer Azure AD Domain Services** est lancé.</span><span class="sxs-lookup"><span data-stu-id="25159-113">The **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="25159-114">Tâche 1 : Configurer les paramètres de base</span><span class="sxs-lookup"><span data-stu-id="25159-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="25159-115">Dans la page **Fonctions de base** de l’Assistant, vous pouvez spécifier le nom de domaine DNS pour le domaine managé.</span><span class="sxs-lookup"><span data-stu-id="25159-115">In the **Basics** page of the wizard, you can specify the DNS domain name for the managed domain.</span></span> <span data-ttu-id="25159-116">Vous pouvez également choisir le groupe de ressources et l’emplacement Azure sur lequel le domaine managé doit être déployé.</span><span class="sxs-lookup"><span data-stu-id="25159-116">You can also choose the resource group and Azure location to which the managed domain should be deployed.</span></span>

![Configurer les fonctions de base](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="25159-118">Choisissez le **Nom de domaine DNS** pour votre domaine managé.</span><span class="sxs-lookup"><span data-stu-id="25159-118">Choose the **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="25159-119">Le nom de domaine par défaut du répertoire (avec un suffixe **.onmicrosoft.com**) est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="25159-119">The default domain name of the directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="25159-120">Vous pouvez également entrer un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="25159-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="25159-121">Dans cet exemple, le nom de domaine personnalisé est *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="25159-121">In this example, the custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="25159-122">Le préfixe du nom de domaine spécifié (par exemple, *contoso100* dans le nom de domaine *contoso100.com*) doit contenir au maximum 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="25159-122">The prefix of your specified domain name (for example, *contoso100* in the *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="25159-123">Vous ne pouvez pas créer de domaine managé avec un préfixe de plus de 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="25159-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="25159-124">Vérifiez que le nom de domaine DNS choisi pour le domaine géré n’existe pas au sein du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="25159-124">Ensure that the DNS domain name you have chosen for the managed domain does not already exist in the virtual network.</span></span> <span data-ttu-id="25159-125">Plus spécifiquement, vérifiez les poins suivants :</span><span class="sxs-lookup"><span data-stu-id="25159-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="25159-126">Vous disposez d’un domaine présentant le nom de domaine DNS au sein du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="25159-126">You already have a domain with the same DNS domain name on the virtual network.</span></span>

   * <span data-ttu-id="25159-127">Le réseau virtuel dans lequel vous envisagez d’activer le domaine managé a une connexion VPN avec votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="25159-127">The virtual network where you plan to enable the managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="25159-128">Dans ce scénario, veillez à ne pas avoir de domaine portant le même nom de domaine DNS sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="25159-128">In this scenario, ensure you don't have a domain with the same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="25159-129">Il existe un service cloud portant ce nom sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="25159-129">You have an existing cloud service with that name on the virtual network.</span></span>

3. <span data-ttu-id="25159-130">Choisissez le **type de réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="25159-130">Choose the **type of virtual network**.</span></span> <span data-ttu-id="25159-131">Le type de réseau virtuel **Resource Manager** est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="25159-131">By default, the **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="25159-132">Nous vous recommandons d’utiliser ce type de réseau virtuel pour tous les nouveaux domaines managés.</span><span class="sxs-lookup"><span data-stu-id="25159-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="25159-133">Sélectionnez l’**Abonnement** Azure dans lequel vous souhaitez créer le domaine managé.</span><span class="sxs-lookup"><span data-stu-id="25159-133">Select the Azure **Subscription** in which you would like to create the managed domain.</span></span>

5. <span data-ttu-id="25159-134">Sélectionnez le **Groupe de ressources** auquel le domaine managé doit appartenir.</span><span class="sxs-lookup"><span data-stu-id="25159-134">Select the **Resource group** to which the managed domain should belong.</span></span> <span data-ttu-id="25159-135">Vous avez le choix entre les options **Créer** ou **Utiliser l’existant** pour sélectionner le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="25159-135">You can choose either the **Create new** or **Use existing** options to select the resource group.</span></span>

6. <span data-ttu-id="25159-136">Choisissez l’**Emplacement** Azure dans lequel créer le domaine managé.</span><span class="sxs-lookup"><span data-stu-id="25159-136">Choose the Azure **Location** in which the managed domain should be created.</span></span> <span data-ttu-id="25159-137">Dans la page **Réseau** de l’Assistant, vous voyez uniquement les réseaux virtuels appartenant à l’emplacement que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="25159-137">On the **Network** page of the wizard, you see only virtual networks that belong to the location you have selected.</span></span>

7. <span data-ttu-id="25159-138">Lorsque vous avez terminé, cliquez sur **OK** pour accéder à la page **Réseau** de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="25159-138">When you are done, click **OK** to move on to the **Network** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="25159-139">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="25159-139">Next step</span></span>
[<span data-ttu-id="25159-140">Tâche 2 : Configurer les paramètres réseau</span><span class="sxs-lookup"><span data-stu-id="25159-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
