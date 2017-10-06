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
# <a name="azure-active-directory-b2c-threat-management"></a>Azure Active Directory B2C : Gestion des menaces

La gestion des menaces inclut la planification de la protection contre les attaques des systèmes et des réseaux. Attaques par déni de service peuvent mettre des ressources aux utilisateurs de toointended indisponible. Mot de passe attaques prospect toounauthorized accès tooresources. Azure Active Directory B2C (Azure AD B2C) dispose de fonctionnalités intégrées qui peuvent vous aider à protéger vos données contre ces menaces de plusieurs façons.

## <a name="denial-of-service-attacks"></a>Attaques par déni de service

Azure AD B2C utilise la détection et l’atténuation des techniques telles que les cookies SYN et les taux et connexion tooprotect limites sous-jacent ressources contre les attaques par déni de service.

## <a name="password-attacks"></a>Attaques de mot de passe

Azure AD B2C dispose également de techniques d’atténuation pour contrer les attaques de mot de passe. L’atténuation couvre à la fois les attaques de mot de passe par force brute et celles basées sur un dictionnaire. Les mots de passe qui sont définies par les utilisateurs sont requis toobe relativement complexe. À l’aide de signaux différents, Azure AD B2C analyse l’intégrité de hello de demandes. Azure AD B2C est conçu toointelligently différencier les utilisateurs prévus contre les pirates et botnets. Azure AD B2C fournit un toolock stratégie sophistiquées comptes basée sur les mots de passe hello entrés, probabilité hello d’une attaque.

Pour plus d’informations, visitez hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).
