---
title: "Vérification en deux étapes dans Azure MFA | Microsoft Docs"
description: "En quoi consiste Azure Multi-Factor Authentication (MFA), pourquoi l’utiliser, informations sur le client MFA, différentes méthodes et versions disponibles. "
keywords: "introduction à l'authentification multifacteur, vue d'ensemble de l'authentification multifacteur, définition de l'authentification multifacteur"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="92a17-104">Présentation d'Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="92a17-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="92a17-105">La vérification en deux étapes est une méthode d’authentification qui nécessite plusieurs méthodes de vérification et ajoute une deuxième couche critique de sécurité aux connexions et transactions des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="92a17-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="92a17-106">Cette authentification fonctionne en nécessitant au minimum deux des méthodes de vérification suivantes :</span><span class="sxs-lookup"><span data-stu-id="92a17-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="92a17-107">Un élément que vous connaissez (généralement un mot de passe)</span><span class="sxs-lookup"><span data-stu-id="92a17-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="92a17-108">Un élément que vous possédez (un appareil de confiance qui n'est pas facilement dupliqué, comme un téléphone)</span><span class="sxs-lookup"><span data-stu-id="92a17-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="92a17-109">Un élément vous concernant particulièrement (biométrie)</span><span class="sxs-lookup"><span data-stu-id="92a17-109">Something you are (biometrics)</span></span>

<span data-ttu-id="92a17-110"><center>![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificats](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce virtuelle](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="92a17-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="92a17-111">Azure Multi-Factor Authentication (MFA) est la solution de vérification en deux étapes de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92a17-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="92a17-112">Azure MFA contribue à sécuriser l’accès aux données et aux applications tout en répondant à la demande des utilisateurs souhaitant un processus d’authentification simple.</span><span class="sxs-lookup"><span data-stu-id="92a17-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="92a17-113">Il fournit une authentification forte au moyen de diverses méthodes de vérification, notamment les appels téléphoniques, l’envoi de SMS ou la vérification sur l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="92a17-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="92a17-114">Pourquoi utiliser Azure Multi-Factor Authentication ?</span><span class="sxs-lookup"><span data-stu-id="92a17-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="92a17-115">Aujourd’hui, plus que jamais, les personnes sont de plus en plus connectées.</span><span class="sxs-lookup"><span data-stu-id="92a17-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="92a17-116">Avec les smartphones, les tablettes, les PC portables et les PC de bureau, les utilisateurs ont plusieurs options différentes pour se connecter et rester connecté à tout moment.</span><span class="sxs-lookup"><span data-stu-id="92a17-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="92a17-117">Ils peuvent accéder à leurs comptes et leurs applications où qu’ils soient, cela signifie qu’ils peuvent être plus productifs et mieux servir leurs clients.</span><span class="sxs-lookup"><span data-stu-id="92a17-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="92a17-118">Azure Multi-Factor Authentication est une solution facile à utiliser, évolutive et fiable qui fournit une deuxième méthode d'authentification pour que vos utilisateurs soient toujours protégés.</span><span class="sxs-lookup"><span data-stu-id="92a17-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Facile à utiliser](./media/multi-factor-authentication/simple.png) | ![Évolutif](./media/multi-factor-authentication/scalable.png) | ![Toujours protégé](./media/multi-factor-authentication/protected.png) | ![Fiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="92a17-123">**Facile à utiliser**</span><span class="sxs-lookup"><span data-stu-id="92a17-123">**Easy to use**</span></span> |<span data-ttu-id="92a17-124">**Évolutif**</span><span class="sxs-lookup"><span data-stu-id="92a17-124">**Scalable**</span></span> |<span data-ttu-id="92a17-125">**Toujours protégé**</span><span class="sxs-lookup"><span data-stu-id="92a17-125">**Always Protected**</span></span> |<span data-ttu-id="92a17-126">**Fiable**</span><span class="sxs-lookup"><span data-stu-id="92a17-126">**Reliable**</span></span> |

* <span data-ttu-id="92a17-127">**Facile à utiliser** : Azure Multi-Factor Authentication est simple à configurer et utiliser.</span><span class="sxs-lookup"><span data-stu-id="92a17-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="92a17-128">La protection supplémentaire fournie par Azure Multi-Factor Authentication permet aux utilisateurs de gérer leurs propres appareils.</span><span class="sxs-lookup"><span data-stu-id="92a17-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="92a17-129">De plus, dans de nombreux cas elle peut être configurée de manière très simple.</span><span class="sxs-lookup"><span data-stu-id="92a17-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="92a17-130">**Évolutif** : Azure Multi-Factor Authentication utilise la puissance du cloud et s’intègre à votre site Active Directory local et à vos applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="92a17-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="92a17-131">Cette protection est même étendue à vos scénarios à mission critique volumineux.</span><span class="sxs-lookup"><span data-stu-id="92a17-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="92a17-132">**Toujours protégé** : Azure Multi-Factor Authentication fournit une authentification forte qui utilise les normes les plus strictes du secteur.</span><span class="sxs-lookup"><span data-stu-id="92a17-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="92a17-133">**Fiable** : nous garantissons une disponibilité à 99,9 % d'Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="92a17-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="92a17-134">Le service est considéré comme non disponible quand il ne parvient pas à recevoir ou traiter des demandes de vérification pour la vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="92a17-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="92a17-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92a17-135">Next steps</span></span>

- <span data-ttu-id="92a17-136">En savoir plus sur le [fonctionnement d’Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="92a17-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="92a17-137">En savoir plus sur les différentes [versions et méthodes de consommation pour Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="92a17-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
