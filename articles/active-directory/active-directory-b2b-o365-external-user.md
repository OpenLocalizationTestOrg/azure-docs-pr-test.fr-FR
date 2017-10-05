---
title: Partage externe dans Office 365 et Azure Active Directory B2B Collaboration | Microsoft Docs
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
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="660fe-103">Partage externe dans Office 365 et Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="660fe-104">Le partage externe dans Office 365 (OneDrive, SharePoint Online, groupes unifiés, etc.) et Azure Active Directory (Azure AD) B2B Collaboration revient techniquement au même.</span><span class="sxs-lookup"><span data-stu-id="660fe-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="660fe-105">Tous les partages externes (à l’exception de OneDrive/SharePoint Online), notamment les invités dans les groupes Office 365, utilisent déjà les API d’invitation Azure AD B2B Collaboration pour le partage.</span><span class="sxs-lookup"><span data-stu-id="660fe-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="660fe-106">OneDrive/SharePoint Online possède un gestionnaire d’invitation distinct.</span><span class="sxs-lookup"><span data-stu-id="660fe-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="660fe-107">La prise en charge par OneDrive/SharePoint Online du partage externe a démarré avant qu’Azure AD ne propose sa prise en charge.</span><span class="sxs-lookup"><span data-stu-id="660fe-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="660fe-108">Au fil du temps, plusieurs fonctionnalités ont été ajoutées au partage externe OneDrive/SharePoint Online, ce qui a attiré de des millions d’utilisateurs exploitant le modèle de partage intégré.</span><span class="sxs-lookup"><span data-stu-id="660fe-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="660fe-109">Cependant, il existe quelques différences subtiles entre le fonctionnement du partage externe OneDrive/SharePoint Online et le fonctionnement d’Azure AD B2B Collaboration :</span><span class="sxs-lookup"><span data-stu-id="660fe-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="660fe-110">OneDrive/SharePoint Online ajoute les utilisateurs au répertoire une fois qu’ils ont utilisé leurs invitations.</span><span class="sxs-lookup"><span data-stu-id="660fe-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="660fe-111">Par conséquent, avant qu’il utilise son invitation, l’utilisateur n’apparaît pas dans le portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="660fe-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="660fe-112">Si un autre site invite un utilisateur dans l’intervalle, une nouvelle invitation est générée.</span><span class="sxs-lookup"><span data-stu-id="660fe-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="660fe-113">En revanche, lorsque vous utilisez Azure AD B2B Collaboration, les utilisateurs sont ajoutés immédiatement sur invitation afin qu’ils apparaissent partout.</span><span class="sxs-lookup"><span data-stu-id="660fe-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="660fe-114">L’expérience d’utilisation de l’invitation dans OneDrive/SharePoint Online est différente de celle d’Azure AD B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="660fe-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="660fe-115">Une fois l’invitation utilisée, les expériences sont similaires.</span><span class="sxs-lookup"><span data-stu-id="660fe-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="660fe-116">Les utilisateurs invités par Azure AD B2B Collaboration peuvent être sélectionnés à partir des boîtes de dialogue de partage de OneDrive/SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="660fe-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="660fe-117">Les utilisateurs invités par OneDrive/SharePoint Online apparaissent également dans Azure AD une fois qu’ils ont utilisé leur invitation.</span><span class="sxs-lookup"><span data-stu-id="660fe-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="660fe-118">Pour gérer le partage externe dans OneDrive/SharePoint Online avec Azure AD B2B Collaboration, définissez le paramètre OneDrive/SharePoint Online de partage externe sur **Autoriser le partage uniquement avec des utilisateurs externes figurant déjà dans le répertoire**.</span><span class="sxs-lookup"><span data-stu-id="660fe-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="660fe-119">Les utilisateurs peuvent accéder à des sites partagés de manière externe et choisir parmi les collaborateurs externes ajoutés par l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="660fe-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="660fe-120">L’administrateur peut ajouter les collaborateurs externes par le biais des API d’invitation B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="660fe-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![Paramètre OneDrive/SharePoint Online de partage externe](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="660fe-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="660fe-122">Next steps</span></span>

<span data-ttu-id="660fe-123">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="660fe-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="660fe-124">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="660fe-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="660fe-125">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="660fe-126">Ajout d’un utilisateur B2B Collaboration à un rôle</span><span class="sxs-lookup"><span data-stu-id="660fe-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="660fe-127">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="660fe-128">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="660fe-129">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="660fe-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="660fe-130">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="660fe-131">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="660fe-132">Mappage des revendications utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="660fe-133">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="660fe-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
