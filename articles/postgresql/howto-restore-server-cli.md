---
title: "Comment tooback et restaurer un serveur de base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Découvrez comment tooback haut et restaurer un serveur de base de données Azure pour PostgreSQL à l’aide de hello CLI d’Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Comment tooback des et restaurer un serveur de base de données Azure pour PostgreSQL à l’aide de hello CLI d’Azure

Utilisez base de données Azure pour PostgreSQL toorestore un tooan de base de données de serveur date antérieure qui s’étend du too35 des 7 derniers jours.

## <a name="prerequisites"></a>Composants requis
toocomplete cette procédure-tooguide, vous devez :
- Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Si vous installez et utilisez hello CLI d’Azure localement, cette procédure-tooguide nécessite que vous utilisez Azure CLI 2.0 ou version ultérieure. version de hello tooconfirm, à l’invite de commande CLI d’Azure hello, entrez `az --version`. tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>La sauvegarde s’effectue automatiquement
Lorsque vous utilisez la base de données Azure pour PostgreSQL, service de base de données hello effectue automatiquement une sauvegarde du service de hello toutes les 5 minutes. 

Pour le niveau de base, les sauvegardes de hello sont disponibles pendant 7 jours. Pour le niveau Standard, les sauvegardes de hello sont disponibles pour des 35 derniers jours. Pour plus d’informations, consultez [Niveaux tarifaires dans Base de données Azure pour PostgreSQL](concepts-service-tiers.md).

Avec cette fonctionnalité de sauvegarde automatique, vous pouvez restaurer les serveur hello et son tooan de bases de données de date antérieure, ou point dans le temps.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Restaurer un état antérieur de tooa de base de données dans le temps à l’aide de hello CLI d’Azure
Utiliser la base de données Azure pour point précédent tooa de serveur hello PostgreSQL toorestore dans le temps. les données de salutation restaurée sont tooa copié un nouveau serveur, et serveur existant de hello demeure en l’état. Par exemple, si une table est supprimée par inadvertance à midi aujourd'hui, vous pouvez restaurer le temps toohello juste avant midi. Ensuite, vous pouvez récupérer hello manquant de table et les données à partir de la copie restaurée de hello du serveur de hello. 

serveur de hello toorestore, utilisez hello CLI d’Azure [restauration du serveur az postgres](/cli/azure/postgres/server#restore) commande.

### <a name="run-hello-restore-command"></a>Exécutez la commande de restauration hello

serveur de hello toorestore, à l’invite de commande CLI d’Azure hello, entrez hello de commande suivante :

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` commande nécessite hello paramètres suivants :
| Paramètre | Valeur suggérée | Description  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  Le groupe de ressources dans lequel le serveur de source de hello existe.  |
| name | mypgserver-restored | nom Hello hello nouveau serveur qui est créé par la commande de restauration hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Sélectionnez un point dans toorestore de temps à. Cette date / heure doivent être dans hello du serveur source dans une période de rétention. Utilisez le format de date et d’heure hello ISO8601. Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`. Vous pouvez également utiliser hello UTC Zoulou mettre en forme, par exemple, `2017-04-13T13:59:00Z`. |
| source-server | mypgserver-20170401 | nom de Hello ou ID de hello toorestore de serveur source à partir de. |

Lorsque vous restaurez un serveur tooan point antérieur dans le temps, un nouveau serveur est créé. serveur d’origine de Hello et ses bases de données à partir de hello spécifié de point dans le temps sont copiés toohello nouveau serveur.

valeurs de niveau de Hello emplacement et la tarification pour le serveur hello restauré sont toujours hello même en tant que serveur d’origine de hello. 

Hello `az postgres server restore` commande est synchrone. Après que hello serveur est restauré, vous pouvez l’utiliser à nouveau processus de hello toorepeat pour un autre point dans le temps. 

Après avoir hello se termine le processus de restauration, recherche hello nouveau serveur et vérifier que les données de salutation sont restaurées comme prévu.

## <a name="next-steps"></a>Étapes suivantes
[Bibliothèques de connexions pour Azure Database pour PostgreSQL](concepts-connection-libraries.md)
