---
title: "aaaSecuring PaaS web et des applications mobiles à l’aide des Services d’application Azure | Documents Microsoft"
description: " Découvrez les bonnes pratiques en matière de sécurité d’Azure App Services pour protéger vos applications mobiles et web PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Sécurisation des applications mobiles et web PaaS à l’aide d’Azure App Services

Dans cet article, nous abordons un ensemble de bonnes pratiques de sécurité [Azure App Services](https://azure.microsoft.com/services/app-service/) pour protéger vos applications mobiles et web PaaS. Ces recommandations sont dérivées de notre expérience avec Azure et les expériences hello de clients comme vous-même.

## <a name="azure-app-services"></a>Azure App Services
[Services d’application Azure](../app-service/app-service-value-prop-what-is.md) est une offre de PaaS qui vous permet de créer des applications web et mobiles pour chaque plate-forme ou périphérique et connecter toodata n’importe où, dans le cloud de hello ou localement. Inclut des Services d’application web de hello et de capacités qui ont été précédemment remises séparément en tant que sites Web Azure et Azure Mobile Services. Il inclut également de nouvelles fonctionnalités d’automatisation des processus d’entreprise et d’hébergement d’API cloud. Comme un service intégré, Services d’application met un riche ensemble de capacités scénarios tooweb, mobile et l’intégration.

toolearn, voir vue d’ensemble sur [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) et [Web Apps](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Meilleures pratiques

Quand vous utilisez App Services, appliquez les bonnes pratiques suivantes :

- [S’authentifier par le biais d’Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). App Services fournit un service OAuth 2.0 pour votre fournisseur d’identité. OAuth 2.0 privilégie la simplicité du développement client tout en fournissant des flux d’autorisation spécifiques pour les applications web, les applications de bureau et les téléphones mobiles. Azure AD utilise OAuth 2.0 tooenable vous tooauthorize accès toomobile et les applications web.
- Restreindre l’accès en fonction de hello besoin tooknow et les principes de sécurité de privilège minimum. Il est impératif pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données de restreindre l’accès. Contrôle d’accès en fonction du rôle (RBAC) peut être utilisé tooassign autorisations toousers, des groupes et des applications au niveau d’une certaine étendue. toolearn savoir plus sur l’octroi aux utilisateurs d’accès tooapplications, consultez [prise en main la gestion des accès](../active-directory/role-based-access-control-what-is.md).
- Protégez vos clés. Si vous perdez vos clés d’abonnement, qu’importe la qualité de votre stratégie de sécurité ! Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (tels que les clés d’authentification, les clés de compte de stockage, les clés de chiffrement de données, les fichiers PFX et les mots de passe) à l’aide de clés protégées par des modules de sécurité matériels (HSM). Pour une meilleure garantie, vous pouvez importer ou générer des clés HSM. Consultez [Azure Key Vault](../key-vault/key-vault-whatis.md) toolearn plus. Vous pouvez également utiliser le coffre de clés toomanage vos certificats TLS avec renouvellement automatique.
- Limitez les adresses IP source entrantes. L’[environnement App Services](../app-service-web/app-service-app-service-environment-intro.md) propose une fonctionnalité d’intégration de réseau virtuel qui vous permet de limiter les adresses IP sources entrantes par le biais de groupes de sécurité réseau (NSG). Si vous n’êtes pas familiarisé avec les réseaux virtuels Azure (réseaux virtuels), il s’agit d’une fonctionnalité qui vous permet de tooplace la plupart de vos ressources Azure dans un réseau routable en non internet que vous contrôlez l’accès à. toolearn, voir [intégrer votre application à un réseau virtuel Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Étapes suivantes
Cet article introduit collection tooa de Services d’application meilleures pratiques de sécurité pour sécuriser votre PaaS applications web et mobiles. toolearn savoir plus sur la sécurisation de vos déploiements PaaS, consultez :

- [Sécurisation des déploiements PaaS](security-paas-deployments.md)
- [Sécurisation des applications mobiles et web PaaS à l’aide d’Azure SQL Database et de SQL Data Warehouse](security-paas-applications-using-sql.md)
