---
title: "Utiliser une application gérée Azure | Microsoft Docs"
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="5b6e2-103">Utiliser une application managée interne</span><span class="sxs-lookup"><span data-stu-id="5b6e2-103">Consume an internal managed application</span></span>

<span data-ttu-id="5b6e2-104">Vous pouvez utiliser des [applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="5b6e2-105">Par exemple, vous pouvez sélectionner des applications managées dans votre service informatique qui garantissent la conformité par rapport aux normes de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="5b6e2-106">Ces applications managées sont disponibles via le catalogue de services, et non la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="5b6e2-107">Avant d’aller plus loin dans la lecture de cet article, vérifiez qu’une application managée est disponible dans le catalogue de services de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="5b6e2-108">Si personne au sein de votre organisation n’a encore créé une application managée, consultez [Publier une application managée pour une utilisation interne](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e2-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="5b6e2-109">Actuellement, vous pouvez utiliser Azure CLI ou le portail Azure pour utiliser une application gérée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="5b6e2-110">Créer l’application gérée à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="5b6e2-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="5b6e2-111">Pour déployer une application managée via le portail, suivez ces étapes :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="5b6e2-112">Accédez au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-112">Go to the Azure portal.</span></span> <span data-ttu-id="5b6e2-113">Recherchez **Application managée du catalogue de services**.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Application gérée du catalogue de services](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="5b6e2-115">Sélectionnez l’application managée que vous voulez créer dans la liste des solutions disponibles.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="5b6e2-116">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-116">Select **Create**.</span></span>

   ![Sélection d’application gérée](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="5b6e2-118">Fournissez les valeurs des paramètres nécessaires à l’approvisionnement des ressources.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="5b6e2-119">Sélectionnez **Ouest-Centre des États-Unis** comme emplacement.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-119">Select **West Central US** for location.</span></span> <span data-ttu-id="5b6e2-120">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-120">Select **OK**.</span></span>

   ![Paramètres de l’application gérée](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="5b6e2-122">Le modèle valide les valeurs que vous avez fournies.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-122">The template validates the values you provided.</span></span> <span data-ttu-id="5b6e2-123">Si la validation aboutit, sélectionnez **OK** pour commencer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Validation de l’application managée](./media/managed-application-consumption/validation.png)

<span data-ttu-id="5b6e2-125">Une fois le déploiement terminé, les ressources appropriées définies dans le modèle sont approvisionnées dans le groupe de ressources gérées fourni.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="5b6e2-126">Créer l’application gérée à l’aide de l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="5b6e2-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="5b6e2-127">Il existe deux manières de créer une application gérée à l’aide d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="5b6e2-128">Utilisez la commande permettant de créer des applications managées.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="5b6e2-129">Utilisez la commande de déploiement de modèle standard.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="5b6e2-130">Utiliser la commande de déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="5b6e2-130">Use the template deployment command</span></span>

<span data-ttu-id="5b6e2-131">Déployez le fichier applianceMainTemplate.json créé par le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="5b6e2-132">Puis, créez deux groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-132">Then create two resource groups.</span></span> <span data-ttu-id="5b6e2-133">Le premier groupe de ressources se trouve là où la ressource d’application managée est créée : Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="5b6e2-134">Le deuxième groupe de ressources contient toutes les ressources définies dans le fichier mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="5b6e2-135">Ce groupe de ressources est géré par l’éditeur de logiciels indépendants.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="5b6e2-136">Utilisez `westcentralus` comme emplacement du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="5b6e2-137">Utilisez la commande suivante pour déployer le fichier applianceMainTemplate.json dans mainResourceGroup :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="5b6e2-138">Après l’exécution du modèle précédent, il vous demande les valeurs des paramètres qui sont définis dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="5b6e2-139">Outre les paramètres requis pour l’approvisionnement des ressources dans un modèle, vous avez besoin de deux valeurs de paramètre essentielles :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="5b6e2-140">**managedResourceGroupId** : ID du groupe de ressources contenant les ressources définies dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="5b6e2-141">L’ID est au format `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="5b6e2-142">Dans l’exemple précédent, il s’agit de l’ID de `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="5b6e2-143">**applianceDefinitionId** : ID de la ressource de la définition de l’application gérée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="5b6e2-144">Cette valeur est fournie par l’éditeur de logiciels indépendants.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="5b6e2-145">L’éditeur doit accorder l’accès au groupe de ressources qui contient la définition d’application managée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="5b6e2-146">La ressource de définition est créée dans l’abonnement de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="5b6e2-147">Par conséquent, un utilisateur, un groupe d’utilisateurs ou une application du locataire client a besoin d’accéder en lecture à cette ressource.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="5b6e2-148">À l’issue du déploiement, vous pouvez constater que l’application managée est créée dans mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="5b6e2-149">La ressource storageAccount est créée dans managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="5b6e2-150">Utiliser la commande create</span><span class="sxs-lookup"><span data-stu-id="5b6e2-150">Use the create command</span></span>

<span data-ttu-id="5b6e2-151">Vous pouvez utiliser la commande `az managedapp create` pour créer une application gérée à partir de la définition d’application gérée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="5b6e2-152">**appliance-definition-Id** : ID de ressource de la définition de l’application managée créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="5b6e2-153">Pour obtenir cet ID, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="5b6e2-154">Cette commande retourne la définition de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-154">This command returns the managed application definition.</span></span> <span data-ttu-id="5b6e2-155">Vous avez besoin de la valeur de la propriété ID.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="5b6e2-156">**managed-rg-id** : nom du groupe de ressources contenant les ressources définies dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="5b6e2-157">Ce groupe de ressources est le groupe de ressources gérées.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="5b6e2-158">Il est géré par l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-158">It's managed by the publisher.</span></span> <span data-ttu-id="5b6e2-159">S’il n’existe pas, il est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="5b6e2-160">**resource-group** : groupe de ressources dans lequel la ressource d’application managée est créée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="5b6e2-161">La ressource Microsoft.Solutions/appliance se trouve dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="5b6e2-162">**parameters** : paramètres qui sont nécessaires aux ressources définies dans le fichier applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5b6e2-163">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="5b6e2-163">Known issues</span></span>

<span data-ttu-id="5b6e2-164">Cette version préliminaire comprend les problèmes suivants :</span><span class="sxs-lookup"><span data-stu-id="5b6e2-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="5b6e2-165">Une erreur de serveur interne 500 apparaît pendant la création de l’application managée.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="5b6e2-166">Si vous rencontrez ce problème, il est sans doute intermittent.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="5b6e2-167">Retentez l’opération.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-167">Retry the operation.</span></span>
* <span data-ttu-id="5b6e2-168">Un nouveau groupe de ressources est nécessaire pour le groupe de ressources gérées.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="5b6e2-169">L’utilisation d’un groupe de ressources existant provoque l’échec du déploiement.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="5b6e2-170">Le groupe de ressources qui contient la ressource Microsoft.Solutions/appliances doit être créé à l’emplacement **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="5b6e2-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b6e2-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b6e2-171">Next steps</span></span>

* <span data-ttu-id="5b6e2-172">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e2-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5b6e2-173">Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e2-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="5b6e2-174">Pour plus d’informations sur la publication d’applications gérées sur la Place de marché, consultez l’article [Applications gérées sur la Place de marché](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e2-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="5b6e2-175">Pour plus d’informations sur l’utilisation d’applications gérées de la Place de marché, consultez l’article [Utilisation des applications gérées de la Place de marché Azure](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="5b6e2-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
