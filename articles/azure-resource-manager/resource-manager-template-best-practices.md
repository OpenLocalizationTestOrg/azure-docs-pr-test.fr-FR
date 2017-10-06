---
title: "pratiques aaaBest pour la création de modèles Resource Manager | Documents Microsoft"
description: "Instructions pour simplifier vos modèles Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>Bonnes pratiques relatives à la création de modèles Azure Resource Manager
Ces instructions peuvent vous aider à créer des modèles Azure Resource Manager sont toouse simple et fiable. instructions de Hello sont uniquement des suggestions. Il ne s’agit pas de spécifications requises, sauf indication contraire. Votre scénario peut nécessiter une variante de l’un des hello suivant des approches ou exemples.

## <a name="resource-names"></a>Noms de ressource
Il existe généralement trois types de noms de ressource avec lesquels vous travaillez dans Resource Manager :

* des noms de ressource qui doivent être uniques ;
* Les noms de ressources qui ne sont pas requis toobe unique, mais que vous choisissez un nom qui peut vous aider à identifier une ressource basée sur le contexte de tooprovide.
* des noms de ressources qui peuvent être génériques.

 Pour plus d’informations sur les restrictions de noms de ressource, consultez [Conventions d’affectation de noms recommandées pour les ressources Azure](../guidance/guidance-naming-conventions.md).

### <a name="unique-resource-names"></a>Noms de ressource uniques
Vous devez fournir un nom de ressource unique pour tout type de ressource disposant d’un point de terminaison d’accès aux données. Certains types de ressource courants nécessitent un nom unique, notamment :

* Azure Storage<sup>1</sup> 
* Fonctionnalité Web Apps d’Azure App Service
* SQL Server
* coffre de clés Azure
* Cache Redis Azure
* Azure Batch
* Azure Traffic Manager
* Recherche Azure
* Azure HDInsight

<sup>1</sup> Les noms de compte de stockage doivent être en minuscules, comporter 24 caractères au maximum et ne pas comprendre de traits d’union.

Si vous fournissez un paramètre pour un nom de ressource, vous devez fournir un nom unique lorsque vous déployez des ressources de hello. Si vous le souhaitez, vous pouvez créer une variable qui utilise hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nom de fonction. 

Vous pourrez également voulez tooadd un préfixe ou suffixe toohello **uniqueString** résultat. Nom unique des hello modification peut vous aider plus facilement identifier le type de ressource hello du nom de hello. Par exemple, vous pouvez générer un nom unique pour un compte de stockage à l’aide de hello suivant variable :

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>Noms de ressource pour l’identification
Certains types de ressources vous pourriez tooname, mais leurs noms n’ont pas toobe unique. Pour ces types de ressources, vous pouvez fournir un nom qui identifie le contexte de la ressource hello et type de ressource hello. Fournissez un nom descriptif qui vous permet d’identifier les ressources hello dans une liste de ressources. Si vous avez besoin d’un autre nom de ressource de différents déploiements de toouse, vous pouvez utiliser un paramètre pour le nom de hello :

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

Si vous n’avez pas besoin de toopass dans un nom de durant le déploiement, vous pouvez utiliser une variable : 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

Vous pouvez également utiliser une valeur codée en dur :

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>Noms de ressource génériques
Pour les types de ressources auxquels vous accédez principalement via une autre ressource, vous pouvez utiliser un nom générique qui est codé en dur dans le modèle de hello. Par exemple, vous pouvez définir un nom générique standard pour les règles de pare-feu sur un serveur SQL :

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>Paramètres
Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des paramètres :

* Réduisez l’utilisation des paramètres. Si possible, utilisez une variable ou une valeur littérale. Utilisez des paramètres uniquement pour les scénarios suivants :
   
   * Paramètres que vous souhaitez toouse les variations de selon tooenvironment (référence (SKU), taille, capacité).
   * Noms de ressources que vous souhaitez toospecify pour faciliter l’identification.
   * Valeurs que vous utilisez fréquemment toocomplete autres tâches (par exemple, un nom d’utilisateur admin).
   * les clés secrètes (notamment les mots de passe) ;
   * nombre de Hello ou tableau de valeurs toouse lorsque vous créez plusieurs instances d’un type de ressource.
* Utilisez la casse mixte pour les noms de paramètre.
* Fournissez une description de chaque paramètre dans les métadonnées de hello :

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* Définissez des valeurs par défaut pour les paramètres (à l’exception des mots de passe et des clés SSH) :
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* Utilisez **SecureString** pour tous les mots de passe et les clés secrètes : 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* Si possible, n’utilisez pas un emplacement de toospecify de paramètre. Au lieu de cela, utilisez hello **emplacement** propriété hello du groupe de ressources. À l’aide de hello **resourceGroup () .location** expression pour toutes vos ressources, les ressources dans le modèle de hello sont déployés dans hello même emplacement que le groupe de ressources hello :
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   Si un type de ressource est prise en charge uniquement un nombre limité d’emplacements, vous pourriez toospecify un emplacement valide directement dans le modèle de hello. Si vous devez utiliser un **emplacement** paramètre, partager cette valeur de paramètre autant que possible avec les ressources qui sont susceptibles de toobe Bonjour même emplacement. Cela réduit le nombre de hello de fois où les utilisateurs sont invités à tooprovide informations d’emplacement.
* Évitez d’utiliser un paramètre ou une variable pour la version de l’API hello pour un type de ressource. Les propriétés de ressource et les valeurs peuvent varier selon le numéro de version. IntelliSense dans un éditeur de code ne peut pas déterminer les schéma correct hello lorsque la valeur de version de l’API hello tooa paramètre ou une variable. Au lieu de cela, coder en dur hello version d’API dans le modèle de hello.

## <a name="variables"></a>variables
Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des variables :

* Utiliser des variables pour les valeurs que vous devez toouse plusieurs fois dans un modèle. Si une valeur est utilisée qu’une seule fois, une valeur codée en dur rend votre tooread plus facile de modèle.
* Vous ne pouvez pas utiliser hello [référence](resource-group-template-functions-resource.md#reference) fonction Bonjour **variables** section du modèle de hello. Hello **référence** fonction dérive sa valeur à partir de l’état d’exécution de la ressource hello. Toutefois, les variables sont résolus pendant hello initiale de l’analyse du modèle de hello. Construire des valeurs qui doivent hello **référence** fonction directement dans hello **ressources** ou **génère** section du modèle de hello.
* Incluez des variables pour les noms de ressource qui doivent être uniques, comme indiqué dans [Noms de ressources](#resource-names).
* Vous pouvez regrouper des variables dans des objets complexes. Hello d’utilisation **variable.subentry** tooreference une valeur à partir d’un objet complexe de format. Le regroupement de variables peut vous aider à effectuer le suivi des variables liées. Il améliore également la lisibilité du modèle de hello. Voici un exemple :
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > Un objet complexe ne peut pas contenir une expression qui fait référence à la valeur d’un objet complexe. Définissez une variable distincte à cette fin.
   > 
   > 
   
     Pour obtenir des exemples avancés de l’utilisation d’objets complexes en tant que variables, voir [Partage d’état dans les modèles Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="resources"></a>Ressources
Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des ressources :

* toohelp autres collaborateurs comprendre objectif hello de ressource de hello, spécifiez **commentaires** pour chaque ressource de modèle de hello :
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* Vous pouvez utiliser des balises tooadd métadonnées tooresources. Utiliser des informations de métadonnées tooadd sur vos ressources. Par exemple, vous pouvez ajouter des métadonnées toorecord détails sur la facturation pour une ressource. Pour plus d’informations, consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md).
* Si vous utilisez un *point de terminaison public* dans votre modèle (par exemple, un objet Blob d’Azure stockage public point de terminaison), *pas coder en dur* hello d’espace de noms. Hello d’utilisation **référence** fonction toodynamically récupérer l’espace de noms hello. Vous pouvez utiliser cet espace de noms public environnements d’approche toodeploy hello modèle toodifferent sans modifier manuellement le point de terminaison hello dans le modèle de hello. Définir hello API version toohello même version que vous utilisez pour le compte de stockage hello dans votre modèle :
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Si le compte de stockage hello est déployé dans hello même modèle que vous créez, vous n’avez pas besoin toospecify hello fournisseur espace de noms lorsque vous faites référence à des ressources de hello. Il s’agit de la syntaxe de hello simplifié :
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   Si vous avez d’autres valeurs dans votre modèle toouse configuré un espace de noms public, modifiez ces valeurs tooreflect hello même **référence** (fonction). Par exemple, vous pouvez définir hello **storageUri** propriété de profil de diagnostics de machine virtuelle hello :
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   Vous pouvez également référencer un compte de stockage existant dans un autre groupe de ressources :

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* Affecter publique virtuels tooa adresses IP uniquement quand une application requiert. tooconnect tooa ordinateur virtuel (VM) pour le débogage, ou de la gestion ou à des fins d’administration, utilisez les règles NAT entrantes, une passerelle de réseau virtuel ou un jumpbox.
   
     Pour plus d’informations sur la connexion toovirtual machines, consultez :
   
   * [Exécuter des machines virtuelles pour une architecture à plusieurs niveaux dans Azure](../guidance/guidance-compute-n-tier-vm.md)
   * [Configurer l’accès WinRM pour les machines virtuelles dans Azure Resource Manager](../virtual-machines/windows/winrm.md)
   * [Autoriser l’accès externe tooyour machine virtuelle à l’aide de hello portail Azure](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [Autoriser l’accès externe tooyour machine virtuelle à l’aide de PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [Autoriser l’accès externe tooyour Linux VM à l’aide de CLI d’Azure](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* Hello **domainNameLabel** propriété pour les adresses IP publiques doit être unique. Hello **domainNameLabel** valeur doit être comprise entre 3 et 63 caractères et suivre les règles de hello spécifiés par cette expression régulière : `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`. Étant donné que hello **uniqueString** fonction génère une chaîne qui est 13 caractères hello **dnsPrefixString** paramètre est limitée too50 caractères :

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* Lorsque vous ajoutez une extension de script personnalisé tooa mot de passe, utilisez hello **commandToExecute** propriété Bonjour **protectedSettings** propriété :
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > tooensure les clés secrètes sont chiffrés lorsqu’ils sont passés comme paramètres tooVMs et extensions, utilisez hello **protectedSettings** propriété des extensions de pertinentes hello.
   > 
   > 

## <a name="outputs"></a>outputs
Si vous utilisez un modèle toocreate des adresses IP publiques, inclure une **génère** section qui renvoie les détails de l’adresse IP de hello et nom de domaine complet de hello (FQDN). Vous pouvez utiliser la sortie valeurs tooeasily récupérer détails sur les adresses IP et les noms de domaine complets public après le déploiement. Lorsque vous référencez des ressources de hello, utilisez la version hello API que vous avez utilisé toocreate il : 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>Modèle unique ou modèles imbriqués
toodeploy votre solution, vous pouvez utiliser un modèle unique ou un modèle principal avec plusieurs modèles imbriqués. Les modèles imbriqués sont courants dans des scénarios plus avancés. À l’aide d’une offre de modèle imbriqué vous hello suivant avantages :

* Ils permettent de décomposer une solution en composants ciblés.
* Ils peuvent être réutilisés dans différents modèles principaux.

Si vous choisissez les modèles toouse imbriqué, hello suivant les recommandations peut vous aider à normaliser la conception de votre modèle. Ces instructions sont basées sur les [modèles pour la conception de modèles Azure Resource Manager](best-practices-resource-manager-design-templates.md). Nous vous recommandons une conception qui a hello suivant de modèles :

* **Modèle principal** (azuredeploy.json). À utiliser pour les paramètres d’entrée hello.
* **Modèle de ressource partagé**. Toodeploy d’utilisation des ressources qui utilisent de toutes les autres ressources partagées (par exemple, virtuel réseau et la disponibilité ensembles). Hello d’utilisation **dependsOn** tooensure expression que ce modèle est déployé avant les autres modèles.
* **Modèle de ressource facultatif**. Utilisez tooconditionally déployer les ressources basées sur un paramètre (par exemple, un jumpbox).
* **Modèle de ressource de membre**. Chaque type d’instance dans une couche application a sa propre configuration. Au sein d’un niveau, vous pouvez définir différents types d’instance. (Par exemple, hello première instance crée un cluster et des instances supplémentaires sont ajoutées cluster existant de toohello.) Chaque type d’instance a son propre modèle de déploiement.
* **Scripts**. Des scripts largement réutilisables sont applicables pour chaque type d’instance (par exemple, l’initialisation et le formatage de disques supplémentaires). Les scripts personnalisés que vous créez dans un but de personnalisation spécifiques sont différents, selon le type d’instance hello.

![Modèle imbriqué](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

Pour plus d’informations, voir [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).

## <a name="conditionally-link-toonested-templates"></a>Lier de manière conditionnelle toonested modèles
Vous pouvez utiliser un paramètre tooconditionally lien toonested des modèles. paramètre Hello devient partie intégrante de hello URI pour le modèle de hello :

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>Format de modèle
Il s’agit d’une bonne approche en matière toopass votre modèle via un validateur JSON. Un validateur peut vous aider à supprimer les virgules, parenthèses et crochets superflus susceptibles de provoquer une erreur lors du déploiement. Essayez [JSONlint](http://jsonlint.com/) ou un package de linter pour votre environnement d’édition favori (Visual Studio Code, Atom, Sublime Text, Visual Studio).

Il est également une bonne idée tooformat votre JSON pour une meilleure lisibilité. Vous pouvez utiliser un package de formatage JSON de votre éditeur local. Dans Visual Studio, le document de hello tooformat, appuyez sur **Ctrl + K, Ctrl + D**. Dans Visual Studio Code, appuyez sur **Alt + Maj + F**. Si votre éditeur local ne de format de document de hello, vous pouvez utiliser un [formateur en ligne](https://www.bing.com/search?q=json+formatter).

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des conseils sur la conception de votre solution pour des machines virtuelles, voir [Exécution d’une machine virtuelle Windows sur Azure](../guidance/guidance-compute-single-vm.md) et [Exécution d’une machine virtuelle Linux sur Azure](../guidance/guidance-compute-single-vm-linux.md).
* Pour des conseils sur la configuration d’un compte de stockage, voir [Liste de contrôle des performances et de l’extensibilité d’Azure Storage](../storage/common/storage-performance-checklist.md).
* toolearn sur comment une entreprise peut utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise : la gouvernance des abonnement](resource-manager-subscription-governance.md).

