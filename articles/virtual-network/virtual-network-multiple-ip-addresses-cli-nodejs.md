---
title: "aaaVM avec plusieurs adresses IP à l’aide de hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples à l’aide de machine virtuelle tooa hello Azure CLI 1.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Affecter plusieurs adresses IP des ordinateurs de toovirtual à l’aide de Azure CLI 1.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Cet article explique comment toocreate un ordinateur virtuel (VM) l’utilisation de modèle de déploiement Azure Resource Manager hello hello Azure CLI 1.0. Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP. toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP

Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 1.0 (cet article) ou hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello. Modifiez les noms des variables et les types d’adresses IP en fonction des besoins de votre implémentation.

1. Installer et configurer Azure CLI 1.0 par hello suivant les étapes de hello Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article et connectez-vous à votre compte Azure avec hello `azure-login` commande.

2. Créez un groupe de ressources :
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Créez un réseau virtuel :

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Créer un sous-réseau de réseau virtuel de hello :

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Créer un compte de stockage pour hello machine virtuelle. Avant d’exécuter hello suivant de commande, remplacez *mystorageaccount* avec un nom unique. nom de Hello doit être unique dans Azure :

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Créer des configurations IP, une carte réseau, hello et affecter hello IP configurations toohello carte réseau. Vous pouvez ajouter, supprimer ou modifier les configurations de hello selon les besoins. Hello, suivant les configurations est décrites dans le scénario de hello :

    **IPConfig-1**

    Entrez les commandes hello qui suivent toocreate :

    - une ressource d’adresse IP publique avec une adresse IP publique statique ;
    - Une carte de réseau, affectation d’adresse IP publique de hello et un tooit d’adresse IP privée statique.
    
    Remplacez *mypublicdns* avec un nom qui est unique au sein de hello emplacement Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.

    **IPConfig-2**

     Entrez hello suivant de commandes toocreate une nouvelle ressource d’adresse IP publique et une nouvelle configuration IP avec une adresse IP publique statique et une adresse IP privée statique :
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Entrez hello suivant de commandes toocreate une configuration IP avec une adresse IP privée statique et aucune adresse IP publique :

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Bien que cet article affecte tous les tooa de configurations IP carte réseau unique, vous pouvez également affecter tooany de configurations IP plusieurs cartes réseau dans une machine virtuelle. toolearn comment lu d’une machine virtuelle avec plusieurs cartes réseau, toocreate hello créer une machine virtuelle avec plusieurs cartes réseau article.

7. Créer une machine virtuelle Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    hello toochange v2 de tooStandard DS2 de taille de machine virtuelle, par exemple, ajoutez simplement hello suivant propriété `--vm-size Standard_DS3_v2` toohello `azure vm create` commande à l’étape 6.

8. Entrez hello suivant commande tooview hello NIC et hello des configurations IP associées :

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.

## <a name="add"></a>Ajouter tooa d’adresses IP virtuelle

Vous pouvez ajouter plus privé et public IP adresses tooan existant de carte réseau en effectuant les étapes hello qui suivent. les exemples Hello reposent sur hello [scénario](#Scenario) décrit dans cet article.

1. Ouvrez CLI d’Azure et complète hello restant des étapes de cette section au sein d’une seule session CLI. Si vous n’avez pas encore installé et configuré CLI d’Azure, hello terminé les étapes Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article et connectez-vous à votre compte Azure.

2. Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :

    - **Ajouter une adresse IP privée**
    
        tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP à l’aide de la commande hello ci-dessous. adresse Hello doit être une adresse non utilisée pour le sous-réseau de hello.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).

    - **Ajouter une adresse IP publique**
    
        Une adresse IP publique est ajoutée en l’associant tooeither une nouvelle configuration IP ou une configuration IP existante. Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.

        > [!NOTE]
        > Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.
        >

        **Associer hello ressource tooa nouvelle configuration IP**
    
        Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée. Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une. toocreate un nouveau, entrez hello de commande suivante :

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIP3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Associer la configuration IP existante de hello ressource tooan**

        Une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé. Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Recherchez un toohello similaire de ligne qui suit pour 3-IPConfig Bonjour retourné de sortie :

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Depuis hello **adresse IP publique** colonne *IpConfig-3* est vide, aucune ressource d’adresse IP publique n’est tooit actuellement associé. Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IPConfig-3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Afficher les adresses IP privées hello et hello toohello attribué ressources IP adresse publique carte réseau en entrant hello la commande suivante :

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hello retourné la sortie est similaire toohello suivantes :
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Ajouter des adresses IP privées de hello, vous avez ajouté le système d’exploitation VM toohello NIC toohello en suivant les instructions de hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresses toohello système d’exploitation.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
