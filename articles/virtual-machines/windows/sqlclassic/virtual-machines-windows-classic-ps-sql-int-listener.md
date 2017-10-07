---
title: "aaaConfigure un écouteur d’équilibrage de charge interne pour les groupes de disponibilité Always On dans Azure | Documents Microsoft"
description: "Ce didacticiel utilise des ressources créées avec le modèle de déploiement classique hello et crée un écouteur de groupe de disponibilité Always On dans Azure qui utilise un équilibrage de charge interne."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Configurer un écouteur à équilibrage de charge interne pour des groupes de disponibilité Always On dans Azure
> [!div class="op_single_selector"]
> * [Écouteur interne](../classic/ps-sql-int-listener.md)
> * [Écouteur externe](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Vue d'ensemble

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article traite des utilisez hello hello classique de modèle de déploiement. Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.

tooconfigure un écouteur pour un groupe de disponibilité Always On dans le modèle de gestionnaire de ressources hello, consultez [configurer un équilibreur de charge pour un groupe de disponibilité Always On dans Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

Votre groupe de disponibilité peut contenir des réplicas locaux uniquement, Azure uniquement, ou locaux et Azure pour les configurations hybrides. Azure peuvent résider dans hello même région ou dans plusieurs régions qui utilisent plusieurs réseaux virtuels. Hello dans cet article supposent que vous avez déjà [configuré un groupe de disponibilité](../classic/portal-sql-alwayson-availability-groups.md) mais n’avez pas encore configuré un port d’écoute.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Instructions et limitations pour les écouteurs internes
Hello l’utilisation d’un équilibreur de charge interne (ILB) avec un écouteur de groupe de disponibilité dans Azure est toohello sujet suivant les instructions :

* écouteur du groupe de disponibilité Hello est pris en charge sur Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2.
* Qu’un seul écouteur interne est prise en charge pour chaque service cloud, car hello écouteur est configuré toohello équilibrage de charge interne, et qu’un seul équilibrage de charge pour chaque service cloud. Toutefois, il est possible de toocreate plusieurs écouteurs externes. Pour plus d’informations, voir [Configurer un écouteur externe pour les groupes de disponibilité Always On dans Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Déterminer l’accessibilité hello d’écouteur de hello
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Cet article se concentre sur la création d’un écouteur qui utilise un équilibreur de charge interne. Si vous avez besoin d’un écouteur public ou externe, consultez la version hello de cet article traite de la configuration d’un [port d’écoute externe](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Créer des points de terminaison de machine virtuelle à charge équilibrée avec retour direct du serveur
Vous créez tout d’abord un équilibrage de charge interne en exécutant le script de hello plus loin dans cette section.

Créez un point de terminaison avec équilibrage de charge pour chaque machine virtuelle qui héberge un réplica Azure. Si vous avez des réplicas dans plusieurs régions, chaque réplica pour cette région doit être dans le même service de cloud de hello hello même réseau virtuel Azure. La création de réplicas de groupe de disponibilité couvrant plusieurs régions Azure nécessite de configurer plusieurs réseaux virtuels. Pour plus d’informations sur la configuration de cross-connectivité de réseau virtuel, consultez [configurer la connectivité de réseau virtuel toovirtual réseau](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Bonjour portail Azure, accédez à tooeach machine virtuelle qui héberge un réplica tooview hello plus d’informations.

2. Cliquez sur hello **points de terminaison** onglet pour chaque machine virtuelle.

3. Vérifiez que hello **nom** et **Port Public** du point de terminaison d’écouteur hello que vous souhaitez toouse ne sont pas déjà en cours d’utilisation. Dans l’exemple hello dans cette section, nom de hello est *MyEndpoint*, et le port hello est *1433*.

4. Sur votre ordinateur client local, téléchargez et installez hello dernières [module PowerShell](https://azure.microsoft.com/downloads/).

5. Lancez Azure PowerShell.  
    Une nouvelle session PowerShell s’ouvre, avec hello Azure modules d’administration chargés.

6. Exécutez `Get-AzurePublishSettingsFile`. Cette applet de commande dirige toodownload de navigateur tooa un répertoire local de publier les paramètres fichiers tooa. Vous serez peut-être invité à entrer les informations d'identification de connexion de votre abonnement Azure.

7. Exécutez hello `Import-AzurePublishSettingsFile` commande avec le chemin d’accès de hello Hello publier le fichier de paramètres que vous avez téléchargé :

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Une fois que hello publié l’importation du fichier de paramètres, vous pouvez gérer votre abonnement Azure dans la session de PowerShell hello.

8. Affectez une adresse IP statique pour l’*équilibrage de charge interne*. Examiner la configuration du réseau virtuel en cours hello en exécutant hello de commande suivante :

        (Get-AzureVNetConfig).XMLConfiguration
9. Hello de note *sous-réseau* nom de sous-réseau hello qui contient des machines virtuelles hello qui hébergent les réplicas hello. Ce nom est utilisé dans le paramètre hello $SubnetName dans le script de hello.

10. Hello de note *VirtualNetworkSite* nommer et hello commençant *AddressPrefix* pour le sous-réseau hello qui contient des machines virtuelles hello qui hébergent les réplicas hello. Rechercher une adresse IP disponible en passant les deux valeurs toohello `Test-AzureStaticVNetIP` commande et en examinant hello *AvailableAddresses*. Par exemple, si hello réseau virtuel est nommé *MyVNet* et a une plage d’adresses de sous-réseau qui commence à *172.16.0.128*, suivants de hello commande répertorie les adresses disponibles :

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Sélectionnez une des adresses disponibles de hello et l’utiliser dans le paramètre hello $ILBStaticIP du script hello dans l’étape suivante de hello.

12. Copiez hello suivant l’éditeur de texte tooa script PowerShell et définissez toosuit des valeurs de variable hello votre environnement. Les valeurs par défaut ont été fournies pour certains paramètres.  

    Les déploiements existants qui utilisent des groupes d'affinités ne peuvent pas ajouter un équilibrage de charge interne. Pour plus d’informations sur les exigences liées à l’équilibreur de charge interne, consultez la rubrique [Présentation de l’équilibrage de charge interne](../../../load-balancer/load-balancer-internal-overview.md).

    En outre, si votre groupe de disponibilité s’étend sur les régions Azure, vous devez exécuter une fois hello script dans chaque centre de données pour le service cloud hello et les nœuds qui résident dans ce centre de données.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Après avoir défini les variables hello, hello de copie créer un script à partir de hello texte éditeur tooyour PowerShell session toorun. Si l’invite de commandes hello affiche toujours  **>>** , appuyez sur entrée à nouveau script de hello que toomake commence à s’exécuter.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Vérifiez que KB2854082 est installé le cas échéant
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Ouvrir les ports du pare-feu hello dans les nœuds de groupe de disponibilité
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Créer l’écouteur du groupe de disponibilité hello

Créez un écouteur du groupe de disponibilité hello en deux étapes. Tout d’abord, créer la ressource de cluster hello point de l’accès client et configurer les dépendances. Ensuite, configurez les ressources de cluster hello dans PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Créer le point d’accès client hello et configurer les dépendances de cluster de hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurer les ressources de cluster hello dans PowerShell
1. Pour l’équilibrage de charge interne, vous devez utiliser adresse IP hello hello équilibrage de charge interne qui a été créé précédemment. tooobtain cette adresse IP d’adresses dans PowerShell, hello utilisez script suivant :

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Sur l’un des ordinateurs virtuels de hello, copiez le script PowerShell de hello pour votre éditeur de texte tooa système d’exploitation, puis définir des variables de hello toohello les valeurs notées précédemment.

    Pour Windows Server 2012 ou version ultérieure, utilisez hello script suivant :

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Pour Windows Server 2008 R2, utilisez hello script suivant :

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Une fois que vous avez ensemble hello variables, ouvrez une fenêtre Windows PowerShell avec élévation de privilèges, coller hello créer un script à partir de l’éditeur de texte hello dans votre toorun de session PowerShell. Si l’invite de commandes hello affiche toujours  **>>** , appuyez sur entrée à nouveau les toomake assurer que le script de hello démarre en cours d’exécution.

4. Répétez les étapes précédentes pour chaque ordinateur virtuel de hello.  
    Ce script configure la ressource d’adresse IP hello avec l’adresse IP de hello du service de cloud hello et définit d’autres paramètres, tel que le port de sonde hello. Lors de la ressource d’adresse IP hello est mises en ligne, il peut répondre toohello sur le port de la sonde hello hello équilibrée point de terminaison que vous avez créé précédemment.

## <a name="bring-hello-listener-online"></a>Mettez écouteur hello en ligne
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Éléments de suivi
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Écouteur du groupe de disponibilité hello test (dans hello même réseau virtuel)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
