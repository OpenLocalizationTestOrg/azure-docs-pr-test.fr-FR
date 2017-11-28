---
title: "aaaCharacteristics d’Azure Active Directory locataire intercaction | Documents Microsoft"
description: "Gérer vos locataires Azure Active Directory en les considérant comme des ressources entièrement indépendantes"
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="137fb-103">Comprendre l’interaction entre plusieurs locataires Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="137fb-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="137fb-104">Dans Azure Active Directory (Azure AD), chaque tenent est une ressource entièrement indépendante : un homologue logiquement indépendant hello autres clients que vous gérez.</span><span class="sxs-lookup"><span data-stu-id="137fb-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from hello other tenants that you manage.</span></span> <span data-ttu-id="137fb-105">Il n’existe pas de relation parent-enfant entre les locataires.</span><span class="sxs-lookup"><span data-stu-id="137fb-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="137fb-106">Cette indépendance entre les locataires vaut pour les ressources, l’administration et la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="137fb-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="137fb-107">Indépendance des ressources</span><span class="sxs-lookup"><span data-stu-id="137fb-107">Resource independence</span></span>
* <span data-ttu-id="137fb-108">Si vous créez ou supprimez une ressource dans un locataire, il n’a aucun impact sur les ressources dans une autre locataire, à l’exception de partielle de hello des utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="137fb-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with hello partial exception of external users.</span></span> 
* <span data-ttu-id="137fb-109">Si vous utilisez l’un de vos noms de domaine avec un locataire, il ne peut être utilisé avec aucun autre locataire.</span><span class="sxs-lookup"><span data-stu-id="137fb-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="137fb-110">Indépendance de l’administration</span><span class="sxs-lookup"><span data-stu-id="137fb-110">Administrative independence</span></span>
<span data-ttu-id="137fb-111">Si un utilisateur non administrateur du locataire « Contoso » crée le locataire de test « Test », alors :</span><span class="sxs-lookup"><span data-stu-id="137fb-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="137fb-112">Par défaut, utilisateur hello qui crée un client est ajouté en tant qu’un utilisateur externe dans un nouveau client et rôle d’administrateur général hello affectées dans ce locataire.</span><span class="sxs-lookup"><span data-stu-id="137fb-112">By default, hello user who creates a tenant is added as an external user in that new tenant, and assigned hello global administrator role in that tenant.</span></span>
* <span data-ttu-id="137fb-113">les administrateurs de Hello du client « Contoso » n’ont aucun tootenant des privilèges d’administrateur direct « Test », sauf si un administrateur de « Test » leur ait spécifiquement accordé ces privilèges.</span><span class="sxs-lookup"><span data-stu-id="137fb-113">hello administrators of tenant 'Contoso' have no direct administrative privileges tootenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="137fb-114">Toutefois, les administrateurs de « Contoso » peuvent contrôler les accès tootenant 'Test' Si contrôle de compte d’utilisateur hello créé « Test ».</span><span class="sxs-lookup"><span data-stu-id="137fb-114">However, administrators of 'Contoso' can control access tootenant 'Test' if they control hello user account that created 'Test.'</span></span>
* <span data-ttu-id="137fb-115">Si vous ajouter/supprimer un rôle d’administrateur d’un utilisateur dans un locataire, la fonction changement de hello ne pas les rôles d’administrateur de hello affectent ce hello utilisateur a dans un autre client.</span><span class="sxs-lookup"><span data-stu-id="137fb-115">If you add/remove an administrator role for a user in one tenant, hello change does not affect hello administrator roles that hello user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="137fb-116">Indépendance de la synchronisation</span><span class="sxs-lookup"><span data-stu-id="137fb-116">Synchronization independence</span></span>
<span data-ttu-id="137fb-117">Vous pouvez configurer chaque Azure AD de locataire indépendamment tooget les données synchronisées à partir d’une seule instance d’un :</span><span class="sxs-lookup"><span data-stu-id="137fb-117">You can configure each Azure AD tenant independently tooget data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="137fb-118">outil de connexion Hello Azure AD, données toosynchronize avec une seule forêt Active Directory.</span><span class="sxs-lookup"><span data-stu-id="137fb-118">hello Azure AD Connect tool, toosynchronize data with a single AD forest.</span></span>
* <span data-ttu-id="137fb-119">Hello locataire Azure Active connecteur pour Forefront Identity Manager, les données toosynchronize avec l’un ou plusieurs locaux forêts et/ou des sources de données non-Azure AD.</span><span class="sxs-lookup"><span data-stu-id="137fb-119">hello Azure Active tenant Connector for Forefront Identity Manager, toosynchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="137fb-120">Ajouter un locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="137fb-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="137fb-121">tooadd un locataire Azure AD Bonjour portail Azure, connectez-vous trop[hello portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global Azure AD et, sur hello gauche, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="137fb-121">tooadd an Azure AD tenant in hello Azure portal, sign in too[hello Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on hello left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="137fb-122">Contrairement aux autres ressources Azure, vos locataires ne sont pas des ressources enfants d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="137fb-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="137fb-123">Si votre abonnement Azure est annulée ou a expiré, vous pouvez toujours accéder à vos données client à l’aide du centre d’administration hello Office 365, hello API Azure Graph ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="137fb-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, hello Azure Graph API, or hello Office 365 Admin Center.</span></span> <span data-ttu-id="137fb-124">Vous pouvez également associer un autre abonnement hello client.</span><span class="sxs-lookup"><span data-stu-id="137fb-124">You can also associate another subscription with hello tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="137fb-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="137fb-125">Next steps</span></span>
<span data-ttu-id="137fb-126">Pour obtenir une vue d’ensemble des problèmes de licence Azure AD et découvrir les bonnes pratiques, consultez [Qu’est-ce que la gestion de licences de locataires Azure Active Directory ?](active-directory-licensing-whatis-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="137fb-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
