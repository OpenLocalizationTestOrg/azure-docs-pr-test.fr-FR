---
title: "Chiffrement de base de données au repos : Azure Cosmos DB | Microsoft Docs"
description: "Découvrez comment Azure Cosmos DB assure le chiffrement par défaut de toutes les données."
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Chiffrement de base de données Azure Cosmos DB au repos

Le chiffrement au repos est une expression qui fait généralement référence toohello le chiffrement des données sur les périphériques de stockage non volatile, telles que les lecteurs de solid state Drive (SSD) et les lecteurs de disque dur (HDD). Cosmos DB stocke ses bases de données primaires sur des SSD. Ses pièces jointes multimédias et ses sauvegardes sont stockées dans le Stockage Blob Azure, qui est généralement sauvegardé sur des disques durs. Avec la version hello du chiffrement au repos pour Cosmos DB, toutes les bases de données, les pièces jointes de support et les sauvegardes sont chiffrées. Vos données sont désormais chiffrées en transit (sur le réseau de hello) et au repos (stockage non volatile), ce qui vous donne le chiffrement de bout en bout.

Comme un service PaaS, Cosmos DB est très facile toouse. Étant donné que toutes les données utilisateur stockées dans la base de données Cosmos est chiffré au repos et de transport, vous n’avez tootake toute action. Une autre façon tooput, c’est que le chiffrement au repos est « sur » par défaut. Il n’y aucun tooturn contrôles il ou désactiver. Nous fournir cette fonctionnalité, alors que nous continuons toomeet notre [SLA de disponibilité et les performances](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Implémenter le chiffrement au repos

Le chiffrement au repos est implémenté à l’aide d’un certain nombre de technologies de sécurité, notamment des systèmes de stockage de clés sécurisés, des réseaux chiffrés et des API de chiffrement. Les systèmes déchiffrement et traitent les données sont toocommunicate avec les systèmes de gestion des clés. diagramme de Hello montre comment le stockage de gestion des données et de hello chiffrée des clés est séparé. 

![Schéma montrant la conception](./media/database-encryption-at-rest/design-diagram.png)

flux de base Hello d’une demande de l’utilisateur est la suivante :
- compte d’utilisateur de base de données Hello est prête, et les clés de stockage sont récupérées via un fournisseur de ressources de Service de gestion de toohello demande.
- Un utilisateur crée une base de données de tooCosmos connexion via le transport HTTPS sécurisé. (détails de hello abstraite hello kits de développement logiciel).
- utilisateur de Hello envoie un toobe de document JSON stocké sur hello précédemment créé une connexion sécurisée.
- document JSON Hello est indexée, sauf si l’utilisateur de hello a désactivé l’indexation.
- Hello document JSON et les données d’index sont écrites toosecure stockage.
- Périodiquement, les données sont lues à partir du stockage sécurisé de hello et sauvegardées toohello magasin d’objets Blob Azure chiffré.

## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>Q : Quel est le coût supplémentaire de Stockage Azure si le chiffrement du service de stockage est activé ?
R : Aucun coût supplémentaire n’est facturé.

### <a name="q-who-manages-hello-encryption-keys"></a>Q : qui gère les clés de chiffrement hello ?
R : les clés de hello sont gérées par Microsoft.

### <a name="q-how-often-are-encryption-keys-rotated"></a>Q : À quelle fréquence les clés de chiffrement tournent-elles ?
R : Microsoft a un ensemble de règles internes pour la rotation des clés de chiffrement, qui sont suivies par Cosmos DB. des recommandations spécifiques Hello ne sont pas publiées. Microsoft ne publie pas hello [du cycle de vie de développement de sécurité (SDL)](https://www.microsoft.com/sdl/default.aspx), qui est considéré comme un sous-ensemble de conseil interne et a utiles meilleures pratiques pour les développeurs.

### <a name="q-can-i-use-my-own-encryption-keys"></a>Q : Puis-je utiliser mes propres clés de chiffrement ?
R : cosmos DB est un service PaaS, et nous avons travaillé dur tookeep hello service simple toouse. Nous avons constaté que cette question est souvent posée en rapport avec la conformité à des normes comme PCI-DSS. Dans le cadre de la création de cette fonctionnalité, nous avons collaboré avec tooensure auditeurs de conformité que les clients qui utilisent la base de données Cosmos répondre aux exigences sans les clés toomanage hello besoin eux-mêmes.
Par conséquent, nous actuellement n’offrent pas les utilisateurs hello option tooburden eux-mêmes avec la gestion de clés.

### <a name="q-what-regions-have-encryption-turned-on"></a>Q : Dans quelles régions le chiffrement est-il activé ?
R : Le chiffrement est activé dans toutes les régions Azure Cosmos DB pour l’ensemble des données utilisateur.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>Q : chiffrement affecte-t-elle la latence de performances hello et débit SLA ?
R : il n’existe aucun impact ou modifications toohello de performances SLA maintenant que le chiffrement au repos est activé pour tous les comptes existants et nouveaux. Vous pouvez en savoir plus sur hello [SLA pour la base de données Cosmos](https://azure.microsoft.com/support/legal/sla/cosmos-db) page garanties de dernière toosee hello.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>Q : émulateur local de hello prend-il en charge le chiffrement au repos ?
R : émulateur de hello est un outil de développement/test autonome et n’utilise pas les services de gestion de clés hello qui hello managé Cosmos DB service utilise. Notre recommandation est tooenable BitLocker sur les lecteurs où vous stockez les données de test émulateur sensibles. Hello [émulateur prend en charge le répertoire de données par défaut hello modification](local-emulator.md) ainsi qu’à l’aide d’un emplacement connu.

## <a name="next-steps"></a>Étapes suivantes

Pour une vue d’ensemble de sécurité de la base de données Cosmos et les dernières améliorations du hello, consultez [sécurité de base de données de base de données Azure Cosmos](database-security.md).
Pour plus d’informations sur les certifications Microsoft, consultez hello [Azure Trust Center](https://azure.microsoft.com/en-us/support/trust-center/).
