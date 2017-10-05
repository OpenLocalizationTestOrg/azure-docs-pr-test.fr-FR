---
title: "Étapes suivantes de la gestion des accès à l’aide de groupes | Microsoft Docs"
description: "Procédures avancées concernant la gestion des groupes de sécurité et l’utilisation de ces groupes pour gérer l’accès à une ressource."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="96e4f-103">Gestion des propriétaires d’un groupe</span><span class="sxs-lookup"><span data-stu-id="96e4f-103">Managing owners for a group</span></span>
<span data-ttu-id="96e4f-104">Une fois que le propriétaire d'une ressource a attribué l'accès à une ressource à un groupe Azure AD, l'appartenance au groupe est gérée par le propriétaire du groupe.</span><span class="sxs-lookup"><span data-stu-id="96e4f-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="96e4f-105">Le propriétaire de la ressource délègue effectivement au propriétaire du groupe l’autorisation d’affecter des utilisateurs aux ressources.</span><span class="sxs-lookup"><span data-stu-id="96e4f-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96e4f-106">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="96e4f-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="96e4f-107">Affectation de l'appartenance de groupe</span><span class="sxs-lookup"><span data-stu-id="96e4f-107">Assigning group ownership</span></span>
<span data-ttu-id="96e4f-108">**Pour ajouter un propriétaire à un groupe**</span><span class="sxs-lookup"><span data-stu-id="96e4f-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="96e4f-109">Dans le [portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="96e4f-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="96e4f-110">Sélectionnez l’onglet **Groupes** , puis ouvrez le groupe auquel vous souhaitez ajouter des propriétaires.</span><span class="sxs-lookup"><span data-stu-id="96e4f-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="96e4f-111">Sélectionnez **Ajouter des propriétaires**.</span><span class="sxs-lookup"><span data-stu-id="96e4f-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="96e4f-112">Sur la page **Ajouter des propriétaires**, sélectionnez l’utilisateur à ajouter en tant que propriétaire de ce groupe, puis vérifiez que son nom a été ajouté au volet **Sélectionné**.</span><span class="sxs-lookup"><span data-stu-id="96e4f-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="96e4f-113">**Pour supprimer un propriétaire d'un groupe**</span><span class="sxs-lookup"><span data-stu-id="96e4f-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="96e4f-114">Dans le [portail Azure Classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="96e4f-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="96e4f-115">Sélectionnez l’onglet **Groupes** , puis ouvrez le groupe duquel vous souhaitez supprimer un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="96e4f-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="96e4f-116">Sélectionnez l’onglet **Propriétaires** .</span><span class="sxs-lookup"><span data-stu-id="96e4f-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="96e4f-117">Sélectionnez le propriétaire que vous souhaitez supprimer de ce groupe, puis choisissez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="96e4f-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="96e4f-118">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="96e4f-118">Additional information</span></span>
<span data-ttu-id="96e4f-119">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96e4f-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="96e4f-120">Gestion de l’accès aux ressources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96e4f-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="96e4f-121">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96e4f-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="96e4f-122">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96e4f-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="96e4f-123">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="96e4f-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="96e4f-124">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96e4f-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
