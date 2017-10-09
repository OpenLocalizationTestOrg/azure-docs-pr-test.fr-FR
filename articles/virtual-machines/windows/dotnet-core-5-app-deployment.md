---
title: "aaaAutomating déploiement d’applications avec les Extensions de Machine virtuelle | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Déploiement d’applications avec des modèles Azure Resource Manager pour les machines virtuelles Windows

Une fois que toutes les exigences d’infrastructures Azure ont été identifiés et de traduire un modèle de déploiement, déploiement d’application réelle hello doit toobe adressé. Déploiement d’application fait référence des fichiers binaires d’application réelle de hello tooinstalling sur les ressources Azure. Pour un exemple de magasin de musique hello, .net Core et IIS doivent toobe installé et configuré sur chaque ordinateur virtuel. Bonjour magasin de musique binaires doivent toobe installé sur l’ordinateur virtuel de hello et hello de base de données du magasin de musique créé au préalable.

Ce document décrit en détail comment extensions de Machine virtuelle peuvent automatiser la configuration et déploiement tooAzure ordinateurs virtuels d’application. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Script de configuration
Extensions de Machine virtuelle sont des programmes spécialisés qui s’exécutent sur l’automatisation de machines virtuelles tooprovide configuration. Les extensions sont disponibles pour de nombreux objectifs spécifiques tels que la protection contre les virus, la configuration de la journalisation et la configuration de Docker. Hello, extension de Script personnalisé peut être utilisé toorun un script sur un ordinateur virtuel. Exemple de magasin de musique hello, il est les machines virtuelles de toohello script personnalisé extension tooconfigure hello Windows et installer l’application de magasin de musique hello.

Avant indiquant comment les extensions de machine virtuelle sont déclarées dans un modèle Azure Resource Manager, examinez le script hello qui est exécuté. Ce script configure la machine virtuelle toohost hello de hello Windows application de magasin de musique. Lors de l’exécution, le script de hello installe les logiciels requis de tous les installer l’application de magasin de musique hello à partir du contrôle de code source et préparer hello de base de données. 

> Cet exemple ne sert qu’à des fins de démonstration.

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a>Extension de script de machine virtuelle
Extensions de machine virtuelle peut être exécutées sur un ordinateur virtuel au moment de la génération en incluant la ressource d’extension hello dans le modèle de gestionnaire de ressources Azure hello. extension de Hello peut être ajoutée avec l’Assistant de Visual Studio ajouter une ressource hello, ou en insérant un JSON valide dans le modèle de hello. Hello ressource d’Extension de Script est imbriquée dans hello ressource d’ordinateur virtuel ; Ceci peut être observé dans hello l’exemple suivant.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Extension de Script de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Notez dans hello ci-dessous JSON qui hello script est stocké dans GitHub. Ce script pourrait également être stocké dans Stockage Blob Azure. Modèles Azure Resource Manager permettent également, hello script d’exécution chaîne toobe construit de telle sorte que les valeurs de paramètres de modèle peuvent être utilisées en tant que paramètres pour l’exécution du script. Dans ce cas les données sont fournies lors du déploiement de modèles de hello, et ces valeurs peuvent ensuite être utilisées lors de l’exécution du script de hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

Comme indiqué ci-dessus, il est également de toostore possible vos scripts dans le stockage d’objets Blob Azure. Il existe deux options pour stocker les ressources de script hello dans le stockage blob ; choix entre rendre hello public du conteneur/script et suivez hello même approche comme indiqué ci-dessus, ou il peut être conservée dans le stockage blob privé qui nécessite que vous tooprovide hello storageAccountName et storageAccountKey toohello CustomScriptExtension définition de ressource.

Dans l’exemple hello ci-dessous nous avons passé une étape supplémentaire. Bien qu’il soit nom de compte de stockage possible tooprovide hello et la clé en tant que paramètre ou variable durant le déploiement, les modèles de gestionnaire de ressources fournissent hello `listKeys` fonction qui peut obtenir du compte de stockage hello par programmation la clé et de l’insérer dans toohello modèle au moment du déploiement.

Dans l’exemple hello CustomScriptExtension définition de ressource ci-dessous, notre script personnalisé a déjà été téléchargé tooan appelé compte de stockage Azure `mystorageaccount9999` qui existe dans un autre groupe de ressources appelé `mysa999rgname`. Lorsque nous déployez un modèle qui contient cette ressource, hello `listKeys` fonction obtient par programme hello de la clé de compte de stockage hello `mystorageaccount9999` dans le groupe de ressources de hello `mysa999rgname` et l’insère dans le modèle de toohello pour nous.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

Hello le principal avantage de cette approche est qu’il ne nécessite pas toochange vous votre modèle ou les paramètres de déploiement dans l’événement de hello hello de modification de clé de compte de stockage.

Pour plus d’informations sur l’utilisation d’extension de script personnalisé hello, consultez [extensions de script personnalisé avec les modèles de gestionnaire de ressources](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Étape suivante
<hr>

[Découvrir d’autres modèles Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

