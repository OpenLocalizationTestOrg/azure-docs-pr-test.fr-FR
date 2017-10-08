---
title: "les étapes pour la gestion de l’accès à l’aide de groupes aaaNext | Documents Microsoft"
description: "Advanced comment-pour la gestion des groupes de sécurité et comment toouse ces ressources de groupes toomanage accès tooa."
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="31329-103">Gestion des propriétaires d’un groupe</span><span class="sxs-lookup"><span data-stu-id="31329-103">Managing owners for a group</span></span>
<span data-ttu-id="31329-104">Lorsqu’un propriétaire de la ressource a affecté le groupe AD Azure tooan accès tooa ressource, l’appartenance de hello du groupe de hello est gérée par le propriétaire du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="31329-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="31329-105">propriétaire de la ressource Hello délègue efficacement hello autorisation tooassign utilisateurs toohello toohello propriétaire de la ressource du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="31329-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31329-106">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="31329-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="31329-107">Affectation de l'appartenance de groupe</span><span class="sxs-lookup"><span data-stu-id="31329-107">Assigning group ownership</span></span>
<span data-ttu-id="31329-108">**tooadd un groupe de tooa propriétaire**</span><span class="sxs-lookup"><span data-stu-id="31329-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="31329-109">Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="31329-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="31329-110">Sélectionnez hello **groupes** onglet et un groupe puis ouvrez hello aux propriétaires de tooadd souhaitées.</span><span class="sxs-lookup"><span data-stu-id="31329-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="31329-111">Sélectionnez **Ajouter des propriétaires**.</span><span class="sxs-lookup"><span data-stu-id="31329-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="31329-112">Sur hello **d’ajouter des propriétaires** page, l’utilisateur hello select que vous souhaitez tooadd en tant que propriétaire hello de ce groupe et assurez-vous que ce nom est ajouté toohello **sélectionnés** volet.</span><span class="sxs-lookup"><span data-stu-id="31329-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="31329-113">**tooremove un propriétaire d’un groupe**</span><span class="sxs-lookup"><span data-stu-id="31329-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="31329-114">Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="31329-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="31329-115">Sélectionnez hello **groupes** onglet et puis ouvrez hello du groupe que vous souhaitez tooremove un propriétaire à partir de.</span><span class="sxs-lookup"><span data-stu-id="31329-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="31329-116">Sélectionnez hello **propriétaires** onglet.</span><span class="sxs-lookup"><span data-stu-id="31329-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="31329-117">Propriétaire hello SELECT que vous souhaitez tooremove à partir de ce groupe, puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="31329-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="31329-118">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="31329-118">Additional information</span></span>
<span data-ttu-id="31329-119">Ces articles fournissent des informations supplémentaires sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="31329-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="31329-120">La gestion des accès tooresources avec les groupes Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31329-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="31329-121">Configuration des paramètres de groupe avec les applets de commande Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31329-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="31329-122">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31329-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="31329-123">Qu’est-ce qu’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="31329-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="31329-124">Intégration des identités locales dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31329-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
