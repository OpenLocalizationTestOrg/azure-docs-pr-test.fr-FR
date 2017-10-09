---
title: aaaAdd un tooyour utilisateur collection Azure RemoteApp | Documents Microsoft
description: "Découvrez comment les utilisateurs de tooadd tooyour collection Azure RemoteApp"
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
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="6d820-103">Comment tooadd un tooyour utilisateur collection Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6d820-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d820-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="6d820-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6d820-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6d820-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6d820-106">Vos utilisateurs peuvent voir et utiliser vos applications dans Azure RemoteApp, vous devez toogrant les accès tooyour collection.</span><span class="sxs-lookup"><span data-stu-id="6d820-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="6d820-107">Cela fait partie de facile hello : sur hello **accès utilisateur** onglet, entrez les informations du compte d’utilisateur de hello hello, puis cliquez sur la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="6d820-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="6d820-108">Quelles sont les informations de compte dont vous avez besoin ?</span><span class="sxs-lookup"><span data-stu-id="6d820-108">What account information do you need?</span></span> <span data-ttu-id="6d820-109">Cela dépend de type hello de collection vous avez créé (cloud ou hybride), et que vous utilisez Office 365 ProPlus dans cette collection.</span><span class="sxs-lookup"><span data-stu-id="6d820-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="6d820-110">Identités d'utilisateurs prises en charge</span><span class="sxs-lookup"><span data-stu-id="6d820-110">Supported user identities</span></span>
<span data-ttu-id="6d820-111">Hello différents types de collection (cloud ou hybride) prend en charge à l’aide de différentes identités d’utilisateur pour l’accès tooapplications.</span><span class="sxs-lookup"><span data-stu-id="6d820-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="6d820-112">Pour une collection hybride de RemoteApp, tooset une infrastructure de domaine Active Directory sur site et un locataire Azure Active Directory avec l’intégration Active (et éventuellement l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="6d820-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="6d820-113">En outre, vous devez toocreate certains objets Active Directory dans le répertoire local de hello.</span><span class="sxs-lookup"><span data-stu-id="6d820-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="6d820-114">Pour une collection de cloud de RemoteApp, tout utilisateur disposant d’Azure Active Directory prend en charge les identités peut être accordée utilisateur accès tooRemoteApp tooinclude Accounts Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6d820-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="6d820-115">Consultez le tableau de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6d820-115">See hello table below.</span></span>

<span data-ttu-id="6d820-116">Les utilisateurs Office 365 sont des utilisateurs Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d820-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="6d820-117">S'ils possèdent des comptes Azure Active Directory hybrides synchronisés, ils peuvent bénéficier de l'accès utilisateur dans un déploiement hybride de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6d820-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="6d820-118">Vous pouvez utiliser cette table comme une référence rapide pour lequel identity est pris en charge dans votre collection et quelles sont les exigences d’Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="6d820-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="6d820-119">Comptes d'utilisateurs</span><span class="sxs-lookup"><span data-stu-id="6d820-119">User accounts</span></span> | <span data-ttu-id="6d820-120">Cloud</span><span class="sxs-lookup"><span data-stu-id="6d820-120">Cloud</span></span> | <span data-ttu-id="6d820-121">Hybride</span><span class="sxs-lookup"><span data-stu-id="6d820-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d820-122">Compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="6d820-122">Microsoft Account</span></span> |<span data-ttu-id="6d820-123">Oui</span><span class="sxs-lookup"><span data-stu-id="6d820-123">Yes</span></span> |<span data-ttu-id="6d820-124">Non</span><span class="sxs-lookup"><span data-stu-id="6d820-124">No</span></span> |
| <span data-ttu-id="6d820-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="6d820-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="6d820-126">Cloud Azure AD uniquement</span><span class="sxs-lookup"><span data-stu-id="6d820-126">Azure AD cloud only</span></span> |<span data-ttu-id="6d820-127">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-127">Yes</span></span> |<span data-ttu-id="6d820-128">Non</span><span class="sxs-lookup"><span data-stu-id="6d820-128">No</span></span> |
| <span data-ttu-id="6d820-129">ADsync avec synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="6d820-129">ADsync with password sync</span></span> |<span data-ttu-id="6d820-130">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-130">Yes</span></span> |<span data-ttu-id="6d820-131">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-131">Yes</span></span> |
| <span data-ttu-id="6d820-132">ADsync sans synchronisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="6d820-132">ADsync without password sync</span></span> |<span data-ttu-id="6d820-133">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-133">Yes</span></span> |<span data-ttu-id="6d820-134">Non</span><span class="sxs-lookup"><span data-stu-id="6d820-134">No</span></span> |
| <span data-ttu-id="6d820-135">ADsync avec AD FS</span><span class="sxs-lookup"><span data-stu-id="6d820-135">ADsync with AD FS</span></span> |<span data-ttu-id="6d820-136">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-136">Yes</span></span> |<span data-ttu-id="6d820-137">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-137">Yes</span></span> |
| <span data-ttu-id="6d820-138">[Fournisseurs d’identités tiers pris en charge par Azure](https://msdn.microsoft.com/library/azure/jj679342.aspx) (par exemple Ping)</span><span class="sxs-lookup"><span data-stu-id="6d820-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="6d820-139">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-139">Yes</span></span> |<span data-ttu-id="6d820-140">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-140">Yes</span></span> |
| <span data-ttu-id="6d820-141">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6d820-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="6d820-142">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-142">Yes</span></span> |<span data-ttu-id="6d820-143">OUI</span><span class="sxs-lookup"><span data-stu-id="6d820-143">Yes</span></span> |

<span data-ttu-id="6d820-144">Consultez [plus d'informations](remoteapp-ad.md) sur la configuration d'Active Directory pour RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="6d820-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="6d820-145">utilisateurs d’Azure Active Directory Hello doivent provenir de locataire hello qui est associé à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d820-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="6d820-146">(Vous pouvez afficher et modifier votre abonnement sur hello **paramètres** hello portail.</span><span class="sxs-lookup"><span data-stu-id="6d820-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="6d820-147">Consultez [client Azure Active Directory de modification hello utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d’informations.)</span><span class="sxs-lookup"><span data-stu-id="6d820-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="6d820-148">Informations de compte d'utilisateur Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="6d820-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="6d820-149">Si vous utilisez une image de modèle Office 365 ProPlus hello dans votre collection de *ou* si vous avez créé une image personnalisée qui utilise Office 365, vous êtes uniquement autorisé tooadd les utilisateurs d’Azure Active Directory qui ont des abonnements Office 365 pour hello domaine par défaut de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6d820-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="6d820-150">Consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="6d820-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

