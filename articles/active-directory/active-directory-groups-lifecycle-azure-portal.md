---
title: "aaaPreview Office 365 regroupe d’expiration dans Azure Active Directory | Documents Microsoft"
description: "Façon dont les groupes tooset d’expiration pour Office 365 dans Azure Active Directory (version préliminaire)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="945db-103">Configurer l’expiration des groupes Office 365 (préversion)</span><span class="sxs-lookup"><span data-stu-id="945db-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="945db-104">Vous pouvez désormais gérer hello du cycle de vie des groupes Office 365 en définissant la date d’expiration pour les groupes Office 365 que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="945db-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="945db-105">Une fois cette expiration est définie, les propriétaires de ces groupes sont demandé toorenew leurs groupes s’ils doivent toujours les groupes hello.</span><span class="sxs-lookup"><span data-stu-id="945db-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="945db-106">Les groupes Office 365 qui ne sont pas renouvelés seront supprimés.</span><span class="sxs-lookup"><span data-stu-id="945db-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="945db-107">N’importe quel groupe Office 365 qui a été supprimé peut être restauré dans les 30 jours par les propriétaires de groupe hello ou un administrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="945db-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="945db-108">Vous pouvez définir l’expiration pour les groupes Office 365 uniquement.</span><span class="sxs-lookup"><span data-stu-id="945db-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="945db-109">La définition de l’expiration pour les groupes O365 nécessite qu’une licence Azure AD Premium soit affectée à</span><span class="sxs-lookup"><span data-stu-id="945db-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="945db-110">administrateur de Hello qui configure les paramètres d’expiration de hello pour le client de hello</span><span class="sxs-lookup"><span data-stu-id="945db-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="945db-111">Tous les membres de groupes hello sélectionnés pour ce paramètre</span><span class="sxs-lookup"><span data-stu-id="945db-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="945db-112">Définir l’expiration des groupes Office 365</span><span class="sxs-lookup"><span data-stu-id="945db-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="945db-113">Ouvrez hello [centre d’administration Azure AD](https://aad.portal.azure.com) avec un compte qui est un administrateur global dans votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="945db-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="945db-114">Ouvrez Azure AD et sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="945db-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="945db-115">Sélectionnez **paramètres de groupe** , puis sélectionnez **Expiration** paramètres d’expiration de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="945db-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Panneau Expiration](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="945db-117">Sur hello **Expiration** panneau, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="945db-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="945db-118">Définir la durée de vie de groupe hello en jours.</span><span class="sxs-lookup"><span data-stu-id="945db-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="945db-119">Vous pouvez sélectionner un des hello prédéfinie de valeurs ou une valeur personnalisée (doit être 31 jours ou plus).</span><span class="sxs-lookup"><span data-stu-id="945db-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="945db-120">Spécifiez une adresse de messagerie dans lequel les notifications d’expiration et le renouvellement hello entraînant l’envoi d’un groupe n’a aucun propriétaire.</span><span class="sxs-lookup"><span data-stu-id="945db-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="945db-121">Sélectionnez les groupes Office 365 qui expirent.</span><span class="sxs-lookup"><span data-stu-id="945db-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="945db-122">Vous pouvez activer l’expiration pour **tous les** les groupes Office 365, vous pouvez sélectionner parmi les groupes hello Office 365, ou que vous sélectionnez **aucun** pour désactiver la date d’expiration pour tous les groupes.</span><span class="sxs-lookup"><span data-stu-id="945db-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="945db-123">Enregistrer vos paramètres lorsque vous avez terminé en sélectionnant **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="945db-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="945db-124">Pour obtenir des instructions sur la façon dont toodownload et installez hello d’expiration tooconfigure de module PowerShell de Microsoft pour les groupes Office 365 via PowerShell, consultez [Module Azure Active Directory V2 PowerShell - version préliminaire publique 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="945db-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="945db-125">Les notifications par courrier électronique similaires sont envoyées à 30 jours, 15 jours, les propriétaires de groupe toohello Office 365 et tooexpiration préalable de 1 jour du groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="945db-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Notification par e-mail de l’expiration](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="945db-127">propriétaire du groupe Hello peut ensuite sélectionner **renouveler groupe** toorenew hello groupe Office 365, ou pouvez sélectionner **accédez toogroup** membres de hello toosee et d’autres détails sur hello groupe.</span><span class="sxs-lookup"><span data-stu-id="945db-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="945db-128">Lors de l’expiration d’un groupe, groupe de hello est supprimé d’un jour après la date d’expiration de hello.</span><span class="sxs-lookup"><span data-stu-id="945db-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="945db-129">Une notification par courrier électronique, tels que celui-ci est envoyée de propriétaires du groupe toohello Office 365 pour l’informer sur d’expiration de hello ultérieure la suppression et de leur groupe Office 365.</span><span class="sxs-lookup"><span data-stu-id="945db-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Notification par e-mail de la suppression du groupe](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="945db-131">groupe de Hello peut être restaurée en sélectionnant **groupe restauration** ou à l’aide des applets de commande PowerShell, comme décrit dans [groupe restauration un supprimé Office 365 dans Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="945db-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="945db-132">Si le groupe hello que vous restaurez contient des documents, les sites SharePoint ou autres objets persistants, elle peut prendre le groupe hello restauration too24 heures toofully et son contenu.</span><span class="sxs-lookup"><span data-stu-id="945db-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="945db-133">Lorsque vous déployez des paramètres d’expiration de hello, il peut y avoir certains groupes qui sont antérieurs à la fenêtre d’expiration hello.</span><span class="sxs-lookup"><span data-stu-id="945db-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="945db-134">Ces groupes ne sont pas supprimées immédiatement, mais sont de définir les jours too30 avant l’expiration.</span><span class="sxs-lookup"><span data-stu-id="945db-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="945db-135">Hello premier renouvellement notification par courrier électronique est envoyée au sein d’un jour.</span><span class="sxs-lookup"><span data-stu-id="945db-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="945db-136">Par exemple, le groupe A a été créé 400 jours, et que l’intervalle d’expiration hello est défini too180 jours.</span><span class="sxs-lookup"><span data-stu-id="945db-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="945db-137">Lorsque vous appliquez les paramètres d’expiration, le groupe A a 30 jours avant d’être supprimé, sauf si le propriétaire de hello renouvelle celui-ci.</span><span class="sxs-lookup"><span data-stu-id="945db-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="945db-138">Lorsqu’un groupe dynamique est supprimé et restauré, il est considéré comme un nouveau groupe et le nouveau remplis règle toohello correspondants.</span><span class="sxs-lookup"><span data-stu-id="945db-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="945db-139">Ce processus peut prendre des heures de too24.</span><span class="sxs-lookup"><span data-stu-id="945db-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="945db-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="945db-140">Next steps</span></span>
<span data-ttu-id="945db-141">Ces articles fournissent des informations supplémentaires sur les groupes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="945db-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="945db-142">Consulter les groupes existants</span><span class="sxs-lookup"><span data-stu-id="945db-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="945db-143">Gérer les paramètres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="945db-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="945db-144">Gérer les membres d’un groupe</span><span class="sxs-lookup"><span data-stu-id="945db-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="945db-145">Gérer l’appartenance à un groupe</span><span class="sxs-lookup"><span data-stu-id="945db-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="945db-146">Gérer les règles dynamiques pour les utilisateurs dans un groupe</span><span class="sxs-lookup"><span data-stu-id="945db-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
