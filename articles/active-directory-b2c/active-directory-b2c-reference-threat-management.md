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
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="1dea4-103">Azure Active Directory B2C : Gestion des menaces</span><span class="sxs-lookup"><span data-stu-id="1dea4-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="1dea4-104">La gestion des menaces inclut la planification de la protection contre les attaques des systèmes et des réseaux.</span><span class="sxs-lookup"><span data-stu-id="1dea4-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="1dea4-105">Attaques par déni de service peuvent mettre des ressources aux utilisateurs de toointended indisponible.</span><span class="sxs-lookup"><span data-stu-id="1dea4-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="1dea4-106">Mot de passe attaques prospect toounauthorized accès tooresources.</span><span class="sxs-lookup"><span data-stu-id="1dea4-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="1dea4-107">Azure Active Directory B2C (Azure AD B2C) dispose de fonctionnalités intégrées qui peuvent vous aider à protéger vos données contre ces menaces de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="1dea4-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="1dea4-108">Attaques par déni de service</span><span class="sxs-lookup"><span data-stu-id="1dea4-108">Denial-of-service attacks</span></span>

<span data-ttu-id="1dea4-109">Azure AD B2C utilise la détection et l’atténuation des techniques telles que les cookies SYN et les taux et connexion tooprotect limites sous-jacent ressources contre les attaques par déni de service.</span><span class="sxs-lookup"><span data-stu-id="1dea4-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="1dea4-110">Attaques de mot de passe</span><span class="sxs-lookup"><span data-stu-id="1dea4-110">Password attacks</span></span>

<span data-ttu-id="1dea4-111">Azure AD B2C dispose également de techniques d’atténuation pour contrer les attaques de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1dea4-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="1dea4-112">L’atténuation couvre à la fois les attaques de mot de passe par force brute et celles basées sur un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="1dea4-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="1dea4-113">Les mots de passe qui sont définies par les utilisateurs sont requis toobe relativement complexe.</span><span class="sxs-lookup"><span data-stu-id="1dea4-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="1dea4-114">À l’aide de signaux différents, Azure AD B2C analyse l’intégrité de hello de demandes.</span><span class="sxs-lookup"><span data-stu-id="1dea4-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="1dea4-115">Azure AD B2C est conçu toointelligently différencier les utilisateurs prévus contre les pirates et botnets.</span><span class="sxs-lookup"><span data-stu-id="1dea4-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="1dea4-116">Azure AD B2C fournit un toolock stratégie sophistiquées comptes basée sur les mots de passe hello entrés, probabilité hello d’une attaque.</span><span class="sxs-lookup"><span data-stu-id="1dea4-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="1dea4-117">Pour plus d’informations, visitez hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="1dea4-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
