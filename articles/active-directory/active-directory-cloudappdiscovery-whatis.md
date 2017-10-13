---
title: "Détecter les applications cloud non gérées avec Cloud App Discovery dans Azure Active Directory| Microsoft Docs"
description: Fournit une vue d'ensemble de la recherche et de la gestion d'applications avec Cloud App Discovery, ainsi que des informations sur ses avantages et son fonctionnement.
services: active-directory
keywords: "détection d'applications cloud, gestion d'applications"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 35b898aa3c03aeef914a7df574ac65a22a6c7bec
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="find-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Détecter les applications cloud non gérées avec Cloud App Discovery
## <a name="summary"></a>Résumé

Cloud App Discovery est une fonctionnalité d’Azure Active Directory Premium qui vous permet de détecter les applications cloud non gérées utilisées par les membres de votre organisation. Dans les entreprises modernes, les services informatiques n’ont souvent pas connaissance de toutes les applications cloud utilisées par les membres de l’organisation pour effectuer leur travail. Il est facile de comprendre pourquoi les administrateurs s’inquiètent d’un accès non autorisé aux données d'entreprise, de possibles fuites de données et autres risques de sécurité. Négliger cet aspect peut sérieusement compliquer l’élaboration d'un plan visant à gérer ces risques de sécurité.

> [!TIP] 
> Découvrez les améliorations apportées au service Cloud App Discovery dans Azure Active Directory (Azure AD), qui sont rendues possibles par [l’intégration à Microsoft Cloud App Security](https://portal.cloudappsecurity.com).

**Avec Cloud App Discovery, vous pouvez :**

* détecter les applications cloud utilisées et mesurer l’utilisation par nombre d’utilisateurs, volume de trafic ou nombre de demandes web à l’application ;
* identifier les utilisateurs d’une application ;
* exporter des données pour effectuer une analyse hors ligne ;
* confier le contrôle de ces applications au service informatique et activer l’authentification unique pour la gestion des utilisateurs.

## <a name="how-it-works"></a>Fonctionnement
1. Des agents d'utilisation des applications sont installés sur les ordinateurs de l'utilisateur.
2. Les informations sur l’utilisation des applications capturées par les agents sont envoyées via un canal sécurisé et chiffré au service Cloud App Discovery.
3. Celui-ci évalue les données et génère des rapports.

![Diagramme Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)


## <a name="next-steps"></a>Étapes suivantes
* [Considérations relatives à la confidentialité et à la sécurité de Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Paramètres de Registre de Cloud App Discovery pour les services de proxy avec ports personnalisés](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery - Agent Changelog ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

