---
title: "aaaCreate et publier une application de catalogue managé service Azure | Documents Microsoft"
description: "Montre comment toocreate Azure gérés à application qui est destinée aux membres de votre organisation."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Publier une application managée pour une utilisation interne

Vous pouvez créer et publier des[applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation. Par exemple, un service informatique peut publier des applications managées destinées à contrôler la conformité par rapport aux normes de l’organisation. Ces applications gérées sont disponibles via le catalogue de services hello, pas hello Azure Marketplace.

toopublish une application managée hello catalogue de services, vous devez :

* Créer un package .zip qui contient les trois fichiers de modèle requis hello.
* Décider quel utilisateur, groupe ou une application a besoin d’accès toohello ressource groupe dans l’abonnement de l’utilisateur hello.
* Créer la définition d’application hello géré qui pointe le package .zip de toohello et demande l’accès pour l’identité de hello.

## <a name="create-a-managed-application-package"></a>Créer un package d’application gérée

première étape de Hello est fichiers de modèles requis trois toocreate hello. Les trois fichiers de package dans un fichier .zip et téléchargez-le tooan emplacement accessible, tel qu’un compte de stockage. Vous passez un fichier .zip de toothis lien lors de la création hello gérés définition d’application.

* **applianceMainTemplate.json**: ce fichier définit hello Azure application gérée de ressources qui sont configurés en tant que partie de hello. modèle de Hello n’est pas différente de celle d’un modèle de gestionnaire de ressources normal. Par exemple, toocreate un compte de stockage via une application managée, applianceMainTemplate.json contient :

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: les utilisateurs déployer ce modèle lors de la création d’hello application gérée. Il définit la ressource application hello géré, qui est un type de ressource Microsoft.Solutions/appliances. Ce fichier contient tous les paramètres de hello que vous avez besoin pour les ressources hello dans applianceMainTemplate.json.

  Vous définissez deux propriétés importantes dans ce modèle. Tout d’abord, hello **applianceDefinitionId** propriété est ID hello hello géré de définition d’application. Vous créez définition de hello plus loin dans cette rubrique. Lorsque vous définissez cette valeur, vous devez décider quel abonnement et le toouse de groupe de ressources pour le stockage des définitions d’application managée de hello. Et, vous devez choisir un nom pour la définition de hello. ID de Hello est au format de hello :

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  En second lieu, hello **managedResourceGroupId** propriété est ID hello hello du groupe de ressources où hello ressources Azure sont créées. Vous pouvez affecter une valeur pour le nom de ce groupe de ressources ou permettent de fournir un nom d’utilisateur de hello. format Hello hello ID est :

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Hello l’exemple suivant montre un fichier mainTemplate.json. Il spécifie un groupe de ressources pour les ressources de hello déployé. ID de définition de Hello est toouse de jeu nommée d’une définition de **storageApp** dans un groupe de ressources nommé **managedApplicationGroup**. Vous pouvez modifier ces noms de différentes valeurs toouse. Fournir votre propre ID d’abonnement dans l’ID de définition hello.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: hello portail Azure utilise ce fichier toogenerate hello interface utilisateur pour les utilisateurs qui créent hello application managée. Vous déterminez la façon dont les utilisateurs fournissent une entrée pour chaque paramètre. Vous pouvez utiliser des options comme un sélecteur de liste déroulante, une zone de texte, une zone de mot de passe et d’autres outils de saisie. toolearn toocreate un fichier de définition de l’interface utilisateur pour une application managée, voir [prise en main CreateUiDefinition](managed-application-createuidefinition-overview.md).

  Hello exemple suivant illustre un fichier applianceCreateUiDefinition.json qui permet aux utilisateurs toospecify hello stockage compte préfixe du nom dans une zone de texte.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

Après que tous les fichiers hello nécessité sont prêts, empaqueter les sous la forme d’un fichier .zip. Hello trois fichiers doivent être au niveau racine de hello du fichier .zip de hello. Si vous les placez dans un dossier, vous recevez une erreur lors de la création d’hello géré de définition d’application indiquant hello requis de fichiers ne sont pas présents. Télécharger un emplacement accessible tooan package hello d’où il peut être consommé. reste Hello de cet article suppose le fichier .zip de hello existe dans un conteneur d’objets blob de stockage accessible publiquement.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Créer un groupe d’utilisateurs ou une application Azure Active Directory

deuxième étape de Hello est tooselect un groupe d’utilisateurs ou une application pour la gestion des ressources de hello pour le compte du client de hello. Ce groupe d’utilisateurs ou cette application dispose des autorisations sur hello ressource managée conséquente toohello rôle de groupe qui est affecté. rôle de Hello peut être n’importe quel rôle intégré de contrôle d’accès en fonction du rôle (RBAC) comme propriétaire ou contributeur. Vous pouvez également fournir un utilisateur individuel ressources de hello toomanage autorisation, mais que vous attribuez généralement ce groupe d’utilisateurs tooa autorisation. toocreate un nouveau groupe d’utilisateurs Active Directory, voir [créer un groupe et ajouter des membres dans Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).

Vous avez besoin d’ID d’objet hello de toouse de groupe utilisateur hello pour la gestion des ressources de hello. Bonjour à l’exemple suivant montre comment tooget hello ID d’objet à partir du nom complet du groupe hello :

```azurecli-interactive
az ad group show --group exampleGroupName
```

exemple de commande Hello renvoie hello suivant de sortie :

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

ID d’objet tooretrieve hello seulement, utilisez :

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Obtenir l’ID de définition de rôle hello

Ensuite, vous devez les ID de définition de rôle hello Hello rôle intégré de RBAC toogrant toohello utilisateur, groupe d’utilisateurs, ou l’application. En règle générale, vous utilisez hello propriétaire ou rôle de contributeur ou lecteur. Hello commande suivante montre comment tooget hello ID de définition de rôle pour le rôle de propriétaire hello :


```azurecli-interactive
az role definition list --name owner
```

Cette commande renvoie hello suivant de sortie :

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

Vous devez valeur hello de propriété « name » hello précédant l’exemple hello. Vous pouvez récupérer uniquement cette propriété avec :

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Créer la définition de l’application hello géré

Si vous ne disposez pas déjà d’un groupe de ressources pour stocker la définition de votre application managée, créez-en un maintenant :

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

À présent, créer la ressource de définition d’application hello géré.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

paramètres de Hello utilisés Bonjour précédent exemple sont :

* **groupe de ressources**: nom hello hello du groupe de ressources où hello géré définition d’application est créé.
* **niveau de verrou**: type hello de verrou placé sur le groupe de ressources managé hello. Il empêche les clients hello d’effectuer des opérations indésirables sur ce groupe de ressources. Actuellement, en lecture seule est hello pris en charge uniquement au niveau du verrou. Lorsque ReadOnly est spécifié, les clients hello peuvent lire uniquement les ressources de hello présents dans le groupe de ressources managé hello.
* **autorisations**: décrit les ID du principal hello et ID de définition de rôle hello qui sont un groupe de ressources managé toohello toogrant utilisé autorisation. Il est spécifié au format hello de `<principalId>:<roleDefinitionId>`. Plusieurs valeurs peuvent également être spécifiées pour cette propriété. Si plusieurs valeurs sont nécessaires, ils doivent être spécifiés sous forme de hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Les valeurs sont séparées par un espace.
* **uri de fichier de package**: hello emplacement du package d’application managée hello qui contient les fichiers de modèle hello, qui peuvent être un objet blob de stockage Azure.

## <a name="next-steps"></a>Étapes suivantes

* Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).
* Pour obtenir des exemples de fichiers de hello, consultez [gérés des exemples d’applications](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).
* Pour plus d’informations sur la publication des applications managées toohello Azure Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).
* Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).
* toolearn toocreate un fichier de définition de l’interface utilisateur pour une application managée, voir [prise en main CreateUiDefinition](managed-application-createuidefinition-overview.md).
