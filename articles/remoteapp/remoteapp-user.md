---
title: "Ajouter un utilisateur à votre collection Azure RemoteApp | Microsoft Docs"
description: "Découvrez comment ajouter des utilisateurs dans votre collection Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 281e74c7941c42d8a3e4351953391229e54ce0a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-a-user-to-your-azure-remoteapp-collection"></a><span data-ttu-id="e6daf-103">Procédure : ajout d'un utilisateur dans votre collection Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e6daf-103">How to add a user to your Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e6daf-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="e6daf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e6daf-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="e6daf-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e6daf-106">Avant que vos utilisateurs puissent afficher et utiliser vos applications dans Azure RemoteApp, vous devez leur accorder l’accès à votre collection.</span><span class="sxs-lookup"><span data-stu-id="e6daf-106">Before your users can see and use your apps in Azure RemoteApp, you have to grant them access to your collection.</span></span> <span data-ttu-id="e6daf-107">C'est l'étape la plus facile : sous l'onglet **Accès utilisateur** , entrez les informations de compte de l'utilisateur, puis cliquez sur la coche.</span><span class="sxs-lookup"><span data-stu-id="e6daf-107">This is the easy part: On the **User Access** tab, enter the account information for the user, and then click the check mark.</span></span>

<span data-ttu-id="e6daf-108">Quelles sont les informations de compte dont vous avez besoin ?</span><span class="sxs-lookup"><span data-stu-id="e6daf-108">What account information do you need?</span></span> <span data-ttu-id="e6daf-109">Cela dépend du type de collection que vous avez créé (cloud ou hybride) et si vous utilisez Office 365 ProPlus dans cette collection.</span><span class="sxs-lookup"><span data-stu-id="e6daf-109">That depends on the type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="e6daf-110">Identités d'utilisateurs prises en charge</span><span class="sxs-lookup"><span data-stu-id="e6daf-110">Supported user identities</span></span>
<span data-ttu-id="e6daf-111">Les différents types de collection (cloud ou hybride) prennent en charge différentes identités d’utilisateur pour l’accès aux applications.</span><span class="sxs-lookup"><span data-stu-id="e6daf-111">The different collection types (cloud vs. hybrid) support using different user identities for access to applications.</span></span>  

<span data-ttu-id="e6daf-112">Pour une collection hybride de RemoteApp, vous devez configurer une infrastructure de domaine Active Directory locale et un locataire Azure Active Directory avec intégration d'annuaire (et éventuellement l'authentification unique).</span><span class="sxs-lookup"><span data-stu-id="e6daf-112">For a hybrid collection of RemoteApp, you need to set up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="e6daf-113">Par ailleurs, vous devez créer des objets Active Directory dans l'annuaire local.</span><span class="sxs-lookup"><span data-stu-id="e6daf-113">Additionally, you need to create some Active Directory objects in the on-premises directory.</span></span>  

<span data-ttu-id="e6daf-114">Pour une collection cloud de RemoteApp, tout utilisateur prenant en charge les identités Azure Active Directory peut recevoir l'accès utilisateur à RemoteApp pour inclure des comptes Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e6daf-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access to RemoteApp to include Microsoft Accounts.</span></span>  <span data-ttu-id="e6daf-115">Consultez le tableau ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e6daf-115">See the table below.</span></span>

<span data-ttu-id="e6daf-116">Les utilisateurs Office 365 sont des utilisateurs Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e6daf-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="e6daf-117">S'ils possèdent des comptes Azure Active Directory hybrides synchronisés, ils peuvent bénéficier de l'accès utilisateur dans un déploiement hybride de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e6daf-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="e6daf-118">Vous pouvez utiliser ce tableau de référence pour déterminer rapidement quelle identité est prise en charge dans votre collection et quelle configuration est requise pour Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e6daf-118">You can use this table as a quick reference for which identity is supported in your collection and what the Active Directory requirements are.</span></span>

| <span data-ttu-id="e6daf-119">Comptes d'utilisateurs</span><span class="sxs-lookup"><span data-stu-id="e6daf-119">User accounts</span></span> | <span data-ttu-id="e6daf-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="e6daf-120">Cloud</span></span> | <span data-ttu-id="e6daf-121">Hybride</span><span class="sxs-lookup"><span data-stu-id="e6daf-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6daf-122">Compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="e6daf-122">Microsoft Account</span></span> |<span data-ttu-id="e6daf-123">Oui</span><span class="sxs-lookup"><span data-stu-id="e6daf-123">Yes</span></span> |<span data-ttu-id="e6daf-124">Non</span><span class="sxs-lookup"><span data-stu-id="e6daf-124">No</span></span> |
| <span data-ttu-id="e6daf-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="e6daf-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="e6daf-126">Cloud Azure AD uniquement</span><span class="sxs-lookup"><span data-stu-id="e6daf-126">Azure AD cloud only</span></span> |<span data-ttu-id="e6daf-127">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-127">Yes</span></span> |<span data-ttu-id="e6daf-128">Non</span><span class="sxs-lookup"><span data-stu-id="e6daf-128">No</span></span> |
| <span data-ttu-id="e6daf-129">ADsync avec synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="e6daf-129">ADsync with password sync</span></span> |<span data-ttu-id="e6daf-130">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-130">Yes</span></span> |<span data-ttu-id="e6daf-131">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-131">Yes</span></span> |
| <span data-ttu-id="e6daf-132">ADsync sans synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="e6daf-132">ADsync without password sync</span></span> |<span data-ttu-id="e6daf-133">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-133">Yes</span></span> |<span data-ttu-id="e6daf-134">Non</span><span class="sxs-lookup"><span data-stu-id="e6daf-134">No</span></span> |
| <span data-ttu-id="e6daf-135">ADsync avec AD FS</span><span class="sxs-lookup"><span data-stu-id="e6daf-135">ADsync with AD FS</span></span> |<span data-ttu-id="e6daf-136">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-136">Yes</span></span> |<span data-ttu-id="e6daf-137">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-137">Yes</span></span> |
| <span data-ttu-id="e6daf-138">[Fournisseurs d’identités tiers pris en charge par Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (par exemple Ping)</span><span class="sxs-lookup"><span data-stu-id="e6daf-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="e6daf-139">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-139">Yes</span></span> |<span data-ttu-id="e6daf-140">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-140">Yes</span></span> |
| <span data-ttu-id="e6daf-141">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e6daf-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="e6daf-142">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-142">Yes</span></span> |<span data-ttu-id="e6daf-143">OUI</span><span class="sxs-lookup"><span data-stu-id="e6daf-143">Yes</span></span> |

<span data-ttu-id="e6daf-144">Consultez [plus d'informations](remoteapp-ad.md) sur la configuration d'Active Directory pour RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e6daf-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="e6daf-145">Les utilisateurs Azure Active Directory doivent provenir du locataire associé à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e6daf-145">The Azure Active Directory users must be from the tenant that's associated with your subscription.</span></span> <span data-ttu-id="e6daf-146">(Vous pouvez afficher et modifier votre abonnement sous l’onglet **Paramètres** du portail.</span><span class="sxs-lookup"><span data-stu-id="e6daf-146">(You can view and modify your subscription on the **Settings** tab in the portal.</span></span> <span data-ttu-id="e6daf-147">Consultez [Modifier le locataire Azure Active Directory utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d'informations.)</span><span class="sxs-lookup"><span data-stu-id="e6daf-147">See [Change the Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="e6daf-148">Informations de compte d'utilisateur Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="e6daf-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="e6daf-149">Si vous utilisez l’image de modèle Office 365 ProPlus dans votre collection *ou* si vous avez créé une image personnalisée qui utilise Office 365, vous êtes uniquement autorisé à ajouter des utilisateurs Azure Active Directory disposant d’abonnements Office 365 pour le domaine par défaut de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e6daf-149">If you are using the Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed to add Azure Active Directory users that have Office 365 subscriptions for the default domain of your subscription.</span></span> <span data-ttu-id="e6daf-150">Consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="e6daf-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

