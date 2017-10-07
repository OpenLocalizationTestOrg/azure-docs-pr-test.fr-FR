---
title: "aaaManaging tooapps de l’accès à l’aide d’Azure AD | Documents Microsoft"
description: "Décrit comment Azure Active Directory permet aux organisations toospecify hello applications toowhich chaque utilisateur a accès."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Gestion des accès tooapps
Gestion de l’accès en cours, l’évaluation de l’utilisation et création de rapports continuent toobe un défi, une fois qu’une application est intégrée dans le système d’identité de votre organisation. Dans de nombreux cas, les administrateurs informatiques ou le support technique ont tootake un rôle actif en cours de la gestion des applications de tooyour d’accès. Parfois, l’affectation est effectuée par une équipe informatique générale ou rattachée à une division. Souvent, la décision de l’attribution de hello est prévue toobe toohello déléguée décideur, nécessitant une approbation avant informatique rend hello affectation.  D’autres organisations investissent dans l’intégration à un système automatisé de gestion des identités et des accès, tel que le contrôle d’accès en fonction du rôle (RBAC) ou le contrôle d’accès en fonction de l’attribut (ABAC). Intégration de hello et développement de la règle ont tendance toobe spécialisée et coûteux. Quelle que soit la méthode de gestion, l’analyse ou la création de rapports suppose un investissement distinct, coûteux et complexe.

## <a name="how-does-azure-active-directory-help"></a>En quoi Azure Active Directory peut-il vous aider ?
 Azure AD prend en charge étendue gestion de l’accès pour les applications configurées, l’activation des organisations tooeasily obtenir des stratégies d’accès appropriés hello allant de l’attribution automatique, basée sur l’attribut (fichier ABAC ou RBAC scénarios) via la délégation et en incluant gestion des administrateurs. Avec Azure AD, vous pouvez facilement obtenir stratégies complexes, associant plusieurs modèles d’administration pour une application unique et peuvent même réutiliser des règles de gestion entre les applications avec hello mêmes audiences.

* [Ajout d’applications nouvelles ou existantes](active-directory-sso-integrate-saas-apps.md)

 L’affectation d’applications Azure AD se concentre sur deux modes d’affectation principaux :

* **Affectation** un administrateur informatique avec des autorisations d’administrateur général de répertoire permettre sélectionner des comptes d’utilisateur individuels et leur accorder l’accès toohello application.
* **Affectation basée sur le groupe (payée AD Azure uniquement)** un administrateur avec des autorisations d’administrateur général active peut affecter une application toohello de groupe. L’accès des utilisateurs spécifiques est déterminé par ce qu’ils soient membres du groupe de hello au moment de hello ils tentent d’application de hello tooaccess. En d’autres termes, un administrateur peut créer efficacement une règle d’affectation indiquant « n’importe quel membre actuel de hello affecté groupe a accès toohello application ». Avec cette option d’affectation, les administrateurs peuvent tirer parti des options de gestion de groupe Azure AD, notamment des [groupes dynamiques basés sur l’attribut](active-directory-accessmanagement-manage-groups.md), des groupes de systèmes externes (par exemple, Active Directory local ou Workday) ou des groupes gérés par un administrateur ou en libre-service. Un seul groupe peut être facilement affecté toomultiple applications, vous être assuré que les applications avec l’affinité d’affectation peuvent partager des règles d’affectation, ce qui réduit hello la complexité de la gestion globale. Veuillez noter ce groupe imbriqué appartenances ne sont pas pris en charge pour l’affectation basée sur le groupe tooapplications pour l’instant.

Grâce à ces deux modes d’affectation, les administrateurs peuvent mettre en œuvre toute approche de gestion d’affectation souhaitable.

Avec Azure AD, l’utilisation et les rapports d’affectations est entièrement intégré, l’activation de rapport de tooeasily administrateurs sur l’état d’affectation, erreurs d’affectation et même l’utilisation.

## <a name="complex-application-assignment-with-azure-ad"></a>Affectation d’application complexe avec Azure AD
Considérez une application comme Salesforce. Dans de nombreuses organisations, force de vente est principalement utilisé par les organisations de vente et marketing hello. Souvent, les membres de l’équipe marketing de hello ont privilèges très élevés tooSalesforce d’accès, tandis que les membres de l’équipe de vente hello ont un accès limité. Dans de nombreux cas, une large population de travailleurs ont limité accès toohello application. Règles d’exceptions toothese compliquent les choses. Il est souvent prérogative hello de hello marketing ou de ventes leadership équipes toogrant un utilisateur l’accès ou modifier leurs rôles indépendamment de ces règles génériques.

Avec Azure AD, les applications telles que Salesforce peuvent être préconfigurées pour l’authentification unique (SSO) et l’automatisation de l’approvisionnement. Une fois que l’application hello est configurée, un administrateur peut prendre hello action unique toocreate et affecter les groupes appropriés hello. Dans cet exemple, un administrateur pourrait exécuter hello suivant affectations :

* [Groupes dynamiques](active-directory-accessmanagement-manage-groups.md) peut être défini tooautomatically représenter tous les membres des équipes de vente et marketing hello à l’aide des attributs tels que le service ou le rôle :
  
  * Tous les membres de groupes marketing doivent être affectées toohello le rôle « marketing » dans Salesforce
  * Tous les membres des ventes de groupes de l’équipe doivent être affectées toohello le rôle « ventes » dans Salesforce. Un affinage supplémentaire peut utiliser plusieurs groupes qui représentent des équipes commerciales régionales toodifferent Salesforce rôles attribués.
* mécanisme d’exception tooenable hello, un groupe libre-service peut être créé pour chaque rôle. Par exemple, le groupe de « Salesforce marketing exception » de hello peut être créé comme un groupe libre-service. rôle de marketing Salesforce toohello peut être attribué à groupe de Hello et propriétaires peut être effectuée à équipe dirigeante de la commercialisation hello. Membres de l’équipe dirigeante de la commercialisation hello peuvent ajouter ou supprimer les utilisateurs, définir une stratégie de jointure, ou même approuver ou refuser toojoin des demandes des utilisateurs individuels. Ces fonctionnalités reposent sur une expérience de travailleur de l’information appropriée qui ne nécessite pas de formation spécialisée pour les propriétaires ou les membres.

Dans ce cas, tous les utilisateurs affectés serait tooSalesforce configuré automatiquement, car ils sont des groupes toodifferent ajouté que leur attribution de rôle sera actualisée dans Salesforce. Les utilisateurs sont en mesure de toodiscover et accès Salesforce via un panneau d’accès application hello Microsoft, les clients Office web, ou même de navigation dans la page de connexion tootheir d’organisation Salesforce. Les administrateurs seraient en mesure de tooeasily afficher d’utilisation et l’attribution de l’état à l’aide de la création de rapports Azure AD.

Les administrateurs peuvent utiliser [accès conditionnel Azure AD](active-directory-conditional-access.md) tooset les stratégies d’accès pour des rôles spécifiques. Ces stratégies peuvent inclure si l’accès est autorisé en dehors d’environnement d’entreprise de hello et même l’authentification multifacteur ou un accès tooachieve exigences des appareils dans différents cas.

## <a name="how-can-i-get-started"></a>Comment faire pour démarrer ?
Avant tout, si vous n’utilisez pas déjà Azure AD et que vous êtes administrateur informatique :

* [Essayez-le !](https://azure.microsoft.com/trial/get-started-active-directory/) Vous pouvez vous inscrire pour une période d’essai gratuit de 30 jours, puis déployer votre première solution cloud en moins de 5 minutes.

Les fonctionnalités Azure AD qui permettent le partage de compte sont les suivantes :

* [Affectation de groupe](active-directory-accessmanagement-self-service-group-management.md)
* Ajout d’applications tooAzure AD
* Prise en main de l’affectation
* FAQ relative à l’affectation d’applications
* [Tableau de bord/rapports d’utilisation des applications](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>Où en savoir plus ?
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Protection des applications avec accès conditionnel](active-directory-conditional-access.md)
* [Gestion des groupes en libre service/accès aux applications en libre-service](active-directory-accessmanagement-self-service-group-management.md)

