---
title: "aaaFinding non managée à des applications de cloud avec Cloud App Discovery | Documents Microsoft"
description: Fournit des informations sur la recherche et la gestion des applications avec Cloud App Discovery, quels sont les avantages de hello et son fonctionnement.
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
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Détection des applications cloud non gérées avec Cloud App Discovery
## <a name="overview"></a>Vue d'ensemble
Dans les entreprises modernes, les services informatiques sont souvent pas conscients de toutes les applications de cloud hello que les membres de leur organisation utilisent toodo leur travail. Il est facile toosee pourquoi administrateurs auront des problèmes sur les données toocorporate de tout accès non autorisé, les fuites de données possibles et les autres risques de sécurité. Négliger cet aspect peut sérieusement compliquer l’élaboration d'un plan visant à gérer ces risques de sécurité.

Cloud App Discovery est une fonctionnalité Premium d’Azure Active Directory (AD) qui permet à vos applications de cloud toodiscover utilisées par les personnes hello dans votre organisation.

**Avec Cloud App Discovery, vous pouvez :**

* Recherche des applications de cloud hello utilisées et que l’utilisation de mesures par nombre d’utilisateurs, le volume de trafic ou du nombre d’applications de toohello de demandes web.
* Identifiez les utilisateurs hello qui utilisent une application.
* exporter des données pour effectuer une analyse hors ligne ;
* confier le contrôle de ces applications au service informatique et activer l'authentification unique pour la gestion des utilisateurs.

## <a name="how-it-works"></a>Fonctionnement
1. Des agents d'utilisation des applications sont installés sur les ordinateurs de l'utilisateur.
2. informations d’utilisation application Hello capturées par les agents hello sont envoyées via un canal sécurisé, chiffré toohello cloud découverte du service d’applications.
3. Hello service Cloud App Discovery évalue les données hello et génère des rapports.

![Diagramme Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

tooget démarrer avec Cloud App Discovery, consultez [mise en route a démarré avec Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Articles connexes
* [Considérations relatives à la confidentialité et à la sécurité de Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Guide de déploiement d’une stratégie de groupe Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Guide de déploiement de Cloud App Discovery System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Paramètres de Registre de Cloud App Discovery pour les services de proxy avec ports personnalisés](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery - Agent Changelog ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Cloud App Discovery - Forum aux Questions](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

