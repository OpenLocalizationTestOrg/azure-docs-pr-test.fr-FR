---
title: groupes aaaDedicated dans Azure Active Directory | Documents Microsoft
description: "Vue d’ensemble du fonctionnement et de la création des groupes dédiés dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="57c25-103">Groupes dédiés dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57c25-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="57c25-104">Dans Azure Active Directory (Azure AD), fonctionnalité de groupes dédiés hello crée et remplit l’appartenance des groupes Azure Active Directory prédéfini automatiquement.</span><span class="sxs-lookup"><span data-stu-id="57c25-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="57c25-105">Les membres des groupes dédiés ne peut pas être ajoutés ou supprimé à l’aide de hello Azure classic portail, les cmdlets Windows PowerShell, ou par programme.</span><span class="sxs-lookup"><span data-stu-id="57c25-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="57c25-106">Les groupes dédiés nécessitent qu’une licence Azure AD Premium soit affectée à</span><span class="sxs-lookup"><span data-stu-id="57c25-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="57c25-107">administrateur Hello qui gère la règle hello sur un groupe</span><span class="sxs-lookup"><span data-stu-id="57c25-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="57c25-108">tous les utilisateurs qui sont sélectionnées par hello règle toobe un membre du groupe de hello</span><span class="sxs-lookup"><span data-stu-id="57c25-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="57c25-109">**groupes de tooenable dédié**</span><span class="sxs-lookup"><span data-stu-id="57c25-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="57c25-110">Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="57c25-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="57c25-111">Sélectionnez hello **groupes** onglet et groupe hello puis ouvrez tooedit.</span><span class="sxs-lookup"><span data-stu-id="57c25-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="57c25-112">Sélectionnez hello **configurer** onglet, puis définissez **activer les groupes dédiés** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="57c25-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="57c25-113">Une fois que hello activer les groupes dédiés commutateur est défini trop**Oui**, vous pouvez activer davantage hello Active tooautomatically créer groupe dédié de tous les utilisateurs de hello en hello de définition **activer « Tous les utilisateurs » groupe** basculer trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="57c25-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="57c25-114">Vous pouvez modifier puis également nom hello de ce groupe dédié en le tapant dans hello **nom d’affichage pour « Tous les utilisateurs » groupe** champ.</span><span class="sxs-lookup"><span data-stu-id="57c25-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="57c25-115">groupe de tous les utilisateurs Hello peut être utilisé tooassign hello aux mêmes autorisations tooall hello utilisateurs dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="57c25-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="57c25-116">Par exemple, vous pouvez accorder tous les utilisateurs dans votre tooa d’accès de répertoire application SaaS en attribuant l’accès pour hello tous les utilisateurs groupe dédié toothis application.</span><span class="sxs-lookup"><span data-stu-id="57c25-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="57c25-117">groupe de tous les utilisateurs Hello dédié inclut tous les utilisateurs dans le répertoire hello, y compris les invités et les utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="57c25-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="57c25-118">Si vous avez besoin d’un groupe qui exclut les utilisateurs externes, puis procéder à la création d’un groupe avec une règle dynamique basée sur les attributs tels que les suivants hello :</span><span class="sxs-lookup"><span data-stu-id="57c25-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="57c25-119">Pour un groupe qui exclut tous les invités, utilisez une règle, tels que les suivants hello :</span><span class="sxs-lookup"><span data-stu-id="57c25-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="57c25-120">toolearn comment toocreate *avancées* règles (qui peut contenir plusieurs comparaisons) pour l’appartenance au groupe dynamique, consultez [à l’aide des attributs toocreate des règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="57c25-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="57c25-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57c25-121">Next steps</span></span>
<span data-ttu-id="57c25-122">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57c25-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="57c25-123">La gestion des accès tooresources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57c25-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="57c25-124">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57c25-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="57c25-125">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="57c25-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="57c25-126">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57c25-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
