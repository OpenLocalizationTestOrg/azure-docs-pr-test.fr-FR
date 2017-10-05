---
title: "Déploiement de plusieurs instances de ressources Azure | Microsoft Docs"
description: "Utilisez l’opération de copie et les tableaux dans un modèle Azure Resource Manager pour effectuer une itération à plusieurs reprises lors du déploiement de ressources."
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
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="fedc2-103">Déployer plusieurs instances d’une ressource ou d’une propriété dans des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fedc2-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="fedc2-104">Cette rubrique montre comment procéder à une itération dans votre modèle Azure Resource Manager pour créer plusieurs instances d’une ressource ou d’une propriété sur une ressource.</span><span class="sxs-lookup"><span data-stu-id="fedc2-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="fedc2-105">Si vous devez ajouter une logique à votre modèle, qui vous permette de spécifier si une ressource est déployée, voir [Déployer une ressource de manière conditionnelle](#conditionally-deploy-resource).</span><span class="sxs-lookup"><span data-stu-id="fedc2-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="fedc2-106">Itération de ressource</span><span class="sxs-lookup"><span data-stu-id="fedc2-106">Resource iteration</span></span>
<span data-ttu-id="fedc2-107">Pour créer plusieurs instances d’un type de ressource, ajoutez un élément `copy` au type de ressource.</span><span class="sxs-lookup"><span data-stu-id="fedc2-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="fedc2-108">Dans l’élément copy, vous indiquez le nombre d’itérations et un nom pour cette boucle.</span><span class="sxs-lookup"><span data-stu-id="fedc2-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="fedc2-109">La valeur de décompte doit être un entier positif et ne pas dépasser 800.</span><span class="sxs-lookup"><span data-stu-id="fedc2-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="fedc2-110">Resource Manager crée les ressources en parallèle.</span><span class="sxs-lookup"><span data-stu-id="fedc2-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="fedc2-111">Par conséquent, l’ordre de création n’est pas garanti.</span><span class="sxs-lookup"><span data-stu-id="fedc2-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="fedc2-112">Pour créer des ressources itérées en séquence, consultez [Copie en série](#serial-copy).</span><span class="sxs-lookup"><span data-stu-id="fedc2-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="fedc2-113">La ressource à créer plusieurs fois prend le format suivant :</span><span class="sxs-lookup"><span data-stu-id="fedc2-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="fedc2-114">Notez que le nom de chaque ressource inclut la fonction `copyIndex()`, qui renvoie l’itération actuelle de la boucle.</span><span class="sxs-lookup"><span data-stu-id="fedc2-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="fedc2-115">`copyIndex()` est basé sur zéro.</span><span class="sxs-lookup"><span data-stu-id="fedc2-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="fedc2-116">Si bien que l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fedc2-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="fedc2-117">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="fedc2-117">Creates these names:</span></span>

* <span data-ttu-id="fedc2-118">storage0</span><span class="sxs-lookup"><span data-stu-id="fedc2-118">storage0</span></span>
* <span data-ttu-id="fedc2-119">storage1</span><span class="sxs-lookup"><span data-stu-id="fedc2-119">storage1</span></span>
* <span data-ttu-id="fedc2-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="fedc2-120">storage2.</span></span>

<span data-ttu-id="fedc2-121">Pour décaler la valeur d’index, vous pouvez transmettre une valeur dans la fonction copyIndex().</span><span class="sxs-lookup"><span data-stu-id="fedc2-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="fedc2-122">Le nombre d’itérations à effectuer est toujours spécifié dans l’élément copy, mais la valeur de copyIndex est décalée en fonction de la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="fedc2-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="fedc2-123">Si bien que l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fedc2-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="fedc2-124">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="fedc2-124">Creates these names:</span></span>

* <span data-ttu-id="fedc2-125">storage1</span><span class="sxs-lookup"><span data-stu-id="fedc2-125">storage1</span></span>
* <span data-ttu-id="fedc2-126">storage2</span><span class="sxs-lookup"><span data-stu-id="fedc2-126">storage2</span></span>
* <span data-ttu-id="fedc2-127">storage3</span><span class="sxs-lookup"><span data-stu-id="fedc2-127">storage3</span></span>

<span data-ttu-id="fedc2-128">L’opération copy se révèle utile lorsque vous travaillez avec des tableaux, car vous pouvez itérer sur chaque élément du tableau.</span><span class="sxs-lookup"><span data-stu-id="fedc2-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="fedc2-129">Utilisez la fonction `length` sur le tableau pour spécifier le nombre d’itérations, et `copyIndex` pour récupérer l’index actuel dans le tableau.</span><span class="sxs-lookup"><span data-stu-id="fedc2-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="fedc2-130">Si bien que l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fedc2-130">So, the following example:</span></span>

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

<span data-ttu-id="fedc2-131">Crée les noms suivants :</span><span class="sxs-lookup"><span data-stu-id="fedc2-131">Creates these names:</span></span>

* <span data-ttu-id="fedc2-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="fedc2-132">storagecontoso</span></span>
* <span data-ttu-id="fedc2-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="fedc2-133">storagefabrikam</span></span>
* <span data-ttu-id="fedc2-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="fedc2-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="fedc2-135">Copie en série</span><span class="sxs-lookup"><span data-stu-id="fedc2-135">Serial copy</span></span>

<span data-ttu-id="fedc2-136">Lorsque vous utilisez l’élément de copie pour créer plusieurs instances d’un type de ressource, Resource Manager déploie par défaut ces instances en parallèle.</span><span class="sxs-lookup"><span data-stu-id="fedc2-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="fedc2-137">Toutefois, vous souhaiterez peut-être spécifier que les ressources soient déployées en séquence.</span><span class="sxs-lookup"><span data-stu-id="fedc2-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="fedc2-138">Par exemple, lors de la mise à jour d’un environnement de production, vous souhaiterez échelonner les mises à jour afin que seulement un certain nombre soient mises à jour à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="fedc2-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="fedc2-139">Resource Manager fournit des propriétés sur l’élément de copie qui vous permettent de déployer en série plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="fedc2-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="fedc2-140">Dans l’élément de copie, définissez `mode` sur **serial** et `batchSize` sur le nombre d’instances à déployer en même temps.</span><span class="sxs-lookup"><span data-stu-id="fedc2-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="fedc2-141">Avec le mode série, Resource Manager crée une dépendance sur les instances précédentes de la boucle, afin de ne pas démarrer un lot tant que le précédent n’est pas terminé.</span><span class="sxs-lookup"><span data-stu-id="fedc2-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="fedc2-142">La propriété mode accepte également **parallel**, qui est la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="fedc2-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="fedc2-143">Pour tester la copie en série sans créer de ressources réelles, utilisez le modèle suivant qui déploie des modèles imbriqués vides :</span><span class="sxs-lookup"><span data-stu-id="fedc2-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="fedc2-144">Dans l’historique de déploiement, vous remarquez que les déploiements imbriqués sont traités en séquence.</span><span class="sxs-lookup"><span data-stu-id="fedc2-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![déploiement en série](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="fedc2-146">Pour un scénario plus réaliste, l’exemple suivant déploie deux instances à la fois d’une machine virtuelle Linux à partir d’un modèle imbriqué :</span><span class="sxs-lookup"><span data-stu-id="fedc2-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
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
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="fedc2-147">Itération de propriété</span><span class="sxs-lookup"><span data-stu-id="fedc2-147">Property iteration</span></span>

<span data-ttu-id="fedc2-148">Pour créer des valeurs multiples pour une propriété sur une ressource, ajoutez un tableau `copy` dans l’élément Propriétés.</span><span class="sxs-lookup"><span data-stu-id="fedc2-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="fedc2-149">Ce tableau contient des objets possédant tous les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="fedc2-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="fedc2-150">name : nom de la propriété pour laquelle créer plusieurs valeurs</span><span class="sxs-lookup"><span data-stu-id="fedc2-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="fedc2-151">count : nombre de valeurs à créer</span><span class="sxs-lookup"><span data-stu-id="fedc2-151">count - the number of values to create</span></span>
* <span data-ttu-id="fedc2-152">input : objet contenant les valeurs à assigner à la propriété</span><span class="sxs-lookup"><span data-stu-id="fedc2-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="fedc2-153">L’exemple suivant montre comment appliquer `copy` à la propriété dataDisks sur une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="fedc2-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="fedc2-154">Notez que, lorsque vous utilisez `copyIndex` à l’intérieur d’une itération de propriété, vous devez fournir le nom de l’itération.</span><span class="sxs-lookup"><span data-stu-id="fedc2-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="fedc2-155">Il est inutile de fournir le nom quand l’itération de propriété est utilisé avec une itération de ressource.</span><span class="sxs-lookup"><span data-stu-id="fedc2-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="fedc2-156">Le Gestionnaire des ressources développe le tableau `copy` durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="fedc2-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="fedc2-157">Le nom du tableau devient celui de la propriété.</span><span class="sxs-lookup"><span data-stu-id="fedc2-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="fedc2-158">Les valeurs d’entrée deviennent les propriétés de l’objet.</span><span class="sxs-lookup"><span data-stu-id="fedc2-158">The input values become the object properties.</span></span> <span data-ttu-id="fedc2-159">Le modèle déployé devient :</span><span class="sxs-lookup"><span data-stu-id="fedc2-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="fedc2-160">Vous pouvez utiliser des itérations de ressource et de propriété ensemble.</span><span class="sxs-lookup"><span data-stu-id="fedc2-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="fedc2-161">Référencez l’itération de propriété par son nom.</span><span class="sxs-lookup"><span data-stu-id="fedc2-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="fedc2-162">Vous ne pouvez inclure qu’un seul élément de copie dans les propriétés de chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="fedc2-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="fedc2-163">Pour spécifier une boucle d’itération pour plusieurs propriétés, définissez plusieurs objets dans le tableau de copie.</span><span class="sxs-lookup"><span data-stu-id="fedc2-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="fedc2-164">Chaque objet est itéré séparément.</span><span class="sxs-lookup"><span data-stu-id="fedc2-164">Each object is iterated separately.</span></span> <span data-ttu-id="fedc2-165">Par exemple, pour créer plusieurs instances des propriétés `frontendIPConfigurations` et `loadBalancingRules` sur un équilibreur de charge, définissez les deux objets dans un élément de copie unique :</span><span class="sxs-lookup"><span data-stu-id="fedc2-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="fedc2-166">En fonction des ressources dans une boucle</span><span class="sxs-lookup"><span data-stu-id="fedc2-166">Depend on resources in a loop</span></span>
<span data-ttu-id="fedc2-167">Vous spécifiez qu’une ressource est déployée après une autre ressource à l’aide de l’élément `dependsOn`.</span><span class="sxs-lookup"><span data-stu-id="fedc2-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="fedc2-168">Pour déployer une ressource qui dépend de la collection de ressources dans une boucle, vous pouvez utiliser le nom de la boucle de copie dans l’élément dependsOn.</span><span class="sxs-lookup"><span data-stu-id="fedc2-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="fedc2-169">L’exemple suivant montre comment déployer trois comptes de stockage avant de déployer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fedc2-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="fedc2-170">La définition complète de la machine virtuelle n’est pas affichée.</span><span class="sxs-lookup"><span data-stu-id="fedc2-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="fedc2-171">Notez que le nom de l’élément de copie a la valeur `storagecopy` et que l’élément dependsOn pour la machine virtuelle est également défini sur `storagecopy`.</span><span class="sxs-lookup"><span data-stu-id="fedc2-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="fedc2-172">Création de plusieurs instances d’une ressource enfant</span><span class="sxs-lookup"><span data-stu-id="fedc2-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="fedc2-173">Vous ne pouvez pas utiliser une boucle de copie pour une ressource enfant.</span><span class="sxs-lookup"><span data-stu-id="fedc2-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="fedc2-174">Pour créer plusieurs instances d’une ressource que vous définissez généralement comme imbriquée dans une autre ressource, vous devez plutôt créer cette ressource comme une ressource de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="fedc2-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="fedc2-175">Vous définissez la relation avec la ressource parente par le biais des propriétés type et name.</span><span class="sxs-lookup"><span data-stu-id="fedc2-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="fedc2-176">Par exemple, supposons que vous définissez généralement un jeu de données comme une ressource enfant dans une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="fedc2-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="fedc2-177">Pour créer plusieurs instances de jeux de données, vous devez le déplacer en dehors de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="fedc2-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="fedc2-178">Le jeu de données doit être au même niveau que la fabrique de données, mais il est toujours une ressource enfant de la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="fedc2-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="fedc2-179">Vous conservez la relation entre le jeu de données et la fabrique de données par le biais des propriétés type et name.</span><span class="sxs-lookup"><span data-stu-id="fedc2-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="fedc2-180">Étant donné que le type ne peut plus peut être déduit à partir de sa position dans le modèle, vous devez fournir le type qualifié complet au format : `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span><span class="sxs-lookup"><span data-stu-id="fedc2-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="fedc2-181">Pour établir une relation parent/enfant avec une instance de la fabrique de données, fournissez un nom pour le jeu de données incluant le nom de la ressource parente.</span><span class="sxs-lookup"><span data-stu-id="fedc2-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="fedc2-182">Utilisez le format : `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="fedc2-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="fedc2-183">L’exemple ci-après illustre l’implémentation :</span><span class="sxs-lookup"><span data-stu-id="fedc2-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="fedc2-184">Déployer une ressource de manière conditionnelle</span><span class="sxs-lookup"><span data-stu-id="fedc2-184">Conditionally deploy resource</span></span>

<span data-ttu-id="fedc2-185">Pour spécifier si une ressource est déployée, utilisez l’élément `condition`.</span><span class="sxs-lookup"><span data-stu-id="fedc2-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="fedc2-186">La valeur de cet élément est résolue en true ou false.</span><span class="sxs-lookup"><span data-stu-id="fedc2-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="fedc2-187">Lorsque la valeur est true, la ressource est déployée.</span><span class="sxs-lookup"><span data-stu-id="fedc2-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="fedc2-188">Lorsque la valeur est false, la ressource n’est pas déployée.</span><span class="sxs-lookup"><span data-stu-id="fedc2-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="fedc2-189">Par exemple, pour spécifier si un nouveau compte de stockage est déployé ou si un compte de stockage existant est utilisé, utilisez :</span><span class="sxs-lookup"><span data-stu-id="fedc2-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="fedc2-190">Pour obtenir un exemple d’utilisation d’une ressource nouvelle ou existante, voir [Modèle de condition New ou Existing](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span><span class="sxs-lookup"><span data-stu-id="fedc2-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="fedc2-191">Pour obtenir un exemple d’utilisation d’un mot de passe ou d’une clé SSH pour déployer une machine virtuelle, voir [Modèle de condition Username ou SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span><span class="sxs-lookup"><span data-stu-id="fedc2-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fedc2-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fedc2-192">Next steps</span></span>
* <span data-ttu-id="fedc2-193">Pour en savoir plus sur les sections d’un modèle, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fedc2-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="fedc2-194">Pour savoir comment déployer votre modèle, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fedc2-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

