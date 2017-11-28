---
title: "Supprimer une passerelle de réseau virtuel : PowerShell : Azure Classic | Microsoft Docs"
description: "Supprimez une passerelle de réseau virtuel avec PowerShell dans le modèle de déploiement classique."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="765df-103">Supprimer une passerelle de réseau virtuel avec PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="765df-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="765df-104">Resource Manager - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="765df-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="765df-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="765df-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="765df-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="765df-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="765df-107">Cet article vous aide à supprimer une passerelle VPN dans le modèle de déploiement classique à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="765df-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="765df-108">Une fois la passerelle de réseau virtuel supprimée, modifiez le fichier de configuration réseau pour supprimer les éléments que vous n’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="765df-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="765df-109"><a name="connect"></a>Étape 1 : Connectez-vous à Azure</span><span class="sxs-lookup"><span data-stu-id="765df-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="765df-110">1. Installez les dernières applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="765df-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="765df-111">Téléchargez et installez la dernière version des applets de commande PowerShell Azure Service Management (SM).</span><span class="sxs-lookup"><span data-stu-id="765df-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="765df-112">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="765df-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="765df-113">2. Connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="765df-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="765df-114">Ouvrez la console PowerShell avec des droits élevés et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="765df-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="765df-115">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="765df-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="765df-116"><a name="export"></a>Étape 2 : Exportez et affichez le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="765df-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="765df-117">Créez un répertoire sur votre ordinateur, puis exportez le fichier de configuration réseau dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="765df-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="765df-118">Vous utilisez ce fichier aussi bien pour afficher les informations de configuration actuelles que pour modifier la configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="765df-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="765df-119">Dans cet exemple, le fichier de configuration réseau est exporté vers C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="765df-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="765df-120">Dans un éditeur de texte, ouvrez le fichier, puis affichez le nom de votre réseau virtuel classique.</span><span class="sxs-lookup"><span data-stu-id="765df-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="765df-121">Quand vous créez un réseau virtuel dans le portail Azure, le nom complet utilisé par Azure n’est pas visible dans le portail.</span><span class="sxs-lookup"><span data-stu-id="765df-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="765df-122">Par exemple, un réseau virtuel qui figure sous le nom « ClassicVNet1 » dans le portail Azure peut avoir un nom beaucoup plus long dans le fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="765df-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="765df-123">Le nom peut ressembler à ceci : « Group ClassicRG1 ClassicVNet1 ».</span><span class="sxs-lookup"><span data-stu-id="765df-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="765df-124">Les noms des réseaux virtuels sont répertoriés sous la forme **'VirtualNetworkSite name ='**.</span><span class="sxs-lookup"><span data-stu-id="765df-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="765df-125">Utilisez les noms indiqués dans le fichier de configuration réseau lors de l’exécution de vos applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="765df-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="765df-126"><a name="delete"></a>Étape 3 : Supprimez la passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="765df-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="765df-127">Lorsque vous supprimez une passerelle de réseau virtuel, toutes les connexions au réseau virtuel via la passerelle sont déconnectées.</span><span class="sxs-lookup"><span data-stu-id="765df-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="765df-128">Si vous disposez de clients P2S connectés au réseau virtuel, ils sont déconnectés sans avertissement.</span><span class="sxs-lookup"><span data-stu-id="765df-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="765df-129">Cet exemple supprime la passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="765df-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="765df-130">Vérifiez que vous utilisez le nom complet du réseau virtuel indiqué dans le fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="765df-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="765df-131">Si l’opération réussit, la valeur de retour s’affiche :</span><span class="sxs-lookup"><span data-stu-id="765df-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="765df-132"><a name="modify"></a>Étape 4 : Modifiez le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="765df-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="765df-133">Lorsque vous supprimez une passerelle de réseau virtuel, l’applet de commande ne modifie pas le fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="765df-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="765df-134">Vous devez le modifier pour supprimer les éléments qui ne sont plus utilisés.</span><span class="sxs-lookup"><span data-stu-id="765df-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="765df-135">Les sections suivantes vous aident à modifier le fichier de configuration réseau que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="765df-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="765df-136"><a name="lnsref"></a>Informations de référence de site de réseau local</span><span class="sxs-lookup"><span data-stu-id="765df-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="765df-137">Pour supprimer les informations de référence de site, apportez des modifications de configuration à **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="765df-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="765df-138">La suppression d’une référence de site local déclenche la suppression d’un tunnel par Azure.</span><span class="sxs-lookup"><span data-stu-id="765df-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="765df-139">En fonction de la configuration que vous avez créée, il se peut qu’une **LocalNetworkSiteRef** ne soit pas répertoriée.</span><span class="sxs-lookup"><span data-stu-id="765df-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="765df-140">Exemple :</span><span class="sxs-lookup"><span data-stu-id="765df-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="765df-141"><a name="lns"></a>Sites de réseau local</span><span class="sxs-lookup"><span data-stu-id="765df-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="765df-142">Supprimez les sites locaux que vous n’utilisez plus.</span><span class="sxs-lookup"><span data-stu-id="765df-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="765df-143">Selon la configuration que vous avez créée, il est possible qu’un **LocalNetworkSite** ne soit pas répertorié.</span><span class="sxs-lookup"><span data-stu-id="765df-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="765df-144">Dans cet exemple, nous avons supprimé uniquement Site3.</span><span class="sxs-lookup"><span data-stu-id="765df-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="765df-145"><a name="clientaddresss"></a>Pool d’adresses de client</span><span class="sxs-lookup"><span data-stu-id="765df-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="765df-146">Si vous aviez une connexion P2S à votre réseau virtuel, vous avez un **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="765df-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="765df-147">Supprimez les pools d’adresses de client qui correspondent à la passerelle de réseau virtuel que vous avez supprimée.</span><span class="sxs-lookup"><span data-stu-id="765df-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="765df-148">Exemple :</span><span class="sxs-lookup"><span data-stu-id="765df-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="765df-149"><a name="gwsub"></a>Sous-réseau de passerelle</span><span class="sxs-lookup"><span data-stu-id="765df-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="765df-150">Supprimez le **GatewaySubnet** qui correspond au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="765df-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="765df-151">Exemple :</span><span class="sxs-lookup"><span data-stu-id="765df-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="765df-152"><a name="upload"></a>Étape 5 : Chargez le fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="765df-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="765df-153">Enregistrez vos modifications et chargez le fichier de configuration réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="765df-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="765df-154">Assurez-vous que vous modifiez le chemin d'accès selon les besoins de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="765df-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="765df-155">Si l’opération réussit, la valeur de retour affiche un contenu semblable à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="765df-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded