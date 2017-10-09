---
title: "aaaLearn sur la vérification en deux étapes dans l’authentification Multifacteur Azure | Documents Microsoft"
description: "Quelle est l’authentification multifacteur Azure, pourquoi utiliser l’authentification Multifacteur, plus d’informations sur le client de l’authentification multifacteur hello et les différentes méthodes de hello et les versions disponibles. "
keywords: "Introduction tooMFA, vue d’ensemble de l’authentification multifacteur, quelle est l’authentification multifacteur"
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
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="9e663-104">Présentation d'Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9e663-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="9e663-105">Vérification en deux étapes est une méthode d’authentification qui nécessite plus d’une méthode de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions.</span><span class="sxs-lookup"><span data-stu-id="9e663-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="9e663-106">Elle fonctionne avec deux ou plusieurs de hello les méthodes de vérification suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e663-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="9e663-107">Un élément que vous connaissez (généralement un mot de passe)</span><span class="sxs-lookup"><span data-stu-id="9e663-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="9e663-108">Un élément que vous possédez (un appareil de confiance qui n'est pas facilement dupliqué, comme un téléphone)</span><span class="sxs-lookup"><span data-stu-id="9e663-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="9e663-109">Un élément vous concernant particulièrement (biométrie)</span><span class="sxs-lookup"><span data-stu-id="9e663-109">Something you are (biometrics)</span></span>

<span data-ttu-id="9e663-110"><center>![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/pword.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificats](./media/multi-factor-authentication/phone.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce](./media/multi-factor-authentication/smart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce virtuelle](./media/multi-factor-authentication/vsmart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="9e663-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="9e663-111">Azure Multi-Factor Authentication (MFA) est la solution de vérification en deux étapes de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9e663-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="9e663-112">Azure MFA permet toodata d’accès de sauvegarde et d’applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.</span><span class="sxs-lookup"><span data-stu-id="9e663-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="9e663-113">Il fournit une authentification forte au moyen de diverses méthodes de vérification, notamment les appels téléphoniques, l’envoi de SMS ou la vérification sur l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="9e663-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="9e663-114">Pourquoi utiliser Azure Multi-Factor Authentication ?</span><span class="sxs-lookup"><span data-stu-id="9e663-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="9e663-115">Aujourd’hui, plus que jamais, les personnes sont de plus en plus connectées.</span><span class="sxs-lookup"><span data-stu-id="9e663-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="9e663-116">Avec les Smartphones, tablettes, ordinateurs portables et PC, personnes ont plusieurs options sur comment ils vont tooconnect et restent connectés à tout moment.</span><span class="sxs-lookup"><span data-stu-id="9e663-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="9e663-117">Ils peuvent accéder à leurs comptes et leurs applications où qu’ils soient, cela signifie qu’ils peuvent être plus productifs et mieux servir leurs clients.</span><span class="sxs-lookup"><span data-stu-id="9e663-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="9e663-118">L’authentification multifacteur Azure est un toouse facile, évolutive, et une solution fiable qui fournit une deuxième méthode d’authentification pour vos utilisateurs sont toujours protégés.</span><span class="sxs-lookup"><span data-stu-id="9e663-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![TooUse simple](./media/multi-factor-authentication/simple.png) | ![Évolutif](./media/multi-factor-authentication/scalable.png) | ![Toujours protégé](./media/multi-factor-authentication/protected.png) | ![Fiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="9e663-123">**Toouse simple**</span><span class="sxs-lookup"><span data-stu-id="9e663-123">**Easy toouse**</span></span> |<span data-ttu-id="9e663-124">**Évolutif**</span><span class="sxs-lookup"><span data-stu-id="9e663-124">**Scalable**</span></span> |<span data-ttu-id="9e663-125">**Toujours protégé**</span><span class="sxs-lookup"><span data-stu-id="9e663-125">**Always Protected**</span></span> |<span data-ttu-id="9e663-126">**Fiable**</span><span class="sxs-lookup"><span data-stu-id="9e663-126">**Reliable**</span></span> |

* <span data-ttu-id="9e663-127">**TooUse facile** -Azure multi-Factor Authentication est simple tooset des et utilisation.</span><span class="sxs-lookup"><span data-stu-id="9e663-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="9e663-128">Hello une protection supplémentaire qui est fourni avec l’authentification multifacteur Azure permet aux utilisateurs toomanage leurs propres appareils.</span><span class="sxs-lookup"><span data-stu-id="9e663-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="9e663-129">De plus, dans de nombreux cas elle peut être configurée de manière très simple.</span><span class="sxs-lookup"><span data-stu-id="9e663-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="9e663-130">**Évolutive** -Azure multi-Factor Authentication utilise l’alimentation hello du cloud de hello et s’intègre à votre site AD et les applications personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9e663-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="9e663-131">Cette protection est étendue même tooyour des scénarios critiques, de haut volume.</span><span class="sxs-lookup"><span data-stu-id="9e663-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="9e663-132">**Toujours protégé** -Azure multi-Factor Authentication fournit une authentification forte à l’aide de normes du secteur hello la plus élevées.</span><span class="sxs-lookup"><span data-stu-id="9e663-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="9e663-133">**Fiable** : nous garantissons une disponibilité à 99,9 % d'Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="9e663-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="9e663-134">Hello service est considérée comme non disponible lorsqu’il est impossible de demandes de vérification tooreceive ou processus pour la vérification en deux étapes hello.</span><span class="sxs-lookup"><span data-stu-id="9e663-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="9e663-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e663-135">Next steps</span></span>

- <span data-ttu-id="9e663-136">En savoir plus sur le [fonctionnement d’Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="9e663-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="9e663-137">En savoir plus sur hello différents [versions et les méthodes de consommation pour l’authentification multifacteur Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="9e663-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
