---
title: "Modèle de gestionnaire de ressources de Configuration d’état d’aaaDesired | Documents Microsoft"
description: "Définition du modèle Resource Manager pour la configuration d’état souhaité dans Azure avec des exemples et informations pour la résolution des problèmes"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>VMSS Windows et Configuration d’état souhaité avec des modèles Azure Resource Manager
Cet article décrit le modèle de gestionnaire de ressources hello pour hello [Gestionnaire d’extensions DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Exemple de modèle pour une machine virtuelle sous Windows
Hello extrait de code suivant passe en hello section ressource de modèle de hello.

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a>Exemple de modèle pour un VMSS Windows
Un nœud mise a une section « Propriétés » avec hello « VirtualMachineProfile », « extensionProfile » attribut. L’extension Configuration d’état souhaité (DSC) est ajoutée sous « extensions ». 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a>Informations détaillées sur les paramètres
Bonjour schéma suivant est pour une partie des paramètres hello Hello extension Azure DSC dans un modèle Azure Resource Manager.

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a>Détails
| Nom de la propriété | Type | Description |
| --- | --- | --- |
| settings.wmfVersion |string |Spécifie la version de hello de hello Windows Management Framework doit être installé sur votre machine virtuelle. Définition de cette propriété too'latest' hello installe la version la plus à jour de WMF. Hello uniquement actuel valeurs possibles pour cette propriété sont **« 4.0 », '5.0', ' 5.0PP' et 'latest'**. Ces valeurs possibles sont tooupdates de sujet. valeur par défaut de Hello est « dernier ». |
| settings.configuration.url |string |Spécifie les emplacement de l’URL à partir de quels toodownload hello votre fichier zip de configuration DSC. Si l’URL hello fournie nécessite un jeton SAS pour l’accès, vous devez tooset hello protectedSettings.configurationUrlSasToken propriété toohello égal à votre jeton SAP. Cette propriété est requise si la propriété settings.configuration.script ou settings.configuration.function est définie. |
| settings.configuration.script |string |Spécifie le nom du fichier de script hello qui contient la définition de votre configuration DSC de hello hello. Ce script doit être dans le dossier racine de hello du fichier zip de hello téléchargé à partir de l’URL de hello spécifiée par la propriété configuration.url hello. Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.script est définie. |
| settings.configuration.function |string |Spécifie le nom hello de votre configuration DSC. configuration Hello nommée doit être contenue dans le script hello défini par configuration.script. Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.function est définie. |
| settings.configurationArguments |Collection |Définit tous les paramètres que vous souhaitez que la configuration de DSC toopass tooyour. Cette propriété n’est pas chiffrée. |
| settings.configurationData.url |string |Spécifie l’URL hello à partir de quels toodownload votre configuration (.psd1) du fichier de données toouse en tant qu’entrée pour votre configuration DSC. Si l’URL hello fournie nécessite un jeton SAS pour l’accès, vous devez tooset hello protectedSettings.configurationDataUrlSasToken propriété toohello égal à votre jeton SAP. |
| settings.privacy.dataEnabled |string |Active ou désactive la collecte télémétrique. Hello uniquement les valeurs possibles pour cette propriété sont **'Activer', 'Désactiver', '', ou $null**. Le fait de laisser cette propriété vide ou de la définir sur $null active la télémétrie. la valeur par défaut Hello est ''. [Plus d’informations](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Collection |Définit d’autres emplacements à partir de quels toodownload hello WMF. [Plus d’informations](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Collection |Définit tous les paramètres que vous souhaitez que la configuration de DSC toopass tooyour. Cette propriété est chiffrée. |
| protectedSettings.configurationUrlSasToken |string |Spécifie hello SAS tooaccess jeton hello URL définie par configuration.url. Cette propriété est chiffrée. |
| protectedSettings.configurationDataUrlSasToken |string |Spécifie hello SAS tooaccess jeton hello URL définie par configurationData.url. Cette propriété est chiffrée. |

## <a name="settings-vs-protectedsettings"></a>settings vs protectedSettings
Tous les paramètres sont enregistrés dans un fichier texte de paramètres sur la machine virtuelle de hello.
Propriétés sous « paramètres » sont des propriétés publiques, car elles ne sont pas chiffrées dans le fichier texte de paramètres hello.
Propriétés de « protectedSettings » sont chiffrées avec un certificat et n’apparaissent pas en texte brut dans ce fichier sur hello machine virtuelle.

Si la configuration de hello a besoin des informations d’identification, elles peuvent être incluses dans protectedSettings :

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a>Exemple
Hello suivant dérive hello « Getting Started » section hello [page de vue d’ensemble du Gestionnaire d’extensions DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Cet exemple utilise des modèles de gestionnaire de ressources au lieu de l’extension de hello toodeploy applets de commande. Enregistrer la configuration de « IisInstall.ps1 » hello, placez-le dans un. ZIP et télécharger des fichiers de hello dans une URL accessible. Cet exemple utilise le stockage d’objets blob Azure, mais il est possible de toodownload. Fichiers ZIP à partir de n’importe quel emplacement arbitraire.

Dans le modèle de gestionnaire de ressources Azure hello, hello de code suivant indique le fichier approprié pour hello VM toodownload hello et exécuter une fonction PowerShell appropriée de hello :

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a>Mise à jour à partir de hello Format antérieur
Tous les paramètres dans hello format antérieur (qui contient les propriétés publiques de hello ModulesUrl, ConfigurationFunction, SasToken ou propriétés) automatiquement adaptent le format actuel de toohello et s’exécuter comme avant.

Hello suivant le schéma est le schéma des paramètres précédents hello présentait :

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

Voici comment le format précédent de hello adapte format actuel de toohello :

| Nom de la propriété | Équivalent dans le schéma précédent |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |Première partie de settings.ConfigurationFunction (avant « \\\\ ») |
| settings.configuration.function |Deuxième partie de settings.ConfigurationFunction (après « \\\\ ») |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (sans jeton SAP) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |Jeton SAP de protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Dépannage : code d’erreur 1100
Code d’erreur 1100 indique qu’il existe un problème avec hello extension de toohello DSC d’entrée d’utilisateur.
texte Hello de ces erreurs est variable et peut changer.
Voici quelques-unes des erreurs hello que vous risquez de rencontrer et comment les résoudre.

### <a name="invalid-values"></a>Valeurs non valides
« Privacy.dataCollection is '{0}'. Hello uniquement les valeurs possibles sont « 'Enable' et 'Disable' » « WmfVersion est '{0}'. Les seules valeurs possibles sont les suivantes : and ’latest’"

Problème : Une valeur fournie n’est pas autorisée.

Solution : Définissez la valeur valide du tooa hello valeur non valide. Consultez la table hello dans la section relative aux détails hello.

### <a name="invalid-url"></a>URL non valide
« ConfigurationData.url is '{0}'. This is not a valid URL » (configurationData.url est « {0} ». Il ne s’agit pas d’une URL valide.) « DataBlobUri is '{0}'. This is not a valid URL » (DataBlobUri est « {0} ». Il ne s’agit pas d’une URL valide.) « Configuration.url is '{0}'. This is not a valid URL » (configuration.url est « {0} ». Il ne s’agit pas d’une URL valide.)

Problème : Une URL fournie n’est pas valide.

Solution : Vérifiez toutes les URL que vous avez fournies. Assurez-vous que toutes les URL de résoudre les emplacements de toovalid extension de hello accessible sur l’ordinateur distant de hello.

### <a name="invalid-configurationargument-type"></a>Type configurationArguments non valide
« Invalid configurationArguments type {0} » (Type configurationArguments {0} non valide)

Problème : hello ConfigurationArguments propriété ne peut pas résoudre les objets de table de hachage tooa. 

Solution : Faites de votre propriété configurationArguments une table de hachage. Suivez le format hello fourni dans l’exemple précédent de hello. Prenez garde aux guillemets, aux virgules et aux accolades.

### <a name="duplicate-configurationarguments"></a>Propriétés configurationArguments en double
« Found duplicate arguments '{0}' in both public and protected configurationArguments » (Arguments « {0} » en double trouvés dans les paramètres configurationArguments publics et protégés)

Problème : hello ConfigurationArguments dans paramètres publics et hello ConfigurationArguments dans les paramètres protégés contiennent des propriétés avec hello même nom.

Solution : Supprimez l’une des propriétés en double de hello.

### <a name="missing-properties"></a>Propriétés manquantes
« Configuration.function requires that configuration.url or configuration.module is specified » (configuration.url ou configuration.module doit être spécifié pour configuration.function.)

« Configuration.url requires that configuration.script is specified » (configuration.script doit être spécifié pour configuration.url)

« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configuration.script)

« Configuration.url requires that configuration.function is specified » (configuration.function doit être spécifié pour configuration.url)

« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configurationUrlSasToken)

« ConfigurationDataUrlSasToken requires that configurationData.url is specified » (configurationData.url doit être spécifié pour configurationDataUrlSasToken)

Problème : Une propriété définie a besoin d’une autre propriété qui est manquante.

Solutions : 

* Fournir la propriété manquante de hello.
* Supprimez la propriété hello nécessitant une propriété manquante de hello.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur DSC et l’échelle de machines virtuelles définit [à l’aide de Virtual Machine échelle définit par hello extensions Azure DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

En savoir plus sur la [Gestion des informations d’identification sécurisées de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

