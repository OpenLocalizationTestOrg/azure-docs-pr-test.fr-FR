---
title: "aaaPass de valeurs complexes entre les modèles Azure | Documents Microsoft"
description: "Montre recommandé approches pour l’utilisation de données d’état des objets complexes tooshare avec les modèles liés et les modèles Azure Resource Manager."
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="97953-103">Tooand d’état de partage à partir de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97953-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="97953-104">Cette rubrique présente les bonnes pratiques pour gérer et partager l’état dans les modèles.</span><span class="sxs-lookup"><span data-stu-id="97953-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="97953-105">Hello paramètres et des variables dans cette rubrique sont des exemples de type hello d’objets que vous pouvez définir tooconveniently organiser vos exigences de déploiement.</span><span class="sxs-lookup"><span data-stu-id="97953-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="97953-106">À partir de ces exemples, vous pouvez implémenter vos propres objets avec les valeurs de propriété pertinentes pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="97953-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="97953-107">Cette rubrique fait partie d’un livre blanc plus volumineux.</span><span class="sxs-lookup"><span data-stu-id="97953-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="97953-108">hello tooread complète papier, téléchargez [World classe ressource Gestionnaire de modèles et éprouvée méthodes conseillées](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="97953-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="97953-109">Fournir les paramètres de configuration standard</span><span class="sxs-lookup"><span data-stu-id="97953-109">Provide standard configuration settings</span></span>
<span data-ttu-id="97953-110">Au lieu de proposer un modèle qui fournit une flexibilité totale et nombreuses variations, un modèle commun est tooprovide une sélection de configurations connues.</span><span class="sxs-lookup"><span data-stu-id="97953-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="97953-111">En effet, les utilisateurs peuvent sélectionner des tailles de t-shirt standard comme enfant, petite, moyenne et grande.</span><span class="sxs-lookup"><span data-stu-id="97953-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="97953-112">Les autres exemples de taille standard sont des offres de produits, telles que l’édition Community ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="97953-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="97953-113">Dans d’autres cas, il peut s’agir de configurations d’une technologie propres à une charge de travail, par exemple MapReduce ou sans SQL.</span><span class="sxs-lookup"><span data-stu-id="97953-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="97953-114">Avec les objets complexes, vous pouvez créer des variables qui contiennent des collections de données, parfois appelées « conteneurs de propriétés » et utiliser cette déclaration de ressource données toodrive hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="97953-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="97953-115">Cette approche fournit des configurations correctes, connues de différentes tailles qui sont préconfigurées pour les clients.</span><span class="sxs-lookup"><span data-stu-id="97953-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="97953-116">Sans des configurations connues, les utilisateurs du modèle de hello doivent déterminer la taille de cluster sur leur propre facteur de contraintes de ressources de plateforme et faire mathématiques tooidentify hello résultant partitionnement des comptes de stockage et d’autres ressources (en raison de la taille de toocluster et contraintes de ressources).</span><span class="sxs-lookup"><span data-stu-id="97953-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="97953-117">En outre toomaking une meilleure expérience client de hello, quelques configurations connues toosupport plus facile et peuvent vous aider à assurer un haut niveau de densité.</span><span class="sxs-lookup"><span data-stu-id="97953-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="97953-118">Hello suivant montre l’exemple de comment toodefine les variables qui contiennent les objets complexes pour représenter des collections de données.</span><span class="sxs-lookup"><span data-stu-id="97953-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="97953-119">collections de Hello définissent les valeurs qui sont utilisées pour la taille de machine virtuelle, les paramètres réseau, les paramètres de système d’exploitation et les paramètres de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="97953-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="97953-120">Notez que hello **tshirtSize** variable concatène une taille de t-shirt hello fourni via un paramètre (**petit**, **support**, **grande**) toohello texte **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="97953-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="97953-121">Vous utilisez cette variable objet complexe associé de hello tooretrieve variable pour cette taille de t-shirt.</span><span class="sxs-lookup"><span data-stu-id="97953-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="97953-122">Vous pouvez ensuite référencer ces variables plus loin dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="97953-123">Hello tooreference possibilité nommé-variables et leurs propriétés simplifie la syntaxe de modèle hello et rend facile toounderstand contexte.</span><span class="sxs-lookup"><span data-stu-id="97953-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="97953-124">Hello, l’exemple suivant définit un toodeploy de ressources à l’aide d’objets hello illustrés précédemment tooset valeurs.</span><span class="sxs-lookup"><span data-stu-id="97953-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="97953-125">Par exemple, hello taille de machine virtuelle est définie en récupérant la valeur hello pour `variables('tshirtSize').vmSize` tandis que la valeur de hello pour la taille du disque hello est récupéré à partir de `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="97953-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="97953-126">En outre, hello URI pour un modèle lié est défini avec la valeur hello pour `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="97953-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="97953-127">Passez le modèle d’état tooa</span><span class="sxs-lookup"><span data-stu-id="97953-127">Pass state tooa template</span></span>
<span data-ttu-id="97953-128">Vous pouvez partager l’état dans un modèle via les paramètres que vous fournissez directement pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="97953-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="97953-129">Hello table des paramètres de listes couramment utilisées dans les modèles suivants.</span><span class="sxs-lookup"><span data-stu-id="97953-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="97953-130">Nom</span><span class="sxs-lookup"><span data-stu-id="97953-130">Name</span></span> | <span data-ttu-id="97953-131">Valeur</span><span class="sxs-lookup"><span data-stu-id="97953-131">Value</span></span> | <span data-ttu-id="97953-132">Description</span><span class="sxs-lookup"><span data-stu-id="97953-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97953-133">location</span><span class="sxs-lookup"><span data-stu-id="97953-133">location</span></span> |<span data-ttu-id="97953-134">Chaîne obtenue à partir d’une liste contrainte des régions Azure</span><span class="sxs-lookup"><span data-stu-id="97953-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="97953-135">emplacement Hello où vous déployez des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="97953-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="97953-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="97953-137">String</span><span class="sxs-lookup"><span data-stu-id="97953-137">String</span></span> |<span data-ttu-id="97953-138">Nom DNS unique pour hello compte de stockage où sont placés les disques de l’ordinateur virtuel hello</span><span class="sxs-lookup"><span data-stu-id="97953-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="97953-139">domainName</span><span class="sxs-lookup"><span data-stu-id="97953-139">domainName</span></span> |<span data-ttu-id="97953-140">String</span><span class="sxs-lookup"><span data-stu-id="97953-140">String</span></span> |<span data-ttu-id="97953-141">Nom de domaine de hello accessible publiquement jumpbox machine virtuelle dans un format de hello : **{domainName}. {} emplacement}.cloudapp.com** par exemple : **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="97953-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="97953-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="97953-142">adminUsername</span></span> |<span data-ttu-id="97953-143">String</span><span class="sxs-lookup"><span data-stu-id="97953-143">String</span></span> |<span data-ttu-id="97953-144">Nom d’utilisateur pour hello machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="97953-144">Username for hello VMs</span></span> |
| <span data-ttu-id="97953-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="97953-145">adminPassword</span></span> |<span data-ttu-id="97953-146">String</span><span class="sxs-lookup"><span data-stu-id="97953-146">String</span></span> |<span data-ttu-id="97953-147">Mot de passe pour hello machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="97953-147">Password for hello VMs</span></span> |
| <span data-ttu-id="97953-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="97953-148">tshirtSize</span></span> |<span data-ttu-id="97953-149">Chaîne obtenue à partir d’une liste contrainte des propositions de tailles de t-shirt</span><span class="sxs-lookup"><span data-stu-id="97953-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="97953-150">Hello nommé tooprovision de taille d’unité mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="97953-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="97953-151">Par exemple, « Petit », « Moyen », « Grand »</span><span class="sxs-lookup"><span data-stu-id="97953-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="97953-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="97953-152">virtualNetworkName</span></span> |<span data-ttu-id="97953-153">String</span><span class="sxs-lookup"><span data-stu-id="97953-153">String</span></span> |<span data-ttu-id="97953-154">Nom de réseau virtuel hello hello consommateur souhaite toouse.</span><span class="sxs-lookup"><span data-stu-id="97953-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="97953-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="97953-155">enableJumpbox</span></span> |<span data-ttu-id="97953-156">Chaîne obtenue à partir d’une liste contrainte (activée/désactivée)</span><span class="sxs-lookup"><span data-stu-id="97953-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="97953-157">Paramètre qui identifie si tooenable un jumpbox pour l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="97953-158">Valeurs : « activée », « désactivée »</span><span class="sxs-lookup"><span data-stu-id="97953-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="97953-159">Hello **tshirtSize** paramètre utilisé dans la section précédente de hello est défini en tant que :</span><span class="sxs-lookup"><span data-stu-id="97953-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="97953-160">Passer des modèles de toolinked d’état</span><span class="sxs-lookup"><span data-stu-id="97953-160">Pass state toolinked templates</span></span>
<span data-ttu-id="97953-161">Lors de la connexion toolinked modèles, vous souvent utilisez un mélange de static et généré des variables.</span><span class="sxs-lookup"><span data-stu-id="97953-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="97953-162">Variables statiques</span><span class="sxs-lookup"><span data-stu-id="97953-162">Static variables</span></span>
<span data-ttu-id="97953-163">Les variables statiques sont souvent des valeurs de base tooprovide utilisées, telles que les URL, qui sont utilisés dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="97953-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="97953-164">Bonjour suivant extrait du modèle, `templateBaseUrl` Spécifie l’emplacement racine du hello pour le modèle de hello dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="97953-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="97953-165">ligne suivante de Hello génère une nouvelle variable `sharedTemplateUrl` qui concatène hello les URL de base avec le nom connu de hello du modèle de ressources partagées hello.</span><span class="sxs-lookup"><span data-stu-id="97953-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="97953-166">Sous cette ligne, une variable objet complexe toostore utilisé une taille de t-shirt, où est URL de base hello toohello concaténée connu d’emplacement de modèle de configuration et stockées dans hello `vmTemplate` propriété.</span><span class="sxs-lookup"><span data-stu-id="97953-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="97953-167">avantage Hello de cette approche est que si l’emplacement du modèle hello change, vous devez uniquement variable statique de hello toochange dans un seul endroit, ce qui se passe dans l’ensemble de modèles de hello lié.</span><span class="sxs-lookup"><span data-stu-id="97953-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="97953-168">Variables générées</span><span class="sxs-lookup"><span data-stu-id="97953-168">Generated variables</span></span>
<span data-ttu-id="97953-169">Dans les variables toostatic de plus, plusieurs variables sont générées dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="97953-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="97953-170">Cette section répertorie quelques-uns des types courants de hello de variables générés.</span><span class="sxs-lookup"><span data-stu-id="97953-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="97953-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="97953-171">tshirtSize</span></span>
<span data-ttu-id="97953-172">Vous êtes familiarisé avec cette variable générée à partir d’exemples hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="97953-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="97953-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="97953-173">networkSettings</span></span>
<span data-ttu-id="97953-174">Un Bonjour de capacité, fonctionnalité ou le modèle de solution avec étendue de bout en bout, modèles liés créent généralement des ressources qui existent sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="97953-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="97953-175">Une approche simple est toouse paramètres réseau toostore objet complexe et les passer toolinked modèles.</span><span class="sxs-lookup"><span data-stu-id="97953-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="97953-176">Un exemple de paramètres de réseau de communication est affiché ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="97953-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="97953-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="97953-177">availabilitySettings</span></span>
<span data-ttu-id="97953-178">Les ressources créées dans des modèles liés sont souvent placées dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="97953-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="97953-179">Dans l’exemple suivant de hello, nom du jeu de disponibilité hello est spécifié et également hello domaine d’erreur et toouse de compte de domaine de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="97953-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="97953-180">Si vous avez besoin de plusieurs groupes à haute disponibilité (par exemple, un pour les nœuds principaux) et l’autre pour les nœuds de données, vous pouvez utiliser un nom en tant que préfixe, spécifiez plusieurs ensembles de disponibilité ou de suivre le modèle hello indiquée précédemment pour créer une variable pour une taille de t-shirt spécifique.</span><span class="sxs-lookup"><span data-stu-id="97953-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="97953-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="97953-181">storageSettings</span></span>
<span data-ttu-id="97953-182">Les détails du stockage sont souvent partagés avec les modèles liés.</span><span class="sxs-lookup"><span data-stu-id="97953-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="97953-183">Dans l’exemple hello ci-dessous, un *storageSettings* objet fournit des détails sur hello les noms de compte et conteneur de stockage.</span><span class="sxs-lookup"><span data-stu-id="97953-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="97953-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="97953-184">osSettings</span></span>
<span data-ttu-id="97953-185">Avec les modèles liés, vous devrez peut-être toopass les types de nœuds de toovarious paramètres de système d’exploitation sur les types de configuration connu différente.</span><span class="sxs-lookup"><span data-stu-id="97953-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="97953-186">Un objet complexe est un moyen simple toostore et partage de système d’exploitation et le rend également toosupport plus facilement plusieurs choix de système d’exploitation pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="97953-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="97953-187">Hello suivant montre un objet pour *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="97953-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="97953-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="97953-188">machineSettings</span></span>
<span data-ttu-id="97953-189">Une variable générée, *machineSettings* est un objet complexe contenant un mélange de variables de base pour la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="97953-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="97953-190">les variables Hello incluent une référence d’image de système d’exploitation, nom d’utilisateur administrateur et un mot de passe et un préfixe pour les noms de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="97953-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="97953-191">Notez que *osImageReference* récupère hello des valeurs à partir de hello *osSettings* variable définie dans les modèles principal hello.</span><span class="sxs-lookup"><span data-stu-id="97953-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="97953-192">Cela signifie que vous pouvez facilement modifier le système d’exploitation de hello pour une machine virtuelle — totalement ou selon la préférence hello d’un consommateur de modèle.</span><span class="sxs-lookup"><span data-stu-id="97953-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="97953-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="97953-193">vmScripts</span></span>
<span data-ttu-id="97953-194">Hello *vmScripts* de l’objet contient des détails sur toodownload de scripts hello et d’exécution sur une instance de machine virtuelle, y compris les références externes et internes.</span><span class="sxs-lookup"><span data-stu-id="97953-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="97953-195">En dehors de références incluent les infrastructure hello.</span><span class="sxs-lookup"><span data-stu-id="97953-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="97953-196">Les références à l’intérieur incluent la configuration et les logiciels installé de hello installé.</span><span class="sxs-lookup"><span data-stu-id="97953-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="97953-197">Vous utilisez hello *scriptsToDownload* hello toolist de propriété scripts toodownload toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="97953-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="97953-198">Cet objet contient également des références des arguments de ligne toocommand pour différents types d’actions.</span><span class="sxs-lookup"><span data-stu-id="97953-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="97953-199">Ces actions incluent l’exécution d’installation par défaut de hello pour chaque nœud, une installation qui s’exécute après que tous les nœuds sont déployés et des scripts supplémentaires qui peuvent être spécifique tooa donné du modèle.</span><span class="sxs-lookup"><span data-stu-id="97953-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="97953-200">Cet exemple fait à partir d’un modèle utilisé de toodeploy MongoDB, qui requiert une arbitre toodeliver une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="97953-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="97953-201">Hello *arbiterNodeInstallCommand* a été ajouté trop*vmScripts* tooinstall l’arbitre hello.</span><span class="sxs-lookup"><span data-stu-id="97953-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="97953-202">section de variables Hello est où trouver des variables hello qui définissent le script de hello tooexecute hello un texte spécifique avec les valeurs appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="97953-203">Retourner l’état à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="97953-203">Return state from a template</span></span>
<span data-ttu-id="97953-204">Non seulement peuvent passer des données dans un modèle, vous pouvez également un modèle de partage de données toohello précédent appel.</span><span class="sxs-lookup"><span data-stu-id="97953-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="97953-205">Bonjour **génère** section d’un modèle lié, vous pouvez fournir des paires clé/valeur qui peuvent être consommés par le modèle de source de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="97953-206">Hello suivant montre comment toopass hello adresse IP privée générée dans un modèle lié.</span><span class="sxs-lookup"><span data-stu-id="97953-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="97953-207">Dans le modèle principal de hello, vous pouvez utiliser ces données avec la syntaxe de hello :</span><span class="sxs-lookup"><span data-stu-id="97953-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="97953-208">Vous pouvez utiliser cette expression dans hello sorties soit hello ressources de modèle principal de hello.</span><span class="sxs-lookup"><span data-stu-id="97953-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="97953-209">Impossible d’utiliser expression de hello dans la section des variables hello, car il s’appuie sur l’état d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="97953-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="97953-210">tooreturn cette valeur à partir du modèle principal hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="97953-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="97953-211">Pour obtenir un exemple d’utilisation de hello génère section un modèle lié tooreturn de disques de données pour un ordinateur virtuel, consultez [création de plusieurs disques de données pour un ordinateur virtuel](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="97953-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="97953-212">Définir les paramètres d’authentification d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="97953-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="97953-213">Vous pouvez utiliser hello même modèle indiqué précédemment pour les paramètres d’authentification hello des toospecify de paramètres de configuration pour un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="97953-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="97953-214">Vous créez un paramètre pour passer de type hello d’authentification.</span><span class="sxs-lookup"><span data-stu-id="97953-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="97953-215">Vous ajoutez des variables pour hello différents types d’authentification et une variable toostore que le type est utilisé pour ce déploiement basé sur la valeur hello du paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="97953-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="97953-216">Lorsque vous définissez l’ordinateur virtuel de hello, vous définissez hello **osProfile** variable toohello vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="97953-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="97953-217">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="97953-217">Next steps</span></span>
* <span data-ttu-id="97953-218">toolearn sur les sections hello hello du modèle de, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="97953-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="97953-219">les fonctions hello toosee qui sont disponibles dans un modèle, consultez [fonctions de modèle de gestionnaire de ressources Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="97953-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
