---
title: "application gérée d’aaaConsume Azure | Documents Microsoft"
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
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="0be43-103">Utiliser une application managée interne</span><span class="sxs-lookup"><span data-stu-id="0be43-103">Consume an internal managed application</span></span>

<span data-ttu-id="0be43-104">Vous pouvez utiliser des [applications managées](managed-application-overview.md) Azure pour les besoins des membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="0be43-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="0be43-105">Par exemple, vous pouvez sélectionner des applications managées dans votre service informatique qui garantissent la conformité par rapport aux normes de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="0be43-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="0be43-106">Ces applications gérées sont disponibles via hello catalogue de services, pas hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0be43-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="0be43-107">Avant de procéder à cet article, vous devez disposer d’une application managée disponible dans le catalogue de services hello pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0be43-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="0be43-108">Si personne au sein de votre organisation n’a encore créé une application managée, consultez [Publier une application managée pour une utilisation interne](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0be43-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="0be43-109">Actuellement, vous pouvez utiliser soit une CLI d’Azure hello tooconsume portail Azure une application managée.</span><span class="sxs-lookup"><span data-stu-id="0be43-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="0be43-110">Créer l’application hello géré à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="0be43-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="0be43-111">toodeploy une application managée via le portail de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0be43-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="0be43-112">Accédez toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0be43-112">Go toohello Azure portal.</span></span> <span data-ttu-id="0be43-113">Recherchez **Application managée du catalogue de services**.</span><span class="sxs-lookup"><span data-stu-id="0be43-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Application gérée du catalogue de services](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="0be43-115">Sélectionnez hello gérés à application que vous souhaitez toocreate à partir de la liste de hello des solutions disponibles.</span><span class="sxs-lookup"><span data-stu-id="0be43-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="0be43-116">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0be43-116">Select **Create**.</span></span>

   ![Sélection d’application gérée](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="0be43-118">Fournir des valeurs pour les paramètres de hello qui sont des ressources de hello tooprovision requis.</span><span class="sxs-lookup"><span data-stu-id="0be43-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="0be43-119">Sélectionnez **Ouest-Centre des États-Unis** comme emplacement.</span><span class="sxs-lookup"><span data-stu-id="0be43-119">Select **West Central US** for location.</span></span> <span data-ttu-id="0be43-120">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0be43-120">Select **OK**.</span></span>

   ![Paramètres de l’application gérée](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="0be43-122">modèle de Hello valide les valeurs hello que vous avez fourni.</span><span class="sxs-lookup"><span data-stu-id="0be43-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="0be43-123">Si la validation réussit, sélectionnez **OK** déploiement de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="0be43-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Validation de l’application managée](./media/managed-application-consumption/validation.png)

<span data-ttu-id="0be43-125">Une fois hello s’achève, les ressources appropriées de hello définis dans le modèle de hello sont configurés dans le groupe de ressources managé hello que vous avez fourni.</span><span class="sxs-lookup"><span data-stu-id="0be43-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="0be43-126">Créer des application hello géré à l’aide de CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="0be43-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="0be43-127">Il existe deux façons toocreate une application managée à l’aide d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="0be43-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="0be43-128">Utilisez la commande hello pour créer des applications managées.</span><span class="sxs-lookup"><span data-stu-id="0be43-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="0be43-129">Utilisez la commande de déploiement de modèle Normal hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="0be43-130">Utilisez la commande de déploiement de modèle de hello</span><span class="sxs-lookup"><span data-stu-id="0be43-130">Use hello template deployment command</span></span>

<span data-ttu-id="0be43-131">Déployer le fichier applianceMainTemplate.json hello hello fournisseur créé.</span><span class="sxs-lookup"><span data-stu-id="0be43-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="0be43-132">Puis, créez deux groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="0be43-132">Then create two resource groups.</span></span> <span data-ttu-id="0be43-133">Hello premier groupe de ressources est où hello ressources d’application managée est créé : Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="0be43-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="0be43-134">deuxième groupe de ressources Hello contient toutes les ressources hello définis dans mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="0be43-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="0be43-135">Ce groupe de ressources est géré par hello ISV.</span><span class="sxs-lookup"><span data-stu-id="0be43-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="0be43-136">Utilisez `westcentralus` comme emplacement hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0be43-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="0be43-137">applianceMainTemplate.json toodeploy dans mainResourceGroup, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0be43-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="0be43-138">Après avoir hello précédent s’exécute le modèle, il vous invite pour les valeurs de paramètres hello qui sont définis dans le modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="0be43-139">En outre les paramètres de toohello qui sont nécessaires tooprovision des ressources dans un modèle, vous avez besoin de deux valeurs de paramètre de clé :</span><span class="sxs-lookup"><span data-stu-id="0be43-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="0be43-140">**managedResourceGroupId**: hello ID des ressources de hello contenant hello ressource groupe défini dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="0be43-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="0be43-141">ID de Hello se présente sous forme de hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="0be43-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="0be43-142">Bonjour précédent exemple, il ID de l’élément hello de `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="0be43-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="0be43-143">**applianceDefinitionId**: ID de hello Hello gérés ressource de définition d’application.</span><span class="sxs-lookup"><span data-stu-id="0be43-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="0be43-144">Cette valeur est fournie par hello ISV.</span><span class="sxs-lookup"><span data-stu-id="0be43-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="0be43-145">serveur de publication Hello doit accorder l’accès toohello ressource groupe qui contient la définition de l’application hello géré.</span><span class="sxs-lookup"><span data-stu-id="0be43-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="0be43-146">ressource de définition Hello est créée dans l’abonnement du serveur de publication hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="0be43-147">Par conséquent, un utilisateur, un groupe d’utilisateurs ou une application dans le locataire hello a besoin d’accès en lecture toothis ressource.</span><span class="sxs-lookup"><span data-stu-id="0be43-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="0be43-148">Une fois le déploiement de hello se termine correctement, vous voyez hello géré application est créée dans mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="0be43-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="0be43-149">ressources de storageAccount Hello est créé dans managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="0be43-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="0be43-150">Hello d’utilisation Créer commande</span><span class="sxs-lookup"><span data-stu-id="0be43-150">Use hello create command</span></span>

<span data-ttu-id="0be43-151">Vous pouvez utiliser hello `az managedapp create` commande toocreate une application managée à partir de hello gérés définition d’application.</span><span class="sxs-lookup"><span data-stu-id="0be43-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="0be43-152">**Id de définition d’application**: ID de ressource hello Hello gérés créée dans hello précédant l’étape de définition d’application.</span><span class="sxs-lookup"><span data-stu-id="0be43-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="0be43-153">tooobtain cet ID, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0be43-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="0be43-154">Cette commande renvoie la définition de l’application hello géré.</span><span class="sxs-lookup"><span data-stu-id="0be43-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="0be43-155">Vous devez valeur hello de propriété d’ID hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="0be43-156">**id du groupe de routage managé**: nom hello des ressources de hello contenant hello ressource groupe défini dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="0be43-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="0be43-157">Ce groupe de ressources est un groupe de ressources managé hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="0be43-158">Il est géré par le serveur de publication hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-158">It's managed by hello publisher.</span></span> <span data-ttu-id="0be43-159">S’il n’existe pas, il est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="0be43-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="0be43-160">**groupe de ressources**: groupe de ressources hello où hello géré de ressource d’application est créé.</span><span class="sxs-lookup"><span data-stu-id="0be43-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="0be43-161">Hello Microsoft.Solutions/appliance ressource se situe à ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0be43-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="0be43-162">**paramètres**: hello des paramètres qui sont nécessaires pour les ressources hello définis dans applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="0be43-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0be43-163">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="0be43-163">Known issues</span></span>

<span data-ttu-id="0be43-164">Cette préversion inclut hello suivants :</span><span class="sxs-lookup"><span data-stu-id="0be43-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="0be43-165">Une erreur de serveur interne 500 apparaît lors de la création de hello de l’application hello géré.</span><span class="sxs-lookup"><span data-stu-id="0be43-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="0be43-166">Si vous rencontrez ce problème, il est probable toobe intermittent.</span><span class="sxs-lookup"><span data-stu-id="0be43-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="0be43-167">Recommencez l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-167">Retry hello operation.</span></span>
* <span data-ttu-id="0be43-168">Un groupe de ressources est nécessaire pour le groupe de ressources managé hello.</span><span class="sxs-lookup"><span data-stu-id="0be43-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="0be43-169">Si vous utilisez un groupe de ressources existant, le déploiement de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="0be43-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="0be43-170">Hello groupe de ressources qui contient la ressource de Microsoft.Solutions/appliances hello doit être créée dans hello **westcentralus** emplacement.</span><span class="sxs-lookup"><span data-stu-id="0be43-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0be43-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0be43-171">Next steps</span></span>

* <span data-ttu-id="0be43-172">Pour une introduction toomanaged les applications, voir [vue d’ensemble de Managed application](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0be43-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0be43-173">Pour plus d’informations sur la publication d’une application gérée de catalogue de services, consultez l’article [Créer et publier une application gérée de catalogue de services](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0be43-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="0be43-174">Pour plus d’informations sur la publication des applications managées toohello Azure Marketplace, consultez [Azure géré applications Bonjour Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="0be43-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="0be43-175">Pour plus d’informations sur la consommation d’une application managée à partir de hello Marketplace, consultez [Azure de consommer gérés applications Bonjour Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="0be43-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
