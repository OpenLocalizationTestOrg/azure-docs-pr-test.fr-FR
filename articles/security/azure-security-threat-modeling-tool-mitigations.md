---
title: "aaaMitigations - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "Page d’atténuation pour toohello les solutions possibles mise en surbrillance outil de modélisation de menace Microsoft hello plus exposé généré menaces."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 000c0980d976b09fc9287e582e3776efaf7e390c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool-mitigations"></a>Atténuations de l’outil Microsoft de modélisation des menaces

Hello, outil de modélisation des menaces est un élément essentiel du hello du cycle de vie de développement de sécurité Microsoft (SDL). Il permet aux logiciels architectes tooidentify et d’atténuer les problèmes de sécurité potentiels au plus tôt, lorsqu’ils sont relativement facile et plus économique tooresolve. Par conséquent, il réduit considérablement les coût total de hello du développement. En outre, nous avons conçu outil de hello avec des experts de sécurité à l’esprit, facilitant la modélisation des menaces pour tous les développeurs en fournissant des indications précises sur la création et l’analyse des modèles de menace.

Visitez hello  **[outil de modélisation des menaces](./azure-security-threat-modeling-tool.md)**  tooget dès aujourd'hui !

## <a name="mitigation-categories"></a>Catégories d’atténuation

les solutions d’atténuation Hello outil de modélisation des menaces sont classées en fonction de toohello cadre de sécurité des applications Web, qui se compose des éléments suivants de hello :

| Catégorie | Description |
| -------- | ----------- |
| **[Audit et journalisation](./azure-security-threat-modeling-tool-auditing-and-logging.md)** | Qui a fait quoi et quand ? L’audit et journalisation font référence toohow votre application enregistrements événements de sécurité |
| **[Authentification](./azure-security-threat-modeling-tool-authentication.md)** | Qui êtes-vous ? L’authentification est le processus hello dans lequel une entité prouve identité hello d’une autre entité, généralement par le biais d’informations d’identification, telles qu’un nom d’utilisateur et un mot de passe |
| **[Autorisation](./azure-security-threat-modeling-tool-authorization.md)** | Que pouvez-vous faire ? L’autorisation désigne la manière dont votre application fournit des contrôles d’accès pour les ressources et les opérations |
| **[Sécurité des communications](./azure-security-threat-modeling-tool-communication-security.md)** | À qui parlez-vous ? La sécurité des communications garantit que toutes les communications effectuées sont aussi sécurisées que possible |
| **[Gestion des configurations](./azure-security-threat-modeling-tool-configuration-management.md)** | Pour qui votre application s’exécute-t-elle ? À quelles bases de données se connecte-t-elle ? Comment votre application est-elle administrée ? Comment ces paramètres sont-ils sécurisés ? Gestion de la configuration fait référence toohow votre application gère ces problèmes opérationnels |
| **[Cryptographie](./azure-security-threat-modeling-tool-cryptography.md)** | Comment conservez-vous les secrets (confidentialité) ? Comment protégez-vous vos données ou vos bibliothèques de la falsification (intégrité) ? Comment obtenez-vous des valeurs aléatoires solides d’un point de vue cryptographique ? Chiffrement fait référence toohow votre application applique la confidentialité et l’intégrité |
| **[Gestion des exceptions](./azure-security-threat-modeling-tool-exception-management.md)** | En cas d’échec d’un appel de méthode dans votre application, que fait votre application ? Dans quelle mesure révélez-vous vos informations ? Retournent une erreur conviviale tooend informations que les utilisateurs ? Vous passez de l’appelant d’exception précieuses informations toohello précédent ? Votre application échoue-t-elle de manière appropriée ? |
| **[Validation des entrées](./azure-security-threat-modeling-tool-input-validation.md)** | Comment savoir que les entrées de hello reçoit de votre application sont valides et sans échec ? Validation d’entrée fait référence à toohow votre application filtre, nettoie ou refuse les entrées avant un traitement supplémentaire. Pensez à limiter les entrées par le biais des points d’entrée et à encoder les sorties par le biais des points de sortie. Faites-vous confiance aux données provenant de sources telles que les bases de données et les partages de fichiers ? |
| **[Données sensibles](./azure-security-threat-modeling-tool-sensitive-data.md)** | Comment votre application gère-t-elle les données sensibles ? Les données sensibles fait référence toohow que votre application gère toutes les données qui doivent être protégées en mémoire, sur le réseau de hello, ou dans les magasins persistants |
| **[Gestion des sessions](./azure-security-threat-modeling-tool-session-management.md)** | Comment votre application gère-t-elle et protège-t-elle les sessions utilisateur ? Une session fait référence à des séries de tooa d’interactions associées entre un utilisateur et votre application Web |

Cela vous permet d’identifier :

* Où est hello erreurs les plus courantes
* Où est hello plus exploitables améliorations

Par conséquent, vous utilisez ces toofocus de catégories et de hiérarchiser votre travail de sécurité, afin que si vous connaissez les problèmes de sécurité prédominant hello se produisent dans les catégories de validation, l’authentification et l’autorisation d’entrée hello, vous pouvez commencer de là. Pour plus d’informations, consultez **[ce lien de brevet](https://www.google.com/patents/US7818788)**

## <a name="next-steps"></a>Étapes suivantes

Visitez  **[menace pour la modélisation des menaces d’outil](./azure-security-threat-modeling-tool-threats.md)**  toolearn savoir plus sur hello menace outil hello de catégories utilise les menaces toogenerate conception possible.
