---
title: "aaaCreate un réseau virtuel | Modèle de gestionnaire de ressources Azure | Documents Microsoft"
description: "Découvrez comment toocreate un virtuel réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Créer un réseau virtuel à l’aide d’un modèle Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure propose deux modèles de déploiement : Azure Resource Manager et classique. Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello. toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.
 
Cet article explique comment toocreate un réseau virtuel via le déploiement du Gestionnaire de ressources hello modèle à l’aide d’un modèle Azure Resource Manager. Vous pouvez également créer un réseau virtuel via le Gestionnaire de ressources à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique hello en sélectionnant une option différente de hello suivant liste :

> [!div class="op_single_selector"]
- [Portail](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [INTERFACE DE LIGNE DE COMMANDE](virtual-networks-create-vnet-arm-cli.md)
- [Modèle](virtual-networks-create-vnet-arm-template-click.md)
- [Portail (classique)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (classique)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [Interface de ligne de commande (classique)](virtual-networks-create-vnet-classic-cli.md)

Vous allez apprendre comment toodownload et modifier existant modèle ARM à partir de GitHub et déployer le modèle hello à partir de GitHub, PowerShell et hello CLI d’Azure.

Si vous déployez simplement modèle ARM de hello directement à partir de GitHub, sans aucune modification, ignorez trop[déployer un modèle à partir de github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Télécharger et de comprendre le modèle de gestionnaire de ressources Azure hello
Vous pouvez télécharger le modèle existant de hello pour la création d’un réseau virtuel et deux sous-réseaux à partir de GitHub, apporter des modifications que vous souhaitez et la réutiliser. toodo effectuez donc hello comme suit :

1. Accédez trop[page de modèle exemple hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Cliquez sur **azuredeploy.json**, puis sur **RAW**.
3. Enregistrez hello fichier tooa un dossier local sur votre ordinateur.
4. Si vous êtes familiarisé avec les modèles, passez toostep 7.
5. Ouvrir le fichier hello vous venez d’enregistrer et d’examiner le contenu de hello sous **paramètres** à la ligne 5. Les paramètres de modèle ARM fournissent un espace réservé pour les valeurs à remplir lors du déploiement.
   
   | Paramètre | Description |
   | --- | --- |
   | **location** |Région Azure où hello réseau virtuel sera créé |
   | **vnetName** |Nom de hello nouveau réseau virtuel |
   | **addressPrefix** |Espace d’adressage pour hello réseau virtuel, au format CIDR |
   | **subnet1Name** |Nom de hello premier réseau virtuel |
   | **subnet1Prefix** |Bloc CIDR pour le premier sous-réseau de hello |
   | **subnet2Name** |Nom de hello deuxième réseau virtuel |
   | **subnet2Prefix** |Bloc CIDR pour le sous-réseau de deuxième hello |
   
   > [!IMPORTANT]
   > Les modèles Azure Resource Manager de GitHub sont susceptibles d’évoluer. Vérifiez le modèle de hello avant de l’utiliser.
   > 
   > 
6. Vérifiez le contenu de hello sous **ressources** et notez les éléments suivants de hello :
   
   * **type**. Type de ressource en cours de création par le modèle de hello. Dans ce cas, **Microsoft.Network/virtualNetworks**, qui représente un réseau virtuel.
   * **name**. Nom de ressource de hello. Utilisation de hello avis de **[parameters('vnetName')]**, qui signifie hello sera nom fourni en tant qu’entrée par l’utilisateur de hello ou un fichier de paramètres au cours du déploiement.
   * **properties**. Liste de propriétés pour la ressource de hello. Ce modèle utilise les propriétés d’espace et le sous-réseau d’adresse hello lors de la création du réseau virtuel.
7. Naviguer vers l’arrière trop[page de modèle exemple hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Cliquez sur **azuredeploy-paremeters.json**, puis cliquez sur **RAW**.
9. Enregistrez hello fichier tooa un dossier local sur votre ordinateur.
10. Ouvrez le fichier hello que vous venez d’enregistrer et modifier des valeurs de hello pour les paramètres de hello. Utilisez hello valeurs ci-dessous toodeploy hello hello scénario de réseau virtuel suivantes :

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. Enregistrez le fichier de hello.


## <a name="deploy-hello-template-using-powershell"></a>Déployer le modèle de hello à l’aide de PowerShell

Hello complet suivant le modèle de hello toodeploy étapes que vous avez téléchargé à l’aide de PowerShell :

1. Installer et configurer Azure PowerShell en effectuant les étapes hello Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Exécutez hello suivant commande toocreate un groupe de ressources :

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    commande Hello crée un groupe de ressources nommé *TestRG* Bonjour *du centre des États-Unis* région azure. Pour plus d’informations sur les groupes de ressources, consultez [Présentation d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    Sortie attendue :

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Exécutez hello toodeploy hello nouveau réseau virtuel à l’aide de fichiers de modèle et le paramètre hello vous avez téléchargé et de modifier les propriétés de commande suivante :

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Sortie attendue :
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. Suivante d’exécution hello commande tooview des propriétés de hello Hello nouveau réseau virtuel :

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Sortie attendue :

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a>Déployer à l’aide de clic sur le déploiement de modèle de hello

Vous pouvez réutiliser prédéfini Azure Resource Manager modèles tooa téléchargé GitHub espace de stockage géré par Microsoft et la Communauté de toohello ouvert. Ces modèles peuvent être déployées directement GitHub, ou téléchargé et modifié toofit à vos besoins. toodeploy un modèle qui crée un réseau virtuel avec deux sous-réseaux, hello complète comme suit :

1. À partir d’un navigateur, accédez trop[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Faites défiler la liste hello des modèles et cliquez sur **101-réseau virtuel-deux sous-réseaux**. Vérifiez hello **README.md** de fichiers, comme indiqué ci-dessous.

    ![Fichier READEME.md dans GitHub](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Cliquez sur **déployer tooAzure**. Si nécessaire, entrez vos informations d’identification Azure. 
4. Bonjour **paramètres** panneau, entrez les valeurs hello vous souhaitez toouse toocreate votre nouveau réseau virtuel, puis cliquez sur **OK**. Hello figure ci-dessous illustre les valeurs hello pour le scénario de hello :
   
    ![Paramètres de modèle ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Cliquez sur **groupe de ressources** et sélectionnez hello virtuel à un tooadd de groupe de ressources, ou cliquez sur **nouvel** tooadd hello réseau virtuel tooa nouveau groupe de ressources. Hello figure suivante montre les ressources hello paramètres de groupe pour un groupe de ressources appelé **TestRG**:

    ![Groupe de ressources](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Si nécessaire, modifiez hello **abonnement** et **emplacement** paramètres pour votre réseau virtuel.
7. Si vous ne souhaitez pas toosee hello réseau virtuel sous forme de vignette Bonjour **tableau d’accueil**, désactiver **tooStartboard du code confidentiel**.
8. Cliquez sur **juridiques**, lisez les termes du contrat de hello, puis cliquez sur **acheter** tooagree. 
9. Cliquez sur **créer** toocreate hello réseau virtuel.
   
    ![Mosaïque d’envoi d’un déploiement dans le portail en version préliminaire](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Une fois le déploiement de hello, Bonjour Azure portal cliquez sur **davantage de services**, type *réseaux virtuels* dans la zone de filtre hello qui s’affiche, puis cliquez sur Panneau de réseaux de virtuel réseaux toosee hello virtuel. Dans le panneau de hello, cliquez sur *TestVNet*. Bonjour *TestVNet* panneau, cliquez sur **sous-réseaux** toosee des sous-réseaux hello créé, comme indiqué dans hello illustration suivante :
    
     ![Créer un réseau virtuel dans le portail en version préliminaire](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooconnect :

- Un réseau virtuel tooa de machine virtuelle (VM) par la lecture de hello [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [créer un VM Linux](../virtual-machines/linux/quick-create-portal.md) articles. Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.
- Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) l’article.
- Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute. Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-arm.md) articles.
