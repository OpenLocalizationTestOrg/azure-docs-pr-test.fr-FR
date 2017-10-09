---
title: "aaaAzure haute disponibilité de Machines virtuelles pour SAP NetWeaver | Documents Microsoft"
description: "Guide de haute disponibilité pour SAP NetWeaver sur machines virtuelles Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Haute disponibilité des machines virtuelles Azure pour SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Machines virtuelles Azure est la solution hello pour les organisations qui ont besoin de calcul, stockage et ressources réseau, dans le temps minimal et sans par de longs cycles. Vous pouvez utiliser les applications classiques de Machines virtuelles Azure toodeploy comme basés sur SAP NetWeaver ABAP, Java et une pile ABAP + Java. Élargissez la fiabilité et la disponibilité sans ressources locales supplémentaires. Comme le service Machines virtuelles Azure prend en charge la connectivité intersite, vous pouvez intégrer les machines virtuelles Azure dans les domaines locaux, les clouds privés et le paysage SAP de votre organisation.

Dans cet article, nous aborderons les étapes de hello que vous pouvez bénéficier toodeploy systèmes SAP à haute disponibilité dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello. Nous vous guidons à travers les tâches principales suivantes :

* Trouver des guides d’installation et les Notes SAP droite, répertoriés dans hello de hello [ressources] [ sap-ha-guide-2] section. Cet article complète la documentation d’installation SAP et les Notes SAP, qui sont des ressources principales hello qui peuvent vous aider à installer et déployer des logiciels SAP sur des plateformes spécifiques.
* Découvrez les différences de hello entre le modèle de déploiement du Gestionnaire de ressources Azure hello et le modèle de déploiement classique Azure hello.
* En savoir plus sur les modes de quorum le Clustering de basculement Windows Server, afin de pouvoir modèle hello qui convient à votre déploiement Azure.
* Découvrir le stockage partagé en cluster de basculement Windows Server dans les services Azure.
* Découvrez comment toohelp protègent les composants de l’unique point de défaillance comme Advanced Business Application Programming (ABAP) SAP Central Services (ASC) / SAP Central Services (SCS) et les systèmes de gestion de base de données (SGBD) et des composants redondants, tels que SAP Serveur d’applications dans Azure.
* Suivre un exemple pas à pas d’installation et de configuration d’un système SAP à haute disponibilité dans un cluster de clustering de basculement Windows Server dans Azure en utilisant Azure Resource Manager.
* Obtenir des informations sur les étapes supplémentaires requises toouse est Clustering de basculement Windows Server dans Azure, mais qui ne sont pas nécessaires dans un déploiement sur site.

déploiement de toosimplify et de configuration, dans cet article, nous utilisons hello des modèles de gestionnaire de ressources haute disponibilité SAP à trois niveaux. modèles de Hello automatisent le déploiement de hello toute infrastructure dont vous avez besoin pour un système SAP à haute disponibilité. infrastructure de Hello prend également en charge le dimensionnement de SAP Application performances Standard (SAP) de votre système SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Conditions préalables
Avant de commencer, assurez-vous que conditions préalables hello qui sont décrites dans les sections suivantes de hello. En outre, être toocheck que toutes les ressources répertoriées dans hello [ressources] [ sap-ha-guide-2] section.

Dans cet article, nous utilisons des modèles Azure Resource Manager pour [SAP NetWeaver à trois niveaux à l’aide des disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Pour une vue d’ensemble utile des modèles Azure Resource Manager SAP, consultez [cet article](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Ressources
Ces articles couvrent les déploiements SAP dans Azure :

* [Planification et implémentation de machines virtuelles Azure pour SAP NetWeaver][planning-guide]
* [Déploiement de machines virtuelles Azure pour SAP NetWeaver][deployment-guide]
* [Déploiement SGBD de machines virtuelles Azure pour SAP NetWeaver][dbms-guide]
* [Haute disponibilité des machines virtuelles Azure pour SAP NetWeaver (ce guide)][sap-ha-guide]

> [!NOTE]
> Chaque fois que possible, nous vous offrons une toohello lien référence guide d’installation SAP (voir hello [guides d’installation SAP][sap-installation-guides]). Pour les conditions préalables et les informations sur les processus d’installation de hello, elle une installation de SAP NetWeaver conseillé tooread hello Guide avec soin. Cet article traite uniquement des tâches spécifiques pour les systèmes basés sur SAP NetWeaver que vous pouvez utiliser avec le service Machines virtuelles Azure.
>
>

Ces Notes SAP sont rubrique toohello connexes de SAP dans Azure :

| Numéro de la note | Intitulé |
| --- | --- |
| [1928533] |Applications SAP sur Azure : dimensionnement et produits pris en charge |
| [2015553] |SAP sur Microsoft Azure : configuration requise |
| [1999351] |Surveillance Azure améliorée pour SAP |
| [2178632] |Métriques de surveillance clés pour SAP sur Microsoft Azure |
| [1999351] |Virtualisation sur Windows : surveillance améliorée |
| [2243692] |Utilisation du stockage SSD Azure Premium pour l’instance de SGBD SAP |

En savoir plus sur hello [limitations des abonnements Azure][azure-subscription-service-limits-subscription], y compris les limitations générales par défaut et limitations maximales.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Haute disponibilité SAP avec Azure Resource Manager et le modèle de déploiement classique Azure hello
Hello Azure Resource Manager et les modèles de déploiement classique Azure sont différentes dans hello suivant de zones :

- Groupes de ressources
- Azure interne charger la dépendance d’équilibrage sur le groupe de ressources Azure hello
- Prise en charge des scénarios SAP multi-SID

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Groupes de ressources
Dans le Gestionnaire de ressources Azure, vous pouvez utiliser toomanage de groupes de ressources toutes les ressources de l’application hello dans votre abonnement Azure. Une approche intégrée, dans un groupe de ressources, toutes les ressources ont hello même cycle de vie. Par exemple, toutes les ressources sont créées à hello même temps et ils sont supprimés à hello même temps. En savoir plus sur les [groupes de ressources](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interne charger la dépendance d’équilibrage sur le groupe de ressources Azure hello

Dans le modèle de déploiement classique Azure hello, il existe une dépendance entre l’équilibreur de charge interne Azure hello (service d’équilibrage de charge Azure) et le service de cloud computing hello. Chaque équilibreur de charge interne a besoin d’un service cloud.

Dans le Gestionnaire de ressources Azure, toutes les ressources Azure doit toobe placé dans un groupe de ressources Azure, et il est également valide pour l’équilibrage de charge Azure. Toutefois, aucun groupe d’une ressource Azure toohave nécessaire par l’équilibrage de charge Azure, par exemple, un groupe de ressources Azure peut contenir plusieurs équilibrages de charge Azure. environnement de Hello est plus simple et flexible. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Prise en charge des scénarios SAP multi-SID

Dans Azure Resource Manager, vous pouvez installer plusieurs instances d’identificateur système SAP (SID) ASCS/SCS dans un cluster. Il est possible d’utiliser des instances multi-SID en raison de la prise en charge de plusieurs adresses IP pour chaque équilibreur de charge interne Azure.

toouse hello du modèle de déploiement classique Azure, suivez les procédures hello décrites dans [SAP NetWeaver dans Azure : les instances de Clustering ASCS/SCS SAP à l’aide de Clustering de basculement Windows Server dans Azure avec SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Nous vous recommandons fortement d’utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello pour les installations SAP. Il offre de nombreux avantages qui ne sont pas disponibles dans le modèle de déploiement classique hello. En savoir plus sur les [modèles de déploiement][virtual-machines-azure-resource-manager-architecture-benefits-arm] Azure.   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Clustering de basculement Windows Server
Le Clustering de basculement Windows Server est foundation hello d’une installation SAP ASCS/SCS de haute disponibilité et un SGBD dans Windows.

Un cluster de basculement est un groupe de 1 + n serveurs indépendants (nœuds) qui fonctionnent ensemble de disponibilité de hello tooincrease des applications et services. En cas de défaillance d’un nœud, le Clustering de basculement Windows Server calcule nombre hello d’échecs qui peuvent se produire lors de la gestion d’état de fonctionnement normal de cluster tooprovide applications et services. Vous pouvez choisir de quorum différents modes tooachieve le clustering de basculement.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modes de quorum
Lorsque vous utilisez le clustering de basculement Windows Server, vous pouvez choisir parmi quatre modes de quorum :

* **Nœud majoritaire** : Chaque nœud du cluster de hello peut voter. Bonjour cluster ne fonctionne uniquement avec la majorité des votes, autrement dit, avec plus de la moitié des votes de hello. Nous recommandons cette option pour les clusters qui présentent un nombre impair de nœuds. Par exemple, trois nœuds dans un cluster à sept nœuds peuvent échouer et images fixes de cluster hello atteigne une majorité et continue toorun.  
* **Nœud et disque majoritaires** : Chaque nœud et un disque désigné (un témoin de disque) dans le stockage de cluster hello peuvent voter lorsqu’ils sont disponibles et en communication. Hello cluster ne fonctionne seulement avec une majorité de hello de votes, autrement dit, avec plus de la moitié des votes de hello. Ce mode est pertinent dans un environnement de cluster comprenant un nombre pair de nœuds. Si les nœuds de moitié hello et de disque de hello sont en ligne, le cluster de hello reste dans un état sain.
* **Nœud et partage de fichiers majoritaires** : Chaque nœud et partage de fichiers désigné (un témoin de partage de fichiers) qui hello administrateur crée peut voter, que les nœuds hello et partage de fichiers soient disponibles et en communication. Hello cluster ne fonctionne seulement avec une majorité de hello de votes, autrement dit, avec plus de la moitié des votes de hello. Ce mode est pertinent dans un environnement de cluster comprenant un nombre pair de nœuds. Il est similaire toohello nœud et le mode disque majoritaires, mais il utilise un partage de fichiers témoin au lieu d’un disque témoin. Ce mode est tooimplement facile, mais si un partage de fichiers de hello lui-même n’est pas hautement disponible, il peut devenir un point de défaillance unique.
* **Pas de majorité : disque uniquement** : cluster de Hello possède un quorum si un nœud est disponible et en communication avec un disque spécifique du stockage de cluster hello. Seuls les nœuds hello qui se trouvent également dans la communication avec ce disque peuvent être ajouté hello cluster. Nous vous déconseillons d’utiliser ce mode.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Clustering de basculement Windows Server local
La figure 1 illustre un cluster de deux nœuds. Si hello Échec de la connexion réseau entre les nœuds de hello et les deux nœuds restent des et en cours d’exécution, un quorum disque ou partage de fichiers détermine quel nœud continuera de cluster tooprovide hello applications et services. nœud Hello qui possède le disque quorum accès toohello ou partager des fichiers est le nœud hello qui permet aux services de continuer.

Étant donné que cet exemple utilise un cluster à deux nœuds, nous utilisons hello nœud et le mode de quorum de partage de fichiers majoritaires. Hello nœud et disque majoritaires également est une option valide. Dans un environnement de production, nous vous recommandons d’utiliser un disque quorum. Vous pouvez utiliser le réseau et stockage toomake de technologie système hautement disponibles.

![Figure 1 : Exemple de configuration de clustering de basculement Windows Server pour SAP ASCS/SCS dans Azure][sap-ha-guide-figure-1000]

_**Figure 1 :** Exemple de configuration de clustering de basculement Windows Server pour SAP ASCS/SCS dans Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Stockage partagé
La figure 1 illustre également un cluster de stockage partagé à deux nœuds. Dans un cluster de stockage partagé local, tous les nœuds de cluster de hello détectent le stockage partagé. Un mécanisme de verrouillage protège les données de hello contre d’éventuels dommages. Tous les nœuds peuvent détecter si un autre nœud échoue. Si un nœud échoue, nœud restant de hello prend possession des ressources de stockage hello et garantit la disponibilité de hello des services.

> [!NOTE]
> Avec certaines applications de SGBD, telles que SQL Server, vous n’avez pas besoin de disques partagés pour atteindre une haute disponibilité. SQL Server Always On réplique les fichiers de données et les journaux du SGBD à partir du disque local de hello de disque local de la toohello de nœud d’un cluster d’un autre nœud de cluster. Dans ce cas, configuration du cluster Windows hello n’a pas besoin d’un disque partagé.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Mise en réseau et résolution de noms
Les ordinateurs clients d’accéder cluster de hello sur une adresse IP virtuelle et un nom d’hôte virtuel que hello fournit du serveur DNS. Hello nœuds sur site et le serveur DNS de hello peut gérer plusieurs adresses IP.

Dans une installation type, vous utilisez deux ou plusieurs connexions réseau :

* Un stockage de toohello connexion dédiée
* Une connexion de réseau interne de cluster pour la vérification des pulsations hello
* Un réseau public que les clients utilisent tooconnect toohello cluster

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Clustering de basculement Windows Server dans Azure
Comparé les déploiements de cloud privé ou complète toobare, les Machines virtuelles Azure nécessite tooconfigure des étapes supplémentaires Clustering de basculement Windows Server. Lorsque vous créez un disque de cluster partagé, vous devez tooset plusieurs adresses IP et l’hôte virtuel des noms d’instance de SAP ASCS/SCS hello.

Dans cet article, nous présentent les concepts clés et hello toobuild requis d’étapes supplémentaires un cluster de haute disponibilité des services centrale SAP dans Azure. Nous vous indiquons comment tooset des hello un outil tiers SIOS DataKeeper, et comment tooconfigure hello Azure interne l’équilibrage de charge. Vous pouvez utiliser ces outils de toocreate un cluster de basculement Windows avec un témoin de partage de fichiers dans Azure.

![Figure 2 : Configuration du clustering de basculement Windows Server dans Azure sans disque partagé][sap-ha-guide-figure-1001]

_**Figure 2 :** Configuration du clustering de basculement Windows Server dans Azure sans disque partagé_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disque partagé dans Azure avec SIOS DataKeeper
Vous avez besoin d’un stockage partagé en cluster pour bénéficier d’une instance SAP ASCS/SCS à haute disponibilité. Comme de septembre 2016, Azure n’offre pas un stockage partagé que vous pouvez utiliser toocreate un cluster de stockage partagé. Vous pouvez utiliser un logiciel tiers SIOS DataKeeper Cluster Edition toocreate un stockage en miroir qui simule le stockage partagé de cluster. Hello solution SIOS assure une réplication synchrone des données en temps réel. Voici comment créer une ressource de disque partagé pour un cluster :

1. Attacher un tooeach disque supplémentaire de hello machines () dans une configuration de cluster Windows.
2. Exécutez SIOS DataKeeper Cluster Edition sur les deux nœuds de machine virtuelle.
3. Configurer le Cluster SIOS DataKeeper Edition afin qu’elle reflète le contenu du volume de disque supplémentaires attaché hello hello source machine virtuelle toohello supplémentaires disque attaché volume sur la machine virtuelle cible hello hello. SIOS DataKeeper résume les volumes locaux hello source et cible et les présente ensuite tooWindows Clustering de basculement de serveur en tant qu’un disque partagé.

Vous trouverez plus d’informations sur SIOS DataKeeper [ici](http://us.sios.com/products/datakeeper-cluster/).

![Figure 3 : Configuration du clustering de basculement Windows Server dans Azure à l’aide de SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figure 3 :** Configuration du clustering de basculement Windows Server dans Azure à l’aide de SIOS DataKeeper_

> [!NOTE]
> Avec certains SGBD, tels que SQL Server, vous n’avez pas besoin de disques partagés pour atteindre une haute disponibilité. SQL Server Always On réplique les fichiers de données et les journaux du SGBD à partir du disque local de hello de disque local de la toohello de nœud d’un cluster d’un autre nœud de cluster. Dans ce cas, configuration du cluster Windows hello n’a pas besoin d’un disque partagé.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Résolution de noms dans Azure
plateforme de cloud computing Azure Hello n’offre pas hello option tooconfigure adresses IP virtuelles, telles que les adresses IP flottantes. Vous avez besoin d’un tooset autre solution d’une virtuel tooreach hello cluster ressource d’adresse IP dans le cloud de hello.
Azure a un équilibreur de charge interne Bonjour service d’équilibrage de charge Azure. Avec équilibrage de charge interne hello, les clients atteindre cluster de hello sur l’adresse IP virtuelle du cluster hello.
Vous avez besoin d’équilibreur de charge interne toodeploy hello dans le groupe de ressources hello qui contient les nœuds de cluster hello. Ensuite, configurez tous les ports nécessaires, règles de transfert avec une sonde hello ports d’équilibrage de charge interne hello.
les clients de Hello peuvent se connecter via un nom d’hôte virtuel hello. serveur DNS de Hello résout l’adresse IP du cluster hello et port d’handles équilibrage de charge interne hello toohello le nœud actif du cluster de hello de transfert.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Haute disponibilité pour SAP NetWeaver dans Azure IaaS (Infrastructure as a Service)
tooachieve SAP haute disponibilité des applications, par exemple pour les composants logiciels SAP, vous devez hello tooprotect suivant des composants :

* Instance de serveur d’applications SAP
* Instance SAP ASCS/SCS
* Serveur SGBD

Pour plus d’informations sur la protection des composants SAP dans des scénarios de haute disponibilité, consultez [Planification et implémentation de machines virtuelles Azure pour SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Serveur d’applications SAP à haute disponibilité
Vous ne devez généralement une solution de haute disponibilité spécifique pour les instances de serveur d’applications SAP et de la boîte de dialogue hello. La haute disponibilité s’obtient par redondance, et vous configurez plusieurs instances de dialogue sur différentes instances de machines virtuelles Azure. Vous devez avoir au moins deux instances d’applications SAP installées dans deux instances de machines virtuelles Azure.

![Figure 4 : Serveur d’applications SAP à haute disponibilité][sap-ha-guide-figure-2000]

_**Figure 4 :** Serveur d’applications SAP à haute disponibilité_

Vous devez placer tous les ordinateurs virtuels que les instances de serveur d’applications SAP d’hôte hello même groupe à haute disponibilité Azure. Un groupe à haute disponibilité Azure garantit que :

* Tous les ordinateurs virtuels font partie de hello même domaine de mise à niveau. Un domaine de mise à niveau, par exemple, permet de s’assurer que les ordinateurs virtuels de hello ne sont pas mis à jour à hello même temps pendant le temps mort de maintenance planifiée.
* Tous les ordinateurs virtuels font partie de hello même domaine par défaut. Un domaine d’erreur, par exemple, permet de s’assurer que les ordinateurs virtuels sont déployés afin qu’aucun point de défaillance unique n’affecte la disponibilité de hello de tous les ordinateurs virtuels.

En savoir plus sur la façon trop[gérer la disponibilité hello des machines virtuelles][virtual-machines-manage-availability].

Disque non managée uniquement : hello compte de stockage Azure est un point de défaillance unique potentiel, il est important toohave au moins deux comptes de stockage Azure, dans laquelle au moins deux ordinateurs virtuels sont distribuées. Dans une configuration idéale, disques hello de chaque ordinateur virtuel qui exécute une instance de la boîte de dialogue SAP sont déployées dans un autre compte de stockage.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instance SAP ASCS/SCS à haute disponibilité
La figure 5 est un exemple d’instance SAP ASCS/SCS à haute disponibilité.

![Figure 5 : Instance SAP ASCS/SCS à haute disponibilité][sap-ha-guide-figure-2001]

_**Figure 5 :** Instance SAP ASCS/SCS à haute disponibilité_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Haute disponibilité de l’instance SAP ASCS/SCS avec le clustering de basculement Windows Server dans Azure
Comparé les déploiements de cloud privé ou complète toobare, les Machines virtuelles Azure nécessite tooconfigure des étapes supplémentaires Clustering de basculement Windows Server. toobuild un cluster de basculement Windows, vous devez un disque de cluster partagé, plusieurs adresses IP, plusieurs noms d’hôte virtuel et un équilibrage de charge interne Azure pour le clustering d’une instance SAP ASCS/SCS. Nous aborderons cela plus en détail plus loin dans l’article de hello.

![Figure 6 : Configuration du clustering de basculement Windows Server pour une instance SAP ASCS/SCS dans Azure à l’aide de SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figure 6 :** Configuration du clustering de basculement Windows Server pour une instance SAP ASCS/SCS dans Azure à l’aide de SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Instance SGBD à haute disponibilité
Hello SGBD est également un point de contact unique dans un système SAP. Vous devez tooprotect à l’aide d’une solution de haute disponibilité. La figure 7 illustre une solution de haute disponibilité SQL Server Always On dans Azure, avec le Clustering de basculement Windows Server et hello Azure interne l’équilibrage de charge. SQL Server Always On réplique les fichiers journaux et les données du SGBD à l’aide de sa propre réplication de SGBD. Dans ce cas, vous ne devez disques de cluster partagés, qui simplifie la configuration entière de hello.

![Figure 7 : Exemple de SGBD SAP à haute disponibilité avec SQL Server Always On][sap-ha-guide-figure-2003]

_**Figure 7 :** Exemple de SGBD SAP à haute disponibilité avec SQL Server Always On_

Pour plus d’informations sur les clusters SQL Server dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello, voir les articles suivants :

* [Configuration manuelle d’un groupe de disponibilité Always On dans une machine virtuelle Azure à l’aide de Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Configurer un équilibrage de charge interne Azure pour un groupe de disponibilité Always On dans Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Scénarios de déploiement à haute disponibilité de bout en bout

### <a name="deployment-scenario-using-architectural-template-1"></a>Scénario de déploiement à l’aide du modèle architectural n°1

La figure 8 illustre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **un** système SAP. Ce scénario est défini comme suit :

- Un cluster dédié est utilisé pour l’instance de SAP ASCS/SCS hello.
- Un cluster dédié est utilisé pour l’instance de SGBD hello.
- Des instances de serveurs d’applications SAP sont déployées dans des machines virtuelles dédiées.

![Figure 8 : Modèle d’architecture SAP à haute disponibilité n°1, avec un cluster dédié à ASCS/SCS et SGBD][sap-ha-guide-figure-2004]

_**Figure 8 :** Modèle d’architecture SAP à haute disponibilité n°1, avec des clusters dédiés à ASCS/SCS et SGBD_

### <a name="deployment-scenario-using-architectural-template-2"></a>Scénario de déploiement à l’aide du modèle architectural n°2

La figure 9 illustre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **un** système SAP. Ce scénario est défini comme suit :

- Un cluster dédié est utilisé pour **les deux** hello SAP ASCS/SCS d’instance et hello SGBD.
- Des instances de serveurs d’applications SAP sont déployées dans leurs propres machines virtuelles dédiées.

![Figure 9 : Modèle d’architecture SAP à haute disponibilité n°2, avec un cluster dédié à l’instance ASCS/SCS et un cluster dédié à SGBD][sap-ha-guide-figure-2005]

_**Figure 9 :** Modèle d’architecture SAP à haute disponibilité n°2, avec un cluster dédié à l’instance ASCS/SCS et un cluster dédié à SGBD_

### <a name="deployment-scenario-using-architectural-template-3"></a>Scénario de déploiement à l’aide du modèle architectural n°3

La figure 10 montre une architecture SAP NetWeaver à haute disponibilité dans Azure pour **deux** systèmes SAP, avec &lt;SID1&gt; et &lt;SID2&gt;. Ce scénario est défini comme suit :

- Un cluster dédié est utilisé pour **les deux** instance de hello SAP ASCS/SCS SID1 *et* l’instance hello SAP ASCS/SCS SID2 (un cluster).
- Un cluster dédié est utilisé pour SGBD SID1, et un autre cluster dédié est utilisé pour SGBD SID2 (deux clusters).
- Instances de serveur d’applications SAP pourquoi le système SAP SID1 ont leurs propres ordinateurs virtuels dédiés.
- Instances de serveur d’applications SAP pourquoi le système SAP SID2 ont leurs propres ordinateurs virtuels dédiés.

![Figure 10 : Modèle d’architecture SAP à haute disponibilité n°3, avec un cluster dédié aux différentes instances ASCS/SCS][sap-ha-guide-figure-6003]

_**Figure 10 :** Modèle d’architecture SAP à haute disponibilité n°3, avec un cluster dédié aux différentes instances ASCS/SCS_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Préparer l’infrastructure de hello

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Préparer l’infrastructure de hello pour architecture modèle 1
Les modèles Azure Resource Manager pour SAP simplifient le déploiement des ressources requises.

modèles à trois niveaux de Hello dans Azure Resource Manager prennent également en charge des scénarios de haute disponibilité, comme dans l’architecture 1 de modèle, qui a deux clusters. Chaque cluster constitue un point de défaillance pour l’instance SAP ASCS/SCS et l’instance SGBD.

Voici où obtenir des modèles Azure Resource Manager pour le scénario d’exemple hello que nous décrivons dans cet article :

* [Image Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Image de Place de marché Azure au moyen de disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Image personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Image personnalisée à l’aide de disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

infrastructure de hello tooprepare pour architecture modèle 1 :

- Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **SYSTEMAVAILABILITY** boîte, sélectionnez **HA**.

  ![Figure 11 : Définir les paramètres Azure Resource Manager de haute disponibilité SAP][sap-ha-guide-figure-3000]

_**Figure 11 :** Définir les paramètres Azure Resource Manager de haute disponibilité SAP_


  créent des modèles de Hello :

  * **Des machines virtuelles** :
    * Des machines virtuelles de serveur d’applications SAP : <*SIDSystèmeSAP*>-di-<*Numéro*>
    * Des machines virtuelles de cluster ASCS/SCS : <*SIDSystèmeSAP*>-ascs-<*Numéro*>
    * Cluster SGBD : <*SIDSystèmeSAP*>-db-<*Numéro*>

  * **Des cartes réseau pour toutes les machines virtuelles, avec une adresse IP associée** :
    * <*SIDSystèmeSAP*&gt;-nic-di-&lt;*Numéro*>
    * <*SIDSystèmeSAP*&gt;-nic-ascs-&lt;*Numéro*>
    * <*SIDSystèmeSAP*&gt;-nic-db-&lt;*Numéro*>

  * **Comptes de stockage Azure (disques non gérés uniquement)**

  * **Des groupes de disponibilité** pour :
    * Les machines virtuelles de serveur d’applications SAP : <*SIDSystèmeSAP*>-avset-di
    * Les machines virtuelles de cluster SAP ASCS/SCS : <*SIDSystèmeSAP*>-avset-ascs
    * Les machines virtuelles de cluster SGBD : <*SIDSystèmeSAP*>-avset-db

  * **Un équilibrage de charge interne Azure** :
    * Avec tous les ports pour l’instance ASCS/SCS hello et l’adresse IP <*SAPSystemSID*> - lb - ASC
    * Avec tous les ports pour hello système SGBD de SQL Server et l’adresse IP <*SAPSystemSID*> - lb - db

  * **Un groupe de sécurité réseau** : &lt;*SIDSystèmeSAP*&gt;-nsg-ascs-0  
    * Avec un toohello de port de protocole RDP (Remote Desktop) externe ouvrir <*SAPSystemSID*> - ASC - 0 virtual machine

> [!NOTE]
> Toutes les adresses IP des cartes réseau de hello et équilibreurs de charge interne Azure sont **dynamique** par défaut. Modifiez-les trop**statique** des adresses IP. Nous allons décrire comment toodo cela plus loin dans l’article de hello.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Déployer des ordinateurs virtuels avec toouse (entre sites) de connectivité de réseau d’entreprise en production
Pour les systèmes SAP de production, déployez les machines virtuelles Azure avec une [connectivité de réseau d’entreprise (intersite)][planning-guide-2.2] à l’aide d’un VPN de site à site Azure ou d’Azure ExpressRoute.

> [!NOTE]
> Vous pouvez utiliser votre instance de réseau virtuel Azure. sous-réseau et réseau virtuel de hello ont déjà été créés et préparés.
>
>

1.  Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **NEWOREXISTINGSUBNET** boîte, sélectionnez **existant**.
2.  Bonjour **IDSOUSRÉSEAU** zone, ajouter hello de chaîne complet de votre réseau Azure préparée IDSousRéseau où vous prévoyez toodeploy vos machines virtuelles Azure.
3.  tooget une liste de tous les sous-réseaux du réseau Azure, exécutez la commande PowerShell :

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Hello **ID** champ affiche hello **IDSOUSRÉSEAU**.
4. tooget une liste de tous les **IDSOUSRÉSEAU** valeurs, exécutez la commande PowerShell :

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Hello **IDSOUSRÉSEAU** ressemble à ceci :

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Déployer des instances SAP dans le cloud uniquement à des fins de test et de démonstration
Vous pouvez déployer votre système SAP à haute disponibilité dans un modèle de déploiement cloud uniquement. Ce type de déploiement est surtout utile pour les démonstrations et les tests. Il ne convient pas à une utilisation en production.

- Bonjour portail Azure, sur hello **paramètres** panneau, Bonjour **NEWOREXISTINGSUBNET** boîte, sélectionnez **nouveau**. Laissez hello **IDSOUSRÉSEAU** champ vide.

  Hello crée automatiquement le Gestionnaire des ressources SAP Azure hello sous-réseau et réseau virtuel Azure.

> [!NOTE]
> Vous devez également toodeploy au moins l’un dédié machine virtuelle pour Active Directory et DNS dans hello la même instance de réseau virtuel Azure. modèle de Hello ne crée pas ces ordinateurs virtuels.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Préparer infrastructure de hello pour architecture modèle 2

Vous pouvez utiliser ce modèle de gestionnaire de ressources Azure pour SAP toohelp simplifier le déploiement des ressources de l’infrastructure requise pour 2 modèle Architectural de SAP.

Voici où vous pouvez obtenir des modèles Azure Resource Manager pour ce scénario de déploiement :

* [Image Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Image de Place de marché Azure au moyen de disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Image personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Image personnalisée à l’aide de disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Préparer infrastructure de hello pour les modèles architecturaux de 3

Vous pouvez préparer l’infrastructure de hello et configurer SAP pour **multi-SID**. Par exemple, vous pouvez ajouter une instance SAP ASCS/SCS supplémentaire à une configuration de cluster *existante*. Pour plus d’informations, consultez [configurer une instance SAP ASCS/SCS supplémentaire dans un toocreate de configuration de cluster existant une configuration de multi-SID SAP dans Azure Resource Manager][sap-ha-multi-sid-guide].

Si vous voulez toocreate un nouveau cluster multi-SID, vous pouvez utiliser hello multi-SID [modèles de démarrage rapide sur GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate un nouveau cluster multi-SID, vous devez hello toodeploy suivant trois modèles :

* [Modèle ASCS/SCS](#ASCS-SCS-template)
* [Modèle de base de données](#database-template)
* [Modèle de serveurs d’applications](#application-servers-template)

Hello sections suivantes incluent des informations supplémentaires sur les modèles hello et paramètres hello tooprovide dans les modèles de hello.

#### <a name="ASCS-SCS-template"></a> Modèle ASCS/SCS

modèle ASCS/SCS Hello déploie les deux ordinateurs virtuels que vous pouvez utiliser toocreate un cluster de basculement Windows Server qui héberge plusieurs instances ASCS/SCS.

tooset modèle hello ASCS/SCS multi-SID, Bonjour [modèle de multi-SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] ou [modèle de multi-SID ASCS/SCS à l’aide de disques gérés] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], entrez des valeurs pour hello paramètres suivants :

  - **Préfixe de ressource**.  Définir le préfixe de ressource hello, qui est utilisé tooprefix toutes les ressources qui sont créés au cours du déploiement de hello. Étant donné que les ressources hello ne font pas partie d’un même système SAP tooonly, préfixe hello de ressource de hello n’est pas hello SID d’un système SAP.  préfixe de Hello doit être comprise entre **trois à six caractères**.
  - **Type de pile**. Sélectionnez le type de pile hello Hello système SAP. Selon le type de pile hello, équilibrage de charge Azure a un (ABAP ou Java uniquement) ou deux (ABAP + Java) des adresses IP privées par le système SAP.
  -  **Type de système d’exploitation**. Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.
  -  **Nombre de systèmes SAP**. Sélectionnez le nombre de hello de systèmes SAP, vous souhaitez tooinstall dans ce cluster.
  -  **Disponibilité du système**. Sélectionnez la haute disponibilité **(HA)**.
  -  **Nom d’utilisateur et mot de passe d’administrateur**. Créer un utilisateur qui peut être utilisé toosign dans toohello machine.
  -  **Sous-réseau nouveau ou existant**. Déterminez s’il faut créer un réseau virtuel et un sous-réseau, ou utiliser un sous-réseau existant. Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez **existant**.
  -  **ID du sous-réseau**. ID de hello l’ensemble d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté. Sélectionnez sous-réseau hello de votre réseau privé virtuel (VPN) ou de réseau local de tooyour ExpressRoute réseau virtuel tooconnect hello de machines virtuelles. ID de Hello ressemble généralement à ceci :

   /subscriptions/<*subscription id*>/resourceGroups/<*resource group name*>/providers/Microsoft.Network/virtualNetworks/<*virtual network name*>/subnets/<*subnet name*>

modèle de Hello déploie une seule instance d’équilibrage de charge Azure, qui prend en charge plusieurs systèmes SAP.

- Hello ASC sont configurées pour le numéro d’instance de 00, 10, 20...
- Hello SCS sont configurées pour le numéro d’instance 01, 11, 21...
- Hello ASC Enqueue réplication serveur ERS (Linux uniquement) sont configurées pour le numéro d’instance 02, 12, 22...
- Hello SCS ERS (Linux uniquement) sont configurées pour le numéro d’instance 03, 13, 23...

équilibrage de charge Hello contient 1 (2 pour Linux) VIP(s), 1 VIP x ASCS/SCS et adresse IP virtuelle de 1 x pour ERS (Linux uniquement).

Hello liste suivante contient des règles (où x est le nombre de hello de hello système SAP, par exemple, 1, 2, 3, etc.) d’équilibrage de charge de toutes les :
- Ports spécifiques de Windows pour chaque système SAP 445, 5985
- Ports ASCS (numéro d’instance x0) : 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016
- Ports SCS (numéro d’instance x1) : 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116
- Ports ASCS ERS sous Linux (numéro d’instance x2) : 33x2, 5x213, 5x214, 5x216
- Ports SCS ERS sous Linux (numéro d’instance x3) : 33x3, 5x313, 5x314, 5x316

équilibrage de charge Hello est hello toouse configuré suivant des ports de sonde (où x est le nombre de hello de hello système SAP, par exemple, 1, 2, 3...) :
- Port de sondage d’équilibrage de charge interne ASCS/SCS : 620x0
- Port de sondage d’équilibrage de charge interne ERS (Linux uniquement) : 621x2

#### <a name="database-template"></a> Modèle de base de données

modèle de base de données Hello déploie une ou deux machines virtuelles que vous pouvez utiliser tooinstall hello le système de gestion de base de données relationnelle (SGBDR) pour un système SAP. Par exemple, si vous déployez un modèle ASCS/SCS pour les cinq systèmes SAP, vous devez toodeploy ce modèle cinq fois.

tooset modèle de multi-SID de base de données hello, Bonjour [modèle de base de données multi-SID] [ sap-templates-3-tier-multisid-db-marketplace-image] ou [modèle multi-SID de base de données à l’aide de disques gérés] [ sap-templates-3-tier-multisid-db-marketplace-image-md], entrez des valeurs pour hello paramètres suivants :

  -  **ID du système SAP**. Entrez l’ID du système SAP hello Hello système SAP tooinstall. Hello ID sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.
  -  **Type de système d’exploitation**. Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.
  -  **Type de base de données**. Sélectionnez le type de hello de base de données hello souhaité tooinstall sur le cluster de hello. Sélectionnez **SQL** si vous souhaitez tooinstall Microsoft SQL Server. Sélectionnez **HANA** si vous envisagez de tooinstall SAP HANA sur des machines virtuelles de hello. Assurez-vous que tooselect hello type de système d’exploitation correct : sélectionnez **Windows** pour SQL, sélectionnez une distribution Linux pour HANA. Hello équilibrage de charge Azure qui est connecté toohello ordinateurs virtuels doivent être configurés type de base de données toosupport hello sélectionné :
    * **SQL**. équilibrage de charge Hello est le port 1433 équilibrer la charge. Assurez-vous que toouse ce port pour votre installation de SQL Server Always On.
    * **HANA**. équilibrage de charge Hello sera équilibrer la charge de ports 35015 et 35017. Assurez-vous que tooinstall SAP HANA avec numéro d’instance **50**.
    équilibrage de charge Hello utilisera le port de la sonde 62550.
  -  **Taille du système SAP**. Nombre de hello ensemble du système de nouveau hello SAP fournit. Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, demandez à votre partenaire technologique SAP ou un intégrateur de système.
  -  **Disponibilité du système**. Sélectionnez la haute disponibilité **(HA)**.
  -  **Nom d’utilisateur et mot de passe d’administrateur**. Créer un utilisateur qui peut être utilisé toosign dans toohello machine.
  -  **ID du sous-réseau**. Entrez hello les ID de sous-réseau hello que vous avez utilisé lors du déploiement hello du modèle ASCS/SCS hello ou hello de sous-réseau hello qui a été créé dans le cadre de hello déploiement de modèle ASCS/SCS.

#### <a name="application-servers-template"></a> Modèle de serveurs d’applications

modèle de serveurs d’application Hello déploie deux ou plusieurs ordinateurs virtuels qui peut être utilisés en tant qu’instances de serveur d’applications SAP pour un système SAP. Par exemple, si vous déployez un modèle ASCS/SCS pour les cinq systèmes SAP, vous devez toodeploy ce modèle cinq fois.

tooset des hello serveurs multi-SID modèle d’application Bonjour [ce modèle d’application serveurs multi-SID] [ sap-templates-3-tier-multisid-apps-marketplace-image] ou [modèle de SID de plusieurs serveurs d’application à l’aide de disques gérés] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], entrez des valeurs pour hello paramètres suivants :

  -  **ID du système SAP**. Entrez l’ID du système SAP hello Hello système SAP tooinstall. Hello ID sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.
  -  **Type de système d’exploitation**. Sélectionnez le système d’exploitation de hello d’ordinateurs virtuels hello.
  -  **Taille du système SAP**. nombre de Hello du nouveau système SAP hello fournissent. Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, demandez à votre partenaire technologique SAP ou un intégrateur de système.
  -  **Disponibilité du système**. Sélectionnez la haute disponibilité **(HA)**.
  -  **Nom d’utilisateur et mot de passe d’administrateur**. Créer un utilisateur qui peut être utilisé toosign dans toohello machine.
  -  **ID du sous-réseau**. Entrez hello les ID de sous-réseau hello que vous avez utilisé lors du déploiement hello du modèle ASCS/SCS hello ou hello de sous-réseau hello qui a été créé dans le cadre de hello déploiement de modèle ASCS/SCS.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Réseau virtuel Azure
Dans notre exemple, espace d’adressage hello Hello réseau virtuel Azure est 10.0.0.0/16. Il existe un sous-réseau appelé **Subnet** (Sous-réseau), avec la plage d’adresses 10.0.0.0/24. L’ensemble des machines virtuelles et des équilibrages de charge internes sont déployés au sein de ce réseau virtuel.

> [!IMPORTANT]
> N’apportez aucune modification des paramètres de réseau toohello à l’intérieur du système d’exploitation de hello invité. (adresses IP, serveurs DNS, sous-réseau, etc.). Configurez tous vos paramètres réseau dans Azure. Hello service de Configuration protocole DHCP (Dynamic Host) propage vos paramètres.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a>Adresses IP DNS

tooset hello nécessaire que des adresses IP DNS, hello comme suit.

1.  Bonjour portail Azure, sur hello **serveurs DNS** panneau, assurez-vous que votre réseau virtuel **serveurs DNS** option a la valeur trop**personnalisé DNS**.
2.  Sélectionnez vos paramètres en fonction de type hello du réseau que vous avez. Pour plus d’informations, consultez hello suivant des ressources :
    * [Connectivité de réseau d’entreprise (intersite)][planning-guide-2.2]: ajouter hello des adresses IP des serveurs DNS de local hello.  
    Vous pouvez étendre locale DNS serveurs toohello machines virtuelles qui s’exécutent dans Azure. Dans ce scénario, vous pouvez ajouter des adresses IP de hello Hello Azure des machines virtuelles sur lequel vous exécutez le service DNS hello.
    * [Déploiement de cloud uniquement][planning-guide-2.1]: déployer un ordinateur virtuel supplémentaire dans hello même instance de réseau virtuel qui sert à un serveur DNS. Ajouter des adresses IP hello Hello Azure des machines virtuelles que vous avez configuré le service DNS toorun.

    ![Figure 12 : Configurer les serveurs DNS du réseau virtuel Azure][sap-ha-guide-figure-3001]

    _**Figure 12 :** Configurer les serveurs DNS du réseau virtuel Azure_

  > [!NOTE]
  > Si vous modifiez les adresses IP de hello des serveurs DNS de hello, vous devez toorestart hello machines virtuelles tooapply hello de modification et de propager les nouveaux serveurs DNS de hello.
  >
  >

Dans notre exemple, hello service DNS est installé et configuré sur ces ordinateurs virtuels de Windows :

| Rôle de la machine virtuelle | Nom d’hôte de la machine virtuelle | Nom de la carte réseau | Adresse IP statique |
| --- | --- | --- | --- |
| Premier serveur DNS |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| Deuxième serveur DNS |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Les noms d’hôte et des adresses IP statiques pour l’instance en cluster de SAP ASCS/SCS hello et l’instance en cluster du SGBD

Pour un déploiement local, vous avez besoin des noms d’hôtes et adresses IP réservés suivants :

| Rôle du nom d’hôte virtuel | Nom d’hôte virtuel | Adresse IP statique virtuelle |
| --- | --- | --- |
| Nom d’hôte virtuel du premier cluster SAP ASCS/SCS (pour la gestion du cluster) |pr1-ascs-vir |10.0.0.42 |
| Nom d’hôte virtuel de l’instance SAP ASCS/SCS |pr1-ascs-sap |10.0.0.43 |
| Nom d’hôte virtuel du deuxième cluster SAP SGBD (gestion du cluster) |pr1-dbms-vir |10.0.0.32 |

Lorsque vous créez le cluster de hello, les noms d’hôte virtuel hello créer **pr1-ASC-vir** et **pr1-SGBD-vir** et hello associés à des adresses IP qui gèrent le cluster hello lui-même. Pour plus d’informations sur la façon toodo, consultez [collecter les nœuds de cluster dans une configuration de cluster][sap-ha-guide-8.12.1].

Vous pouvez créer manuellement hello autres deux noms d’hôte virtuel, **pr1 ASC sap** et **pr1 SGBD sap**, et hello associés à des adresses IP sur le serveur DNS de hello. Hello instance SAP ASCS/SCS en cluster et instance de SGBD hello en cluster utilisent ces ressources. Pour plus d’informations sur la façon toodo, consultez [créer un nom d’hôte virtuel pour une instance SAP ASCS/SCS cluster][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Définir les adresses IP statiques pour les ordinateurs virtuels SAP hello
Après avoir déployé toouse de machines virtuelles hello dans votre cluster, vous devez tooset des adresses IP statiques pour tous les ordinateurs virtuels. Cela dans la configuration de réseau virtuel Azure hello et pas dans le système de d’exploitation invité hello.

1.  Bonjour portail Azure, sélectionnez **groupe de ressources** > **carte réseau** > **paramètres** > **adresse IP** .
2.  Sur hello **des adresses IP** panneau, sous **affectation**, sélectionnez **statique**. Bonjour **adresse IP** , entrez l’adresse IP de hello que vous souhaitez toouse.

  > [!NOTE]
  > Si vous changez d’adresse IP de hello hello de carte de réseau, vous devez toorestart hello machines virtuelles tooapply hello de modification.  
  >
  >

  ![Figure 13 : Définir des adresses IP statiques pour la carte réseau de hello de chaque ordinateur virtuel][sap-ha-guide-figure-3002]

  _**Figure 13 :** définir les adresses IP statiques pour la carte réseau de hello de chaque ordinateur virtuel_

  Répétez cette étape pour toutes les interfaces réseau, autrement dit, pour tous les ordinateurs virtuels, y compris les ordinateurs virtuels que vous souhaitez toouse pour votre service Active Directory/DNS.

Dans notre exemple, nous avons les machines virtuelles et les adresses IP statiques suivantes :

| Rôle de la machine virtuelle | Nom d’hôte de la machine virtuelle | Nom de la carte réseau | Adresse IP statique |
| --- | --- | --- | --- |
| Première instance du serveur d’applications SAP |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| Deuxième instance du serveur d’applications SAP |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Dernière instance du serveur d’applications SAP serveur d’applications SAP |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| Premier nœud de cluster pour l’instance ASCS/SCS |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| Deuxième nœud de cluster pour l’instance ASCS/SCS |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| Premier nœud de cluster pour l’instance SGBD |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| Deuxième nœud de cluster pour l’instance SGBD |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Définissez une adresse IP statique pour l’équilibrage de charge interne Azure hello

modèle de SAP Azure Resource Manager Hello crée un équilibreur de charge interne Azure qui est utilisé pour l’instance SAP ASCS/SCS hello et clusters de SGBD hello.

> [!IMPORTANT]
> Hello adresse IP du nom d’hôte virtuel hello Hello SAP ASCS/SCS est hello même en tant qu’adresse IP de hello Hello équilibreur de charge interne SAP ASCS/SCS : **pr1-lb-ASC**.
> Hello adresse IP du nom virtuel de hello Hello SGBD est hello même en tant qu’adresse IP de hello Hello équilibreur de charge interne SGBD : **pr1-lb-SGBD**.
>
>

équilibrage de charge tooset une adresse IP statique pour hello Azure interne :

1.  Hello déploiement initial définit adresse IP d’équilibrage de charge interne hello trop**dynamique**. Bonjour portail Azure, sur hello **des adresses IP** panneau, sous **affectation**, sélectionnez **statique**.
2.  Définir l’adresse IP de hello d’équilibreur de charge interne hello **pr1-lb-ASC** adresse toohello de nom d’hôte virtuel hello d’instance de SAP ASCS/SCS hello.
3.  Définir l’adresse IP de hello d’équilibreur de charge interne hello **pr1-lb-SGBD** adresse toohello de nom d’hôte virtuel hello d’instance de SGBD hello.

  ![La figure 14 : Définir des adresses IP statiques pour l’équilibrage de charge interne hello pour l’instance de SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  _**La figure 14 :** définir des adresses IP statiques pour l’équilibrage de charge interne hello pour l’instance de SAP ASCS/SCS hello_

Dans notre exemple, nous avons deux équilibrages de charge internes Azure qui présentent les adresses IP statiques suivantes :

| Rôle de l’équilibrage de charge interne Azure | Nom de l’équilibrage de charge interne Azure | Adresse IP statique |
| --- | --- | --- |
| Équilibrage de charge interne de l’instance SAP ASCS/SCS |pr1-lb-ascs |10.0.0.43 |
| Équilibrage de charge interne du SGBD SAP |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Par défaut pour l’équilibrage de charge interne Azure hello les règles d’équilibrage de charge ASCS/SCS

modèle de SAP Azure Resource Manager Hello crée des ports hello que vous avez besoin :
* Une instance ABAP ASCS, avec le numéro d’instance par défaut hello **00**
* Une instance Java SCS, avec le numéro d’instance par défaut hello **01**

Lorsque vous installez votre instance SAP ASCS/SCS, vous devez utiliser le numéro d’instance par défaut hello **00** votre ABAP ASCS instance et hello par défaut instance numéro **01** pour votre instance Java SCS.

Ensuite, créez des points de terminaison pour les ports de SAP NetWeaver hello d’équilibrage de charge d’interne requise.

toocreate requis de points de terminaison de l’équilibrage de charge interne, créez tout d’abord, ces points de terminaison pour les ports de SAP NetWeaver ABAP ASC hello d’équilibrage de charge :

| Service/nom de la règle d’équilibrage de charge | Numéros de ports par défaut | Ports concrets pour (instance ASCS avec numéro d’instance 00) (ERS avec 10) |
| --- | --- | --- |
| Serveur de file d’attente / *lbrule3200* |32<*NuméroInstance*> |3200 |
| Serveur de messages ABAP / *lbrule3600* |36<*NuméroInstance*> |3600 |
| Message ABAP interne / *lbrule3900* |39<*NuméroInstance*> |3900 |
| Serveur de messages HTTP / *Lbrule8100* |81<*NuméroInstance*> |8100 |
| Service de démarrage SAP ASCS HTTP / *Lbrule50013* |5<*NuméroInstance*>13 |50013 |
| Service de démarrage SAP ASCS HTTPS / *Lbrule50014* |5<*NuméroInstance*>14 |50014 |
| Réplication de la file d’attente / *Lbrule50016* |5<*NuméroInstance*>16 |50016 |
| Service de démarrage SAP ERS HTTP / *Lbrule51013* |5<*NuméroInstance*>13 |51013 |
| Service de démarrage SAP ERS HTTP / *Lbrule51014* |5<*NuméroInstance*>14 |51014 |
| WinRM *Lbrule5985* | |5985 |
| Partage de fichiers *Lbrule445* | |445 |

_**Tableau 1 :** numéros d’instances de SAP NetWeaver ABAP ASC hello de Port_

Ensuite, créez ces points de terminaison pour les ports de SAP NetWeaver Java SCS hello d’équilibrage de charge :

| Service/nom de la règle d’équilibrage de charge | Numéros de ports par défaut | Ports concrets pour (instance SCS avec numéro d’instance 01) (ERS avec 11) |
| --- | --- | --- |
| Serveur de file d’attente / *lbrule3201* |32<*NuméroInstance*> |3201 |
| Serveur de passerelle / *lbrule3301* |33<*NuméroInstance*> |3301 |
| Serveur de messages Java / *lbrule3900* |39<*NuméroInstance*> |3901 |
| Serveur de messages HTTP / *Lbrule8101* |81<*NuméroInstance*> |8101 |
| Service de démarrage SAP SCS HTTP / *Lbrule50113* |5<*NuméroInstance*>13 |50113 |
| Service de démarrage SAP SCS HTTPS / *Lbrule50114* |5<*NuméroInstance*>14 |50114 |
| Réplication de la file d’attente / *Lbrule50116* |5<*NuméroInstance*>16 |50116 |
| Service de démarrage SAP ERS HTTP / *Lbrule51113* |5<*NuméroInstance*>13 |51113 |
| Service de démarrage SAP ERS HTTP / *Lbrule51114* |5<*NuméroInstance*>14 |51114 |
| WinRM *Lbrule5985* | |5985 |
| Partage de fichiers *Lbrule445* | |445 |

_**Tableau 2 :** numéros d’instances de SAP NetWeaver Java SCS hello de Port_

![Figure 15 : Par défaut ASCS/SCS équilibrage de la charge des règles pour l’équilibrage de charge interne Azure hello][sap-ha-guide-figure-3004]

_**Figure 15 :** règles pour l’équilibrage de charge interne Azure hello équilibrage de la valeur par défaut ASCS/SCS_

Définir l’adresse IP de hello d’équilibrage de charge hello **pr1-lb-SGBD** adresse toohello de nom d’hôte virtuel hello d’instance de SGBD hello.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Modifier les règles pour l’équilibrage de charge interne Azure hello d’équilibrage de charge de valeur par défaut ASCS/SCS de hello

Si vous souhaitez toouse différents nombres pour hello ASCS SAP ou des instances SCS, vous devez modifier les noms de hello et les valeurs de leurs ports des valeurs par défaut.

1.  Bonjour portail Azure, sélectionnez  **<* SID*> - lb - ASC charge équilibrage ** > **règles d’équilibrage de charge**.
2.  Pour les règles qui appartiennent toohello ASCS SAP ou instance SCS d’équilibrage de charge tous les, modifiez ces valeurs :

  * Nom
  * Port
  * Port principal

  Par exemple, si vous souhaitez que le numéro d’instance ASC toochange hello par défaut à partir de 00 too31, vous devez les modifications de hello toomake pour tous les ports répertoriés dans le tableau 1.

  Voici un exemple de mise à jour pour le port *lbrule3200*.

  ![Figure 16 : Modifier des règles pour l’équilibrage de charge interne Azure hello d’équilibrage de charge de valeur par défaut ASCS/SCS de hello][sap-ha-guide-figure-3005]

  _**Figure 16 :** modification hello ASCS/SCS par défaut l’équilibrage de charge des règles pour l’équilibrage de charge interne Azure hello_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Ajouter le domaine toohello de machines virtuelles Windows

Une fois que vous affectez un statique IP adresse toohello les ordinateurs virtuels, ajoutez le domaine de toohello de machines virtuelles de hello.

![Figure 17 : Ajouter un domaine tooa de machine virtuelle][sap-ha-guide-figure-3006]

_**Figure 17 :** ajouter un domaine tooa de machine virtuelle_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Ajouter des entrées de Registre sur les deux nœuds de cluster de l’instance de SAP ASCS/SCS hello

L’équilibrage de charge Azure a un équilibreur de charge interne que les connexions se ferme quand les connexions hello sont inactives pendant un laps de temps (délai d’inactivité). Le processus de travail SAP dans la boîte de dialogue instances connexions ouvertes toohello SAP enqueue traiter dès que hello première file d’attente/de retrait demande toobe besoins envoyé. Ces connexions sont généralement établies jusqu'à ce que le processus de travail hello ou hello du processus de file d’attente. Toutefois, si la connexion de hello est inactive pendant un laps de temps défini, hello connexions hello de charge interne Azure équilibrage se ferme. Cela n’est pas un problème car hello processus de travail SAP rétablit le processus de file d’attente toohello hello connexion si elle n’existe plus. Ces activités sont documentées dans les traces de développeur hello processus SAP, mais ils créent une grande quantité de contenu supplémentaire dans les traces. Il s’agit d’un Bonjour de toochange conseillé TCP/IP `KeepAliveTime` et `KeepAliveInterval` sur les deux nœuds de cluster. Combiner ces modifications dans les paramètres TCP/IP hello avec des paramètres de profil SAP, décrites plus loin dans l’article de hello.

tooadd les entrées de Registre sur les deux nœuds de cluster d’instance SAP ASCS/SCS hello, ajoutent d’abord ces entrées de Registre Windows sur les deux nœuds de cluster Windows pour SAP ASCS/SCS :

| Chemin | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nom de la variable |`KeepAliveTime` |
| Type de variable |REG_DWORD (décimal) |
| Valeur |120 000 |
| Lien toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tableau 3 :** modification hello premier TCP/IP paramètre_

Puis, ajoutez ces entrées de registre Windows aux deux nœuds de cluster Windows pour l’instance SAP ASCS/SCS :

| Chemin | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nom de la variable |`KeepAliveInterval` |
| Type de variable |REG_DWORD (décimal) |
| Valeur |120 000 |
| Lien toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tableau 4 :** modification hello deuxième TCP/IP paramètre_

**modifications de hello tooapply, redémarrez les deux nœuds de cluster**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurer un cluster de clustering de basculement Windows Server pour une instance SAP ASCS/SCS

La configuration d’un cluster de basculement Windows Server pour une instance SAP ASCS/SCS implique les tâches suivantes :

- Collecte des nœuds de cluster hello dans une configuration de cluster
- Configurer un témoin de partage de fichiers de cluster

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Collecter les nœuds de cluster hello dans une configuration de cluster

1.  Dans Ajouter un rôle de hello Assistant et de fonctionnalités, ajouter tooboth les nœuds de cluster de clustering de basculement.
2.  Configurer le cluster de basculement hello à l’aide du Gestionnaire du Cluster de basculement. Dans le Gestionnaire de Cluster de basculement, sélectionnez **création d’un Cluster**, puis ajoutez uniquement hello nom de cluster première hello, nœud A. N’ajoutez pas de nœud de deuxième hello vous allez ajouter le nœud de deuxième hello dans une étape ultérieure.

  ![La figure 18 : Ajouter hello nom du serveur ou ordinateur virtuel du premier nœud de cluster hello][sap-ha-guide-figure-3007]

  _**La figure 18 :** ajouter hello machine virtuelle nom du serveur ou du premier nœud de cluster hello_

3.  Entrez le nom hello réseau (nom d’hôte virtuel) du cluster de hello.

  ![Figure 19 : Entrez le nom du cluster hello][sap-ha-guide-figure-3008]

  _**Figure 19 :** Entrez le nom de cluster hello_

4.  Une fois que vous avez créé le cluster de hello, exécutez un test de validation de cluster.

  ![Figure 20 : Exécuter la vérification de validation de cluster de hello][sap-ha-guide-figure-3009]

  _**Figure 20 :** exécuter le contrôle de validation de cluster hello_

  Vous pouvez ignorer les avertissements relatifs à des disques à ce stade dans le processus de hello. Vous allez ajouter qu'un témoin de partage de fichiers et de hello SIOS des disques partagés plus tard. À ce stade, vous n’avez pas besoin tooworry sur ayant un quorum.

  ![Figure 21 : Aucun disque quorum trouvé][sap-ha-guide-figure-3010]

  _**Figure 21 :** Aucun disque quorum trouvé_

  ![Figure 22 : La ressource principale du cluster a besoin d’une nouvelle adresse IP][sap-ha-guide-figure-3011]

  _**Figure 22 :** La ressource principale du cluster a besoin d’une nouvelle adresse IP_

5.  Modifier l’adresse IP de hello hello principaux du service de cluster. Hello ne peut pas le démarrage du cluster jusqu'à ce que vous modifiez l’adresse IP de hello hello principaux du service de cluster, car les points de l’adresse hello du serveur de hello tooone de nœuds de machine virtuelle hello. Cela sur hello **propriétés** page de ressource d’IP du service cluster hello core.

  Par exemple, nous devons tooassign une adresse IP (dans notre exemple, **10.0.0.42**) pour le nom d’hôte virtuel de cluster de hello **pr1-ASC-vir**.

  ![Figure 23 : Modifier dans la boîte de dialogue de propriétés hello, adresse IP de hello][sap-ha-guide-figure-3012]

  _**La figure 23 :** Bonjour **propriétés** boîte de dialogue, de modifier l’adresse IP hello_

  ![Figure 24 : Affecter des adresses IP hello qui est réservée pour le cluster de hello][sap-ha-guide-figure-3013]

  _**Figure 24 :** affecter l’adresse IP hello qui est réservée pour le cluster de hello_

6.  Mettez le nom d’hôte virtuel cluster hello en ligne.

  ![Figure 25 : Le service principal de Cluster est activé et en cours d’exécution et avec hello Corrigez l’adresse IP][sap-ha-guide-figure-3014]

  _**Figure 25 :** service principal de Cluster est activé et en cours d’exécution et avec hello Corrigez l’adresse IP_

7.  Ajouter le second nœud de cluster hello.

  Maintenant que le service de cluster hello principal est en cours d’exécution, vous pouvez ajouter le second nœud de cluster hello.

  ![Figure 26 : Ajouter le second nœud de cluster hello][sap-ha-guide-figure-3015]

  _**Figure 26 :** ajouter hello second nœud de cluster_

8.  Entrez un nom pour le second hôte de nœud de cluster hello.

  ![Figure 27 : Entrez le nom d’hôte de nœud de hello deuxième cluster][sap-ha-guide-figure-3016]

  _**Figure 27 :** nom d’entrée hello deuxième cluster nœud hôte_

  > [!IMPORTANT]
  > Veillez à ce que hello **ajouter tous les totalité du stockage du cluster toohello** case à cocher est **pas** sélectionné.  
  >
  >

  ![Figure 28 : Ne sélectionnez pas la case à cocher hello][sap-ha-guide-figure-3017]

  _**Figure 28 :** faire **pas** sélectionnez hello case à cocher_

  Vous pouvez ignorer les avertissements concernant le quorum et les disques. Vous devez définir hello quorum et partage hello disque ultérieurement, comme décrit dans [installation SIOS DataKeeper Cluster Edition pour le partage de disque du cluster de SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Figure 29 : Ignorer les avertissements sur le quorum de disque hello][sap-ha-guide-figure-3018]

  _**Figure 29 :** ignorer les avertissements sur le quorum de disque hello_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurer un témoin de partage de fichiers de cluster

La configuration d’un témoin de partage de fichiers de cluster implique les tâches suivantes :

- Création d'un partage de fichiers
- Configuration de quorum de témoin de partage de fichiers hello Gestionnaire du Cluster de basculement

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Créer un partage de fichiers

1.  Sélectionnez un témoin de partage de fichiers plutôt qu’un disque quorum. SIOS DataKeeper prend en charge cette option.

  Dans les exemples hello dans cet article, le témoin de partage de fichiers hello est sur le serveur DNS d’Active Directory/hello qui s’exécute dans Azure. Hello témoin de partage de fichiers est appelée **domcontr-0**. Il serez que vous avez configuré un tooAzure de la connexion VPN (via un VPN de Site à Site ou ExpressRoute Azure), témoin de partage de votre Active Directory/DNS service est sur site et n’est pas un fichier de toorun approprié.

  > [!NOTE]
  > Si votre service Active Directory/DNS s’exécute uniquement sur site, ne configurez pas votre témoin de partage de fichiers sur système d’exploitation Active Directory/DNS Windows hello locale est en cours d’exécution. La latence du réseau entre les nœuds de cluster exécutés dans Azure et le service Active Directory/DNS local peut être trop importante et entraîner des problèmes de connectivité. Être vraiment tooconfigure hello partage témoin de fichiers sur une machine virtuelle Azure qui exécute le nœud de cluster toohello fermer.  
  >
  >

  lecteur de quorum Hello doit au moins 1 024 Mo d’espace libre. Nous vous recommandons de 2 048 Mo d’espace libre pour le lecteur quorum hello.

2.  Ajoutez l’objet nom de cluster hello.

  ![La figure 30 : Affecter des autorisations de hello sur Partage hello pour l’objet nom de cluster hello][sap-ha-guide-figure-3019]

  _**La figure 30 :** affecter des autorisations hello sur Partage hello pour l’objet nom de cluster hello_

  Assurez-vous que les autorisations hello incluent des données toochange de l’autorité hello dans un partage de hello pour l’objet nom de cluster hello (dans notre exemple, **pr1-ASC-vir$**).

3.  tooadd hello cluster nom objet toohello liste, sélectionnez **ajouter**. Modifiez toocheck de filtre hello pour les objets ordinateur dans toothose Ajout indiqué dans la Figure 31.

  ![Figure 31 : Modifier les ordinateurs tooinclude hello les Types d’objets][sap-ha-guide-figure-3020]

  _**Figure 31 :** modifier hello Types d’objet tooinclude ordinateurs_

  ![Figure 32 : Sélectionnez la case à cocher ordinateurs hello][sap-ha-guide-figure-3021]

  _**La figure 32 :** hello sélectionnez **ordinateurs** case à cocher_

4.  Entrez l’objet nom de cluster hello comme indiqué dans la Figure 31. Car hello enregistrement a déjà été créé, vous pouvez modifier les autorisations de hello, comme indiqué dans la Figure 30.

5.  Sélectionnez hello **sécurité** onglet de partage de hello et définissez les autorisations pour l’objet nom de cluster hello plus détaillée.

  ![Figure 33 : Définir les attributs de sécurité hello pour l’objet nom de cluster hello sur le quorum du partage de fichier hello][sap-ha-guide-figure-3022]

  _**Figure 33 :** définir les attributs de sécurité hello pour l’objet nom de cluster hello sur le quorum du partage de fichier hello_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Quorum témoin de partage de fichiers hello ensemble gestionnaire du Cluster de basculement

1.  Ouvrez hello Assistant Configuration de Quorum du paramètre.

  ![Figure 34 : Démarrer l’Assistant Configuration du paramètre de Quorum du Cluster de hello][sap-ha-guide-figure-3023]

  _**Figure 34 :** Start hello Assistant Configuration des paramètres du Quorum de Cluster_

2.  Sur hello **sélectionner la Configuration de Quorum** , sélectionnez **sélectionner le témoin de quorum hello**.

  ![Figure 35 : Configurations de quorum sélectionnables][sap-ha-guide-figure-3024]

  _**Figure 35 :** Configurations de quorum sélectionnables_

3.  Sur hello **sélectionner le témoin de Quorum** , sélectionnez **configurer un témoin de partage de fichiers**.

  ![Figure 36 : Témoin de partage de fichier hello Select][sap-ha-guide-figure-3025]

  _**Figure 36 :** sélectionnez hello témoin de partage de fichiers_

4.  Entrez le partage de fichiers toohello hello UNC chemin (dans notre exemple, \\domcontr-0\FSW). toosee une liste de modifications hello possibles, sélectionnez **suivant**.

  ![Figure 37 : Définir l’emplacement du partage de fichier pour partage de témoin hello hello][sap-ha-guide-figure-3026]

  _**Figure 37 :** définir l’emplacement du partage de fichier pour partage de témoin hello hello_

5.  Sélectionnez hello modifications souhaitées, puis sélectionnez **suivant**. Vous devez toosuccessfully reconfigurer la configuration du cluster hello comme indiqué dans la Figure 38.  

  ![Figure 38 : Confirmation que vous avez reconfiguré le cluster de hello][sap-ha-guide-figure-3027]

  _**Figure 38 :** Confirmation que vous avez reconfiguré le cluster de hello_

Après avoir installé hello Cluster de basculement Windows avec succès, les modifications doivent toobe apportée toosome seuils tooadapt basculement détection tooconditions dans Azure. Hello toobe paramètres modifié sont documentées dans ce billet de blog : https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. En supposant que vos deux machines virtuelles qui générer hello Configuration en Cluster Windows pour ASCS/SCS sont dans hello même sous-réseau, hello paramètres suivants doivent toobe modifié toothese valeurs :
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Ces paramètres ont été testés avec les clients et fournis un bon compromis toobe suffisamment résilient hello un côté. Sur hello contre ces paramètres ont été fournissant rapide suffisamment basculement dans les conditions d’erreur réelle en cas d’échec de nœud/machine virtuelle ou de logiciels SAP. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Installer SIOS DataKeeper Cluster Edition pour le disque de partage de cluster hello SAP ASCS/SCS

Vous disposez maintenant d’une configuration fonctionnelle de clustering de basculement Windows Server dans Azure. Mais, tooinstall une instance SAP ASCS/SCS, vous avez besoin d’une ressource de disque partagé. Impossible de créer des ressources de disque hello partagé que nécessaires dans Azure. SIOS DataKeeper Cluster Edition est une solution de tiers que vous pouvez utiliser les ressources de disque toocreate partagé.

Installation de l’édition de Cluster SIOS DataKeeper pour hello SAP ASCS/SCS disque de cluster partage implique les tâches :

- Ajout de hello .NET Framework 3.5
- Installation de SIOS DataKeeper
- Configuration de SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Ajouter hello .NET Framework 3.5
Hello Microsoft .NET Framework 3.5 n’est pas automatiquement activé ou installé sur Windows Server 2012 R2. SIOS DataKeeper nécessitant toobe de .NET Framework hello sur tous les nœuds que vous installez DataKeeper sur, vous devez installer hello .NET Framework 3.5 sur hello systèmes d’exploitation de tous les ordinateurs virtuels dans un cluster de hello.

Il existe deux hello de tooadd méthodes .NET Framework 3.5 :

- Utiliser hello ajouter Assistant de rôles et fonctionnalités dans Windows, comme indiqué dans la Figure 39.

  ![Figure 39 : Installer hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant][sap-ha-guide-figure-3028]

  _**Figure 39 :** hello installer .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant_

  ![Figure 40 : Progression de l’Installation de la barre lorsque vous installez hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant][sap-ha-guide-figure-3029]

  _**Figure 40 :** progression de l’Installation de la barre lorsque vous installez hello .NET Framework 3.5 à l’aide de hello Ajout de rôles et fonctionnalités Assistant_

- À présent utiliser dism.exe d’outil de ligne de commande hello. Pour ce type d’installation, vous avez besoin d’un répertoire SxS tooaccess hello hello support d’installation Windows. Dans une invite de commandes avec élévation de privilèges, tapez :

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> Installer SIOS DataKeeper

Installez SIOS DataKeeper Cluster Edition sur chaque nœud de cluster de hello. un stockage partagé virtuel toocreate avec SIOS DataKeeper, créer un miroir synchronisé et simuler ensuite le stockage partagé de cluster.

Avant d’installer des logiciels SIOS hello, créez l’utilisateur de domaine hello **DataKeeperSvc**.

> [!NOTE]
> Ajouter hello **DataKeeperSvc** utilisateur toohello **administrateur Local** groupe sur les deux nœuds de cluster.
>
>

tooinstall SIOS DataKeeper :

1.  Installer le logiciel SIOS hello sur les deux nœuds de cluster.

  ![Programme d’installation de SIOS][sap-ha-guide-figure-3030]

  ![Figure 41 : Première page de hello SIOS DataKeeper installation][sap-ha-guide-figure-3031]

  _**Figure 41 :** première page de hello SIOS DataKeeper installation_

2.  Dans la boîte de dialogue hello indiqué dans la Figure 42, sélectionnez **Oui**.

  ![Figure 42 : DataKeeper vous indique qu’un service va être désactivé][sap-ha-guide-figure-3032]

  _**Figure 42 :** DataKeeper vous indique qu’un service va être désactivé_

3.  Dans la boîte de dialogue hello illustré à la Figure 43, nous vous recommandons de sélectionner **compte de domaine ou serveur**.

  ![Figure 43 : Sélection de l’utilisateur de SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Figure 43:** Sélection de l’utilisateur de SIOS DataKeeper_

4.  Entrez le nom d’utilisateur domaine hello et des mots de passe que vous avez créé pour SIOS DataKeeper.

  ![Figure 44 : Entrez les nom d’utilisateur de domaine de hello et un mot de passe pour hello SIOS DataKeeper installation][sap-ha-guide-figure-3034]

  _**Figure 44 :** Entrez le nom d’utilisateur de domaine de hello et un mot de passe pour hello SIOS DataKeeper installation_

5.  Installez la clé de licence hello pour votre instance de SIOS DataKeeper, comme indiqué dans la Figure 45.

  ![Figure 45 : Entrer votre clé licence SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Figure 45 :** Entrer votre clé de licence SIOS DataKeeper_

6.  Lorsque vous y êtes invité, redémarrez hello virtual machine.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurer SIOS DataKeeper

Après avoir installé SIOS DataKeeper sur les deux nœuds, vous avez besoin de configuration de hello toostart. Hello configuration de hello vise toohave la réplication synchrone des données entre des disques supplémentaires hello attaché tooeach d’ordinateurs virtuels hello.

1.  Démarrer hello DataKeeper Management et l’outil de Configuration, puis sélectionnez **connexion serveur**. (Cette option est entourée en rouge dans la figure 46.)

  ![Figure 46 : Outil de configuration et de gestion de SIOS DataKeeper][sap-ha-guide-figure-3036]

  _**Figure 46 :** Outil de configuration et de gestion de SIOS DataKeeper_

2.  Entrez hello nom ou adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à, puis, dans un deuxième temps, le nœud de deuxième hello.

  ![Figure 47 : Insérer le nom hello ou une adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à et dans un deuxième temps, le nœud de deuxième hello][sap-ha-guide-figure-3037]

  _**Figure 47 :** insérer le nom hello ou une adresse TCP/IP de hello premier nœud hello outil et de gestion Configuration doit se connecter à et dans un deuxième temps, le nœud de deuxième hello_

3.  Créer un travail de réplication hello entre deux nœuds de hello.

  ![Figure 48 : Créer un travail de réplication][sap-ha-guide-figure-3038]

  _**Figure 48 :** Créer un travail de réplication_

  Un Assistant vous guide tout au long des processus de hello de création d’un travail de réplication.
4.  Définissez hello nom et adresse TCP/IP, volume de disque du nœud de source de hello.

  ![Figure 49 : Définissez le nom de hello du travail de réplication hello][sap-ha-guide-figure-3039]

  _**Figure 49 :** nom hello de définir de tâche de réplication hello_

  ![Figure 50 : Définir les données de base hello pour nœud hello, qui doit être de nœud de source hello actuel][sap-ha-guide-figure-3040]

  _**Figure 50 :** définissent les données de base hello pour nœud hello, qui doit être de nœud de source hello actuel_

5.  Définissez hello nom et adresse TCP/IP, volume de disque du nœud cible de hello.

  ![Figure 51 : Définir les données de base hello pour nœud hello, qui doit être nœud cible en cours de hello][sap-ha-guide-figure-3041]

  _**Figure 51 :** définissent les données de base hello pour nœud hello, qui doit être nœud cible en cours de hello_

6.  Définir les algorithmes de compression hello. Dans notre exemple, nous vous recommandons de compresser les flux de réplication hello. En particulier dans les situations de resynchronisation, la compression du flux de réplication hello hello réduit considérablement les temps de resynchronisation. Notez que la compression utilise des ressources de processeur et de RAM hello d’un ordinateur virtuel. Comme le taux de compression hello augmente, donc hello que le volume de ressources du processeur utilisées. Vous pouvez également ajuster ce paramètre ultérieurement.

7.  Un autre paramètre, vous devez toocheck sera si hello réplication synchrone ou asynchrone. *Lorsque vous protégez des configurations SAP ASCS/SCS, vous devez utiliser la réplication synchrone*.  

  ![Figure 52 : Définir les détails de la réplication][sap-ha-guide-figure-3042]

  _**Figure 52 :** Définir les détails de la réplication_

8.  Définir si le volume hello répliquée par le travail de réplication hello doit être représenté tooa configuration de cluster Clustering de basculement Windows Server comme un disque partagé. Pour une configuration SAP ASCS/SCS hello, sélectionnez **Oui** afin que Windows hello cluster voit hello volume répliqué comme un disque partagé qu’il peut utiliser comme un volume de cluster.

  ![Figure 53 : Sélectionnez Oui tooset hello répliquées volume comme volume de cluster][sap-ha-guide-figure-3043]

  _**Figure 53 :** sélectionnez **Oui** tooset hello répliquées que le volume d’un cluster_

  Après la création de volume de hello, outil de Configuration et la gestion de DataKeeper hello illustre que cette tâche de réplication hello est active.

  ![Figure 54 : DataKeeper mise en miroir synchrone de hello SAP ASCS/SCS partage de disque est actif][sap-ha-guide-figure-3044]

  _**Figure 54 :** la mise en miroir synchrone de DataKeeper pour hello SAP ASCS/SCS de partage de disque est actif_

  Gestionnaire du Cluster de basculement affiche maintenant disque hello en tant que DataKeeper disque, comme indiqué dans la Figure 55.

  ![Figure 55 : Le Gestionnaire du Cluster de basculement présente disque hello DataKeeper de réplication][sap-ha-guide-figure-3045]

  _**Figure 55 :** Gestionnaire du Cluster de basculement affiche les disques hello que DataKeeper répliquée_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Installer le système SAP NetWeaver de hello

Nous ne décrivons le programme d’installation de hello SGBD, car les configurations varient en fonction de hello système SGBD que vous utilisez. Toutefois, nous supposons que haute disponibilité avec hello SGBD tenant avec fonctionnalités hello prennent en charge de différents fournisseurs de SGBD hello pour Azure. par exemple Always On ou la mise en miroir de base de données pour SQL Server, et Oracle Data Guard pour bases de données Oracle. Dans le scénario de hello que nous utilisons dans cet article, nous n’avez pas ajouté plus protection toohello SGBD.

Il n’existe pas de considérations particulières lorsque différents services de SGBD interagissent avec ce type de configuration SAP ASCS/SCS en cluster dans Azure.

> [!NOTE]
> procédures d’installation Hello des systèmes de ABAP SAP NetWeaver, les systèmes de Java et les systèmes ABAP + Java sont presque identiques. différence la plus significative Hello est qu’une seule instance ASC sur un système SAP ABAP. Hello système Java de SAP a une seule instance SCS. Hello système SAP ABAP + Java a une seule instance ASC et une seule instance SCS en cours d’exécution hello même groupe de clusters de basculement de Microsoft. Toute différence d’installation pour chaque pile d’installation de SAP NetWeaver est mentionnée explicitement. Vous pouvez supposer que toutes les autres parties sont hello identiques.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Installer SAP avec une instance ASCS/SCS à haute disponibilité

> [!IMPORTANT]
> Veillez pas les tooplace du fichier de votre page sur DataKeeper des volumes en miroir. DataKeeper ne prend pas en charge les volumes mis en miroir. Vous pouvez laisser votre fichier d’échange sur le lecteur temporaire hello D d’une machine virtuelle Azure, qui est la valeur par défaut hello. S’il n’y ne figure pas déjà, déplacez hello Windows page fichier toodrive D: de votre machine virtuelle Azure.
>
>

L’installation de SAP avec une instance ASCS/SCS à haute disponibilité implique les tâches suivantes :

- Création d’un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster
- Lors de l’installation hello SAP premier nœud de cluster
- Modifier le profil SAP hello de l’instance ASCS/SCS hello
- Ajout d'un port de sondage
- Ouverture du port de sondage du pare-feu Windows hello

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Créer un nom d’hôte virtuel d’instance de SAP ASCS/SCS hello en cluster

1.  Dans le Gestionnaire DNS Windows hello, créez une entrée DNS pour le nom d’hôte virtuel hello de l’instance ASCS/SCS hello.

  > [!IMPORTANT]
  > Hello adresse IP que vous attribuez le nom d’hôte virtuel toohello Hello ASCS/SCS instance doit être hello même en tant qu’adresse IP de hello que vous avez affecté tooAzure équilibrage de charge (**<*SID*> - lb - ASC **).  
  >
  >

  Hello d’adresse IP du nom d’hôte hello virtuel SAP ASCS/SCS (**pr1 ASC sap**) est identique à hello en tant qu’adresse IP de hello d’équilibrage de charge Azure (**pr1-lb-ASC**).

  ![Figure 56 : Définir l’entrée DNS de hello pour le nom virtuel du cluster SAP ASCS/SCS hello et adresse TCP/IP][sap-ha-guide-figure-3046]

  _**Figure 56 :** définir l’entrée DNS de hello pour le nom virtuel du cluster SAP ASCS/SCS hello et adresse TCP/IP_

2.  toodefine hello IP adresse affectée toohello nom d’hôte virtuel, sélectionnez **Gestionnaire DNS** > **domaine**.

  ![Figure 57 : Nouveau nom virtuel et nouvelle adresse TCP/IP de la configuration du cluster SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Figure 57 :** Nouveau nom virtuel et nouvelle adresse TCP/IP de la configuration du cluster SAP ASCS/SCS_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Installer hello SAP premier nœud de cluster

1.  Exécuter l’option de nœud de cluster première hello sur le nœud de cluster A. Par exemple, sur hello **pr1-ascs-0** hôte.
2.  les ports par défaut tookeep hello pour hello Azure interne l’équilibrage de charge, sélectionnez :

  * **Système ABAP** : numéro d’instance **ASCS****00**
  * **Système Java** : numéro d’instance **SCS****01**
  * **Système ABAP+Java** : numéro d’instance **ASCS****00** et numéro d’instance **SCS****01**

  chiffres de toouse instance autre que 00 pour hello ABAP ASCS, instance et 01 pour l’instance de Java SCS hello, vous devez commencer toochange hello de charge interne Azure par défaut d’équilibrage de règles, décrites dans [charge par défaut de modification hello ASCS/SCS règles pour l’équilibrage de charge interne Azure hello d’équilibrage][sap-ha-guide-8.9].

Hello suivants certaines tâches ne sont pas décrits dans la documentation d’installation SAP standard hello.

> [!NOTE]
> Hello documentation d’installation SAP décrit comment tooinstall hello premier nœud de cluster ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modifier hello profil de SAP de l’instance ASCS/SCS hello

Vous devez tooadd un nouveau paramètre de profil. paramètre de profil Hello empêche des connexions entre les processus de travail SAP et le serveur de file d’attente hello de fermer lorsqu’elles sont inactives pendant trop longtemps. Nous l’avons mentionné problème du scénario hello dans [ajouter des entrées de Registre sur les deux nœuds de cluster de l’instance de SAP ASCS/SCS hello][sap-ha-guide-8.11]. Dans cette section, nous avons introduit également deux paramètres de connexion de TCP/IP base modifications toosome. Dans un deuxième temps, vous devez tooset hello enqueue server toosend un `keep_alive` signal afin que les connexions hello n’atteint le seuil d’inactivité de l’équilibrage de charge interne Azure hello.

hello toomodify profil SAP d’instance ASCS/SCS hello :

1.  Ajoutez cette toohello de paramètre de profil profil d’instance SAP ASCS/SCS :

  ```
  enque/encni/set_so_keepalive = true
  ```
  Dans notre exemple, le chemin d’accès de hello est :

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Par exemple, profil d’instance SAP SCS toohello et chemin d’accès correspondant :

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  modifications de hello tooapply, redémarrez l’instance de ASCS SAP /SCS de hello.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Ajouter un port de sondage

Utilisez le travail de configuration de l’équilibrage de charge interne hello sonde fonctionnalité toomake hello ensemble du cluster avec équilibrage de charge Azure. équilibrage de charge interne Azure Hello distribue généralement hello entrants la charge de travail entre les participants machines virtuelles. Toutefois, cela ne fonctionne pas dans certaines configurations de cluster, car une seule instance est active. Bonjour autre instance est passive et ne peut pas accepter des charges de travail hello. Une fonctionnalité de sonde est utile lors de la lui affecte équilibreur de charge interne Azure hello tooan uniquement les instances actives de travail. Avec la fonctionnalité de sonde hello, l’équilibreur de charge interne hello peut détecter les instances sont actifs et puis ciblent uniquement les instance hello avec une charge de travail hello.

tooadd un port de la sonde :

1.  Vérifiez hello actuel **ProbePort** définition en exécutant hello suivant de commande PowerShell. Exécuter à partir de dans une des machines virtuelles de hello dans la configuration de cluster hello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Définissez un port de sondage. numéro de port de sonde Hello par défaut est **0**. Dans notre exemple, nous utilisons le port de sondage **62000**.

  ![Figure 58 : port de la sonde hello cluster configuration par défaut est 0][sap-ha-guide-figure-3048]

  _**Figure 58 :** port de la sonde du cluster configuration de hello par défaut est 0_

  numéro de port Hello est défini dans les modèles SAP Azure Resource Manager. Vous pouvez affecter le numéro de port hello dans PowerShell.

  tooset une nouvelle valeur de ProbePort pour hello  **SAP <*SID*> IP ** ressource de cluster, exécutez hello suite du script PowerShell. Mettre à jour les variables PowerShell hello pour votre environnement. Après l’exécution du script de hello, vous serez invité à toorestart hello SAP groupe tooactivate hello les modifications de cluster.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Après avoir mis hello  **SAP <*SID*> ** rôle en ligne du cluster, vérifiez que **ProbePort** a la valeur toohello nouvelle valeur.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figure 59 : Port de la sonde hello cluster après avoir défini la nouvelle valeur de hello][sap-ha-guide-figure-3049]

  _**Figure 59 :** sonde de port de cluster hello après avoir défini la nouvelle valeur de hello_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Ouvrez le port de sondage du pare-feu Windows hello

Vous devez tooopen un port de sondage du pare-feu Windows sur les deux nœuds de cluster. Utilisez hello suivant script tooopen un port de sondage du pare-feu Windows. Mettre à jour les variables PowerShell hello pour votre environnement.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Hello **ProbePort** est défini trop**62000**. Maintenant vous pourrez accéder au partage de fichiers hello  **\\\ascsha-clsap\sapmnt** d’autres hôtes, notamment du **ascsha-DBA**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Installer l’instance de base de données hello

base de données tooinstall hello d’une instance, suivez hello est décrite dans la documentation d’installation SAP de hello.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Installer le second nœud de cluster hello

tooinstall hello deuxième cluster, suivez les étapes hello Bonjour guide d’installation SAP.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Modifier le type de démarrage hello d’instance de service SAP ERS Windows hello

Modifier le type de démarrage de hello Hello service SAP ERS Windows trop**automatique (début différé)** sur les deux nœuds de cluster.

![Figure 60 : Modifier le type de service hello pour hello SAP ERS instance toodelayed automatique][sap-ha-guide-figure-3050]

_**Figure 60 :** modifier le type de service hello pour hello SAP ERS instance toodelayed automatique_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Installer hello principal serveur d’applications SAP

Installer l’instance de serveur d’Application principal (PAS) hello <*SID*> - di - 0 sur l’ordinateur virtuel hello que vous avez désigné toohost hello PAS. Il n’existe aucune dépendance sur des paramètres spécifiques à Azure ou DataKeeper.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Installer hello serveur d’applications SAP supplémentaires

Installez une SAP supplémentaires Application serveur (agents) sur tous les ordinateurs virtuels de hello que vous avez désigné toohost une instance de serveur d’applications SAP. Par exemple, sur <*SID*> - di - 1 trop <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Cela termine installation hello d’un système SAP NetWeaver de haute disponibilité. Procédez maintenant à un test de basculement.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Tester une instance SAP ASCS/SCS hello ou la réplication SIOS
Il est facile tootest et surveiller une instance SAP ASCS/SCS ou réplication de disque SIOS en utilisant le Gestionnaire du Cluster de basculement et l’outil de Configuration et la gestion de DataKeeper de SIOS hello.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> L’instance SAP ASCS/SCS s’exécute sur le nœud de cluster A

Hello **SAP PR1** groupe du cluster est en cours d’exécution sur le nœud de cluster A. Par exemple, sur **pr1-ascs-0**. Affecter le lecteur de disque hello partagé S, qui fait partie de hello **SAP PR1** groupe du cluster, et l’instance ASCS/SCS hello utilise, toocluster nœud A.

![Figure 61 : Gestionnaire du Cluster de basculement : groupe de clusters SAP < SID > hello est en cours d’exécution sur le nœud de cluster A][sap-ha-guide-figure-5000]

_**Figure 61 :** Gestionnaire du Cluster de basculement : hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster A_

Dans hello SIOS DataKeeper gestion et l’outil de Configuration, vous pouvez voir ce disque partagé hello les données sont répliquées de façon synchrone à partir du lecteur de volume hello source S sur le nœud de cluster toohello lecteur cible de volume S sur le nœud de cluster B. Par exemple, elle est répliquée à partir de **pr1-ascs-0 [10.0.0.40]** trop**pr1-ascs-1 [de 10.0.0.41]**.

![Figure 62 : Dans SIOS DataKeeper, répliquer volume local de hello à partir du nœud de cluster nœud toocluster B][sap-ha-guide-figure-5001]

_**Figure 62 :** dans SIOS DataKeeper, répliquer le volume local de hello à partir du nœud de cluster nœud toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Basculement de nœud A toonode B

1.  Choisissez une de ces options tooinitiate un basculement de hello SAP <*SID*> groupe de clusters à partir du cluster A toocluster nœud b :
  - Utiliser le Gestionnaire du cluster de basculement  
  - Utiliser l’applet de commande PowerShell de cluster de basculement

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Redémarrez le nœud de cluster A hello Windows système d’exploitation invité (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).  
3.  Redémarrage d’un nœud de cluster à partir de hello portail Azure (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).  
4.  Redémarrage d’un nœud de cluster à l’aide de Azure PowerShell (cette commande lance un basculement automatique de hello SAP <*SID*> groupe de clusters à partir du nœud A toonode B).

  Après le basculement, hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster B. Par exemple, il est en cours d’exécution **pr1-ascs-1**.

  ![Figure 63 : Dans le Gestionnaire de Cluster de basculement, groupe de clusters SAP < SID > hello est en cours d’exécution sur le nœud de cluster B][sap-ha-guide-figure-5002]

  _**Figure 63**: basculement Gestionnaire du Cluster de hello SAP <*SID*> groupe de cluster est en cours d’exécution sur le nœud de cluster B_

  Hello disque partagé est maintenant monté sur un cluster de nœud B. SIOS DataKeeper réplique des données à partir du lecteur de volume source S sur le cluster le nœud B tootarget volume lecteur S sur le nœud de cluster A. Par exemple, il se réplique à partir de **pr1-ascs-1 [de 10.0.0.41]** trop**pr1-ascs-0 [10.0.0.40]**.

  ![Figure 64 : SIOS DataKeeper réplique le volume de local hello de cluster B toocluster nœud A][sap-ha-guide-figure-5003]

  _**Figure 64 :** SIOS DataKeeper réplique le volume de local hello du nœud de toocluster B de nœud de cluster A_
