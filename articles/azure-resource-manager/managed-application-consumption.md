---
title: "application gérée d’aaaConsume Azure | Documents Microsoft"
description: "Décrit comment un client crée une application gérée Azure à partir de fichiers publiés."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Utiliser une application managée interne

Vous pouvez utiliser des [applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation. Par exemple, vous pouvez sélectionner des applications managées dans votre service informatique qui garantissent la conformité par rapport aux normes de l’organisation. Ces applications gérées sont disponibles via hello catalogue de services, pas hello Azure Marketplace.

Avant de procéder à cet article, vous devez disposer d’une application managée disponible dans le catalogue de services hello pour votre abonnement. Si personne au sein de votre organisation n’a encore créé une application managée, consultez [Publier une application managée pour une utilisation interne](managed-application-publishing.md).

Actuellement, vous pouvez utiliser soit une CLI d’Azure hello tooconsume portail Azure une application managée.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Créer l’application hello géré à l’aide du portail de hello

toodeploy une application managée via le portail de hello, procédez comme suit :

1. Accédez toohello portail Azure. Recherchez **Application managée du catalogue de services**.

   ![Application gérée du catalogue de services](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Sélectionnez hello gérés à application que vous souhaitez toocreate à partir de la liste de hello des solutions disponibles. Sélectionnez **Créer**.

   ![Sélection d’application gérée](./media/managed-application-consumption/select-offer.png)

1. Fournir des valeurs pour les paramètres de hello qui sont des ressources de hello tooprovision requis. Sélectionnez **Ouest-Centre des États-Unis** comme emplacement. Sélectionnez **OK**.

   ![Paramètres de l’application gérée](./media/managed-application-consumption/input-parameters.png)

1. modèle de Hello valide les valeurs hello que vous avez fourni. Si la validation réussit, sélectionnez **OK** déploiement de hello toostart.

   ![Validation de l’application managée](./media/managed-application-consumption/validation.png)

Une fois hello s’achève, les ressources appropriées de hello définis dans le modèle de hello sont configurés dans le groupe de ressources managé hello que vous avez fourni.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Créer des application hello géré à l’aide de CLI d’Azure

Il existe deux façons toocreate une application managée à l’aide d’Azure CLI :

* Utilisez la commande hello pour créer des applications managées.
* Utilisez la commande de déploiement de modèle Normal hello.

### <a name="use-hello-template-deployment-command"></a>Utilisez la commande de déploiement de modèle de hello

Déployer le fichier applianceMainTemplate.json hello hello fournisseur créé.

Puis, créez deux groupes de ressources. Hello premier groupe de ressources est où hello ressources d’application managée est créé : Microsoft.Solutions/appliances. deuxième groupe de ressources Hello contient toutes les ressources hello définis dans mainTemplate.json. Ce groupe de ressources est géré par hello ISV.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Utilisez `westcentralus` comme emplacement hello hello du groupe de ressources.
>

applianceMainTemplate.json toodeploy dans mainResourceGroup, hello utilisez commande suivante :

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Après avoir hello précédent s’exécute le modèle, il vous invite pour les valeurs de paramètres hello qui sont définis dans le modèle de hello hello. En outre les paramètres de toohello qui sont nécessaires tooprovision des ressources dans un modèle, vous avez besoin de deux valeurs de paramètre de clé :

- **managedResourceGroupId**: hello ID des ressources de hello contenant hello ressource groupe défini dans applianceMainTemplate.json. ID de Hello se présente sous forme de hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. Bonjour précédent exemple, il ID de l’élément hello de `managedResourceGroup`.
- **applianceDefinitionId**: ID de hello Hello gérés ressource de définition d’application. Cette valeur est fournie par hello ISV.

> [!NOTE]
> serveur de publication Hello doit accorder l’accès toohello ressource groupe qui contient la définition de l’application hello géré. ressource de définition Hello est créée dans l’abonnement du serveur de publication hello. Par conséquent, un utilisateur, un groupe d’utilisateurs ou une application dans le locataire hello a besoin d’accès en lecture toothis ressource.

Une fois le déploiement de hello se termine correctement, vous voyez hello géré application est créée dans mainResourceGroup. ressources de storageAccount Hello est créé dans managedResourceGroup.

### <a name="use-hello-create-command"></a>Hello d’utilisation Créer commande

Vous pouvez utiliser hello `az managedapp create` commande toocreate une application managée à partir de hello gérés définition d’application.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **Id de définition d’application**: ID de ressource hello Hello gérés créée dans hello précédant l’étape de définition d’application. tooobtain cet ID, exécutez hello de commande suivante :

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Cette commande renvoie la définition de l’application hello géré. Vous devez valeur hello de propriété d’ID hello.

* **id du groupe de routage managé**: nom hello des ressources de hello contenant hello ressource groupe défini dans applianceMainTemplate.json. Ce groupe de ressources est un groupe de ressources managé hello. Il est géré par le serveur de publication hello. S’il n’existe pas, il est créé pour vous.
* **groupe de ressources**: groupe de ressources hello où hello géré de ressource d’application est créé. Hello Microsoft.Solutions/appliance ressource se situe à ce groupe de ressources.
* **paramètres**: hello des paramètres qui sont nécessaires pour les ressources hello définis dans applianceMainTemplate.json.

## <a name="known-issues"></a>Problèmes connus

Cette préversion inclut hello suivants :

* Une erreur de serveur interne 500 apparaît lors de la création de hello de l’application hello géré. Si vous rencontrez ce problème, il est probable toobe intermittent. Recommencez l’opération de hello.
* Un groupe de ressources est nécessaire pour le groupe de ressources managé hello. Si vous utilisez un groupe de ressources existant, le déploiement de hello échoue.
* Hello groupe de ressources qui contient la ressource de Microsoft.Solutions/appliances hello doit être créée dans hello **westcentralus** emplacement.

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).
* Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).
* Pour plus d’informations sur la publication des applications managées toohello Azure Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).
* Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).
