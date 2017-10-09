---
title: "aaaServer les concepts de base de données PostgreSQL Azure | Documents Microsoft"
description: "Cette rubrique propose des considérations et des instructions relatives à l’utilisation des serveurs de base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Serveurs de base de données Azure pour PostgreSQL
Cette rubrique propose des considérations et des instructions relatives à l’utilisation des serveurs de base de données Azure pour PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Qu’est-ce qu’un serveur de base de données Azure pour PostgreSQL ?
Un serveur de base de données Azure pour PostgreSQL est un point d’administration central pour plusieurs bases de données. Il s’agit de hello même construction serveur PostgreSQL que vous connaissez peut-être dans Bonjour tout le monde sur site. Plus précisément, hello PostgreSQL service géré, fournit des garanties de performances, expose les fonctionnalités d’accès et au niveau serveur.

Un serveur de base de données Azure pour PostgreSQL :

- est créé dans un abonnement Azure ;
- Est la ressource parent de hello pour les bases de données.
- fournit un espace de noms aux bases de données ;
- Est un conteneur avec la sémantique de durée de vie fort - supprimer un serveur et supprime les bases de données hello contenu.
- colocalise les ressources d’une région ;
- fournit un point de terminaison de connexion pour l’accès au serveur et aux bases de données (.postgresql.database.azure.com) ;
- Fournit la portée hello pour les stratégies de gestion qui s’appliquent les bases de données tooits : connexion, le pare-feu, les utilisateurs, rôles, configurations, etc..
- est disponible dans plusieurs versions (pour plus d’informations, consultez la page [Versions prises en charge des bases de données PostgreSQL](concepts-supported-versions.md)) ;
- peut être étendu par les utilisateurs (pour plus d’informations, consultez la page [Extensions de PostgreSQL](concepts-extensions.md)).

Dans une base de données Azure Database pour serveur PostgreSQL, vous pouvez créer une ou plusieurs bases de données. Vous pouvez choisir toocreate une base de données par serveur tooutilize toutes les ressources hello ou créer plusieurs bases de données tooshare les ressources hello. Hello est structuré par serveur, en fonction de la configuration de hello du niveau de tarification, calculer les unités de stockage (Go). Pour plus d’informations, consultez [Niveaux tarifaires](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Comment se connecter et s’authentifier tooan Azure de base de données PostgreSQL serveur ?
Hello éléments suivants permettent de garantir de base de données tooyour d’accès sécurisé.

|||
| :-- | :-- |
| **Authentification et autorisation** | Le serveur de base de données Azure pour PostgreSQL prend en charge l’authentification PostgreSQL native. Vous pouvez connecter et s’authentifier tooserver avec ouverture de session du serveur hello admin. |
| **Protocole** | service de Hello prend en charge un protocole de message utilisé par PostgreSQL. |
| **TCP/IP** | protocole de Hello est pris en charge sur TCP/IP et via des sockets Unix-domaine. |
| **Pare-feu** | toohelp protéger vos données, une règle de pare-feu empêche le serveur de base de données de tous les accès tooyour ou bases de données de tooits, jusqu'à ce que vous spécifiez les ordinateurs qui ont des autorisations. Consultez la page [Règles de pare-feu d’un serveur de base de données Azure pour PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Comment gérer un serveur ?
Vous pouvez gérer la base de données Azure pour serveurs PostgreSQL à l’aide de hello portail Azure ou hello [CLI d’Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Étapes suivantes
- Pour une vue d’ensemble du service de hello, consultez [base de données Azure pour une vue d’ensemble de PostgreSQL](overview.md)
- Pour plus d’informations sur les quotas de ressources et les limitations associés à votre **niveau de service**, consultez la page [Niveaux de service](concepts-service-tiers.md).
- Pour plus d’informations sur la connexion toohello service, consultez [des bibliothèques de connexions de base de données Azure pour PostgreSQL](concepts-connection-libraries.md).
