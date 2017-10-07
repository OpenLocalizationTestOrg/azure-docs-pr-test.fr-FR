---
title: 'Azure AD Connect Sync : Activer la Corbeille AD | Microsoft Docs'
description: "Cette rubrique recommande l’utilisation de hello de fonctionnalité de corbeille Active Directory avec Azure AD Connect."
services: active-directory
keywords: Corbeille AD, suppression accidentelle, ancre source
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="0fe87-104">Azure AD Connect Sync : Activer la Corbeille AD</span><span class="sxs-lookup"><span data-stu-id="0fe87-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="0fe87-105">Il est recommandé d’activer la fonctionnalité de Corbeille hello AD pour vos annuaires Active Directory local, qui sont synchronisé tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe87-105">It is recommended that you enable hello AD Recycle Bin feature for your on-premises Active Directories, which are synchronized tooAzure AD.</span></span> 

<span data-ttu-id="0fe87-106">Si vous avez supprimé par inadvertance un site local objet utilisateur AD et restauration à l’aide de la fonctionnalité de hello, Azure AD restaure objet utilisateur Azure AD correspondant de hello.</span><span class="sxs-lookup"><span data-stu-id="0fe87-106">If you accidentally deleted an on-premises AD user object and restore it using hello feature, Azure AD restores hello corresponding Azure AD user object.</span></span>  <span data-ttu-id="0fe87-107">Pour plus d’informations sur la fonctionnalité de Corbeille hello AD, consultez tooarticle [vue d’ensemble du scénario de restauration des objets Active Directory supprimés](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fe87-107">For information about hello AD Recycle Bin feature, refer tooarticle [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a><span data-ttu-id="0fe87-108">Avantages de l’activation de hello AD la Corbeille</span><span class="sxs-lookup"><span data-stu-id="0fe87-108">Benefits of enabling hello AD recycle bin</span></span>
<span data-ttu-id="0fe87-109">Cette fonctionnalité permet à la restauration des objets utilisateur Azure AD de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="0fe87-109">This feature helps with restoring Azure AD user objects by doing hello following:</span></span>

* <span data-ttu-id="0fe87-110">Si vous avez accidentellement supprimé localement l’objet utilisateur Active Directory, objet utilisateur Azure AD correspondant de hello est supprimé dans hello prochain cycle de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="0fe87-110">If you accidentally deleted an on-premises AD user object, hello corresponding Azure AD user object will be deleted in hello next sync cycle.</span></span> <span data-ttu-id="0fe87-111">Par défaut, Azure AD conserve un objet d’utilisateur Azure AD hello supprimé supprimé l’état pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="0fe87-111">By default, Azure AD keeps hello deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="0fe87-112">Si vous avez localement fonctionnalité Corbeille Active Directory est activée, vous pouvez restaurer hello supprimé localement objet utilisateur AD sans modifier sa valeur d’ancre Source.</span><span class="sxs-lookup"><span data-stu-id="0fe87-112">If you have on-premises AD Recycle Bin feature enabled, you can restore hello deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="0fe87-113">Lorsque hello récupérées localement synchronisation de l’objet utilisateur AD tooAzure AD, Azure AD permet de restaurer hello correspondant supprimé objet utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fe87-113">When hello recovered on-premises AD user object is synchronized tooAzure AD, Azure AD will restore hello corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="0fe87-114">Pour plus d’informations sur l’attribut d’ancrage de la Source, consultez tooarticle [Azure AD Connect : concepts de conception](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="0fe87-114">For information about Source Anchor attribute, refer tooarticle [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="0fe87-115">Si vous n’avez pas local AD recycler fonctionnalité Corbeille activée, vous pouvez toocreate requis AD utilisateur tooreplace hello supprimés d’objet.</span><span class="sxs-lookup"><span data-stu-id="0fe87-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required toocreate an AD user object tooreplace hello deleted object.</span></span> <span data-ttu-id="0fe87-116">Si Service de synchronisation Azure AD Connect est configuré toouse généré par le système attribut AD (par exemple, ObjectGuid) pour l’attribut d’ancre Source hello, hello objet d’utilisateur Active Directory qui vient d’être créé ne sera pas avoir hello même valeur d’ancre Source comme hello supprimé l’objet utilisateur AD.</span><span class="sxs-lookup"><span data-stu-id="0fe87-116">If Azure AD Connect Synchronization Service is configured toouse system-generated AD attribute (such as ObjectGuid) for hello Source Anchor attribute, hello newly created AD user object will not have hello same Source Anchor value as hello deleted AD user object.</span></span> <span data-ttu-id="0fe87-117">Lorsque hello nouvellement créé l’objet utilisateur Active Directory est synchronisé tooAzure AD, Azure AD crée un nouvel objet utilisateur d’Azure AD au lieu de restaurer l’objet d’utilisateur Azure AD hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="0fe87-117">When hello newly created AD user object is synchronized tooAzure AD, Azure AD creates a new Azure AD user object instead of restoring hello soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe87-118">Par défaut, AD Azure conserve les objets d’utilisateur Azure AD dans un état supprimé temporairement pendant 30 jours avant suppression définitive.</span><span class="sxs-lookup"><span data-stu-id="0fe87-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="0fe87-119">Toutefois, les administrateurs peuvent accélérer la suppression de ces objets hello.</span><span class="sxs-lookup"><span data-stu-id="0fe87-119">However, administrators can accelerate hello deletion of such objects.</span></span> <span data-ttu-id="0fe87-120">Une fois que les objets hello sont définitivement supprimés, ils ne peuvent plus être restaurées, même si locaux Corbeille Active Directory est activée.</span><span class="sxs-lookup"><span data-stu-id="0fe87-120">Once hello objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0fe87-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0fe87-121">Next steps</span></span>
<span data-ttu-id="0fe87-122">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="0fe87-122">**Overview topics**</span></span>

* [<span data-ttu-id="0fe87-123">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="0fe87-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="0fe87-124">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fe87-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
