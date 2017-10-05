---
title: 'Azure AD Connect Sync : Activer la Corbeille AD | Microsoft Docs'
description: "Cette rubrique recommande l’utilisation de la fonctionnalité Corbeille d’AD avec Azure AD Connect."
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
ms.openlocfilehash: eb455477547f3db8245cf3601576eba9c6fdc56f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a><span data-ttu-id="c35cd-104">Azure AD Connect Sync : Activer la Corbeille AD</span><span class="sxs-lookup"><span data-stu-id="c35cd-104">Azure AD Connect sync: Enable AD recycle bin</span></span>
<span data-ttu-id="c35cd-105">Il est recommandé d’activer la fonctionnalité Corbeille d’AD pour vos annuaires Active Directory locaux, qui sont synchronisés avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c35cd-105">It is recommended that you enable the AD Recycle Bin feature for your on-premises Active Directories, which are synchronized to Azure AD.</span></span> 

<span data-ttu-id="c35cd-106">Si vous avez supprimé accidentellement un objet utilisateur AD local et le restaurez à l’aide de cette fonctionnalité, Azure AD restaure l’objet utilisateur Azure AD correspondant.</span><span class="sxs-lookup"><span data-stu-id="c35cd-106">If you accidentally deleted an on-premises AD user object and restore it using the feature, Azure AD restores the corresponding Azure AD user object.</span></span>  <span data-ttu-id="c35cd-107">Pour plus d’informations sur la fonctionnalité Corbeille d’AD, reportez-vous à l’article [Présentation du scénario pour la restauration d’objets Active Directory supprimés](https://technet.microsoft.com/library/dd379542.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35cd-107">For information about the AD Recycle Bin feature, refer to article [Scenario Overview for Restoring Deleted Active Directory Objects](https://technet.microsoft.com/library/dd379542.aspx).</span></span>

## <a name="benefits-of-enabling-the-ad-recycle-bin"></a><span data-ttu-id="c35cd-108">Avantages de l’activation de la Corbeille d’AD</span><span class="sxs-lookup"><span data-stu-id="c35cd-108">Benefits of enabling the AD recycle bin</span></span>
<span data-ttu-id="c35cd-109">Cette fonctionnalité vous aide à restaurer des objets utilisateur Azure AD en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="c35cd-109">This feature helps with restoring Azure AD user objects by doing the following:</span></span>

* <span data-ttu-id="c35cd-110">Si vous avez supprimé accidentellement un objet utilisateur AD local, l’objet utilisateur Azure AD correspondant sera supprimé lors du prochain cycle de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="c35cd-110">If you accidentally deleted an on-premises AD user object, the corresponding Azure AD user object will be deleted in the next sync cycle.</span></span> <span data-ttu-id="c35cd-111">Par défaut, Azure AD conserve les objets utilisateur Azure AD supprimés en état de suppression temporaire pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="c35cd-111">By default, Azure AD keeps the deleted Azure AD user object in soft-deleted state for 30 days.</span></span>

* <span data-ttu-id="c35cd-112">Si vous avez activé la fonctionnalité Corbeille d’AD locale, vous pouvez restaurer l’objet utilisateur supprimé localement sans modifier sa valeur d’ancre source.</span><span class="sxs-lookup"><span data-stu-id="c35cd-112">If you have on-premises AD Recycle Bin feature enabled, you can restore the deleted on-premises AD user object without changing its Source Anchor value.</span></span> <span data-ttu-id="c35cd-113">Lorsque l’objet utilisateur AD local récupéré est synchronisé avec Azure AD, Azure AD est restaure l’objet utilisateur Azure AD supprimé temporairement correspondant.</span><span class="sxs-lookup"><span data-stu-id="c35cd-113">When the recovered on-premises AD user object is synchronized to Azure AD, Azure AD will restore the corresponding soft-deleted Azure AD user object.</span></span> <span data-ttu-id="c35cd-114">Pour plus d’informations sur l’attribut d’ancre source, reportez-vous à l’article [Azure Connect AD : Principes de conception](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span><span class="sxs-lookup"><span data-stu-id="c35cd-114">For information about Source Anchor attribute, refer to article [Azure AD Connect: Design concepts](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).</span></span>

* <span data-ttu-id="c35cd-115">Si vous n’avez pas activé la fonctionnalité Corbeille d’AD locale, vous pourriez avoir à créer un objet d’utilisateur AD pour remplacer l’objet supprimé.</span><span class="sxs-lookup"><span data-stu-id="c35cd-115">If you do not have on-premises AD Recycle Bin feature enabled, you may be required to create an AD user object to replace the deleted object.</span></span> <span data-ttu-id="c35cd-116">Si le service de synchronisation Azure AD Connect est configuré pour utiliser un attribut AD généré par le système (comme ObjectGuid) comme attribut d’ancre source, l’objet utilisateur AD nouvellement créé n’aura pas la même valeur d’ancre source que l’objet utilisateur AD supprimé.</span><span class="sxs-lookup"><span data-stu-id="c35cd-116">If Azure AD Connect Synchronization Service is configured to use system-generated AD attribute (such as ObjectGuid) for the Source Anchor attribute, the newly created AD user object will not have the same Source Anchor value as the deleted AD user object.</span></span> <span data-ttu-id="c35cd-117">Lorsque l’objet utilisateur AD nouvellement créé est synchronisé avec Azure AD, Azure AD crée un nouvel objet d’utilisateur Azure AD au lieu de restaurer l’objet utilisateur Azure AD supprimé temporairement.</span><span class="sxs-lookup"><span data-stu-id="c35cd-117">When the newly created AD user object is synchronized to Azure AD, Azure AD creates a new Azure AD user object instead of restoring the soft-deleted Azure AD user object.</span></span>

> [!NOTE]
> <span data-ttu-id="c35cd-118">Par défaut, AD Azure conserve les objets d’utilisateur Azure AD dans un état supprimé temporairement pendant 30 jours avant suppression définitive.</span><span class="sxs-lookup"><span data-stu-id="c35cd-118">By default, Azure AD keeps deleted Azure AD user objects in soft-deleted state for 30 days before they are permanently deleted.</span></span> <span data-ttu-id="c35cd-119">Toutefois, les administrateurs peuvent accélérer la suppression de ces objets.</span><span class="sxs-lookup"><span data-stu-id="c35cd-119">However, administrators can accelerate the deletion of such objects.</span></span> <span data-ttu-id="c35cd-120">Une fois que les objets sont définitivement supprimés, ils ne peuvent plus être restaurés, même si la fonctionnalité Corbeille AD locale est activée.</span><span class="sxs-lookup"><span data-stu-id="c35cd-120">Once the objects are permanently deleted, they can no longer be recovered, even if on-premises AD Recycle Bin feature is enabled.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c35cd-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c35cd-121">Next steps</span></span>
<span data-ttu-id="c35cd-122">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="c35cd-122">**Overview topics**</span></span>

* [<span data-ttu-id="c35cd-123">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="c35cd-123">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="c35cd-124">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c35cd-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
