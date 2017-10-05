---
title: "Guide pratique pour affecter des utilisateurs à des applications | Microsoft Docs"
description: "Comprendre comment les utilisateurs sont affectés à une application dans votre client"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="d5b16-103">Guide pratique pour affecter des utilisateurs à des applications</span><span class="sxs-lookup"><span data-stu-id="d5b16-103">How to assign users to applications</span></span>

<span data-ttu-id="d5b16-104">Cet article vous explique comment les utilisateurs sont affectés à une application dans votre client.</span><span class="sxs-lookup"><span data-stu-id="d5b16-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="d5b16-105">Comment les utilisateurs sont-ils affectés à une application dans Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="d5b16-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="d5b16-106">Pour qu’un utilisateur puisse accéder à une application, il doit tout d’abord être affecté à cette application d’une certaine manière.</span><span class="sxs-lookup"><span data-stu-id="d5b16-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="d5b16-107">L’affectation peut être effectuée par un administrateur, un délégué de l’entreprise ou, parfois, par l’utilisateur lui-même.</span><span class="sxs-lookup"><span data-stu-id="d5b16-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="d5b16-108">Voici une description des méthodes permettant d’affecter des utilisateurs à des applications :</span><span class="sxs-lookup"><span data-stu-id="d5b16-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="d5b16-109">Un administrateur [affecte un utilisateur](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) directement à l’application</span><span class="sxs-lookup"><span data-stu-id="d5b16-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="d5b16-110">Un administrateur [affecte un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) dont l’utilisateur est membre à l’application, y compris :</span><span class="sxs-lookup"><span data-stu-id="d5b16-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="d5b16-111">Un groupe synchronisé localement</span><span class="sxs-lookup"><span data-stu-id="d5b16-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="d5b16-112">Un groupe de sécurité statique créé dans le cloud</span><span class="sxs-lookup"><span data-stu-id="d5b16-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="d5b16-113">Un [groupe de sécurité dynamique](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) créé dans le cloud</span><span class="sxs-lookup"><span data-stu-id="d5b16-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="d5b16-114">Un groupe Office 365 créé dans le cloud</span><span class="sxs-lookup"><span data-stu-id="d5b16-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="d5b16-115">Le groupe [Tous les utilisateurs](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups)</span><span class="sxs-lookup"><span data-stu-id="d5b16-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="d5b16-116">Un administrateur active l[’accès aux applications en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) pour autoriser un utilisateur à ajouter une application à l’aide de la fonctionnalité **Ajouter une application** du [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction), **sans approbation de l’entreprise**</span><span class="sxs-lookup"><span data-stu-id="d5b16-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="d5b16-117">Un administrateur active l[’accès aux applications en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) pour autoriser un utilisateur à ajouter une application à l’aide de la fonctionnalité **Ajouter une application** du [volet d’accès aux applications](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction), mais uniquement **après approbation d’un ensemble sélectionné d’approbateurs d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="d5b16-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="d5b16-118">Un administrateur active la [gestion des groupes en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) pour permettre à un utilisateur de joindre un groupe auquel une application est affectée, **sans approbation d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="d5b16-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="d5b16-119">Un administrateur active la [gestion des groupes en libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) pour permettre à un utilisateur de joindre un groupe auquel une application est affectée, mais uniquement **après approbation d’un ensemble sélectionné d’approbateurs d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="d5b16-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="d5b16-120">Un administrateur affecte une licence à un utilisateur pour une première application, par exemple [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="d5b16-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="d5b16-121">Un administrateur affecte une licence à un groupe dont l’utilisateur est membre pour une première application, par exemple [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="d5b16-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="d5b16-122">Un [administrateur donne son consentement à une application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) pour être utilisée par tous les utilisateurs, puis un utilisateur se connecte à l’application</span><span class="sxs-lookup"><span data-stu-id="d5b16-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="d5b16-123">Un utilisateur [donne lui-même son consentement à une application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) en se connectant à l’application</span><span class="sxs-lookup"><span data-stu-id="d5b16-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5b16-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5b16-124">Next steps</span></span>
[<span data-ttu-id="d5b16-125">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5b16-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
