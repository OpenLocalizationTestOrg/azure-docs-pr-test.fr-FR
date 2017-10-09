---
title: "aaaDeploying Linux des ressources de calcul avec des modèles de gestionnaire de ressources Azure | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="1e152-103">Architecture d’application avec des modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="1e152-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="1e152-104">Lors du développement d’un déploiement d’Azure Resource Manager, de calcul des besoins de services et des ressources de tooAzure toobe mappé.</span><span class="sxs-lookup"><span data-stu-id="1e152-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="1e152-105">Si une application se compose de plusieurs points de terminaison http, une base de données et un service de mise en cache de données, hello des ressources Azure qui hébergent chacun de ces composants doit toobe version rationalisé.</span><span class="sxs-lookup"><span data-stu-id="1e152-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="1e152-106">Par exemple, application de magasin de musique exemple hello inclut une application web qui est hébergée sur un ordinateur virtuel et une base de données SQL, qui est hébergé dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1e152-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="1e152-107">Ce document décrit en détail comment les ressources de calcul du magasin de musique hello sont configurés dans le modèle de gestionnaire de ressources Azure exemple hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="1e152-108">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="1e152-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="1e152-109">Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="1e152-110">modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="1e152-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="1e152-111">Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e152-111">Virtual Machine</span></span>
<span data-ttu-id="1e152-112">Hello application de magasin de musique inclut une application web où les clients peuvent rechercher et acquérir de la musique.</span><span class="sxs-lookup"><span data-stu-id="1e152-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="1e152-113">Bien qu’il existe plusieurs services Azure capables d’héberger des applications web, pour cet exemple, une machine virtuelle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="1e152-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="1e152-114">À l’aide du modèle de magasin de musique exemple hello, un ordinateur virtuel est déployé, un serveur web installer et site Web du magasin de musique hello installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="1e152-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="1e152-115">Par souci de hello de cet article, le déploiement d’ordinateurs virtuels uniquement hello est détaillé.</span><span class="sxs-lookup"><span data-stu-id="1e152-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="1e152-116">configuration Hello du serveur web de hello et application hello est détaillée dans un article de la version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1e152-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="1e152-117">Modèle de tooa à l’aide de Visual Studio ajouter une nouvelle ressource, Assistant ou en insérant un JSON valide dans le modèle de déploiement hello de hello peut être ajouté à un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1e152-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="1e152-118">Lors du déploiement d’une machine virtuelle, plusieurs ressources associées sont également nécessaires.</span><span class="sxs-lookup"><span data-stu-id="1e152-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="1e152-119">Si vous utilisez le modèle de Visual Studio toocreate hello, ces ressources sont créés pour vous.</span><span class="sxs-lookup"><span data-stu-id="1e152-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="1e152-120">Si vous construisez manuellement le modèle de hello, ces ressources doivent toobe inséré et configuré.</span><span class="sxs-lookup"><span data-stu-id="1e152-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="1e152-121">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [JSON de l’ordinateur virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="1e152-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

<span data-ttu-id="1e152-122">Une fois déployé, les propriétés d’une machine virtuelle hello peuvent être consultées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e152-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![Machine virtuelle](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="1e152-124">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="1e152-124">Storage Account</span></span>
<span data-ttu-id="1e152-125">Les comptes de stockage offrent de nombreuses options et fonctionnalités de stockage.</span><span class="sxs-lookup"><span data-stu-id="1e152-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="1e152-126">Pour le contexte de hello de machines virtuelles Azure, un compte de stockage conserve des disques durs virtuels hello de machine virtuelle de hello et toutes les autres disques de données.</span><span class="sxs-lookup"><span data-stu-id="1e152-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="1e152-127">exemple de magasin de musique Hello comprend un stockage compte toohold hello disque dur virtuel de chaque ordinateur virtuel dans un déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="1e152-128">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="1e152-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="1e152-129">Un compte de stockage est associé à un ordinateur virtuel à l’intérieur de déclaration de modèle hello Gestionnaire de ressources de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="1e152-130">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association de Machine virtuelle et le compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="1e152-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="1e152-131">Après le déploiement, compte de stockage hello peut être consultée dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e152-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![Compte de stockage](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="1e152-133">En cliquant sur dans le conteneur objets blob du compte de stockage hello, le fichier de disque dur virtuel hello pour chaque ordinateur virtuel déployé avec le modèle de hello peut être consulté.</span><span class="sxs-lookup"><span data-stu-id="1e152-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![Disques durs virtuels](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="1e152-135">Pour plus d’informations sur Stockage Azure, voir la [documentation d’Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="1e152-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="1e152-136">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1e152-136">Virtual Network</span></span>
<span data-ttu-id="1e152-137">Si un ordinateur virtuel nécessite la mise en réseau interne comme toocommunicate de capacité hello avec d’autres machines virtuelles et les ressources Azure, un réseau virtuel Azure est requis.</span><span class="sxs-lookup"><span data-stu-id="1e152-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="1e152-138">Un réseau virtuel ne fait pas hello virtual machine accessible sur internet de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="1e152-139">La connectivité publique requiert une adresse IP publique, qui est détaillée plus loin dans cette série.</span><span class="sxs-lookup"><span data-stu-id="1e152-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="1e152-140">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [réseau virtuel et sous-réseaux](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="1e152-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="1e152-141">À partir de hello portail Azure, réseau virtuel de hello ressemble hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="1e152-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="1e152-142">Notez que tous les ordinateurs virtuels déployés avec le modèle de hello sont attachés toohello les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="1e152-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![Réseau virtuel](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="1e152-144">Interface réseau</span><span class="sxs-lookup"><span data-stu-id="1e152-144">Network Interface</span></span>
 <span data-ttu-id="1e152-145">Une interface réseau connecte à un réseau virtuel de machine virtuelle tooa, le plus précisément les sous-réseaux tooa a été défini dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="1e152-146">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Interface réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="1e152-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="1e152-147">Chaque ressource de machine virtuelle comprend un profil réseau.</span><span class="sxs-lookup"><span data-stu-id="1e152-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="1e152-148">interface de réseau Hello est associé à la machine virtuelle de hello dans ce profil.</span><span class="sxs-lookup"><span data-stu-id="1e152-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="1e152-149">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [profil réseau de Machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="1e152-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="1e152-150">À partir de hello portail Azure, interface de réseau hello ressemble hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="1e152-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="1e152-151">adresse IP interne de Hello et l’association de machine virtuelle hello peuvent être consultés sur la ressource d’interface réseau hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![Interface réseau](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="1e152-153">Pour plus d’informations sur les réseaux virtuels Azure, voir la [du réseau virtuel Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="1e152-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="1e152-154">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1e152-154">Azure SQL Database</span></span>
<span data-ttu-id="1e152-155">En outre, ordinateur virtuel de tooa qui héberge le site Web du magasin de musique hello, une base de données SQL Azure est base de données du magasin de musique toohost déployé hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="1e152-156">présente l’avantage Hello ici de base de données SQL Azure est un deuxième ensemble d’ordinateurs virtuels n’est pas nécessaire que l’échelle et la disponibilité est intégrée à service de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="1e152-157">Une base de données SQL Azure peut être ajouté à l’aide de Visual Studio ajouter une nouvelle ressource, Assistant ou en insérant un JSON valide dans un modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="1e152-158">Hello ressource SQL Server inclut un nom d’utilisateur et un mot de passe disposant de droits d’administrateur sur l’instance SQL hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="1e152-159">Par ailleurs, une ressource de pare-feu SQL est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="1e152-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="1e152-160">Par défaut, les applications hébergées dans Azure sont en mesure de tooconnect avec l’instance SQL hello.</span><span class="sxs-lookup"><span data-stu-id="1e152-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="1e152-161">application tooallow externe telle une SQL Server Management studio tooconnect toohello instance SQL, pare-feu de hello doit toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="1e152-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="1e152-162">Par souci de hello de démonstration du magasin de musique hello, configuration par défaut de hello est correct.</span><span class="sxs-lookup"><span data-stu-id="1e152-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="1e152-163">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [base de données SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="1e152-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="1e152-164">Une vue de hello SQL server et de la base de données MusicStore comme Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e152-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="1e152-166">Pour plus d’informations sur le déploiement d’Azure SQL Database, voir la [Documentation d’Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="1e152-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="1e152-167">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1e152-167">Next step</span></span>
<hr>

[<span data-ttu-id="1e152-168">Étape 2 : accès et sécurité dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1e152-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

