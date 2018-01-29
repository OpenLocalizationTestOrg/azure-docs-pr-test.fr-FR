---
title: "Règles de pare-feu d’un serveur de base de données Azure pour PostgreSQL | Microsoft Docs"
description: "Décrit les règles de pare-feu d’un serveur de base de données Azure pour PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/03/2017
ms.openlocfilehash: 7fec71f621ffeff2fc42a5a9464ae9011b2e2fee
ms.sourcegitcommit: 38c9176c0c967dd641d3a87d1f9ae53636cf8260
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Règles de pare-feu d’un serveur de base de données Azure pour PostgreSQL
Le pare-feu Azure Database pour PostgreSQL empêche tout accès à votre serveur de base de données jusqu’à ce que vous spécifiiez les ordinateurs qui disposent d’autorisations. Le pare-feu octroie l’accès au serveur en fonction de l’adresse IP d’origine de chaque demande.
Pour configurer votre pare-feu, vous créez des règles de pare-feu qui spécifient les plages d’adresses IP acceptables. Vous pouvez créer des règles de pare-feu au niveau du serveur.

**Règles de pare-feu :** ces règles permettent aux clients d’accéder à l’ensemble de votre serveur de base de données Azure pour PostgreSQL, c’est-à-dire à toutes les bases de données qui se trouvent sur le même serveur logique. Les règles de pare-feu au niveau du serveur peuvent être configurées en utilisant le Portail Azure ou des commandes d’Azure CLI. Pour créer des règles de pare-feu au niveau du serveur, vous devez être le propriétaire de l’abonnement ou collaborateur.

## <a name="firewall-overview"></a>Présentation du pare-feu
Par défaut, tous les accès au serveur de base de données Azure pour PostgreSQL sont bloqués par le pare-feu. Pour pouvoir utiliser votre serveur à partir d’un autre ordinateur, vous devez spécifier une ou plusieurs règles de pare-feu au niveau du serveur afin de permettre l’accès à votre serveur. Utilisez les règles de pare-feu pour spécifier les plages d’adresses IP d’Internet à autoriser. L’accès au site web du Portail Azure proprement dit n’est pas affecté par les règles de pare-feu.
Les tentatives de connexion à partir d’Internet et d’Azure doivent franchir le pare-feu pour pouvoir atteindre votre base de données PostgreSQL, comme l’illustre le diagramme suivant :

![Exemple de flux de fonctionnement du pare-feu](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a>Connexion à partir d’Internet
Les règles de pare-feu au niveau du serveur s’appliquent à toutes les bases de données qui se trouvent sur le même serveur Azure Database pour PostgreSQL. Si l’adresse IP de la demande appartient à une des plages spécifiées dans les règles de pare-feu au niveau du serveur, la connexion est accordée.
Si l’adresse IP de la demande n’appartient pas aux plages spécifiées dans une règle de pare-feu au niveau du serveur, la demande de connexion échoue.
Par exemple, si votre application se connecte au pilote JDBC pour PostgreSQL, il se peut que vous rencontriez cette erreur au cours de la tentative de connexion, si le pare-feu la bloque.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Gestion par programmation des règles de pare-feu
En dehors du Portail Azure, les règles de pare-feu peuvent être gérées par programmation à l’aide d’Azure CLI.
Consultez également la page [Créer et gérer les règles de pare-feu de la base de données Azure pour PostgreSQL à l’aide d’Azure CLI](howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-the-database-server-firewall"></a>Dépannage du pare-feu du serveur de base de données
Considérez les points suivants quand l’accès au service de serveur de base de données Microsoft Azure pour PostgreSQL présente un comportement anormal :

* **Les modifications apportées à la liste d’approbation n’ont pas encore pris effet :** jusqu’à cinq minutes peuvent s’écouler avant que les modifications apportées à la configuration du pare-feu du serveur de base de données Azure pour PostgreSQL ne soient effectives.

* **La connexion n’est pas autorisée ou un mot de passe incorrect a été utilisé :** si une connexion n’a pas d’autorisations sur le serveur de base de données Azure pour PostgreSQL ou que le mot de passe est incorrect, la connexion au serveur de base de données Azure pour PostgreSQL est refusée. Créer un paramètre de pare-feu permet uniquement aux clients de tenter de se connecter à votre serveur ; chaque client doit tout de même fournir les informations d’identification de sécurité nécessaires.

Par exemple, avec un client JDBC, l’erreur suivante est susceptible d’apparaître.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"

* **Adresse IP dynamique :** si vous avez une connexion Internet avec adressage IP dynamique et que le pare-feu demeure infranchissable, vous pouvez essayer une des solutions suivantes :

* Demandez à votre fournisseur de services Internet (ISP) la plage d’adresses IP affectée à vos ordinateurs clients qui accèdent au serveur de base de données Azure pour PostgreSQL, puis ajoutez cette plage dans une règle de pare-feu.

* Obtenez un adressage IP statique à la place pour vos ordinateurs clients, puis ajoutez l’adresse IP statique en tant que règle de pare-feu.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations sur la création de règles de pare-feu au niveau du serveur, consultez les articles suivants :
* [Créer et gérer des règles de pare-feu d’Azure Database pour PostgreSQL à l’aide du portail Azure](howto-manage-firewall-using-portal.md)
* [Créer et gérer des règles de pare-feu d’Azure Database pour PostgreSQL à l’aide d’Azure CLI](howto-manage-firewall-using-cli.md)
