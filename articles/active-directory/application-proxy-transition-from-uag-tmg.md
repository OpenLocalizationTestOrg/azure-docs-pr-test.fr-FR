---
title: "aaaUpgrade tooAzure AD Proxy d’Application | Documents Microsoft"
description: "Choisissez la meilleure solution de proxy si vous effectuez une mise à niveau à partir de Microsoft Forefront ou de Unified Access Gateway."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>Comparer les solutions d’accès à distance

Le proxy d’application Azure Active Directory est l’une des deux solutions d’accès à distance proposées par Microsoft. Hello autres est la version locale de hello, Proxy d’Application Web. Ces deux solutions remplacent d’anciens produits proposés par Microsoft : Microsoft Forefront Threat Management Gateway (TMG) et Unified Access Gateway (UAG). Utilisez cette toounderstand article comment ces quatre solutions comparer tooeach autres. Pour ceux qui utilisent toujours les hello déconseillée solutions TMG ou UAG, vous pouvez utiliser ce plan de toohelp d’article votre tooone de migration de hello Proxy d’Application. 


## <a name="feature-comparison"></a>Comparaison des fonctionnalités

Utilisez cette toounderstand table Threat Management Gateway (TMG), Unified Access Gateway (UAG), Web Application Proxy (WAP) et Azure AD Application Proxy (PA) les différences tooeach autres.

| Fonctionnalité | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| Authentification par certificat | Oui | Oui | - | - |
| Publier de manière sélective les applications de navigateur | Oui | Oui | Oui | Oui |
| Préauthentification et authentification unique | Oui | Oui | Oui | Oui | 
| Pare-feu de couche 2/3 | Oui | Oui | - | - |
| Transférer des fonctionnalités de proxy | Oui | - | - | - |
| Fonctionnalités VPN | Oui | Oui | - | - |
| Prise en charge du protocole riche | - | Oui | Oui, en cas d’exécution sur HTTP | Oui, en cas d’exécution sur HTTP ou via la passerelle des services Bureau à distance |
| Sert de serveur proxy AD FS | - | Oui | Oui | - |
| Un portail pour l’accès de l’application | - | Oui | - | Oui |
| Traduction du lien de corps de réponse | Oui | Oui | - | Oui | 
| Authentification avec des en-têtes | - | Oui | - | Oui, avec PingAccess | 
| Sécurité à l’échelle du cloud | - | - | - | Oui | 
| Accès conditionnel | - | Oui | - | Oui |
| Aucun composant de hello de zone démilitarisée (DMZ) | - | - | - | Oui |
| Aucune connexion entrante | - | - | - | Oui |

La plupart des scénarios, nous vous recommandons d’aucune Application Azure AD en tant que solution de moderne hello. Le proxy d’application Web est uniquement recommandé dans les scénarios qui requièrent un serveur proxy pour AD FS, et que vous ne pouvez pas utiliser de domaines personnalisés dans Azure Active Directory. 

Proxy d’Application Azure AD offre des avantages uniques, lorsque comparées toosimilar produits, notamment :

- Étendre les ressources Azure AD local tooon
   - La protection et la sécurité à l’échelle du cloud
   - Fonctionnalités telles que les conditions d’accès et l’authentification multifacteur sont tooenable facile
- Aucun composant dans la zone démilitarisée de hello
- Aucune connexion entrante nécessaire
- Panneau d’un accès que vos utilisateurs peuvent accéder à toofor toutes leurs applications, y compris Office 365, Azure AD intégré applications SaaS et applications de votre site web. 


## <a name="next-steps"></a>Étapes suivantes

- [Utiliser des applications de site tooon Application Azure AD tooprovide sécuriser l’accès à distance](active-directory-application-proxy-get-started.md)
- [Transition de Forefront TMG et UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).
