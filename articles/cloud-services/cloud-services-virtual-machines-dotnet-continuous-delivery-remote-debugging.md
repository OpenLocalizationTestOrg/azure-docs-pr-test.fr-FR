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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="80a1c-103">Activer le débogage distant lors de l’utilisation de livraison continue toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="80a1c-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="80a1c-104">Vous pouvez activer le débogage distant dans Azure, pour les services de cloud computing ou des machines virtuelles, lorsque vous utilisez [livraison continue](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish en suivant ces étapes.</span><span class="sxs-lookup"><span data-stu-id="80a1c-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="80a1c-105">Activation du débogage distant pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="80a1c-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="80a1c-106">Agent de build hello, définis initial de l’environnement hello pour Azure comme indiqué dans [de ligne de commande Build pour Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="80a1c-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="80a1c-107">Comme hello runtime de débogage distant (msvsmon.exe) est requis pour le package de hello, installez hello **des outils à distance pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="80a1c-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="80a1c-108">Outils de contrôle à distance de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="80a1c-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="80a1c-109">Outils de contrôle à distance de Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="80a1c-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="80a1c-110">Outils de contrôle à distance de Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="80a1c-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="80a1c-111">En guise d’alternative, vous pouvez copier les fichiers binaires de débogage distant hello à partir d’un système qui a installé Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80a1c-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="80a1c-112">Créez un certificat comme expliqué dans [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="80a1c-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="80a1c-113">Conserver hello .pfx et l’empreinte numérique du certificat RDP et télécharger le service cloud cible hello certificat toohello.</span><span class="sxs-lookup"><span data-stu-id="80a1c-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="80a1c-114">Utilisez hello suivant les options dans toobuild de ligne de commande MSBuild hello et le package avec le débogage distant activé.</span><span class="sxs-lookup"><span data-stu-id="80a1c-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="80a1c-115">(Remplacez par les chemins d’accès réels tooyour système et projet les fichiers pour les éléments mis entre crochets pointus hello.)</span><span class="sxs-lookup"><span data-stu-id="80a1c-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="80a1c-116">`VSX64RemoteDebuggerPath`est le dossier de toohello de chemin d’accès de hello contenant msvsmon.exe dans les outils à distance hello pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80a1c-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="80a1c-117">`RemoteDebuggerConnectorVersion`est la version du Kit de développement logiciel Azure hello dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="80a1c-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="80a1c-118">Elle doit également correspondre à version hello installée avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80a1c-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="80a1c-119">Publier le service de cloud toohello cible à l’aide de hello package et le fichier .cscfg généré à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="80a1c-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="80a1c-120">Importer hello certificat (fichier .pfx) toohello ordinateur disposant de Visual Studio avec le Kit de développement logiciel Azure pour .NET est installé.</span><span class="sxs-lookup"><span data-stu-id="80a1c-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="80a1c-121">Assurez-vous que tooimport toohello `CurrentUser\My` magasin de certificats, sinon attachement débogueur toohello dans Visual Studio risque d’échouer.</span><span class="sxs-lookup"><span data-stu-id="80a1c-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="80a1c-122">Activation du débogage distant pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="80a1c-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="80a1c-123">Créez une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="80a1c-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="80a1c-124">Consultez [Création d’une machine virtuelle exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Créer et gérer des machines virtuelles Azure dans Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80a1c-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="80a1c-125">Sur hello [page du portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=269851), afficher du tableau de bord toosee hello l’ordinateur virtuel l’ordinateur virtuel de hello **l’empreinte numérique du certificat RDP**.</span><span class="sxs-lookup"><span data-stu-id="80a1c-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="80a1c-126">Cette valeur est utilisée pour hello `ServerThumbprint` valeur dans la configuration de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="80a1c-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="80a1c-127">Créer un certificat client, comme indiqué dans [vue d’ensemble des certificats pour les Services de Cloud Azure](cloud-services-certs-create.md) (laissez hello .pfx et l’empreinte numérique du certificat RDP).</span><span class="sxs-lookup"><span data-stu-id="80a1c-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="80a1c-128">Installez Azure Powershell (version 0.7.4 ou une version ultérieure) comme indiqué dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80a1c-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="80a1c-129">Exécutez hello suivant l’extension de script tooenable hello RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="80a1c-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="80a1c-130">Remplacez les chemins d’accès hello et données personnelles avec vos propres, telles que votre nom de l’abonnement, le nom du service et l’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="80a1c-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80a1c-131">Ce script est configuré pour Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="80a1c-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="80a1c-132">Si vous utilisez Visual Studio 2013 ou Visual Studio 2017, modifier hello `$referenceName` et `$extensionName` affectations ci-dessous trop`RemoteDebugVS2013` ou `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="80a1c-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="80a1c-133">Importation hello certificat (.pfx) toohello ordinateur sur lequel Visual Studio avec le Kit de développement logiciel Azure pour .NET est installé.</span><span class="sxs-lookup"><span data-stu-id="80a1c-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

