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
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="c0608-103">Gérer le contrôle d’accès en fonction du rôle avec l’API REST de hello</span><span class="sxs-lookup"><span data-stu-id="c0608-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0608-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0608-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="c0608-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c0608-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="c0608-106">API REST</span><span class="sxs-lookup"><span data-stu-id="c0608-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="c0608-107">Basé sur le rôle de contrôle d’accès (RBAC) Bonjour portail Azure et des API Azure Resource Manager vous permet de gérer l’accès tooyour abonnement et ressources à un niveau de granularité fin.</span><span class="sxs-lookup"><span data-stu-id="c0608-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="c0608-108">Avec cette fonctionnalité, vous pouvez accorder l’accès pour les utilisateurs, groupes ou principaux du service Active Directory en attribuant certains toothem de rôles à une portée particulière.</span><span class="sxs-lookup"><span data-stu-id="c0608-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="c0608-109">Répertorie toutes les affectations de rôle</span><span class="sxs-lookup"><span data-stu-id="c0608-109">List all role assignments</span></span>
<span data-ttu-id="c0608-110">Répertorie toutes les attributions de hello en hello spécifié étendue et subscopes.</span><span class="sxs-lookup"><span data-stu-id="c0608-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="c0608-111">attributions de rôles toolist, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/read` opération étendue hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="c0608-112">Tous les rôles intégrés hello sont accordées opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="c0608-113">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-114">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-114">Request</span></span>
<span data-ttu-id="c0608-115">Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="c0608-116">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-117">Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="c0608-118">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-119">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-120">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-121">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-122">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="c0608-123">Remplacez *{filter}* avec condition hello que vous souhaitez que la liste de l’attribution de rôle tooapply toofilter hello :</span><span class="sxs-lookup"><span data-stu-id="c0608-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="c0608-124">Liste des attributions de rôle pour hello uniquement spécifié étendue, y compris les attributions de rôles hello à subscopes ne pas :`atScope()`</span><span class="sxs-lookup"><span data-stu-id="c0608-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="c0608-125">Répertorier les affectations de rôle pour un utilisateur, un groupe ou une application spécifique : `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="c0608-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="c0608-126">Répertorier les affectations de rôle pour un utilisateur spécifique, y compris celles héritées de groupes | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="c0608-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="c0608-127">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-127">Response</span></span>
<span data-ttu-id="c0608-128">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="c0608-129">Obtention d’informations sur une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="c0608-129">Get information about a role assignment</span></span>
<span data-ttu-id="c0608-130">Obtient des informations sur une attribution de rôle unique spécifiée par l’identificateur de l’attribution de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="c0608-131">tooget plus d’informations sur une attribution de rôle, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/read` opération.</span><span class="sxs-lookup"><span data-stu-id="c0608-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="c0608-132">Tous les rôles intégrés hello sont accordées opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="c0608-133">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-134">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-134">Request</span></span>
<span data-ttu-id="c0608-135">Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="c0608-136">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-137">Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="c0608-138">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-139">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-140">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-141">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-142">Remplacez *{role-assignment-id}* avec l’identificateur GUID hello attribution de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="c0608-143">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="c0608-144">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-144">Response</span></span>
<span data-ttu-id="c0608-145">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="c0608-146">Créer une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="c0608-146">Create a Role Assignment</span></span>
<span data-ttu-id="c0608-147">Créer un rôle d’attribution à hello spécifié étendue pour hello spécifiée rôle spécifié principal qui accorde hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="c0608-148">toocreate une attribution de rôle, vous devez avoir accès trop`Microsoft.Authorization/roleAssignments/write` opération.</span><span class="sxs-lookup"><span data-stu-id="c0608-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="c0608-149">Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="c0608-150">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-151">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-151">Request</span></span>
<span data-ttu-id="c0608-152">Hello d’utilisation **PUT** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="c0608-153">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-154">Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez toocreate attributions hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="c0608-155">Lorsque vous créez une attribution de rôle à une portée parent, toutes les portées enfants héritent hello même attribution de rôle.</span><span class="sxs-lookup"><span data-stu-id="c0608-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="c0608-156">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-157">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-158">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="c0608-159">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-160">Remplacez *{role-assignment-id}* avec un nouveau GUID, qui devient l’identificateur GUID de hello de nouvelle attribution de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="c0608-161">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="c0608-162">Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c0608-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="c0608-163">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="c0608-163">Element Name</span></span> | <span data-ttu-id="c0608-164">Requis</span><span class="sxs-lookup"><span data-stu-id="c0608-164">Required</span></span> | <span data-ttu-id="c0608-165">Type</span><span class="sxs-lookup"><span data-stu-id="c0608-165">Type</span></span> | <span data-ttu-id="c0608-166">Description</span><span class="sxs-lookup"><span data-stu-id="c0608-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0608-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="c0608-167">roleDefinitionId</span></span> |<span data-ttu-id="c0608-168">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-168">Yes</span></span> |<span data-ttu-id="c0608-169">String</span><span class="sxs-lookup"><span data-stu-id="c0608-169">String</span></span> |<span data-ttu-id="c0608-170">Identificateur Hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-170">hello identifier of hello role.</span></span> <span data-ttu-id="c0608-171">format Hello de hello est la suivante :`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="c0608-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="c0608-172">principalId</span><span class="sxs-lookup"><span data-stu-id="c0608-172">principalId</span></span> |<span data-ttu-id="c0608-173">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-173">Yes</span></span> |<span data-ttu-id="c0608-174">String</span><span class="sxs-lookup"><span data-stu-id="c0608-174">String</span></span> |<span data-ttu-id="c0608-175">objectId du principal hello Azure AD (utilisateur, groupe ou principal du service) toowhich hello rôle est attribué.</span><span class="sxs-lookup"><span data-stu-id="c0608-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="c0608-176">Réponse</span><span class="sxs-lookup"><span data-stu-id="c0608-176">Response</span></span>
<span data-ttu-id="c0608-177">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="c0608-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="c0608-178">Supprimer une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="c0608-178">Delete a Role Assignment</span></span>
<span data-ttu-id="c0608-179">Supprimer une attribution de rôle à hello spécifié étendue.</span><span class="sxs-lookup"><span data-stu-id="c0608-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="c0608-180">toodelete une attribution de rôle, vous devez avoir accès toohello `Microsoft.Authorization/roleAssignments/delete` opération.</span><span class="sxs-lookup"><span data-stu-id="c0608-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="c0608-181">Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="c0608-182">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-183">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-183">Request</span></span>
<span data-ttu-id="c0608-184">Hello d’utilisation **supprimer** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="c0608-185">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-186">Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez toocreate attributions hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="c0608-187">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-188">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-189">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-190">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-191">Remplacez *{role-assignment-id}* avec l’id de l’attribution de rôle hello GUID.</span><span class="sxs-lookup"><span data-stu-id="c0608-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="c0608-192">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="c0608-193">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-193">Response</span></span>
<span data-ttu-id="c0608-194">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="c0608-195">Répertorier tous les rôles</span><span class="sxs-lookup"><span data-stu-id="c0608-195">List all Roles</span></span>
<span data-ttu-id="c0608-196">Répertorie tous les rôles hello qui sont disponibles pour l’attribution de hello spécifié étendue.</span><span class="sxs-lookup"><span data-stu-id="c0608-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="c0608-197">rôles de toolist, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/read` opération étendue hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="c0608-198">Tous les rôles intégrés hello sont accordées opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="c0608-199">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-200">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-200">Request</span></span>
<span data-ttu-id="c0608-201">Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="c0608-202">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-203">Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist les rôles hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="c0608-204">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-205">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-206">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-207">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-208">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="c0608-209">Remplacez *{filter}* avec condition hello que vous souhaitez que la liste de hello tooapply toofilter des rôles :</span><span class="sxs-lookup"><span data-stu-id="c0608-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="c0608-210">Liste des rôles disponibles pour l’assignation à hello spécifié étendue et toutes ses étendues enfant :`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="c0608-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="c0608-211">Rechercher un rôle utilisant le nom d’affichage exact : `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="c0608-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="c0608-212">Utilisez hello forme codée URL de nom d’affichage exacte hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="c0608-213">Par exemple, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="c0608-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="c0608-214">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-214">Response</span></span>
<span data-ttu-id="c0608-215">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-215">Status code: 200</span></span>

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

## <a name="get-information-about-a-role"></a><span data-ttu-id="c0608-216">Obtention des informations sur un rôle</span><span class="sxs-lookup"><span data-stu-id="c0608-216">Get information about a Role</span></span>
<span data-ttu-id="c0608-217">Obtient des informations sur un rôle unique spécifié par l’identificateur de définition de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="c0608-218">tooget d’informations sur un rôle unique à l’aide de son nom complet, consultez [liste de tous les rôles](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="c0608-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="c0608-219">tooget des informations sur un rôle, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/read` opération.</span><span class="sxs-lookup"><span data-stu-id="c0608-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="c0608-220">Tous les rôles intégrés hello sont accordées opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="c0608-221">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-222">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-222">Request</span></span>
<span data-ttu-id="c0608-223">Hello d’utilisation **obtenir** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="c0608-224">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-225">Remplacez *{scope}* avec une portée hello pour laquelle vous souhaitez toolist des attributions de rôles hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="c0608-226">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-227">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-228">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-229">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-230">Remplacez *{role-definition-id}* avec l’identificateur GUID de hello de définition de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="c0608-231">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="c0608-232">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-232">Response</span></span>
<span data-ttu-id="c0608-233">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-233">Status code: 200</span></span>

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

## <a name="create-a-custom-role"></a><span data-ttu-id="c0608-234">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="c0608-234">Create a Custom Role</span></span>
<span data-ttu-id="c0608-235">Créez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-235">Create a custom role.</span></span>

<span data-ttu-id="c0608-236">toocreate un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/write` opération sur tous les hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="c0608-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="c0608-237">Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="c0608-238">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-239">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-239">Request</span></span>
<span data-ttu-id="c0608-240">Hello d’utilisation **PUT** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="c0608-241">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-242">Remplacez *{scope}* avec hello première *AssignableScope* de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="c0608-243">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux.</span><span class="sxs-lookup"><span data-stu-id="c0608-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="c0608-244">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-245">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-246">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-247">Remplacez *{role-definition-id}* avec un nouveau GUID, qui devient l’identificateur GUID de hello de nouveau rôle de hello personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="c0608-248">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="c0608-249">Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c0608-249">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="c0608-250">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="c0608-250">Element Name</span></span> | <span data-ttu-id="c0608-251">Requis</span><span class="sxs-lookup"><span data-stu-id="c0608-251">Required</span></span> | <span data-ttu-id="c0608-252">Type</span><span class="sxs-lookup"><span data-stu-id="c0608-252">Type</span></span> | <span data-ttu-id="c0608-253">Description</span><span class="sxs-lookup"><span data-stu-id="c0608-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0608-254">name</span><span class="sxs-lookup"><span data-stu-id="c0608-254">name</span></span> |<span data-ttu-id="c0608-255">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-255">Yes</span></span> |<span data-ttu-id="c0608-256">String</span><span class="sxs-lookup"><span data-stu-id="c0608-256">String</span></span> |<span data-ttu-id="c0608-257">Identificateur GUID de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="c0608-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="c0608-258">properties.roleName</span></span> |<span data-ttu-id="c0608-259">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-259">Yes</span></span> |<span data-ttu-id="c0608-260">String</span><span class="sxs-lookup"><span data-stu-id="c0608-260">String</span></span> |<span data-ttu-id="c0608-261">Nom complet du rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-261">Display name of hello custom role.</span></span> <span data-ttu-id="c0608-262">Taille maximale de 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="c0608-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="c0608-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="c0608-263">properties.description</span></span> |<span data-ttu-id="c0608-264">Non</span><span class="sxs-lookup"><span data-stu-id="c0608-264">No</span></span> |<span data-ttu-id="c0608-265">String</span><span class="sxs-lookup"><span data-stu-id="c0608-265">String</span></span> |<span data-ttu-id="c0608-266">Description de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-266">Description of hello custom role.</span></span> <span data-ttu-id="c0608-267">Taille maximale de 1024 caractères.</span><span class="sxs-lookup"><span data-stu-id="c0608-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="c0608-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="c0608-268">properties.type</span></span> |<span data-ttu-id="c0608-269">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-269">Yes</span></span> |<span data-ttu-id="c0608-270">String</span><span class="sxs-lookup"><span data-stu-id="c0608-270">String</span></span> |<span data-ttu-id="c0608-271">Définir trop « CustomRole ».</span><span class="sxs-lookup"><span data-stu-id="c0608-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="c0608-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="c0608-272">properties.permissions.actions</span></span> |<span data-ttu-id="c0608-273">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-273">Yes</span></span> |<span data-ttu-id="c0608-274">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-274">String[]</span></span> |<span data-ttu-id="c0608-275">Tableau d’action des chaînes en spécifiant les opérations hello accordées par les rôles personnalisés hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="c0608-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="c0608-276">properties.permissions.notActions</span></span> |<span data-ttu-id="c0608-277">Non</span><span class="sxs-lookup"><span data-stu-id="c0608-277">No</span></span> |<span data-ttu-id="c0608-278">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-278">String[]</span></span> |<span data-ttu-id="c0608-279">Un tableau de chaînes d’action en spécifiant tooexclude d’opérations hello à partir d’opérations hello accordées par les rôles personnalisés hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="c0608-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="c0608-280">properties.assignableScopes</span></span> |<span data-ttu-id="c0608-281">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-281">Yes</span></span> |<span data-ttu-id="c0608-282">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-282">String[]</span></span> |<span data-ttu-id="c0608-283">Un tableau d’étendues dans le hello des rôles personnalisés peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="c0608-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="c0608-284">Réponse</span><span class="sxs-lookup"><span data-stu-id="c0608-284">Response</span></span>
<span data-ttu-id="c0608-285">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="c0608-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="c0608-286">Mettre à jour un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="c0608-286">Update a Custom Role</span></span>
<span data-ttu-id="c0608-287">Modifiez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-287">Modify a custom role.</span></span>

<span data-ttu-id="c0608-288">toomodify un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/write` opération sur tous les hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="c0608-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="c0608-289">Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="c0608-290">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-291">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-291">Request</span></span>
<span data-ttu-id="c0608-292">Hello d’utilisation **PUT** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="c0608-293">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-294">Remplacez *{scope}* avec hello première *AssignableScope* de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="c0608-295">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-296">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-297">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-298">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-299">Remplacez *{role-definition-id}* avec l’identificateur GUID de rôle personnalisé hello hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="c0608-300">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="c0608-301">Pour le corps de demande hello, fournir des valeurs de hello Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c0608-301">For hello request body, provide hello values in hello following format:</span></span>

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

| <span data-ttu-id="c0608-302">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="c0608-302">Element Name</span></span> | <span data-ttu-id="c0608-303">Requis</span><span class="sxs-lookup"><span data-stu-id="c0608-303">Required</span></span> | <span data-ttu-id="c0608-304">Type</span><span class="sxs-lookup"><span data-stu-id="c0608-304">Type</span></span> | <span data-ttu-id="c0608-305">Description</span><span class="sxs-lookup"><span data-stu-id="c0608-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0608-306">name</span><span class="sxs-lookup"><span data-stu-id="c0608-306">name</span></span> |<span data-ttu-id="c0608-307">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-307">Yes</span></span> |<span data-ttu-id="c0608-308">String</span><span class="sxs-lookup"><span data-stu-id="c0608-308">String</span></span> |<span data-ttu-id="c0608-309">Identificateur GUID de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="c0608-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="c0608-310">properties.roleName</span></span> |<span data-ttu-id="c0608-311">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-311">Yes</span></span> |<span data-ttu-id="c0608-312">String</span><span class="sxs-lookup"><span data-stu-id="c0608-312">String</span></span> |<span data-ttu-id="c0608-313">Nom complet de hello mis à jour le rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="c0608-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="c0608-314">properties.description</span></span> |<span data-ttu-id="c0608-315">Non</span><span class="sxs-lookup"><span data-stu-id="c0608-315">No</span></span> |<span data-ttu-id="c0608-316">String</span><span class="sxs-lookup"><span data-stu-id="c0608-316">String</span></span> |<span data-ttu-id="c0608-317">Description de hello mis à jour le rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="c0608-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="c0608-318">properties.type</span></span> |<span data-ttu-id="c0608-319">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-319">Yes</span></span> |<span data-ttu-id="c0608-320">String</span><span class="sxs-lookup"><span data-stu-id="c0608-320">String</span></span> |<span data-ttu-id="c0608-321">Définir trop « CustomRole ».</span><span class="sxs-lookup"><span data-stu-id="c0608-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="c0608-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="c0608-322">properties.permissions.actions</span></span> |<span data-ttu-id="c0608-323">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-323">Yes</span></span> |<span data-ttu-id="c0608-324">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-324">String[]</span></span> |<span data-ttu-id="c0608-325">Un tableau de chaînes d’action en spécifiant hello de toowhich hello opérations mis à jour personnalisées rôle accorde l’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="c0608-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="c0608-326">properties.permissions.notActions</span></span> |<span data-ttu-id="c0608-327">Non</span><span class="sxs-lookup"><span data-stu-id="c0608-327">No</span></span> |<span data-ttu-id="c0608-328">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-328">String[]</span></span> |<span data-ttu-id="c0608-329">Tableau d’action chaînes tooexclude d’opérations hello en spécifiant des opérations hello quels hello mis à jour octroie des rôles personnalisés.</span><span class="sxs-lookup"><span data-stu-id="c0608-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="c0608-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="c0608-330">properties.assignableScopes</span></span> |<span data-ttu-id="c0608-331">Oui</span><span class="sxs-lookup"><span data-stu-id="c0608-331">Yes</span></span> |<span data-ttu-id="c0608-332">String[]</span><span class="sxs-lookup"><span data-stu-id="c0608-332">String[]</span></span> |<span data-ttu-id="c0608-333">Un tableau d’étendues dans le hello des rôles personnalisés mis à jour peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="c0608-334">Réponse</span><span class="sxs-lookup"><span data-stu-id="c0608-334">Response</span></span>
<span data-ttu-id="c0608-335">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="c0608-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="c0608-336">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="c0608-336">Delete a Custom Role</span></span>
<span data-ttu-id="c0608-337">Supprimez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c0608-337">Delete a custom role.</span></span>

<span data-ttu-id="c0608-338">toodelete un rôle personnalisé, vous devez avoir accès trop`Microsoft.Authorization/roleDefinitions/delete` opération sur tous les hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="c0608-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="c0608-339">Hello rôles intégrés uniquement *propriétaire* et *administrateur de l’accès utilisateur* bénéficient d’opération toothis d’accès.</span><span class="sxs-lookup"><span data-stu-id="c0608-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="c0608-340">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0608-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="c0608-341">Demande</span><span class="sxs-lookup"><span data-stu-id="c0608-341">Request</span></span>
<span data-ttu-id="c0608-342">Hello d’utilisation **supprimer** méthode avec hello suivant l’URI :</span><span class="sxs-lookup"><span data-stu-id="c0608-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="c0608-343">Dans l’URI de hello, effectuez hello après les substitutions toocustomize votre demande :</span><span class="sxs-lookup"><span data-stu-id="c0608-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="c0608-344">Remplacez *{scope}* avec une portée hello à laquelle vous souhaitez la définition de rôle toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="c0608-345">Hello suivant exemples montrent comment toospecify hello étendue pour différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="c0608-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="c0608-346">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="c0608-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="c0608-347">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="c0608-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="c0608-348">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="c0608-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="c0608-349">Remplacez *{role-definition-id}* avec l’id de définition de rôle GUID hello de rôle personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c0608-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="c0608-350">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="c0608-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="c0608-351">Response</span><span class="sxs-lookup"><span data-stu-id="c0608-351">Response</span></span>
<span data-ttu-id="c0608-352">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="c0608-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c0608-353">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0608-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
