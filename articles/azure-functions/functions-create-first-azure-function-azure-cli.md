---
title: "aaaCreate votre première fonction à partir de hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate votre première Azure de fonction pour l’utilisation de l’exécution sans serveur hello CLI d’Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Créer votre première fonction à l’aide de hello CLI d’Azure

Ce didacticiel de démarrage rapide décrit en détail le toouse Azure fonctions toocreate votre première fonction. Vous utilisez hello CLI d’Azure toocreate une application de fonction qui est hello sans infrastructure qui héberge votre fonction. code de fonction Hello lui-même est déployée à partir d’un dépôt d’exemples GitHub.    

Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux. 

## <a name="prerequisites"></a>Composants requis 

Avant d’exécuter cet exemple, vous devez disposer de hello :

+ Un compte [GitHub](https://github.com) actif. 
+ Un abonnement Azure actif.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [az groupe créer](/cli/azure/group#create). Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les Function Apps, les bases de données et les comptes de stockage sont déployées et gérées.

Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup`.  
Si vous n’utilisez pas Cloud Shell, vous devez d’abord vous connecter à l’aide de `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Création d'un compte Azure Storage

Fonctions utilise un état de toomaintain de compte de stockage Azure et d’autres informations sur vos fonctions. Créer un compte de stockage dans le groupe de ressources hello vous avez créé à l’aide de hello [créer de compte de stockage az](/cli/azure/storage/account#create) commande.

Bonjour suivant de commande, remplacez par votre propre nom de compte de stockage global unique dans lequel vous consultez hello `<storage_name>` espace réservé. Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Après avoir créé le compte de stockage hello, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Créer une Function App

Vous devez disposer d’une application toohost hello exécution d’une fonction de vos fonctions. application de fonction Hello fournit un environnement d’exécution sans serveur de votre code de fonction. Elle vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources. Créer une application de la fonction à l’aide de hello [az functionapp créer](/cli/azure/functionapp#create) commande. 

Bonjour suivant de commande, remplacez par votre propre nom de l’application une fonction unique dans lequel vous consultez hello `<app_name>` espace réservé et hello nom de compte de stockage pour `<storage_name>`. Hello `<app_name>` est utilisé comme domaine DNS par défaut hello pour application de fonction hello et c’est le cas hello nom doit toobe unique entre toutes les applications dans Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Par défaut, une application de la fonction est créée avec hello consommation plan d’hébergement, ce qui signifie que les ressources sont ajoutées dynamiquement comme requis par vos fonctions et que vous payez uniquement lors de l’exécutant des fonctions. Pour plus d’informations, consultez [plan d’hébergement approprié choisir hello](functions-scale.md). 

Après que application de fonction hello a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Maintenant que vous avez une application de la fonction, vous pouvez déployer le code de fonction réelle hello de dépôt d’exemples hello GitHub.

## <a name="deploy-your-function-code"></a>Déployer votre code de fonction  

Il existe plusieurs façons toocreate votre code de fonction dans votre nouvelle application de la fonction. Cette rubrique connecte dépôt d’exemples tooa dans GitHub. Comme avant, Bonjour suivant code remplacer hello `<app_name>` espace réservé nommé hello d’application de fonction hello vous avez créé. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Après le déploiement de hello source été définie, hello CLI d’Azure affiche des informations toohello similaire (les valeurs null sont supprimées pour une meilleure lisibilité) de l’exemple suivant :

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Fonction hello de test

Utiliser cURL tootest hello déployé sur un ordinateur Mac ou Linux ou à l’aide d’un interpréteur de commandes sous Windows. Exécutez hello cURL commande, en remplaçant hello suivante `<app_name>` espace réservé nommé hello de votre application de la fonction. Ajouter la chaîne de requête hello `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Réponse de la fonction affichée dans un navigateur.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Si vous n’avez pas cURL disponible dans votre ligne de commande, entrez hello même URL dans la zone Adresse hello de votre navigateur web. Là encore, remplacez hello `<app_name>` espace réservé nommé hello de votre application de la fonction et ajoute la chaîne de requête hello `&name=<yourname>` toohello URL et l’exécution de la demande de hello. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Réponse de la fonction affichée dans un navigateur.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Supprimer des ressources

Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. Si vous prévoyez toocontinue sur toowork Démarrages rapides suivants ou avec des didacticiels de hello, procédez de nettoyer les ressources hello créées dans ce démarrage rapide. Si vous n’envisagez pas de toocontinue, utilisez hello suivant commande toodelete toutes les ressources créées par ce démarrage rapide :

```azurecli-interactive
az group delete --name myResourceGroup
```
Quand vous y êtes invité, tapez `y`.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
