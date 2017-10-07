---
title: "vue d’ensemble du fournisseur de ressources d’aaaNetwork | Documents Microsoft"
description: "En savoir plus sur hello nouveau fournisseur de ressources réseau dans le Gestionnaire de ressources Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="cf98f-103">Fournisseur de ressources réseau</span><span class="sxs-lookup"><span data-stu-id="cf98f-103">Network Resource Provider</span></span>
<span data-ttu-id="cf98f-104">Un besoin sous-jacente dans le succès d’une entreprise d’aujourd'hui, est hello toobuild de capacité et de gérer les applications prenant en charge du réseau à grande échelle d’une manière agile, souple, sécurisée et reproductible.</span><span class="sxs-lookup"><span data-stu-id="cf98f-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="cf98f-105">Gestionnaire de ressources Azure permet de vous toocreate de telles applications, comme un ensemble unique de ressources dans les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="cf98f-106">Ces ressources sont gérées via divers fournisseurs de ressources sous Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cf98f-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="cf98f-107">Le Gestionnaire de ressources Azure dépend de différents fournisseurs tooprovide accès tooyour ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="cf98f-108">Il existe trois fournisseurs de ressources principaux : réseau, stockage et calcul.</span><span class="sxs-lookup"><span data-stu-id="cf98f-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="cf98f-109">Ce document décrit les caractéristiques de hello et les avantages de hello fournisseur de ressources réseau, y compris :</span><span class="sxs-lookup"><span data-stu-id="cf98f-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="cf98f-110">**Métadonnées** – vous pouvez ajouter tooresources plus d’informations à l’aide de balises.</span><span class="sxs-lookup"><span data-stu-id="cf98f-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="cf98f-111">Ces balises peuvent être utilisées tootrack l’utilisation des ressources entre les abonnements et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="cf98f-112">**Contrôle accru de votre réseau** : les ressources réseau sont faiblement couplées et vous pouvez les contrôler de manière plus précise.</span><span class="sxs-lookup"><span data-stu-id="cf98f-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="cf98f-113">Cela signifie que vous avez plus de souplesse dans la gestion des ressources de mise en réseau hello.</span><span class="sxs-lookup"><span data-stu-id="cf98f-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="cf98f-114">**Configuration plus rapide** : étant donné que les ressources réseau sont faiblement couplées, vous pouvez créer et organiser les ressources réseau en parallèle.</span><span class="sxs-lookup"><span data-stu-id="cf98f-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="cf98f-115">Cela a considérablement réduit le temps de configuration.</span><span class="sxs-lookup"><span data-stu-id="cf98f-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="cf98f-116">**Contrôle d’accès basé sur rôle** -RBAC fournit des rôles par défaut, avec une étendue de sécurité spécifique, dans la création de hello tooallowing Ajout de rôles personnalisés pour la gestion sécurisée.</span><span class="sxs-lookup"><span data-stu-id="cf98f-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="cf98f-117">**Gestion plus facile et le déploiement** -il est plus facile toodeploy et gérer des applications car vous pouvez que vous pouvez créer une pile de l’ensemble de l’application comme une même collection de ressources dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="cf98f-118">Et toodeploy plus rapide, étant donné que vous pouvez déployer en fournissant une charge utile JSON de modèle.</span><span class="sxs-lookup"><span data-stu-id="cf98f-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="cf98f-119">**Personnalisation rapide** -vous pouvez utiliser la personnalisation de reproductibles et rapide de tooenable des déploiements de modèles de style déclaratif.</span><span class="sxs-lookup"><span data-stu-id="cf98f-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="cf98f-120">**Personnalisation REPEATABLE** -vous pouvez utiliser la personnalisation de reproductibles et rapide de tooenable des déploiements de modèles de style déclaratif.</span><span class="sxs-lookup"><span data-stu-id="cf98f-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="cf98f-121">**Interfaces de gestion** -vous pouvez utiliser des hello suivant interfaces toomanage vos ressources :</span><span class="sxs-lookup"><span data-stu-id="cf98f-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="cf98f-122">API REST</span><span class="sxs-lookup"><span data-stu-id="cf98f-122">REST based API</span></span>
  * <span data-ttu-id="cf98f-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf98f-123">PowerShell</span></span>
  * <span data-ttu-id="cf98f-124">Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="cf98f-124">.NET SDK</span></span>
  * <span data-ttu-id="cf98f-125">Kit de développement logiciel (SDK) Node.JS</span><span class="sxs-lookup"><span data-stu-id="cf98f-125">Node.JS SDK</span></span>
  * <span data-ttu-id="cf98f-126">Kit de développement logiciel (SDK) Java</span><span class="sxs-lookup"><span data-stu-id="cf98f-126">Java SDK</span></span>
  * <span data-ttu-id="cf98f-127">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="cf98f-127">Azure CLI</span></span>
  * <span data-ttu-id="cf98f-128">Portail en version préliminaire</span><span class="sxs-lookup"><span data-stu-id="cf98f-128">Preview Portal</span></span>
  * <span data-ttu-id="cf98f-129">Langage du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf98f-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="cf98f-130">Ressources réseau</span><span class="sxs-lookup"><span data-stu-id="cf98f-130">Network resources</span></span>
<span data-ttu-id="cf98f-131">Vous pouvez désormais gérer les ressources réseau indépendamment, au lieu qu'elles soient toutes gérées via une ressource de calcul unique (un machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="cf98f-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="cf98f-132">Cela garantit un degré de flexibilité et de souplesse plus élevé dans la composition d'une infrastructure complexe et à grande échelle dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="cf98f-133">Une vue conceptuelle d'un exemple de déploiement impliquant une application multicouche est présentée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf98f-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="cf98f-134">Chaque ressource que vous voyez, par exemple, les cartes réseau, les adresses IP publiques et les machines virtuelles, peut être gérée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="cf98f-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modèle de ressource réseau](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="cf98f-136">Chaque ressource contient un ensemble commun de propriétés et son jeu de propriétés individuelles.</span><span class="sxs-lookup"><span data-stu-id="cf98f-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="cf98f-137">Propriétés communes de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="cf98f-137">hello common properties are:</span></span>

| <span data-ttu-id="cf98f-138">Propriété</span><span class="sxs-lookup"><span data-stu-id="cf98f-138">Property</span></span> | <span data-ttu-id="cf98f-139">Description</span><span class="sxs-lookup"><span data-stu-id="cf98f-139">Description</span></span> | <span data-ttu-id="cf98f-140">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="cf98f-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf98f-141">**name**</span><span class="sxs-lookup"><span data-stu-id="cf98f-141">**name**</span></span> |<span data-ttu-id="cf98f-142">Nom de ressource unique.</span><span class="sxs-lookup"><span data-stu-id="cf98f-142">Unique resource name.</span></span> <span data-ttu-id="cf98f-143">Chaque type de ressource a ses propres restrictions d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="cf98f-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="cf98f-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="cf98f-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="cf98f-145">**location**</span><span class="sxs-lookup"><span data-stu-id="cf98f-145">**location**</span></span> |<span data-ttu-id="cf98f-146">Région Azure dans le hello ressource réside</span><span class="sxs-lookup"><span data-stu-id="cf98f-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="cf98f-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="cf98f-147">westus, eastus</span></span> |
| <span data-ttu-id="cf98f-148">**id**</span><span class="sxs-lookup"><span data-stu-id="cf98f-148">**id**</span></span> |<span data-ttu-id="cf98f-149">Identification en fonction d’un URI unique</span><span class="sxs-lookup"><span data-stu-id="cf98f-149">Unique URI based identification</span></span> |<span data-ttu-id="cf98f-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="cf98f-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="cf98f-151">Vous pouvez vérifier les propriétés individuelles de hello des ressources dans les sections hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf98f-151">You can check hello individual properties of resources in hello sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="cf98f-152">Interfaces de gestion</span><span class="sxs-lookup"><span data-stu-id="cf98f-152">Management interfaces</span></span>
<span data-ttu-id="cf98f-153">Vous pouvez gérer vos ressources de réseau Azure à l’aide de différentes interfaces.</span><span class="sxs-lookup"><span data-stu-id="cf98f-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="cf98f-154">Dans ce document nous allons nous concentrer sur le dépannage de ces interfaces : API REST et modèles.</span><span class="sxs-lookup"><span data-stu-id="cf98f-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="cf98f-155">API REST</span><span class="sxs-lookup"><span data-stu-id="cf98f-155">REST API</span></span>
<span data-ttu-id="cf98f-156">Comme mentionné précédemment, les ressources réseau peuvent être gérées via une variété d'interfaces, notamment l'API REST, le Kit de développement logiciel (SDK) .NET, le Kit de développement logiciel (SDK) Node.JS, le Kit de développement logiciel (SDK) Java, PowerShell, l'interface en ligne de commande, le portail Azure et des modèles.</span><span class="sxs-lookup"><span data-stu-id="cf98f-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="cf98f-157">l’API Rest de Hello conforme toohello spécification du protocole HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="cf98f-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="cf98f-158">Hello URI structure générale de hello API est présentée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cf98f-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="cf98f-159">Et les paramètres de hello entre accolades représentent hello suivant d’éléments :</span><span class="sxs-lookup"><span data-stu-id="cf98f-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="cf98f-160">**subscription-id** : ID de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cf98f-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="cf98f-161">**Resource-provider-namespace** -espace de noms de fournisseur hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="cf98f-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="cf98f-162">la valeur de fournisseur de ressources réseau hello Hello est *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="cf98f-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="cf98f-163">**nom de la région** -nom de la région Azure hello</span><span class="sxs-lookup"><span data-stu-id="cf98f-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="cf98f-164">Hello méthodes HTTP suivantes sont prises en charge lors de l’établissement des appels toohello API REST :</span><span class="sxs-lookup"><span data-stu-id="cf98f-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="cf98f-165">**PUT** - utilisés toocreate une ressource d’un type donné, modifier une propriété de ressource ou une association entre les ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="cf98f-166">**OBTENIR** -utilisé tooretrieve informations pour une ressource mis en service.</span><span class="sxs-lookup"><span data-stu-id="cf98f-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="cf98f-167">**SUPPRIMER** -utilisé toodelete une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="cf98f-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="cf98f-168">Hello demande et réponse respecter le format de charge utile JSON tooa.</span><span class="sxs-lookup"><span data-stu-id="cf98f-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="cf98f-169">Pour plus d'informations, consultez [API de gestion des ressources Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf98f-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="cf98f-170">Langage du modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf98f-170">Resource Manager template language</span></span>
<span data-ttu-id="cf98f-171">Dans les ressources de toomanaging Ajout impérative (via API ou le Kit de développement logiciel), vous pouvez également utiliser un toobuild de style de programmation déclarative et gérer des ressources réseau à l’aide de hello langue du modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="cf98f-172">Un exemple de représentation d'un modèle est fourni ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cf98f-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="cf98f-173">modèle de Hello est essentiellement une description JSON des ressources de hello et des valeurs d’instance hello injectés via les paramètres définis.</span><span class="sxs-lookup"><span data-stu-id="cf98f-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="cf98f-174">exemple Hello ci-dessous peut être utilisé toocreate un réseau virtuel avec 2 sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="cf98f-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="cf98f-175">Vous pouvez hello fournissant des valeurs de paramètre hello manuellement lors de l’utilisation d’un modèle, ou vous pouvez utiliser un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="cf98f-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="cf98f-176">exemple Hello ci-dessous montre un ensemble possible de toobe de valeurs de paramètre utilisée avec le modèle hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="cf98f-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="cf98f-177">Hello principaux avantages de l’utilisation de modèles sont :</span><span class="sxs-lookup"><span data-stu-id="cf98f-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="cf98f-178">Vous pouvez créer dans un style déclaratif une infrastructure complexe dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="cf98f-179">Hello d’orchestration de la création de ressources hello, y compris la gestion des dépendances, est gérée par le Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="cf98f-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="cf98f-180">infrastructure de Hello peut être créé de manière reproductible dans diverses régions et dans une région en modifiant simplement les paramètres.</span><span class="sxs-lookup"><span data-stu-id="cf98f-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="cf98f-181">style déclaratif de Hello conduit tooshorter le délai de création de modèles de hello et déploiement d’une infrastructure de hello.</span><span class="sxs-lookup"><span data-stu-id="cf98f-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="cf98f-182">Pour obtenir des exemples de modèles, consultez [Modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="cf98f-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="cf98f-183">Pour plus d’informations sur hello langue du modèle de gestionnaire de ressources, consultez [langue de modèle de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cf98f-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="cf98f-184">Hello exemple de modèle ci-dessus utilise les réseaux virtuels hello et ressources de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="cf98f-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="cf98f-185">Il existe d'autres ressources réseau que vous pouvez utiliser, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cf98f-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="cf98f-186">Utilisation d’un modèle</span><span class="sxs-lookup"><span data-stu-id="cf98f-186">Using a template</span></span>
<span data-ttu-id="cf98f-187">Vous pouvez déployer tooAzure de services à partir d’un modèle à l’aide de PowerShell, AzureCLI, ou en effectuant un toodeploy cliquez sur à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf98f-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="cf98f-188">services toodeploy à partir d’un modèle dans GitHub, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf98f-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="cf98f-189">Ouvrez le fichier de template3 hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="cf98f-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="cf98f-190">Par exemple, ouvrez [Réseau virtuel avec deux sous-réseaux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="cf98f-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="cf98f-191">Cliquez sur **déployer tooAzure**, puis connectez-vous sur toohello portail Azure avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="cf98f-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="cf98f-192">Vérifier le modèle de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cf98f-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="cf98f-193">Cliquez sur **modifier les paramètres** et sélectionnez un emplacement, tel que *ouest des États-Unis*, pour les sous-réseaux et les réseaux de hello.</span><span class="sxs-lookup"><span data-stu-id="cf98f-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="cf98f-194">Si nécessaire, modifiez hello **ADDRESSPREFIX** et **SUBNETPREFIX** paramètres, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf98f-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="cf98f-195">Cliquez sur **sélectionner un groupe de ressources** , puis cliquez sur hello groupe ressources tooadd hello réseaux et les sous-réseaux à.</span><span class="sxs-lookup"><span data-stu-id="cf98f-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="cf98f-196">Vous pouvez également créer un nouveau groupe de ressources en cliquant sur **Ou créer un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="cf98f-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="cf98f-197">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cf98f-197">Click **Create**.</span></span> <span data-ttu-id="cf98f-198">Notez hello vignette affichage **déploiement d’un modèle de configuration**.</span><span class="sxs-lookup"><span data-stu-id="cf98f-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="cf98f-199">Une fois le déploiement de hello est terminé, vous verrez un écran semblable tooone ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cf98f-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Exemple de déploiement de modèle](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="cf98f-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf98f-201">Next steps</span></span>
[<span data-ttu-id="cf98f-202">Langue du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf98f-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="cf98f-203">Mise en réseau Azure : modèles couramment utilisés</span><span class="sxs-lookup"><span data-stu-id="cf98f-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="cf98f-204">Déploiement Azure Resource Manager et déploiement Classic</span><span class="sxs-lookup"><span data-stu-id="cf98f-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="cf98f-205">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cf98f-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

