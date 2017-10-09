---
title: "aaaOverview de base de données Azure pour le service de base de données relationnelle MySQL | Documents Microsoft"
description: "Vue d’ensemble de hello Azure de base de données pour le service de base de données relationnelle de MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a>Qu’est-ce qu’Azure Database pour MySQL ? Présentation du service
Base de données Azure pour MySQL est un service de base de données relationnelle dans hello cloud de Microsoft en fonction du [MySQL Community Edition](https://www.mysql.com/products/community/) moteur de base de données.  Azure Database pour MySQL offre :

- Performances prévisibles sur plusieurs niveaux de service
- Évolutivité dynamique sans interruption de l’application
- Haute disponibilité intégrée
- Protection des données

Ces fonctionnalités ne nécessitent presque aucune administration, et toutes sont fournies sans coût supplémentaire. Elles vous permettent de toofocus sur le développement d’applications rapide et accélérer votre toomarket de temps, au lieu d’allouer beaucoup de temps et ressources toomanaging virtual machines et l’infrastructure. En outre, vous pouvez continuer toodevelop votre application avec hello ouvrir les outils de la source et la plate-forme de votre choix et livrer avec une vitesse hello et l’efficacité de vos activités professionnelles sans avoir toolearn nouvelles compétences.

![Diagramme conceptuel d’Azure Database pour MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

Cet article est une base de données de tooAzure introduction pour MySQL principaux concepts et tooperformance connexes de fonctionnalités, l’évolutivité et la facilité de gestion avec des détails sur les liens tooexplore. Consultez que ces rapide démarre tooget que vous avez démarré :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure](quickstart-create-mysql-server-database-using-azure-cli.md)

Pour accéder à des exemples Azure CLI, consultez :
- [Exemples de CLI Azure pour Azure Database pour MySQL](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajustez les performances et la mise à l'échelle sans interruption de service
Le service Azure Database pour MySQL propose deux niveaux de service : De base et Standard. Chaque niveau offre des performances différentes et les charges de travail fonctionnalités toosupport tooheavyweight léger de base de données. Vous pouvez créer votre première application sur une petite base de données pour quelques dollars un mois, puis modifier votre tooscale de niveau de service avec des besoins de votre solution sans temps mort. Évolutivité dynamique permet à votre toorapidly de répondre tootransparently de base de données modifie les besoins de ressources. Vous payez uniquement pour les ressources hello que vous avez besoin, lorsque vous avez besoin.

## <a name="monitoring-and-alerting"></a>Surveillance et alerte
Comment savoir hello bouton droit sur-arrêt lorsque vous composez le haut et bas ? Utilisez l’analyse des performances intégrés hello et fonctionnalités, combinées avec des évaluations de performances hello en fonction de l’unité de calcul d’alerte. À l’aide de ces fonctionnalités, vous pouvez rapidement évaluer impact hello de mise à l’échelle vers le haut ou vers le bas en fonction de votre actuel ou les besoins de performances. Consultez [Concepts : niveaux de service](concepts-service-tiers.md) pour plus d’informations.

## <a name="keep-your-app-and-business-running"></a>Votre application et votre activité ne s’arrêtent jamais
Avec un temps de disponibilité de 99,99 %, l’excellent contrat de niveau de service (SLA) d’Azure, soutenu par un réseau mondial de centres de données gérés par Microsoft, permet d’exécuter votre application 24 heures sur 24, 7 jours sur 7. Chaque base de données Azure pour le serveur MySQL, vous tirer parti de la sécurité intégrée, la tolérance de panne et protection des données que vous devriez autrement toobuy ou conception, générer et gérer. Avec la base de données Azure pour MySQL, vous pouvez utiliser le point-à-temps restauration toorecover un tooan de serveur d’état précédemment, en remontant jusqu'à 35 jours.

## <a name="secure-your-data"></a>Sécurisez vos données
Les services de base de données Azure ont une tradition de sécurité des données qu’Azure Database pour MySQL respecte avec des fonctionnalités qui limitent l’accès, protègent les données au repos et en mouvement, et vous aident à surveiller l’activité. Visitez hello [Azure Trust Center](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) pour plus d’informations sur la sécurité de plateforme Azure.

Hello Azure de base de données pour le service MySQL utilise le chiffrement de stockage pour les données au repos. Chiffrement des données, y compris les sauvegardes, sur le disque (à l’exception de hello des fichiers temporaires créés par le moteur de hello lors de l’exécution de requêtes). service de Hello utilise le chiffrement AES 256 bits qui est inclus dans le chiffrement de stockage Azure, et les clés de hello sont générées par le système. Le chiffrement de stockage est toujours activé et ne peut pas être désactivé.

Par défaut, hello de base de données Azure pour service MySQL est configuré toorequire [sécurité de connexion SSL](./concepts-ssl-connection-security.md) pour les données en mouvement réseau hello. Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.  Si vous le souhaitez, vous pouvez désactiver l’utilisation de SSL pour la connexion de service de base de données tooyour si votre application cliente ne prend pas en charge la connectivité SSL.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez lu un tooAzure de présentation de base de données de MySQL et ayant obtenu une réponse de question de hello « Qu’est une base de données Azure pour MySQL ? », vous êtes prêt à :
- Consultez hello page pour les comparaisons de coût et les calculatrices de tarification. [Tarification](https://azure.microsoft.com/pricing/details/mysql/)
- Commencez par créer votre premier serveur. [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Générer votre première application dans Python, PHP, Ruby, C\#, Java, Node.js : [les bibliothèques de connectivité permettant tooconnect tooAzure base de données MySQL](concepts-connection-libraries.md)
