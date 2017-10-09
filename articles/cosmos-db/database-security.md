---
title: "sécurité aaaDatabase - base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment Azure Cosmos DB garantit la protection de la base de données et la sécurité de vos données."
keywords: "sécurité de la base de données NoSQL, sécurité des informations, sécurité des données, chiffrement de base de données, protection de base de données, stratégies de sécurité, tests de sécurité"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Sécurité de la base de données Azure Cosmos DB

Cet article traite des meilleures pratiques de sécurité de base de données et les principales fonctionnalités offertes par base de données Azure Cosmos toohelp vous empêchez, détecter et répondre toodatabase violations.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Quelles sont les nouveautés en matière de sécurité dans Azure Cosmos DB ?

Le chiffrement au repos est désormais disponible pour les documents et les sauvegardes stockés dans Azure Cosmos DB dans toutes les régions Azure. Un chiffrement au repos est automatiquement appliqué aux clients nouveaux et existants dans ces régions. Il n’existe aucun besoin tooconfigure quoi que ce soit ; et que vous obtenez hello même latence élevée, le débit, disponibilité et des fonctionnalités comme avant avantage hello de connaître vos données sûre et sécurisée avec le chiffrement au repos.

## <a name="how-do-i-secure-my-database"></a>Comment sécuriser ma base de données ? 

Sécurité des données est une partage des responsabilités entre vous, hello client et votre fournisseur de base de données. Selon le choix du fournisseur de base de données hello, quantité hello de responsabilité que vous effectuer peut varier. Si vous choisissez une solution sur site, vous devez tooprovide allant de la sécurité de toophysical protection de point de terminaison de votre matériel - qui n’est pas une tâche facile. Si vous choisissez un fournisseur de base de données cloud PaaS comme Azure Cosmos DB, vous réduisez considérablement votre niveau d’inquiétude. Hello suivants image, provenant de Microsoft [partagé des responsabilités de Cloud Computing](https://aka.ms/sharedresponsibility) livre blanc indique comment votre responsabilité diminue avec un fournisseur PaaS comme base de données Azure Cosmos.

![Responsabilités du client et du fournisseur de base de données](./media/database-security/nosql-database-security-responsibilities.png)

Hello diagramme précédent montre les composants de sécurité globale de cloud, mais les éléments que vous devez tooworry sur spécifiquement pour votre solution de base de données ? Et comment vous pouvez comparer les solutions tooeach autres ? 

Nous vous recommandons de hello suivant de liste de vérification de la configuration requise sur les systèmes de base de données toocompare :

- Sécurité du réseau et paramètres de pare-feu
- Authentification des utilisateurs et contrôles utilisateur affinés
- Données de tooreplicate de capacité global pour les défaillances régionales
- Basculements de tooperform de capacité de données d’un centre de tooanother
- Réplication locale des données dans un centre de données
- Sauvegardes automatiques des données
- Restauration des données supprimées à partir de sauvegardes
- Protection et isolement des données sensibles
- Surveillance des attaques
- Répondre tooattacks
- Restrictions de gouvernance capacité limite de toogeo données tooadhere toodata
- Protection physique des serveurs dans les centres de données protégés

Et il a beau sembler évidentes, récente [violations de la base de données à grande échelle](http://thehackernews.com/2017/01/mongodb-database-security.html) nous rappeler une importance hello simple mais critiques de hello suivant les exigences :
- Corrigé les serveurs qui sont conservés les toodate
- Chiffrement HTTPS par défaut/SSL
- Comptes administratifs avec des mots de passe forts

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Comment Azure Cosmos DB sécurise-t-il ma base de données ?

Examinons précédent hello précède liste - combien de ces exigences de sécurité Azure Cosmos DB fournit-il ? Toutes, sans exception.

Examinons à présent chacune d’entre elles en détail.

|Exigence de sécurité|Approche de la sécurité d’Azure Cosmos DB|
|---|---|---|
|Sécurité du réseau|Utilisation d’un pare-feu IP est hello première couche de protection toosecure votre base de données. Azure Cosmos DB prend en charge les contrôles d’accès basés sur une stratégie IP pour le pare-feu entrant. contrôles d’accès basé sur IP Hello sont des règles de pare-feu similaires toohello utilisés par les systèmes de base de données traditionnelle, mais elles sont développées afin qu’un compte de base de données de base de données Azure Cosmos soit uniquement accessible à partir d’un jeu approuvé d’ordinateurs ou de services de cloud computing. <br><br>Base de données Azure Cosmos permet de vous tooenable combinaisons des plages et adresses IP, une plage IP (168.61.48.0/8) et une adresse IP spécifique (168.61.48.0). <br><br>Toutes les demandes provenant d’ordinateurs ne figurant pas dans cette liste sont bloquées par Azure Cosmos DB. Demandes d’approuvées ordinateurs et services de cloud computing puis devront effectuer toobe de processus d’authentification hello donné d’accéder aux ressources de toohello de contrôle.<br><br>Pour plus d’informations, consultez [Prise en charge du pare-feu dans Azure Cosmos DB](firewall-support.md).|
|Autorisation|Azure Cosmos DB utilise un code d’authentification de message basé sur le hachage (HMAC) pour l’autorisation. <br><br>Chaque demande est haché à l’aide de la clé de secret principal compte hello et hello ultérieures hachage codé en base 64 est envoyé avec chaque tooAzure appel Cosmos DB. demande de toovalidate hello, par service de base de données Azure Cosmos hello hello propriétés toogenerate un hachage et clé secrète appropriée, puis il compare la valeur hello avec hello une dans la demande hello. Si hello deux valeurs correspondent, opération de hello est autorisée avec succès et hello demande est traitée, dans le cas contraire, il existe un échec d’autorisation et hello demande est rejetée.<br><br>Vous pouvez utiliser un [clé principale](secure-access-to-data.md#master-keys), ou un [jeton de ressource](secure-access-to-data.md#resource-tokens) permettant la ressource de tooa accès affinée tel qu’un document.<br><br>Pour en savoir plus [sécurisation de l’accès tooAzure Cosmos DB ressources](secure-access-to-data.md).|
|Utilisateurs et autorisations|À l’aide de hello [clé principale de](#master-key) pour le compte de hello, vous pouvez créer des ressources de l’utilisateur et autorisation par base de données. A [jeton de ressource](#resource-token) est associé à une autorisation dans une base de données et détermine si hello utilisateur a accès (en lecture-écriture, en lecture seule, ou aucun accès) tooan ressource d’application dans la base de données hello. Les ressources d’application comprennent les collections, les documents, les pièces jointes, les procédures stockées, les déclencheurs et les fonctions définies par l’utilisateur. jeton de ressource Hello est ensuite utilisé lors de l’authentification tooprovide ou refuse l’accès toohello ressource.<br><br>Pour en savoir plus [sécurisation de l’accès tooAzure Cosmos DB ressources](secure-access-to-data.md).|
|Intégration d’Active Directory (RBAC)| Vous pouvez également fournir le compte de base de données access toohello à l’aide du contrôle d’accès (IAM) Bonjour portail Azure, comme indiqué dans la capture d’écran hello qui suit ce tableau. IAM fournit un contrôle d’accès basé sur les rôles et s’intègre à Active Directory. Vous pouvez utiliser les rôles intégrés ou personnalisés pour les individus et aux groupes, comme indiqué dans hello suivant l’image.|
|Réplication mondiale|Base de données Azure Cosmos offre clé en main distribution globale, ce qui vous permet de tooreplicate votre tooany de données qu’un des centres de données du Azure monde avec hello du clic sur un bouton. Réplication globale vous permet de mettre à l’échelle globalement et fournissent des données de tooyour de faible latence accès monde hello.<br><br>Dans le contexte de sécurité de hello, réplication globale garantit la protection des données contre les défaillances régionales.<br><br>Pour en savoir plus, consultez [Distribution mondiale des données avec DocumentDB](distribute-data-globally.md).|
|Basculements régionaux|Si vous avez répliqué vos données dans plusieurs centres de données, Azure Cosmos DB bascule automatiquement vos opérations si un centre de données régional est indisponible. Vous pouvez créer une liste hiérarchisée des régions de basculement à l’aide de régions hello dans lequel vos données sont répliquées. <br><br>Pour en savoir plus, consultez [Basculements régionaux automatiques pour la continuité des activités dans Azure Cosmos DB](regional-failover.md).|
|Réplication locale|Même dans un centre de données, base de données Azure Cosmos réplique automatiquement les données pour une haute disponibilité en donnant hello de choix de [niveaux de cohérence](consistency-levels.md). Cela assure un  [SLA avec disponibilité de 99,99 %](https://azure.microsoft.com/support/legal/sla/cosmos-db) et une garantie financière, ce qu’aucun autre service de base de données ne propose.|
|Sauvegardes en ligne automatisées|Les bases de données Azure Cosmos DB sont régulièrement sauvegardées et stockées dans un magasin géoredondant. <br><br>Pour en savoir plus, consultez [Sauvegarde et restauration en ligne automatiques avec Azure Cosmos DB](online-backup-and-restore.md).|
|Restauration de données supprimées|Hello automatisée des sauvegardes en ligne peuvent être utilisés toorecover des données vous avez accidentellement supprimé des trop ~ 30 jours après l’événement de hello. <br><br>Pour en savoir plus, consultez [Sauvegarde et restauration en ligne automatiques avec Azure Cosmos DB](online-backup-and-restore.md).|
|Protection et isolement des données sensibles|Toutes les données dans des régions hello répertoriées dans [Nouveautés ?](#whats-new) sont maintenant chiffrées au repos.<br><br>Informations d’identification personnelle et d’autres données confidentielles peuvent être des collections de toospecific isolé et en lecture-écriture, ou l’accès en lecture seule peut être limité toospecific utilisateurs.|
|Surveillance des attaques|À l’aide des enregistrements d’audit et des journaux d’activité, vous pouvez surveiller les activités normales et anormales de votre compte. Vous pouvez afficher les opérations qui ont été exécutées sur vos ressources, ce qui a lancé une opération hello, lors de l’opération de hello s’est produite, état hello d’opération de hello et beaucoup plus, comme indiqué dans la capture d’écran hello sous ce tableau.|
|Répondre tooattacks|Une fois que vous avez contacté le support Azure tooreport une attaque potentielle, un processus de réponse à l’étape 5 est lancé. Hello processus en 5 étapes hello vise opérations et sécurité du service normal toorestore aussi rapidement que possible après un problème est détecté et une enquête a démarré.<br><br>Pour en savoir plus [réponse de sécurité Microsoft Azure Bonjour Cloud](https://aka.ms/securityresponsepaper).|
|Délimitation géographique|Azure Cosmos DB garantit la gouvernance et la conformité des données dans les régions souveraines (par exemple, en Allemagne, en Chine, pour le gouvernement américain).|
|Installations protégées|Dans Azure Cosmos DB, les données sont stockées sur des disques SSD dans les centres de données protégées d’Azure.<br><br>Pour en savoir plus, consultez les [centres de données Microsoft globaux](https://www.microsoft.com/en-us/cloud-platform/global-datacenters).|
|Chiffrement HTTPS/SSL/TLS|Toutes les interactions client-service d’Azure Cosmos DB appliquent un chiffrement SSL/TLS 1.2, tout comme les réplications au sein des centres de données ou entre différents centres de données.|
|Chiffrement au repos|Toutes les données stockées dans Azure Cosmos DB sont chiffrées au repos. Pour en savoir plus, consultez [Chiffrement de base de données Azure Cosmos DB au repos](.\database-encryption-at-rest.md).|
|Serveurs corrigés|Comme une base de données managé, base de données Azure Cosmos élimine les hello besoin toomanage et correctif serveurs, qui a fait automatiquement pour vous.|
|Comptes administratifs avec des mots de passe forts|Son disque dur toobelieve nous même devez toomention cette exigence, mais contrairement à certains de nos concurrents, il est impossible toohave un compte d’administrateur sans mot de passe dans la base de données Azure Cosmos.<br><br> La sécurité via SSL et l’authentification basée sur un secret HMAC sont intégrées par défaut.|
|Certifications de sécurité et de protection des données|Azure Cosmos DB détient les certifications [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [EUMC (European Model Clauses)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses) et [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA). Des certifications supplémentaires sont en cours.|

Hello capture d’écran suivante montre l’intégration Active directory (RBAC) à l’aide du contrôle d’accès (IAM) Bonjour Azure portal : ![contrôle (IAM) d’accès Bonjour Azure portal - illustrant la sécurité de la base de données](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Hello capture d’écran suivante montre comment vous pouvez utiliser l’enregistrement d’audit et des journaux d’activité toomonitor votre compte : ![des journaux d’activité pour la base de données Azure Cosmos](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les clés principales et les jetons de ressource, consultez [tooAzure accès de sécurisation des données de base de données Cosmos](secure-access-to-data.md).

Pour plus d’informations sur les certifications Microsoft, consultez le [Centre de confidentialité Azure](https://azure.microsoft.com/support/trust-center/).
