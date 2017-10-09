---
title: aaaAzure multi-Factor Authentication - son fonctionnement
description: "L’authentification multifacteur Azure permet de toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="63773-104">Azure Multi-Factor Authentication : fonctionnement</span><span class="sxs-lookup"><span data-stu-id="63773-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="63773-105">sécurité de Hello de vérification en deux étapes réside dans son approche en couches.</span><span class="sxs-lookup"><span data-stu-id="63773-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="63773-106">Compromettre plusieurs facteurs d'authentification présente un défi de taille pour les attaquants.</span><span class="sxs-lookup"><span data-stu-id="63773-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="63773-107">Même si une personne malveillante parvient toolearn hello mot de passe utilisateur, il est inutile sans également en sa possession de l’appareil de confiance hello.</span><span class="sxs-lookup"><span data-stu-id="63773-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Vérification](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="63773-109">L’authentification multifacteur Azure permet de toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.</span><span class="sxs-lookup"><span data-stu-id="63773-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="63773-110">Il fournit une sécurité supplémentaire en exigeant un deuxième formulaire d'authentification et fournit une authentification renforcée via un éventail d'options de vérification simples.</span><span class="sxs-lookup"><span data-stu-id="63773-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="63773-111">Méthodes disponibles pour la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="63773-111">Methods available for two-step verification</span></span>
<span data-ttu-id="63773-112">Lorsqu’un utilisateur se connecte, une vérification supplémentaire est envoyée toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="63773-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="63773-113">Hello Voici une liste des méthodes qui peut être utilisé pour cette vérification du second.</span><span class="sxs-lookup"><span data-stu-id="63773-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="63773-114">Méthode de vérification</span><span class="sxs-lookup"><span data-stu-id="63773-114">Verification Method</span></span> | <span data-ttu-id="63773-115">Description</span><span class="sxs-lookup"><span data-stu-id="63773-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63773-116">appel téléphonique</span><span class="sxs-lookup"><span data-stu-id="63773-116">Phone call</span></span> |<span data-ttu-id="63773-117">Un appel est passé de téléphone enregistré de l’utilisateur tooa.</span><span class="sxs-lookup"><span data-stu-id="63773-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="63773-118">utilisateur de Hello entre un code PIN si nécessaire, puis appuie sur la touche # de hello.</span><span class="sxs-lookup"><span data-stu-id="63773-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="63773-119">SMS</span><span class="sxs-lookup"><span data-stu-id="63773-119">Text message</span></span> |<span data-ttu-id="63773-120">Un message texte est envoyé de téléphone mobile de l’utilisateur tooa avec un code à six chiffres.</span><span class="sxs-lookup"><span data-stu-id="63773-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="63773-121">utilisateur de Hello entre ce code sur la page de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="63773-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="63773-122">Notification sur l’application mobile</span><span class="sxs-lookup"><span data-stu-id="63773-122">Mobile app notification</span></span> |<span data-ttu-id="63773-123">Une demande de vérification est envoyée Smartphone tooa de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="63773-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="63773-124">Hello utilisateur entre un code PIN si nécessaire, puis sélectionne **Vérifiez** sur l’application mobile hello.</span><span class="sxs-lookup"><span data-stu-id="63773-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="63773-125">Code de vérification de l’application mobile</span><span class="sxs-lookup"><span data-stu-id="63773-125">Mobile app verification code</span></span> |<span data-ttu-id="63773-126">application mobile Hello, qui s’exécute sur un Smartphone d’un utilisateur, affiche un code de vérification que les modifications apportées à toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="63773-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="63773-127">utilisateur de Hello recherche le code le plus récent hello et l’insère dans la page de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="63773-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="63773-128">Jetons OATH tiers</span><span class="sxs-lookup"><span data-stu-id="63773-128">Third-party OATH tokens</span></span> | <span data-ttu-id="63773-129">Serveur Azure multi-Factor peuvent être des méthodes de vérification de l’application tierce de tooaccept configuré.</span><span class="sxs-lookup"><span data-stu-id="63773-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="63773-130">Azure Multi-Factor Authentication fournit des méthodes de vérification sélectionnables pour cloud et pour serveur.</span><span class="sxs-lookup"><span data-stu-id="63773-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="63773-131">Vous pouvez choisir les méthodes mises à la disposition de vos utilisateurs : appel téléphonique, SMS, notification sur l’application ou codes d’application.</span><span class="sxs-lookup"><span data-stu-id="63773-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="63773-132">Pour plus d’informations, consultez [Méthodes de vérification sélectionnables](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="63773-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63773-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63773-133">Next steps</span></span>

- <span data-ttu-id="63773-134">En savoir plus sur hello différents [versions et les méthodes de consommation pour l’authentification multifacteur Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="63773-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="63773-135">Choisissez si toodeploy Azure MFA [dans hello ou local](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="63773-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="63773-136">Obtenez des réponses aux [questions fréquemment posées](multi-factor-authentication-faq.md).</span><span class="sxs-lookup"><span data-stu-id="63773-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>