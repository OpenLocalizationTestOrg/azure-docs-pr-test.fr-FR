---
title: aaaDeploy plusieurs instances de ressources Azure | Documents Microsoft
description: "Utilisez opération de copie et de tableaux dans un tooiterate de modèle Azure Resource Manager plusieurs fois lors du déploiement de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="87442-103">Déployer plusieurs instances d’une ressource ou d’une propriété dans des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87442-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="87442-104">Cette rubrique vous montre comment tooiterate dans votre toocreate de modèle Azure Resource Manager plusieurs instances d’une ressource, ou plusieurs instances d’une propriété sur une ressource.</span><span class="sxs-lookup"><span data-stu-id="87442-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="87442-105">Si vous avez besoin tooadd logique tooyour modèle qui vous permet de toospecify qu’une ressource est déployée, consultez [déployer de manière conditionnelle ressource](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="87442-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="87442-106">Itération de ressource</span><span class="sxs-lookup"><span data-stu-id="87442-106">Resource iteration</span></span>
<span data-ttu-id="87442-107">Ajout de plusieurs instances d’un type de ressource, toocreate un `copy` type d’élément de ressource toohello.</span><span class="sxs-lookup"><span data-stu-id="87442-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="87442-108">Dans l’élément de copie hello, vous spécifiez nombre hello des itérations et un nom pour cette boucle.</span><span class="sxs-lookup"><span data-stu-id="87442-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="87442-109">valeur du nombre Hello doit être un entier positif et ne peut pas dépasser 800.</span><span class="sxs-lookup"><span data-stu-id="87442-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="87442-110">Le Gestionnaire de ressources crée les ressources hello en parallèle.</span><span class="sxs-lookup"><span data-stu-id="87442-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="87442-111">Par conséquent, la commande hello dans lequel ils sont créés n’est pas garantie.</span><span class="sxs-lookup"><span data-stu-id="87442-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="87442-112">ressources toocreate itérée dans l’ordre, consultez [copie série](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="87442-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="87442-113">Hello ressource toocreate plusieurs fois prend hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="87442-113">hello resource toocreate multiple times takes hello following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="87442-114">Notez que hello nom de chaque ressource inclut hello `copyIndex()` fonction, qui retourne l’itération actuelle de hello dans la boucle de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="87442-115">`copyIndex()` est basé sur zéro.</span><span class="sxs-lookup"><span data-stu-id="87442-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="87442-116">Hello c’est le cas, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87442-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="87442-117">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="87442-117">Creates these names:</span></span>

* <span data-ttu-id="87442-118">storage0</span><span class="sxs-lookup"><span data-stu-id="87442-118">storage0</span></span>
* <span data-ttu-id="87442-119">storage1</span><span class="sxs-lookup"><span data-stu-id="87442-119">storage1</span></span>
* <span data-ttu-id="87442-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="87442-120">storage2.</span></span>

<span data-ttu-id="87442-121">valeur d’index toooffset hello, vous pouvez passer une valeur dans la fonction de copyIndex() hello.</span><span class="sxs-lookup"><span data-stu-id="87442-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="87442-122">Hello nombre d’itérations tooperform est toujours spécifié dans l’élément de copie hello, mais valeur hello copyIndex est décalé par hello spécifié valeur.</span><span class="sxs-lookup"><span data-stu-id="87442-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="87442-123">Hello c’est le cas, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87442-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="87442-124">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="87442-124">Creates these names:</span></span>

* <span data-ttu-id="87442-125">storage1</span><span class="sxs-lookup"><span data-stu-id="87442-125">storage1</span></span>
* <span data-ttu-id="87442-126">storage2</span><span class="sxs-lookup"><span data-stu-id="87442-126">storage2</span></span>
* <span data-ttu-id="87442-127">storage3</span><span class="sxs-lookup"><span data-stu-id="87442-127">storage3</span></span>

<span data-ttu-id="87442-128">opération de copie Hello est utile lorsque vous travaillez avec des tableaux, car vous pouvez itérer dans chaque élément de tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="87442-129">Hello d’utilisation `length` fonction hello tableau toospecify hello termes de nombre d’itérations, et `copyIndex` tooretrieve hello actuel index hello tableau.</span><span class="sxs-lookup"><span data-stu-id="87442-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="87442-130">Hello c’est le cas, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87442-130">So, hello following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="87442-131">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="87442-131">Creates these names:</span></span>

* <span data-ttu-id="87442-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="87442-132">storagecontoso</span></span>
* <span data-ttu-id="87442-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="87442-133">storagefabrikam</span></span>
* <span data-ttu-id="87442-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="87442-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="87442-135">Copie en série</span><span class="sxs-lookup"><span data-stu-id="87442-135">Serial copy</span></span>

<span data-ttu-id="87442-136">Lorsque vous utilisez hello copie élément toocreate plusieurs instances d’un type de ressource, le Gestionnaire de ressources, par défaut, déploie ces instances en parallèle.</span><span class="sxs-lookup"><span data-stu-id="87442-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="87442-137">Toutefois, vous souhaiterez peut-être toospecify que hello ressources sont déployées dans la séquence.</span><span class="sxs-lookup"><span data-stu-id="87442-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="87442-138">Par exemple, lors de la mise à jour d’un environnement de production, vous pouvez choisir toostagger hello et seul un certain nombre des mises à jour sont mis à jour à tout moment.</span><span class="sxs-lookup"><span data-stu-id="87442-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="87442-139">Le Gestionnaire de ressources fournit des propriétés qui permettent de vous tooserially sur l’élément de copie hello déploiement plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="87442-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="87442-140">Dans l’élément de copie hello, définissez `mode` trop**série** et `batchSize` nombre toohello de toodeploy d’instances à la fois.</span><span class="sxs-lookup"><span data-stu-id="87442-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="87442-141">En mode série, le Gestionnaire de ressources crée une dépendance sur les instances plus haut dans la boucle de hello, afin qu’il ne démarre pas un lot jusqu'à ce que le lot précédent de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="87442-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="87442-142">Hello propriété mode accepte également **parallèles**, qui est la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="87442-143">tootest série copie sans créer de ressources réelles, hello utilisation suivant le modèle qui déploie des modèles imbriqués vides :</span><span class="sxs-lookup"><span data-stu-id="87442-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="87442-144">Dans l’historique de déploiement hello, notez que hello déploiements imbriquées sont traitées dans la séquence.</span><span class="sxs-lookup"><span data-stu-id="87442-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![déploiement en série](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="87442-146">Pour un scénario plus réaliste, hello exemple suivant déploie les deux instances à la fois d’un VM Linux à partir d’un modèle imbriqué :</span><span class="sxs-lookup"><span data-stu-id="87442-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="87442-147">Itération de propriété</span><span class="sxs-lookup"><span data-stu-id="87442-147">Property iteration</span></span>

<span data-ttu-id="87442-148">Ajout de plusieurs valeurs pour une propriété sur une ressource, toocreate un `copy` tableau dans l’élément de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="87442-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="87442-149">Ce tableau contient des objets, et chaque objet a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="87442-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="87442-150">nom : nom de hello de hello propriété toocreate plusieurs valeurs pour</span><span class="sxs-lookup"><span data-stu-id="87442-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="87442-151">Count : nombre de hello de valeurs toocreate</span><span class="sxs-lookup"><span data-stu-id="87442-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="87442-152">entrée - un objet qui contient la propriété hello valeurs tooassign toohello</span><span class="sxs-lookup"><span data-stu-id="87442-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="87442-153">Hello suivant montre l’exemple de comment tooapply `copy` propriété dataDisks de toohello sur un ordinateur virtuel :</span><span class="sxs-lookup"><span data-stu-id="87442-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="87442-154">Notez que lorsque vous utilisez `copyIndex` à l’intérieur d’une itération de la propriété, vous devez fournir le nom hello d’itération de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="87442-155">Vous n’avez pas de nom de hello tooprovide lorsqu’il est utilisé avec l’itération de la ressource.</span><span class="sxs-lookup"><span data-stu-id="87442-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="87442-156">Le Gestionnaire de ressources se développe hello `copy` tableau durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="87442-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="87442-157">nom de Hello du tableau de hello devient nom hello de propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="87442-158">les valeurs d’entrée Hello deviennent des propriétés de l’objet hello.</span><span class="sxs-lookup"><span data-stu-id="87442-158">hello input values become hello object properties.</span></span> <span data-ttu-id="87442-159">modèle de Hello déployé devient :</span><span class="sxs-lookup"><span data-stu-id="87442-159">hello deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="87442-160">Vous pouvez utiliser des itérations de ressource et de propriété ensemble.</span><span class="sxs-lookup"><span data-stu-id="87442-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="87442-161">Référence hello propriété l’itération par nom.</span><span class="sxs-lookup"><span data-stu-id="87442-161">Reference hello property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="87442-162">Vous ne pouvez inclure qu’un seul élément de la copie dans les propriétés de hello pour chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="87442-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="87442-163">toospecify une boucle d’itération pour plus d’une propriété, définir plusieurs objets dans le tableau de copie hello.</span><span class="sxs-lookup"><span data-stu-id="87442-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="87442-164">Chaque objet est itéré séparément.</span><span class="sxs-lookup"><span data-stu-id="87442-164">Each object is iterated separately.</span></span> <span data-ttu-id="87442-165">Par exemple, toocreate plusieurs instances de ces deux hello `frontendIPConfigurations` propriété et hello `loadBalancingRules` propriété sur un équilibrage de charge, définir les deux objets dans un élément de copie unique :</span><span class="sxs-lookup"><span data-stu-id="87442-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="87442-166">En fonction des ressources dans une boucle</span><span class="sxs-lookup"><span data-stu-id="87442-166">Depend on resources in a loop</span></span>
<span data-ttu-id="87442-167">Vous spécifiez qu’une ressource est déployée après une autre ressource à l’aide de hello `dependsOn` élément.</span><span class="sxs-lookup"><span data-stu-id="87442-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="87442-168">toodeploy une ressource dont dépend la collection hello des ressources dans une boucle, fournir un nom hello de boucle de copie hello dans l’élément dependsOn de hello.</span><span class="sxs-lookup"><span data-stu-id="87442-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="87442-169">Bonjour à l’exemple suivant montre comment toodeploy trois comptes de stockage avant de déployer hello Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="87442-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="87442-170">définition de Machine virtuelle complète Hello n’est pas affichée.</span><span class="sxs-lookup"><span data-stu-id="87442-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="87442-171">Notez que cet élément de la copie hello a le nom défini trop`storagecopy` et élément de dependsOn hello pour les Machines virtuelles de hello est également défini trop`storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="87442-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="87442-172">Création de plusieurs instances d’une ressource enfant</span><span class="sxs-lookup"><span data-stu-id="87442-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="87442-173">Vous ne pouvez pas utiliser une boucle de copie pour une ressource enfant.</span><span class="sxs-lookup"><span data-stu-id="87442-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="87442-174">toocreate plusieurs instances d’une ressource que vous définissez généralement comme imbriquées dans une autre ressource, vous devez créer à la place cette ressource en tant qu’une ressource de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="87442-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="87442-175">Vous définissez la relation de hello avec la ressource parent de hello via les propriétés de type et le nom hello.</span><span class="sxs-lookup"><span data-stu-id="87442-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="87442-176">Par exemple, supposons que vous définissez généralement un jeu de données comme une ressource enfant dans une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="87442-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="87442-177">toocreate plusieurs instances de jeux de données, déplacez-la en dehors de la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="87442-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="87442-178">Hello dataset doit être au même niveau en tant que fabrique de données hello de hello, mais il est toujours une ressource enfant hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="87442-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="87442-179">Vous conservez la relation hello entre le jeu de données et de la fabrique de données via les propriétés de type et le nom hello.</span><span class="sxs-lookup"><span data-stu-id="87442-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="87442-180">Étant donné que le type n’est plus peut être déduit qu’à partir de sa position dans le modèle de hello, vous devez fournir le type hello complet au format de hello : `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="87442-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="87442-181">tooestablish une relation parent/enfant avec une instance de la fabrique de données hello, fournissez un nom pour le jeu de données hello qui inclut le nom de la ressource parent hello.</span><span class="sxs-lookup"><span data-stu-id="87442-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="87442-182">Utilisez le format hello : `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="87442-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="87442-183">Hello exemple suivant illustre hello implémentation :</span><span class="sxs-lookup"><span data-stu-id="87442-183">hello following example shows hello implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="87442-184">Déployer une ressource de manière conditionnelle</span><span class="sxs-lookup"><span data-stu-id="87442-184">Conditionally deploy resource</span></span>

<span data-ttu-id="87442-185">toospecify si une ressource est déployée, utilisez hello `condition` élément.</span><span class="sxs-lookup"><span data-stu-id="87442-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="87442-186">valeur Hello pour cet élément résout tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="87442-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="87442-187">Lorsque la valeur de hello est true, les ressources hello sont déployé.</span><span class="sxs-lookup"><span data-stu-id="87442-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="87442-188">Lorsque la valeur de hello est false, les ressources hello ne sont pas déployée.</span><span class="sxs-lookup"><span data-stu-id="87442-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="87442-189">Par exemple, toospecify si un compte de stockage est déployé ou un compte de stockage existant est utilisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="87442-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="87442-190">Pour obtenir un exemple d’utilisation d’une ressource nouvelle ou existante, voir [Modèle de condition New ou Existing](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="87442-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="87442-191">Pour obtenir un exemple de l’utilisation d’un mot de passe ou d’un ordinateur virtuel de toodeploy clé SSH, consultez [modèle de condition de nom d’utilisateur ou de SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="87442-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87442-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87442-192">Next steps</span></span>
* <span data-ttu-id="87442-193">Si vous souhaitez toolearn sur les sections hello d’un modèle, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="87442-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="87442-194">toolearn comment toodeploy votre modèle, consultez [déployer une application avec le modèle de gestionnaire de ressources Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="87442-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

