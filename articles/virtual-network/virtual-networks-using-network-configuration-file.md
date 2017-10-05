---
title: "Configurer un réseau virtuel Azure (Classic) - Fichier config réseau | Microsoft Docs"
description: "Découvrez comment créer et modifier des réseaux virtuels (Classic) en exportant, modifiant et important un fichier config réseau."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="24097-103">Configurer un réseau virtuel (Classic) à l’aide d’un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="24097-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="24097-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24097-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="24097-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="24097-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="24097-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24097-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="24097-107">Vous pouvez créer et configurer un réseau virtuel (Classic) avec un fichier config réseau à l’aide de l’interface de ligne de commande Azure (CLI) 1.0 ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24097-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="24097-108">Vous ne pouvez pas utiliser de fichier de configuration de réseau pour créer ou modifier un réseau virtuel via le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24097-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="24097-109">Vous ne pouvez pas utiliser le portail Azure pour créer ou modifier un réseau virtuel (Classic) à l’aide d’un fichier config réseau, mais vous pouvez utiliser le portail Azure pour créer un réseau virtuel (Classic) sans l’aide d’un fichier config réseau.</span><span class="sxs-lookup"><span data-stu-id="24097-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="24097-110">La création et la configuration d’un réseau virtuel (Classic) avec un fichier config réseau requièrent l’exportation, la modification et l’importation du fichier.</span><span class="sxs-lookup"><span data-stu-id="24097-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="24097-111"><a name="export"></a>Exporter un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="24097-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="24097-112">Vous pouvez utiliser PowerShell ou l’interface CLI Azure pour exporter un fichier config réseau.</span><span class="sxs-lookup"><span data-stu-id="24097-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="24097-113">PowerShell exporte un fichier XML tandis que l’interface Azure CLI exporte un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="24097-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="24097-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24097-114">PowerShell</span></span>
 
1. <span data-ttu-id="24097-115">[Installez Azure PowerShell et connectez-vous à Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24097-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="24097-116">Modifiez le répertoire (et assurez-vous qu’il existe) ainsi que le nom de fichier dans la commande suivante, selon vos besoins, puis exécutez la commande pour exporter le fichier config réseau :</span><span class="sxs-lookup"><span data-stu-id="24097-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="24097-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="24097-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="24097-118">[Installez l’interface de ligne de commande Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24097-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="24097-119">Effectuez les étapes restantes à partir d’une invite de commandes Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="24097-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="24097-120">Connectez-vous à Azure en entrant la commande `azure login`.</span><span class="sxs-lookup"><span data-stu-id="24097-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="24097-121">Assurez-vous que vous vous trouvez bien en mode ASM par le biais de la commande `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="24097-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="24097-122">Modifiez le répertoire (et assurez-vous qu’il existe) ainsi que le nom de fichier dans la commande suivante, selon vos besoins, puis exécutez la commande pour exporter le fichier config réseau :</span><span class="sxs-lookup"><span data-stu-id="24097-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="24097-123">Créer ou modifier un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="24097-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="24097-124">Un fichier config réseau est un fichier XML (lorsque vous utilisez PowerShell) ou un fichier JSON (lorsque vous utilisez l’interface de ligne de commande Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="24097-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="24097-125">Vous pouvez modifier le fichier dans n’importe quel éditeur de texte, ou XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="24097-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="24097-126">L’article [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) (Paramètres de schéma de fichier config réseau) inclut des informations détaillées pour tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="24097-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="24097-127">Pour obtenir des explications supplémentaires sur les paramètres, consultez [Afficher des réseaux virtuels et des paramètres](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="24097-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="24097-128">Les modifications apportées au fichier :</span><span class="sxs-lookup"><span data-stu-id="24097-128">The changes you make to the file:</span></span>

- <span data-ttu-id="24097-129">Doivent respecter le schéma, sans quoi l’importation du fichier config réseau échouera.</span><span class="sxs-lookup"><span data-stu-id="24097-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="24097-130">Remplacent les paramètres réseau existants de votre abonnement : soyez donc très vigilant lors de vos modifications.</span><span class="sxs-lookup"><span data-stu-id="24097-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="24097-131">Par exemple, servez-vous des exemples de fichier config réseau qui suivent.</span><span class="sxs-lookup"><span data-stu-id="24097-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="24097-132">Supposons que le fichier d’origine contienne deux instances **VirtualNetworkSite** et que vous l’avez modifié comme indiqué dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="24097-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="24097-133">Lorsque vous importez le fichier, Azure supprime le réseau virtuel de l’instance **VirtualNetworkSite** que vous avez supprimée dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="24097-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="24097-134">Ce scénario simplifié suppose qu’aucune ressource ne se trouve dans le réseau virtuel, car dans le cas contraire, le réseau virtuel ne pourrait pas être supprimé, et l’importation échouerait.</span><span class="sxs-lookup"><span data-stu-id="24097-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24097-135">Azure considère tout sous-réseau qui comprend des éléments déployés comme étant **« en cours d'utilisation »**.</span><span class="sxs-lookup"><span data-stu-id="24097-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="24097-136">Une fois le sous-réseau utilisé, il ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="24097-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="24097-137">Avant toute modification des informations de sous-réseau dans un fichier config réseau, déplacez tout ce que vous avez déployé sur le sous-réseau vers un autre sous-réseau qui n’est pas en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="24097-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="24097-138">Consultez [Déplacer une machine virtuelle ou une instance de rôle vers un autre sous-réseau](virtual-networks-move-vm-role-to-subnet.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="24097-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="24097-139">Exemple de code XML pour une utilisation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="24097-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="24097-140">L’exemple de fichier config réseau suivant crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* dans la région Azure *États-Unis de l’Est*.</span><span class="sxs-lookup"><span data-stu-id="24097-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="24097-141">Le réseau virtuel contient un sous-réseau nommé *mySubnet* avec le préfixe d’adresse *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="24097-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="24097-142">Si le fichier config réseau que vous avez exporté ne comporte aucun contenu, vous pouvez copier le code XML de l’exemple précédent et le coller dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="24097-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="24097-143">Exemple JSON pour une utilisation avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="24097-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="24097-144">L’exemple de fichier config réseau suivant crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* dans la région Azure *États-Unis de l’Est*.</span><span class="sxs-lookup"><span data-stu-id="24097-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="24097-145">Le réseau virtuel contient un sous-réseau nommé *mySubnet* avec le préfixe d’adresse *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="24097-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="24097-146">Si le fichier config réseau que vous avez exporté ne comporte aucun contenu, vous pouvez copier le code JSON de l’exemple précédent et le coller dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="24097-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="24097-147"><a name="import"></a>Importer un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="24097-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="24097-148">Vous pouvez utiliser PowerShell ou l’interface CLI Azure pour importer un fichier config réseau.</span><span class="sxs-lookup"><span data-stu-id="24097-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="24097-149">PowerShell importe un fichier XML tandis qu’Azure CLI importe un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="24097-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="24097-150">Si l’importation échoue, vérifiez que le fichier est compatible avec le [schéma de configuration réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="24097-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="24097-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24097-151">PowerShell</span></span>
 
1. <span data-ttu-id="24097-152">[Installez Azure PowerShell et connectez-vous à Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24097-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="24097-153">Modifiez le répertoire ainsi que le nom de fichier dans la commande suivante, selon vos besoins, puis exécutez la commande pour importer le fichier config réseau :</span><span class="sxs-lookup"><span data-stu-id="24097-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="24097-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="24097-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="24097-155">[Installez l’interface de ligne de commande Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="24097-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="24097-156">Effectuez les étapes restantes à partir d’une invite de commandes Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="24097-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="24097-157">Connectez-vous à Azure en entrant la commande `azure login`.</span><span class="sxs-lookup"><span data-stu-id="24097-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="24097-158">Assurez-vous que vous vous trouvez bien en mode ASM par le biais de la commande `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="24097-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="24097-159">Modifiez le répertoire ainsi que le nom de fichier dans la commande suivante, selon vos besoins, puis exécutez la commande pour importer le fichier config réseau :</span><span class="sxs-lookup"><span data-stu-id="24097-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
