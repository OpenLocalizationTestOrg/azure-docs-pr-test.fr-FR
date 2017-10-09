---
title: "aaaAzure exemple de Script CLI - créez un compte Batch | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer un compte Batch"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Créer un compte de traitement par lots avec hello CLI d’Azure

Ce script crée un compte Azure Batch et montre comment différentes propriétés du compte de hello peuvent être interrogées et mis à jour.

## <a name="prerequisites"></a>Composants requis

Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.

## <a name="batch-account-sample-script"></a>Exemple de script de compte Batch

Lorsque vous créez un compte de traitement par lots, par défaut ses nœuds de calcul sont attribuées en interne par hello service Batch. Nœuds de calcul alloué sera le quota de sujet tooa distinct et compte de hello peut être authentifié via les informations d’identification de clé partagée ou un jeton de répertoire Active de Azure.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Compte Batch utilisant un exemple de script d’abonnement

Vous pouvez également choisir de toohave lot créer ses nœuds de calcul dans votre propre abonnement Azure.
Comptes qui allouent de calcul nœuds à votre abonnement doivent être authentifiées via un jeton d’Azure Active Directory et les nœuds de calcul hello alloués seront comptabilisée dans le quota de votre abonnement. toocreate un compte dans ce mode, un doit spécifier une référence de coffre de clés lors de la création du compte de hello.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Une fois que vous exécutez Hello au-dessus des exemples de scripts, exécutez hello suivant commande tooremove le groupe de ressources et toutes les ressources (y compris les comptes de lots, comptes de stockage Azure et les coffres de clés Azure).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, du compte Batch et toutes les ressources associées. Chaque commande dans la table de hello lie documentation toocommand spécifique.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Crée un compte de traitement par lots hello.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | Met à jour les propriétés de hello compte Batch.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | Récupère les détails de hello spécifié du compte Batch.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Récupère les clés d’accès hello Hello spécifié du compte Batch.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | S’authentifie avec hello spécifié pour l’interaction de CLI davantage le compte Batch.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | Crée un compte de stockage. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | Crée un coffre de clés. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Mettre à jour la stratégie de sécurité hello de coffre de clés spécifié hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).
