---
title: "Créer et publier une application managée du catalogue de services Azure | Microsoft Docs"
description: "Montre comment créer une application managée Azure destinée aux membres de votre organisation."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 39b74984ec2f89ed39753963de7fe3ff79577c9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="ef5bf-103">Publier une application managée pour une utilisation interne</span><span class="sxs-lookup"><span data-stu-id="ef5bf-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="ef5bf-104">Vous pouvez créer et publier des[applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="ef5bf-105">Par exemple, un service informatique peut publier des applications managées destinées à contrôler la conformité par rapport aux normes de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="ef5bf-106">Ces applications managées sont disponibles via le catalogue de services, et non la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-106">These managed applications are available through the service catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="ef5bf-107">Pour publier une application managée pour le catalogue de services, vous devez :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-107">To publish a managed application for the service catalog, you must:</span></span>

* <span data-ttu-id="ef5bf-108">créer un package .zip qui contient les trois fichiers modèles nécessaires ;</span><span class="sxs-lookup"><span data-stu-id="ef5bf-108">Create a .zip package that contains the three required template files.</span></span>
* <span data-ttu-id="ef5bf-109">désigner l’utilisateur, le groupe ou l’application qui doit avoir accès au groupe de ressources dans l’abonnement de l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="ef5bf-109">Decide which user, group, or application needs access to the resource group in the user's subscription.</span></span>
* <span data-ttu-id="ef5bf-110">créer la définition de l’application managée qui pointe vers le package .zip et qui demande l’accès pour l’identité.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-110">Create the managed application definition that points to the .zip package and requests access for the identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="ef5bf-111">Créer un package d’application gérée</span><span class="sxs-lookup"><span data-stu-id="ef5bf-111">Create a managed application package</span></span>

<span data-ttu-id="ef5bf-112">La première étape consiste à créer les trois fichiers modèles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-112">The first step is to create the three required template files.</span></span> <span data-ttu-id="ef5bf-113">Compressez les trois fichiers dans un fichier .zip, puis chargez ce package à un emplacement accessible, par exemple un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-113">Package all three files into a .zip file, and upload it to an accessible location, such as a storage account.</span></span> <span data-ttu-id="ef5bf-114">Vous transmettez un lien à ce fichier .zip au moment de créer la définition de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-114">You pass a link to this .zip file when creating the managed application definition.</span></span>

* <span data-ttu-id="ef5bf-115">**applianceMainTemplate.json** : ce fichier définit les ressources Azure approvisionnées pour l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-115">**applianceMainTemplate.json**: This file defines the Azure resources that are provisioned as part of the managed application.</span></span> <span data-ttu-id="ef5bf-116">Le modèle n’est en rien différent d’un modèle Resource Manager normal.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-116">The template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="ef5bf-117">Par exemple, pour créer un compte de stockage via une application managée, le fichier applianceMainTemplate.json contient :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-117">For example, to create a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="ef5bf-118">**mainTemplate.json** : les utilisateurs déploient ce modèle au moment de créer l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-118">**mainTemplate.json**: Users deploy this template when creating the managed application.</span></span> <span data-ttu-id="ef5bf-119">Il définit la ressource d’application managée, qui est un type de ressource Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-119">It defines the managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="ef5bf-120">Ce fichier contient tous les paramètres dont vous avez besoin pour les ressources contenues dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-120">This file contains all the parameters you need for the resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="ef5bf-121">Vous définissez deux propriétés importantes dans ce modèle.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-121">You set two important properties in this template.</span></span> <span data-ttu-id="ef5bf-122">La première est la propriété **applianceDefinitionId**, qui correspond à l’ID de la définition de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-122">First, the **applianceDefinitionId** property is the ID of the managed application definition.</span></span> <span data-ttu-id="ef5bf-123">Vous créerez cette définition plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-123">You create the definition later in this topic.</span></span> <span data-ttu-id="ef5bf-124">Au moment de définir cette valeur, vous devez indiquer quel abonnement et quels groupes de ressources utiliser pour stocker les définitions de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-124">When setting this value, you must decide which subscription and resource group to use for storing the managed application definitions.</span></span> <span data-ttu-id="ef5bf-125">Par ailleurs, vous devez décider du nom que vous souhaitez attribuer à la définition.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-125">And, you must decide on a name for the definition.</span></span> <span data-ttu-id="ef5bf-126">L’ID est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-126">The ID is in the format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="ef5bf-127">La deuxième propriété, **managedResourceGroupId**, correspond à l’ID du groupe de ressources dans lequel les ressources Azure sont créées.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-127">Second, the **managedResourceGroupId** property is the ID of the resource group where the Azure resources are created.</span></span> <span data-ttu-id="ef5bf-128">Vous pouvez affecter une valeur à ce nom de groupe de ressources ou laisser le soin à l’utilisateur d’indiquer un nom.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-128">You can assign a value for this resource group name or let the user provide a name.</span></span> <span data-ttu-id="ef5bf-129">L’ID est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-129">The format of the ID is:</span></span>

  <span data-ttu-id="ef5bf-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="ef5bf-131">L’exemple suivant présente un fichier mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-131">The following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="ef5bf-132">Il spécifie un groupe de ressources pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-132">It specifies a resource group for the deployed resources.</span></span> <span data-ttu-id="ef5bf-133">L’ID de définition utilise ici une définition nommée **storageApp** dans un groupe de ressources nommé **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-133">The definition ID is set to use a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="ef5bf-134">Vous pouvez modifier ces valeurs de façon à utiliser d’autres noms.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-134">You can change these values to use different names.</span></span> <span data-ttu-id="ef5bf-135">Indiquez votre propre ID d’abonnement dans l’ID de définition.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-135">Provide your own subscription ID in the definition ID.</span></span>

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

* <span data-ttu-id="ef5bf-136">**applianceCreateUiDefinition.json** : le portail Azure utilise ce fichier pour générer l’interface utilisateur pour les clients qui créent l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-136">**applianceCreateUiDefinition.json**: The Azure portal uses this file to generate the user interface for users who create the managed application.</span></span> <span data-ttu-id="ef5bf-137">Vous déterminez la façon dont les utilisateurs fournissent une entrée pour chaque paramètre.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="ef5bf-138">Vous pouvez utiliser des options comme un sélecteur de liste déroulante, une zone de texte, une zone de mot de passe et d’autres outils de saisie.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="ef5bf-139">Pour en savoir plus sur la création d’un fichier de définition de l’interface utilisateur pour une application gérée, consultez [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-139">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="ef5bf-140">L’exemple suivant présente un fichier applianceCreateUiDefinition.json qui permet aux utilisateurs de spécifier le préfixe du nom du compte de stockage dans une zone de texte.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-140">The following example shows an applianceCreateUiDefinition.json file that enables users to specify the storage account name prefix through a textbox.</span></span>

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
                "toolTip": "Provide a value that is used for the prefix of your storage account. Limit to 11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-11 characters long."
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

<span data-ttu-id="ef5bf-141">Une fois que tous les fichiers nécessaires sont prêts, empaquetez-les sous forme de fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-141">After all the needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="ef5bf-142">Les trois fichiers doivent se trouver au niveau racine du fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-142">The three files must be at the root level of the .zip file.</span></span> <span data-ttu-id="ef5bf-143">Si vous les placez dans un dossier, vous obtenez une erreur au moment de créer la définition de l’application managée qui indique que les fichiers nécessaires ne sont pas présents.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-143">If you put them in a folder, you receive an error when creating the managed application definition that states the required files are not present.</span></span> <span data-ttu-id="ef5bf-144">Chargez le package à un emplacement accessible à partir de là où il peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-144">Upload the package to an accessible location from where it can be consumed.</span></span> <span data-ttu-id="ef5bf-145">La suite de cet article considère que le fichier .zip existe dans un conteneur d’objets blob de stockage accessible publiquement.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-145">The remainder of this article assumes the .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="ef5bf-146">Créer un groupe d’utilisateurs ou une application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef5bf-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="ef5bf-147">La deuxième étape consiste à sélectionner un groupe d’utilisateurs ou une application pour gérer les ressources pour le compte du client.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-147">The second step is to select a user group or application for managing the resources on behalf of the customer.</span></span> <span data-ttu-id="ef5bf-148">Ce groupe d’utilisateurs ou l’application dispose d’autorisations sur le groupe de ressources managé en fonction du rôle attribué.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-148">This user group or application has permissions on the managed resource group according to the role that is assigned.</span></span> <span data-ttu-id="ef5bf-149">Le rôle peut être n’importe quel rôle Contrôle d’accès en fonction du rôle (RBAC) intégré, par exemple Propriétaire ou Contributeur.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-149">The role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="ef5bf-150">Vous pouvez également autoriser un utilisateur individuel à pour gérer les ressources, mais en général, cette autorisation est attribuée à un groupe d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-150">You also can give an individual user permission to manage the resources, but typically you assign this permission to a user group.</span></span> <span data-ttu-id="ef5bf-151">Pour créer un groupe d’utilisateurs Active Directory, consultez [Créer un groupe et ajouter des membres dans Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-151">To create a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="ef5bf-152">Vous avez besoin de l’ID d’objet du groupe d’utilisateurs à utiliser pour gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-152">You need the object ID of the user group to use for managing the resources.</span></span> <span data-ttu-id="ef5bf-153">L’exemple suivant montre comment obtenir l’ID d’objet à partir du nom d’affichage du groupe :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-153">The following example shows how to get the object ID from the group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="ef5bf-154">L’exemple de commande renvoie le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-154">The example command returns the following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="ef5bf-155">Pour récupérer uniquement l’ID d’objet, utilisez :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-155">To retrieve just the object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-the-role-definition-id"></a><span data-ttu-id="ef5bf-156">Obtenir l’ID de définition de rôle</span><span class="sxs-lookup"><span data-stu-id="ef5bf-156">Get the role definition ID</span></span>

<span data-ttu-id="ef5bf-157">Ensuite, vous avez besoin de l’ID de définition de rôle du rôle RBAC intégré auquel vous souhaitez accorder l’accès à l’utilisateur, au groupe d’utilisateurs ou à l’application.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-157">Next, you need the role definition ID of the RBAC built-in role you want to grant access to the user, user group, or application.</span></span> <span data-ttu-id="ef5bf-158">En règle générale, vous utilisez le rôle Propriétaire, Collaborateur ou Lecteur.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-158">Typically, you use the Owner or Contributor or Reader role.</span></span> <span data-ttu-id="ef5bf-159">La commande suivante montre comment obtenir l’ID de définition de rôle pour le rôle Propriétaire :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-159">The following command shows how to get the role definition ID for the Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="ef5bf-160">Cette commande renvoie le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-160">That command returns the following output:</span></span>

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access to resources.",
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

<span data-ttu-id="ef5bf-161">Vous avez besoin de la valeur de la propriété « name » issue de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-161">You need the value of the "name" property from the preceding example.</span></span> <span data-ttu-id="ef5bf-162">Vous pouvez récupérer uniquement cette propriété avec :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-the-managed-application-definition"></a><span data-ttu-id="ef5bf-163">Créer la définition d’application gérée</span><span class="sxs-lookup"><span data-stu-id="ef5bf-163">Create the managed application definition</span></span>

<span data-ttu-id="ef5bf-164">Si vous ne disposez pas déjà d’un groupe de ressources pour stocker la définition de votre application managée, créez-en un maintenant :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="ef5bf-165">À présent, créez la ressource de définition de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-165">Now, create the managed application definition resource.</span></span>

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

<span data-ttu-id="ef5bf-166">Les paramètres utilisés dans cet exemple sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ef5bf-166">The parameters used in the preceding example are:</span></span>

* <span data-ttu-id="ef5bf-167">**resource-group** : nom du groupe de ressources dans lequel la définition de l’application managée est créée.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-167">**resource-group**: The name of the resource group where the managed application definition is created.</span></span>
* <span data-ttu-id="ef5bf-168">**lock-level**: type de verrou placé sur le groupe de ressources gérées.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-168">**lock-level**: The type of lock placed on the managed resource group.</span></span> <span data-ttu-id="ef5bf-169">Il empêche le client d’effectuer des opérations indésirables sur ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-169">It prevents the customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="ef5bf-170">Actuellement, ReadOnly est le seul niveau de verrou pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-170">Currently, ReadOnly is the only supported lock level.</span></span> <span data-ttu-id="ef5bf-171">Lorsque ReadOnly est spécifié, le client peut lire uniquement les ressources présentes dans le groupe de ressources gérées.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-171">When ReadOnly is specified, the customer can only read the resources present in the managed resource group.</span></span>
* <span data-ttu-id="ef5bf-172">**authorizations** : décrit l’ID principal et l’ID de définition de rôle utilisés pour accorder des autorisations au groupe de ressources gérées.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-172">**authorizations**: Describes the principal ID and the role definition ID that are used to grant permission to the managed resource group.</span></span> <span data-ttu-id="ef5bf-173">Il est spécifié sous la forme `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-173">It's specified in the format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="ef5bf-174">Plusieurs valeurs peuvent également être spécifiées pour cette propriété.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="ef5bf-175">Si plusieurs valeurs sont nécessaires, elles doivent être spécifiées sous la forme `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-175">If multiple values are needed, they should be specified in the form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="ef5bf-176">Les valeurs sont séparées par un espace.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="ef5bf-177">**package-file-uri** : emplacement du package de l’application managée qui contient les fichiers modèles, qui peut être un objet blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-177">**package-file-uri**: The location of the managed application package that contains the template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef5bf-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef5bf-178">Next steps</span></span>

* <span data-ttu-id="ef5bf-179">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-179">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="ef5bf-180">Consultez les [exemples d’application gérée](https://github.com/Azure/azure-managedapp-samples/tree/master/samples) pour voir des exemples de fichiers.</span><span class="sxs-lookup"><span data-stu-id="ef5bf-180">For examples of the files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="ef5bf-181">Pour plus d’informations sur l’utilisation d’une application gérée de catalogue de services, consultez l’article [Utiliser une application gérée du catalogue de services](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="ef5bf-182">Pour plus d’informations sur la publication d’applications gérées sur la Place de marché, consultez l’article [Applications gérées sur la Place de marché](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-182">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="ef5bf-183">Pour plus d’informations sur l’utilisation d’applications gérées de la Place de marché, consultez l’article [Utilisation des applications gérées de la Place de marché Azure](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-183">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="ef5bf-184">Pour en savoir plus sur la création d’un fichier de définition de l’interface utilisateur pour une application gérée, consultez [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef5bf-184">To learn how to create a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
