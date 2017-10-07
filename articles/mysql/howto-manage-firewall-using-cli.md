---
title: "aaaCreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit comment toocreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de la ligne de commande CLI d’Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a>Création et gestion des règles de pare-feu Azure Database pour MySQL à l’aide de l’interface de ligne de commande Azure
Les règles de pare-feu de niveau serveur activer administrateurs toomanage accès tooan base de données Azure pour MySQL Server à partir d’une adresse IP spécifique ou de la plage d’adresses IP. À l’aide des commandes CLI d’Azure pratiques, vous pouvez créer, mettre à jour, supprimer, répertorier et afficher toomanage de règles de pare-feu de votre serveur. Pour une vue d’ensemble des pare-feu Azure Database pour MySQL, consultez la rubrique [Règles de pare-feu d’Azure Database pour MySQL](./concepts-firewall-rules.md)

## <a name="prerequisites"></a>Composants requis
* [Installation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)
* Installation du Kit de développement logiciel (SDK) Python pour les services PostgreSQL et MySQL
* Installer le composant de CLI d’Azure hello pour les services PostgreSQL et MySQL
* Créer un serveur de base de données Azure pour MySQL

## <a name="firewall-rule-commands"></a>Commandes des règles de pare-feu :
Hello **az mysql server-règle de pare-feu** commande est utilisée à partir d’Azure CLI toocreate, supprimer, répertorier, afficher et mettre à jour les règles de pare-feu.

Commandes :
- **create** : créez une règle de pare-feu du serveur Azure MySQL.
- **delete** : supprimez une règle de pare-feu du serveur Azure MySQL.
- **liste** : liste des règles de pare-feu de serveur MySQL de Azure hello.
- **afficher** : afficher les détails de hello d’un serveur MySQL de Azure règle de pare-feu.
- **update**: mettez à jour une règle de pare-feu du serveur Azure MySQL.

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a>Connexion tooAzure liste et votre base de données Azure pour serveurs MySQL
Connectez-vous en toute sécurité à votre compte Azure à l’aide de l’interface de ligne de commande Azure. Hello d’utilisation **ouverture de session az** commande toodo cela.

1. Exécutez hello de commande suivante à partir de la ligne de commande hello.
```azurecli
az login
```
Cette commande génère un code toouse à l’étape suivante de hello.

2. Utiliser une page hello navigateur tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) et entrez le code de hello.

3. À l’invite de hello, connectez-vous en utilisant vos informations d’identification Azure.

4. Une fois que votre connexion est autorisée, une liste des abonnements est imprimée dans la console hello. Id du hello Hello souhaité abonnement tooset hello actuel abonnement toobe utilisé progresser.
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. Si vous ne connaissez pas les noms de hello de liste hello bases de données Azure pour les serveurs MySQL pour votre groupe d’abonnement et de ressources.

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   Notez attribut nom hello Bonjour répertoriant, qui sera utilisé toospecify le toowork de serveur MySQL sur. Si nécessaire, vérifiez les détails de hello pour ce serveur toousing hello attribut tooconfirm nom est correct :

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a>Répertorier les règles de pare-feu d’un serveur Azure Database pour MySQL 
À l’aide du nom du serveur hello et nom du groupe de ressources de hello, liste hello serveur règles de pare-feu existantes sur le serveur de hello. Notez cet attribut de nom de serveur hello est spécifié dans hello **--serveur** basculer et pas hello **--nom** basculer.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
sortie de Hello répertorie les règles hello si elle existe, par défaut au format JSON de format. Vous pouvez utiliser le commutateur de hello **--table de sortie** pour un format plus lisible de la table en tant que sortie de hello.
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a>Création d’une règle de pare-feu d’un serveur Azure Database pour MySQL
Nom du serveur MySQL de Azure hello et nom de groupe de ressources hello, créez une règle de pare-feu sur le serveur de hello. Fournissez un nom pour la règle hello, adresse IP de début hello et IP de fin pour hello règle toocover un accès de tooallow adresses plage IP.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
Pour une adresse IP au singulier d’adresses toobe autorisé à accéder, fournissez hello la même adresse que hello IP de début et l’adresse IP de fin, comme dans cet exemple.
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez créé, par défaut au format JSON. En cas de panne, sortie de hello afficher texte du message d’erreur à la place.

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a>Mise à jour d’une règle de pare-feu d’un serveur Azure Database pour MySQL 
À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, mettre à jour une règle de pare-feu existante sur le serveur de hello. Fournir le nom hello de règle de pare-feu existante hello comme entrée et tooupdate par démarrer hello IP et de fin attributs IP.
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez mis à jour, par défaut au format JSON. En cas de panne, sortie de hello afficher texte du message d’erreur à la place.

> [!NOTE]
> Si la règle de pare-feu hello n’existe pas, il sera créé par la commande de mise à jour hello.

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a>Affichage des détails d’une règle de pare-feu d’un serveur Azure Database pour MySQL
À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, afficher les détails de règle de pare-feu existante hello du serveur de hello. Fournissez le nom hello de règle de pare-feu existante hello comme entrée.
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez spécifié, par défaut au format JSON. En cas de panne, sortie de hello afficher texte du message d’erreur à la place.

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a>Suppression d’une règle de pare-feu d’un serveur Azure Database pour MySQL
À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, supprimez une règle de pare-feu existante du serveur de hello. Fournir le nom hello hello existant de règle de pare-feu.
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
En cas de réussite, aucun résultat ne s’affiche. En cas d’échec, le texte de message d’erreur hello est retourné.

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur les [règles de pare-feu du serveur Azure Database pour MySQL](./concepts-firewall-rules.md)
- [Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure](./howto-manage-firewall-using-portal.md)
