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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="3b00b-103">VMSS Windows et Configuration d’état souhaité avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b00b-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="3b00b-104">Cet article décrit le modèle de gestionnaire de ressources hello pour hello [Gestionnaire d’extensions DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b00b-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="3b00b-105">Exemple de modèle pour une machine virtuelle sous Windows</span><span class="sxs-lookup"><span data-stu-id="3b00b-105">Template example for a Windows VM</span></span>
<span data-ttu-id="3b00b-106">Hello extrait de code suivant passe en hello section ressource de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-106">hello following snippet goes into hello Resource section of hello template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="3b00b-107">Exemple de modèle pour un VMSS Windows</span><span class="sxs-lookup"><span data-stu-id="3b00b-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="3b00b-108">Un nœud mise a une section « Propriétés » avec hello « VirtualMachineProfile », « extensionProfile » attribut.</span><span class="sxs-lookup"><span data-stu-id="3b00b-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="3b00b-109">L’extension Configuration d’état souhaité (DSC) est ajoutée sous « extensions ».</span><span class="sxs-lookup"><span data-stu-id="3b00b-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="3b00b-110">Informations détaillées sur les paramètres</span><span class="sxs-lookup"><span data-stu-id="3b00b-110">Detailed Settings Information</span></span>
<span data-ttu-id="3b00b-111">Bonjour schéma suivant est pour une partie des paramètres hello Hello extension Azure DSC dans un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b00b-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="3b00b-112">Détails</span><span class="sxs-lookup"><span data-stu-id="3b00b-112">Details</span></span>
| <span data-ttu-id="3b00b-113">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="3b00b-113">Property Name</span></span> | <span data-ttu-id="3b00b-114">Type</span><span class="sxs-lookup"><span data-stu-id="3b00b-114">Type</span></span> | <span data-ttu-id="3b00b-115">Description</span><span class="sxs-lookup"><span data-stu-id="3b00b-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b00b-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3b00b-116">settings.wmfVersion</span></span> |<span data-ttu-id="3b00b-117">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-117">string</span></span> |<span data-ttu-id="3b00b-118">Spécifie la version de hello de hello Windows Management Framework doit être installé sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b00b-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="3b00b-119">Définition de cette propriété too'latest' hello installe la version la plus à jour de WMF.</span><span class="sxs-lookup"><span data-stu-id="3b00b-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="3b00b-120">Hello uniquement actuel valeurs possibles pour cette propriété sont **« 4.0 », '5.0', ' 5.0PP' et 'latest'**.</span><span class="sxs-lookup"><span data-stu-id="3b00b-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="3b00b-121">Ces valeurs possibles sont tooupdates de sujet.</span><span class="sxs-lookup"><span data-stu-id="3b00b-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="3b00b-122">valeur par défaut de Hello est « dernier ».</span><span class="sxs-lookup"><span data-stu-id="3b00b-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="3b00b-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="3b00b-123">settings.configuration.url</span></span> |<span data-ttu-id="3b00b-124">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-124">string</span></span> |<span data-ttu-id="3b00b-125">Spécifie les emplacement de l’URL à partir de quels toodownload hello votre fichier zip de configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="3b00b-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="3b00b-126">Si l’URL hello fournie nécessite un jeton SAS pour l’accès, vous devez tooset hello protectedSettings.configurationUrlSasToken propriété toohello égal à votre jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="3b00b-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="3b00b-127">Cette propriété est requise si la propriété settings.configuration.script ou settings.configuration.function est définie.</span><span class="sxs-lookup"><span data-stu-id="3b00b-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="3b00b-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="3b00b-128">settings.configuration.script</span></span> |<span data-ttu-id="3b00b-129">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-129">string</span></span> |<span data-ttu-id="3b00b-130">Spécifie le nom du fichier de script hello qui contient la définition de votre configuration DSC de hello hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="3b00b-131">Ce script doit être dans le dossier racine de hello du fichier zip de hello téléchargé à partir de l’URL de hello spécifiée par la propriété configuration.url hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="3b00b-132">Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.script est définie.</span><span class="sxs-lookup"><span data-stu-id="3b00b-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="3b00b-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="3b00b-133">settings.configuration.function</span></span> |<span data-ttu-id="3b00b-134">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-134">string</span></span> |<span data-ttu-id="3b00b-135">Spécifie le nom hello de votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="3b00b-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="3b00b-136">configuration Hello nommée doit être contenue dans le script hello défini par configuration.script.</span><span class="sxs-lookup"><span data-stu-id="3b00b-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="3b00b-137">Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.function est définie.</span><span class="sxs-lookup"><span data-stu-id="3b00b-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="3b00b-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3b00b-138">settings.configurationArguments</span></span> |<span data-ttu-id="3b00b-139">Collection</span><span class="sxs-lookup"><span data-stu-id="3b00b-139">Collection</span></span> |<span data-ttu-id="3b00b-140">Définit tous les paramètres que vous souhaitez que la configuration de DSC toopass tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b00b-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="3b00b-141">Cette propriété n’est pas chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3b00b-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="3b00b-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="3b00b-142">settings.configurationData.url</span></span> |<span data-ttu-id="3b00b-143">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-143">string</span></span> |<span data-ttu-id="3b00b-144">Spécifie l’URL hello à partir de quels toodownload votre configuration (.psd1) du fichier de données toouse en tant qu’entrée pour votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="3b00b-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="3b00b-145">Si l’URL hello fournie nécessite un jeton SAS pour l’accès, vous devez tooset hello protectedSettings.configurationDataUrlSasToken propriété toohello égal à votre jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="3b00b-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="3b00b-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3b00b-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="3b00b-147">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-147">string</span></span> |<span data-ttu-id="3b00b-148">Active ou désactive la collecte télémétrique.</span><span class="sxs-lookup"><span data-stu-id="3b00b-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="3b00b-149">Hello uniquement les valeurs possibles pour cette propriété sont **'Activer', 'Désactiver', '', ou $null**.</span><span class="sxs-lookup"><span data-stu-id="3b00b-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="3b00b-150">Le fait de laisser cette propriété vide ou de la définir sur $null active la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="3b00b-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="3b00b-151">la valeur par défaut Hello est ''.</span><span class="sxs-lookup"><span data-stu-id="3b00b-151">hello default value is ''.</span></span> [<span data-ttu-id="3b00b-152">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="3b00b-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="3b00b-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3b00b-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="3b00b-154">Collection</span><span class="sxs-lookup"><span data-stu-id="3b00b-154">Collection</span></span> |<span data-ttu-id="3b00b-155">Définit d’autres emplacements à partir de quels toodownload hello WMF.</span><span class="sxs-lookup"><span data-stu-id="3b00b-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="3b00b-156">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="3b00b-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="3b00b-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3b00b-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="3b00b-158">Collection</span><span class="sxs-lookup"><span data-stu-id="3b00b-158">Collection</span></span> |<span data-ttu-id="3b00b-159">Définit tous les paramètres que vous souhaitez que la configuration de DSC toopass tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b00b-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="3b00b-160">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3b00b-160">This property is encrypted.</span></span> |
| <span data-ttu-id="3b00b-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3b00b-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="3b00b-162">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-162">string</span></span> |<span data-ttu-id="3b00b-163">Spécifie hello SAS tooaccess jeton hello URL définie par configuration.url.</span><span class="sxs-lookup"><span data-stu-id="3b00b-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="3b00b-164">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3b00b-164">This property is encrypted.</span></span> |
| <span data-ttu-id="3b00b-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3b00b-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="3b00b-166">string</span><span class="sxs-lookup"><span data-stu-id="3b00b-166">string</span></span> |<span data-ttu-id="3b00b-167">Spécifie hello SAS tooaccess jeton hello URL définie par configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="3b00b-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="3b00b-168">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3b00b-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="3b00b-169">settings vs protectedSettings</span><span class="sxs-lookup"><span data-stu-id="3b00b-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="3b00b-170">Tous les paramètres sont enregistrés dans un fichier texte de paramètres sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="3b00b-171">Propriétés sous « paramètres » sont des propriétés publiques, car elles ne sont pas chiffrées dans le fichier texte de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="3b00b-172">Propriétés de « protectedSettings » sont chiffrées avec un certificat et n’apparaissent pas en texte brut dans ce fichier sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3b00b-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="3b00b-173">Si la configuration de hello a besoin des informations d’identification, elles peuvent être incluses dans protectedSettings :</span><span class="sxs-lookup"><span data-stu-id="3b00b-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="3b00b-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="3b00b-174">Example</span></span>
<span data-ttu-id="3b00b-175">Hello suivant dérive hello « Getting Started » section hello [page de vue d’ensemble du Gestionnaire d’extensions DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b00b-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="3b00b-176">Cet exemple utilise des modèles de gestionnaire de ressources au lieu de l’extension de hello toodeploy applets de commande.</span><span class="sxs-lookup"><span data-stu-id="3b00b-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="3b00b-177">Enregistrer la configuration de « IisInstall.ps1 » hello, placez-le dans un. ZIP et télécharger des fichiers de hello dans une URL accessible.</span><span class="sxs-lookup"><span data-stu-id="3b00b-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="3b00b-178">Cet exemple utilise le stockage d’objets blob Azure, mais il est possible de toodownload. Fichiers ZIP à partir de n’importe quel emplacement arbitraire.</span><span class="sxs-lookup"><span data-stu-id="3b00b-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="3b00b-179">Dans le modèle de gestionnaire de ressources Azure hello, hello de code suivant indique le fichier approprié pour hello VM toodownload hello et exécuter une fonction PowerShell appropriée de hello :</span><span class="sxs-lookup"><span data-stu-id="3b00b-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

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

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="3b00b-180">Mise à jour à partir de hello Format antérieur</span><span class="sxs-lookup"><span data-stu-id="3b00b-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="3b00b-181">Tous les paramètres dans hello format antérieur (qui contient les propriétés publiques de hello ModulesUrl, ConfigurationFunction, SasToken ou propriétés) automatiquement adaptent le format actuel de toohello et s’exécuter comme avant.</span><span class="sxs-lookup"><span data-stu-id="3b00b-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="3b00b-182">Hello suivant le schéma est le schéma des paramètres précédents hello présentait :</span><span class="sxs-lookup"><span data-stu-id="3b00b-182">hello following schema is what hello previous settings schema looked like:</span></span>

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

<span data-ttu-id="3b00b-183">Voici comment le format précédent de hello adapte format actuel de toohello :</span><span class="sxs-lookup"><span data-stu-id="3b00b-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="3b00b-184">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="3b00b-184">Property Name</span></span> | <span data-ttu-id="3b00b-185">Équivalent dans le schéma précédent</span><span class="sxs-lookup"><span data-stu-id="3b00b-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="3b00b-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3b00b-186">settings.wmfVersion</span></span> |<span data-ttu-id="3b00b-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="3b00b-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="3b00b-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="3b00b-188">settings.configuration.url</span></span> |<span data-ttu-id="3b00b-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="3b00b-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="3b00b-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="3b00b-190">settings.configuration.script</span></span> |<span data-ttu-id="3b00b-191">Première partie de settings.ConfigurationFunction (avant « \\\\ »)</span><span class="sxs-lookup"><span data-stu-id="3b00b-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="3b00b-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="3b00b-192">settings.configuration.function</span></span> |<span data-ttu-id="3b00b-193">Deuxième partie de settings.ConfigurationFunction (après « \\\\ »)</span><span class="sxs-lookup"><span data-stu-id="3b00b-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="3b00b-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3b00b-194">settings.configurationArguments</span></span> |<span data-ttu-id="3b00b-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="3b00b-195">settings.Properties</span></span> |
| <span data-ttu-id="3b00b-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="3b00b-196">settings.configurationData.url</span></span> |<span data-ttu-id="3b00b-197">protectedSettings.DataBlobUri (sans jeton SAP)</span><span class="sxs-lookup"><span data-stu-id="3b00b-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="3b00b-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3b00b-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="3b00b-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="3b00b-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="3b00b-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3b00b-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="3b00b-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="3b00b-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="3b00b-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="3b00b-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="3b00b-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="3b00b-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="3b00b-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3b00b-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="3b00b-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="3b00b-205">settings.SasToken</span></span> |
| <span data-ttu-id="3b00b-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="3b00b-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="3b00b-207">Jeton SAP de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="3b00b-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="3b00b-208">Dépannage : code d’erreur 1100</span><span class="sxs-lookup"><span data-stu-id="3b00b-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="3b00b-209">Code d’erreur 1100 indique qu’il existe un problème avec hello extension de toohello DSC d’entrée d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3b00b-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="3b00b-210">texte Hello de ces erreurs est variable et peut changer.</span><span class="sxs-lookup"><span data-stu-id="3b00b-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="3b00b-211">Voici quelques-unes des erreurs hello que vous risquez de rencontrer et comment les résoudre.</span><span class="sxs-lookup"><span data-stu-id="3b00b-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="3b00b-212">Valeurs non valides</span><span class="sxs-lookup"><span data-stu-id="3b00b-212">Invalid Values</span></span>
<span data-ttu-id="3b00b-213">« Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3b00b-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="3b00b-214">Hello uniquement les valeurs possibles sont « 'Enable' et 'Disable' » « WmfVersion est '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3b00b-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="3b00b-215">Les seules valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b00b-215">Only possible values are …</span></span> <span data-ttu-id="3b00b-216">and ’latest’"</span><span class="sxs-lookup"><span data-stu-id="3b00b-216">and 'latest'"</span></span>

<span data-ttu-id="3b00b-217">Problème : Une valeur fournie n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="3b00b-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="3b00b-218">Solution : Définissez la valeur valide du tooa hello valeur non valide.</span><span class="sxs-lookup"><span data-stu-id="3b00b-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="3b00b-219">Consultez la table hello dans la section relative aux détails hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="3b00b-220">URL non valide</span><span class="sxs-lookup"><span data-stu-id="3b00b-220">Invalid URL</span></span>
<span data-ttu-id="3b00b-221">« ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3b00b-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="3b00b-222">This is not a valid URL » (configurationData.url est « {0} ». Il ne s’agit pas d’une URL valide.) « DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3b00b-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="3b00b-223">This is not a valid URL » (DataBlobUri est « {0} ». Il ne s’agit pas d’une URL valide.) « Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="3b00b-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="3b00b-224">This is not a valid URL » (configuration.url est « {0} ». Il ne s’agit pas d’une URL valide.)</span><span class="sxs-lookup"><span data-stu-id="3b00b-224">This is not a valid URL"</span></span>

<span data-ttu-id="3b00b-225">Problème : Une URL fournie n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="3b00b-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="3b00b-226">Solution : Vérifiez toutes les URL que vous avez fournies.</span><span class="sxs-lookup"><span data-stu-id="3b00b-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="3b00b-227">Assurez-vous que toutes les URL de résoudre les emplacements de toovalid extension de hello accessible sur l’ordinateur distant de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="3b00b-228">Type configurationArguments non valide</span><span class="sxs-lookup"><span data-stu-id="3b00b-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="3b00b-229">« Invalid configurationArguments type {0} » (Type configurationArguments {0} non valide)</span><span class="sxs-lookup"><span data-stu-id="3b00b-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="3b00b-230">Problème : hello ConfigurationArguments propriété ne peut pas résoudre les objets de table de hachage tooa.</span><span class="sxs-lookup"><span data-stu-id="3b00b-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="3b00b-231">Solution : Faites de votre propriété configurationArguments une table de hachage.</span><span class="sxs-lookup"><span data-stu-id="3b00b-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="3b00b-232">Suivez le format hello fourni dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="3b00b-233">Prenez garde aux guillemets, aux virgules et aux accolades.</span><span class="sxs-lookup"><span data-stu-id="3b00b-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="3b00b-234">Propriétés configurationArguments en double</span><span class="sxs-lookup"><span data-stu-id="3b00b-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="3b00b-235">« Found duplicate arguments '{0}' in both public and protected configurationArguments » (Arguments « {0} » en double trouvés dans les paramètres configurationArguments publics et protégés)</span><span class="sxs-lookup"><span data-stu-id="3b00b-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="3b00b-236">Problème : hello ConfigurationArguments dans paramètres publics et hello ConfigurationArguments dans les paramètres protégés contiennent des propriétés avec hello même nom.</span><span class="sxs-lookup"><span data-stu-id="3b00b-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="3b00b-237">Solution : Supprimez l’une des propriétés en double de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="3b00b-238">Propriétés manquantes</span><span class="sxs-lookup"><span data-stu-id="3b00b-238">Missing Properties</span></span>
<span data-ttu-id="3b00b-239">« Configuration.function requires that configuration.url or configuration.module is specified » (configuration.url ou configuration.module doit être spécifié pour configuration.function.)</span><span class="sxs-lookup"><span data-stu-id="3b00b-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="3b00b-240">« Configuration.url requires that configuration.script is specified » (configuration.script doit être spécifié pour configuration.url)</span><span class="sxs-lookup"><span data-stu-id="3b00b-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="3b00b-241">« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configuration.script)</span><span class="sxs-lookup"><span data-stu-id="3b00b-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="3b00b-242">« Configuration.url requires that configuration.function is specified » (configuration.function doit être spécifié pour configuration.url)</span><span class="sxs-lookup"><span data-stu-id="3b00b-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="3b00b-243">« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configurationUrlSasToken)</span><span class="sxs-lookup"><span data-stu-id="3b00b-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="3b00b-244">« ConfigurationDataUrlSasToken requires that configurationData.url is specified » (configurationData.url doit être spécifié pour configurationDataUrlSasToken)</span><span class="sxs-lookup"><span data-stu-id="3b00b-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="3b00b-245">Problème : Une propriété définie a besoin d’une autre propriété qui est manquante.</span><span class="sxs-lookup"><span data-stu-id="3b00b-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="3b00b-246">Solutions :</span><span class="sxs-lookup"><span data-stu-id="3b00b-246">Solutions:</span></span> 

* <span data-ttu-id="3b00b-247">Fournir la propriété manquante de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-247">Provide hello missing property.</span></span>
* <span data-ttu-id="3b00b-248">Supprimez la propriété hello nécessitant une propriété manquante de hello.</span><span class="sxs-lookup"><span data-stu-id="3b00b-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b00b-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b00b-249">Next Steps</span></span>
<span data-ttu-id="3b00b-250">En savoir plus sur DSC et l’échelle de machines virtuelles définit [à l’aide de Virtual Machine échelle définit par hello extensions Azure DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="3b00b-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="3b00b-251">En savoir plus sur la [Gestion des informations d’identification sécurisées de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b00b-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3b00b-252">Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b00b-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3b00b-253">Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="3b00b-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

