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
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a><span data-ttu-id="9dec9-103">Plus de détails sur les fonctionnalités de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="9dec9-103">More details about features in preview</span></span>
<span data-ttu-id="9dec9-104">Cette rubrique décrit l’utilisation des fonctionnalités disponibles dans la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="9dec9-104">This topic describes how to use features currently in preview.</span></span>

## <a name="group-writeback"></a><span data-ttu-id="9dec9-105">Écriture différée de groupe</span><span class="sxs-lookup"><span data-stu-id="9dec9-105">Group writeback</span></span>
<span data-ttu-id="9dec9-106">L’option pour l’écriture différée de groupe dans les fonctionnalités facultatives permet l’écriture différée de **groupes dans Office 365** vers une forêt avec Exchange installé.</span><span class="sxs-lookup"><span data-stu-id="9dec9-106">The option for group writeback in optional features allows you to writeback **Office 365 Groups** to a forest with Exchange installed.</span></span> <span data-ttu-id="9dec9-107">Il s’agit d’un nouveau type de groupe qui est toujours contrôlé dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="9dec9-107">This is a group that is always mastered in the cloud.</span></span> <span data-ttu-id="9dec9-108">Si Exchange est installé sur site, vous pouvez réécrire ces groupes en local afin que les utilisateurs disposant d’une boîte aux lettres Exchange locale puissent envoyer et recevoir des e-mails de la part de ces groupes.</span><span class="sxs-lookup"><span data-stu-id="9dec9-108">If you have Exchange on-premises, then you can write back these groups to on-premises so users with an on-premises Exchange mailbox can send and receive emails from these groups.</span></span>

<span data-ttu-id="9dec9-109">Vous trouverez [ici](http://aka.ms/O365g)d’autres informations sur les groupes Office 365 et la façon de les utiliser.</span><span class="sxs-lookup"><span data-stu-id="9dec9-109">More information about Office 365 Groups and how to use them can be found [here](http://aka.ms/O365g).</span></span>

<span data-ttu-id="9dec9-110">Un groupe Office 365 est représenté comme un groupe de distribution dans les versions locales d’AD DS.</span><span class="sxs-lookup"><span data-stu-id="9dec9-110">An Office 365 group is represented as a distribution group in on-premises AD DS.</span></span> <span data-ttu-id="9dec9-111">Votre serveur Exchange local doit être au niveau de la mise à jour cumulative 8 d’Exchange 2013 (publiée en mars 2015) ou d’Exchange 2016 pour pouvoir reconnaître ce nouveau type de groupe.</span><span class="sxs-lookup"><span data-stu-id="9dec9-111">Your on-premises Exchange server must be on Exchange 2013 cumulative update 8 (released in March 2015) or Exchange 2016 to recognize this new group type.</span></span>

<span data-ttu-id="9dec9-112">**Notes relatives à la version préliminaire**</span><span class="sxs-lookup"><span data-stu-id="9dec9-112">**Notes during the preview**</span></span>

* <span data-ttu-id="9dec9-113">L’attribut de carnet d’adresses n’est pas rempli pour l’instant dans la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="9dec9-113">The address book attribute is currently not populated in the preview.</span></span> <span data-ttu-id="9dec9-114">Sans cet attribut, le groupe n’est pas visible dans la liste d’adresses globale.</span><span class="sxs-lookup"><span data-stu-id="9dec9-114">Without this attribute, the group is not visible in the GAL.</span></span> <span data-ttu-id="9dec9-115">Le moyen le plus simple de renseigner cet attribut est d’utiliser l’applet de commande Exchange PowerShell `update-recipient`.</span><span class="sxs-lookup"><span data-stu-id="9dec9-115">The easiest way to populate this attribute is to use the Exchange PowerShell cmdlet `update-recipient`.</span></span>
* <span data-ttu-id="9dec9-116">Seules les forêts dotées du schéma Exchange constituent des cibles valides pour les groupes.</span><span class="sxs-lookup"><span data-stu-id="9dec9-116">Only forests with the Exchange schema are valid targets for groups.</span></span> <span data-ttu-id="9dec9-117">Si aucune version d’Exchange n’est détectée, il est impossible d’activer l’écriture différée de groupe.</span><span class="sxs-lookup"><span data-stu-id="9dec9-117">If no Exchange was detected, then group writeback is not possible to enable.</span></span>
* <span data-ttu-id="9dec9-118">Seuls les déploiements d’entreprise basés sur une seule forêt Exchange sont actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9dec9-118">Only single-forest Exchange organization deployments are currently supported.</span></span> <span data-ttu-id="9dec9-119">Si vous avez plusieurs organisations Exchange en local, vous avez besoin d’une solution GALSync locale pour que ces groupes s’affichent dans vos autres forêts.</span><span class="sxs-lookup"><span data-stu-id="9dec9-119">If you have more than one Exchange organization on-premises, then you need an on-premises GALSync solution for these groups to appear in your other forests.</span></span>
* <span data-ttu-id="9dec9-120">La fonctionnalité d’écriture différée de groupe ne prend pas en charge les groupes de sécurité ou les groupes de distribution.</span><span class="sxs-lookup"><span data-stu-id="9dec9-120">The Group writeback feature does not handle security groups or distribution groups.</span></span>

> [!NOTE]
> <span data-ttu-id="9dec9-121">L’écriture différée des groupes nécessite un abonnement Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="9dec9-121">A subscription to Azure AD Premium is required for group writeback.</span></span>
> 
>

## <a name="user-writeback"></a><span data-ttu-id="9dec9-122">Écriture différée de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="9dec9-122">User writeback</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9dec9-123">La fonctionnalité d’écriture différée utilisateur en version préliminaire a été supprimée lors de la mise à jour d’Azure AD Connect en août 2015.</span><span class="sxs-lookup"><span data-stu-id="9dec9-123">The user writeback preview feature was removed in the August 2015 update to Azure AD Connect.</span></span> <span data-ttu-id="9dec9-124">Si vous l'avez activée, vous devez désactiver cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9dec9-124">If you have enabled it, then you should disable this feature.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9dec9-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9dec9-125">Next steps</span></span>
<span data-ttu-id="9dec9-126">Poursuivez votre [installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="9dec9-126">Continue your [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

<span data-ttu-id="9dec9-127">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9dec9-127">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
