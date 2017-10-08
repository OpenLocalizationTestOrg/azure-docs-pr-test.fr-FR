---
title: aaaOffice 365 partage externe et Azure Active Directory B2B collaboration | Documents Microsoft
description: "référence de mappage des revendications pour Azure Active Directory B2B Collaboration"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="93e4b-103">Partage externe dans Office 365 et Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="93e4b-104">Externe partage dans Office 365 (OneDrive, SharePoint Online, groupes unifiés, etc.) et Azure Active Directory (Azure AD) B2B collaboration sont techniquement hello même chose.</span><span class="sxs-lookup"><span data-stu-id="93e4b-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="93e4b-105">Partage toutes externes (à l’exception de OneDrive/SharePoint Online), y compris les invités dans les groupes Office 365, invitation de hello Azure AD B2B collaboration API est déjà utilisé pour le partage.</span><span class="sxs-lookup"><span data-stu-id="93e4b-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="93e4b-106">OneDrive/SharePoint Online possède un gestionnaire d’invitation distinct.</span><span class="sxs-lookup"><span data-stu-id="93e4b-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="93e4b-107">La prise en charge par OneDrive/SharePoint Online du partage externe a démarré avant qu’Azure AD ne propose sa prise en charge.</span><span class="sxs-lookup"><span data-stu-id="93e4b-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="93e4b-108">Au fil du temps, partage externe OneDrive/SharePoint Online a à recevoir plusieurs fonctionnalités et des millions d’utilisateurs qui utilisent hello produit dans-intégrée de modèle de partage.</span><span class="sxs-lookup"><span data-stu-id="93e4b-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="93e4b-109">Cependant, il existe quelques différences subtiles entre le fonctionnement du partage externe OneDrive/SharePoint Online et le fonctionnement d’Azure AD B2B Collaboration :</span><span class="sxs-lookup"><span data-stu-id="93e4b-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="93e4b-110">OneDrive/SharePoint Online ajoute active de toohello aux utilisateurs une fois que les utilisateurs ont échangé leur invitation.</span><span class="sxs-lookup"><span data-stu-id="93e4b-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="93e4b-111">Par conséquent, avant de remboursement, vous ne voyez pas utilisateur hello dans le portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93e4b-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="93e4b-112">Si un autre site invite un utilisateur Bonjour pendant ce temps, une nouvelle invitation est générée.</span><span class="sxs-lookup"><span data-stu-id="93e4b-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="93e4b-113">En revanche, lorsque vous utilisez Azure AD B2B Collaboration, les utilisateurs sont ajoutés immédiatement sur invitation afin qu’ils apparaissent partout.</span><span class="sxs-lookup"><span data-stu-id="93e4b-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="93e4b-114">expérience de remboursement Hello dans OneDrive/SharePoint Online, différent de l’expérience hello dans Azure AD B2B collaboration.</span><span class="sxs-lookup"><span data-stu-id="93e4b-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="93e4b-115">Une fois un utilisateur a utilisé une invitation, hello expériences similitude.</span><span class="sxs-lookup"><span data-stu-id="93e4b-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="93e4b-116">Les utilisateurs invités par Azure AD B2B Collaboration peuvent être sélectionnés à partir des boîtes de dialogue de partage de OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="93e4b-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="93e4b-117">Les utilisateurs invités par OneDrive/SharePoint Online apparaissent également dans Azure AD une fois qu’ils ont utilisé leur invitation.</span><span class="sxs-lookup"><span data-stu-id="93e4b-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="93e4b-118">toomanage externe partage dans OneDrive/SharePoint Online avec Azure AD B2B collaboration, définissez hello OneDrive/SharePoint Online externe aussi un paramètre de partage**uniquement autoriser le partage avec des utilisateurs externes déjà dans le répertoire de hello**.</span><span class="sxs-lookup"><span data-stu-id="93e4b-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="93e4b-119">Les utilisateurs peuvent accéder à des sites de tooexternally partagé et choix de collaborateurs externes qui hello admin a ajouté.</span><span class="sxs-lookup"><span data-stu-id="93e4b-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="93e4b-120">Hello administrateur peut ajouter des collaborateurs externes de hello via hello invitation de collaboration B2B API.</span><span class="sxs-lookup"><span data-stu-id="93e4b-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![Hello externe partagent le même paramètre OneDrive/SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="93e4b-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93e4b-122">Next steps</span></span>

<span data-ttu-id="93e4b-123">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="93e4b-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="93e4b-124">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="93e4b-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="93e4b-125">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="93e4b-126">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="93e4b-127">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="93e4b-128">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="93e4b-129">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="93e4b-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="93e4b-130">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="93e4b-131">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="93e4b-132">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="93e4b-133">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="93e4b-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
