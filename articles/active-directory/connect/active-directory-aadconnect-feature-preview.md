---
title: "Azure AD Connect : fonctionnalités de la version préliminaire | Microsoft Docs"
description: "Cette rubrique décrit en détail les fonctionnalités disponibles en version préliminaire dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="0bc28-103">Plus de détails sur les fonctionnalités de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="0bc28-103">More details about features in preview</span></span>
<span data-ttu-id="0bc28-104">Cette rubrique décrit comment toouse fonctionnalités actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="0bc28-104">This topic describes how toouse features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="0bc28-105">Écriture différée de groupe</span><span class="sxs-lookup"><span data-stu-id="0bc28-105">Group writeback</span></span>
<span data-ttu-id="0bc28-106">option Hello pour l’écriture différée de groupe dans des fonctionnalités facultatives vous permet de toowriteback **les groupes Office 365** forêt tooa avec Exchange est installé.</span><span class="sxs-lookup"><span data-stu-id="0bc28-106">hello option for group writeback in optional features allows you toowriteback **Office 365 Groups** tooa forest with Exchange installed.</span></span> <span data-ttu-id="0bc28-107">Il s’agit d’un groupe qui est toujours masterisé dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="0bc28-107">This is a group that is always mastered in hello cloud.</span></span> <span data-ttu-id="0bc28-108">Si vous avez Exchange sur site, puis vous pouvez écrire dans ces groupes tooon locaux pour les utilisateurs disposant d’une boîte aux lettres Exchange de local peuvent envoyer et recevoir des courriers électroniques à partir de ces groupes.</span><span class="sxs-lookup"><span data-stu-id="0bc28-108">If you have Exchange on-premises, then you can write back these groups tooon-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="0bc28-109">Plus d’informations sur les groupes Office 365 et comment toouse les trouverez [ici](http://aka.ms/O365g).</span><span class="sxs-lookup"><span data-stu-id="0bc28-109">More information about Office 365 Groups and how toouse them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="0bc28-110">Un groupe Office 365 est représenté comme un groupe de distribution dans les versions locales d’AD DS.</span><span class="sxs-lookup"><span data-stu-id="0bc28-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="0bc28-111">Votre Exchange server sur site doit être sur Exchange 2013 mise à jour cumulative 8 (publiée en mars 2015) ou Exchange 2016 toorecognize ce nouveau type de groupe.</span><span class="sxs-lookup"><span data-stu-id="0bc28-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 toorecognize this new group type.</span></span>

<span data-ttu-id="0bc28-112">**Notes de version préliminaire hello**</span><span class="sxs-lookup"><span data-stu-id="0bc28-112">**Notes during hello preview**</span></span>

* <span data-ttu-id="0bc28-113">attribut de carnet d’adresses Hello n’est actuellement pas remplie dans l’aperçu de hello.</span><span class="sxs-lookup"><span data-stu-id="0bc28-113">hello address book attribute is currently not populated in hello preview.</span></span> <span data-ttu-id="0bc28-114">Sans cet attribut, groupe de hello n’est pas visible dans la liste d’adresses globale de hello.</span><span class="sxs-lookup"><span data-stu-id="0bc28-114">Without this attribute, hello group is not visible in hello GAL.</span></span> <span data-ttu-id="0bc28-115">Hello toopopulate de façon plus simple cet attribut est l’applet de commande PowerShell Exchange toouse hello `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="0bc28-115">hello easiest way toopopulate this attribute is toouse hello Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="0bc28-116">Seules les forêts avec schéma de Exchange hello sont des cibles valides pour les groupes.</span><span class="sxs-lookup"><span data-stu-id="0bc28-116">Only forests with hello Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="0bc28-117">Si aucun Exchange a été détecté, l’écriture différée de groupe n’est pas possible tooenable.</span><span class="sxs-lookup"><span data-stu-id="0bc28-117">If no Exchange was detected, then group writeback is not possible tooenable.</span></span>
* <span data-ttu-id="0bc28-118">Seuls les déploiements d’entreprise basés sur une seule forêt Exchange sont actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0bc28-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="0bc28-119">Si vous avez plusieurs Exchange organisation sur site, vous devez une solution GALSync établit un local pour tooappear de ces groupes dans vos autres forêts.</span><span class="sxs-lookup"><span data-stu-id="0bc28-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups tooappear in your other forests.</span></span>
* <span data-ttu-id="0bc28-120">fonctionnalité d’écriture différée de groupe de Hello ne gère pas les groupes de sécurité ou des groupes de distribution.</span><span class="sxs-lookup"><span data-stu-id="0bc28-120">hello Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="0bc28-121">Un tooAzure abonnement Premium d’Active Directory est requis pour l’écriture différée de groupe.</span><span class="sxs-lookup"><span data-stu-id="0bc28-121">A subscription tooAzure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="0bc28-122">Écriture différée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="0bc28-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0bc28-123">fonctionnalité d’aperçu de l’écriture différée d’utilisateur Hello a été supprimée dans tooAzure de mise à jour d’août 2015 hello AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0bc28-123">hello user writeback preview feature was removed in hello August 2015 update tooAzure AD Connect.</span></span> <span data-ttu-id="0bc28-124">Si vous l'avez activée, vous devez désactiver cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0bc28-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0bc28-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bc28-125">Next steps</span></span>
<span data-ttu-id="0bc28-126">Poursuivez votre [installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0bc28-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="0bc28-127">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0bc28-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
