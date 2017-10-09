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
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Configurer un réseau virtuel (Classic) à l’aide d’un fichier config réseau
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle de déploiement du Gestionnaire de ressources hello.

Vous pouvez créer et configurer un réseau virtuel (classiques) avec un fichier de configuration de réseau à l’aide de hello Azure interface de ligne de commande (CLI) 1.0 ou Azure PowerShell. Impossible de créer ou modifier un réseau virtuel via le modèle de déploiement hello Azure Resource Manager à l’aide d’un fichier de configuration réseau. Impossible d’utiliser hello toocreate portail Azure ou modifier un réseau virtuel (classiques) à l’aide d’un fichier de configuration réseau, vous pouvez utiliser hello toocreate portail Azure (classique), un réseau virtuel sans utiliser un fichier de configuration réseau.

Création et configuration d’un réseau virtuel (classiques) avec un fichier de configuration réseau requièrent l’exportation, la modification et l’importation du fichier de hello.

## <a name="export"></a>Exporter un fichier config réseau

Vous pouvez utiliser PowerShell ou hello CLI d’Azure tooexport un fichier de configuration réseau. PowerShell exporte un fichier XML, tandis que hello CLI d’Azure exporte un fichier json.

### <a name="powershell"></a>PowerShell
 
1. [Installez Azure PowerShell et connectez-vous à tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Changer de répertoire de hello (et assurez-vous qu’il existe) et le nom de fichier dans hello suivant de commande en tant que souhaité, puis exécution hello commande tooexport hello fichier de configuration réseau :

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Installer hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Terminer hello restant des étapes à partir d’une invite de commandes Azure CLI 1.0.
2. Se connecter en entrant hello tooAzure `azure login` commande.
3. Vérifiez le mode asm en entrant hello `azure config mode asm` commande.
4. Changer de répertoire de hello (et assurez-vous qu’il existe) et le nom de fichier dans hello suivant de commande en tant que souhaité, puis exécution hello commande tooexport hello fichier de configuration réseau :
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Créer ou modifier un fichier config réseau

Un fichier de configuration de réseau est un fichier XML (lors de l’utilisation de PowerShell) ou un fichier json (quand vous utilisez hello CLI d’Azure). Vous pouvez modifier le fichier hello dans n’importe quel éditeur de texte, ou XML/json. Hello [les paramètres de schéma de fichier de configuration du réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx) article inclut des informations détaillées pour tous les paramètres. Pour obtenir des explications supplémentaires des paramètres de hello, consultez [afficher les paramètres et les réseaux virtuels](virtual-network-manage-network.md#view-vnet). Hello apportées toohello fichier :

- Doit être compatible avec le schéma de hello ou importation hello réseau fichier de configuration échoue.
- Remplacent les paramètres réseau existants de votre abonnement : soyez donc très vigilant lors de vos modifications. Par exemple, référencer des fichiers de configuration du réseau d’exemple hello qui suivent. Par exemple hello le fichier d’origine contenait deux **VirtualNetworkSite** instances et vous modifié, comme indiqué dans les exemples hello. Lorsque vous importez le fichier de hello, Azure supprime le réseau virtuel hello hello **VirtualNetworkSite** instance que vous avez supprimé dans le fichier de hello. Ce scénario simplifié suppose aucune ressource se trouvaient dans le réseau virtuel de hello, comme si elle existait, réseau virtuel de hello n’a pas pu être supprimé, et importation de hello échouerait.

> [!IMPORTANT]
> Azure considère un sous-réseau que quelque chose a déployé tooit comme **en cours d’utilisation**. Une fois le sous-réseau utilisé, il ne peut pas être modifié. Avant de modifier les informations de sous-réseau dans un fichier de configuration réseau, déplacez tout ce que vous avez déployé toohello sous-réseau tooa sous-réseau différent qui n’est pas en cours de modification. Consultez [déplacer un sous-réseau différent de tooa machine virtuelle ou Instance de rôle](virtual-networks-move-vm-role-to-subnet.md) pour plus d’informations.

### <a name="example-xml-for-use-with-powershell"></a>Exemple de code XML pour une utilisation avec PowerShell

fichier de configuration de réseau suivant exemple Hello crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* Bonjour *États-Unis* Azure région. réseau virtuel de Hello contient un sous-réseau nommé *mySubnet* avec un préfixe d’adresse *10.0.0.0/24*.

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

Si le fichier de configuration de réseau hello que vous exportées ne contient aucuns contenu, vous pouvez copier hello XML dans l’exemple précédent de hello et collez-le dans un nouveau fichier.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Exemple de JSON pour une utilisation avec hello Azure CLI 1.0

fichier de configuration de réseau suivant exemple Hello crée un réseau virtuel nommé *myVirtualNetwork* avec un espace d’adressage *10.0.0.0/16* Bonjour *États-Unis* Azure région. réseau virtuel de Hello contient un sous-réseau nommé *mySubnet* avec un préfixe d’adresse *10.0.0.0/24*.

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

Si le fichier de configuration de réseau hello que vous exportées ne contient aucuns contenu, vous pouvez copier hello json dans l’exemple précédent de hello et collez-le dans un nouveau fichier.

## <a name="import"></a>Importer un fichier config réseau

Vous pouvez utiliser PowerShell ou hello CLI d’Azure tooimport un fichier de configuration réseau. PowerShell importe un fichier XML, tandis que hello CLI d’Azure importe un fichier json. Si hello importation échoue, vérifiez que hello est conforme à hello [schéma de configuration réseau](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Installez Azure PowerShell et connectez-vous à tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Modifier le répertoire de hello et le fichier Bonjour suivant de commande si nécessaire, puis exécutez le fichier de configuration de réseau hello commande tooimport hello :
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Installer hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Terminer hello restant des étapes à partir d’une invite de commandes Azure CLI 1.0.
2. Se connecter en entrant hello tooAzure `azure login` commande.
3. Vérifiez le mode asm en entrant hello `azure config mode asm` commande.
4. Modifier le répertoire de hello et le fichier Bonjour suivant de commande si nécessaire, puis exécutez le fichier de configuration de réseau hello commande tooimport hello :

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
