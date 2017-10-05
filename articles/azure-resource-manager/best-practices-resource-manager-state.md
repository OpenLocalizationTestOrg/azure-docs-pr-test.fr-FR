---
title: "Transmettre des valeurs complexes entre les modèles Azure | Microsoft Docs"
description: "Ce didacticiel présente des approches recommandées pour l’utilisation des objets complexes afin de partager des données d’état avec des modèles Azure Resource Manager et leurs modèles liés."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="14099-103">Partage d’état vers et depuis les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14099-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="14099-104">Cette rubrique présente les bonnes pratiques pour gérer et partager l’état dans les modèles.</span><span class="sxs-lookup"><span data-stu-id="14099-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="14099-105">Les paramètres et les variables présentés dans cette rubrique sont des exemples du type d'objets que vous pouvez définir pour organiser aisément votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="14099-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="14099-106">À partir de ces exemples, vous pouvez implémenter vos propres objets avec les valeurs de propriété pertinentes pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="14099-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="14099-107">Cette rubrique fait partie d’un livre blanc plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="14099-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="14099-108">Pour lire le livre blanc complet, téléchargez [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf) (Considérations et pratiques éprouvées concernant les modèles Resource Manager de classe mondiale).</span><span class="sxs-lookup"><span data-stu-id="14099-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="14099-109">Fournir les paramètres de configuration standard</span><span class="sxs-lookup"><span data-stu-id="14099-109">Provide standard configuration settings</span></span>
<span data-ttu-id="14099-110">Au lieu de proposer un modèle qui fournit une flexibilité totale et des variations innombrables, il est courant de fournir une sélection de configurations connues.</span><span class="sxs-lookup"><span data-stu-id="14099-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="14099-111">En effet, les utilisateurs peuvent sélectionner des tailles de t-shirt standard comme enfant, petite, moyenne et grande.</span><span class="sxs-lookup"><span data-stu-id="14099-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="14099-112">Les autres exemples de taille standard sont des offres de produits, telles que l’édition Community ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="14099-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="14099-113">Dans d’autres cas, il peut s’agir de configurations d’une technologie propres à une charge de travail, par exemple MapReduce ou sans SQL.</span><span class="sxs-lookup"><span data-stu-id="14099-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="14099-114">Avec des objets complexes, vous pouvez créer des variables qui contiennent des collections de données, parfois appelées « conteneurs de propriétés » et utiliser ces données pour effectuer la déclaration de ressources dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="14099-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="14099-115">Cette approche fournit des configurations correctes, connues de différentes tailles qui sont préconfigurées pour les clients.</span><span class="sxs-lookup"><span data-stu-id="14099-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="14099-116">Sans configurations connues, les utilisateurs du modèle doivent eux-mêmes déterminer la taille de cluster, tenir compte des contraintes des ressources de plateforme et effectuer des opérations mathématiques pour identifier le partitionnement résultant des comptes de stockage et des autres ressources (en raison des contraintes de taille de cluster et de ressource).</span><span class="sxs-lookup"><span data-stu-id="14099-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="14099-117">Outre l’amélioration de l’expérience du client qu’il procure, un petit nombre de configurations connues est plus facile à prendre en charge et peut vous aider à fournir un haut niveau de densité.</span><span class="sxs-lookup"><span data-stu-id="14099-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="14099-118">L’exemple suivant indique comment définir des variables qui contiennent des objets complexes pour représenter des collections de données.</span><span class="sxs-lookup"><span data-stu-id="14099-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="14099-119">Les collections définissent des valeurs utilisées pour la taille de machine virtuelle, des paramètres réseau, des paramètres de système d’exploitation et des paramètres de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="14099-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="14099-120">Notez que la variable **tshirtSize** concatène la taille de t-shirt que vous avez fournie via un paramètre (**Small**, **Medium**, **Large**) au texte **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="14099-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="14099-121">Cette variable permet de récupérer la variable objet complexe associée pour cette taille de t-shirt.</span><span class="sxs-lookup"><span data-stu-id="14099-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="14099-122">Vous pouvez ensuite référencer ces variables plus loin dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="14099-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="14099-123">La possibilité de référencer des variables nommées et leurs propriétés simplifie la syntaxe du modèle et la compréhension du contexte.</span><span class="sxs-lookup"><span data-stu-id="14099-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="14099-124">L’exemple suivant définit une ressource à déployer à l’aide d’objets indiqués précédemment pour définir des valeurs.</span><span class="sxs-lookup"><span data-stu-id="14099-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="14099-125">Par exemple, la taille de la machine virtuelle est définie en récupérant la valeur de `variables('tshirtSize').vmSize` tandis que la valeur de la taille du disque est extraite de `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="14099-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="14099-126">En outre, l'URI d'un modèle lié est défini avec la valeur de `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="14099-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="14099-127">Passer l’état à un modèle</span><span class="sxs-lookup"><span data-stu-id="14099-127">Pass state to a template</span></span>
<span data-ttu-id="14099-128">Vous pouvez partager l’état dans un modèle via les paramètres que vous fournissez directement pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="14099-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="14099-129">Le tableau suivant répertorie les paramètres couramment utilisés dans les modèles.</span><span class="sxs-lookup"><span data-stu-id="14099-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="14099-130">Nom</span><span class="sxs-lookup"><span data-stu-id="14099-130">Name</span></span> | <span data-ttu-id="14099-131">Valeur</span><span class="sxs-lookup"><span data-stu-id="14099-131">Value</span></span> | <span data-ttu-id="14099-132">Description</span><span class="sxs-lookup"><span data-stu-id="14099-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="14099-133">location</span><span class="sxs-lookup"><span data-stu-id="14099-133">location</span></span> |<span data-ttu-id="14099-134">Chaîne obtenue à partir d’une liste contrainte des régions Azure</span><span class="sxs-lookup"><span data-stu-id="14099-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="14099-135">L’emplacement où les ressources sont déployées.</span><span class="sxs-lookup"><span data-stu-id="14099-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="14099-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="14099-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="14099-137">String</span><span class="sxs-lookup"><span data-stu-id="14099-137">String</span></span> |<span data-ttu-id="14099-138">Il s’agit du nom DNS unique du compte de stockage où sont placés les disques de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="14099-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="14099-139">domainName</span><span class="sxs-lookup"><span data-stu-id="14099-139">domainName</span></span> |<span data-ttu-id="14099-140">String</span><span class="sxs-lookup"><span data-stu-id="14099-140">String</span></span> |<span data-ttu-id="14099-141">Il s’agit du nom de domaine de la machine virtuelle jumpbox publique, dont le format est : **{Nom_de_domaine}.{emplacement}.cloudapp.com**. Par exemple : **monnomdedomaine.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="14099-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="14099-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="14099-142">adminUsername</span></span> |<span data-ttu-id="14099-143">Chaîne</span><span class="sxs-lookup"><span data-stu-id="14099-143">String</span></span> |<span data-ttu-id="14099-144">Il s’agit du nom d’utilisateur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="14099-144">Username for the VMs</span></span> |
| <span data-ttu-id="14099-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="14099-145">adminPassword</span></span> |<span data-ttu-id="14099-146">Chaîne</span><span class="sxs-lookup"><span data-stu-id="14099-146">String</span></span> |<span data-ttu-id="14099-147">Il s’agit du mot de passe des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="14099-147">Password for the VMs</span></span> |
| <span data-ttu-id="14099-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="14099-148">tshirtSize</span></span> |<span data-ttu-id="14099-149">Chaîne obtenue à partir d’une liste contrainte des propositions de tailles de t-shirt</span><span class="sxs-lookup"><span data-stu-id="14099-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="14099-150">Il s’agit de la taille d’unité d’échelle nommée à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="14099-150">The named scale unit size to provision.</span></span> <span data-ttu-id="14099-151">Par exemple, « Petit », « Moyen », « Grand »</span><span class="sxs-lookup"><span data-stu-id="14099-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="14099-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="14099-152">virtualNetworkName</span></span> |<span data-ttu-id="14099-153">Chaîne</span><span class="sxs-lookup"><span data-stu-id="14099-153">String</span></span> |<span data-ttu-id="14099-154">Il s’agit du nom du réseau virtuel que le consommateur souhaite utiliser.</span><span class="sxs-lookup"><span data-stu-id="14099-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="14099-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="14099-155">enableJumpbox</span></span> |<span data-ttu-id="14099-156">Chaîne obtenue à partir d’une liste contrainte (activée/désactivée)</span><span class="sxs-lookup"><span data-stu-id="14099-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="14099-157">Paramètre indiquant s’il faut activer une jumpbox pour l’environnement.</span><span class="sxs-lookup"><span data-stu-id="14099-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="14099-158">Valeurs : « activée », « désactivée »</span><span class="sxs-lookup"><span data-stu-id="14099-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="14099-159">Le paramètre **tshirtSize** utilisé dans la section précédente est défini comme suit :</span><span class="sxs-lookup"><span data-stu-id="14099-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="14099-160">Passer l’état à des modèles liés</span><span class="sxs-lookup"><span data-stu-id="14099-160">Pass state to linked templates</span></span>
<span data-ttu-id="14099-161">Lors de la connexion aux modèles liés, vous utilisez généralement une combinaison de variables statiques et générées.</span><span class="sxs-lookup"><span data-stu-id="14099-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="14099-162">Variables statiques</span><span class="sxs-lookup"><span data-stu-id="14099-162">Static variables</span></span>
<span data-ttu-id="14099-163">Des variables statiques sont souvent utilisées pour fournir les valeurs de base, telles que des URL, qui sont utilisées au sein d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="14099-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="14099-164">Dans l’extrait de modèle suivant, `templateBaseUrl` indique l’emplacement racine du modèle dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="14099-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="14099-165">La ligne suivante génère une nouvelle variable `sharedTemplateUrl` qui concatène l’URL de base avec le nom connu du modèle de ressources partagées.</span><span class="sxs-lookup"><span data-stu-id="14099-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="14099-166">En dessous de cette ligne, une variable objet complexe est utilisée pour stocker une taille de t-shirt, dans laquelle l’URL de base est concaténée à l’emplacement du modèle de configuration connu et stockée dans la propriété `vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="14099-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="14099-167">L’avantage de cette approche est que si l’emplacement du modèle change, il vous suffit de modifier la variable statique à un endroit, d’où la modification est transmise à tous les modèles liés.</span><span class="sxs-lookup"><span data-stu-id="14099-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="14099-168">Variables générées</span><span class="sxs-lookup"><span data-stu-id="14099-168">Generated variables</span></span>
<span data-ttu-id="14099-169">En plus des variables statiques, plusieurs variables sont générées dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="14099-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="14099-170">Cette section répertorie les types courants de variables générées.</span><span class="sxs-lookup"><span data-stu-id="14099-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="14099-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="14099-171">tshirtSize</span></span>
<span data-ttu-id="14099-172">Vous connaissez déjà cette variable générée de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="14099-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="14099-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="14099-173">networkSettings</span></span>
<span data-ttu-id="14099-174">Dans une capacité, une fonctionnalité ou un modèle de solution étendue de bout en bout, les modèles liés créent généralement des ressources qui existent sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="14099-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="14099-175">Une approche simple consiste à utiliser un objet complexe pour stocker les paramètres de réseau et les transmettre aux modèles liés.</span><span class="sxs-lookup"><span data-stu-id="14099-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="14099-176">Un exemple de paramètres de réseau de communication est affiché ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="14099-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="14099-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="14099-177">availabilitySettings</span></span>
<span data-ttu-id="14099-178">Les ressources créées dans des modèles liés sont souvent placées dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="14099-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="14099-179">Dans l’exemple suivant, le nom du groupe à haute disponibilité est spécifié, ainsi que le nombre de domaines d’erreur et de domaines de mise à jour à utiliser.</span><span class="sxs-lookup"><span data-stu-id="14099-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="14099-180">Si vous avez besoin de plusieurs groupes à haute disponibilité (par exemple, un pour les nœuds principaux et un autre pour les nœuds de données), vous pouvez utiliser un nom en tant que préfixe, indiquer plusieurs groupes à haute disponibilité, ou suivre le modèle indiqué précédemment pour créer une variable pour une taille de t-shirt spécifique.</span><span class="sxs-lookup"><span data-stu-id="14099-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="14099-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="14099-181">storageSettings</span></span>
<span data-ttu-id="14099-182">Les détails du stockage sont souvent partagés avec les modèles liés.</span><span class="sxs-lookup"><span data-stu-id="14099-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="14099-183">Dans l'exemple ci-dessous, un objet *storageSettings* fournit des détails sur les noms du compte de stockage et du conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="14099-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="14099-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="14099-184">osSettings</span></span>
<span data-ttu-id="14099-185">Si vous utilisez des modèles liés, vous devrez peut-être transmettre des paramètres de système d’exploitation à différents types de nœuds entre les différents types de configurations connus.</span><span class="sxs-lookup"><span data-stu-id="14099-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="14099-186">Un objet complexe est pratique pour stocker et partager facilement des informations de système d’exploitation et facilite également la prise en charge de plusieurs options de système d’exploitation pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="14099-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="14099-187">L’exemple suivant montre un objet pour *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="14099-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="14099-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="14099-188">machineSettings</span></span>
<span data-ttu-id="14099-189">Une variable générée, *machineSettings* est un objet complexe contenant un mélange de variables de base pour la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="14099-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="14099-190">Les variables incluent le nom et le mot de passe d’utilisateur administrateur, un préfixe pour les noms de machine virtuelle et une référence de l’image du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="14099-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="14099-191">Notez que *osImageReference* récupère les valeurs à partir de la variable *osSettings* définie dans le modèle principal.</span><span class="sxs-lookup"><span data-stu-id="14099-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="14099-192">Cela signifie que vous pouvez facilement modifier le système d’exploitation d’une machine virtuelle, soit entièrement, soit en fonction de la préférence d’un consommateur du modèle.</span><span class="sxs-lookup"><span data-stu-id="14099-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="14099-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="14099-193">vmScripts</span></span>
<span data-ttu-id="14099-194">L'objet *vmScripts* contient des détails sur les scripts à télécharger et exécuter sur une instance de machine virtuelle, notamment des références externes et internes.</span><span class="sxs-lookup"><span data-stu-id="14099-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="14099-195">Les références extérieures incluent l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="14099-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="14099-196">Les références intérieures incluent le logiciel installé et la configuration.</span><span class="sxs-lookup"><span data-stu-id="14099-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="14099-197">La propriété *scriptsToDownload* permet de répertorier les scripts à télécharger vers la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="14099-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="14099-198">Cet objet contient également des références pointant vers des arguments de ligne de commande pour différents types d’actions.</span><span class="sxs-lookup"><span data-stu-id="14099-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="14099-199">Ces actions incluent l’exécution de l’installation par défaut pour chaque nœud, une installation qui s’exécute après le déploiement de tous les nœuds et l’exécution de tous les scripts pouvant être spécifiques à un modèle donné.</span><span class="sxs-lookup"><span data-stu-id="14099-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="14099-200">Cet exemple est tiré d’un modèle utilisé pour déployer MongoDB, qui nécessite un arbitre pour garantir une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="14099-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="14099-201">La chaîne *arbiterNodeInstallCommand* a été ajoutée à *vmScripts* pour installer l’arbitre.</span><span class="sxs-lookup"><span data-stu-id="14099-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="14099-202">Dans la section des variables, vous trouvez les variables qui définissent le texte spécifique pour exécuter le script avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="14099-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="14099-203">Retourner l’état à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="14099-203">Return state from a template</span></span>
<span data-ttu-id="14099-204">Vous pouvez non seulement transmettre des données vers un modèle, mais également renvoyer des données partagées vers le modèle d’appel.</span><span class="sxs-lookup"><span data-stu-id="14099-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="14099-205">Dans la section **sortie** d'un modèle lié, vous pouvez fournir des paires clé/valeur qui peuvent être utilisées par le modèle source.</span><span class="sxs-lookup"><span data-stu-id="14099-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="14099-206">L’exemple suivant montre comment transmettre l’adresse IP privée générée dans un modèle lié.</span><span class="sxs-lookup"><span data-stu-id="14099-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="14099-207">Dans le modèle principal, vous pouvez utiliser ces données avec la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="14099-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="14099-208">Vous pouvez utiliser cette expression dans la section outputs ou la section resources du modèle principal.</span><span class="sxs-lookup"><span data-stu-id="14099-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="14099-209">En revanche, vous ne pouvez pas l’utiliser dans la section variables, car elle dépend de l’état d’exécution.</span><span class="sxs-lookup"><span data-stu-id="14099-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="14099-210">Pour retourner cette valeur à partir du modèle principal, utilisez :</span><span class="sxs-lookup"><span data-stu-id="14099-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="14099-211">Pour obtenir un exemple dans lequel la section outputs d’un modèle lié est utilisée pour retourner des disques de données pour une machine virtuelle, consultez [Création de plusieurs disques de données pour une machine virtuelle](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="14099-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="14099-212">Définir les paramètres d’authentification d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="14099-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="14099-213">Vous pouvez spécifier les paramètres d’authentification d’une machine virtuelle selon le modèle présenté précédemment pour les paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="14099-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="14099-214">Vous créez un paramètre pour passer le type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="14099-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="14099-215">Vous ajoutez des variables pour les différents types d’authentification et une variable pour stocker le type utilisé pour ce déploiement en fonction de la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="14099-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="14099-216">Au moment de définir la machine virtuelle, vous affectez à **osProfile** la variable que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="14099-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="14099-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14099-217">Next steps</span></span>
* <span data-ttu-id="14099-218">Pour en savoir plus sur les sections du modèle, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="14099-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="14099-219">Pour consulter les fonctions disponibles dans un modèle, voir [Fonctions des modèles Azure Resource Manager](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="14099-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
