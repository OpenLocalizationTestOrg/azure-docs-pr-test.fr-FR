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
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="8762a-103">Publier une application managée pour une utilisation interne</span><span class="sxs-lookup"><span data-stu-id="8762a-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="8762a-104">Vous pouvez créer et publier des[applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="8762a-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="8762a-105">Par exemple, un service informatique peut publier des applications managées destinées à contrôler la conformité par rapport aux normes de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="8762a-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="8762a-106">Ces applications gérées sont disponibles via le catalogue de services hello, pas hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8762a-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="8762a-107">toopublish une application managée hello catalogue de services, vous devez :</span><span class="sxs-lookup"><span data-stu-id="8762a-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="8762a-108">Créer un package .zip qui contient les trois fichiers de modèle requis hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="8762a-109">Décider quel utilisateur, groupe ou une application a besoin d’accès toohello ressource groupe dans l’abonnement de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="8762a-110">Créer la définition d’application hello géré qui pointe le package .zip de toohello et demande l’accès pour l’identité de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="8762a-111">Créer un package d’application gérée</span><span class="sxs-lookup"><span data-stu-id="8762a-111">Create a managed application package</span></span>

<span data-ttu-id="8762a-112">première étape de Hello est fichiers de modèles requis trois toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="8762a-113">Les trois fichiers de package dans un fichier .zip et téléchargez-le tooan emplacement accessible, tel qu’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8762a-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="8762a-114">Vous passez un fichier .zip de toothis lien lors de la création hello gérés définition d’application.</span><span class="sxs-lookup"><span data-stu-id="8762a-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="8762a-115">**applianceMainTemplate.json**: ce fichier définit hello Azure application gérée de ressources qui sont configurés en tant que partie de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="8762a-116">modèle de Hello n’est pas différente de celle d’un modèle de gestionnaire de ressources normal.</span><span class="sxs-lookup"><span data-stu-id="8762a-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="8762a-117">Par exemple, toocreate un compte de stockage via une application managée, applianceMainTemplate.json contient :</span><span class="sxs-lookup"><span data-stu-id="8762a-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="8762a-118">**mainTemplate.json**: les utilisateurs déployer ce modèle lors de la création d’hello application gérée.</span><span class="sxs-lookup"><span data-stu-id="8762a-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="8762a-119">Il définit la ressource application hello géré, qui est un type de ressource Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="8762a-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="8762a-120">Ce fichier contient tous les paramètres de hello que vous avez besoin pour les ressources hello dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8762a-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="8762a-121">Vous définissez deux propriétés importantes dans ce modèle.</span><span class="sxs-lookup"><span data-stu-id="8762a-121">You set two important properties in this template.</span></span> <span data-ttu-id="8762a-122">Tout d’abord, hello **applianceDefinitionId** propriété est ID hello hello géré de définition d’application.</span><span class="sxs-lookup"><span data-stu-id="8762a-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="8762a-123">Vous créez définition de hello plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="8762a-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="8762a-124">Lorsque vous définissez cette valeur, vous devez décider quel abonnement et le toouse de groupe de ressources pour le stockage des définitions d’application managée de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="8762a-125">Et, vous devez choisir un nom pour la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="8762a-126">ID de Hello est au format de hello :</span><span class="sxs-lookup"><span data-stu-id="8762a-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="8762a-127">En second lieu, hello **managedResourceGroupId** propriété est ID hello hello du groupe de ressources où hello ressources Azure sont créées.</span><span class="sxs-lookup"><span data-stu-id="8762a-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="8762a-128">Vous pouvez affecter une valeur pour le nom de ce groupe de ressources ou permettent de fournir un nom d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="8762a-129">format Hello hello ID est :</span><span class="sxs-lookup"><span data-stu-id="8762a-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="8762a-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="8762a-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="8762a-131">Hello l’exemple suivant montre un fichier mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8762a-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="8762a-132">Il spécifie un groupe de ressources pour les ressources de hello déployé.</span><span class="sxs-lookup"><span data-stu-id="8762a-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="8762a-133">ID de définition de Hello est toouse de jeu nommée d’une définition de **storageApp** dans un groupe de ressources nommé **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="8762a-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="8762a-134">Vous pouvez modifier ces noms de différentes valeurs toouse.</span><span class="sxs-lookup"><span data-stu-id="8762a-134">You can change these values toouse different names.</span></span> <span data-ttu-id="8762a-135">Fournir votre propre ID d’abonnement dans l’ID de définition hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="8762a-136">**applianceCreateUiDefinition.json**: hello portail Azure utilise ce fichier toogenerate hello interface utilisateur pour les utilisateurs qui créent hello application managée.</span><span class="sxs-lookup"><span data-stu-id="8762a-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="8762a-137">Vous déterminez la façon dont les utilisateurs fournissent une entrée pour chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="8762a-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="8762a-138">Vous pouvez utiliser des options comme un sélecteur de liste déroulante, une zone de texte, une zone de mot de passe et d’autres outils de saisie.</span><span class="sxs-lookup"><span data-stu-id="8762a-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="8762a-139">toolearn toocreate un fichier de définition de l’interface utilisateur pour une application managée, voir [prise en main CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="8762a-140">Hello exemple suivant illustre un fichier applianceCreateUiDefinition.json qui permet aux utilisateurs toospecify hello stockage compte préfixe du nom dans une zone de texte.</span><span class="sxs-lookup"><span data-stu-id="8762a-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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

<span data-ttu-id="8762a-141">Après que tous les fichiers hello nécessité sont prêts, empaqueter les sous la forme d’un fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="8762a-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="8762a-142">Hello trois fichiers doivent être au niveau racine de hello du fichier .zip de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="8762a-143">Si vous les placez dans un dossier, vous recevez une erreur lors de la création d’hello géré de définition d’application indiquant hello requis de fichiers ne sont pas présents.</span><span class="sxs-lookup"><span data-stu-id="8762a-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="8762a-144">Télécharger un emplacement accessible tooan package hello d’où il peut être consommé.</span><span class="sxs-lookup"><span data-stu-id="8762a-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="8762a-145">reste Hello de cet article suppose le fichier .zip de hello existe dans un conteneur d’objets blob de stockage accessible publiquement.</span><span class="sxs-lookup"><span data-stu-id="8762a-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="8762a-146">Créer un groupe d’utilisateurs ou une application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8762a-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="8762a-147">deuxième étape de Hello est tooselect un groupe d’utilisateurs ou une application pour la gestion des ressources de hello pour le compte du client de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="8762a-148">Ce groupe d’utilisateurs ou cette application dispose des autorisations sur hello ressource managée conséquente toohello rôle de groupe qui est affecté.</span><span class="sxs-lookup"><span data-stu-id="8762a-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="8762a-149">rôle de Hello peut être n’importe quel rôle intégré de contrôle d’accès en fonction du rôle (RBAC) comme propriétaire ou contributeur.</span><span class="sxs-lookup"><span data-stu-id="8762a-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="8762a-150">Vous pouvez également fournir un utilisateur individuel ressources de hello toomanage autorisation, mais que vous attribuez généralement ce groupe d’utilisateurs tooa autorisation.</span><span class="sxs-lookup"><span data-stu-id="8762a-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="8762a-151">toocreate un nouveau groupe d’utilisateurs Active Directory, voir [créer un groupe et ajouter des membres dans Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="8762a-152">Vous avez besoin d’ID d’objet hello de toouse de groupe utilisateur hello pour la gestion des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="8762a-153">Bonjour à l’exemple suivant montre comment tooget hello ID d’objet à partir du nom complet du groupe hello :</span><span class="sxs-lookup"><span data-stu-id="8762a-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="8762a-154">exemple de commande Hello renvoie hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="8762a-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="8762a-155">ID d’objet tooretrieve hello seulement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="8762a-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="8762a-156">Obtenir l’ID de définition de rôle hello</span><span class="sxs-lookup"><span data-stu-id="8762a-156">Get hello role definition ID</span></span>

<span data-ttu-id="8762a-157">Ensuite, vous devez les ID de définition de rôle hello Hello rôle intégré de RBAC toogrant toohello utilisateur, groupe d’utilisateurs, ou l’application.</span><span class="sxs-lookup"><span data-stu-id="8762a-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="8762a-158">En règle générale, vous utilisez hello propriétaire ou rôle de contributeur ou lecteur.</span><span class="sxs-lookup"><span data-stu-id="8762a-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="8762a-159">Hello commande suivante montre comment tooget hello ID de définition de rôle pour le rôle de propriétaire hello :</span><span class="sxs-lookup"><span data-stu-id="8762a-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="8762a-160">Cette commande renvoie hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="8762a-160">That command returns hello following output:</span></span>

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

<span data-ttu-id="8762a-161">Vous devez valeur hello de propriété « name » hello précédant l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="8762a-162">Vous pouvez récupérer uniquement cette propriété avec :</span><span class="sxs-lookup"><span data-stu-id="8762a-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="8762a-163">Créer la définition de l’application hello géré</span><span class="sxs-lookup"><span data-stu-id="8762a-163">Create hello managed application definition</span></span>

<span data-ttu-id="8762a-164">Si vous ne disposez pas déjà d’un groupe de ressources pour stocker la définition de votre application managée, créez-en un maintenant :</span><span class="sxs-lookup"><span data-stu-id="8762a-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="8762a-165">À présent, créer la ressource de définition d’application hello géré.</span><span class="sxs-lookup"><span data-stu-id="8762a-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="8762a-166">paramètres de Hello utilisés Bonjour précédent exemple sont :</span><span class="sxs-lookup"><span data-stu-id="8762a-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="8762a-167">**groupe de ressources**: nom hello hello du groupe de ressources où hello géré définition d’application est créé.</span><span class="sxs-lookup"><span data-stu-id="8762a-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="8762a-168">**niveau de verrou**: type hello de verrou placé sur le groupe de ressources managé hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="8762a-169">Il empêche les clients hello d’effectuer des opérations indésirables sur ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8762a-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="8762a-170">Actuellement, en lecture seule est hello pris en charge uniquement au niveau du verrou.</span><span class="sxs-lookup"><span data-stu-id="8762a-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="8762a-171">Lorsque ReadOnly est spécifié, les clients hello peuvent lire uniquement les ressources de hello présents dans le groupe de ressources managé hello.</span><span class="sxs-lookup"><span data-stu-id="8762a-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="8762a-172">**autorisations**: décrit les ID du principal hello et ID de définition de rôle hello qui sont un groupe de ressources managé toohello toogrant utilisé autorisation.</span><span class="sxs-lookup"><span data-stu-id="8762a-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="8762a-173">Il est spécifié au format hello de `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="8762a-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="8762a-174">Plusieurs valeurs peuvent également être spécifiées pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="8762a-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="8762a-175">Si plusieurs valeurs sont nécessaires, ils doivent être spécifiés sous forme de hello `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="8762a-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="8762a-176">Les valeurs sont séparées par un espace.</span><span class="sxs-lookup"><span data-stu-id="8762a-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="8762a-177">**uri de fichier de package**: hello emplacement du package d’application managée hello qui contient les fichiers de modèle hello, qui peuvent être un objet blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8762a-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8762a-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8762a-178">Next steps</span></span>

* <span data-ttu-id="8762a-179">Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8762a-180">Pour obtenir des exemples de fichiers de hello, consultez [gérés des exemples d’applications](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="8762a-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="8762a-181">Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="8762a-182">Pour plus d’informations sur la publication des applications managées toohello Azure Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="8762a-183">Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="8762a-184">toolearn toocreate un fichier de définition de l’interface utilisateur pour une application managée, voir [prise en main CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8762a-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
