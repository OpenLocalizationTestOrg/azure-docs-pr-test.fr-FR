---
title: aaaAzure exemple de Script CLI - ajouter une Application de traitement par lots | Documents Microsoft
description: "Exemple de script Azure CLI - Ajout d’une application dans Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Ajout d’applications tooAzure lot avec CLI d’Azure

Ce script montre comment tooset d’une application pour une utilisation avec un pool Azure Batch ou une tâche. tooset d’une application, empaqueter votre fichier exécutable, avec toutes ses dépendances, dans un fichier .zip. Dans ce fichier zip d’exécutable hello exemple fichier est appelé « Mon-application-exe.zip ».

## <a name="prerequisites"></a>Composants requis

- Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.
- Créez un compte Azure si vous n’en avez pas. Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.

## <a name="sample-script"></a>Exemple de script

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Supprimer l’application

Après avoir exécuté hello ci-dessus un exemple de script, exécuter hello suivant tooremove de commandes de l’application et tous ses packages d’application chargés.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate une application et le téléchargement d’un package d’application.
Chaque commande dans la table de hello lie documentation toocommand spécifique.

| Commande | Remarques |
|---|---|
| [az batch application create](https://docs.microsoft.com/cli/azure/batch/application#create) | Crée une application.  |
| [az batch application set](https://docs.microsoft.com/cli/azure/batch/application#set) | Met à jour les propriétés d’une application.  |
| [az batch application package create](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Ajoute un toohello de package d’application spécifié application.  |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).
