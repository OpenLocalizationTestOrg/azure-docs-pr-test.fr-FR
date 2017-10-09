---
title: "aaaOverview de base de données Azure pour le service de base de données relationnelle PostgreSQL | Documents Microsoft"
description: "Fournit une vue d’ensemble du service de base de données relationnelle d’Azure Database pour PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 08/01/2017
ms.openlocfilehash: fd6821b56e5295b8b341d87b14d113f7a4b247c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-postgresql"></a>Qu’est-ce qu’Azure Database pour PostgreSQL ?

Base de données Azure pour PostgreSQL est un service de base de données relationnelle dans hello cloud Microsoft conçue pour les développeurs selon la version de communauté hello du open source [PostgreSQL](https://www.postgresql.org/) moteur de base de données. Ce service est en version préliminaire publique. Azure Database pour PostgreSQL offre :
- Performances prévisibles sur plusieurs niveaux de service
- Évolutivité dynamique sans interruption de l’application
- Haute disponibilité intégrée
- Protection des données

Toutes ces fonctionnalités ne nécessitent presque aucune administration, et toutes sont fournies sans coût supplémentaire. Ces fonctionnalités vous permettent de toofocus sur le développement rapide d’application et accélérer votre toomarket de temps, au lieu d’allouer beaucoup de temps et ressources toomanaging virtual machines et l’infrastructure. En outre, vous pouvez continuer toodevelop votre application avec hello ouvrir les outils de la source et la plate-forme de votre choix et livrer avec une vitesse hello et l’efficacité de vos activités professionnelles sans avoir toolearn nouvelles compétences. 

Cet article est une base de données de tooAzure introduction pour PostgreSQL principaux concepts et tooperformance connexes de fonctionnalités, l’évolutivité et la facilité de gestion. Consultez que ces rapide démarre tooget que vous avez démarré :

- [Création d’une instance d’Azure Database pour PostgreSQL à l’aide du portail Azure](quickstart-create-server-database-portal.md)
- [Créer une base de données Azure PostgreSQL à l’aide de hello CLI d’Azure](quickstart-create-server-database-azure-cli.md)

Pour accéder à des exemples Azure CLI et PowerShell, consultez :

- [Exemples Azure CLI pour base de données pour PostgreSQL](./sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a>Ajustez les performances et la mise à l'échelle sans interruption de service

Azure Database pour le service PostgreSQL propose actuellement deux niveaux de service : De base et Standard. Chaque niveau de service offre [différents niveaux de performances, les garanties d’e/s et les fonctionnalités](concepts-service-tiers.md) toosupport tooheavyweight légère des charges de travail de base de données. Vous pouvez créer votre première application sur un petit serveur pour euros quelques mois, puis [modifier le niveau de performance hello](scripts/sample-scale-server-up-or-down.md) au sein du service de niveau manuellement ou par programmation n’importe quel moment toomeet hello les besoins de votre solution. Pour cela, sans temps mort tooyour application ou un tooyour clients. Permet une évolutivité dynamique tootransparently de votre base de données répondre toorapidly la modification des besoins en ressources et vous permet de tooonly vous payez pour les ressources de hello que vous avez besoin lorsque vous en avez besoin.

## <a name="monitoring-and-alerting"></a>Surveillance et alerte
Comment vous décidez lorsque toodial haut et bas ? Vous utilisez l’analyse des performances intégrés hello et fonctionnalités, combinées avec des évaluations de performances hello basées sur des unités de calcul d’alerte. À l’aide de ces outils, vous pouvez rapidement évaluer l’impact de hello de montée en puissance de calcul des unités ou vers le bas en fonction de vos besoins de performances actuel ou prévu. Pour plus de détails, consultez [Options et performances d’Azure Database pour PostgrSQL : comprendre ce qui est disponible dans chaque niveau de service](./concepts-service-tiers.md).

## <a name="keep-your-app-and-business-running"></a>Votre application et votre activité ne s’arrêtent jamais
Avec un temps de disponibilité de 99,99 % (non disponible dans la version préliminaire), l’excellent contrat de niveau de service (SLA) d’Azure, soutenu par un réseau mondial de centres de données gérés par Microsoft, permet d’exécuter votre application 24 heures sur 24, 7 jours sur 7. Chaque base de données Azure pour PostgreSQL serveur, vous tirer parti de la sécurité intégrée, la tolérance de panne et protection des données que vous devriez autrement toobuy ou conception, générer et gérer. Base de données Azure pour PostgreSQL, chaque niveau de service offre un ensemble complet de fonctionnalités de continuité d’activité et les options que vous pouvez utiliser tooget haut et en cours d’exécution et reste de cette façon. Vous pouvez utiliser [point-à-temps restauration](howto-restore-server-portal.md) tooreturn un tooan de la base de données d’état précédemment, en remontant jusqu'à 35 jours. En outre, si le centre de données hello hébergeant vos bases de données connaît une panne, vous pouvez restaurer les bases de données à partir de copies géo-redondant des sauvegardes récentes.

## <a name="secure-your-data"></a>Sécurisez vos données
Les services de base de données Azure ont une tradition de sécurité des données qu’Azure Database pour PostgreSQL respecte avec des fonctionnalités qui limitent l’accès, protègent les données au repos et en mouvement, et vous aident à surveiller l’activité. Visitez hello [Azure Trust Center](https://www.microsoft.com/TrustCenter/Security/default.aspx) pour plus d’informations sur la sécurité de plateforme Azure.

Hello Azure de base de données PostgreSQL service utilise le chiffrement de stockage pour les données au repos. Chiffrement des données, y compris les sauvegardes sur disque (à l’exception de hello des fichiers temporaires créés par le moteur de hello lors de l’exécution de requêtes). service de Hello utilise le chiffrement AES 256 bits qui est inclus dans le chiffrement de stockage Azure, et les clés de hello sont générées par le système. Le chiffrement de stockage est toujours activé et ne peut pas être désactivé.

Par défaut, hello Azure de base de données PostgreSQL service est configuré toorequire [sécurité de connexion SSL](./concepts-ssl-connection-security.md) pour les données en mouvement réseau hello. Application des connexions SSL entre le serveur de base de données et de vos applications clientes vous aide à protéger contre les attaques de « l’homme au milieu de hello » en chiffrant les flux de données hello entre le serveur de hello et votre application.  Si vous le souhaitez, vous pouvez désactiver l’utilisation de SSL pour la connexion de service de base de données tooyour si votre application cliente ne prend pas en charge la connectivité SSL.

## <a name="next-steps"></a>Étapes suivantes
- Consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/postgresql/) pour les comparaisons de coût et les calculatrices de.
- Commencez par [créer votre première instance d’Azure Database pour PostgreSQL](./quickstart-create-server-database-portal.md).
- Créez votre première application Python, PHP, Ruby, C\#, Java, Node.js : [bibliothèques de connexions](./concepts-connection-libraries.md)
