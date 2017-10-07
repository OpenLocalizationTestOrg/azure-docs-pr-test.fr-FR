---
title: "aaaServer enregistre dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Génère des journaux des requêtes et des erreurs dans la base de données Azure pour PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Journaux de serveur dans une base de données Azure pour PostgreSQL 
La base de données Azure pour PostgreSQL génère des journaux des requêtes et des erreurs. Toutefois, les journaux d’accès tootransaction n’est pas pris en charge. Ces journaux peuvent être utilisé tooidentify, dépanner et réparer les erreurs de configuration et des performances optimales. Pour plus d’informations, consultez la page [Signalement et journalisation des erreurs](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Accéder aux journaux du serveur
Vous pouvez répertorier et télécharger les journaux d’erreurs Azure PostgreSQL server à l’aide de hello portail Azure, [CLI d’Azure](howto-configure-server-logs-using-cli.md) et l’API REST Azure.

## <a name="log-retention"></a>Rétention des journaux
Vous pouvez définir la période de rétention hello pour les journaux système à l’aide de la **journal\_rétention\_période** paramètre associé à votre serveur. unité de Hello pour ce paramètre est en jours (peut-être tooconfirm). valeur par défaut de Hello est de trois jours. valeur maximale de Hello est de 7 jours. Notez que votre serveur doit posséder suffisamment fichiers journaux de stockage alloué toocontain hello conservée.
les fichiers journaux Hello pivote chaque 1 heure ou la taille de 100 Mo, selon ce qui se produit en premier.

## <a name="configure-logging-for-azure-postgresql-server"></a>Configurer la journalisation pour le serveur PostgreSQL Azure
Vous pouvez activer la journalisation des requêtes et des erreurs pour votre serveur. Les journaux des erreurs peuvent contenir des informations sur le nettoyage automatique, la connexion et les points de contrôle.

Vous pouvez activer la journalisation des requêtes pour votre instance de base de données PostgreSQL en définissant deux paramètres de serveur : log\_statement et log\_min\_duration\_statement.

Hello **journal\_instruction** paramètre contrôle les instructions SQL sont enregistrées. Nous vous recommandons de définir ce paramètre trop***tous les*** toolog toutes les instructions ; la valeur par défaut de hello est none (peut-être tooconfirm).

Hello **journal\_min\_durée\_instruction** paramètre définit la limite de hello en millisecondes d’un toobe instruction connecté. Toutes les instructions SQL qui s’exécutent plus longtemps que la valeur du paramètre hello sont enregistrées. Ce paramètre est désactivé et défini toominus 1 (-1) par défaut (tooconfirm nécessaire). Il peut être utile d’activer ce paramètre pour dépister les requêtes non optimisées dans vos applications.

Hello **journal\_min\_messages** vous permet de toocontrol les niveaux de message sont écrits les journaux du serveur toohello. valeur par défaut Hello est un avertissement. (peut-être tooconfirm)

Pour plus d’informations sur ces paramètres, consultez la documentation [Signalement et journalisation des erreurs](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html). En particulier, pour configurer les paramètres du serveur de base de données Azure pour PostgreSQL, consultez la page [Journaux du serveur de base de données Azure pour PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Étapes suivantes
- les journaux de tooaccess à l’aide d’interface de ligne de commande CLI d’Azure, consultez [configurer et l’accès aux journaux du serveur à l’aide de CLI d’Azure](howto-configure-server-logs-using-cli.md)
- Pour plus d’informations sur les paramètres du serveur, consultez la rubrique [Personnaliser les paramètres de configuration de serveur à l’aide d’Azure CLI](howto-configure-server-parameters-using-cli.md).