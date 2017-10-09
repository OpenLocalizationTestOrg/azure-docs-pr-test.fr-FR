---
title: "concepts d’aaaServer dans la base de données Azure pour MySQL | Documents Microsoft"
description: "Cette rubrique propose des considérations et des instructions relatives à l’utilisation des serveurs de base de données Azure pour MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>Concepts de serveur dans une base de données Azure pour MySQL
Cette rubrique propose des considérations et des instructions relatives à l’utilisation des serveurs de base de données Azure pour MySQL.

## <a name="what-is-an-azure-database-for-mysql-server"></a>Qu’est-ce qu’un serveur de base de données Azure pour MySQL ?

Un serveur de base de données Azure pour MySQL est un point d’administration central pour plusieurs bases de données. Il s’agit de hello même construction de serveur MySQL que vous connaissez peut-être dans Bonjour tout le monde sur site. Plus précisément, hello Azure de base de données pour le service MySQL est géré, fournit des garanties de performances, expose les fonctionnalités d’accès et au niveau serveur.

Un serveur de base de données Azure pour MySQL :

- est créé dans un abonnement Azure ;
- Est la ressource parent de hello pour les bases de données.
- fournit un espace de noms aux bases de données ;
- Est un conteneur avec la sémantique de durée de vie fort - supprimer un serveur et supprime les bases de données hello contenu.
- colocalise les ressources d’une région ;
- fournit un point de terminaison de connexion pour l’accès au serveur et aux bases de données ;
- Fournit la portée hello pour les stratégies de gestion qui s’appliquent les bases de données tooits : connexion, le pare-feu, les utilisateurs, rôles, configurations, etc..
- est disponible dans plusieurs versions (pour plus d’informations, consultez la page [Versions prises en charge des bases de données Azure pour MySQL](./concepts-supported-versions.md)) ;

Dans un serveur Azure Database pour MySQL, vous pouvez créer une ou plusieurs bases de données. Vous pouvez choisir toocreate une base de données par serveur tooutilize toutes les ressources hello ou créer plusieurs bases de données tooshare les ressources hello. Hello est structuré par serveur, en fonction de la configuration de hello du niveau de tarification, calculer les unités de stockage (Go). Pour plus d’informations, consultez [Niveaux tarifaires](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>Comment se connecter et s’authentifier tooan base de données Azure pour le serveur MySQL ?

Hello éléments suivants permettent de garantir de base de données tooyour d’accès sécurisé.

|||
| :-- | :-- |
| **Authentification et autorisation** | Le serveur de base de données Azure pour MySQL prend en charge l’authentification MySQL native. Vous pouvez connecter et s’authentifier tooserver avec ouverture de session du serveur hello admin. |
| **Protocole** | service de Hello prend en charge un protocole de message utilisé par MySQL. |
| **TCP/IP** | protocole de Hello est pris en charge sur TCP/IP et via des sockets Unix-domaine. |
| **Pare-feu** | toohelp protéger vos données, une règle de pare-feu empêche le serveur de base de données de tous les accès tooyour ou bases de données de tooits, jusqu'à ce que vous spécifiez les ordinateurs qui ont des autorisations. Consultez la page [Règles de pare-feu d’un serveur de base de données Azure pour MySQL](./concepts-firewall-rules.md). |
| **SSL** | service de Hello prend en charge la mise en œuvre des connexions SSL entre vos applications et votre serveur de base de données.  Consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](./howto-configure-ssl.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Comment gérer un serveur ?
Vous pouvez gérer des base de données Azure pour serveurs MySQL à l’aide de hello portail Azure ou hello CLI d’Azure.

## <a name="next-steps"></a>Étapes suivantes
- Pour une vue d’ensemble du service de hello, consultez [base de données Azure pour une vue d’ensemble de MySQL](./overview.md)
- Pour plus d’informations sur les quotas de ressources et les limitations associés à votre **niveau de service**, consultez la page [Niveaux de service](./concepts-service-tiers.md).
- Pour plus d’informations sur la connexion toohello service, consultez [des bibliothèques de connexions de base de données Azure pour MySQL](./concepts-connection-libraries.md).
