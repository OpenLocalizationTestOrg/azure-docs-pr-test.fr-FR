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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="e9c80-103">Élever l’accès en tant qu’administrateur client avec le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="e9c80-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="e9c80-104">Le contrôle d’accès en fonction du rôle permet aux administrateurs clients d’obtenir des élévations temporaires d’accès grâce auxquelles ils peuvent accorder des autorisations plus élevées que la normale.</span><span class="sxs-lookup"><span data-stu-id="e9c80-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="e9c80-105">Un administrateur locataire peut elle-même élever toohello rôle d’utilisateur administrateur de l’accès si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e9c80-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="e9c80-106">Ce rôle donne hello toogrant des autorisations administrateur de locataire elle-même ou autres rôles sur hello étendue « / ».</span><span class="sxs-lookup"><span data-stu-id="e9c80-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="e9c80-107">Cette fonctionnalité est importante car elle permet de client de hello toosee admin que tous hello abonnements qui existent dans une organisation.</span><span class="sxs-lookup"><span data-stu-id="e9c80-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="e9c80-108">Également, il permet à tous les abonnements hello pour tooaccess d’applications (par exemple, la facturation et d’audit) automation et fournissent une vue précise de l’état de hello d’organisation hello pour la gestion de la facturation ou actif.</span><span class="sxs-lookup"><span data-stu-id="e9c80-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="e9c80-109">Comment toouse elevateAccess toogive client access</span><span class="sxs-lookup"><span data-stu-id="e9c80-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="e9c80-110">processus de base Hello fonctionne avec hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e9c80-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="e9c80-111">À l’aide de REST, appelez *elevateAccess*, qui accorde vous hello du rôle d’administrateur de l’accès utilisateur au « / » de portée.</span><span class="sxs-lookup"><span data-stu-id="e9c80-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="e9c80-112">Créer un [attribution de rôle](/rest/api/authorization/roleassignments) tooassign n’importe quel rôle au niveau de n’importe quelle étendue.</span><span class="sxs-lookup"><span data-stu-id="e9c80-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="e9c80-113">Hello, l’exemple suivant montre les propriétés hello pour l’assignation hello le rôle de lecteur au « / » à l’étendue :</span><span class="sxs-lookup"><span data-stu-id="e9c80-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="e9c80-114">En tant qu’administrateur des accès utilisateur, vous pouvez également supprimer des attributions de rôles au niveau de l’étendue « / ».</span><span class="sxs-lookup"><span data-stu-id="e9c80-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="e9c80-115">Révoquez vos privilèges d’administrateur des accès utilisateur jusqu’à ce que vous en ayez à nouveau besoin.</span><span class="sxs-lookup"><span data-stu-id="e9c80-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="e9c80-116">Comment tooundo hello elevateAccess action</span><span class="sxs-lookup"><span data-stu-id="e9c80-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="e9c80-117">Lorsque vous appelez *elevateAccess* vous créez une attribution de rôle pour vous-même, donc toorevoke les privilèges vous devez toodelete hello affectation.</span><span class="sxs-lookup"><span data-stu-id="e9c80-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="e9c80-118">Appelez [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) où roleName = toodetermine de l’administrateur de l’accès utilisateur hello nom GUID du rôle d’administrateur de l’accès utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="e9c80-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="e9c80-119">réponse de Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e9c80-119">hello response should look like this:</span></span>

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

    <span data-ttu-id="e9c80-120">Enregistrer hello GUID à partir de hello *nom* paramètre, dans ce cas **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="e9c80-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="e9c80-121">Appelez [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), où principalId = votre propre ObjectId.</span><span class="sxs-lookup"><span data-stu-id="e9c80-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="e9c80-122">Celle-ci répertorie toutes les attributions de votre client de hello.</span><span class="sxs-lookup"><span data-stu-id="e9c80-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="e9c80-123">Recherchez hello une où la portée de hello est « / » et se termine de RoleDefinitionId hello avec le rôle de hello nom GUID trouvé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e9c80-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="e9c80-124">attribution de rôle Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="e9c80-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="e9c80-125">Là encore, enregistrez hello GUID à partir de hello *nom* paramètre, dans ce cas **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="e9c80-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="e9c80-126">Enfin, appelez [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) où roleAssignmentId = hello nom GUID trouvé à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="e9c80-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9c80-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e9c80-127">Next steps</span></span>

- <span data-ttu-id="e9c80-128">En savoir plus sur la [gestion du contrôle d’accès en fonction du rôle à l’aide de REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="e9c80-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="e9c80-129">[Gérer les affectations d’accès](role-based-access-control-manage-assignments.md) Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="e9c80-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
