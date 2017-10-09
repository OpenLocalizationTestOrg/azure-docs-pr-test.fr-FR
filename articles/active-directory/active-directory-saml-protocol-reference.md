---
title: "aaaAzure référence du protocole SAML AD | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de profils de l’authentification unique et SAML de déconnexion unique hello dans Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Comment Azure Active Directory utilise le protocole SAML de hello
Azure Active Directory (Azure AD) utilise hello SAML 2.0 protocole tooenable applications tooprovide une authentification unique sur expérience tootheir les utilisateurs. Hello [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) et [déconnexion unique](active-directory-single-sign-out-protocol-reference.md) profils SAML d’Azure AD expliquent comment les assertions SAML, les protocoles et les liaisons sont utilisées dans le service de fournisseur d’identité hello.

Protocole SAML requiert le fournisseur d’identité hello (Azure AD) et hello service fournisseur (application hello) tooexchange informations les concernant.

Lorsqu’une application est inscrite auprès d’Azure AD, développeur d’application hello enregistre les informations liées à la fédération avec Azure AD. Cela inclut les hello **URI de redirection** de l’application hello.

Azure Active Directory expose les points de terminaison d’authentification unique et de déconnexion unique communs (indépendants du client) et spécifiques au client. Ces URL représente les emplacements adressables : ils ne sont pas simplement d’identificateurs--vous pouvez accéder des métadonnées de hello tooread toohello point de terminaison.

* point de terminaison Hello spécifiques du client se trouve dans `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Hello <TenantDomainName> espace réservé représente un nom de domaine inscrit ou le GUID de TenantID d’un locataire Azure AD. Par exemple, les métadonnées de fédération hello du client de contoso.com hello sont à : https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* point de terminaison Hello indépendant du client se trouve dans `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. Dans cette adresse de point de terminaison, **commune** s’affiche, au lieu d’un nom de domaine client ou le code.

Pour plus d’informations sur les documents de métadonnées de fédération hello Azure AD publie, consultez [les métadonnées de fédération](active-directory-federation-metadata.md).
