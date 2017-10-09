---
title: "débogage distant avec la livraison continue d’aaaEnable | Documents Microsoft"
description: "Découvrez comment tooenable le débogage à distance lors de l’utilisation de livraison continue toodeploy tooAzure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Activer le débogage distant lors de l’utilisation de livraison continue toopublish tooAzure
Vous pouvez activer le débogage distant dans Azure, pour les services de cloud computing ou des machines virtuelles, lorsque vous utilisez [livraison continue](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish en suivant ces étapes.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Activation du débogage distant pour les services cloud
1. Agent de build hello, définis initial de l’environnement hello pour Azure comme indiqué dans [de ligne de commande Build pour Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Comme hello runtime de débogage distant (msvsmon.exe) est requis pour le package de hello, installez hello **des outils à distance pour Visual Studio**.

    * [Outils de contrôle à distance de Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Outils de contrôle à distance de Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Outils de contrôle à distance de Visual Studio 2013 Update 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    En guise d’alternative, vous pouvez copier les fichiers binaires de débogage distant hello à partir d’un système qui a installé Visual Studio.

3. Créez un certificat comme expliqué dans [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md). Conserver hello .pfx et l’empreinte numérique du certificat RDP et télécharger le service cloud cible hello certificat toohello.
4. Utilisez hello suivant les options dans toobuild de ligne de commande MSBuild hello et le package avec le débogage distant activé. (Remplacez par les chemins d’accès réels tooyour système et projet les fichiers pour les éléments mis entre crochets pointus hello.)
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`est le dossier de toohello de chemin d’accès de hello contenant msvsmon.exe dans les outils à distance hello pour Visual Studio.
    `RemoteDebuggerConnectorVersion`est la version du Kit de développement logiciel Azure hello dans votre service cloud. Elle doit également correspondre à version hello installée avec Visual Studio.
5. Publier le service de cloud toohello cible à l’aide de hello package et le fichier .cscfg généré à l’étape précédente de hello.
6. Importer hello certificat (fichier .pfx) toohello ordinateur disposant de Visual Studio avec le Kit de développement logiciel Azure pour .NET est installé. Assurez-vous que tooimport toohello `CurrentUser\My` magasin de certificats, sinon attachement débogueur toohello dans Visual Studio risque d’échouer.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Activation du débogage distant pour les machines virtuelles
1. Créez une machine virtuelle Azure. Consultez [Création d’une machine virtuelle exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Créer et gérer des machines virtuelles Azure dans Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. Sur hello [page du portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=269851), afficher du tableau de bord toosee hello l’ordinateur virtuel l’ordinateur virtuel de hello **l’empreinte numérique du certificat RDP**. Cette valeur est utilisée pour hello `ServerThumbprint` valeur dans la configuration de l’extension hello.
3. Créer un certificat client, comme indiqué dans [vue d’ensemble des certificats pour les Services de Cloud Azure](cloud-services-certs-create.md) (laissez hello .pfx et l’empreinte numérique du certificat RDP).
4. Installez Azure Powershell (version 0.7.4 ou une version ultérieure) comme indiqué dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
5. Exécutez hello suivant l’extension de script tooenable hello RemoteDebug. Remplacez les chemins d’accès hello et données personnelles avec vos propres, telles que votre nom de l’abonnement, le nom du service et l’empreinte numérique.
   
   > [!NOTE]
   > Ce script est configuré pour Visual Studio 2015. Si vous utilisez Visual Studio 2013 ou Visual Studio 2017, modifier hello `$referenceName` et `$extensionName` affectations ci-dessous trop`RemoteDebugVS2013` ou `RemoteDebugVS2017`.

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. Importation hello certificat (.pfx) toohello ordinateur sur lequel Visual Studio avec le Kit de développement logiciel Azure pour .NET est installé.

