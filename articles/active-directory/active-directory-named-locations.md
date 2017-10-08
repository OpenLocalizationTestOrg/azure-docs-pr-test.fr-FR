---
title: emplacements aaaNamed dans Azure Active Directory | Documents Microsoft
description: "En configurant les emplacements nommés, vous pouvez éviter d’avoir des IP adresses qui sont détenus par votre organisation générant des faux positifs pour les emplacements de tooatypical hello voyage Impossible du type d’événement risque."
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
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a><span data-ttu-id="03cd9-103">Emplacements nommés dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03cd9-103">Named locations in Azure Active Directory</span></span>

<span data-ttu-id="03cd9-104">Avec hello nommé fonctionnalité emplacements d’Azure Active Directory, vous pouvez étiqueter des plages d’adresses IP approuvées dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="03cd9-104">With hello named locations feature of Azure Active Directory, you can label trusted IP address ranges in your organizations.</span></span> <span data-ttu-id="03cd9-105">Dans votre environnement, vous pouvez utiliser les emplacements nommés dans le contexte de hello de détection hello de [risque d’événements](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="03cd9-105">In your environment, you can use named locations in hello context of hello detection of [risk events](active-directory-reporting-risk-events.md).</span></span> <span data-ttu-id="03cd9-106">fonctionnalité de Hello contribue à réduire hello de fausses signalés pour hello *emplacements de voyage Impossible tooatypical* risque de type d’événement.</span><span class="sxs-lookup"><span data-stu-id="03cd9-106">hello feature helps reduce hello number of reported false positives for hello *Impossible travel tooatypical locations* risk event type.</span></span> 

## <a name="configuration"></a><span data-ttu-id="03cd9-107">Configuration</span><span class="sxs-lookup"><span data-stu-id="03cd9-107">Configuration</span></span>

<span data-ttu-id="03cd9-108">tooconfigure un emplacement nommé :</span><span class="sxs-lookup"><span data-stu-id="03cd9-108">tooconfigure a named location:</span></span>

1. <span data-ttu-id="03cd9-109">Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur global.</span><span class="sxs-lookup"><span data-stu-id="03cd9-109">Sign in toohello [Azure portal](https://portal.azure.com) as global administrator.</span></span>

2. <span data-ttu-id="03cd9-110">Dans le volet gauche de hello, cliquez sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="03cd9-110">In hello left pane, click **Azure Active Directory**.</span></span>

    ![lien d’Azure Active Directory Hello dans le volet gauche de hello](./media/active-directory-named-locations/01.png)

3. <span data-ttu-id="03cd9-112">Sur hello **Azure Active Directory** panneau, Bonjour **sécurité** , cliquez sur **accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="03cd9-112">On hello **Azure Active Directory** blade, in hello **Security** section, click **Conditional access**.</span></span>

    ![Hello, la commande d’accès conditionnel](./media/active-directory-named-locations/05.png)


4. <span data-ttu-id="03cd9-114">Sur hello **accès conditionnel** panneau, Bonjour **gérer** , cliquez sur **emplacements nommés**.</span><span class="sxs-lookup"><span data-stu-id="03cd9-114">On hello **Conditional Access** blade, in hello **Manage** section, click **Named locations**.</span></span>

    ![Hello nommé emplacements commande](./media/active-directory-named-locations/06.png)


5. <span data-ttu-id="03cd9-116">Sur hello **emplacements nommés** panneau, cliquez sur **nouvel emplacement**.</span><span class="sxs-lookup"><span data-stu-id="03cd9-116">On hello **Named locations** blade, click **New location**.</span></span>

    ![Hello nouvelle commande de l’emplacement](./media/active-directory-named-locations/07.png)


6. <span data-ttu-id="03cd9-118">Sur hello **nouveau** panneau, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="03cd9-118">On hello **New** blade, do hello following:</span></span>

    ![Nouveau panneau de Hello](./media/active-directory-named-locations/08.png)

    <span data-ttu-id="03cd9-120">a.</span><span class="sxs-lookup"><span data-stu-id="03cd9-120">a.</span></span> <span data-ttu-id="03cd9-121">Bonjour **nom** , tapez un nom pour votre emplacement nommé.</span><span class="sxs-lookup"><span data-stu-id="03cd9-121">In hello **Name** box, type a name for your named location.</span></span>

    <span data-ttu-id="03cd9-122">b.</span><span class="sxs-lookup"><span data-stu-id="03cd9-122">b.</span></span> <span data-ttu-id="03cd9-123">Bonjour **plages IP** , tapez une plage IP.</span><span class="sxs-lookup"><span data-stu-id="03cd9-123">In hello **IP ranges** box, type an IP range.</span></span> <span data-ttu-id="03cd9-124">plage d’adresses IP Hello doit toobe Bonjour *inter-Domain Routing* format (CIDR).</span><span class="sxs-lookup"><span data-stu-id="03cd9-124">hello IP range needs toobe in hello *Classless Inter-Domain Routing* (CIDR) format.</span></span>  

    <span data-ttu-id="03cd9-125">c.</span><span class="sxs-lookup"><span data-stu-id="03cd9-125">c.</span></span> <span data-ttu-id="03cd9-126">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="03cd9-126">Click **Create**.</span></span>



## <a name="what-you-should-know"></a><span data-ttu-id="03cd9-127">Ce que vous devez savoir</span><span class="sxs-lookup"><span data-stu-id="03cd9-127">What you should know</span></span>

<span data-ttu-id="03cd9-128">**Les mises à jour en bloc de**: lorsque vous créez ou mettez à jour les emplacements nommés, pour les mises à jour en bloc, vous pouvez télécharger ou télécharger un fichier CSV avec des plages IP hello.</span><span class="sxs-lookup"><span data-stu-id="03cd9-128">**Bulk updates**: When you create or update named locations, for bulk updates, you can upload or download a CSV file with hello IP ranges.</span></span> <span data-ttu-id="03cd9-129">Un téléchargement ajoute des plages d’adresses IP hello dans la liste toohello des fichiers hello au lieu de remplacer la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="03cd9-129">An upload adds hello IP ranges in hello file toohello list instead of overwriting hello list.</span></span>

![Hello télécharger des liens](./media/active-directory-named-locations/09.png)


<span data-ttu-id="03cd9-131">**Limitations**: vous pouvez définir un maximum de 60 emplacements nommés, avec un tooeach de plage affectée IP d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="03cd9-131">**Limitations**: You can define a maximum of 60 named locations, with one IP range assigned tooeach of them.</span></span> <span data-ttu-id="03cd9-132">Si vous avez qu’un seul emplacement nommé configuré, vous pouvez définir des plages d’adresses IP too500 pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="03cd9-132">If you have just one named location configured, you can define up too500 IP ranges for it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="03cd9-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03cd9-133">Next steps</span></span>

<span data-ttu-id="03cd9-134">toolearn en savoir plus sur les événements à risque, consultez [événements à risque Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="03cd9-134">toolearn more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>

