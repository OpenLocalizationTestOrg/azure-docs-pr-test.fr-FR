---
title: "aaaConfigure un port d’écoute externe pour les groupes de disponibilité AlwaysOn | Documents Microsoft"
description: "Parcours de ce didacticiel vous guide dans les étapes de création d’un toujours sur écouteur dans Azure qui est accessible en externe à l’aide de hello adresse IP virtuelle publique de hello service cloud associé."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Configurer un écouteur externe pour les groupes de disponibilité Always On dans Azure
> [!div class="op_single_selector"]
> * [Écouteur interne](../classic/ps-sql-int-listener.md)
> * [Écouteur externe](../classic/ps-sql-ext-listener.md)
> 
> 

Cette rubrique vous montre comment tooconfigure un écouteur pour un groupe de disponibilité AlwaysOn en externe accessible sur hello internet. Cela est possible en associant du service de cloud hello **publique IP virtuelle (VIP)** adresse qu’un écouteur hello.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Votre groupe de disponibilité peut contenir des réplicas locaux uniquement, Azure uniquement, ou locaux et Azure pour les configurations hybrides. Azure peuvent résider dans hello même région ou dans plusieurs régions à l’aide de plusieurs réseaux virtuels (réseaux virtuels). Hello étapes ci-dessous supposent que vous avez déjà [configuré un groupe de disponibilité](../classic/portal-sql-alwayson-availability-groups.md) mais n’avez pas configuré un port d’écoute.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Instructions et limitations pour les écouteurs externes
Notez hello suivant les instructions à propos de l’écouteur du groupe de disponibilité dans Azure hello lorsque vous déployez à l’aide de hello cloud service répertorié adresse :

* écouteur du groupe de disponibilité Hello est pris en charge sur Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2.
* application cliente de Hello doit résider sur un service cloud différent hello qui contient vos machines virtuelles du groupe de disponibilité. Service de cloud computing Azure ne gère pas les direct retour au serveur avec un client et serveur Bonjour même.
* Par défaut, les étapes de hello dans cet article montrent hello de toouse tooconfigure écouteur une adresse IP virtuelle (VIP) du service de cloud. Toutefois, il est possible de tooreserve et créer plusieurs adresses IP virtuelles pour votre service cloud. Cela vous permet de toouse les étapes de hello dans cette toocreate article plusieurs écouteurs sont chacune associées à une adresse IP virtuelle à l’autre. Pour plus d’informations sur comment toocreate plusieurs adresses IP virtuelles, consultez [plusieurs adresses IP virtuelles par le service cloud](../../../load-balancer/load-balancer-multivip.md).
* Si vous créez un écouteur pour un environnement hybride, réseau local de hello doit avoir toohello de connectivité Internet public dans Ajout toohello VPN de site à site avec hello réseau virtuel Azure. En cas de hello sous-réseau Azure, écouteur hello est accessible uniquement par les hello adresse IP publique du service de cloud respectif hello.
* Il n’est pas pris en charge toocreate un écouteur externe dans le même cloud service où vous avez également un écouteur interne à l’aide de hello hello équilibreur de charge interne (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Déterminer l’accessibilité hello d’écouteur de hello
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Cet article se concentre sur la création d’un écouteur qui utilise un **équilibrage de charge externe**. Si vous souhaitez un écouteur de réseau virtuel est tooyour privé, consultez version hello de cet article fournit les étapes pour configurer un [écouteur avec équilibrage de charge interne](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Créer des points de terminaison de machine virtuelle à charge équilibrée avec retour direct du serveur
L’équilibrage de charge externe utilise hello hello virtuel adresse IP virtuelle publique du service de cloud hello qui héberge vos machines virtuelles. Par conséquent, vous ne devez toocreate ou configurer équilibrage de charge hello dans ce cas.

Vous devez créer un point de terminaison avec équilibrage de charge pour chaque machine virtuelle qui héberge un réplica Azure. Si vous avez des réplicas dans plusieurs régions, chaque réplica hello pour cette région doit être dans le même service de cloud de hello même réseau virtuel. La création de réplicas de groupe de disponibilité couvrant plusieurs régions Azure nécessite de configurer plusieurs réseaux virtuels. Pour plus d’informations sur la configuration de la connectivité de réseau virtuel, consultez [tooVNet de configurer un réseau virtuel connectivité](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Bonjour portail Azure, accédez à tooeach machine virtuelle qui héberge un réplica et consulter les détails de hello.
2. Cliquez sur hello **points de terminaison** onglet pour chacune des machines virtuelles de hello.
3. Vérifiez que hello **nom** et **Port Public** du point de terminaison d’écouteur hello souhaité toouse n’est pas déjà en cours d’utilisation. Dans l’exemple hello ci-dessous, hello nom est « MyEndpoint » et le port hello est « 1433 ».
4. Sur votre ordinateur client local, téléchargez et installez [module PowerShell de la dernière hello](https://azure.microsoft.com/downloads/).
5. Lancez **Azure PowerShell**. Un nouveau PowerShell session est ouverte avec hello des modules d’administration Azure chargés.
6. Exécutez **Get-AzurePublishSettingsFile**. Cette applet de commande dirige toodownload de navigateur tooa un répertoire local de publier les paramètres fichiers tooa. Vous serez peut-être invité à entrer les informations d'identification de connexion de votre abonnement Azure.
7. Exécutez hello **Import-AzurePublishSettingsFile** commande avec le chemin d’accès de hello Hello publier le fichier de paramètres que vous avez téléchargé :
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Une fois que hello publier l’importation du fichier de paramètres, vous pouvez gérer votre abonnement Azure dans la session de PowerShell hello.
    
1. Copiez le script PowerShell de hello ci-dessous dans un éditeur de texte et définir toosuit des valeurs de variable hello votre environnement (valeurs par défaut ont été fournies pour certains paramètres). Notez que si votre groupe de disponibilité s’étend sur les régions Azure, vous devez exécuter les script hello qu’une seule fois dans chaque centre de données pour le service cloud hello et les nœuds qui résident dans ce centre de données.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Une fois que vous avez défini les variables hello, hello de copie créer un script à partir de l’éditeur de texte hello dans votre toorun de session Azure PowerShell. Si l’invite de commandes hello affiche toujours >>, tapez entrer à nouveau toomake vraiment hello script s’exécute.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Vérifiez que KB2854082 est installé le cas échéant
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Ouvrir les ports du pare-feu hello dans les nœuds de groupe de disponibilité
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Créer l’écouteur du groupe de disponibilité hello

Créez un écouteur du groupe de disponibilité hello en deux étapes. Tout d’abord, créer la ressource de cluster hello point de l’accès client et configurer les dépendances. Ensuite, configurez les ressources de cluster hello avec PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Créer le point d’accès client hello et configurer les dépendances de cluster de hello
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurer les ressources de cluster hello dans PowerShell
1. Pour l’équilibrage de charge externe, vous devez obtenir hello adresse IP virtuelle publique du service de cloud hello qui contient vos réplicas. Connectez-vous à hello le portail Azure. Accédez à service de cloud computing toohello qui contient votre machine virtuelle du groupe de disponibilité. Ouvrez hello **tableau de bord** vue.
2. Notez l’adresse hello affichée sous **adresse IP virtuelle publique (VIP)**. Si votre solution couvre des réseaux virtuels, répétez cette étape pour chaque service cloud contenant une machine virtuelle qui héberge un réplica.
3. Sur l’un des ordinateurs virtuels de hello, copiez hello script PowerShell ci-dessous dans un éditeur de texte et définir les variables de hello toohello les valeurs notées précédemment.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Une fois vous avez défini les variables hello, ouvrez une fenêtre Windows PowerShell avec élévation de privilèges, puis copiez le script de hello à partir de l’éditeur de texte hello et collez dans votre toorun de session Azure PowerShell. Si l’invite de commandes hello affiche toujours >>, tapez entrer à nouveau toomake vraiment hello script s’exécute.
5. Répétez cette procédure sur chaque machine virtuelle. Ce script configure la ressource d’adresse IP hello avec l’adresse IP de hello du service de cloud hello et définit d’autres paramètres comme port de la sonde hello. Lors de la ressource d’adresse IP de hello est mis en ligne, il peut ensuite répondre toohello sur le port de la sonde hello point de terminaison d’équilibrage de la charge hello créé précédemment dans ce didacticiel.

## <a name="bring-hello-listener-online"></a>Mettez écouteur hello en ligne
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Éléments de suivi
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Écouteur du groupe de disponibilité hello test (dans hello même réseau virtuel)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Écouteur du groupe de disponibilité test hello (sur hello internet)
Dans l’ordre tooaccess hello port d’écoute de réseau virtuel de hello externe, vous devez utiliser externe/public équilibrage (décrite dans cette rubrique) au lieu de l’équilibrage de charge interne, qui est uniquement accessible dans hello même réseau virtuel. Dans la chaîne de connexion hello, vous spécifiez nom du service cloud hello. Par exemple, si vous aviez un service cloud avec le nom de hello *mycloudservice*, instruction de sqlcmd hello serait comme suit :

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Contrairement aux hello précédent exemple, l’authentification SQL doit être utilisée, car l’appelant de hello ne peut pas utiliser l’authentification windows sur hello internet. Pour plus d’informations, voir [Always On Availability Group in Azure VM: Client Connectivity Scenarios](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)(Groupes de disponibilité Always On dans Azure VM : scénarios de connectivité client). Lorsque vous utilisez l’authentification SQL, vérifiez que vous créez hello même connexion sur les deux réplicas. Pour plus d’informations sur le dépannage des connexions avec les groupes de disponibilité, consultez [comment toomap connexions ou utilisez contenus SQL réplicas de tooother tooconnect utilisateur de base de données et mappez les bases de données tooavailability](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Si hello toujours sur les réplicas se trouvent dans des sous-réseaux différents, les clients doivent spécifier **MultisubnetFailover = True** dans la chaîne de connexion hello. Cela entraîne tooreplicas de tentatives de connexion parallèle dans des sous-réseaux différents hello. Notez que ce scénario inclut un déploiement de groupe de disponibilité Always On dans plusieurs régions.

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

