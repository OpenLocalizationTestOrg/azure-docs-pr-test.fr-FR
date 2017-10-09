---
title: "Dépannage : « Active Directory » est manquant ou non disponible | Documents Microsoft"
description: "Le toodo lors de l’élément de menu Active Directory n’apparaît pas dans hello portail de gestion Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="66414-103">Dépannage : l’élément « Active Directory » est manquant ou non disponible</span><span class="sxs-lookup"><span data-stu-id="66414-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="66414-104">De nombreuses instructions hello pour l’utilisation de services et les fonctionnalités d’Azure Active Directory commencent par « accédez toohello portail de gestion Azure et cliquez sur **Active Directory**. »</span><span class="sxs-lookup"><span data-stu-id="66414-104">Many of hello instructions for using Azure Active Directory features and services begin with "Go toohello Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="66414-105">Mais que faire si hello Active Directory extension ou élément de menu ne s’affiche pas ou si elle est marquée **non disponible**?</span><span class="sxs-lookup"><span data-stu-id="66414-105">But what do you do if hello Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="66414-106">Cette rubrique est conçue toohelp.</span><span class="sxs-lookup"><span data-stu-id="66414-106">This topic is designed toohelp.</span></span> <span data-ttu-id="66414-107">Il décrit dans quelles conditions de hello **Active Directory** n’apparaît pas ou n’est pas disponible et explique comment tooproceed.</span><span class="sxs-lookup"><span data-stu-id="66414-107">It describes hello conditions under which **Active Directory** does not appear or is unavailable and explains how tooproceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="66414-108">Active Directory est manquant</span><span class="sxs-lookup"><span data-stu-id="66414-108">Active Directory is missing</span></span>
<span data-ttu-id="66414-109">En règle générale, une **Active Directory** élément apparaît dans le menu de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="66414-109">Typically, an **Active Directory** item appears in hello left navigation menu.</span></span> <span data-ttu-id="66414-110">instructions de Hello dans les procédures d’Azure Active Directory supposent que cet élément est visible.</span><span class="sxs-lookup"><span data-stu-id="66414-110">hello instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Capture d’écran : Active Directory dans Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="66414-112">élément d’Active Directory Hello s’affiche dans le menu de navigation gauche hello lorsqu’une de hello conditions suivantes est vraie.</span><span class="sxs-lookup"><span data-stu-id="66414-112">hello Active Directory item appears in hello left navigation menu when any of hello following conditions is true.</span></span> <span data-ttu-id="66414-113">Sinon, l’élément de hello n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="66414-113">Otherwise, hello item does not appear.</span></span>

* <span data-ttu-id="66414-114">l’utilisateur actuel Hello connecté avec un compte Microsoft (anciennement un identifiant Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="66414-114">hello current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="66414-115">OU</span><span class="sxs-lookup"><span data-stu-id="66414-115">OR</span></span>
* <span data-ttu-id="66414-116">Hello locataire Azure possède un répertoire et compte de hello actuel est un administrateur d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="66414-116">hello Azure tenant has a directory and hello current account is a directory administrator.</span></span>
  
    <span data-ttu-id="66414-117">OU</span><span class="sxs-lookup"><span data-stu-id="66414-117">OR</span></span>
* <span data-ttu-id="66414-118">Hello locataire Azure possède au moins un espace de noms Azure AD Access Control (ACS).</span><span class="sxs-lookup"><span data-stu-id="66414-118">hello Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="66414-119">Pour plus d’informations, consultez la page [À propos des noms d’espaces de contrôle d’accès](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="66414-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="66414-120">OU</span><span class="sxs-lookup"><span data-stu-id="66414-120">OR</span></span>
* <span data-ttu-id="66414-121">Hello locataire Azure possède au moins un fournisseur multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="66414-121">hello Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="66414-122">Pour plus d’informations, consultez la rubrique [Administration des fournisseurs Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="66414-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="66414-123">toocreate un espace de noms de contrôle d’accès ou un fournisseur multi-Factor Authentication, cliquez sur **+ nouveau** > **des Services d’application** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="66414-123">toocreate an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="66414-124">répertoire de tooa tooget droits d’administration, ont un administrateur attribuer à un administrateur tooyour compte membre du rôle.</span><span class="sxs-lookup"><span data-stu-id="66414-124">tooget administrative rights tooa directory, have an administrator assign an administrator role tooyour account.</span></span> <span data-ttu-id="66414-125">Pour plus de détails, consultez [Attribution de rôles d’administrateur](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="66414-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="66414-126">Active Directory n’est pas disponible</span><span class="sxs-lookup"><span data-stu-id="66414-126">Active Directory is not available</span></span>
<span data-ttu-id="66414-127">Lorsque vous cliquez sur **+ New** > **App Services**, un élément **Active Directory** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="66414-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="66414-128">Plus précisément, élément d’Active Directory hello s’affiche lorsqu’une des fonctionnalités d’Active Directory hello, tels que le répertoire, le contrôle d’accès ou fournisseur d’authentification multifacteur est disponible toohello l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="66414-128">Specifically, hello Active Directory item appears when any of hello Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available toohello current user.</span></span>

<span data-ttu-id="66414-129">Toutefois, pendant le chargement de page de hello, élément de hello est estompé et est marqué comme **non disponible**.</span><span class="sxs-lookup"><span data-stu-id="66414-129">However, while hello page is loading, hello item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="66414-130">Il s’agit d’un état temporaire.</span><span class="sxs-lookup"><span data-stu-id="66414-130">This is a temporary state.</span></span> <span data-ttu-id="66414-131">Si vous attendez quelques secondes, l’élément de hello devienne disponible.</span><span class="sxs-lookup"><span data-stu-id="66414-131">If you wait a few seconds, hello item becomes available.</span></span> <span data-ttu-id="66414-132">Si le délai de hello se prolonge, l’actualisation page web de hello résout souvent problème de hello.</span><span class="sxs-lookup"><span data-stu-id="66414-132">If hello delay is prolonged, refreshing hello web page often resolves hello problem.</span></span>

![Capture d’écran : Active Directory n’est pas disponible](./media/active-directory-troubleshooting/not-available.png)

