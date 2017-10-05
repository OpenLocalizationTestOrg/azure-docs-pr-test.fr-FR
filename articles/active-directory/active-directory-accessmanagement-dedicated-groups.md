---
title: "Groupes dédiés dans Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: d9decd5de6a5bafc525edc5b04c82701185088ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="a6dcb-103">Groupes dédiés dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6dcb-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="a6dcb-104">Dans Azure Active Directory (Azure AD), la fonctionnalité des groupes dédiés crée et remplit automatiquement l’appartenance aux groupes Azure AD prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-104">In Azure Active Directory (Azure AD), the dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="a6dcb-105">Les membres des groupes dédiés ne peuvent pas être ajoutés, ni supprimés via le portail Azure Classic, les applets Windows PowerShell ou via un programme.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-105">Members of dedicated groups cannot be added or removed using the Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="a6dcb-106">Les groupes dédiés nécessitent qu’une licence Azure AD Premium soit affectée à</span><span class="sxs-lookup"><span data-stu-id="a6dcb-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="a6dcb-107">l’administrateur qui gère la règle sur un groupe</span><span class="sxs-lookup"><span data-stu-id="a6dcb-107">the administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="a6dcb-108">tous les utilisateurs qui sont sélectionnés par la règle pour être membres du groupe</span><span class="sxs-lookup"><span data-stu-id="a6dcb-108">all users who are selected by the rule to be a member of the group</span></span>
>
>

<span data-ttu-id="a6dcb-109">**Pour activer les groupes dédiés**</span><span class="sxs-lookup"><span data-stu-id="a6dcb-109">**To enable dedicated groups**</span></span>

1. <span data-ttu-id="a6dcb-110">Dans le [portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-110">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a6dcb-111">Sélectionnez l’onglet **Groupes** , puis ouvrez le groupe que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-111">Select the **Groups** tab, and then open the group you want to edit.</span></span>
3. <span data-ttu-id="a6dcb-112">Sélectionnez l’onglet **Configurer**, puis définissez **Activer les groupes dédiés** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-112">Select the **Configure** tab, and then set **Enable Dedicated Groups** to **Yes**.</span></span>

<span data-ttu-id="a6dcb-113">Une fois que l’option Activer les groupes dédiés est définie sur **Oui**, vous pouvez configurer l’annuaire pour qu’il crée automatiquement le groupe dédié Tous les utilisateurs. Pour ce faire, définissez l’option **Activer le groupe Tous les utilisateurs** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-113">Once the Enable Dedicated Groups switch is set to **Yes**, you can further enable the directory to automatically create the All Users dedicated group by setting the **Enable “All Users” Group** switch to **Yes**.</span></span> <span data-ttu-id="a6dcb-114">Vous pouvez ensuite également modifier le nom de ce groupe dédié, en effectuant votre saisie dans le champ **Nom d’affichage du groupe Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-114">You can then also edit the name of this dedicated group by typing it in the **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="a6dcb-115">Le groupe Tous les utilisateurs peut vous permettre d’attribuer les mêmes autorisations à l’ensemble des utilisateurs de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-115">The All Users group can be used to assign the same permissions to all the users in your directory.</span></span> <span data-ttu-id="a6dcb-116">Par exemple, vous pouvez autoriser l’ensemble des utilisateurs de votre répertoire à accéder à l’application SaaS, en attribuant l’accès à cette application au groupe dédié Tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-116">For example, you can grant all users in your directory access to a SaaS application by assigning access for the All Users dedicated group to this application.</span></span>

<span data-ttu-id="a6dcb-117">Le groupe « Tous les utilisateurs » dédié inclut tous les utilisateurs du répertoire, dont les invités et les utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-117">The dedicated All Users group includes all users in the directory, including guests and external users.</span></span> <span data-ttu-id="a6dcb-118">Si vous avez besoin d’un groupe qui exclut les utilisateurs externes, vous pouvez créer un groupe avec une règle dynamique basée sur attribut telle que la suivante :</span><span class="sxs-lookup"><span data-stu-id="a6dcb-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as the following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="a6dcb-119">Pour un groupe qui exclut tous les invités, utilisez une règle telle que la suivante :</span><span class="sxs-lookup"><span data-stu-id="a6dcb-119">For a group that excludes all Guests, use a rule such as the following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="a6dcb-120">Pour en savoir plus sur la création de règles *avancées* (règles pouvant contenir plusieurs comparaisons) pour l’appartenance dynamique à un groupe, consultez la page [Utilisation d’attributs pour créer des règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="a6dcb-120">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="a6dcb-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6dcb-121">Next steps</span></span>
<span data-ttu-id="a6dcb-122">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6dcb-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a6dcb-123">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6dcb-123">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a6dcb-124">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6dcb-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a6dcb-125">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a6dcb-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a6dcb-126">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6dcb-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
