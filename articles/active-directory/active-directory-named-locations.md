---
title: "Emplacements nommés dans Azure Active Directory | Documents Microsoft"
description: "En configurant des emplacements nommés, vous pouvez éviter que des adresses IP appartenant à votre organisation ne génèrent de faux positifs pour le type d’événement à risque Voyage impossible vers des emplacements inhabituels."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ff31ded1d9d60e47e0ae5f01119de78cd7f2df38
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="f507f-103">Emplacements nommés dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f507f-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="f507f-104">Grâce à la fonctionnalité des emplacements nommés Azure Active Directory, vous pouvez désigner des plages d’adresses IP approuvées au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="f507f-104">With the named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="f507f-105">Dans votre environnement, vous pouvez utiliser les emplacements nommés dans le cadre de la détection d’[événements à risque](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f507f-105">In your environment, you can use named locations in the context of the detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="f507f-106">Cette fonction permet de réduire le nombre de faux-positifs signalés pour le type d’événement à risque *Voyage impossible vers des emplacements inhabituels*.</span><span class="sxs-lookup"><span data-stu-id="f507f-106">The feature helps reduce the number of reported false positives for the *Impossible travel to atypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="f507f-107">Configuration</span><span class="sxs-lookup"><span data-stu-id="f507f-107">Configuration</span></span>

<span data-ttu-id="f507f-108">Pour configurer un emplacement nommé :</span><span class="sxs-lookup"><span data-stu-id="f507f-108">To configure a named location:</span></span>

1. <span data-ttu-id="f507f-109">Connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général.</span><span class="sxs-lookup"><span data-stu-id="f507f-109">Sign in to the [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="f507f-110">Dans le volet gauche, cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f507f-110">In the left pane, click **Azure Active Directory**.</span></span>

    ![Lien Azure Active Directory dans le volet gauche](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="f507f-112">Dans le panneau **Azure Active Directory**, sous la section **Sécurité**, cliquez sur **Accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="f507f-112">On the **Azure Active Directory** blade, in the **Security** section, click **Conditional access**.</span></span>

    ![Commande Accès conditionnel](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="f507f-114">Dans le panneau **Azure Active Directory**, sous la section **Gérer**, cliquez sur **Emplacements nommés**.</span><span class="sxs-lookup"><span data-stu-id="f507f-114">On the **Conditional Access** blade, in the **Manage** section, click **Named locations**.</span></span>

    ![Commande Emplacements nommés](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="f507f-116">Dans le panneau **Emplacements nommés**, cliquez sur **Nouvel emplacement**.</span><span class="sxs-lookup"><span data-stu-id="f507f-116">On the **Named locations** blade, click **New location**.</span></span>

    ![Commande Nouvel emplacement](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="f507f-118">Dans le panneau **Nouveau**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f507f-118">On the **New** blade, do the following:</span></span>

    ![Panneau Nouveau](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="f507f-120">a.</span><span class="sxs-lookup"><span data-stu-id="f507f-120">a.</span></span> <span data-ttu-id="f507f-121">Dans la zone de texte **Nom**, tapez un nom pour votre emplacement nommé.</span><span class="sxs-lookup"><span data-stu-id="f507f-121">In the **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="f507f-122">b.</span><span class="sxs-lookup"><span data-stu-id="f507f-122">b.</span></span> <span data-ttu-id="f507f-123">Dans la zone de texte **Plage d’adresses IP**, tapez une plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="f507f-123">In the **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="f507f-124">La plage d’adresses IP doit être au format *CIDR* (Classless Inter-Domain Routing).</span><span class="sxs-lookup"><span data-stu-id="f507f-124">The IP range needs to be in the *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="f507f-125">c.</span><span class="sxs-lookup"><span data-stu-id="f507f-125">c.</span></span> <span data-ttu-id="f507f-126">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f507f-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="f507f-127">Ce que vous devez savoir</span><span class="sxs-lookup"><span data-stu-id="f507f-127">What you should know</span></span>

<span data-ttu-id="f507f-128">**Mises à jour en bloc** : lorsque vous créez ou mettez à jour des emplacements nommés, pour effectuer des mises à jour en bloc, vous pouvez charger ou télécharger un fichier CSV contenant les plages d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="f507f-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with the IP ranges.</span></span> <span data-ttu-id="f507f-129">Un téléchargement ajoute les plages d’adresses IP dans le fichier au lieu de remplacer la liste.</span><span class="sxs-lookup"><span data-stu-id="f507f-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

![Liens Charger et Télécharger](./media/active-directory-named-locations/09.png)


<span data-ttu-id="f507f-131">**Limites** : vous pouvez définir un maximum de 60 emplacements nommés avec une plage d’adresses IP assignée à chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="f507f-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned to each of them.</span></span> <span data-ttu-id="f507f-132">Si vous n’avez qu’un seul emplacement nommé configuré, vous pouvez définir jusqu’à 500 plages d’adresses IP pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f507f-132">If you have just one named location configured, you can define up to 500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f507f-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f507f-133">Next steps</span></span>

<span data-ttu-id="f507f-134">Pour en savoir plus sur les événements à risque, consultez [Événements à risque dans Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f507f-134">To learn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

