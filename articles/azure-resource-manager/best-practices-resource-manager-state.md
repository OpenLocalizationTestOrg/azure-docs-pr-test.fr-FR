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
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a>Tooand d’état de partage à partir de modèles Azure Resource Manager
Cette rubrique présente les bonnes pratiques pour gérer et partager l’état dans les modèles. Hello paramètres et des variables dans cette rubrique sont des exemples de type hello d’objets que vous pouvez définir tooconveniently organiser vos exigences de déploiement. À partir de ces exemples, vous pouvez implémenter vos propres objets avec les valeurs de propriété pertinentes pour votre environnement.

Cette rubrique fait partie d’un livre blanc plus volumineux. hello tooread complète papier, téléchargez [World classe ressource Gestionnaire de modèles et éprouvée méthodes conseillées](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).

## <a name="provide-standard-configuration-settings"></a>Fournir les paramètres de configuration standard
Au lieu de proposer un modèle qui fournit une flexibilité totale et nombreuses variations, un modèle commun est tooprovide une sélection de configurations connues. En effet, les utilisateurs peuvent sélectionner des tailles de t-shirt standard comme enfant, petite, moyenne et grande. Les autres exemples de taille standard sont des offres de produits, telles que l’édition Community ou Enterprise. Dans d’autres cas, il peut s’agir de configurations d’une technologie propres à une charge de travail, par exemple MapReduce ou sans SQL.

Avec les objets complexes, vous pouvez créer des variables qui contiennent des collections de données, parfois appelées « conteneurs de propriétés » et utiliser cette déclaration de ressource données toodrive hello dans votre modèle. Cette approche fournit des configurations correctes, connues de différentes tailles qui sont préconfigurées pour les clients. Sans des configurations connues, les utilisateurs du modèle de hello doivent déterminer la taille de cluster sur leur propre facteur de contraintes de ressources de plateforme et faire mathématiques tooidentify hello résultant partitionnement des comptes de stockage et d’autres ressources (en raison de la taille de toocluster et contraintes de ressources). En outre toomaking une meilleure expérience client de hello, quelques configurations connues toosupport plus facile et peuvent vous aider à assurer un haut niveau de densité.

Hello suivant montre l’exemple de comment toodefine les variables qui contiennent les objets complexes pour représenter des collections de données. collections de Hello définissent les valeurs qui sont utilisées pour la taille de machine virtuelle, les paramètres réseau, les paramètres de système d’exploitation et les paramètres de disponibilité.

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

Notez que hello **tshirtSize** variable concatène une taille de t-shirt hello fourni via un paramètre (**petit**, **support**, **grande**) toohello texte **tshirtSize**. Vous utilisez cette variable objet complexe associé de hello tooretrieve variable pour cette taille de t-shirt.

Vous pouvez ensuite référencer ces variables plus loin dans le modèle de hello. Hello tooreference possibilité nommé-variables et leurs propriétés simplifie la syntaxe de modèle hello et rend facile toounderstand contexte. Hello, l’exemple suivant définit un toodeploy de ressources à l’aide d’objets hello illustrés précédemment tooset valeurs. Par exemple, hello taille de machine virtuelle est définie en récupérant la valeur hello pour `variables('tshirtSize').vmSize` tandis que la valeur de hello pour la taille du disque hello est récupéré à partir de `variables('tshirtSize').diskSize`. En outre, hello URI pour un modèle lié est défini avec la valeur hello pour `variables('tshirtSize').vmTemplate`.

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

## <a name="pass-state-tooa-template"></a>Passez le modèle d’état tooa
Vous pouvez partager l’état dans un modèle via les paramètres que vous fournissez directement pendant le déploiement.

Hello table des paramètres de listes couramment utilisées dans les modèles suivants.

| Nom | Valeur | Description |
| --- | --- | --- |
| location |Chaîne obtenue à partir d’une liste contrainte des régions Azure |emplacement Hello où vous déployez des ressources de hello. |
| storageAccountNamePrefix |String |Nom DNS unique pour hello compte de stockage où sont placés les disques de l’ordinateur virtuel hello |
| domainName |String |Nom de domaine de hello accessible publiquement jumpbox machine virtuelle dans un format de hello : **{domainName}. {} emplacement}.cloudapp.com** par exemple : **mydomainname.westus.cloudapp.azure.com** |
| adminUsername |String |Nom d’utilisateur pour hello machines virtuelles |
| adminPassword |String |Mot de passe pour hello machines virtuelles |
| tshirtSize |Chaîne obtenue à partir d’une liste contrainte des propositions de tailles de t-shirt |Hello nommé tooprovision de taille d’unité mise à l’échelle. Par exemple, « Petit », « Moyen », « Grand » |
| virtualNetworkName |String |Nom de réseau virtuel hello hello consommateur souhaite toouse. |
| enableJumpbox |Chaîne obtenue à partir d’une liste contrainte (activée/désactivée) |Paramètre qui identifie si tooenable un jumpbox pour l’environnement de hello. Valeurs : « activée », « désactivée » |

Hello **tshirtSize** paramètre utilisé dans la section précédente de hello est défini en tant que :

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


## <a name="pass-state-toolinked-templates"></a>Passer des modèles de toolinked d’état
Lors de la connexion toolinked modèles, vous souvent utilisez un mélange de static et généré des variables.

### <a name="static-variables"></a>Variables statiques
Les variables statiques sont souvent des valeurs de base tooprovide utilisées, telles que les URL, qui sont utilisés dans un modèle.

Bonjour suivant extrait du modèle, `templateBaseUrl` Spécifie l’emplacement racine du hello pour le modèle de hello dans GitHub. ligne suivante de Hello génère une nouvelle variable `sharedTemplateUrl` qui concatène hello les URL de base avec le nom connu de hello du modèle de ressources partagées hello. Sous cette ligne, une variable objet complexe toostore utilisé une taille de t-shirt, où est URL de base hello toohello concaténée connu d’emplacement de modèle de configuration et stockées dans hello `vmTemplate` propriété.

avantage Hello de cette approche est que si l’emplacement du modèle hello change, vous devez uniquement variable statique de hello toochange dans un seul endroit, ce qui se passe dans l’ensemble de modèles de hello lié.

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

### <a name="generated-variables"></a>Variables générées
Dans les variables toostatic de plus, plusieurs variables sont générées dynamiquement. Cette section répertorie quelques-uns des types courants de hello de variables générés.

#### <a name="tshirtsize"></a>tshirtSize
Vous êtes familiarisé avec cette variable générée à partir d’exemples hello ci-dessus.

#### <a name="networksettings"></a>networkSettings
Un Bonjour de capacité, fonctionnalité ou le modèle de solution avec étendue de bout en bout, modèles liés créent généralement des ressources qui existent sur un réseau. Une approche simple est toouse paramètres réseau toostore objet complexe et les passer toolinked modèles.

Un exemple de paramètres de réseau de communication est affiché ci-dessous.

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

#### <a name="availabilitysettings"></a>availabilitySettings
Les ressources créées dans des modèles liés sont souvent placées dans un groupe à haute disponibilité. Dans l’exemple suivant de hello, nom du jeu de disponibilité hello est spécifié et également hello domaine d’erreur et toouse de compte de domaine de mise à jour.

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

Si vous avez besoin de plusieurs groupes à haute disponibilité (par exemple, un pour les nœuds principaux) et l’autre pour les nœuds de données, vous pouvez utiliser un nom en tant que préfixe, spécifiez plusieurs ensembles de disponibilité ou de suivre le modèle hello indiquée précédemment pour créer une variable pour une taille de t-shirt spécifique.

#### <a name="storagesettings"></a>storageSettings
Les détails du stockage sont souvent partagés avec les modèles liés. Dans l’exemple hello ci-dessous, un *storageSettings* objet fournit des détails sur hello les noms de compte et conteneur de stockage.

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a>osSettings
Avec les modèles liés, vous devrez peut-être toopass les types de nœuds de toovarious paramètres de système d’exploitation sur les types de configuration connu différente. Un objet complexe est un moyen simple toostore et partage de système d’exploitation et le rend également toosupport plus facilement plusieurs choix de système d’exploitation pour le déploiement.

Hello suivant montre un objet pour *osSettings*:

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a>machineSettings
Une variable générée, *machineSettings* est un objet complexe contenant un mélange de variables de base pour la création d’une machine virtuelle. les variables Hello incluent une référence d’image de système d’exploitation, nom d’utilisateur administrateur et un mot de passe et un préfixe pour les noms de machine virtuelle hello.

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

Notez que *osImageReference* récupère hello des valeurs à partir de hello *osSettings* variable définie dans les modèles principal hello. Cela signifie que vous pouvez facilement modifier le système d’exploitation de hello pour une machine virtuelle — totalement ou selon la préférence hello d’un consommateur de modèle.

#### <a name="vmscripts"></a>vmScripts
Hello *vmScripts* de l’objet contient des détails sur toodownload de scripts hello et d’exécution sur une instance de machine virtuelle, y compris les références externes et internes. En dehors de références incluent les infrastructure hello.
Les références à l’intérieur incluent la configuration et les logiciels installé de hello installé.

Vous utilisez hello *scriptsToDownload* hello toolist de propriété scripts toodownload toohello machine virtuelle. Cet objet contient également des références des arguments de ligne toocommand pour différents types d’actions. Ces actions incluent l’exécution d’installation par défaut de hello pour chaque nœud, une installation qui s’exécute après que tous les nœuds sont déployés et des scripts supplémentaires qui peuvent être spécifique tooa donné du modèle.

Cet exemple fait à partir d’un modèle utilisé de toodeploy MongoDB, qui requiert une arbitre toodeliver une haute disponibilité. Hello *arbiterNodeInstallCommand* a été ajouté trop*vmScripts* tooinstall l’arbitre hello.

section de variables Hello est où trouver des variables hello qui définissent le script de hello tooexecute hello un texte spécifique avec les valeurs appropriées de hello.

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a>Retourner l’état à partir d’un modèle
Non seulement peuvent passer des données dans un modèle, vous pouvez également un modèle de partage de données toohello précédent appel. Bonjour **génère** section d’un modèle lié, vous pouvez fournir des paires clé/valeur qui peuvent être consommés par le modèle de source de hello.

Hello suivant montre comment toopass hello adresse IP privée générée dans un modèle lié.

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

Dans le modèle principal de hello, vous pouvez utiliser ces données avec la syntaxe de hello :

    "[reference('master-node').outputs.masterip.value]"

Vous pouvez utiliser cette expression dans hello sorties soit hello ressources de modèle principal de hello. Impossible d’utiliser expression de hello dans la section des variables hello, car il s’appuie sur l’état d’exécution hello. tooreturn cette valeur à partir du modèle principal hello, utilisez :

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

Pour obtenir un exemple d’utilisation de hello génère section un modèle lié tooreturn de disques de données pour un ordinateur virtuel, consultez [création de plusieurs disques de données pour un ordinateur virtuel](resource-group-create-multiple.md).

## <a name="define-authentication-settings-for-virtual-machine"></a>Définir les paramètres d’authentification d’une machine virtuelle
Vous pouvez utiliser hello même modèle indiqué précédemment pour les paramètres d’authentification hello des toospecify de paramètres de configuration pour un ordinateur virtuel. Vous créez un paramètre pour passer de type hello d’authentification.

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

Vous ajoutez des variables pour hello différents types d’authentification et une variable toostore que le type est utilisé pour ce déploiement basé sur la valeur hello du paramètre hello.

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

Lorsque vous définissez l’ordinateur virtuel de hello, vous définissez hello **osProfile** variable toohello vous avez créée.

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les sections hello hello du modèle de, consultez [de création de modèles de gestionnaire de ressources Azure](resource-group-authoring-templates.md)
* les fonctions hello toosee qui sont disponibles dans un modèle, consultez [fonctions de modèle de gestionnaire de ressources Azure](resource-group-template-functions.md)
