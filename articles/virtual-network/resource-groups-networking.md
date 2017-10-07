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
# <a name="network-resource-provider"></a>Fournisseur de ressources réseau
Un besoin sous-jacente dans le succès d’une entreprise d’aujourd'hui, est hello toobuild de capacité et de gérer les applications prenant en charge du réseau à grande échelle d’une manière agile, souple, sécurisée et reproductible. Gestionnaire de ressources Azure permet de vous toocreate de telles applications, comme un ensemble unique de ressources dans les groupes de ressources. Ces ressources sont gérées via divers fournisseurs de ressources sous Resource Manager.

Le Gestionnaire de ressources Azure dépend de différents fournisseurs tooprovide accès tooyour ressources. Il existe trois fournisseurs de ressources principaux : réseau, stockage et calcul. Ce document décrit les caractéristiques de hello et les avantages de hello fournisseur de ressources réseau, y compris :

* **Métadonnées** – vous pouvez ajouter tooresources plus d’informations à l’aide de balises. Ces balises peuvent être utilisées tootrack l’utilisation des ressources entre les abonnements et les groupes de ressources.
* **Contrôle accru de votre réseau** : les ressources réseau sont faiblement couplées et vous pouvez les contrôler de manière plus précise. Cela signifie que vous avez plus de souplesse dans la gestion des ressources de mise en réseau hello.
* **Configuration plus rapide** : étant donné que les ressources réseau sont faiblement couplées, vous pouvez créer et organiser les ressources réseau en parallèle. Cela a considérablement réduit le temps de configuration.
* **Contrôle d’accès basé sur rôle** -RBAC fournit des rôles par défaut, avec une étendue de sécurité spécifique, dans la création de hello tooallowing Ajout de rôles personnalisés pour la gestion sécurisée.
* **Gestion plus facile et le déploiement** -il est plus facile toodeploy et gérer des applications car vous pouvez que vous pouvez créer une pile de l’ensemble de l’application comme une même collection de ressources dans un groupe de ressources. Et toodeploy plus rapide, étant donné que vous pouvez déployer en fournissant une charge utile JSON de modèle.
* **Personnalisation rapide** -vous pouvez utiliser la personnalisation de reproductibles et rapide de tooenable des déploiements de modèles de style déclaratif.
* **Personnalisation REPEATABLE** -vous pouvez utiliser la personnalisation de reproductibles et rapide de tooenable des déploiements de modèles de style déclaratif.
* **Interfaces de gestion** -vous pouvez utiliser des hello suivant interfaces toomanage vos ressources :
  * API REST
  * PowerShell
  * Kit de développement logiciel (SDK) .NET
  * Kit de développement logiciel (SDK) Node.JS
  * Kit de développement logiciel (SDK) Java
  * Interface de ligne de commande Azure
  * Portail en version préliminaire
  * Langage du modèle Resource Manager

## <a name="network-resources"></a>Ressources réseau
Vous pouvez désormais gérer les ressources réseau indépendamment, au lieu qu'elles soient toutes gérées via une ressource de calcul unique (un machine virtuelle). Cela garantit un degré de flexibilité et de souplesse plus élevé dans la composition d'une infrastructure complexe et à grande échelle dans un groupe de ressources.

Une vue conceptuelle d'un exemple de déploiement impliquant une application multicouche est présentée ci-dessous. Chaque ressource que vous voyez, par exemple, les cartes réseau, les adresses IP publiques et les machines virtuelles, peut être gérée indépendamment.

![Modèle de ressource réseau](./media/resource-groups-networking/Figure2.png)

Chaque ressource contient un ensemble commun de propriétés et son jeu de propriétés individuelles. Propriétés communes de Hello sont :

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **name** |Nom de ressource unique. Chaque type de ressource a ses propres restrictions d’affectation de noms. |PIP01, VM01, NIC01 |
| **location** |Région Azure dans le hello ressource réside |westus, eastus |
| **id** |Identification en fonction d’un URI unique |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Vous pouvez vérifier les propriétés individuelles de hello des ressources dans les sections hello ci-dessous.

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

## <a name="management-interfaces"></a>Interfaces de gestion
Vous pouvez gérer vos ressources de réseau Azure à l’aide de différentes interfaces. Dans ce document nous allons nous concentrer sur le dépannage de ces interfaces : API REST et modèles.

### <a name="rest-api"></a>API REST
Comme mentionné précédemment, les ressources réseau peuvent être gérées via une variété d'interfaces, notamment l'API REST, le Kit de développement logiciel (SDK) .NET, le Kit de développement logiciel (SDK) Node.JS, le Kit de développement logiciel (SDK) Java, PowerShell, l'interface en ligne de commande, le portail Azure et des modèles.

l’API Rest de Hello conforme toohello spécification du protocole HTTP 1.1. Hello URI structure générale de hello API est présentée ci-dessous :

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

Et les paramètres de hello entre accolades représentent hello suivant d’éléments :

* **subscription-id** : ID de votre abonnement Azure.
* **Resource-provider-namespace** -espace de noms de fournisseur hello utilisé. la valeur de fournisseur de ressources réseau hello Hello est *Microsoft.Network*.
* **nom de la région** -nom de la région Azure hello

Hello méthodes HTTP suivantes sont prises en charge lors de l’établissement des appels toohello API REST :

* **PUT** - utilisés toocreate une ressource d’un type donné, modifier une propriété de ressource ou une association entre les ressources.
* **OBTENIR** -utilisé tooretrieve informations pour une ressource mis en service.
* **SUPPRIMER** -utilisé toodelete une ressource existante.

Hello demande et réponse respecter le format de charge utile JSON tooa. Pour plus d'informations, consultez [API de gestion des ressources Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Langage du modèle Resource Manager
Dans les ressources de toomanaging Ajout impérative (via API ou le Kit de développement logiciel), vous pouvez également utiliser un toobuild de style de programmation déclarative et gérer des ressources réseau à l’aide de hello langue du modèle de gestionnaire de ressources.

Un exemple de représentation d'un modèle est fourni ci-dessous :

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

modèle de Hello est essentiellement une description JSON des ressources de hello et des valeurs d’instance hello injectés via les paramètres définis. exemple Hello ci-dessous peut être utilisé toocreate un réseau virtuel avec 2 sous-réseaux.

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

Vous pouvez hello fournissant des valeurs de paramètre hello manuellement lors de l’utilisation d’un modèle, ou vous pouvez utiliser un fichier de paramètres. exemple Hello ci-dessous montre un ensemble possible de toobe de valeurs de paramètre utilisée avec le modèle hello ci-dessus :

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


Hello principaux avantages de l’utilisation de modèles sont :

* Vous pouvez créer dans un style déclaratif une infrastructure complexe dans un groupe de ressources. Hello d’orchestration de la création de ressources hello, y compris la gestion des dépendances, est gérée par le Gestionnaire de ressources.
* infrastructure de Hello peut être créé de manière reproductible dans diverses régions et dans une région en modifiant simplement les paramètres.
* style déclaratif de Hello conduit tooshorter le délai de création de modèles de hello et déploiement d’une infrastructure de hello.

Pour obtenir des exemples de modèles, consultez [Modèles de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates).

Pour plus d’informations sur hello langue du modèle de gestionnaire de ressources, consultez [langue de modèle de gestionnaire de ressources Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Hello exemple de modèle ci-dessus utilise les réseaux virtuels hello et ressources de sous-réseau. Il existe d'autres ressources réseau que vous pouvez utiliser, comme indiqué ci-dessous :

### <a name="using-a-template"></a>Utilisation d’un modèle
Vous pouvez déployer tooAzure de services à partir d’un modèle à l’aide de PowerShell, AzureCLI, ou en effectuant un toodeploy cliquez sur à partir de GitHub. services toodeploy à partir d’un modèle dans GitHub, exécutez hello comme suit :

1. Ouvrez le fichier de template3 hello à partir de GitHub. Par exemple, ouvrez [Réseau virtuel avec deux sous-réseaux](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Cliquez sur **déployer tooAzure**, puis connectez-vous sur toohello portail Azure avec vos informations d’identification.
3. Vérifier le modèle de hello, puis cliquez sur **enregistrer**.
4. Cliquez sur **modifier les paramètres** et sélectionnez un emplacement, tel que *ouest des États-Unis*, pour les sous-réseaux et les réseaux de hello.
5. Si nécessaire, modifiez hello **ADDRESSPREFIX** et **SUBNETPREFIX** paramètres, puis cliquez sur **OK**.
6. Cliquez sur **sélectionner un groupe de ressources** , puis cliquez sur hello groupe ressources tooadd hello réseaux et les sous-réseaux à. Vous pouvez également créer un nouveau groupe de ressources en cliquant sur **Ou créer un nouveau**.
7. Cliquez sur **Créer**. Notez hello vignette affichage **déploiement d’un modèle de configuration**. Une fois le déploiement de hello est terminé, vous verrez un écran semblable tooone ci-dessous.

![Exemple de déploiement de modèle](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Étapes suivantes
[Langue du modèle Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)

[Mise en réseau Azure : modèles couramment utilisés](https://github.com/Azure/azure-quickstart-templates)

[Déploiement Azure Resource Manager et déploiement Classic](../azure-resource-manager/resource-manager-deployment-model.md)

[Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

