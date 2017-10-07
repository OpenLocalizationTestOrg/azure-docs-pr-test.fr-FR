---
title: "aaaConnect votre réseau virtuel de tooyour application à l’aide de PowerShell"
description: "Obtenir des instructions sur le fonctionnement de tooconnect tooand avec des réseaux virtuels à l’aide de PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Connecter votre réseau virtuel de tooyour application à l’aide de PowerShell
## <a name="overview"></a>Vue d'ensemble
Dans Azure App Service, vous pouvez connecter votre application (API, mobile ou web) tooan réseau virtuel Azure (VNet) dans votre abonnement. Cette fonctionnalité est appelée « intégration au réseau virtuel ». fonctionnalité d’intégration de réseau virtuel Hello ne doit pas être confondue avec fonctionnalité d’environnement App Service hello, qui vous permet de toorun une instance de Service d’applications Azure dans votre réseau virtuel.

fonctionnalité d’intégration de réseau virtuel Hello possède une interface utilisateur (IU) dans le nouveau portail de hello que vous pouvez utiliser toointegrate avec des réseaux virtuels sont déployés à l’aide du modèle de déploiement classique hello ou de modèle de déploiement du Gestionnaire de ressources Azure hello. Si vous souhaitez toolearn plus d’informations sur la fonctionnalité de hello, consultez [intégrer votre application à un réseau virtuel Azure](web-sites-integrate-with-vnet.md).

Cet article n’est pas sur comment toouse hello UI mais plutôt sur l’intégration de tooenable à l’aide de PowerShell. Étant donné que les commandes hello pour chaque modèle de déploiement sont différents, cet article comporte une section pour chaque modèle de déploiement.  

Avant de poursuivre la lecture de cet article, vérifiez ce qui suit :

* Hello que dernière Azure PowerShell SDK installé. Vous pouvez installer cette avec hello Web Platform Installer.
* Une application dans Azure App Service est en cours d’exécution dans le niveau Standard ou Premium.

## <a name="classic-virtual-networks"></a>Réseaux virtuels classiques
Cette section décrit les trois tâches pour les réseaux virtuels qui utilisent le modèle de déploiement classique hello :

1. Connecter votre application tooa préexistants réseau virtuel qui a une passerelle et est configuré pour la connectivité de point-to-site.
2. Mettre à jour des informations relatives à l’intégration au réseau virtuel pour votre application.
3. Déconnecter votre application du réseau virtuel.

### <a name="connect-an-app-tooa-classic-vnet"></a>Se connecter à une application tooa réseau virtuel classique
tooconnect un réseau virtuel tooa d’application, suivez ces trois étapes :

1. Déclarez l’application web toohello qu’il devra joindre à un réseau virtuel particulier. application Hello génère un certificat qui sera allouée toohello des réseaux virtuels pour la connectivité de point-to-site.
2. Réseau virtuel toohello du certificat application hello web de télécharger et extraire les URI du package hello point-to-site VPN.
3. Mettre à jour la connexion de réseau virtuel de l’application hello web avec l’URI du package de point-to-site hello.

Hello premier et troisième étapes sont entièrement scriptable, mais la deuxième étape de hello nécessite une action manuelle à usage unique via le portail de hello ou accès tooperform **PUT** ou **correctif** actions sur le réseau virtuel de hello Point de terminaison du Gestionnaire de ressources Azure. Contactez le Support Azure toohave cette option est activée. Avant de commencer, vérifiez que vous disposez d’un réseau virtuel classique avec une connectivité de point à site activée et une passerelle déployée. toocreate hello passerelle et activer point-to-site connectivité, vous devez portal de hello toouse comme décrit dans [création d’une passerelle VPN][createvpngateway].

réseau virtuel classique Hello doit toobe Bonjour même abonnement que votre Service d’applications de planifier cette application hello blocages que vous intégrez avec.

##### <a name="set-up-azure-powershell-sdk"></a>Configurer le Kit de développement logiciel (SDK)
Ouvrez une fenêtre PowerShell et configurez votre abonnement et votre compte Azure comme suit :

    Login-AzureRmAccount

Cette commande ouvre une invite de commandes tooget vos informations d’identification Azure. Après que vous être connecté, utilisez une de hello suivant l’abonnement de hello tooselect de commandes que vous souhaitez toouse. Assurez-vous que vous utilisez abonnement hello qui se trouvent dans votre réseau virtuel et un plan de Service d’application.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

ou

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variables utilisées dans cet article
les commandes toosimplify, nous allons définir un **$Configuration** variable PowerShell avec une configuration spécifique hello.

Définissez une variable comme suit dans PowerShell avec hello paramètres suivants :

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

emplacement de l’application Hello doit être emplacement hello sans espaces. Par exemple, « West US » devient westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

élément suivant de Hello est où le certificat de hello doit être écrits. Il doit s’agir d’un chemin d’accès en écriture sur votre ordinateur local. Assurez-vous que tooinclude .cer à fin de hello.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee vous définissez, type **$Configuration**.

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

reste Hello de cette section part du principe que vous disposez d’une variable créée comme décrit ci-dessus.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Déclarer des application toohello de réseau virtuel hello
Utilisez hello suivant commande tootell hello application qu’il doit utiliser ce réseau virtuel spécifique. Cela entraîne hello application toogenerate certificats nécessaires :

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Si cette commande réussit, **$vnet** doit inclure une variable **Properties**. Hello **propriétés** variable doit contenir à la fois une empreinte numérique et hello certificat données de certificat.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Télécharger le réseau virtuel toohello du certificat application hello web
Une étape unique manuelle est requise pour chaque combinaison réseau virtuel/abonnement. Autrement dit, si vous vous connectez des applications dans l’abonnement A tooVirtual réseau A, vous devez toodo cette étape qu’une seule fois, quelle que soit le nombre d’applications que vous configurez. Si vous ajoutez un nouveau réseau virtuel de tooanother d’application, vous devez toodo ce message. Hello en fait un jeu de certificats est généré au niveau de l’abonnement dans Azure App Service que hello jeu est générée une fois pour chaque réseau virtuel auquel hello applications seront connectent.

Hello certificats seront ont déjà été définies si vous avez suivi ces étapes, ou si vous avez intégré hello même réseau virtuel à l’aide du portail de hello.

première étape de Hello est un fichier .cer de hello toogenerate. deuxième étape de Hello est un réseau virtuel tooyour du fichier .cer tooupload hello. toogenerate de fichier .cer hello à partir de l’appel d’API de hello Bonjour étape antérieure, exécutez hello suivant les commandes.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certificat de Hello se trouve dans un emplacement de hello qui **$Configuration.GeneratedCertificatePath** spécifie.

certificat de hello tooupload utiliser manuellement, hello [portail Azure] [ azureportal] et **parcourir le réseau virtuel (classiques)** > **lesconnexionsVPN**  >  **Point-to-site** > **gérer les certificats**. À partir de là, téléchargez votre certificat.

##### <a name="get-hello-point-to-site-package"></a>Obtenir le package de point-to-site hello
étape suivante de Hello dans la configuration d’une connexion de réseau virtuel sur une application web est le package de point-to-site tooget hello et fournit l’application web tooyour.

Enregistrez hello appelé GetNetworkPackageUri.json quelque part sur votre ordinateur, par exemple, C:\Azure\Templates\GetNetworkPackageUri.json par le fichier modèle tooa suivant.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


Définissez les paramètres d’entrée :

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Script hello d’appel :

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


variable de Hello **$output. Outputs.packageUri** contient désormais hello package URI toobe donné tooyour l’application web.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Télécharger l’application tooyour de package de point-to-site hello
étape finale de Hello est application hello de tooprovide avec ce package. Exécutez simplement la commande suivante hello :

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Si un message vous demande tooconfirm que vous remplacez une ressource existante, assurez-vous que tooallow il.

Une fois cette commande réussit, votre application doit maintenant être connecté toohello des réseaux virtuels. tooconfirm cas de réussite, accédez tooyour console d’application et tapez Bonjour qui suit :

    SET WEBSITE_

S’il existe une variable d’environnement appelée WEBSITE_VNETNAME qui a une valeur qui correspond au nom hello du réseau virtuel de hello cible, toutes les configurations ont réussi.

### <a name="update-classic-vnet-integration-information"></a>Mettre à jour des informations relatives à l’intégration au réseau virtuel classique
tooupdate ou resynchronisation de vos informations, répétez simplement les étapes hello que vous avez suivi lors de la création de l’intégration hello en premier lieu de hello. à savoir :

1. Définir vos informations de configuration.
2. Déclarer des application toohello de réseau virtuel hello.
3. Obtenir le package de point-to-site hello.
4. Télécharger l’application tooyour de package de point-to-site hello.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Déconnecter votre application d’un réseau virtuel classique
toodisconnect hello application, vous avez besoin des informations de configuration hello qui a été définies lors de l’intégration de réseau virtuel. À l’aide de ces informations, il est ensuite un toodisconnect de commande votre application à partir de votre réseau virtuel.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Réseaux virtuels Resource Manager
Les réseaux virtuels Resource Manager disposent d’API Azure Resource Manager, qui simplifient certains processus si on les compare aux réseaux virtuels classiques. Nous avons un script qui vous aideront à exécuter hello tâches suivantes :

* Créer un réseau virtuel Resource Manager et y intégrer votre application
* Créer une passerelle, configurer la connectivité de point à site dans un réseau virtuel Resource Manager préexistant, puis y intégrer votre application.
* Intégrer votre application à un réseau virtuel Resource Manager préexistant disposant d’une passerelle et sur lequel la connectivité de point à site est activée.
* Déconnecter votre application du réseau virtuel.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script d’intégration App Service pour les réseaux virtuels Resource Manager
Copiez hello suivants de script et enregistrement les fichiers tooa. Si vous ne souhaitez pas script de hello toouse, vous pouvez toolearn libre à partir de celui-ci toosee comment tooset les choses avec un réseau virtuel du Gestionnaire de ressources.

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

Enregistrer une copie du script de hello. Dans cet article, il est appelé V2VnetAllinOne.ps1, mais vous pouvez utiliser un autre nom. Ce script n’inclut aucun argument. Vous devez simplement l’exécuter. Hello première script de hello effectuera est invite toosign dans. Après que vous être connecté, script de hello Obtient des informations relatives à votre compte et retourne une liste des abonnements. Sans compter demande hello vos informations d’identification, l’exécution du script initiale hello ressemble à ceci :

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Choose an option: 3

    Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47

    Veuillez entrer hello groupe de ressources de votre application : hcdemo-rg entrez hello nom de votre application : v2vnetpowershell comment vous souhaitez toodo ?

    1) Ajouter une application de tooan nouveau réseau virtuel
    2) Ajouter une application de tooan réseau virtuel existant
    3) Remove a Virtual Network from an App

reste Hello de cette section décrit chacune de ces trois options.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Créer et intégrer un réseau virtuel Resource Manager
Sélectionnez d’un réseau virtuel qu’utilise hello du modèle de déploiement de gestionnaire de ressources et l’intégrer à votre application, toocreate **1) ajouter un nouveau réseau virtuel de tooan application**. Vous serez invité pour nom hello du réseau virtuel de hello. Dans mon cas, comme vous pouvez le voir Bonjour suivant les paramètres, j’ai utilisé le nom hello, v2pshell.

script de Hello donne des détails de hello sur le réseau virtuel hello en cours de création. Si vous le souhaitez, je peux modifier une des valeurs de hello. Dans l’exécution de cet exemple, j’ai créé un réseau virtuel qui a hello suivant les paramètres :

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Si vous souhaitez une des valeurs de hello toochange, tapez **Y** et apporter des modifications de hello. Lorsque vous êtes satisfait des paramètres de réseau virtuel hello, tapez **N** ou appuyez simplement sur ENTRÉE lorsque vous êtes invité à modifier les paramètres de hello. À partir de là sur jusqu'à la fin, le script de hello vous indiquera parmi ce qu’il « i effectuant jusqu'à ce qu’il démarre la passerelle de réseau virtuel toocreate hello. Cette étape peut prendre jusqu'à tooan heure. Il n’existe aucun indicateur de progression durant cette phase, mais le script de hello vous avertit quand une passerelle de hello a été créé.

Une fois le script de hello, il indiquera **terminé**. À ce stade, vous aurez un réseau virtuel du Gestionnaire de ressources qui a le nom de hello et les paramètres que vous avez sélectionné. Ce nouveau réseau virtuel sera également intégré à votre application.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Intégrer votre application à un réseau virtuel Resource Manager préexistant
Lorsque vous intégrez avec un réseau virtuel préexistant, si vous fournissez un réseau virtuel du Gestionnaire de ressources qui n’a pas de passerelle ou de connectivité de point à site, hello script qui définit. Si hello réseau virtuel possède déjà les éléments de configuration, le script de hello va intégration toohello droite de l’application. toostart ce processus, sélectionnez simplement **2) ajouter un réseau virtuel existant de tooan application**.

Cette option fonctionne uniquement si vous avez un réseau virtuel Gestionnaire de ressources préexistantes qui se trouve dans hello même abonnement que votre application. Une fois que vous sélectionnez hello option, une liste de vos réseaux virtuels du Gestionnaire de ressources s’affiche.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Choose an option: 5

Il suffit de sélectionner réseau virtuel hello toointegrate avec souhaitées. Si vous disposez déjà d’une passerelle qui dispose d’une connectivité de point-to-site activée, le script de hello s’intègre simplement votre application avec votre réseau virtuel. Si vous ne disposez pas d’une passerelle, vous devez le sous-réseau de passerelle toospecify hello. Votre sous-réseau de passerelle doit être situé dans votre espace d’adressage de réseau virtuel. Il ne peut pas être situé dans un autre sous-réseau. Si vous avez un réseau virtuel sans passerelle et que vous exécutez cette étape, voici ce que vous obtenez :

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

Dans cet exemple, j’ai créé une passerelle de réseau virtuel qui a hello suivant les paramètres :

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

Si vous souhaitez toochange un de ces paramètres, vous pouvez le faire. Dans le cas contraire, appuyez sur entrée et hello script créer votre passerelle et attacher votre réseau virtuel de tooyour application. heure de création de passerelle Hello est toujours une heure, bien que, par conséquent, assurez-vous que vous esprit qui. Lorsque tout est terminé, le script de hello indiquera **terminé**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Se déconnecter de votre application à partir d’un réseau virtuel Resource Manager
Déconnexion de votre application à partir de votre réseau virtuel ne pas arrêter la passerelle de hello ou désactiver la connectivité de point-to-site. Vous pouvez donc utiliser ces dernières à d’autres fins. Il également ne pas déconnecte toutes les autres applications autres que hello vous fourni. tooperform cette action, sélectionnez **3) supprimer un réseau virtuel à partir d’une application**. Vous obtenez ceci :

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Bien que le script de hello indique que la suppression, il ne supprime pas de réseau virtuel de hello. Il supprime simplement l’intégration hello. Après avoir confirmé que c’est ce que vous voulez toodo, commande hello est traitée très rapidement et vous indique **True** quand il est terminé.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
