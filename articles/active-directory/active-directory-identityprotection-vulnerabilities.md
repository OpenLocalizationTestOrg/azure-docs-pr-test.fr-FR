---
title: "aaaVulnerabilities détectés par la Protection d’identité Azure Active Directory | Documents Microsoft"
description: "Vue d’ensemble des vulnérabilités hello détectés par la Protection d’identité Azure Active Directory."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnérabilités détectées par Azure Active Directory Identity Protection
Les vulnérabilités sont des points faibles exploitables par un cybercriminel au sein de votre environnement. Nous vous recommandons de résoudre ces posture de sécurité hello tooimprove des vulnérabilités de votre organisation et d’empêcher les intrus de les exploiter.


![vulnérabilités](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnérabilités")



Hello sections suivantes fournissent une vue d’ensemble des vulnérabilités hello signalés par la Protection de l’identité.

## <a name="multi-factor-authentication-registration-not-configured"></a>Inscription à l’authentification multifacteur non configurée
Cette vulnérabilité vous permet de contrôler le déploiement de hello d’Azure multi-Factor Authentication dans votre organisation. 

L’authentification multifacteur Azure fournit une deuxième couche toouser d’authentification de sécurité. Il vous aide à toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une authentification forte via diverses options de vérification simples : appel téléphonique, message texte, notification par application mobile ou code de vérification et jetons OATH tiers.

Nous vous recommandons d’exiger l’authentification multifacteur d’Azure pour les connexions des utilisateurs. L’authentification multifacteur joue un rôle clé dans les stratégies d’accès conditionnel en fonction des risques disponibles via Identity Protection.

Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Applications cloud non gérées
Cette vulnérabilité vous permet d’identifier les applications cloud non gérées au sein de votre organisation.

Dans les entreprises modernes, les services informatiques sont souvent pas conscients de toutes les applications de cloud hello que les utilisateurs dans leur organisation utilisent toodo leur travail. Il est facile toosee pourquoi administrateurs auront des problèmes sur les données toocorporate de tout accès non autorisé, les fuites de données possibles et les autres risques de sécurité. 

Nous recommandons que votre organisation déployer des applications de cloud Cloud App Discovery toodiscover non managée et toomanage ces applications à l’aide d’Azure Active Directory.

Pour plus d’informations, consultez l’article [Détection des applications cloud non gérées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Alertes de sécurité du service Privileged Identity Management
Cette vulnérabilité vous aide à détecter et à résoudre les alertes relatives aux identités privilégiées dans votre organisation.  

toocarry d’utilisateurs tooenable opérations nécessitant des privilèges, les organisations ont besoin les utilisateurs toogrant temporaires ou définitives des privilèges d’accès dans Azure AD, les ressources Azure ou Office 365 ou autres applications SaaS. Chacune de ces surface d’attaque hello augmente les utilisateurs privilégiés de votre organisation. Cette vulnérabilité vous aide à identifier les utilisateurs avec un accès privilégié inutile et prendre les mesures appropriées tooreduce ou éliminer le risque de hello qu’ils représentent. 

Il est recommandé que votre organisation utilise Azure AD Privileged Identity Management toomanage, contrôle et identités d’analyse privilégié et leurs tooresources d’accès dans Azure AD ainsi que d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.

Pour plus d’informations, consultez l’article [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Voir aussi
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

