---
title: "Contrôle d’accès en fonction des rôles avec REST - Azure AD | Microsoft Docs"
description: "Gestion du contrôle d’accès basé sur les rôles à l’aide de l’API REST"
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="f9d82-103">Gérer le contrôle d’accès en fonction des rôles à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="f9d82-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9d82-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9d82-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="f9d82-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f9d82-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="f9d82-106">API REST</span><span class="sxs-lookup"><span data-stu-id="f9d82-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="f9d82-107">Le contrôle d’accès en fonction du rôle (RBAC) disponible dans le portail Azure et l’API Azure Resource Manager permet une gestion très fine de l’accès à votre abonnement et à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="f9d82-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="f9d82-108">Cette fonctionnalité vous permet d’accorder l’accès aux utilisateurs, groupes et principaux du service Active Directory en leur affectant certains rôles avec une étendue spécifique.</span><span class="sxs-lookup"><span data-stu-id="f9d82-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="f9d82-109">Répertorie toutes les affectations de rôle</span><span class="sxs-lookup"><span data-stu-id="f9d82-109">List all role assignments</span></span>
<span data-ttu-id="f9d82-110">Répertorie toutes les affectations de rôle de la portée spécifiée et des étendues secondaires.</span><span class="sxs-lookup"><span data-stu-id="f9d82-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="f9d82-111">Pour répertorier les attributions de rôle, vous devez avoir accès à l’opération `Microsoft.Authorization/roleAssignments/read` dans la portée.</span><span class="sxs-lookup"><span data-stu-id="f9d82-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="f9d82-112">Tous les rôles intégrés se voient octroyer l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f9d82-113">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-114">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-114">Request</span></span>
<span data-ttu-id="f9d82-115">Utilisez la méthode **GET** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="f9d82-116">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-117">Remplacez *{scope}* par la portée dont vous souhaitez répertorier les attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f9d82-118">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-119">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-120">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-121">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-122">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="f9d82-123">Remplacez *{filter}* par la condition que vous souhaitez appliquer pour filtrer la liste des attributions de rôle :</span><span class="sxs-lookup"><span data-stu-id="f9d82-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="f9d82-124">Répertorier les affectations de rôle pour la portée spécifiée seulement, sans y inclure les affectations de rôles à des étendues secondaires : `atScope()`</span><span class="sxs-lookup"><span data-stu-id="f9d82-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="f9d82-125">Répertorier les affectations de rôle pour un utilisateur, un groupe ou une application spécifique : `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="f9d82-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="f9d82-126">Répertorier les affectations de rôle pour un utilisateur spécifique, y compris celles héritées de groupes | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="f9d82-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-127">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-127">Response</span></span>
<span data-ttu-id="f9d82-128">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="f9d82-129">Obtention d’informations sur une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="f9d82-129">Get information about a role assignment</span></span>
<span data-ttu-id="f9d82-130">Obtient des informations sur une affectation de rôle unique spécifiée par l’identificateur d’affectation de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="f9d82-131">Pour obtenir des informations sur une affectation de rôle, vous devez avoir accès à l’opération `Microsoft.Authorization/roleAssignments/read` .</span><span class="sxs-lookup"><span data-stu-id="f9d82-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="f9d82-132">Tous les rôles intégrés se voient octroyer l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f9d82-133">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-134">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-134">Request</span></span>
<span data-ttu-id="f9d82-135">Utilisez la méthode **GET** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f9d82-136">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-137">Remplacez *{scope}* par la portée dont vous souhaitez répertorier les attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f9d82-138">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-139">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-140">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-141">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-142">Remplacez *{role-assignment-id}* par l’identificateur GUID de l’attribution de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="f9d82-143">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-144">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-144">Response</span></span>
<span data-ttu-id="f9d82-145">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="f9d82-146">Créer une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="f9d82-146">Create a Role Assignment</span></span>
<span data-ttu-id="f9d82-147">Créer une affectation de rôle dans la portée spécifiée pour le principal qui octroie le rôle spécifié.</span><span class="sxs-lookup"><span data-stu-id="f9d82-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="f9d82-148">Pour créer une attribution de rôle, vous devez avoir accès à l’opération `Microsoft.Authorization/roleAssignments/write` .</span><span class="sxs-lookup"><span data-stu-id="f9d82-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="f9d82-149">Parmi les rôles intégrés, seuls ceux du *propriétaire* et de *l’administrateur des accès utilisateur* se voient accorder l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f9d82-150">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-151">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-151">Request</span></span>
<span data-ttu-id="f9d82-152">Utilisez la méthode **PUT** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f9d82-153">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-154">Remplacez *{scope}* par la portée sur laquelle vous souhaitez créer les attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="f9d82-155">Lorsque vous créez une affectation de rôle pour une portée parent, toutes les portées enfants en héritent.</span><span class="sxs-lookup"><span data-stu-id="f9d82-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="f9d82-156">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-157">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-158">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="f9d82-159">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-160">Remplacez *{role-assignment-id}* par un nouveau GUID, qui devient l’identificateur GUID de la nouvelle attribution de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="f9d82-161">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f9d82-162">Pour le corps de la requête, saisissez les valeurs au format suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="f9d82-163">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="f9d82-163">Element Name</span></span> | <span data-ttu-id="f9d82-164">Requis</span><span class="sxs-lookup"><span data-stu-id="f9d82-164">Required</span></span> | <span data-ttu-id="f9d82-165">Type</span><span class="sxs-lookup"><span data-stu-id="f9d82-165">Type</span></span> | <span data-ttu-id="f9d82-166">Description</span><span class="sxs-lookup"><span data-stu-id="f9d82-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9d82-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="f9d82-167">roleDefinitionId</span></span> |<span data-ttu-id="f9d82-168">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-168">Yes</span></span> |<span data-ttu-id="f9d82-169">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-169">String</span></span> |<span data-ttu-id="f9d82-170">L’identificateur du rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-170">The identifier of the role.</span></span> <span data-ttu-id="f9d82-171">Le format de l’identificateur est : `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="f9d82-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="f9d82-172">principalId</span><span class="sxs-lookup"><span data-stu-id="f9d82-172">principalId</span></span> |<span data-ttu-id="f9d82-173">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-173">Yes</span></span> |<span data-ttu-id="f9d82-174">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-174">String</span></span> |<span data-ttu-id="f9d82-175">objectId du principal Azure AD (utilisateur, groupe ou principal de service) auquel le rôle est affecté.</span><span class="sxs-lookup"><span data-stu-id="f9d82-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="f9d82-176">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-176">Response</span></span>
<span data-ttu-id="f9d82-177">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="f9d82-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="f9d82-178">Supprimer une affectation de rôle</span><span class="sxs-lookup"><span data-stu-id="f9d82-178">Delete a Role Assignment</span></span>
<span data-ttu-id="f9d82-179">Supprimez une affectation de rôle au niveau de la portée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f9d82-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="f9d82-180">Pour supprimer une attribution de rôle, vous devez avoir accès à l’opération `Microsoft.Authorization/roleAssignments/delete` .</span><span class="sxs-lookup"><span data-stu-id="f9d82-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="f9d82-181">Parmi les rôles intégrés, seuls ceux du *propriétaire* et de *l’administrateur des accès utilisateur* se voient accorder l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f9d82-182">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-183">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-183">Request</span></span>
<span data-ttu-id="f9d82-184">Utilisez la méthode **DELETE** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="f9d82-185">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-186">Remplacez *{scope}* par la portée sur laquelle vous souhaitez créer les attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="f9d82-187">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-188">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-189">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-190">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-191">Remplacez *{role-assignment-id}* par le GUID de l’ID d’attribution de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="f9d82-192">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-193">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-193">Response</span></span>
<span data-ttu-id="f9d82-194">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="f9d82-195">Répertorier tous les rôles</span><span class="sxs-lookup"><span data-stu-id="f9d82-195">List all Roles</span></span>
<span data-ttu-id="f9d82-196">Répertorie tous les rôles disponibles à l’attribution sur la portée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="f9d82-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="f9d82-197">Pour répertorier les rôles, vous devez avoir accès à l’opération `Microsoft.Authorization/roleDefinitions/read` dans la portée.</span><span class="sxs-lookup"><span data-stu-id="f9d82-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="f9d82-198">Tous les rôles intégrés se voient octroyer l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f9d82-199">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-200">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-200">Request</span></span>
<span data-ttu-id="f9d82-201">Utilisez la méthode **GET** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="f9d82-202">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-203">Remplacez *{scope}* par la portée dont vous souhaitez répertorier les rôles.</span><span class="sxs-lookup"><span data-stu-id="f9d82-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="f9d82-204">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-205">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-206">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-207">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-208">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="f9d82-209">Remplacez *{filter}* par la condition que vous souhaitez appliquer pour filtrer la liste des rôles :</span><span class="sxs-lookup"><span data-stu-id="f9d82-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="f9d82-210">Répertorier les rôles disponibles à l’affectation à la portée spécifiée et chacune de ses portées enfants : `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="f9d82-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="f9d82-211">Rechercher un rôle utilisant le nom d’affichage exact : `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="f9d82-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="f9d82-212">Utilisez la forme codée de l’URL du nom d’affichage exact du rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="f9d82-213">Par exemple, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="f9d82-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-214">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-214">Response</span></span>
<span data-ttu-id="f9d82-215">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="f9d82-216">Obtention des informations sur un rôle</span><span class="sxs-lookup"><span data-stu-id="f9d82-216">Get information about a Role</span></span>
<span data-ttu-id="f9d82-217">Obtient des informations sur un rôle unique spécifié par l’identificateur de définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="f9d82-218">Pour obtenir des informations sur un rôle unique en utilisant son nom d’affichage, voir [Répertorier tous les rôles](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="f9d82-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="f9d82-219">Pour obtenir des informations sur un rôle, vous devez avoir accès à l’opération `Microsoft.Authorization/roleDefinitions/read` .</span><span class="sxs-lookup"><span data-stu-id="f9d82-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="f9d82-220">Tous les rôles intégrés se voient octroyer l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="f9d82-221">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-222">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-222">Request</span></span>
<span data-ttu-id="f9d82-223">Utilisez la méthode **GET** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f9d82-224">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-225">Remplacez *{scope}* par la portée dont vous souhaitez répertorier les attributions de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="f9d82-226">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-227">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-228">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-229">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-230">Remplacez *{role-definition-id}* par l’identificateur de définition GUID de la définition du rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="f9d82-231">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-232">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-232">Response</span></span>
<span data-ttu-id="f9d82-233">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="f9d82-234">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="f9d82-234">Create a Custom Role</span></span>
<span data-ttu-id="f9d82-235">Créez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-235">Create a custom role.</span></span>

<span data-ttu-id="f9d82-236">Pour créer un rôle personnalisé, vous devez avoir accès à l’opération `Microsoft.Authorization/roleDefinitions/write` sur l’ensemble des `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f9d82-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f9d82-237">Parmi les rôles intégrés, seuls ceux du *propriétaire* et de *l’administrateur des accès utilisateur* se voient accorder l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f9d82-238">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-239">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-239">Request</span></span>
<span data-ttu-id="f9d82-240">Utilisez la méthode **PUT** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f9d82-241">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-242">Remplacez *{scope}* par le premier élément *AssignableScope* du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="f9d82-243">Les exemples qui suivent montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="f9d82-244">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-245">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-246">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-247">Remplacez *{role-assignment-id}* par un nouveau GUID, qui devient l’identificateur GUID du nouveau rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="f9d82-248">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f9d82-249">Pour le corps de la requête, saisissez les valeurs au format suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="f9d82-250">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="f9d82-250">Element Name</span></span> | <span data-ttu-id="f9d82-251">Requis</span><span class="sxs-lookup"><span data-stu-id="f9d82-251">Required</span></span> | <span data-ttu-id="f9d82-252">Type</span><span class="sxs-lookup"><span data-stu-id="f9d82-252">Type</span></span> | <span data-ttu-id="f9d82-253">Description</span><span class="sxs-lookup"><span data-stu-id="f9d82-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9d82-254">name</span><span class="sxs-lookup"><span data-stu-id="f9d82-254">name</span></span> |<span data-ttu-id="f9d82-255">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-255">Yes</span></span> |<span data-ttu-id="f9d82-256">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-256">String</span></span> |<span data-ttu-id="f9d82-257">Identificateur GUID du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="f9d82-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="f9d82-258">properties.roleName</span></span> |<span data-ttu-id="f9d82-259">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-259">Yes</span></span> |<span data-ttu-id="f9d82-260">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-260">String</span></span> |<span data-ttu-id="f9d82-261">Afficher le nom complet du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-261">Display name of the custom role.</span></span> <span data-ttu-id="f9d82-262">Taille maximale de 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="f9d82-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="f9d82-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="f9d82-263">properties.description</span></span> |<span data-ttu-id="f9d82-264">Non</span><span class="sxs-lookup"><span data-stu-id="f9d82-264">No</span></span> |<span data-ttu-id="f9d82-265">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-265">String</span></span> |<span data-ttu-id="f9d82-266">Description du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-266">Description of the custom role.</span></span> <span data-ttu-id="f9d82-267">Taille maximale de 1024 caractères.</span><span class="sxs-lookup"><span data-stu-id="f9d82-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="f9d82-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="f9d82-268">properties.type</span></span> |<span data-ttu-id="f9d82-269">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-269">Yes</span></span> |<span data-ttu-id="f9d82-270">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-270">String</span></span> |<span data-ttu-id="f9d82-271">Affectez la valeur « CustomRole ».</span><span class="sxs-lookup"><span data-stu-id="f9d82-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="f9d82-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="f9d82-272">properties.permissions.actions</span></span> |<span data-ttu-id="f9d82-273">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-273">Yes</span></span> |<span data-ttu-id="f9d82-274">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-274">String[]</span></span> |<span data-ttu-id="f9d82-275">Tableau de chaînes d’action spécifiant les opérations octroyées par le rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="f9d82-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="f9d82-276">properties.permissions.notActions</span></span> |<span data-ttu-id="f9d82-277">Non</span><span class="sxs-lookup"><span data-stu-id="f9d82-277">No</span></span> |<span data-ttu-id="f9d82-278">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-278">String[]</span></span> |<span data-ttu-id="f9d82-279">Tableau de chaînes d’action spécifiant les opérations à exclure des opérations octroyées par le rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="f9d82-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="f9d82-280">properties.assignableScopes</span></span> |<span data-ttu-id="f9d82-281">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-281">Yes</span></span> |<span data-ttu-id="f9d82-282">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-282">String[]</span></span> |<span data-ttu-id="f9d82-283">Tableau des portées dans lesquelles le rôle personnalisé peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="f9d82-284">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-284">Response</span></span>
<span data-ttu-id="f9d82-285">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="f9d82-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="f9d82-286">Mettre à jour un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="f9d82-286">Update a Custom Role</span></span>
<span data-ttu-id="f9d82-287">Modifiez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-287">Modify a custom role.</span></span>

<span data-ttu-id="f9d82-288">Pour modifier un rôle personnalisé, vous devez avoir accès à l’opération `Microsoft.Authorization/roleDefinitions/write` sur l’ensemble des `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f9d82-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f9d82-289">Parmi les rôles intégrés, seuls ceux du *propriétaire* et de *l’administrateur des accès utilisateur* se voient accorder l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f9d82-290">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-291">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-291">Request</span></span>
<span data-ttu-id="f9d82-292">Utilisez la méthode **PUT** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f9d82-293">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-294">Remplacez *{scope}* par le premier élément *AssignableScope* du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="f9d82-295">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-296">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-297">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-298">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-299">Remplacez *{role-definition-id}* par l’identificateur de définition GUID du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="f9d82-300">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="f9d82-301">Pour le corps de la requête, saisissez les valeurs au format suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="f9d82-302">Nom de l’élément</span><span class="sxs-lookup"><span data-stu-id="f9d82-302">Element Name</span></span> | <span data-ttu-id="f9d82-303">Requis</span><span class="sxs-lookup"><span data-stu-id="f9d82-303">Required</span></span> | <span data-ttu-id="f9d82-304">Type</span><span class="sxs-lookup"><span data-stu-id="f9d82-304">Type</span></span> | <span data-ttu-id="f9d82-305">Description</span><span class="sxs-lookup"><span data-stu-id="f9d82-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f9d82-306">name</span><span class="sxs-lookup"><span data-stu-id="f9d82-306">name</span></span> |<span data-ttu-id="f9d82-307">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-307">Yes</span></span> |<span data-ttu-id="f9d82-308">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-308">String</span></span> |<span data-ttu-id="f9d82-309">Identificateur GUID du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="f9d82-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="f9d82-310">properties.roleName</span></span> |<span data-ttu-id="f9d82-311">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-311">Yes</span></span> |<span data-ttu-id="f9d82-312">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-312">String</span></span> |<span data-ttu-id="f9d82-313">Nom complet du rôle personnalisé mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f9d82-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="f9d82-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="f9d82-314">properties.description</span></span> |<span data-ttu-id="f9d82-315">Non</span><span class="sxs-lookup"><span data-stu-id="f9d82-315">No</span></span> |<span data-ttu-id="f9d82-316">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-316">String</span></span> |<span data-ttu-id="f9d82-317">Description du rôle personnalisé mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f9d82-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="f9d82-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="f9d82-318">properties.type</span></span> |<span data-ttu-id="f9d82-319">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-319">Yes</span></span> |<span data-ttu-id="f9d82-320">Chaîne</span><span class="sxs-lookup"><span data-stu-id="f9d82-320">String</span></span> |<span data-ttu-id="f9d82-321">Affectez la valeur « CustomRole ».</span><span class="sxs-lookup"><span data-stu-id="f9d82-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="f9d82-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="f9d82-322">properties.permissions.actions</span></span> |<span data-ttu-id="f9d82-323">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-323">Yes</span></span> |<span data-ttu-id="f9d82-324">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-324">String[]</span></span> |<span data-ttu-id="f9d82-325">Tableau de chaînes d’action spécifiant les opérations auxquelles le rôle personnalisé mis à jour octroie l’accès.</span><span class="sxs-lookup"><span data-stu-id="f9d82-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="f9d82-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="f9d82-326">properties.permissions.notActions</span></span> |<span data-ttu-id="f9d82-327">Non</span><span class="sxs-lookup"><span data-stu-id="f9d82-327">No</span></span> |<span data-ttu-id="f9d82-328">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-328">String[]</span></span> |<span data-ttu-id="f9d82-329">Tableau de chaînes d’action spécifiant les opérations à exclure des opérations que le rôle personnalisé octroie.</span><span class="sxs-lookup"><span data-stu-id="f9d82-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="f9d82-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="f9d82-330">properties.assignableScopes</span></span> |<span data-ttu-id="f9d82-331">Oui</span><span class="sxs-lookup"><span data-stu-id="f9d82-331">Yes</span></span> |<span data-ttu-id="f9d82-332">String[]</span><span class="sxs-lookup"><span data-stu-id="f9d82-332">String[]</span></span> |<span data-ttu-id="f9d82-333">Tableau des portées dans lesquelles le rôle personnalisé mis à jour peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="f9d82-334">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-334">Response</span></span>
<span data-ttu-id="f9d82-335">Code d’état : 201</span><span class="sxs-lookup"><span data-stu-id="f9d82-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="f9d82-336">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="f9d82-336">Delete a Custom Role</span></span>
<span data-ttu-id="f9d82-337">Supprimez un rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-337">Delete a custom role.</span></span>

<span data-ttu-id="f9d82-338">Pour supprimer un rôle personnalisé, vous devez avoir accès à l’opération `Microsoft.Authorization/roleDefinitions/delete` sur l’ensemble des `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="f9d82-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="f9d82-339">Parmi les rôles intégrés, seuls ceux du *propriétaire* et de *l’administrateur des accès utilisateur* se voient accorder l’accès à cette opération.</span><span class="sxs-lookup"><span data-stu-id="f9d82-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="f9d82-340">Pour plus d’informations sur les attributions de rôle et la gestion des accès aux ressources Azure, consultez [Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9d82-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="f9d82-341">Demande</span><span class="sxs-lookup"><span data-stu-id="f9d82-341">Request</span></span>
<span data-ttu-id="f9d82-342">Utilisez la méthode **DELETE** avec l’URI suivant :</span><span class="sxs-lookup"><span data-stu-id="f9d82-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="f9d82-343">Dans l’URI, procédez aux changements suivants pour personnaliser votre demande :</span><span class="sxs-lookup"><span data-stu-id="f9d82-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="f9d82-344">Remplacez *{scope}* par la portée dont vous souhaitez supprimer la définition de rôle.</span><span class="sxs-lookup"><span data-stu-id="f9d82-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="f9d82-345">Les exemples suivants montrent comment spécifier la portée sur différents niveaux :</span><span class="sxs-lookup"><span data-stu-id="f9d82-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="f9d82-346">Abonnement : /subscriptions/{subscription-id}</span><span class="sxs-lookup"><span data-stu-id="f9d82-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="f9d82-347">Groupe de ressources : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="f9d82-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="f9d82-348">Ressource : /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="f9d82-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="f9d82-349">Remplacez *{role-definition-id}* par l’ID de définition de rôle GUID du rôle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f9d82-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="f9d82-350">Remplacez *{api-version}* par 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="f9d82-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="f9d82-351">Response</span><span class="sxs-lookup"><span data-stu-id="f9d82-351">Response</span></span>
<span data-ttu-id="f9d82-352">Code d’état : 200</span><span class="sxs-lookup"><span data-stu-id="f9d82-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f9d82-353">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9d82-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
