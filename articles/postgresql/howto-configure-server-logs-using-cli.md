---
title: "journaux du serveur aaaConfigure et accès pour PostgreSQL à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit la façon dont les journaux du serveur de hello tooconfigure et d’accès dans la base de données Azure pour PostgreSQL à l’aide de la ligne de commande CLI d’Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configuration et accès aux journaux du serveur à l’aide de la ligne de commande Azure
Vous pouvez télécharger les journaux d’erreurs hello PostgreSQL server à l’aide de hello Interface de ligne de commande (CLI d’Azure). Toutefois, les journaux d’accès tootransaction n’est pas pris en charge. 

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un [serveur Azure Database pour PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) de ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Configuration de la journalisation pour Azure Database pour PostgreSQL
Vous pouvez configurer les journaux de requête tooaccess hello server et les journaux d’erreurs. Les journaux d’erreurs peuvent contenir des informations sur le nettoyage automatique, la connexion et les points de contrôle.
1. Activation de la journalisation
2. Journal de mise à jour\_instruction et journal\_min\_durée\_journalisation des requêtes tooenable instruction
3. Mise à jour de la période de rétention

Pour plus d’informations, consultez [Personnalisation des paramètres de configuration du serveur](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Répertorier les journaux pour le serveur Azure Database pour PostgreSQL
fichiers de journaux disponibles toolist hello pour votre serveur, exécutez hello [liste de journaux du serveur az postgres](/cli/azure/postgres/server-logs#list) commande.

Vous pouvez répertorier les fichiers de journaux hello pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup**et lui demander tooa texte fichier appelé **journal\_fichiers\_liste.txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Télécharger les journaux localement à partir du serveur de hello
Hello [téléchargement des journaux de serveur az postgres](/cli/azure/postgres/server-logs#download) commande vous permet de différents fichiers journaux individuels toodownload pour votre serveur. 

Cet exemple télécharge hello fichier journal spécifique pour le serveur de hello **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup** tooyour des environnement local.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Étapes suivantes
- toolearn en savoir plus sur les journaux du serveur, consultez [journaux du serveur de base de données PostgreSQL Azure](concepts-server-logs.md)
- Pour plus d’informations sur les paramètres du serveur, consultez la rubrique [Personnalisation des paramètres de configuration de serveur à l’aide de l’interface de ligne de commande Azure](howto-configure-server-parameters-using-cli.md)
