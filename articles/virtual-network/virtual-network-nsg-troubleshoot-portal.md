---
title: "aaaTroubleshoot des groupes de sécurité réseau - portail | Documents Microsoft"
description: "Découvrez comment tootroubleshoot des groupes de sécurité réseau dans un déploiement d’Azure Resource Manager hello modèle à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Résoudre les problèmes de groupes de sécurité réseau à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [portail Azure](virtual-network-nsg-troubleshoot-portal.md)
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

### <a name="vm"></a>Afficher les règles de sécurité effectives pour une machine virtuelle
Terminer hello suivant les étapes tootroubleshoot groupes de sécurité réseau pour une machine virtuelle :

Vous pouvez afficher la liste complète des règles de sécurité efficace hello sur une carte réseau, à partir de la machine virtuelle proprement dite de hello. Vous pouvez également ajouter, modifier et supprimer des règles de groupe de sécurité réseau NIC et sous-réseau dans Panneau de règles efficaces hello, si vous disposez d’autorisations tooperform ces opérations.

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **davantage de services**, puis cliquez sur **virtuels** dans la liste hello qui s’affiche.
3. Sélectionnez un tootroubleshoot de machine virtuelle à partir de la liste hello qui s’affiche et un panneau de machine virtuelle avec les options s’affiche.
4. Cliquez sur **Diagnostiquer et résoudre les problèmes**, puis sélectionnez un problème courant. Pour cet exemple, **je ne peux pas me connecter toomy machine virtuelle Windows** est sélectionnée. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Étapes s’affichent sous le problème de hello, comme indiqué dans hello illustration suivante : 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Cliquez sur *les règles de groupe de sécurité efficace* dans la liste hello des étapes recommandées.
6. Hello **obtenir des règles de sécurité efficace** panneau s’affiche, comme indiqué dans hello illustration suivante :
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Notez hello les sections suivantes de l’image de hello :
   
   * **Étendue :** défini trop*VM1*, hello machine virtuelle sélectionnée à l’étape 3.
   * **Interface réseau :***VM1-NIC1* est sélectionné. Une machine virtuelle peut avoir plusieurs interfaces réseau. Chaque carte réseau peut avoir des règles de sécurité effectives uniques. Lors de la résolution des problèmes, vous devrez peut-être les règles de sécurité efficace tooview hello pour chaque carte réseau.
   * **Groupes de sécurité réseau associés :** groupes de sécurité réseau peuvent être appliqués tooboth hello des cartes réseau et hello sous-réseau hello carte réseau est connectée à. Dans l’image de hello, un groupe de sécurité réseau a été tooboth appliqué hello des cartes réseau et hello sous-réseau à qu'il est connecté. Vous pouvez cliquer sur les noms de groupe de sécurité réseau hello toodirectly modifier les règles Bonjour groupes de sécurité réseau.
   * **Onglet de VM1-groupe de sécurité réseau :** hello la liste des règles affichées dans l’image de hello est pour hello NSG appliqué toohello carte Azure crée plusieurs règles par défaut à chaque création d’un groupe de sécurité réseau. Vous ne pouvez pas supprimer les règles par défaut de hello, mais vous pouvez remplacer les règles de priorité plus élevée. toolearn plus d’informations sur les règles par défaut, lire hello [vue d’ensemble du groupe de sécurité réseau](virtual-networks-nsg.md#default-rules) l’article.
   * **Colonne de DESTINATION :** certaines des règles de hello que du texte dans la colonne de hello, tandis que d’autres préfixes d’adresse. texte Hello est nom hello de règle de sécurité de toohello balises appliquées par défaut lors de sa création. les balises de Hello sont des identificateurs fournis par le système qui représentent plusieurs préfixes. Sélection d’une règle avec une balise, tel que *AllowInternetOutBound*, répertorie les préfixes hello Bonjour **préfixes d’adresse** panneau.
   * **Télécharger :** liste hello de règles peut être longue. Vous pouvez télécharger un fichier .csv de règles de hello pour l’analyse hors connexion en cliquant sur **télécharger** et en enregistrant le fichier de hello.
   * **AllowRDP** règle de trafic entrant : cette règle permet de toohello des connexions RDP machine virtuelle.
7. Cliquez sur hello **Subnet1-NSG** onglet tooview hello efficace les règles de hello NSG appliquées toohello sous-réseau, comme indiqué dans hello illustration suivante : 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Hello d’avis *denyRDP* **entrant** règle. Règles de trafic entrant appliqués au sous-réseau de hello sont évaluées avant les règles appliquées à l’interface de réseau hello. Puisque hello refuser la règle est appliquée au sous-réseau de hello, hello demande tooconnect tooTCP 3389 échoue car la règle d’autorisation hello en hello carte réseau n’est jamais évalué. 
   
    Hello *denyRDP* règle est la raison hello pourquoi hello connexion RDP échoue. Sa suppression doit résoudre hello.
   
   > [!NOTE]
   > Si hello VM associé avec hello carte réseau n’est pas en cours d’exécution, ou groupes de sécurité réseau n’ont pas été appliqué toohello carte réseau ou sous-réseau, aucune règle n’est affichées.
   > 
   > 
8. Cliquez sur les règles du groupe de sécurité réseau tooedit, *Subnet1-groupe de sécurité réseau* Bonjour **groupes de sécurité réseau associé** section.
   Cette opération ouvre hello **Subnet1-NSG** panneau. Vous pouvez modifier directement les règles hello en cliquant sur **les règles de sécurité de trafic entrant**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Après avoir supprimé hello *denyRDP* règle de trafic entrant Bonjour **Subnet1-groupe de sécurité réseau** et en ajoutant un *allowRDP* règle de liste de règles efficaces hello ressemble à hello illustration suivante :
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Vérifiez que le port TCP 3389 est ouvert en ouvrant un toohello de connexion RDP machine virtuelle ou en utilisant l’outil PsPing de hello. Vous pouvez en savoir plus sur PsPing par la lecture de hello [page de téléchargement PsPing](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Afficher les règles de sécurité effectives pour une interface réseau
Si le flux de trafic de votre machine virtuelle est affecté pour une carte réseau spécifique, vous pouvez afficher une liste complète des règles de hello efficaces pour hello carte réseau à partir du contexte d’interfaces hello réseau en effectuant hello comme suit :

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **davantage de services**, puis cliquez sur **interfaces réseau** dans la liste hello qui s’affiche.
3. Sélectionnez une interface réseau. Bonjour illustration suivante, une carte réseau nommée *NIC1 de VM1* est sélectionnée.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Notez que hello **étendue** a la valeur toohello interface de réseau sélectionnée. toolearn en savoir plus sur hello indiquées, des informations supplémentaires de lire l’étape 6 de hello **résoudre les groupes de sécurité réseau pour une machine virtuelle** section de cet article.
   
   > [!NOTE]
   > Si un groupe de sécurité réseau est supprimée d’une interface réseau, hello sous-réseau NSG est toujours en vigueur sur hello donné de carte réseau. Dans ce cas, la sortie de hello serait afficher uniquement les règles du sous-réseau de hello groupe de sécurité réseau. Les règles apparaissent uniquement si hello NIC est attaché tooa machine virtuelle.
   > 
   > 
4. Vous pouvez modifier directement les règles des groupes de sécurité réseau associés à une carte réseau et à un sous-réseau. toolearn, voir l’étape 8 de hello **afficher les règles de sécurité efficace pour une machine virtuelle** section de cet article.

## <a name="nsg"></a>Afficher les règles de sécurité effectives pour un groupe de sécurité réseau
Lorsque vous modifiez les règles du groupe de sécurité réseau, vous souhaiterez impact de hello tooreview de règles hello ajouté sur un ordinateur virtuel particulier. Vous pouvez afficher une liste complète des règles de sécurité efficace hello pour tous les hello des cartes réseau qui concerne un groupe de sécurité réseau donné, sans avoir de contexte tooswitch hello donné panneau du groupe de sécurité réseau. tootroubleshoot règles efficace au sein d’un groupe de sécurité réseau, hello complète comme suit :

1. Connexion toohello portail Azure à https://portal.azure.com.
2. Cliquez sur **davantage de services**, puis cliquez sur **groupes de sécurité réseau** dans la liste hello qui s’affiche.
3. Sélectionnez un groupe de sécurité réseau. Bonjour illustration suivante, un groupe de sécurité réseau nommé VM1-groupe de sécurité réseau a été sélectionné.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Notez hello les sections suivantes de l’image précédente de hello :
   
   * **Étendue :** définir toohello groupe de sécurité réseau sélectionnée.
   * **Machine virtuelle :** lorsqu’un groupe de sécurité réseau est appliquée tooa sous-réseau, tooall appliqué interfaces tooall attaché machines virtuelles connectés toohello sous-réseau. Cette liste affiche toutes les machines virtuelles auxquelles ce groupe de sécurité réseau s’applique. Vous pouvez sélectionner n’importe quel ordinateur virtuel à partir de la liste de hello.
     
     > [!NOTE]
     > Si un groupe de sécurité réseau est appliquée tooonly un sous-réseau vide, les machines virtuelles ne seront pas répertoriées. Si un groupe de sécurité réseau est appliquée tooa carte réseau qui n’est pas associé à une machine virtuelle, les cartes réseau est également pas répertorié. 
     > 
     > 
   * **Interface réseau** : une machine virtuelle peut avoir plusieurs interfaces réseau. Vous pouvez sélectionner une interface réseau attachée toohello sélectionné machine virtuelle.
   * **AssociatedNSGs :** à tout moment, une carte réseau peut avoir des tootwo groupes de sécurité réseau efficaces, une appliqué toohello NIC et hello toohello les autres sous-réseaux. Bien que l’étendue de hello est sélectionné comme nsg-VM1, si hello association a un groupe de sécurité réseau de sous-réseau efficace, sortie de hello affichera les deux groupes de sécurité réseau.
4. Vous pouvez modifier directement les règles des groupes de sécurité réseau associés à une carte réseau ou à un sous-réseau. toolearn, voir l’étape 8 de hello **afficher les règles de sécurité efficace pour une machine virtuelle** section de cet article.

toolearn en savoir plus sur hello indiquées, des informations supplémentaires de lire l’étape 6 de hello **afficher les règles de sécurité efficace pour une machine virtuelle** section de cet article.

> [!NOTE]
> Si un sous-réseau et les cartes réseau peuvent avoir qu’un seul groupe de sécurité réseau appliqué toothem, un groupe de sécurité réseau peut être associé toomultiple cartes réseau et plusieurs sous-réseaux.
> 
> 

## <a name="considerations"></a>Considérations
Tenez compte des points suivants lors de la résolution des problèmes de connectivité de hello :

* Règles du groupe de sécurité réseau par défaut bloque l’accès entrant à partir de hello internet et seulement ce réseau virtuel qui permet le trafic entrant. Les règles doivent être ajoutés explicitement tooallow accès entrant depuis Internet, en fonction des besoins.
* S’il n’y a aucune règle de sécurité groupe de sécurité réseau à l’origine de toofail de connectivité de réseau de l’ordinateur virtuel, problème de hello peut être due à :
  * Logiciel de pare-feu qui s’exécutent dans le système d’exploitation de la machine virtuelle hello
  * Itinéraires configurés pour des appliances virtuelles ou un trafic local. Le trafic Internet peut être redirigé tooon-site via le tunneling forcé. Une connexion RDP/SSH à partir de hello Internet tooyour machine virtuelle peut ne pas fonctionne avec ce paramètre, selon la façon dont le matériel de réseau local hello gère ce trafic. Hello de lecture [dépannage des itinéraires](virtual-network-routes-troubleshoot-powershell.md) article toolearn, comment les problèmes d’itinéraire toodiagnose qui peuvent être compromettent hello flux du trafic et se déconnecte de hello machine virtuelle. 
* Si vous avez homologuer les réseaux virtuels, par défaut, hello balise VIRTUAL_NETWORK développe automatiquement les préfixes tooinclude pour les réseaux virtuels de ressources. Vous pouvez afficher ces préfixes Bonjour **ExpandedAddressPrefix** répertorier, tootroubleshoot tout tooVNet connexes de problèmes d’homologation de connectivité. 
* Les règles de sécurité efficace sont affichent uniquement s’il existe qu'un groupe de sécurité réseau associé à la machine virtuelle hello NIC et ou un sous-réseau. 
* Si aucun groupes de sécurité réseau associés hello carte réseau ou sous-réseau et que vous avez une adresse IP publique affectée tooyour machine virtuelle, tous les ports seront ouverts pour un accès entrant et sortant. Si hello machine virtuelle a une adresse IP publique, appliquer des groupes de sécurité réseau toohello carte réseau ou sous-réseau est fortement recommandé.

