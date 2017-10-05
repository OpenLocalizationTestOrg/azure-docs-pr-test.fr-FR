---
title: "Caractéristiques de l’interaction des locataires Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: d25d2c731034d0785bbd404ec693c4c41d913d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a><span data-ttu-id="85726-103">Comprendre l’interaction entre plusieurs locataires Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85726-103">Understand how multiple Azure Active Directory tenants interact</span></span>

<span data-ttu-id="85726-104">Dans Azure Active Directory (Azure AD), chaque locataire est une ressource entièrement indépendante, c’est-à-dire un homologue logiquement indépendant des autres locataires que vous gérez.</span><span class="sxs-lookup"><span data-stu-id="85726-104">In Azure Active Directory (Azure AD), each tenent is a fully independent resource: a peer that is logically independent from the other tenants that you manage.</span></span> <span data-ttu-id="85726-105">Il n’existe pas de relation parent-enfant entre les locataires.</span><span class="sxs-lookup"><span data-stu-id="85726-105">There is no parent-child relationship between tenants.</span></span> <span data-ttu-id="85726-106">Cette indépendance entre les locataires vaut pour les ressources, l’administration et la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="85726-106">This independence between tenants includes resource independence, administrative independence, and synchronization independence.</span></span>

## <a name="resource-independence"></a><span data-ttu-id="85726-107">Indépendance des ressources</span><span class="sxs-lookup"><span data-stu-id="85726-107">Resource independence</span></span>
* <span data-ttu-id="85726-108">Si vous créez ou supprimez une ressource dans un locataire, cela n’a aucun effet sur les ressources d’un autre locataire, si l’on excepte le cas des utilisateurs externes.</span><span class="sxs-lookup"><span data-stu-id="85726-108">If you create or delete a resource in one tenant, it has no impact on any resource in another tenant, with the partial exception of external users.</span></span> 
* <span data-ttu-id="85726-109">Si vous utilisez l’un de vos noms de domaine avec un locataire, il ne peut être utilisé avec aucun autre locataire.</span><span class="sxs-lookup"><span data-stu-id="85726-109">If you use one of your domain names with one tenant, it cannot be used with any other tenant.</span></span>

## <a name="administrative-independence"></a><span data-ttu-id="85726-110">Indépendance de l’administration</span><span class="sxs-lookup"><span data-stu-id="85726-110">Administrative independence</span></span>
<span data-ttu-id="85726-111">Si un utilisateur non administrateur du locataire « Contoso » crée le locataire de test « Test », alors :</span><span class="sxs-lookup"><span data-stu-id="85726-111">If a non-administrative user of tenant 'Contoso' creates a test tenant 'Test,' then:</span></span>

* <span data-ttu-id="85726-112">Par défaut, l’utilisateur qui crée un locataire est ajouté comme utilisateur externe dans ce nouveau locataire et se voit attribuer rôle d’administrateur général dans ce locataire.</span><span class="sxs-lookup"><span data-stu-id="85726-112">By default, the user who creates a tenant is added as an external user in that new tenant, and assigned the global administrator role in that tenant.</span></span>
* <span data-ttu-id="85726-113">Les administrateurs du locataire « Contoso » n’ont pas de privilèges d’administration directs sur le locataire « Test », à moins qu’un administrateur de « Test » leur ait spécifiquement accordé ces privilèges.</span><span class="sxs-lookup"><span data-stu-id="85726-113">The administrators of tenant 'Contoso' have no direct administrative privileges to tenant 'Test,' unless an administrator of 'Test' specifically grants them these privileges.</span></span> <span data-ttu-id="85726-114">Cependant, les administrateurs de « Contoso » peuvent contrôler l’accès au locataire « Test » s’ils contrôlent le compte d’utilisateur qui a créé « Test ».</span><span class="sxs-lookup"><span data-stu-id="85726-114">However, administrators of 'Contoso' can control access to tenant 'Test' if they control the user account that created 'Test.'</span></span>
* <span data-ttu-id="85726-115">Si vous ajoutez et/ou supprimez un rôle d’administrateur pour un utilisateur dans un locataire, la modification n’a aucun impact sur les rôles d’administrateur que l’utilisateur possède dans une autre locataire.</span><span class="sxs-lookup"><span data-stu-id="85726-115">If you add/remove an administrator role for a user in one tenant, the change does not affect the administrator roles that the user has in another tenant.</span></span>

## <a name="synchronization-independence"></a><span data-ttu-id="85726-116">Indépendance de la synchronisation</span><span class="sxs-lookup"><span data-stu-id="85726-116">Synchronization independence</span></span>
<span data-ttu-id="85726-117">Vous pouvez configurer chaque locataire Azure AD de manière indépendante de sorte que les données soient synchronisées à partir d’une même instance de :</span><span class="sxs-lookup"><span data-stu-id="85726-117">You can configure each Azure AD tenant independently to get data synchronized from a single instance of either:</span></span>

* <span data-ttu-id="85726-118">l’outil Azure AD Connect, pour synchroniser les données avec une seule forêt AD ;</span><span class="sxs-lookup"><span data-stu-id="85726-118">The Azure AD Connect tool, to synchronize data with a single AD forest.</span></span>
* <span data-ttu-id="85726-119">Azure Active Directory Connector pour Forefront Identity Manager, pour synchroniser les données avec une ou plusieurs forêts locales et/ou des sources de données non Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85726-119">The Azure Active tenant Connector for Forefront Identity Manager, to synchronize data with one or more on-premises forests, and/or non-Azure AD data sources.</span></span>

## <a name="add-an-azure-ad-tenant"></a><span data-ttu-id="85726-120">Ajouter un locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="85726-120">Add an Azure AD tenant</span></span>
<span data-ttu-id="85726-121">Pour ajouter un locataire Azure AD dans le portail Azure, connectez-vous au [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur général Azure AD et, sur la gauche, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="85726-121">To add an Azure AD tenant in the Azure portal, sign in to [the Azure portal](https://portal.azure.com) with an account that is an Azure AD global administrator, and, on the left, select **New**.</span></span>

> [!NOTE]
> <span data-ttu-id="85726-122">Contrairement aux autres ressources Azure, vos locataires ne sont pas des ressources enfants d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="85726-122">Unlike other Azure resources, your tenants are not child resources of an Azure subscription.</span></span> <span data-ttu-id="85726-123">Si votre abonnement Azure est annulé ou qu’il est arrivé à expiration, vous pouvez toujours accéder aux données de votre locataire via Azure PowerShell, l’API Azure Graph ou le centre d’administration Office 365.</span><span class="sxs-lookup"><span data-stu-id="85726-123">If your Azure subscription is canceled or expired, you can still access your tenant data using Azure PowerShell, the Azure Graph API, or the Office 365 Admin Center.</span></span> <span data-ttu-id="85726-124">Vous pouvez aussi associer un autre abonnement au locataire.</span><span class="sxs-lookup"><span data-stu-id="85726-124">You can also associate another subscription with the tenant.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="85726-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85726-125">Next steps</span></span>
<span data-ttu-id="85726-126">Pour obtenir une vue d’ensemble des problèmes de licence Azure AD et découvrir les bonnes pratiques, consultez [Qu’est-ce que la gestion de licences de locataires Azure Active Directory ?](active-directory-licensing-whatis-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="85726-126">For a broad overview of Azure AD licensing issues and best practices, see [What is Azure Active tenant licensing?](active-directory-licensing-whatis-azure-portal.md)</span></span>
