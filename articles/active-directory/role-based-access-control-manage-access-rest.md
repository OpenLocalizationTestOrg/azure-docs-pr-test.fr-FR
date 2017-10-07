---
title: "Contrôle d’accès basé sur aaaRole avec REST - Azure AD | Documents Microsoft"
description: "Gestion du contrôle d’accès basé sur un rôle avec l’API REST de hello"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Gérer le contrôle d’accès en fonction du rôle avec l’API REST de hello
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)

Basé sur le rôle de contrôle d’accès (RBAC) Bonjour portail Azure et des API Azure Resource Manager vous permet de gérer l’accès tooyour abonnement et ressources à un niveau de granularité fin. Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.

## <a name="list-all-role-assignments"></a>Répertorie toutes les affectations de rôle
Répertorie toutes les attributions de hello en hello spécifié étendue et subscopes.

attributions de rôles toolist, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/read` opération étendue hello. Tous les rôles intégrés hello sont accordées opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{api-version}* par 2015-07-01.
3. Remplacez *{filter}* avec condition hello que vous souhaitez que la liste de l’attribution de rôle tooapply toofilter hello :

   * Liste des attributions de rôle pour hello uniquement spécifié étendue, y compris les attributions de rôles hello à subscopes ne pas :`atScope()`    
   * Répertorier les affectations de rôle pour un utilisateur, un groupe ou une application spécifique : `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Répertorier les affectations de rôle pour un utilisateur spécifique, y compris celles héritées de groupes | `assignedTo('{objectId of user}')`

### <a name="response"></a>Response
Code d’état : 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Obtention d’informations sur une affectation de rôle
Obtient des informations sur une attribution de rôle unique spécifiée par l’identificateur de l’attribution de rôle hello.

tooget plus d’informations sur une attribution de rôle, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/read` opération. Tous les rôles intégrés hello sont accordées opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-assignment-id}* avec l’identificateur GUID hello attribution de rôle hello.
3. Remplacez *{api-version}* par 2015-07-01.

### <a name="response"></a>Response
Code d’état : 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Créer une affectation de rôle
Créer un rôle d’attribution à hello spécifié étendue pour hello spécifiée rôle spécifié principal qui accorde hello.

toocreate une attribution de rôle, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/write` opération. Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **PUT** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez toocreate attributions hello. Lorsque vous créez une attribution de rôle à une portée parent, toutes les portées enfants héritent hello même attribution de rôle. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-assignment-id}* avec un nouveau GUID, qui devient l’identificateur GUID de hello de nouvelle attribution de rôle hello.
3. Remplacez *{api-version}* par 2015-07-01.

Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Nom de l’élément | Requis | Type | Description |
| --- | --- | --- | --- |
| roleDefinitionId |Oui |String |Identificateur Hello du rôle de hello. format Hello de hello est la suivante :`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Oui |String |objectId du principal hello Azure AD (utilisateur, groupe ou principal du service) toowhich hello rôle est attribué. |

### <a name="response"></a>Réponse
Code d’état : 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Supprimer une affectation de rôle
Supprimer une attribution de rôle à hello spécifié étendue.

toodelete une attribution de rôle, vous devez avoir accès toohello `Microsoft.Authorization/roleAssignments/delete` opération. Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **supprimer** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez toocreate attributions hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-assignment-id}* avec l’id de l’attribution de rôle hello GUID.
3. Remplacez *{api-version}* par 2015-07-01.

### <a name="response"></a>Response
Code d’état : 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Répertorier tous les rôles
Répertorie tous les rôles hello qui sont disponibles pour l’attribution de hello spécifié étendue.

rôles de toolist, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/read` opération étendue hello. Tous les rôles intégrés hello sont accordées opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist les rôles hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{api-version}* par 2015-07-01.
3. Remplacez *{filter}* avec condition hello que vous souhaitez que la liste de hello tooapply toofilter des rôles :

   * Liste des rôles disponibles pour l’assignation à hello spécifié étendue et toutes ses étendues enfant :`atScopeAndBelow()`
   * Rechercher un rôle utilisant le nom d’affichage exact : `roleName%20eq%20'{role-display-name}'`. Utilisez hello forme codée URL de nom d’affichage exacte hello du rôle de hello. Par exemple, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Response
Code d’état : 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Obtention des informations sur un rôle
Obtient des informations sur un rôle unique spécifié par l’identificateur de définition de rôle hello. tooget d’informations sur un rôle unique à l’aide de son nom complet, consultez [liste de tous les rôles](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget des informations sur un rôle, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/read` opération. Tous les rôles intégrés hello sont accordées opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-definition-id}* avec l’identificateur GUID de hello de définition de rôle hello.
3. Remplacez *{api-version}* par 2015-07-01.

### <a name="response"></a>Response
Code d’état : 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Créer un rôle personnalisé
Créez un rôle personnalisé.

toocreate un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/write` opération sur tous les hello `AssignableScopes`. Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **PUT** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec hello première *AssignableScope* de rôle personnalisé de hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux.

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-definition-id}* avec un nouveau GUID, qui devient l’identificateur GUID de hello de nouveau rôle de hello personnalisé.
3. Remplacez *{api-version}* par 2015-07-01.

Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nom de l’élément | Requis | Type | Description |
| --- | --- | --- | --- |
| name |Oui |String |Identificateur GUID de rôle personnalisé de hello. |
| properties.roleName |Oui |String |Nom complet du rôle personnalisé de hello. Taille maximale de 128 caractères. |
| properties.description |Non |String |Description de rôle personnalisé de hello. Taille maximale de 1024 caractères. |
| properties.type |Oui |String |Définir trop « CustomRole ». |
| properties.permissions.actions |Oui |String[] |Tableau d’action des chaînes en spécifiant les opérations hello accordées par les rôles personnalisés hello. |
| properties.permissions.notActions |Non |String[] |Un tableau de chaînes d’action en spécifiant tooexclude d’opérations hello à partir d’opérations hello accordées par les rôles personnalisés hello. |
| properties.assignableScopes |Oui |String[] |Un tableau d’étendues dans le hello des rôles personnalisés peuvent être utilisés. |

### <a name="response"></a>Réponse
Code d’état : 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Mettre à jour un rôle personnalisé
Modifiez un rôle personnalisé.

toomodify un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/write` opération sur tous les hello `AssignableScopes`. Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **PUT** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec hello première *AssignableScope* de rôle personnalisé de hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-definition-id}* avec l’identificateur GUID de rôle personnalisé hello hello.
3. Remplacez *{api-version}* par 2015-07-01.

Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nom de l’élément | Requis | Type | Description |
| --- | --- | --- | --- |
| name |Oui |String |Identificateur GUID de rôle personnalisé de hello. |
| properties.roleName |Oui |String |Nom complet de hello mis à jour le rôle personnalisé. |
| properties.description |Non |String |Description de hello mis à jour le rôle personnalisé. |
| properties.type |Oui |String |Définir trop « CustomRole ». |
| properties.permissions.actions |Oui |String[] |Un tableau de chaînes d’action en spécifiant hello de toowhich hello opérations mis à jour personnalisées rôle accorde l’accès. |
| properties.permissions.notActions |Non |String[] |Tableau d’action chaînes tooexclude d’opérations hello en spécifiant des opérations hello quels hello mis à jour octroie des rôles personnalisés. |
| properties.assignableScopes |Oui |String[] |Un tableau d’étendues dans le hello des rôles personnalisés mis à jour peut être utilisé. |

### <a name="response"></a>Réponse
Code d’état : 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Supprimer un rôle personnalisé
Supprimez un rôle personnalisé.

toodelete un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/delete` opération sur tous les hello `AssignableScopes`. Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès. Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).

### <a name="request"></a>Demande
Hello d’utilisation **supprimer** méthode avec hello suivant l’URI :

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :

1. Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez la définition de rôle toodelete hello. Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :

   * Abonnement : /subscriptions/{subscription-id}  
   * Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Remplacez *{role-definition-id}* avec l’id de définition de rôle GUID hello de rôle personnalisé de hello.
3. Remplacez *{api-version}* par 2015-07-01.

### <a name="response"></a>Response
Code d’état : 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
