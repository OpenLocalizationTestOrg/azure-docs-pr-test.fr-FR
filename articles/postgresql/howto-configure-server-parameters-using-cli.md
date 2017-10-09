---
title: "paramètres de service aaaConfigure hello dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Cet article décrit comment les paramètres de service hello tooconfigure dans la base de données Azure pour l’utilisation de PostgreSQL hello ligne de commande CLI d’Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a>Personnalisation des paramètres de configuration du serveur à l’aide de l’interface de ligne de commande Azure
Vous pouvez répertorier, afficher et mettre à jour les paramètres de configuration pour un serveur Azure PostgreSQL à l’aide de hello Interface de ligne de commande (CLI d’Azure). Toutefois, un seul sous-ensemble de configurations de moteur est exposé au niveau du serveur et peut être modifié. 

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un serveur et une base de données [Création d’une base de données Azure POUR PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a>Répertorier les paramètres de configuration de Base de données Azure pour le serveur PostgreSQL
l’exécution de tous les paramètres modifiables dans un serveur et leurs valeurs, toolist hello [liste de configuration du serveur az postgres](/cli/azure/postgres/server/configuration#list) commande.

Vous pouvez répertorier les paramètres de configuration de serveur hello pour le serveur de hello **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup**.
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a>Affichage des détails des paramètres de configuration du serveur
tooshow plus d’informations sur un paramètre de configuration particulière pour un serveur, exécutez hello [afficher de configuration serveur az postgres](/cli/azure/postgres/server/configuration#show) commande.

Cet exemple affiche les détails de hello **journal\_min\_messages** paramètre de configuration du serveur pour le serveur **mypgserver-20170401.postgres.database.azure.com** sous groupe de ressources **myresourcegroup.**
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a>Modification de la valeur de paramètre de configuration du serveur
Vous pouvez également modifier la valeur hello un certain paramètre de configuration du serveur, et cela met à jour la valeur de configuration sous-jacente hello pour le moteur de serveur hello PostgreSQL. hello d’utilisation tooupdate hello configuration [jeu de configuration de serveur az postgres](/cli/azure/postgres/server/configuration#set) commande. 

tooupdate hello **journal\_min\_messages** paramètre de configuration du serveur du serveur **mypgserver-20170401.postgres.database.azure.com** sous le groupe de ressources **myresourcegroup.**
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
Si vous voulez la valeur de hello tooreset d’un paramètre de configuration, vous choisissez simplement tooleave out hello facultatif `--value` paramètre et le service hello seront applique par défaut hello. Dans l’exemple ci-dessus, elle peut se présenter comme suit :
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
Cette action réinitialisera hello **journal\_min\_messages** valeur par défaut de configuration toohello **avertissement**. Pour plus d’informations sur la configuration du serveur et les valeurs autorisées, consultez la documentation PostgreSQL à la rubrique [Configuration du serveur](https://www.postgresql.org/docs/9.6/static/runtime-config.html).

## <a name="next-steps"></a>Étapes suivantes
- journaux du serveur tooconfigure et l’accès, consultez [journaux du serveur de base de données PostgreSQL Azure](concepts-server-logs.md)
