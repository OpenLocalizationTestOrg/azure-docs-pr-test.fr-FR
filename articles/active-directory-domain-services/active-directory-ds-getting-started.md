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
ms.date: 08/28/2017
ms.author: maheshu
ms.openlocfilehash: 79cbb21c4a50194f5ad8ca1a4a8493ee4a260a9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="91c96-103">Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)</span><span class="sxs-lookup"><span data-stu-id="91c96-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>
<span data-ttu-id="91c96-104">Cet article explique comment tooenable Active Directory domaine Services Azure (Azure AD DS) à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="91c96-104">This article shows how tooenable Azure Active Directory Domain Services (Azure AD DS) using hello Azure portal.</span></span>


<span data-ttu-id="91c96-105">toolaunch hello **activer un domaine Azure AD Services** hello Assistant, complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="91c96-105">toolaunch hello **Enable Azure AD Domain Services** wizard, complete hello following steps:</span></span>

1. <span data-ttu-id="91c96-106">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91c96-106">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="91c96-107">Dans le volet gauche de hello, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="91c96-107">In hello left pane, click on **New**.</span></span>
3. <span data-ttu-id="91c96-108">Bonjour **nouveau** panneau, tapez **Services de domaine** dans la barre de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-108">In hello **New** blade, type **Domain Services** into hello search bar.</span></span>

    ![Rechercher Domain Services](./media/getting-started/search-domain-services.png)

4. <span data-ttu-id="91c96-110">Cliquez sur tooselect **les Services de domaine Active Directory de Azure** à partir de la liste de hello des suggestions de recherche.</span><span class="sxs-lookup"><span data-stu-id="91c96-110">Click tooselect **Azure AD Domain Services** from hello list of search suggestions.</span></span> <span data-ttu-id="91c96-111">Sur hello **les Services de domaine Active Directory de Azure** panneau, cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="91c96-111">On hello **Azure AD Domain Services** blade, click hello **Create** button.</span></span>

    ![Panneau Domain Services](./media/getting-started/domain-services-blade.png)

5. <span data-ttu-id="91c96-113">Hello **activer un domaine Azure AD Services** Assistant est lancé.</span><span class="sxs-lookup"><span data-stu-id="91c96-113">hello **Enable Azure AD Domain Services** wizard is launched.</span></span>


## <a name="task-1-configure-basic-settings"></a><span data-ttu-id="91c96-114">Tâche 1 : Configurer les paramètres de base</span><span class="sxs-lookup"><span data-stu-id="91c96-114">Task 1: configure basic settings</span></span>
<span data-ttu-id="91c96-115">Bonjour **notions de base** page de l’Assistant de hello, vous pouvez spécifier le nom de domaine DNS hello pour le domaine géré de hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-115">In hello **Basics** page of hello wizard, you can specify hello DNS domain name for hello managed domain.</span></span> <span data-ttu-id="91c96-116">Vous pouvez également choisir le groupe de ressources hello et emplacement Azure toowhich hello managé domaine doit être déployé.</span><span class="sxs-lookup"><span data-stu-id="91c96-116">You can also choose hello resource group and Azure location toowhich hello managed domain should be deployed.</span></span>

![Configurer les fonctions de base](./media/getting-started/domain-services-blade-basics.png)

1. <span data-ttu-id="91c96-118">Choisissez hello **nom de domaine DNS** pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="91c96-118">Choose hello **DNS domain name** for your managed domain.</span></span>

   * <span data-ttu-id="91c96-119">nom de domaine par défaut Hello du répertoire de hello (avec un **. onmicrosoft.com** suffixe) est spécifié par défaut.</span><span class="sxs-lookup"><span data-stu-id="91c96-119">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is specified by default.</span></span>

   * <span data-ttu-id="91c96-120">Vous pouvez également entrer un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="91c96-120">You can also type in a custom domain name.</span></span> <span data-ttu-id="91c96-121">Dans cet exemple, le nom de domaine personnalisé hello est *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="91c96-121">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="91c96-122">préfixe Hello de votre nom de domaine spécifié (par exemple, *contoso100* Bonjour *contoso100.com* nom de domaine) doit contenir au maximum 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="91c96-122">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="91c96-123">Vous ne pouvez pas créer de domaine managé avec un préfixe de plus de 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="91c96-123">You cannot create a managed domain with a prefix longer than 15 characters.</span></span>
     >
     >

2. <span data-ttu-id="91c96-124">Vérifiez que nom de domaine DNS hello choisie pour hello géré domaine n’existe pas déjà dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-124">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="91c96-125">Plus spécifiquement, vérifiez les poins suivants :</span><span class="sxs-lookup"><span data-stu-id="91c96-125">Specifically, check whether:</span></span>

   * <span data-ttu-id="91c96-126">Vous disposez déjà d’un domaine avec hello même nom de domaine DNS sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-126">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="91c96-127">réseau virtuel de Hello où vous prévoyez de domaine géré de hello tooenable a une connexion VPN avec votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="91c96-127">hello virtual network where you plan tooenable hello managed domain has a VPN connection with your on-premises network.</span></span> <span data-ttu-id="91c96-128">Dans ce scénario, assurez-vous de vous n’avez pas un domaine avec hello même nom de domaine DNS de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="91c96-128">In this scenario, ensure you don't have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="91c96-129">Vous avez un service cloud existant portant le même nom sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-129">You have an existing cloud service with that name on hello virtual network.</span></span>

3. <span data-ttu-id="91c96-130">Choisissez hello **type de réseau virtuel**.</span><span class="sxs-lookup"><span data-stu-id="91c96-130">Choose hello **type of virtual network**.</span></span> <span data-ttu-id="91c96-131">Par défaut, hello **le Gestionnaire de ressources** type de réseau virtuel est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="91c96-131">By default, hello **Resource Manager** virtual network type is selected.</span></span> <span data-ttu-id="91c96-132">Nous vous recommandons d’utiliser ce type de réseau virtuel pour tous les nouveaux domaines managés.</span><span class="sxs-lookup"><span data-stu-id="91c96-132">We recommend using this type of virtual network for all newly created managed domains.</span></span>

4. <span data-ttu-id="91c96-133">Sélectionnez hello Azure **abonnement** dans lequel vous souhaitez que le domaine géré de toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-133">Select hello Azure **Subscription** in which you would like toocreate hello managed domain.</span></span>

5. <span data-ttu-id="91c96-134">Sélectionnez hello **groupe de ressources** domaine géré de hello toowhich doit appartenir.</span><span class="sxs-lookup"><span data-stu-id="91c96-134">Select hello **Resource group** toowhich hello managed domain should belong.</span></span> <span data-ttu-id="91c96-135">Vous pouvez choisir soit hello **nouvel** ou **utiliser l’existante** groupe de ressources options tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-135">You can choose either hello **Create new** or **Use existing** options tooselect hello resource group.</span></span>

6. <span data-ttu-id="91c96-136">Choisissez hello Azure **emplacement** dans quels hello domaine géré doit être créé.</span><span class="sxs-lookup"><span data-stu-id="91c96-136">Choose hello Azure **Location** in which hello managed domain should be created.</span></span> <span data-ttu-id="91c96-137">Sur hello **réseau** page de l’Assistant de hello, vous voyez des réseaux virtuels uniquement appartenant emplacement toohello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="91c96-137">On hello **Network** page of hello wizard, you see only virtual networks that belong toohello location you have selected.</span></span>

7. <span data-ttu-id="91c96-138">Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **réseau** page d’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="91c96-138">When you are done, click **OK** toomove on toohello **Network** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="91c96-139">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="91c96-139">Next step</span></span>
[<span data-ttu-id="91c96-140">Tâche 2 : Configurer les paramètres réseau</span><span class="sxs-lookup"><span data-stu-id="91c96-140">Task 2: configure network settings</span></span>](active-directory-ds-getting-started-network.md)
