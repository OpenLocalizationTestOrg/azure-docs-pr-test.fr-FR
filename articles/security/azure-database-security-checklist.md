---
title: "aide-mémoire de la sécurité de base de données aaaAzure | Documents Microsoft"
description: "Cet article fournit un ensemble de listes de contrôle pour la sécurité des bases de données Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Liste de contrôle de la sécurité des bases de données Azure

toohelp améliorer la sécurité, la base de données Azure inclut un nombre de contrôles de sécurité intégrés que vous pouvez utiliser toolimit et contrôler l’accès.

Vous avez notamment vu les points suivants :

-   Un pare-feu qui vous permet de toocreate [des règles de pare-feu](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) limitant la connectivité par adresse IP,
-   Pare-feu de niveau serveur accessible à partir de hello portail Azure
-   Règles de pare-feu au niveau de la base de données accessibles à partir de SSMS
-   Base de données tooyour connectivité sécurisée à l’aide de chaînes de connexion sécurisées
-   Gestion de l’accès des utilisateurs
-   Chiffrement des données
-   Audit de base de données SQL
-   Détection de menaces pour les bases de données SQL

## <a name="introduction"></a>Introduction
Le cloud computing requiert de nouveaux modèles de sécurité qui sont des utilisateurs d’applications inconnues réduire, les administrateurs de base de données et les programmeurs. Par conséquent, certaines organisations sont hésitent tooimplement une infrastructure cloud pour la gestion des données en raison des risques de sécurité tooperceived. Toutefois, une grande partie de ce problème peut être soulagée par une meilleure compréhension des fonctionnalités de sécurité hello intégrées à Microsoft Azure et base de données SQL Microsoft Azure.

## <a name="checklist"></a>Liste de contrôle
Nous vous recommandons de lire hello [meilleures pratiques de la sécurité de base de données Azure](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) article tooreviewing antérieure à cette liste de vérification. Vous serez hello tooget en mesure de meilleur parti de cette liste de vérification que vous comprenez les meilleures pratiques de hello. Vous pouvez ensuite utiliser cette liste de vérification toomake assurer que vous avez résolu les problèmes importants hello dans la sécurité de la base de données Azure.


|Catégorie de la liste de contrôle| Description|
| ------------ | -------- |
|**Protection les données**||
| <br> Chiffrement en mouvement/transit| <ul><li>[Sécurité de la couche de transport](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), pour le chiffrement des données lorsque les données se déplacent toohello réseaux.</li><li>Base de données requiert une communication sécurisée à partir de clients basés sur hello [TDS (Tabular Data Stream)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protocole sur TLS (Transport Layer Security).</li></ul> |
|<br>Chiffrement au repos| <ul><li>[Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242), lorsque les données inactives sont stockées physiquement dans un format numérique.</li></ul>|
|**Contrôle des accès**||  
|<br> Accès à la base de données | <ul><li>[Authentification](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) AD (Azure Active Directory), qui utilise des identités gérées par Azure Active Directory.</li><li>[Autorisation](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) accorder aux utilisateurs hello des privilèges minimaux nécessaires.</li></ul> |
|<br>Accès aux applications| <ul><li>[Sécurité au niveau de la ligne](https://msdn.microsoft.com/library/dn765131) (à l’aide de stratégie de sécurité, au hello simultanément en limitant l’accès au niveau des lignes selon le contexte d’identité ou le rôle ou l’exécution d’un utilisateur).</li><li>[Masquage dynamique des données](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (à l’aide de l’autorisation et stratégie, limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon)</li></ul>|
|**Surveillance proactive**||  
| <br>Suivi et détection| <ul><li>[L’audit](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) effectue le suivi des événements de base de données et les écrit le journal d’Audit de tooan / activité des journaux votre [compte de stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Suivi de l’intégrité des bases de données Azure à l’aide des [journaux d’activité Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Détection de menaces](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) détecte des activités de la base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles. </li></ul> |
|<br>Azure Security Center| <ul><li>[Surveillance des données](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases), avec Azure Security Center comme solution de surveillance de la sécurité centralisée pour SQL et d’autres services Azure.</li></ul>|     

## <a name="conclusion"></a>Conclusion
Azure Database est une plateforme robuste de base de données, avec un éventail complet de fonctionnalités de sécurité qui répondent à de nombreuses exigences en matière de conformité réglementaire et organisationnelles. Vous pouvez facilement protéger les données en contrôlant les données de tooyour hello accès physique et à l’aide de diverses options de sécurité des données à hello fichier, colonne ou au niveau des lignes avec chiffrement Transparent des données, le chiffrement au niveau des cellules ou sécurité de niveau ligne. Toujours chiffré permet également des opérations sur les données chiffrées, ce qui simplifie le processus hello des mises à jour de l’application. À son tour, journaux tooauditing d’accès de l’activité de la base de données SQL fournit des informations de hello vous avez besoin, ce qui vous tooknow comment et quand les données sont accessibles.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez améliorer la protection de hello de votre base de données contre les utilisateurs malveillants ou de tout accès non autorisé seulement quelques étapes simples. Ce didacticiel vous apprend à effectuer les opérations suivantes :

- Définir des [règles de pare-feu](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) pour votre serveur et/ou base de données.
- Protéger vos données à l’aide du [chiffrement](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Activer l’[audit Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

