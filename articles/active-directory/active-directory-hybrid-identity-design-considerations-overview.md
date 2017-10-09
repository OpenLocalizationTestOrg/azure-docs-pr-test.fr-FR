---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - vue d’ensemble | Documents Microsoft"
description: "Vue d'ensemble et plan du contenu du guide des considérations relatives à la conception des identités hybrides"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Considérations relatives à la conception d'identités hybrides Azure Active Directory
Périphériques basés sur le consommateur sont prolifération Bonjour d’entreprise et software-as-a-service (SaaS) applications cloud sont tooadopt facile. Par conséquent, le maintien du contrôle d'accès des utilisateurs aux applications sur les plateformes cloud et les centres de données internes est difficile.  

Solutions d’identité de Microsoft sont réparties entre locaux et des fonctions nuage, de création d’une identité d’utilisateur unique pour l’authentification et d’autorisation des ressources tooall, indépendamment de l’emplacement. Nous appelons cette identité « identité hybride ». Il existe différentes options de conception et configuration d’identité hybride à l’aide de solutions de Microsoft, et dans certains cas, il peut être difficile toodetermine combinaison répond mieux aux besoins de hello de votre organisation. 

Ce Guide de considérations de conception identité hybride vous aidera toounderstand comment toodesign une solution d’identité hybride qui répond le mieux à la technologie et entreprise de hello a besoin pour votre organisation.  Ce guide détaille une série d’étapes et de tâches que vous pouvez suivre toohelp vous concevez une solution d’identité hybride qui répond aux exigences uniques de votre organisation. Tout au long des étapes de hello et tâches, hello guide présente les technologies pertinentes hello et fonctionnalité options disponibles tooorganizations toomeet fonctionnel et qualité de service (par exemple, la disponibilité, évolutivité, performances, la facilité de gestion et de sécurité) exigences de niveau. 

Plus précisément, les objectifs guide des considérations de conception hello hybride identité sont hello tooanswer suivant questions : 

* Que faire les questions vous avez besoin de tooask et que vous répondez toodrive une conception hybride identité spécifique pour un domaine problématique ou mieux adaptée à mes besoins ?
* Séquence d’activités doit terminer toodesign une solution d’identité hybride pour le domaine ou cette problématique de hello ? 
* Les options de configuration et de technologie d’identité hybride sont disponible toohelp me répondre à mes besoins ? Quelles sont les compromis hello entre ces options afin que je peux sélectionner la meilleure option de hello pour mon entreprise ?

## <a name="who-is-this-guide-intended-for"></a>À qui ce guide est-il destiné ?
 Directeurs informatiques, directeurs des systèmes d'information, responsables de l'architecture des identités, architectes d'entreprise et architectes informatiques chargés de concevoir une solution d'identité hybride pour les entreprises de taille moyenne ou grande.

## <a name="how-can-this-guide-help-you"></a>En quoi ce guide peut-il vous aider ?
Vous pouvez utiliser ce guide toounderstand comment toodesign une solution d’identité hybride qui est en mesure de toointegrate un cloud en fonction de système de gestion d’identité avec votre identité solution locale. 

Hello graphique suivant illustre une solution d’identité hybride qui permet des administrateurs informatiques toomanage toointegrate leurs actuelle Active Directory Windows Server solutions située localement avec Microsoft Azure Active Directory tooenable utilisateurs toouse unique Sign-On (SSO) entre les applications situées dans le cloud de hello et sur site.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Hello ci-dessus illustration est un exemple d’une solution d’identité hybride qui combine cloud et des services de toointegrate avec les fonctionnalités locales dans l’ordre tooprovide une expérience unique la procédure d’authentification de l’utilisateur final toohello toofacilitate informatique gestion ces ressources. Bien que cela peut être un scénario très courant, la conception d’identité de chaque organisation hybride est toobe probablement différente de celle exemple hello illustré dans la Figure 1 en raison des exigences de toodifferent. 

Ce guide fournit une série d’étapes et de tâches que vous pouvez suivre toodesign une solution d’identité hybride qui répond aux exigences uniques de votre organisation. Tout au long de hello suit et tâches, hello hello guide présente les technologies pertinentes et fonctionnalité options exigences au niveau de qualité de service et fonctionnel toomeet tooyou disponibles pour votre organisation.

**Hypothèses**: vous avez un peu d'expérience avec Windows Server, les services de domaine Active Directory et Azure Active Directory. Dans ce document, nous supposons que vous cherchez à savoir en quoi ces solutions peuvent répondre aux besoins de votre entreprise de façon autonome ou dans une solution intégrée.

## <a name="design-considerations-overview"></a>Présentation des considérations relatives à la conception
Ce document fournit un ensemble d’étapes et les tâches que vous pouvez suivre toodesign une solution d’identité hybride qui répond le mieux à vos besoins. les étapes de Hello sont présentées dans un ordre précis. Considérations de conception que vous apprendre dans les étapes suivantes peuvent vous amener toochange décisions dans les étapes précédentes, toutefois, en raison des choix de conception tooconflicting. Chaque tentative tooalert vous toopotential les conflits de conception dans l’ensemble de documents de hello. 

Vous arriverez à la conception hello correspondant le mieux à vos besoins uniquement après l’itération à travers les étapes de hello aussi souvent que nécessaire tooincorporate toutes les considérations hello dans le document de hello. 

| Phase d'identité hybride | Liste des rubriques |
| --- | --- |
| Déterminer les exigences en matière d'identité |[Déterminer les besoins métier](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Déterminer les exigences de synchronisation de répertoire](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Déterminer les exigences d’authentification multifacteur](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Définir une stratégie d'adoption des identités hybrides](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Planifier l'amélioration de la sécurité des données grâce à une solution d'identité solide |[Déterminer les exigences de protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Déterminer les exigences de gestion de contenu](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Déterminer les exigences de contrôle d’accès](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Déterminer les exigences de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Définir les options de protection des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Planifier le cycle de vie des identités hybrides |[Déterminer les tâches de gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Gestion de la synchronisation](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Déterminer la stratégie d’adoption de la gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Télécharger ce guide
Vous pouvez télécharger une version pdf du guide de considérations de conception d’identité hybride hello de hello [galerie Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

