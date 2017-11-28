---
title: "Azure Multi-Factor Authentication : fonctionnement"
description: "Azure Multi-Factor Authentication contribue à sécuriser l'accès aux données et aux applications tout en répondant à la demande de l'utilisateur d'un processus d'authentification simple. Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="ffe9e-104">Azure Multi-Factor Authentication : fonctionnement</span><span class="sxs-lookup"><span data-stu-id="ffe9e-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="ffe9e-105">La sécurité de la vérification en deux étapes repose sur son approche en couche.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="ffe9e-106">Compromettre plusieurs facteurs d'authentification présente un défi de taille pour les attaquants.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="ffe9e-107">Même si un attaquant réussit à connaître le mot de passe de l'utilisateur, ce dernier est inutile sans posséder l'appareil de confiance.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Vérification](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="ffe9e-109">Azure Multi-Factor Authentication contribue à sécuriser l'accès aux données et aux applications tout en répondant à la demande de l'utilisateur d'un processus d'authentification simple.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="ffe9e-110">Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="ffe9e-111">Méthodes disponibles pour la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="ffe9e-111">Methods available for two-step verification</span></span>
<span data-ttu-id="ffe9e-112">Lorsqu'un utilisateur se connecte, une vérification supplémentaire lui est envoyée.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="ffe9e-113">Voici la liste des méthodes qui peuvent être utilisées pour cette seconde vérification.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="ffe9e-114">Méthode de vérification</span><span class="sxs-lookup"><span data-stu-id="ffe9e-114">Verification Method</span></span> | <span data-ttu-id="ffe9e-115">Description</span><span class="sxs-lookup"><span data-stu-id="ffe9e-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ffe9e-116">appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="ffe9e-116">Phone call</span></span> |<span data-ttu-id="ffe9e-117">Un appel est passé au numéro de téléphone enregistré d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="ffe9e-118">L’utilisateur entre un code PIN si nécessaire, puis appuie sur la touche #.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="ffe9e-119">SMS</span><span class="sxs-lookup"><span data-stu-id="ffe9e-119">Text message</span></span> |<span data-ttu-id="ffe9e-120">Un SMS est envoyé sur le téléphone mobile de l’utilisateur avec un code à six chiffres.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="ffe9e-121">L’utilisateur entre ce code sur la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="ffe9e-122">Notification sur l’application mobile</span><span class="sxs-lookup"><span data-stu-id="ffe9e-122">Mobile app notification</span></span> |<span data-ttu-id="ffe9e-123">Une demande de vérification est envoyée au smartphone d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="ffe9e-124">L’utilisateur entre un code PIN si nécessaire, puis sélectionne **Vérifier** sur l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="ffe9e-125">Code de vérification de l’application mobile</span><span class="sxs-lookup"><span data-stu-id="ffe9e-125">Mobile app verification code</span></span> |<span data-ttu-id="ffe9e-126">L’application mobile, qui est exécutée sur le smartphone d’un utilisateur, affiche un code de vérification qui change toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="ffe9e-127">L’utilisateur trouve le code le plus récent et le saisit sur la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="ffe9e-128">Jetons OATH tiers</span><span class="sxs-lookup"><span data-stu-id="ffe9e-128">Third-party OATH tokens</span></span> | <span data-ttu-id="ffe9e-129">Le serveur Azure Multi-Factor Authentication peut être configuré pour accepter les méthodes de vérification tierces.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="ffe9e-130">Azure Multi-Factor Authentication fournit des méthodes de vérification sélectionnables pour cloud et pour serveur.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="ffe9e-131">Vous pouvez choisir les méthodes mises à la disposition de vos utilisateurs : appel téléphonique, SMS, notification sur l’application ou codes d’application.</span><span class="sxs-lookup"><span data-stu-id="ffe9e-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="ffe9e-132">Pour plus d’informations, consultez [Méthodes de vérification sélectionnables](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="ffe9e-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffe9e-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ffe9e-133">Next steps</span></span>

- <span data-ttu-id="ffe9e-134">En savoir plus sur les différentes [versions et méthodes de consommation pour Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="ffe9e-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="ffe9e-135">Choisissez de déployer Azure MFA [dans le cloud ou en local](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="ffe9e-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="ffe9e-136">Obtenez des réponses aux [questions fréquemment posées](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ffe9e-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>