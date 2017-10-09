---
title: "aaaCreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit comment toocreate et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de la ligne de commande CLI d’Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a>Création et gestion des règles de pare-feu Azure Database pour PostgreSQL à l’aide de l’interface de ligne de commande Azure
Les règles de pare-feu de niveau serveur activer administrateurs toomanage accès tooan Azure de base de données PostgreSQL serveur à partir d’une adresse IP spécifique ou de la plage d’adresses IP. À l’aide des commandes CLI d’Azure pratiques, vous pouvez créer, mettre à jour, supprimer, répertorier et afficher toomanage de règles de pare-feu de votre serveur. Pour une vue d’ensemble des pare-feu Azure Database pour PostgreSQL, consultez la rubrique [Règles de pare-feu d’un serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)

## <a name="prerequisites"></a>Composants requis
toostep via ce tooguide de procédure, vous devez :
- Un [serveur Azure Database pour PostgreSQL et une base de données](quickstart-create-server-database-azure-cli.md)
- Installer [Azure CLI 2.0](/cli/azure/install-azure-cli) ligne de commande utilitaires ou utilisez hello Azure Cloud Shell dans le navigateur de hello.

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a>Configuration des règles de pare-feu pour Azure Database pour PostgreSQL
Hello [az postgres server-règle de pare-feu](/cli/azure/postgres/server/firewall-rule) commandes sont des règles de pare-feu tooconfigure utilisé.

## <a name="list-firewall-rules"></a>Répertorier les règles de pare-feu 
existant de hello toolist règles de pare-feu du serveur sur le serveur de hello, exécutez hello [liste de règle de pare-feu du serveur az postgres](/cli/azure/postgres/server/firewall-rule#list) commande.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
sortie de Hello répertorie les règles de hello si elle existe, par défaut au format JSON de format. Vous pouvez utiliser le commutateur de hello `--output table` pour un format plus lisible de la table en tant que sortie de hello.
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a>Créer une règle de pare-feu
toocreate une règle de pare-feu sur le serveur hello, exécutez hello [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) commande. 

Cet exemple permet à une plage de tous les IP adresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
tooallow un tooaccess d’adresse IP au singulier, fournir hello la même adresse que hello IP de début et l’adresse IP de fin, comme dans cet exemple.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez créé, par défaut au format JSON. En cas de panne, hello sortie showserror texte du message à la place.

## <a name="update-firewall-rule"></a>Mettre à jour une règle de pare-feu 
Mettre à jour une règle de pare-feu existante sur l’utilisation de serveur hello [mise à jour des règles de pare-feu serveur postgres az](/cli/azure/postgres/server/firewall-rule#update) commande. Fournir le nom hello de règle de pare-feu existante hello comme entrée et tooupdate par démarrer hello IP et de fin attributs IP.
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez mis à jour, par défaut au format JSON. En cas de panne, hello sortie showserror texte du message à la place.
> [!NOTE]
> Si la règle de pare-feu hello n’existe pas, il est créé par la commande de mise à jour hello.

## <a name="show-firewall-rule-details"></a>Afficher les détails d’une règle de pare-feu
Vous pouvez également afficher des détails de la règle pour un serveur de pare-feu existant hello en exécutant [afficher de règle de pare-feu serveur az postgres](/cli/azure/postgres/server/firewall-rule#show) commande.
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
En cas de réussite, sortie de la commande hello répertorie hello hello de règle de pare-feu que vous avez spécifié, par défaut au format JSON. En cas de panne, hello sortie showserror texte du message à la place.

## <a name="delete-firewall-rule"></a>Supprimer une règle de pare-feu
accès toorevoke pour une plage IP du serveur de hello, supprimer une règle de pare-feu existante en exécutant hello [az postgres server-règle de pare-feu supprimer](/cli/azure/postgres/server/firewall-rule#delete) commande. Fournir le nom hello hello existant de règle de pare-feu.
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
En cas de réussite, aucun résultat ne s’affiche. En cas d’échec, le texte de message d’erreur hello est retourné.

## <a name="next-steps"></a>Étapes suivantes
- De même, vous pouvez utiliser un navigateur web trop[créer et gérer la base de données Azure PostgreSQL aux règles de pare-feu à l’aide de hello portail Azure](howto-manage-firewall-using-portal.md)
- En savoir plus sur les [règles de pare-feu du serveur Azure Database pour PostgreSQL](concepts-firewall-rules.md)
- Pour la connexion tooan Azure de base de données PostgreSQL serveur, consultez [bibliothèques de connexions de base de données Azure pour PostgreSQL](concepts-connection-libraries.md)
