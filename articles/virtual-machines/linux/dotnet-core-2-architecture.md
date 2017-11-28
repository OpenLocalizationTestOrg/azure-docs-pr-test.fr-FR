---
title: "Déploiement de ressources de calcul Linux avec des modèles Azure Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: c3f9f98079e0c89d1231f9c3e62e82c33ad18236
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="adaf3-103">Architecture d’application avec des modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="adaf3-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="adaf3-104">Lors du développement d’un déploiement Azure Resource Manager, les exigences de calcul doivent être mappées aux services et ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="adaf3-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="adaf3-105">Si une application comprend plusieurs points de terminaison http, une base de données, et un service de mise en cache de données, les ressources Azure hébergeant ces composants doivent être rationalisées.</span><span class="sxs-lookup"><span data-stu-id="adaf3-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="adaf3-106">Ainsi, l’exemple d’application du Store musique comprend une application web hébergée sur une machine virtuelle, et une base de données SQL hébergée dans Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="adaf3-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="adaf3-107">Ce document décrit en détail la manière dont les ressources de calcul du Store musique sont configurées dans l’exemple de modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="adaf3-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="adaf3-108">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="adaf3-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="adaf3-109">Pour optimiser l’expérience, prédéployez une instance de la solution sur votre abonnement Azure et travaillez avec le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="adaf3-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="adaf3-110">Pour le modèle complet, consultez [Déploiement du Store musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="adaf3-110">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="adaf3-111">Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="adaf3-111">Virtual Machine</span></span>
<span data-ttu-id="adaf3-112">L’application du Store musique comprend une application web dans laquelle les clients peuvent parcourir et acheter de la musique.</span><span class="sxs-lookup"><span data-stu-id="adaf3-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="adaf3-113">Bien qu’il existe plusieurs services Azure capables d’héberger des applications web, pour cet exemple, une machine virtuelle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="adaf3-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="adaf3-114">Avec l’exemple de modèle du Store musique, une machine virtuelle est déployée, un serveur web est installé, et le site web du Store musique est installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="adaf3-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="adaf3-115">Dans le cadre de cet article, seul le déploiement de machine virtuelle est détaillé.</span><span class="sxs-lookup"><span data-stu-id="adaf3-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="adaf3-116">La configuration du serveur web et de l’application sera décrite en détails dans un prochain article.</span><span class="sxs-lookup"><span data-stu-id="adaf3-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="adaf3-117">Vous pouvez ajouter une machine virtuelle à un modèle à l’aide de l’Assistant Ajouter une nouvelle ressource de Visual Studio, ou en insérant un JSON valide dans le modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="adaf3-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="adaf3-118">Lors du déploiement d’une machine virtuelle, plusieurs ressources associées sont également nécessaires.</span><span class="sxs-lookup"><span data-stu-id="adaf3-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="adaf3-119">Si vous utilisez Visual Studio pour créer le modèle, ces ressources sont créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="adaf3-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="adaf3-120">Si vous construisez manuellement le modèle, ces ressources doivent être insérées et configurées.</span><span class="sxs-lookup"><span data-stu-id="adaf3-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="adaf3-121">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [JSON de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span><span class="sxs-lookup"><span data-stu-id="adaf3-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

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

<span data-ttu-id="adaf3-122">Une fois la machine virtuelle déployée, ses propriétés sont visibles dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="adaf3-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![Machine virtuelle](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="adaf3-124">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="adaf3-124">Storage Account</span></span>
<span data-ttu-id="adaf3-125">Les comptes de stockage offrent de nombreuses options et fonctionnalités de stockage.</span><span class="sxs-lookup"><span data-stu-id="adaf3-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="adaf3-126">Dans le contexte des machines virtuelles Azure, un compte de stockage conserve les disques durs virtuels de la machine virtuelle et tout disque de données supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="adaf3-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="adaf3-127">L’exemple du Store musique inclut un compte de stockage pour stocker le disque dur virtuel de chaque machine virtuelle composant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="adaf3-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="adaf3-128">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span><span class="sxs-lookup"><span data-stu-id="adaf3-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

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

<span data-ttu-id="adaf3-129">Un compte de stockage est associé à une machine virtuelle à l’intérieur de la déclaration de la machine virtuelle du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="adaf3-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="adaf3-130">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Association d’une machine virtuelle et d’un compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span><span class="sxs-lookup"><span data-stu-id="adaf3-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

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

<span data-ttu-id="adaf3-131">Après le déploiement, le compte de stockage est visible dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="adaf3-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![Compte de stockage](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="adaf3-133">Vous pouvez consulter le fichier du lecteur de disque dur virtuel de chaque machine virtuelle déployée avec le modèle en cliquant sur le conteneur d’objets blob du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="adaf3-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![Disques durs virtuels](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="adaf3-135">Pour plus d’informations sur Stockage Azure, voir la [documentation d’Azure Storage](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="adaf3-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="adaf3-136">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="adaf3-136">Virtual Network</span></span>
<span data-ttu-id="adaf3-137">Si une machine virtuelle nécessite une mise en réseau interne offrant, par exemple, la possibilité de communiquer avec d’autres machines virtuelles et ressources Azure, un réseau virtuel Azure est requis.</span><span class="sxs-lookup"><span data-stu-id="adaf3-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="adaf3-138">Un réseau virtuel ne rend pas la machine virtuelle accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="adaf3-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="adaf3-139">La connectivité publique requiert une adresse IP publique, qui est détaillée plus loin dans cette série.</span><span class="sxs-lookup"><span data-stu-id="adaf3-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="adaf3-140">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Réseau et sous-réseaux virtuels](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span><span class="sxs-lookup"><span data-stu-id="adaf3-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

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

<span data-ttu-id="adaf3-141">Dans le portail Azure, le réseau virtuel ressemble à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="adaf3-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="adaf3-142">Notez que toutes les machines virtuelles déployées avec le modèle sont attachées au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="adaf3-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![Réseau virtuel](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="adaf3-144">Interface réseau</span><span class="sxs-lookup"><span data-stu-id="adaf3-144">Network Interface</span></span>
 <span data-ttu-id="adaf3-145">Une interface réseau connecte une machine virtuelle à un réseau virtuel, plus spécifiquement à un sous-réseau défini dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="adaf3-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="adaf3-146">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Interface réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span><span class="sxs-lookup"><span data-stu-id="adaf3-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

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

<span data-ttu-id="adaf3-147">Chaque ressource de machine virtuelle comprend un profil réseau.</span><span class="sxs-lookup"><span data-stu-id="adaf3-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="adaf3-148">L’interface réseau est associée à la machine virtuelle dans ce profil.</span><span class="sxs-lookup"><span data-stu-id="adaf3-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="adaf3-149">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Profil réseau de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span><span class="sxs-lookup"><span data-stu-id="adaf3-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="adaf3-150">Dans le portail Azure, l’interface réseau ressemble à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="adaf3-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="adaf3-151">L’association de l’adresse IP interne et de la machine virtuelle est visible sur la ressource d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="adaf3-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![Interface réseau](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="adaf3-153">Pour plus d’informations sur les réseaux virtuels Azure, voir la [du réseau virtuel Azure](https://azure.microsoft.com/documentation/services/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="adaf3-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="adaf3-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="adaf3-154">Azure SQL Database</span></span>
<span data-ttu-id="adaf3-155">En plus d’une machine virtuelle hébergeant le site web du Store musique, une base de données Azure SQL Database est déployée pour héberger la base de données du Store musique.</span><span class="sxs-lookup"><span data-stu-id="adaf3-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="adaf3-156">L’avantage de l’utilisation d’Azure SQL Database ici est qu’un deuxième ensemble de machines virtuelles n’est pas requis, et que la mise à l’échelle et la disponibilité sont intégrées au service.</span><span class="sxs-lookup"><span data-stu-id="adaf3-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="adaf3-157">Vous pouvez ajouter une base de données Azure SQL Database à l’aide de l’Assistant Ajouter une nouvelle ressource de Visual Studio, ou en insérant un JSON valide dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="adaf3-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="adaf3-158">La ressource SQL Server inclut un nom d’utilisateur et un mot de passe auxquels sont associés des droits d’administration sur l’instance SQL.</span><span class="sxs-lookup"><span data-stu-id="adaf3-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="adaf3-159">Par ailleurs, une ressource de pare-feu SQL est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="adaf3-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="adaf3-160">Par défaut, les applications hébergées dans Azure sont en mesure de se connecter à l’instance SQL.</span><span class="sxs-lookup"><span data-stu-id="adaf3-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="adaf3-161">Pour qu’une application externe telle que SQL Server Management Studio puisse se connecter à l’instance SQL, le pare-feu doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="adaf3-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="adaf3-162">Pour la démonstration du Store musique, la configuration par défaut est correcte.</span><span class="sxs-lookup"><span data-stu-id="adaf3-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="adaf3-163">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span><span class="sxs-lookup"><span data-stu-id="adaf3-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

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

<span data-ttu-id="adaf3-164">Vue des bases de données SQL Server et du Store musique dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="adaf3-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="adaf3-166">Pour plus d’informations sur le déploiement d’Azure SQL Database, voir la [Documentation d’Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="adaf3-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="adaf3-167">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="adaf3-167">Next step</span></span>
<hr>

[<span data-ttu-id="adaf3-168">Étape 2 : accès et sécurité dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="adaf3-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

