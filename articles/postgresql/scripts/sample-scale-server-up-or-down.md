---
title: "AAA » CLI Azure à l’échelle Script Azure base de données PostgreSQL | Documents Microsoft »"
description: "Exemple de Script Azure CLI - la mise à l’échelle de la base de données Azure pour le niveau de performance différents PostgreSQL serveur tooa après interrogation de métriques de hello."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 678b28941dbb4334cb374d4888991a00b44966b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-scale-a-single-postgresql-server-using-azure-cli"></a>Surveiller et mettre à l’échelle d’un seul serveur PostgreSQL à l’aide de la CLI Azure
Cet exemple de script CLI met à l’échelle une base de données Azure unique pour le niveau de performance différents PostgreSQL serveur tooa après interrogation de métriques de hello. 

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Exemple de script
Dans cet exemple de script, modifiez hello mis en surbrillance lignes toocustomize hello admin username et password. Remplacez l’id d’abonnement hello utilisée dans les commandes de moniteur hello az avec votre propre id d’abonnement.[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/scale-postgresql-server.sh?highlight=15-16 "Create and scale Azure Database for PostgreSQL.")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement
Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/scale-postgresql-server/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a>Explication du script
Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| **Commande** | **Remarques** |
|---|---|
| [az group create](/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az postgres server create](/cli/azure/postgres/server#create) | Crée un serveur PostgreSQL qui héberge les bases de données hello. |
| [az monitor metrics list](/cli/azure/monitor/metrics#list) | Liste hello valeur métrique pour les ressources de hello. |
| [az group delete](/cli/azure/group#delete) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes
- En savoir plus sur hello CLI d’Azure : [documentation CLI d’Azure](/cli/azure/overview)
- Essayer des scripts supplémentaires : [Exemples Azure CLI pour Base de données Azure pour PostgreSQL](../sample-scripts-azure-cli.md)
- En savoir plus sur la mise à l’échelle : [Niveaux de service](../concepts-service-tiers.md) et [Unités de calcul et de stockage](../concepts-compute-unit-and-storage.md)
