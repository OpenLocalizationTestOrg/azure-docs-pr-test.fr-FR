---
title: "aaaCreate une application de la fonction et déployer le code de fonction à partir de GitHub | Documents Microsoft"
description: "Créer une Function App et déployer le code de fonction à partir de GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a>Créer un App Service

Cet exemple de script crée une application de la fonction à l’aide de hello [le plan de la consommation](../functions-scale.md#consumption-plan) avec ses ressources connexes et en permanence déploie votre code de fonction à partir d’un référentiel GitHub. Dans cet exemple, vous aurez besoin des éléments suivants :

* Un référentiel GitHub avec du code de fonction, pour lequel vous disposez d’autorisations d’administration.
* Un [jeton d’accès personnel](https://help.github.com/articles/creating-an-access-token-for-command-line-use) pour votre compte GitHub.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Exemple de script

Cet exemple crée une Function App Azure et déploie le code de fonction à partir de GitHub.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Explication du script

Chaque commande figurant dans la documentation spécifique du toocommand liens table hello. Ce script utilise hello :

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az storage account create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Crée un plan App Service. |
| [az functionapp create](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [az appservice web source-control config](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Associe une Function App à un référentiel Git ou Mercurial. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de fonctions Azure Bonjour [documentation Azure fonctions](../functions-cli-samples.md).
