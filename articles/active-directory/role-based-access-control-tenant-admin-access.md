---
title: "aaaTenant admin élever accès - Azure AD | Documents Microsoft"
description: "Cette rubrique décrit hello généré dans des rôles pour le contrôle d’accès basé sur un rôle (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Élever l’accès en tant qu’administrateur client avec le contrôle d’accès en fonction du rôle

Le contrôle d’accès en fonction du rôle permet aux administrateurs clients d’obtenir des élévations temporaires d’accès grâce auxquelles ils peuvent accorder des autorisations plus élevées que la normale. Un administrateur locataire peut elle-même élever toohello rôle d’utilisateur administrateur de l’accès si nécessaire. Ce rôle donne hello toogrant des autorisations administrateur de locataire elle-même ou autres rôles sur hello étendue « / ».

Cette fonctionnalité est importante car elle permet de client de hello toosee admin que tous hello abonnements qui existent dans une organisation. Également, il permet à tous les abonnements hello pour tooaccess d’applications (par exemple, la facturation et d’audit) automation et fournissent une vue précise de l’état de hello d’organisation hello pour la gestion de la facturation ou actif.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Comment toouse elevateAccess toogive client access

processus de base Hello fonctionne avec hello comme suit :

1. À l’aide de REST, appelez *elevateAccess*, qui accorde vous hello du rôle d’administrateur de l’accès utilisateur au « / » de portée.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Créer un [attribution de rôle](/rest/api/authorization/roleassignments) tooassign n’importe quel rôle au niveau de n’importe quelle étendue. Hello, l’exemple suivant montre les propriétés hello pour l’assignation hello le rôle de lecteur au « / » à l’étendue :

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. En tant qu’administrateur des accès utilisateur, vous pouvez également supprimer des attributions de rôles au niveau de l’étendue « / ».

4. Révoquez vos privilèges d’administrateur des accès utilisateur jusqu’à ce que vous en ayez à nouveau besoin.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Comment tooundo hello elevateAccess action

Lorsque vous appelez *elevateAccess* vous créez une attribution de rôle pour vous-même, donc toorevoke les privilèges vous devez toodelete hello affectation.

1.  Appelez [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) où roleName = toodetermine de l’administrateur de l’accès utilisateur hello nom GUID du rôle d’administrateur de l’accès utilisateur hello. réponse de Hello doit ressembler à ceci :

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    Enregistrer hello GUID à partir de hello *nom* paramètre, dans ce cas **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Appelez [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), où principalId = votre propre ObjectId. Celle-ci répertorie toutes les attributions de votre client de hello. Recherchez hello une où la portée de hello est « / » et se termine de RoleDefinitionId hello avec le rôle de hello nom GUID trouvé à l’étape 1. attribution de rôle Hello doit ressembler à ceci :

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    Là encore, enregistrez hello GUID à partir de hello *nom* paramètre, dans ce cas **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Enfin, appelez [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) où roleAssignmentId = hello nom GUID trouvé à l’étape 2.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la [gestion du contrôle d’accès en fonction du rôle à l’aide de REST](role-based-access-control-manage-access-rest.md)

- [Gérer les affectations d’accès](role-based-access-control-manage-assignments.md) Bonjour portail Azure
