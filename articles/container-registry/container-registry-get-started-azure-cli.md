---
title: "Registre de conteneur de Docker privé aaaCreate - CLI d’Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a>Créer un Registre de conteneur Docker privé à l’aide de hello Azure CLI 2.0
Utiliser les commandes hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate un Registre de conteneur et de gérer ses paramètres de votre ordinateur Linux, Mac ou Windows. Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [portail Azure](container-registry-get-started-portal.md) ou par programme avec hello Registre de conteneur [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)
* Aide sur les commandes CLI de Registre de conteneur (`az acr` commandes), passez hello `-h` commande tooany de paramètre.


## <a name="prerequisites"></a>Composants requis
* **Azure CLI 2.0**: tooinstall et prise en main hello CLI 2.0, consultez hello [des instructions d’installation](/cli/azure/install-azure-cli). Connectez-vous à tooyour abonnement Azure en exécutant `az login`. Pour plus d’informations, consultez [prise en main hello CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant. Assurez-vous que le groupe de ressources hello est dans un emplacement où le service de Registre de conteneur de hello est [disponible](https://azure.microsoft.com/regions/services/). un groupe de ressources à l’aide de toocreate hello CLI 2.0, consultez [hello référence CLI 2.0](/cli/azure/group).
* **Compte de stockage** (facultatif) : créez un Azure standard [compte de stockage](../storage/common/storage-introduction.md) tooback Registre de conteneur hello Bonjour même emplacement. Si vous ne spécifiez pas un compte de stockage lors de la création d’un Registre avec `az acr create`, commande hello crée une pour vous. un stockage compte à l’aide de toocreate hello CLI 2.0, consultez [hello référence CLI 2.0](/cli/azure/storage/account). Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.
* **Principal du service** (facultatif) : lorsque vous créez un Registre par hello CLI, par défaut il n'est pas configuré pour l’accès. Selon vos besoins, vous pouvez affecter un Registre tooa principal de service Azure Active Directory existant (ou créer et affecter une autre), ou activer le compte d’utilisateur admin du Registre hello. Consultez les sections hello plus loin dans cet article. Pour plus d’informations sur l’accès au Registre, consultez [authentifier avec le Registre de conteneur hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Créer un registre de conteneur
Exécutez hello `az acr create` commande toocreate un Registre de conteneur.

> [!TIP]
> Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres. nom de Registre Hello dans les exemples hello est `myRegistry1`, mais remplacer par un nom unique de votre choix.
>
>

Hello utilise hello Registre de conteneur toocreate minimal de paramètres de commande suivante `myRegistry1` dans le groupe de ressources hello `myResourceGroup`et à l’aide de hello *base* référence (SKU) :

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* `--storage-account-name` est facultatif. Si ce n’est pas spécifié, un compte de stockage est créé avec un nom composé du nom de Registre hello et un horodatage dans hello spécifié le groupe de ressources.

Lors de la création de Registre de hello, sortie de hello est similaire toohello suivantes :

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


Notez les poins suivants :

* `id`-Identificateur de Registre hello dans votre abonnement, vous avez besoin si vous souhaitez tooassign un principal de service.
* `loginServer`-nom complet de hello vous spécifiez trop[connecter toohello Registre](container-registry-authentication.md). Dans cet exemple, le nom de hello est `myregistry1.exp.azurecr.io` (tout en minuscules).

## <a name="assign-a-service-principal"></a>Affecter un principal de service
Utilisez tooassign des commandes CLI 2.0 un Registre tooa principal du service Azure Active Directory. Hello principal du service dans ces exemples se voit attribuer hello propriétaire du rôle, mais vous pouvez affecter [autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a>Créer un principal de service et assigner le Registre de toohello d’accès
Bonjour la commande suivante, un principal de service est affecté identificateur Registre propriétaire du rôle accès toohello passé avec hello `--scopes` paramètre. Spécifiez un mot de passe fort avec hello `--password` paramètre.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Affecter un principal de service existant
Si vous disposez d’un principal de service déjà et que vous souhaitez tooassign il propriétaire du rôle accès toohello exécution de Registre, un toohello similaire commande exemple suivant. Vous passez l’ID d’application principal de service hello à l’aide de hello `--assignee` paramètre :

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Gérer les informations d’identification de l’administrateur
Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut. Hello suivant illustrent les exemples `az acr` toomanage hello admin informations d’identification pour le Registre de votre conteneur de commandes CLI.

### <a name="obtain-admin-user-credentials"></a>Obtenir les informations d’identification de l’utilisateur Admin
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Activer l’utilisateur Admin pour un registre existant
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Désactiver l’utilisateur Admin pour un registre existant
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>Répertorier les images et les balises
Hello d’utilisation `az acr` commandes CLI de balises dans un référentiel et des images de hello tooquery.

> [!NOTE]
> Actuellement, Registre de conteneur ne prend pas en charge hello `docker search` tooquery de commande pour les images et les balises.


### <a name="list-repositories"></a>Répertorier les référentiels
Hello exemple suivant répertorie les référentiels hello dans un Registre, au format JSON (JavaScript Object Notation) :

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>Répertorier les balises
Hello exemple suivant répertorie les balises hello sur hello **exemples/nginx** référentiel, au format JSON :

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Étapes suivantes
* [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
