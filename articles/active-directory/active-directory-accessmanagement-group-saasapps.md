---
title: "Utilisation d’un groupe pour gérer l’accès aux applications SaaS| Microsoft Docs"
description: "Comment utiliser les groupes dans Azure Active Directory Premium ou Basic pour attribuer l’accès à des applications SaaS intégrées à Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a><span data-ttu-id="0d0c0-103">Utilisation d’un groupe pour gérer l’accès aux applications SaaS</span><span class="sxs-lookup"><span data-stu-id="0d0c0-103">Using a group to manage access to SaaS applications</span></span>
<span data-ttu-id="0d0c0-104">En utilisant Azure Active Directory (Azure AD) avec une licence Azure AD Premium ou Azure AD Basic, vous pouvez utiliser les groupes pour attribuer l’accès à une application SaaS intégrée à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="0d0c0-105">Par exemple, si vous souhaitez attribuer l’accès à différentes applications SaaS au service marketing, vous pouvez créer un groupe comportant les utilisateurs du service marketing, puis allouer ce groupe aux cinq applications SaaS dont il a besoin.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-105">For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department.</span></span> <span data-ttu-id="0d0c0-106">De cette manière, vous pouvez gagner du temps en gérant de manière centralisée l’adhésion du service marketing.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-106">This way you can save time by managing the membership of the marketing department in one place.</span></span> <span data-ttu-id="0d0c0-107">Ensuite, les utilisateurs sont affectés à l’application lorsqu’ils sont ajoutés en tant que membres du groupe marketing. Leurs attributions sont retirées de l’application lors de leur suppression du groupe marketing.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-107">Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d0c0-108">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="0d0c0-109">Cette fonctionnalité peut être utilisée avec des centaines d’applications pouvant être ajoutées à partir de la galerie d’applications Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-109">This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.</span></span>

<span data-ttu-id="0d0c0-110">**Pour attribuer à un groupe l’accès à une application SaaS**</span><span class="sxs-lookup"><span data-stu-id="0d0c0-110">**To assign access for a group to a SaaS application**</span></span>

1. <span data-ttu-id="0d0c0-111">Dans le [portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory** dans la barre de navigation à gauche.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-111">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on the navigation bar on the left hand side.</span></span>
2. <span data-ttu-id="0d0c0-112">Sélectionnez l’onglet **Répertoire** , puis ouvrez le répertoire dans lequel vous souhaitez attribuer l’accès à un groupe à une application SaaS.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-112">Select the **Directory** tab, and then open the directory in which you want to assign access for a group to a SaaS application.</span></span>
3. <span data-ttu-id="0d0c0-113">Sélectionnez l’onglet **Applications** . Sélectionnez une application ajoutée à partir de la galerie d’applications, puis cliquez sur l’onglet **Utilisateurs et groupes** .</span><span class="sxs-lookup"><span data-stu-id="0d0c0-113">Select the **Applications** tab. Select an application that you added from the Application Gallery, and then click  the **Users and Groups** tab.</span></span>
4. <span data-ttu-id="0d0c0-114">Sous l’onglet **Utilisateurs et groupes**, dans le champ **Commencer par**, saisissez le nom du groupe auquel vous souhaitez attribuer l’accès, puis cliquez sur la coche dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-114">On the **Users and Groups** tab, in the **Starting with** field, enter the name of the group to which you want to assign access, and then select the check mark in the upper right.</span></span> <span data-ttu-id="0d0c0-115">Il vous suffit de saisir le début du nom d’un groupe.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-115">You only need to type the first part of a group's name.</span></span>
5. <span data-ttu-id="0d0c0-116">Sélectionnez le groupe, puis cliquez sur le bouton **Autoriser l’accès** .</span><span class="sxs-lookup"><span data-stu-id="0d0c0-116">Select the group, then then select the **Assign Access** button.</span></span> <span data-ttu-id="0d0c0-117">Sélectionnez **Oui** lorsque vous voyez le message de confirmation.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-117">Select **Yes** when you see the confirmation message.</span></span> <span data-ttu-id="0d0c0-118">Les appartenances à des groupes imbriquées ne sont pas prises en charge pour l’affectation basée sur le groupe à des applications à ce stade.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-118">Nested group memberships are not supported for group-based assignment to applications at this time.</span></span>
6. <span data-ttu-id="0d0c0-119">Vous pouvez également voir quels utilisateurs sont affectés à l’application, soit directement ou en étudiant l’adhésion au sein d’un groupe.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-119">You can also see which users are assigned to the application, either directly or by membership in a group.</span></span> <span data-ttu-id="0d0c0-120">Pour ce faire, modifiez la définition de la **liste déroulante Affichage de Groupe** sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-120">To do this, change the **Show dropdown from 'Groups'** to **'All Users'**.</span></span> <span data-ttu-id="0d0c0-121">La liste affiche les utilisateurs du répertoire et indique s’ils sont affectés ou non à l’application.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-121">The list shows users in the directory and whether or not each user is assigned to the application.</span></span> <span data-ttu-id="0d0c0-122">Elle indique également si les utilisateurs sont affectés directement à l’application (type d’affectation direct) ou par le biais de l’adhésion à un groupe (type d’affectation hérité).</span><span class="sxs-lookup"><span data-stu-id="0d0c0-122">The list also shows whether the assigned users are assigned to the application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="0d0c0-123">L’onglet Utilisateurs et groupes ne s’affiche qu’une fois que vous avez activé Azure AD Premium ou Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-123">You can see the Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="0d0c0-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d0c0-124">Next steps</span></span>
<span data-ttu-id="0d0c0-125">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0d0c0-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0d0c0-126">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0c0-126">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="0d0c0-127">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0c0-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="0d0c0-128">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0c0-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="0d0c0-129">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0d0c0-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="0d0c0-130">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0c0-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
