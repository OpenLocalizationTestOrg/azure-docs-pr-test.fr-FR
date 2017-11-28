---
title: "définie des modèles aaaLearn sur l’échelle de machine virtuelle | Documents Microsoft"
description: "En savoir toocreate une échelle viable minimale définie le modèle pour les machines virtuelles identiques"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="ebb82-103">En savoir plus sur les modèles de groupes de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="ebb82-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="ebb82-104">[Les modèles de gestionnaire de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) est un excellent moyen toodeploy groupes de ressources liées.</span><span class="sxs-lookup"><span data-stu-id="ebb82-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="ebb82-105">Cette série de didacticiels montre comment le modèle de jeu de toocreate une échelle viable minimale et toomodify toosuit de ce modèle différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="ebb82-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="ebb82-106">Tous les exemples proviennent de ce [référentiel GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="ebb82-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="ebb82-107">Ce modèle est prévue toobe simple.</span><span class="sxs-lookup"><span data-stu-id="ebb82-107">This template is intended toobe simple.</span></span> <span data-ttu-id="ebb82-108">Pour obtenir des exemples plus complètes de l’échelle définir des modèles, consultez hello [référentiel GitHub de modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates) et recherchez les dossiers qui contiennent la chaîne de hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="ebb82-109">Si vous êtes déjà familiarisé avec la création de modèles, vous pouvez ignorer toohello toosee de section « Étapes suivantes » comment toomodify ce modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb82-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="ebb82-110">Modèle de hello de vérification</span><span class="sxs-lookup"><span data-stu-id="ebb82-110">Review hello template</span></span>

<span data-ttu-id="ebb82-111">Utiliser GitHub tooreview modèle, de jeu de notre échelle viable minimale [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ebb82-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="ebb82-112">Dans ce didacticiel, nous allons examiner hello diff (`git diff master minimum-viable-scale-set`) toocreate hello viable minimale définie modèle élément par élément.</span><span class="sxs-lookup"><span data-stu-id="ebb82-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="ebb82-113">Définir $schema et contentVersion</span><span class="sxs-lookup"><span data-stu-id="ebb82-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="ebb82-114">Tout d’abord, nous définissons `$schema` et `contentVersion` dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="ebb82-115">Hello `$schema` élément définit la version de hello du langage de modèle hello et est utilisé pour la mise en surbrillance de syntaxe Visual Studio et des fonctionnalités similaires de validation.</span><span class="sxs-lookup"><span data-stu-id="ebb82-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="ebb82-116">Hello `contentVersion` élément n’est pas utilisé par Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb82-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="ebb82-117">Au lieu de cela, il vous aide à effectuer le suivi de version du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="ebb82-118">Définir les paramètres</span><span class="sxs-lookup"><span data-stu-id="ebb82-118">Define parameters</span></span>
<span data-ttu-id="ebb82-119">Ensuite, nous définissons deux paramètres, `adminUsername` et `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="ebb82-120">Les paramètres sont des valeurs que vous spécifiez au moment de hello du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ebb82-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="ebb82-121">Hello `adminUsername` paramètre est simplement un `string` type, mais étant donné que `adminPassword` est un secret, nous avons un type `securestring`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="ebb82-122">Une version ultérieure, ces paramètres sont passés dans la configuration du jeu de mise à l’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="ebb82-123">Définir des variables</span><span class="sxs-lookup"><span data-stu-id="ebb82-123">Define variables</span></span>
<span data-ttu-id="ebb82-124">Modèles du Gestionnaire de ressources vous permettent également de définir toobe variables utilisé ultérieurement dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="ebb82-125">Notre exemple n’utilise pas des variables, donc nous avons laissé vide objet JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="ebb82-126">Définir les ressources</span><span class="sxs-lookup"><span data-stu-id="ebb82-126">Define resources</span></span>
<span data-ttu-id="ebb82-127">L’élément suivant est section relative aux ressources de modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="ebb82-128">Ici, vous définissez ce que vous souhaitez réellement toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ebb82-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="ebb82-129">Contrairement à `parameters` et `variables` (qui sont des objets JSON), `resources` est une liste JSON d’objets JSON.</span><span class="sxs-lookup"><span data-stu-id="ebb82-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="ebb82-130">Toutes les ressources nécessitent les propriétés `type`, `name`, `apiVersion` et `location`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="ebb82-131">La première ressource de cet exemple est de type `Microsft.Network/virtualNetwork`, avec le nom `myVnet` et apiVersion `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="ebb82-132">(toofind hello API version la plus récente pour un type de ressource, consultez hello [documentation de l’API REST Azure](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="ebb82-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="ebb82-133">Spécifier l’emplacement</span><span class="sxs-lookup"><span data-stu-id="ebb82-133">Specify location</span></span>
<span data-ttu-id="ebb82-134">emplacement de hello toospecify pour le réseau virtuel de hello, nous utilisons un [fonction de modèle de gestionnaire de ressources](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="ebb82-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="ebb82-135">Cette fonction doit être placée entre guillemets et crochets, comme suit : `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="ebb82-136">Dans ce cas, nous utilisons hello `resourceGroup` (fonction).</span><span class="sxs-lookup"><span data-stu-id="ebb82-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="ebb82-137">Il accepte aucun argument et retourne un objet JSON contenant des métadonnées sur le groupe de ressources hello qu'est déployé pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="ebb82-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="ebb82-138">groupe de ressources Hello est définie par l’utilisateur de hello au moment de hello du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ebb82-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="ebb82-139">Nous puis index dans cet objet JSON avec `.location` emplacement de hello tooget à partir de l’objet JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="ebb82-140">Spécifier les propriétés du réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="ebb82-140">Specify virtual network properties</span></span>
<span data-ttu-id="ebb82-141">Chaque ressource de gestionnaire de ressources a son propre `properties` section pour la ressource toohello spécifique de configurations.</span><span class="sxs-lookup"><span data-stu-id="ebb82-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="ebb82-142">Dans ce cas, nous spécifions ce réseau virtuel hello doit avoir un sous-réseau à l’aide de la plage d’adresses IP privées hello `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="ebb82-143">Un jeu de mise à l’échelle est toujours contenu dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ebb82-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="ebb82-144">Il ne peut pas s’étendre sur plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="ebb82-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="ebb82-145">Ajouter la liste dependsOn</span><span class="sxs-lookup"><span data-stu-id="ebb82-145">Add dependsOn list</span></span>
<span data-ttu-id="ebb82-146">En outre toohello requis `type`, `name`, `apiVersion`, et `location` propriétés, chaque ressource peuvent avoir une option `dependsOn` liste de chaînes.</span><span class="sxs-lookup"><span data-stu-id="ebb82-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="ebb82-147">Cette liste spécifie les autres ressources de ce déploiement qui doivent se terminer avant le déploiement de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="ebb82-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="ebb82-148">Dans ce cas, il n'est qu’un seul élément dans la liste hello, réseau virtuel de hello à partir de l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="ebb82-149">Nous spécifions cette dépendance, car hello ensemble d’échelle besoins hello réseau tooexist avant de créer les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ebb82-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="ebb82-150">De cette manière, un ensemble d’échelle hello peut donner ces adresses IP privées de machines virtuelles à partir de la plage d’adresses IP hello précédemment spécifié dans les propriétés de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="ebb82-151">le format de chaque chaîne dans la liste de dependsOn hello Hello est `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="ebb82-152">Utilisez hello même `type` et `name` précédemment utilisé dans la définition de ressource du réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="ebb82-153">Spécifier les propriétés du groupe identique</span><span class="sxs-lookup"><span data-stu-id="ebb82-153">Specify scale set properties</span></span>
<span data-ttu-id="ebb82-154">Groupes identiques ont de nombreuses propriétés de personnalisation de machines virtuelles de hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="ebb82-155">Pour obtenir une liste complète de ces propriétés, consultez hello [ensemble d’échelle de documentation de l’API REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="ebb82-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="ebb82-156">Pour ce didacticiel, nous ne définirons que quelques propriétés couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="ebb82-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="ebb82-157">Fournir la capacité et la taille de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ebb82-157">Supply VM size and capacity</span></span>
<span data-ttu-id="ebb82-158">ensemble d’échelle de Hello besoins tooknow taille de la machine virtuelle toocreate (« nom de la référence (SKU) ») et combien ce toocreate de machines virtuelles (« capacité de référence (SKU) »).</span><span class="sxs-lookup"><span data-stu-id="ebb82-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="ebb82-159">toosee les tailles de machine virtuelle sont disponibles, consultez hello [documentation des tailles de machine virtuelle](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="ebb82-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="ebb82-160">Choisir le type de mises à jour</span><span class="sxs-lookup"><span data-stu-id="ebb82-160">Choose type of updates</span></span>
<span data-ttu-id="ebb82-161">ensemble d’échelle Hello doit également tooknow comment toohandle met à jour sur l’ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="ebb82-162">Il existe actuellement deux options, `Manual` et `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="ebb82-163">Pour plus d’informations sur les différences de hello entre hello deux, consultez la documentation de la hello sur [comment tooupgrade une ensemble d’échelle](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="ebb82-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="ebb82-164">Choisir le système d’exploitation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ebb82-164">Choose VM operating system</span></span>
<span data-ttu-id="ebb82-165">Hello ensemble d’échelle de besoins tooknow le tooput du système d’exploitation sur des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="ebb82-166">Ici, nous créer des machines virtuelles de hello avec une image de 16.04-LTS Ubuntu tous les correctifs nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ebb82-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="ebb82-167">Spécifier computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="ebb82-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="ebb82-168">ensemble d’échelle Hello déploie plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ebb82-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="ebb82-169">Au lieu de spécifier le nom de chaque machine virtuelle, nous spécifions `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="ebb82-170">Hello ensemble d’échelle ajoute un préfixe de toohello index pour chaque machine virtuelle, pour que les noms de machine virtuelle aient le formulaire de hello `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="ebb82-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="ebb82-171">Bonjour suivant extrait de code, nous utiliser les paramètres de hello d’avant le nom d’utilisateur administrateur tooset hello et le mot de passe pour tous les ordinateurs virtuels dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="ebb82-172">Vous faire avec hello `parameters` fonction de modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb82-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="ebb82-173">Cette fonction accepte une chaîne qui spécifie le tooand toorefer de paramètre génère la valeur hello pour ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="ebb82-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="ebb82-174">Spécifier la configuration du réseau de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ebb82-174">Specify VM network configuration</span></span>
<span data-ttu-id="ebb82-175">Enfin, nous devons la configuration du réseau toospecify hello pour les machines virtuelles hello dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="ebb82-176">Dans ce cas, nous avons besoin uniquement des ID de hello toospecify de sous-réseau hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="ebb82-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="ebb82-177">Cela indique hello ensemble d’échelle tooput les interfaces réseau hello dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ebb82-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="ebb82-178">Vous pouvez obtenir les ID hello du réseau virtuel de hello contenant le sous-réseau de hello à l’aide de hello `resourceId` fonction de modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb82-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="ebb82-179">Cette fonction utilise les type hello et le nom d’une ressource et retourne hello identificateur qualifié complet de la ressource.</span><span class="sxs-lookup"><span data-stu-id="ebb82-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="ebb82-180">Ce code présente sous forme de hello :`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="ebb82-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="ebb82-181">Toutefois, identificateur hello du réseau virtuel de hello n’est pas suffisant.</span><span class="sxs-lookup"><span data-stu-id="ebb82-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="ebb82-182">Vous devez spécifier le sous-réseau spécifique hello hello des machines virtuelles doivent être dans un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="ebb82-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="ebb82-183">toodo, concaténer `/subnets/mySubnet` toohello les ID de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="ebb82-184">résultat de Hello est hello complet des ID de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="ebb82-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="ebb82-185">Effectuer cette concaténation avec hello `concat` fonction qui accepte une série de chaînes et retourne leur concaténation.</span><span class="sxs-lookup"><span data-stu-id="ebb82-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="ebb82-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebb82-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
