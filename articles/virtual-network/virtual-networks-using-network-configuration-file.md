---
title: "aaaConfigure un le réseau virtuel Azure (classique) - fichier de configuration réseau | Documents Microsoft"
description: "Découvrez comment toocreate et modifier des réseaux virtuels (classiques) à exporter, modifier et l’importation d’un fichier de configuration réseau."
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
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="1c67c-103">Configurer un réseau virtuel (Classic) à l’aide d’un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="1c67c-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1c67c-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c67c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1c67c-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1c67c-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="1c67c-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1c67c-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="1c67c-107">Vous pouvez créer et configurer un réseau virtuel (classiques) avec un fichier de configuration de réseau à l’aide de hello Azure interface de ligne de commande (CLI) 1.0 ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c67c-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="1c67c-108">Impossible de créer ou modifier un réseau virtuel via le modèle de déploiement hello Azure Resource Manager à l’aide d’un fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="1c67c-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="1c67c-109">Impossible d’utiliser hello toocreate portail Azure ou modifier un réseau virtuel (classiques) à l’aide d’un fichier de configuration réseau, vous pouvez utiliser hello toocreate portail Azure (classique), un réseau virtuel sans utiliser un fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="1c67c-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="1c67c-110">Création et configuration d’un réseau virtuel (classiques) avec un fichier de configuration réseau requièrent l’exportation, la modification et l’importation du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="1c67c-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="1c67c-111"><a name="export"></a>Exporter un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="1c67c-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="1c67c-112">Vous pouvez utiliser PowerShell ou hello CLI d’Azure tooexport un fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="1c67c-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="1c67c-113">PowerShell exporte un fichier XML, tandis que hello CLI d’Azure exporte un fichier json.</span><span class="sxs-lookup"><span data-stu-id="1c67c-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="1c67c-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c67c-114">PowerShell</span></span>
 
1. <span data-ttu-id="1c67c-115">[Installez Azure PowerShell et connectez-vous à tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c67c-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="1c67c-116">Changer de répertoire de hello (et assurez-vous qu’il existe) et le nom de fichier dans hello suivant de commande en tant que souhaité, puis exécution hello commande tooexport hello fichier de configuration réseau :</span><span class="sxs-lookup"><span data-stu-id="1c67c-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="1c67c-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c67c-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="1c67c-118">[Installer hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c67c-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1c67c-119">Terminer hello restant des étapes à partir d’une invite de commandes Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1c67c-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="1c67c-120">Se connecter en entrant hello tooAzure `azure login` commande.</span><span class="sxs-lookup"><span data-stu-id="1c67c-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="1c67c-121">Vérifiez le mode asm en entrant hello `azure config mode asm` commande.</span><span class="sxs-lookup"><span data-stu-id="1c67c-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="1c67c-122">Changer de répertoire de hello (et assurez-vous qu’il existe) et le nom de fichier dans hello suivant de commande en tant que souhaité, puis exécution hello commande tooexport hello fichier de configuration réseau :</span><span class="sxs-lookup"><span data-stu-id="1c67c-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="1c67c-123">Créer ou modifier un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="1c67c-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="1c67c-124">Un fichier de configuration de réseau est un fichier XML (lors de l’utilisation de PowerShell) ou un fichier json (quand vous utilisez hello CLI d’Azure).</span><span class="sxs-lookup"><span data-stu-id="1c67c-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="1c67c-125">Vous pouvez modifier le fichier hello dans n’importe quel éditeur de texte, ou XML/json.</span><span class="sxs-lookup"><span data-stu-id="1c67c-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="1c67c-126">Hello [les paramètres de schéma de fichier de configuration du réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx) article inclut des informations détaillées pour tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="1c67c-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="1c67c-127">Pour obtenir des explications supplémentaires des paramètres de hello, consultez [afficher les paramètres et les réseaux virtuels](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="1c67c-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="1c67c-128">Hello apportées toohello fichier :</span><span class="sxs-lookup"><span data-stu-id="1c67c-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="1c67c-129">Doit être compatible avec le schéma de hello ou importation hello réseau fichier de configuration échoue.</span><span class="sxs-lookup"><span data-stu-id="1c67c-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="1c67c-130">Remplacent les paramètres réseau existants de votre abonnement : soyez donc très vigilant lors de vos modifications.</span><span class="sxs-lookup"><span data-stu-id="1c67c-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="1c67c-131">Par exemple, référencer des fichiers de configuration du réseau d’exemple hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="1c67c-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="1c67c-132">Par exemple hello le fichier d’origine contenait deux **VirtualNetworkSite** instances et vous modifié, comme indiqué dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="1c67c-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="1c67c-133">Lorsque vous importez le fichier de hello, Azure supprime le réseau virtuel hello hello **VirtualNetworkSite** instance que vous avez supprimé dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="1c67c-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="1c67c-134">Ce scénario simplifié suppose aucune ressource se trouvaient dans le réseau virtuel de hello, comme si elle existait, réseau virtuel de hello n’a pas pu être supprimé, et importation de hello échouerait.</span><span class="sxs-lookup"><span data-stu-id="1c67c-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c67c-135">Azure considère un sous-réseau que quelque chose a déployé tooit comme **en cours d’utilisation**.</span><span class="sxs-lookup"><span data-stu-id="1c67c-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="1c67c-136">Une fois le sous-réseau utilisé, il ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="1c67c-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="1c67c-137">Avant de modifier les informations de sous-réseau dans un fichier de configuration réseau, déplacez tout ce que vous avez déployé toohello sous-réseau tooa sous-réseau différent qui n’est pas en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="1c67c-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="1c67c-138">Consultez [déplacer un sous-réseau différent de tooa machine virtuelle ou Instance de rôle](virtual-networks-move-vm-role-to-subnet.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1c67c-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="1c67c-139">Exemple de code XML pour une utilisation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c67c-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="1c67c-140">fichier de configuration de réseau suivant exemple Hello crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* Bonjour *États-Unis* Azure région.</span><span class="sxs-lookup"><span data-stu-id="1c67c-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="1c67c-141">réseau virtuel de Hello contient un sous-réseau nommé *mySubnet* avec un préfixe d’adresse *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1c67c-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="1c67c-142">Si le fichier de configuration de réseau hello que vous exportées ne contient aucuns contenu, vous pouvez copier hello XML dans l’exemple précédent de hello et collez-le dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="1c67c-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="1c67c-143">Exemple de JSON pour une utilisation avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c67c-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="1c67c-144">fichier de configuration de réseau suivant exemple Hello crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* Bonjour *États-Unis* Azure région.</span><span class="sxs-lookup"><span data-stu-id="1c67c-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="1c67c-145">réseau virtuel de Hello contient un sous-réseau nommé *mySubnet* avec un préfixe d’adresse *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1c67c-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="1c67c-146">Si le fichier de configuration de réseau hello que vous exportées ne contient aucuns contenu, vous pouvez copier hello json dans l’exemple précédent de hello et collez-le dans un nouveau fichier.</span><span class="sxs-lookup"><span data-stu-id="1c67c-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="1c67c-147"><a name="import"></a>Importer un fichier config réseau</span><span class="sxs-lookup"><span data-stu-id="1c67c-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="1c67c-148">Vous pouvez utiliser PowerShell ou hello CLI d’Azure tooimport un fichier de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="1c67c-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="1c67c-149">PowerShell importe un fichier XML, tandis que hello CLI d’Azure importe un fichier json.</span><span class="sxs-lookup"><span data-stu-id="1c67c-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="1c67c-150">Si hello importation échoue, vérifiez que hello est conforme à hello [schéma de configuration réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c67c-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="1c67c-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c67c-151">PowerShell</span></span>
 
1. <span data-ttu-id="1c67c-152">[Installez Azure PowerShell et connectez-vous à tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c67c-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="1c67c-153">Modifier le répertoire de hello et le fichier Bonjour suivant de commande si nécessaire, puis exécutez le fichier de configuration de réseau hello commande tooimport hello :</span><span class="sxs-lookup"><span data-stu-id="1c67c-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="1c67c-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1c67c-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="1c67c-155">[Installer hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c67c-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1c67c-156">Terminer hello restant des étapes à partir d’une invite de commandes Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1c67c-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="1c67c-157">Se connecter en entrant hello tooAzure `azure login` commande.</span><span class="sxs-lookup"><span data-stu-id="1c67c-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="1c67c-158">Vérifiez le mode asm en entrant hello `azure config mode asm` commande.</span><span class="sxs-lookup"><span data-stu-id="1c67c-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="1c67c-159">Modifier le répertoire de hello et le fichier Bonjour suivant de commande si nécessaire, puis exécutez le fichier de configuration de réseau hello commande tooimport hello :</span><span class="sxs-lookup"><span data-stu-id="1c67c-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
