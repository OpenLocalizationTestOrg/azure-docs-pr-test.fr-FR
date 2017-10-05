---
title: "Azure Active Directory B2C : Gestion des menaces | Microsoft Docs"
description: "Découvrez les techniques de détection et de prévention d’attaques par déni de service et d’attaques de mot de passe dans Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="a8395-103">Azure Active Directory B2C : Gestion des menaces</span><span class="sxs-lookup"><span data-stu-id="a8395-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="a8395-104">La gestion des menaces inclut la planification de la protection contre les attaques des systèmes et des réseaux.</span><span class="sxs-lookup"><span data-stu-id="a8395-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="a8395-105">Les attaques par déni de service peuvent rendre les ressources inaccessibles aux utilisateurs prévus.</span><span class="sxs-lookup"><span data-stu-id="a8395-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="a8395-106">Une attaque de mot de passe peut mener à un accès non autorisé aux ressources.</span><span class="sxs-lookup"><span data-stu-id="a8395-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="a8395-107">Azure Active Directory B2C (Azure AD B2C) dispose de fonctionnalités intégrées qui peuvent vous aider à protéger vos données contre ces menaces de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="a8395-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="a8395-108">Attaques par déni de service</span><span class="sxs-lookup"><span data-stu-id="a8395-108">Denial-of-service attacks</span></span>

<span data-ttu-id="a8395-109">Azure AD B2C utilise des techniques de détection et d’atténuation telles que les cookies SYN ainsi que les limites de débit et de connexion pour protéger les ressources sous-jacentes contre les attaques par déni de service.</span><span class="sxs-lookup"><span data-stu-id="a8395-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="a8395-110">Attaques de mot de passe</span><span class="sxs-lookup"><span data-stu-id="a8395-110">Password attacks</span></span>

<span data-ttu-id="a8395-111">Azure AD B2C dispose également de techniques d’atténuation pour contrer les attaques de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a8395-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="a8395-112">L’atténuation couvre à la fois les attaques de mot de passe par force brute et celles basées sur un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="a8395-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="a8395-113">Les mots de passe définis par les utilisateurs doivent être d’une complexité raisonnable.</span><span class="sxs-lookup"><span data-stu-id="a8395-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="a8395-114">À l’aide de différents signaux, Azure AD B2C analyse l’intégrité des demandes.</span><span class="sxs-lookup"><span data-stu-id="a8395-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="a8395-115">Azure AD B2C est conçu pour différencier intelligemment les utilisateurs prévus des pirates et botnets.</span><span class="sxs-lookup"><span data-stu-id="a8395-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="a8395-116">Azure AD B2C fournit une stratégie sophistiquée pour verrouiller les comptes en fonction des mots de passe entrés, dans l’éventualité d’une attaque.</span><span class="sxs-lookup"><span data-stu-id="a8395-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="a8395-117">Pour plus d’informations, consultez le [Centre de gestion de la confidentialité de Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="a8395-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
