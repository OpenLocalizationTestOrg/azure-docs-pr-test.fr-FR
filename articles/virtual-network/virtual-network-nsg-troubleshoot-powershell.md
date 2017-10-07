---
title: "aaaTroubleshoot des groupes de sécurité réseau - PowerShell | Documents Microsoft"
description: "Découvrez comment les groupes de sécurité réseau tootroubleshoot dans un déploiement d’Azure Resource Manager hello modèle à l’aide d’Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Résoudre les groupes de sécurité réseau à l’aide d’Azure PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Si vous configuré des groupes de sécurité réseau (NSG) sur votre machine virtuelle (VM) et qui rencontrent des problèmes de connectivité de machine virtuelle, cet article fournit une vue d’ensemble des fonctionnalités des diagnostics pour les groupes de sécurité réseau toohelp dépannage.

Groupes de sécurité réseau permettent de types de hello toocontrol de trafic ce flux et vos machines virtuelles (VM). Groupes de sécurité réseau peuvent être appliqués toosubnets dans un réseau virtuel de Azure (VNet), les interfaces de réseau (NIC) ou les deux. Hello efficace règles appliquées tooa NIC sont un regroupement de règles hello qui existent dans hello NSG appliqué tooa NIC hello sous-réseau et il est connecté à. Les règles appliquées à ces groupes de sécurité réseau sont parfois en conflit entre elles et peuvent avoir une incidence sur la connectivité réseau d’une machine virtuelle.  

Vous pouvez afficher toutes les règles de sécurité efficace hello à partir de vos groupes de sécurité réseau, tel qu’appliqué sur les cartes d’interface réseau de votre machine virtuelle. Cet article explique comment tootroubleshoot des problèmes de connectivité de la machine virtuelle à l’aide de ces règles dans hello modèle de déploiement Azure Resource Manager. Si vous n’êtes pas familiarisé avec les concepts de réseau virtuel et le groupe de sécurité réseau, lire hello [réseau virtuel](virtual-networks-overview.md) et [groupes de sécurité réseau](virtual-networks-nsg.md) articles de vue d’ensemble.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>À l’aide de flux de trafic des règles de sécurité efficace tootroubleshoot machine virtuelle
scénario Hello qui suit est un exemple d’un problème de connexion courantes :

Une machine virtuelle nommée *VM1* fait partie d’un sous-réseau nommé *Subnet1* au sein d’un réseau virtuel nommé *WestUS-VNet1*. Un toohello tooconnect de tentative de machine virtuelle à l’aide du protocole RDP sur le port TCP 3389 échoue. Groupes de sécurité réseau sont appliquées sur les deux cartes réseau hello *NIC1 de VM1* et hello sous-réseau *Subnet1*. Le port du trafic tooTCP 3389 est autorisé dans hello NSG associée à interface réseau de hello *NIC1 de VM1*toutefois TCP ping échoue de tooVM1 port 3389.

Bien que cet exemple utilise le port TCP 3389, hello comme suit peut être utilisé toodetermine échecs de connexion entrant et sortant sur n’importe quel port.

## <a name="detailed-troubleshooting-steps"></a>Étapes de dépannage détaillées
Terminer hello suivant les étapes tootroubleshoot groupes de sécurité réseau pour une machine virtuelle :

1. Démarrer un tooAzure de session et de connexion Azure PowerShell. Si vous n’êtes pas familiarisé avec l’utilisation d’Azure PowerShell, lire hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Entrez hello commande tooreturn toutes les règles du groupe de sécurité réseau appliquent tooa carte réseau nommée suivante *NIC1 de VM1* dans le groupe de ressources hello *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Si vous ne connaissez pas nom hello d’une carte réseau, entrez hello commande tooretrieve hello nom de toutes les cartes réseau dans un groupe de ressources : 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Hello texte suivant est un exemple de sortie de règles efficaces de hello retournée pour hello *NIC1 de VM1* carte réseau :
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Notez hello informations dans la sortie de hello suivantes :
   
   * Il existe deux sections **NetworkSecurityGroup** : l’une est associée à un sous-réseau (*Subnet1*), et l’autre à une carte d’interface réseau (*VM1-NIC1*). Dans cet exemple, un groupe de sécurité réseau a été appliqué tooeach.
   * **Association** montre les ressources de hello (carte réseau ou sous-réseau) à un groupe de sécurité réseau donné est associé. Si hello ressource du groupe de sécurité réseau est déplacée/dissocié immédiatement avant d’exécuter cette commande, vous devrez peut-être toowait quelques secondes pour tooreflect de modification hello dans la sortie de la commande hello. 
   * les noms de règle qui sont précédés de Hello *defaultSecurityRules*: quand un groupe de sécurité réseau est créé, plusieurs règles de sécurité par défaut sont créés dans celui-ci. Vous ne pouvez pas supprimer des règles par défaut, mais vous pouvez les remplacer par des règles de priorité plus élevée.
     Hello de lecture [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md#default-rules) toolearn article en savoir plus sur le groupe de sécurité réseau par défaut des règles de sécurité.
   * **ExpandedAddressPrefix** développe les préfixes d’adresse hello pour les étiquettes de groupe de sécurité réseau par défaut. Les balises représentent plusieurs préfixes d’adresse. Expansion de balises de hello peut être utile lors de la résolution des problèmes de connectivité de machine virtuelle à partir de préfixes d’adresse spécifique. Par exemple, avec le réseau virtuel d’homologation, balise VIRTUAL_NETWORK développe tooshow homologuer les préfixes de réseau virtuel dans la sortie précédente hello.
     
     > [!NOTE]
     > Bonjour commande effective règles affiche uniquement si un groupe de sécurité réseau est associé à un sous-réseau, une carte réseau ou les deux. Une machine virtuelle peut avoir plusieurs cartes d’interface réseau à laquelle différents groupes de sécurité réseau sont appliqués. Lors de la résolution du problème, exécutez la commande hello pour chaque carte réseau.
     > 
     > 
3. tooease le filtrage sur un plus grand nombre de règles du groupe de sécurité réseau, entrez hello suivant tootroubleshoot des commandes supplémentaires : 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Un filtre pour le trafic RDP (port TCP 3389), est appliqué toohello affichage de grille, comme indiqué dans hello illustration suivante :
   
    ![Liste des règles](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Comme vous pouvez le voir dans l’affichage de grille hello, il existe deux autorisent et refuser des règles pour RDP. sortie de l’étape 2 Hello indique que hello *DenyRDP* règle est Bonjour NSG appliqué toohello sous-réseau. Pour les règles de trafic entrant, groupes de sécurité réseau appliquées toohello sous-réseau sont traitées en premier. Si une correspondance est trouvée, l’interface de réseau toohello hello NSG appliqué n’est pas traitée. Dans ce cas, hello *DenyRDP* de règle de sous-réseau de hello bloque RDP toohello VM (**VM1**).
   
   > [!NOTE]
   > Une machine virtuelle peut avoir plusieurs tooit de cartes réseau attachée. Chacun peut être connecté tooa autre sous-réseau. Étant donné que les commandes hello dans les étapes précédentes hello sont exécutées sur une carte réseau, il est important de tooensure que vous spécifiez hello carte réseau que vous rencontrez Échec de connectivité hello. Si vous n’êtes pas sûr, vous pouvez toujours exécuter des commandes hello sur chaque machine virtuelle de toohello carte réseau attachée.
   > 
   > 
5. tooRDP dans VM1, modification hello *refuser RDP (3389)* trop de règles*autoriser les RDP(3389)* Bonjour **Subnet1-groupe de sécurité réseau** groupe de sécurité réseau. Vérifiez que le port TCP 3389 est ouvert en ouvrant un toohello de connexion RDP machine virtuelle ou en utilisant l’outil PsPing de hello. Vous pouvez en savoir plus sur PsPing par la lecture de hello [page de téléchargement PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Vous pouvez ou supprimez des règles à partir d’un groupe de sécurité réseau en utilisant les informations de hello sortie hello hello de commande suivante :
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Considérations
Tenez compte des points suivants lors de la résolution des problèmes de connectivité de hello :

* Règles du groupe de sécurité réseau par défaut bloque l’accès entrant à partir de hello internet et seulement ce réseau virtuel qui permet le trafic entrant. Les règles doivent être ajoutés explicitement tooallow accès entrant depuis Internet, en fonction des besoins.
* S’il n’y a aucune règle de sécurité groupe de sécurité réseau à l’origine de toofail de connectivité de réseau de l’ordinateur virtuel, problème de hello peut être due à :
  * Logiciel de pare-feu qui s’exécutent dans le système d’exploitation de la machine virtuelle hello
  * Itinéraires configurés pour des appliances virtuelles ou un trafic local. Le trafic Internet peut être redirigé tooon-site via le tunneling forcé. Une connexion RDP/SSH à partir de hello Internet tooyour machine virtuelle peut ne pas fonctionne avec ce paramètre, selon la façon dont le matériel de réseau local hello gère ce trafic. Hello de lecture [dépannage des itinéraires](virtual-network-routes-troubleshoot-powershell.md) article toolearn, comment les problèmes d’itinéraire toodiagnose qui peuvent être compromettent hello flux du trafic et se déconnecte de hello machine virtuelle. 
* Si vous avez homologuer les réseaux virtuels, par défaut, hello balise VIRTUAL_NETWORK développe automatiquement les préfixes tooinclude pour les réseaux virtuels de ressources. Vous pouvez afficher ces préfixes Bonjour **ExpandedAddressPrefix** répertorier, tootroubleshoot tout tooVNet connexes de problèmes d’homologation de connectivité. 
* Les règles de sécurité efficace sont affichent uniquement s’il existe qu'un groupe de sécurité réseau associé à la machine virtuelle hello NIC et ou un sous-réseau. 
* Si aucun groupes de sécurité réseau associés hello carte réseau ou sous-réseau et que vous avez une adresse IP publique affectée tooyour machine virtuelle, tous les ports seront ouverts pour un accès entrant et sortant. Si hello machine virtuelle a une adresse IP publique, appliquer des groupes de sécurité réseau toohello carte réseau ou sous-réseau est fortement recommandé.  

