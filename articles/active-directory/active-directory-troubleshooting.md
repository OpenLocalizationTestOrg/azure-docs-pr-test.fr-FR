---
title: "Dépannage : « Active Directory » est manquant ou non disponible | Documents Microsoft"
description: "Que faire lorsque l’élément de menu Active Directory n’apparaît pas dans le portail de gestion Azure."
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
ms.openlocfilehash: be3a797c4a405fd2f6636e67f4c961dd6d143486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a><span data-ttu-id="0cb23-103">Dépannage : l’élément « Active Directory » est manquant ou non disponible</span><span class="sxs-lookup"><span data-stu-id="0cb23-103">Troubleshooting: 'Active Directory' item is missing or not available</span></span>
<span data-ttu-id="0cb23-104">De nombreuses instructions relatives à l’utilisation des fonctionnalités et des services d’Azure Active Directory commencent par « Accédez au portail de gestion Azure et cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0cb23-104">Many of the instructions for using Azure Active Directory features and services begin with "Go to the Azure Management Portal and click **Active Directory**."</span></span> <span data-ttu-id="0cb23-105">» Mais que faire si l’élément de menu ou l’extension Active Directory n’apparaît pas ou si elle est marquée comme **non disponible**?</span><span class="sxs-lookup"><span data-stu-id="0cb23-105">But what do you do if the Active Directory extension or menu item does not appear or if it is marked **Not Available**?</span></span> <span data-ttu-id="0cb23-106">Cette rubrique d’aide répond à cette question.</span><span class="sxs-lookup"><span data-stu-id="0cb23-106">This topic is designed to help.</span></span> <span data-ttu-id="0cb23-107">Elle décrit les conditions dans lesquelles **Active Directory** n’apparaît pas ou n’est pas disponible et explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="0cb23-107">It describes the conditions under which **Active Directory** does not appear or is unavailable and explains how to proceed.</span></span>

## <a name="active-directory-is-missing"></a><span data-ttu-id="0cb23-108">Active Directory est manquant</span><span class="sxs-lookup"><span data-stu-id="0cb23-108">Active Directory is missing</span></span>
<span data-ttu-id="0cb23-109">En règle générale, un élément **Active Directory** apparaît dans le menu de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="0cb23-109">Typically, an **Active Directory** item appears in the left navigation menu.</span></span> <span data-ttu-id="0cb23-110">Les instructions dans les procédures d’Azure Active Directory supposent que cet élément est visible.</span><span class="sxs-lookup"><span data-stu-id="0cb23-110">The instructions in Azure Active Directory procedures assume that this item is in your view.</span></span>

![Capture d’écran : Active Directory dans Azure](./media/active-directory-troubleshooting/typical-view.png)

<span data-ttu-id="0cb23-112">L’élément Active Directory s’affiche dans le menu de navigation gauche lorsqu’une des conditions suivantes est vraie.</span><span class="sxs-lookup"><span data-stu-id="0cb23-112">The Active Directory item appears in the left navigation menu when any of the following conditions is true.</span></span> <span data-ttu-id="0cb23-113">Sinon, l’élément n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="0cb23-113">Otherwise, the item does not appear.</span></span>

* <span data-ttu-id="0cb23-114">L’utilisateur actuel est connecté avec un compte Microsoft (anciennement appelé identifiant Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="0cb23-114">The current user signed on with a Microsoft account (formerly known as a Windows Live ID).</span></span>
  
    <span data-ttu-id="0cb23-115">OU</span><span class="sxs-lookup"><span data-stu-id="0cb23-115">OR</span></span>
* <span data-ttu-id="0cb23-116">Le locataire Azure possède un répertoire et le compte actuel est un administrateur d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="0cb23-116">The Azure tenant has a directory and the current account is a directory administrator.</span></span>
  
    <span data-ttu-id="0cb23-117">OU</span><span class="sxs-lookup"><span data-stu-id="0cb23-117">OR</span></span>
* <span data-ttu-id="0cb23-118">Le locataire Azure possède au moins un espace de noms Azure AD Access Control (ACS).</span><span class="sxs-lookup"><span data-stu-id="0cb23-118">The Azure tenant has at least one Azure AD Access Control (ACS) namespace.</span></span> <span data-ttu-id="0cb23-119">Pour plus d’informations, consultez la page [À propos des noms d’espaces de contrôle d’accès](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cb23-119">For more information, see [Access Control Namespace](https://msdn.microsoft.com/library/azure/gg185908.aspx).</span></span>
  
    <span data-ttu-id="0cb23-120">OU</span><span class="sxs-lookup"><span data-stu-id="0cb23-120">OR</span></span>
* <span data-ttu-id="0cb23-121">Le locataire Azure possède au moins un fournisseur d’authentification multifacteur Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb23-121">The Azure tenant has at least one Azure Multi-Factor Authentication provider.</span></span> <span data-ttu-id="0cb23-122">Pour plus d’informations, consultez la rubrique [Administration des fournisseurs Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0cb23-122">For more information, see [Administering Azure Multi-Factor Authentication Providers](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).</span></span>

<span data-ttu-id="0cb23-123">Pour créer un espace de noms de contrôle d’accès ou un fournisseur Multi-Factor Authentication, cliquez sur **+ New** > **App Services** > **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0cb23-123">To create an Access Control namespace or a Multi-Factor Authentication provider, click **+New** > **App Services** > **Active Directory**.</span></span>

<span data-ttu-id="0cb23-124">Pour obtenir des droits d’administration d’un répertoire, demandez à un administrateur d’attribuer un rôle d’administrateur à votre compte.</span><span class="sxs-lookup"><span data-stu-id="0cb23-124">To get administrative rights to a directory, have an administrator assign an administrator role to your account.</span></span> <span data-ttu-id="0cb23-125">Pour plus de détails, consultez [Attribution de rôles d’administrateur](active-directory-assign-admin-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0cb23-125">For details, see [Assigning administrator roles](active-directory-assign-admin-roles.md).</span></span>

## <a name="active-directory-is-not-available"></a><span data-ttu-id="0cb23-126">Active Directory n’est pas disponible</span><span class="sxs-lookup"><span data-stu-id="0cb23-126">Active Directory is not available</span></span>
<span data-ttu-id="0cb23-127">Lorsque vous cliquez sur **+ New** > **App Services**, un élément **Active Directory** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0cb23-127">When you click **+New** > **App Services**, an **Active Directory** item appears.</span></span> <span data-ttu-id="0cb23-128">Plus précisément, l’élément Active Directory s’affiche lorsqu’une des fonctionnalités Active Directory, comme le répertoire, le contrôle d’accès ou le fournisseur Multi-Factor Auth, est disponible pour l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="0cb23-128">Specifically, the Active Directory item appears when any of the Active Directory features, such as Directory, Access Control, or Multi-Factor Auth Provider, are available to the current user.</span></span>

<span data-ttu-id="0cb23-129">Toutefois, pendant le chargement de la page, l’élément est estompé et est marqué comme **non disponible**.</span><span class="sxs-lookup"><span data-stu-id="0cb23-129">However, while the page is loading, the item is dimmed and is marked **Not Available**.</span></span> <span data-ttu-id="0cb23-130">Il s’agit d’un état temporaire.</span><span class="sxs-lookup"><span data-stu-id="0cb23-130">This is a temporary state.</span></span> <span data-ttu-id="0cb23-131">Si vous attendez quelques secondes, l’élément devient disponible.</span><span class="sxs-lookup"><span data-stu-id="0cb23-131">If you wait a few seconds, the item becomes available.</span></span> <span data-ttu-id="0cb23-132">Si le délai se prolonge, l’actualisation de la page Web résout souvent le problème.</span><span class="sxs-lookup"><span data-stu-id="0cb23-132">If the delay is prolonged, refreshing the web page often resolves the problem.</span></span>

![Capture d’écran : Active Directory n’est pas disponible](./media/active-directory-troubleshooting/not-available.png)

