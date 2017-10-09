---
title: aaaHow tooAssign utilisateurs tooapplications | Documents Microsoft
description: "Comprendre comment les utilisateurs sont affectées application tooan dans votre client"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="bdba4-103">Comment tooassign utilisateurs tooapplications</span><span class="sxs-lookup"><span data-stu-id="bdba4-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="bdba4-104">Cet article vous a-t-il toounderstand comment les utilisateurs sont affectées application tooan dans votre client.</span><span class="sxs-lookup"><span data-stu-id="bdba4-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="bdba4-105">Comment les utilisateurs sont affectées application tooan dans Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="bdba4-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="bdba4-106">Pour un utilisateur tooaccess une application, ils doivent d’abord être affectés tooit d’une certaine façon.</span><span class="sxs-lookup"><span data-stu-id="bdba4-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="bdba4-107">L’attribution peut être effectuée par un administrateur, un délégué de l’entreprise ou parfois hello utilisateur eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="bdba4-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="bdba4-108">Ci-dessous décrit les façons de hello tooapplications obtenir affecter des utilisateurs :</span><span class="sxs-lookup"><span data-stu-id="bdba4-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="bdba4-109">Un administrateur [affecte un utilisateur](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) application toohello directement</span><span class="sxs-lookup"><span data-stu-id="bdba4-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="bdba4-110">Un administrateur [affecte un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) cet utilisateur hello est un membre de l’application de toohello, y compris :</span><span class="sxs-lookup"><span data-stu-id="bdba4-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="bdba4-111">Un groupe synchronisé localement</span><span class="sxs-lookup"><span data-stu-id="bdba4-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="bdba4-112">Un groupe de sécurité statique créé dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="bdba4-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="bdba4-113">A [groupe de sécurité dynamique](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) créé dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="bdba4-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="bdba4-114">Un groupe Office 365 créé dans hello cloud</span><span class="sxs-lookup"><span data-stu-id="bdba4-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="bdba4-115">Hello [tous les utilisateurs](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) groupe</span><span class="sxs-lookup"><span data-stu-id="bdba4-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="bdba4-116">Un administrateur Active [accès à l’Application libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd utilisateur un à l’aide de l’application hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **ajouter une application** fonctionnalité **sans l’approbation de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="bdba4-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="bdba4-117">Un administrateur Active [accès libre-service à l’Application](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow un tooadd utilisateur un à l’aide de l’application hello [volet d’accès Application](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **ajouter une application** fonctionnalité mais uniquement w **préalable de rang à partir d’un ensemble sélectionné d’approbateurs de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="bdba4-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="bdba4-118">Un administrateur Active [gestion de groupe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin utilisateur un groupe une application est trop**sans l’approbation de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="bdba4-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="bdba4-119">Un administrateur Active [gestion de groupe libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow un toojoin utilisateur un groupe qui est assigné à une application de, mais uniquement **avec une approbation préalable à partir d’un ensemble sélectionné d’approbateurs de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="bdba4-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="bdba4-120">Un administrateur affecte un licence tooa utilisateur directement une première application, comme [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="bdba4-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="bdba4-121">Un administrateur affecte un groupe de tooa de licence qui hello utilisateur est un membre de la première application de partie tooa, comme [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="bdba4-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="bdba4-122">Un [administrateur donne son consentement tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe utilisé par tous les utilisateurs et un utilisateur se connecte ensuite toohello application</span><span class="sxs-lookup"><span data-stu-id="bdba4-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="bdba4-123">Un utilisateur [donne son consentement tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) eux-mêmes en vous connectant toohello application</span><span class="sxs-lookup"><span data-stu-id="bdba4-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdba4-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bdba4-124">Next steps</span></span>
[<span data-ttu-id="bdba4-125">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdba4-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
