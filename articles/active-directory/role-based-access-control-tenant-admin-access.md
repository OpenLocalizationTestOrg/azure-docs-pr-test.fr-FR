---
title: "Élever l’accès d’un administrateur client - Azure AD | Microsoft Docs"
description: "Cette rubrique décrit les rôles intégrés pour le contrôle d’accès en fonction du rôle (RBAC)."
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
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="0a7a2-103">Élever l’accès en tant qu’administrateur client avec le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="0a7a2-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="0a7a2-104">Le contrôle d’accès en fonction du rôle permet aux administrateurs clients d’obtenir des élévations temporaires d’accès grâce auxquelles ils peuvent accorder des autorisations plus élevées que la normale.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="0a7a2-105">Un administrateur client peut s’élever lui-même au rôle d’administrateur des accès utilisateur si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="0a7a2-106">Ce rôle donne à l’administrateur client les autorisations nécessaires pour accorder à lui-même ou à d’autres des rôles au niveau de l’étendue « / ».</span><span class="sxs-lookup"><span data-stu-id="0a7a2-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="0a7a2-107">Cette fonctionnalité est importante, car elle permet à l’administrateur client d’afficher tous les abonnements qui existent dans une organisation.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="0a7a2-108">Elle permet également aux applications d’automatisation (comme la facturation et les audits) d’accéder à tous les abonnements et de fournir une vue précise de l’état de l’organisation pour la facturation et la gestion des actifs.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="0a7a2-109">Utiliser elevateAccess pour donner l’accès client</span><span class="sxs-lookup"><span data-stu-id="0a7a2-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="0a7a2-110">Le processus de base comprend les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0a7a2-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="0a7a2-111">Avec REST, appelez *elevateAccess*, qui vous accorde le rôle d’administrateur des accès utilisateur au niveau de l’étendue « / ».</span><span class="sxs-lookup"><span data-stu-id="0a7a2-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="0a7a2-112">Créez une [attribution de rôle](/rest/api/authorization/roleassignments) pour attribuer le rôle de votre choix quelle que soit l’étendue.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="0a7a2-113">L’exemple suivant montre les propriétés permettant d’attribuer le rôle de lecteur au niveau de l’étendue « / » :</span><span class="sxs-lookup"><span data-stu-id="0a7a2-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="0a7a2-114">En tant qu’administrateur des accès utilisateur, vous pouvez également supprimer des attributions de rôles au niveau de l’étendue « / ».</span><span class="sxs-lookup"><span data-stu-id="0a7a2-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="0a7a2-115">Révoquez vos privilèges d’administrateur des accès utilisateur jusqu’à ce que vous en ayez à nouveau besoin.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="0a7a2-116">Annuler l’action elevateAccess</span><span class="sxs-lookup"><span data-stu-id="0a7a2-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="0a7a2-117">Lorsque vous appelez *elevateAccess*, vous créez une attribution de rôle pour vous-même : pour révoquer ces privilèges, vous devez donc supprimer l’attribution.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="0a7a2-118">Appelez [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get), où roleName = administrateur des accès utilisateur, pour déterminer le GUID de nom du rôle d’administrateur des accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="0a7a2-119">La réponse est de ce type :</span><span class="sxs-lookup"><span data-stu-id="0a7a2-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
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

    <span data-ttu-id="0a7a2-120">Enregistrez le GUID du paramètre *name*, dans ce cas **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="0a7a2-121">Appelez [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), où principalId = votre propre ObjectId.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="0a7a2-122">Cette action liste toutes vos attributions dans le client.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="0a7a2-123">Recherchez celui dont l’étendue est « / » et le RoleDefinitionId se termine par le GUID du nom de rôle que vous avez trouvé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="0a7a2-124">L’attribution de rôle doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="0a7a2-124">The role assignment should look like this:</span></span>

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

    <span data-ttu-id="0a7a2-125">Ici encore, enregistrez le GUID du paramètre *name*, dans ce cas **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="0a7a2-126">Enfin, appelez [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById), où roleAssignmentId = le GUID de nom que vous avez trouvé à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="0a7a2-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a7a2-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a7a2-127">Next steps</span></span>

- <span data-ttu-id="0a7a2-128">En savoir plus sur la [gestion du contrôle d’accès en fonction du rôle à l’aide de REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="0a7a2-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="0a7a2-129">[Gérer les attributions d’accès](role-based-access-control-manage-assignments.md) dans le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0a7a2-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
