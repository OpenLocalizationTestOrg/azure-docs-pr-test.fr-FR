---
title: "Protocoles d’authentification Azure Active Directory | Microsoft Docs"
description: "Vue d’ensemble des protocoles d’authentification pris en charge par Azure Active Directory (AD)"
documentationcenter: dev-center-name
author: priyamohanram
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 7a838ae2-c24c-4304-b6c0-e77fb888e6c0
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 91416669281aa8eeef5916db008f9b0cbcbf77e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# Protocoles d’authentification d’Azure Active Directory
Azure Active Directory (Azure AD) prend en charge plusieurs protocoles d’authentification et d’autorisation parmi ceux les plus couramment utilisés. Les rubriques de cette section décrivent les protocoles pris en charge et leur implémentation dans Azure AD. Les rubriques comprennent une revue des types de revendications pris en charge, une présentation de l’utilisation des métadonnées de fédération, de la documentation de référence détaillée sur les protocoles OAuth 2.0. et SAML 2.0 et une section de dépannage.

## Articles et référence relatifs aux protocoles d’authentification
* [Informations importantes sur la substitution des clés de signature dans Azure AD](active-directory-signing-key-rollover.md) : découvrez le rythme de substitution des clés de signature d’Azure AD, les modifications que vous pouvez effectuer pour mettre la clé à jour automatiquement et une description de la mise à jour des scénarios d’application les plus courants.
* [Types de jeton et de revendication pris en charge](active-directory-token-and-claims.md) : découvrez les revendications des jetons émis par Azure AD.
* [Métadonnées de fédération](active-directory-federation-metadata.md) : découvrez comment trouver et interpréter les documents de métadonnées générés par Azure AD.
* [OAuth 2.0 dans Azure AD](active-directory-protocols-oauth-code.md) : découvrez comment implémenter OAuth 2.0 dans Azure AD.
* [OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) : découvrez comment utiliser OAuth 2.0, un protocole d’autorisation, pour l’authentification.
* [Appels de service à service avec les informations d’identification du client](active-directory-protocols-oauth-service-to-service.md) : découvrez comment utiliser les flux d’octroi d’informations d’identification du client OAuth 2.0 pour les appels de service à service.
* [Appels de service à service avec le flux Pour le compte de](active-directory-protocols-oauth-on-behalf-of.md) : découvrez comment utiliser les flux Pour le compte de OAuth 2.0 pour les appels de service à service.
* [Informations de référence sur le protocole SAML](active-directory-saml-protocol-reference.md) : découvrez les profils SAML d’authentification unique et de déconnexion unique d’Azure AD.

## Voir aussi
[Guide du développeur Azure Active Directory](active-directory-developers-guide.md)

[Utilisation d’Azure AD pour l’authentification](../../app-service-web/web-sites-authentication-authorization.md)

[Exemples de code Azure Active Directory](active-directory-code-samples.md)
