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
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Règles de pare-feu d’un serveur de base de données Azure pour PostgreSQL
Les pare-feu empêchent le serveur de base de données de tous les accès tooyour jusqu'à ce que vous spécifiez les ordinateurs sur lesquels l’autorisation. les pare-feu Hello accorde serveur toohello d’accès basé sur hello adresse IP de chaque demande d’origine.
tooconfigure votre pare-feu, vous créez des règles de pare-feu qui spécifient les plages d’adresses IP acceptables. Vous pouvez créer des règles de pare-feu au niveau du serveur hello.

**Règles de pare-feu :** ces règles permettent tooaccess de clients de votre base de données Azure entier pour PostgreSQL Server, autrement dit, toutes les bases de données hello dans hello même serveur logique. Les règles de pare-feu de niveau serveur peuvent être configurées à l’aide de hello portail Azure ou à l’aide des commandes CLI d’Azure. règles de pare-feu de niveau serveur toocreate, vous devez être propriétaire de l’abonnement hello ou un collaborateur de l’abonnement.

## <a name="firewall-overview"></a>Présentation du pare-feu
Base de données tous les accès tooyour Azure de base de données PostgreSQL serveur est bloqué par le pare-feu hello par défaut. toobegin à l’aide de votre serveur à partir d’un autre ordinateur, vous devez toospecify une ou plus au niveau du serveur pare-feu règles tooenable accès tooyour server. Utilisez toospecify de règles de pare-feu hello quelle adresse IP comprise entre hello Internet tooallow. Accès toohello Azure site Web du portail lui-même n’est pas affecté par les règles de pare-feu hello.
Les tentatives de connexion à partir de hello Internet et Azure doit traverser le pare-feu hello avant de pouvoir atteindre votre base de données PostgreSQL, comme indiqué dans hello suivant schéma :

![Flux d’exemple de fonctionnement du pare-feu de hello](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Connexion à partir de hello Internet
Les règles de pare-feu de niveau serveur s’appliquent à des bases de données tooall sur hello Azure de base de données PostgreSQL serveur. Si l’adresse IP de hello de demande de hello est dans une des plages de hello spécifiées dans les règles de pare-feu de niveau serveur hello, connexion de hello est accordée.
Si l’adresse IP de hello de demande de hello n’est pas dans les plages de hello spécifiées dans un des hello au niveau de la base de données ou règles de pare-feu de niveau serveur, demande de connexion hello échoue.
Par exemple, si votre application se connecte avec le pilote JDBC pour PostgreSQL, vous pouvez rencontrer cette erreur en essayant de tooconnect lorsque hello pare-feu ne bloque les connexions hello.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Gestion par programmation des règles de pare-feu
En outre toohello portail Azure, les pare-feu, les règles peuvent être gérés par programmation à l’aide de CLI d’Azure.
Consultez également la page [Créer et gérer les règles de pare-feu de la base de données Azure pour PostgreSQL à l’aide d’Azure CLI](howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-hello-database-firewall"></a>Dépannage du pare-feu de base de données hello
Tenez compte des hello lorsque toohello d’accès de base de données de Microsoft Azure pour service PostgreSQL Server ne se comporte pas comme prévu les points suivants :

* **Liste verte de modifications toohello n'ont pas encore entrées en vigueur :** il peut y avoir autant qu’un délai de cinq minutes pour change toohello base de données Azure pour effet de tootake de configuration de pare-feu PostgreSQL serveur.

* **la connexion Hello n’est pas autorisée ou un mot de passe incorrect a été utilisée :** si une connexion n’a pas les autorisations sur hello Azure de base de données PostgreSQL serveur hello ou un mot de passe utilisé est incorrect, hello toohello de connexion de base de données Azure pour PostgreSQL serveur est refusé. Création d’un paramètre de pare-feu fournit uniquement les clients avec un tooattempt opportunité connexion tooyour serveur ; chaque client doit fournir les informations d’identification de sécurité nécessaires hello.

Par exemple, à l’aide d’un client JDBC, hello l’erreur suivante peut apparaître.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"

* **Adresse IP dynamique :** si vous avez une connexion Internet avec adressage IP dynamique et que vous rencontrez des problèmes de mise en route à travers le pare-feu hello, vous pouvez tenter de hello suivant solutions :

* Demandez à votre fournisseur de Service Internet (ISP) pour la plage d’adresses IP hello affecté tooyour les ordinateurs clients que hello d’accès de la base de données Azure pour le serveur de PostgreSQL, puis ajoutez plage d’adresses IP hello en tant qu’une règle de pare-feu.

* Obtenir l’adressage IP statique à la place pour vos ordinateurs clients et ajoutez des adresses IP hello en tant que règles de pare-feu.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations sur la création de règles de pare-feu au niveau du serveur et au niveau de la base de données, consultez les articles suivants :
* [Créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure](howto-manage-firewall-using-portal.md)
* [Créer et gérer des règles de pare-feu de la base de données Azure pour PostgreSQL à l’aide d’Azure CLI](howto-manage-firewall-using-cli.md)