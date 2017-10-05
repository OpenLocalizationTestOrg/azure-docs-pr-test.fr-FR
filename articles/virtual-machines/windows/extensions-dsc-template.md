---
title: "Modèle Resource Manager de configuration d’état souhaité | Microsoft Docs"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="48a70-103">VMSS Windows et Configuration d’état souhaité avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48a70-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="48a70-104">Cet article décrit le modèle Resource Manager destiné au [gestionnaire de l’extension Configuration d’état souhaité](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48a70-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="48a70-105">Exemple de modèle pour une machine virtuelle sous Windows</span><span class="sxs-lookup"><span data-stu-id="48a70-105">Template example for a Windows VM</span></span>
<span data-ttu-id="48a70-106">L’extrait de code suivant va dans la section « Resource » du modèle.</span><span class="sxs-lookup"><span data-stu-id="48a70-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="48a70-107">Exemple de modèle pour un VMSS Windows</span><span class="sxs-lookup"><span data-stu-id="48a70-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="48a70-108">Un nœud VMSS comporte une section « properties » avec l’attribut « VirtualMachineProfile », « extensionProfile ».</span><span class="sxs-lookup"><span data-stu-id="48a70-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="48a70-109">L’extension Configuration d’état souhaité (DSC) est ajoutée sous « extensions ».</span><span class="sxs-lookup"><span data-stu-id="48a70-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="48a70-110">Informations détaillées sur les paramètres</span><span class="sxs-lookup"><span data-stu-id="48a70-110">Detailed Settings Information</span></span>
<span data-ttu-id="48a70-111">Voici le schéma pour la section « settings » des paramètres de l’extension DSC Azure dans un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48a70-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="48a70-112">Détails</span><span class="sxs-lookup"><span data-stu-id="48a70-112">Details</span></span>
| <span data-ttu-id="48a70-113">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="48a70-113">Property Name</span></span> | <span data-ttu-id="48a70-114">Type</span><span class="sxs-lookup"><span data-stu-id="48a70-114">Type</span></span> | <span data-ttu-id="48a70-115">Description</span><span class="sxs-lookup"><span data-stu-id="48a70-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48a70-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="48a70-116">settings.wmfVersion</span></span> |<span data-ttu-id="48a70-117">string</span><span class="sxs-lookup"><span data-stu-id="48a70-117">string</span></span> |<span data-ttu-id="48a70-118">Spécifie la version de Windows Management Framework qui doit être installée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48a70-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="48a70-119">Lorsque cette propriété est définie sur « latest », la dernière version de WMF est installée.</span><span class="sxs-lookup"><span data-stu-id="48a70-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="48a70-120">Les seules valeurs possibles actuellement pour cette propriété sont **4.0 », « 5.0 », « 5.0PP », and « latest »**.</span><span class="sxs-lookup"><span data-stu-id="48a70-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="48a70-121">Les valeurs possibles font l’objet de mises à jour.</span><span class="sxs-lookup"><span data-stu-id="48a70-121">These possible values are subject to updates.</span></span> <span data-ttu-id="48a70-122">La valeur par défaut est « latest ».</span><span class="sxs-lookup"><span data-stu-id="48a70-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="48a70-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="48a70-123">settings.configuration.url</span></span> |<span data-ttu-id="48a70-124">string</span><span class="sxs-lookup"><span data-stu-id="48a70-124">string</span></span> |<span data-ttu-id="48a70-125">Spécifie l’adresse URL de téléchargement de votre fichier .zip de configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="48a70-126">Si l’accès à l’URL fournie nécessite un jeton SAP, vous devez définir la propriété protectedSettings.configurationUrlSasToken sur la valeur du jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="48a70-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="48a70-127">Cette propriété est requise si la propriété settings.configuration.script ou settings.configuration.function est définie.</span><span class="sxs-lookup"><span data-stu-id="48a70-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="48a70-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="48a70-128">settings.configuration.script</span></span> |<span data-ttu-id="48a70-129">string</span><span class="sxs-lookup"><span data-stu-id="48a70-129">string</span></span> |<span data-ttu-id="48a70-130">Spécifie le nom de fichier du script qui contient la définition de votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="48a70-131">Ce script doit se trouver dans le dossier racine du fichier .zip téléchargé depuis l’URL spécifiée par la propriété configuration.url.</span><span class="sxs-lookup"><span data-stu-id="48a70-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="48a70-132">Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.script est définie.</span><span class="sxs-lookup"><span data-stu-id="48a70-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="48a70-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="48a70-133">settings.configuration.function</span></span> |<span data-ttu-id="48a70-134">string</span><span class="sxs-lookup"><span data-stu-id="48a70-134">string</span></span> |<span data-ttu-id="48a70-135">Spécifie le nom de votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="48a70-136">La configuration nommée doit se trouver dans le script défini par configuration.script.</span><span class="sxs-lookup"><span data-stu-id="48a70-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="48a70-137">Cette propriété est requise si la propriété settings.configuration.url ou settings.configuration.function est définie.</span><span class="sxs-lookup"><span data-stu-id="48a70-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="48a70-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="48a70-138">settings.configurationArguments</span></span> |<span data-ttu-id="48a70-139">Collection</span><span class="sxs-lookup"><span data-stu-id="48a70-139">Collection</span></span> |<span data-ttu-id="48a70-140">Définit les paramètres à transmettre à votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="48a70-141">Cette propriété n’est pas chiffrée.</span><span class="sxs-lookup"><span data-stu-id="48a70-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="48a70-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="48a70-142">settings.configurationData.url</span></span> |<span data-ttu-id="48a70-143">string</span><span class="sxs-lookup"><span data-stu-id="48a70-143">string</span></span> |<span data-ttu-id="48a70-144">Spécifie l’URL de téléchargement de votre fichier de données de configuration (.psd1) à utiliser comme entrée pour votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="48a70-145">Si l’accès à l’URL fournie nécessite un jeton SAP, vous devez définir la propriété protectedSettings.configurationDataUrlSasToken sur la valeur du jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="48a70-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="48a70-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="48a70-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="48a70-147">string</span><span class="sxs-lookup"><span data-stu-id="48a70-147">string</span></span> |<span data-ttu-id="48a70-148">Active ou désactive la collecte télémétrique.</span><span class="sxs-lookup"><span data-stu-id="48a70-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="48a70-149">Les seules valeurs possibles pour cette propriété sont **« Enable », « Disable », « » ou « $null »**.</span><span class="sxs-lookup"><span data-stu-id="48a70-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="48a70-150">Le fait de laisser cette propriété vide ou de la définir sur $null active la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="48a70-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="48a70-151">La valeur par défaut est « ».</span><span class="sxs-lookup"><span data-stu-id="48a70-151">The default value is ''.</span></span> [<span data-ttu-id="48a70-152">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="48a70-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="48a70-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="48a70-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="48a70-154">Collection</span><span class="sxs-lookup"><span data-stu-id="48a70-154">Collection</span></span> |<span data-ttu-id="48a70-155">Définit d’autres emplacements de téléchargement de WMF.</span><span class="sxs-lookup"><span data-stu-id="48a70-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="48a70-156">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="48a70-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="48a70-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="48a70-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="48a70-158">Collection</span><span class="sxs-lookup"><span data-stu-id="48a70-158">Collection</span></span> |<span data-ttu-id="48a70-159">Définit les paramètres à transmettre à votre configuration DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="48a70-160">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="48a70-160">This property is encrypted.</span></span> |
| <span data-ttu-id="48a70-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="48a70-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="48a70-162">string</span><span class="sxs-lookup"><span data-stu-id="48a70-162">string</span></span> |<span data-ttu-id="48a70-163">Spécifie le jeton SAP permettant d’accéder à l’URL définie par configuration.url.</span><span class="sxs-lookup"><span data-stu-id="48a70-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="48a70-164">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="48a70-164">This property is encrypted.</span></span> |
| <span data-ttu-id="48a70-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="48a70-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="48a70-166">string</span><span class="sxs-lookup"><span data-stu-id="48a70-166">string</span></span> |<span data-ttu-id="48a70-167">Spécifie le jeton SAP permettant d’accéder à l’URL définie par configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="48a70-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="48a70-168">Cette propriété est chiffrée.</span><span class="sxs-lookup"><span data-stu-id="48a70-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="48a70-169">settings vs protectedSettings</span><span class="sxs-lookup"><span data-stu-id="48a70-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="48a70-170">Tous les paramètres sont enregistrés dans un fichier texte de paramètres sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48a70-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="48a70-171">Les propriétés définies sous « settings » sont des propriétés publiques, car elles ne sont pas chiffrées dans le fichier texte de paramètres.</span><span class="sxs-lookup"><span data-stu-id="48a70-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="48a70-172">Les propriétés définies sous « protectedSettings » sont chiffrées avec un certificat et ne sont pas affichées en texte brut dans ce fichier sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48a70-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="48a70-173">Si des informations d’identification sont requises pour la configuration, elles peuvent être incluses dans protectedSettings :</span><span class="sxs-lookup"><span data-stu-id="48a70-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="48a70-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="48a70-174">Example</span></span>
<span data-ttu-id="48a70-175">L’exemple suivant est tiré de la section « Prise en main » de l’article [Présentation du gestionnaire d’extensions de configuration d’état souhaité Microsoft Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48a70-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="48a70-176">Cet exemple utilise des modèles Resource Manager au lieu d’applets de commande pour déployer l’extension.</span><span class="sxs-lookup"><span data-stu-id="48a70-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="48a70-177">Enregistrez la configuration « IisInstall.ps1 », placez-la dans un fichier .zip et chargez le fichier dans une URL accessible.</span><span class="sxs-lookup"><span data-stu-id="48a70-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="48a70-178">Cet exemple utilise le stockage Blob Azure, mais il est possible de télécharger les fichiers .zip depuis n’importe quel emplacement arbitraire.</span><span class="sxs-lookup"><span data-stu-id="48a70-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="48a70-179">Dans le modèle Azure Resource Manager, le code suivant demande à la VM de télécharger le fichier correct et d’exécuter la fonction PowerShell appropriée :</span><span class="sxs-lookup"><span data-stu-id="48a70-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="48a70-180">Mise à jour depuis le format précédent</span><span class="sxs-lookup"><span data-stu-id="48a70-180">Updating from the Previous Format</span></span>
<span data-ttu-id="48a70-181">Tous les paramètres au format précédent (qui contient les propriétés publiques ModulesUrl, ConfigurationFunction, SasToken ou Properties) s’adaptent automatiquement au format actuel et s’exécutent exactement comme avant.</span><span class="sxs-lookup"><span data-stu-id="48a70-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="48a70-182">Le schéma suivant est ce à quoi les paramètres précédents ressemblaient :</span><span class="sxs-lookup"><span data-stu-id="48a70-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="48a70-183">Voici comment le format précédent s’adapte au format actuel :</span><span class="sxs-lookup"><span data-stu-id="48a70-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="48a70-184">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="48a70-184">Property Name</span></span> | <span data-ttu-id="48a70-185">Équivalent dans le schéma précédent</span><span class="sxs-lookup"><span data-stu-id="48a70-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="48a70-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="48a70-186">settings.wmfVersion</span></span> |<span data-ttu-id="48a70-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="48a70-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="48a70-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="48a70-188">settings.configuration.url</span></span> |<span data-ttu-id="48a70-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="48a70-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="48a70-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="48a70-190">settings.configuration.script</span></span> |<span data-ttu-id="48a70-191">Première partie de settings.ConfigurationFunction (avant « \\\\ »)</span><span class="sxs-lookup"><span data-stu-id="48a70-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="48a70-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="48a70-192">settings.configuration.function</span></span> |<span data-ttu-id="48a70-193">Deuxième partie de settings.ConfigurationFunction (après « \\\\ »)</span><span class="sxs-lookup"><span data-stu-id="48a70-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="48a70-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="48a70-194">settings.configurationArguments</span></span> |<span data-ttu-id="48a70-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="48a70-195">settings.Properties</span></span> |
| <span data-ttu-id="48a70-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="48a70-196">settings.configurationData.url</span></span> |<span data-ttu-id="48a70-197">protectedSettings.DataBlobUri (sans jeton SAP)</span><span class="sxs-lookup"><span data-stu-id="48a70-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="48a70-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="48a70-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="48a70-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="48a70-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="48a70-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="48a70-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="48a70-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="48a70-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="48a70-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="48a70-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="48a70-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="48a70-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="48a70-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="48a70-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="48a70-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="48a70-205">settings.SasToken</span></span> |
| <span data-ttu-id="48a70-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="48a70-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="48a70-207">Jeton SAP de protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="48a70-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="48a70-208">Dépannage : code d’erreur 1100</span><span class="sxs-lookup"><span data-stu-id="48a70-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="48a70-209">Le code d’erreur 1100 indique qu’il existe un problème avec l’entrée utilisateur pour l’extension DSC.</span><span class="sxs-lookup"><span data-stu-id="48a70-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="48a70-210">Le texte de ces erreurs est variable et peut changer.</span><span class="sxs-lookup"><span data-stu-id="48a70-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="48a70-211">Voici certaines des erreurs que vous pouvez rencontrer et comment vous pouvez les résoudre.</span><span class="sxs-lookup"><span data-stu-id="48a70-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="48a70-212">Valeurs non valides</span><span class="sxs-lookup"><span data-stu-id="48a70-212">Invalid Values</span></span>
<span data-ttu-id="48a70-213">« Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="48a70-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="48a70-214">The only possible values are '', 'Enable', and 'Disable' » (Privacy.dataCollection est « {0} ». Les seules valeurs possibles sont « », « Enable » et « Disable ».) « WmfVersion is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="48a70-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="48a70-215">Les seules valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="48a70-215">Only possible values are …</span></span> <span data-ttu-id="48a70-216">and ’latest’"</span><span class="sxs-lookup"><span data-stu-id="48a70-216">and 'latest'"</span></span>

<span data-ttu-id="48a70-217">Problème : Une valeur fournie n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="48a70-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="48a70-218">Solution : Remplacer la valeur non valide par une valeur valide.</span><span class="sxs-lookup"><span data-stu-id="48a70-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="48a70-219">Consultez le tableau dans la section Détails.</span><span class="sxs-lookup"><span data-stu-id="48a70-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="48a70-220">URL non valide</span><span class="sxs-lookup"><span data-stu-id="48a70-220">Invalid URL</span></span>
<span data-ttu-id="48a70-221">« ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="48a70-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="48a70-222">This is not a valid URL » (configurationData.url est « {0} ». Il ne s’agit pas d’une URL valide.) « DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="48a70-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="48a70-223">This is not a valid URL » (DataBlobUri est « {0} ». Il ne s’agit pas d’une URL valide.) « Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="48a70-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="48a70-224">This is not a valid URL » (configuration.url est « {0} ». Il ne s’agit pas d’une URL valide.)</span><span class="sxs-lookup"><span data-stu-id="48a70-224">This is not a valid URL"</span></span>

<span data-ttu-id="48a70-225">Problème : Une URL fournie n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="48a70-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="48a70-226">Solution : Vérifiez toutes les URL que vous avez fournies.</span><span class="sxs-lookup"><span data-stu-id="48a70-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="48a70-227">Assurez-vous que toutes les URL se résolvent en emplacements valides auxquels l’extension peut accéder sur l’ordinateur distant.</span><span class="sxs-lookup"><span data-stu-id="48a70-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="48a70-228">Type configurationArguments non valide</span><span class="sxs-lookup"><span data-stu-id="48a70-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="48a70-229">« Invalid configurationArguments type {0} » (Type configurationArguments {0} non valide)</span><span class="sxs-lookup"><span data-stu-id="48a70-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="48a70-230">Problème : La propriété configurationArguments ne peut pas se résoudre en objet de table de hachage.</span><span class="sxs-lookup"><span data-stu-id="48a70-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="48a70-231">Solution : Faites de votre propriété configurationArguments une table de hachage.</span><span class="sxs-lookup"><span data-stu-id="48a70-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="48a70-232">Suivez le format fourni dans l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="48a70-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="48a70-233">Prenez garde aux guillemets, aux virgules et aux accolades.</span><span class="sxs-lookup"><span data-stu-id="48a70-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="48a70-234">Propriétés configurationArguments en double</span><span class="sxs-lookup"><span data-stu-id="48a70-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="48a70-235">« Found duplicate arguments '{0}' in both public and protected configurationArguments » (Arguments « {0} » en double trouvés dans les paramètres configurationArguments publics et protégés)</span><span class="sxs-lookup"><span data-stu-id="48a70-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="48a70-236">Problème : Les arguments configurationArguments dans les paramètres publics et protégés contiennent des propriétés portant le même nom.</span><span class="sxs-lookup"><span data-stu-id="48a70-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="48a70-237">Solution : Supprimez l’une des propriétés en double.</span><span class="sxs-lookup"><span data-stu-id="48a70-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="48a70-238">Propriétés manquantes</span><span class="sxs-lookup"><span data-stu-id="48a70-238">Missing Properties</span></span>
<span data-ttu-id="48a70-239">« Configuration.function requires that configuration.url or configuration.module is specified » (configuration.url ou configuration.module doit être spécifié pour configuration.function.)</span><span class="sxs-lookup"><span data-stu-id="48a70-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="48a70-240">« Configuration.url requires that configuration.script is specified » (configuration.script doit être spécifié pour configuration.url)</span><span class="sxs-lookup"><span data-stu-id="48a70-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="48a70-241">« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configuration.script)</span><span class="sxs-lookup"><span data-stu-id="48a70-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="48a70-242">« Configuration.url requires that configuration.function is specified » (configuration.function doit être spécifié pour configuration.url)</span><span class="sxs-lookup"><span data-stu-id="48a70-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="48a70-243">« Configuration.script requires that configuration.url is specified » (configuration.url doit être spécifié pour configurationUrlSasToken)</span><span class="sxs-lookup"><span data-stu-id="48a70-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="48a70-244">« ConfigurationDataUrlSasToken requires that configurationData.url is specified » (configurationData.url doit être spécifié pour configurationDataUrlSasToken)</span><span class="sxs-lookup"><span data-stu-id="48a70-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="48a70-245">Problème : Une propriété définie a besoin d’une autre propriété qui est manquante.</span><span class="sxs-lookup"><span data-stu-id="48a70-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="48a70-246">Solutions :</span><span class="sxs-lookup"><span data-stu-id="48a70-246">Solutions:</span></span> 

* <span data-ttu-id="48a70-247">Fournissez la propriété manquante.</span><span class="sxs-lookup"><span data-stu-id="48a70-247">Provide the missing property.</span></span>
* <span data-ttu-id="48a70-248">Supprimez la propriété qui a besoin de la propriété manquante.</span><span class="sxs-lookup"><span data-stu-id="48a70-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48a70-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48a70-249">Next Steps</span></span>
<span data-ttu-id="48a70-250">En savoir plus sur DSC et les groupes identiques de machines virtuelles dans [Utilisation des groupes identiques de machines virtuelles avec l’extension DSC Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="48a70-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="48a70-251">En savoir plus sur la [Gestion des informations d’identification sécurisées de DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48a70-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="48a70-252">Pour plus d’informations sur le gestionnaire d’extensions DSC Azure, voir [Présentation du gestionnaire d’extensions de configuration d’état souhaité Microsoft Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48a70-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="48a70-253">Pour plus informations sur DSC PowerShell, [voir le centre de documentation PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="48a70-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

