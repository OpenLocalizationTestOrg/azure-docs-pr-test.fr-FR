---
title: "Créer une fonction Azure qui se connecte à une base de données Azure Cosmos DB | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une fonction Azure qui se connecte à une base de données Azure Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: cfowler
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: c2c3530df62a1f291be51739a7918f7b8ab08487
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a>Créer une fonction Azure Functions qui se connecte à une base de données Azure Cosmos DB

Cet exemple de script crée une Function App Azure et se connecte à une base de données Azure Cosmos DB.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article. Exécutez `az --version` pour trouver la version. Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Exemple de script

Cet exemple crée une Function App Azure et ajoute un point de terminaison et une clé d’accès Cosmos DB aux paramètres d’application.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes. Chaque commande du tableau renvoie à une documentation spécifique.

| Commande | Remarques |
|---|---|
| [az login](https://docs.microsoft.com/cli/azure/#login) | Connexion à Azure. |
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Crée un groupe de ressources avec un emplacement. |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account) | Créez un compte de stockage. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/functionapp#az_functionapp_create) | Crée une Function App. |
| [az documentdb create](https://docs.microsoft.com/cli/azure/documentdb#az_documentdb_create) | Crée une base de données DocumentDB. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#az_group_delete) | Nettoyer |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).




