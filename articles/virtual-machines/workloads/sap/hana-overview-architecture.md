---
title: aaaOverview et Architecture de HANA SAP sur Azure (Instances de grande taille) | Documents Microsoft
description: "Présentation de l’architecture tooDeploy HANA SAP sur Azure (Instances de grande taille)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure

## <a name="what-is-sap-hana-on-azure-large-instances"></a>Qu’est-ce que SAP HANA sur Azure (grandes instances) ?

SAP HANA sur Azure (Instance de grande taille) est une solution unique de tooAzure. En outre tooproviding des Machines virtuelles Azure à des fins de hello de déploiement et l’exécution de SAP HANA, Azure vous offre hello possibilité toorun et déployer SAP HANA sur les serveurs de système NU sont tooyou dédié comme un client. Hello SAP HANA sur la solution Azure (Instances de grande taille) s’appuie sur le serveur/hôte non partagé un matériel nu affecté tooyou en tant que client. matériel de serveur Hello est incorporé dans des tampons plus volumineux qui contiennent l’infrastructure de stockage, de réseau et de calcul/serveur. Cette combinaison est certifiée HANA TDI. offre de service Hello de HANA SAP sur Azure (Instances de grande taille) propose différentes références (SKU) de serveur différent ou tailles, en commençant par les unités comportant 72 unités centrales et 768 Go de mémoire toounits qui disposent de 960 processeurs et la mémoire de 20 To.

isolation du client Hello dans horodatage d’infrastructure hello est effectuée dans les clients, qui ressemble en détail :

- Mise en réseau : isolation des clients au sein de la pile d’infrastructure au travers de réseaux virtuels par locataire assigné à un client. Un client est attribué tooa un seul client. Un client peut avoir plusieurs locataires. isolement du réseau Hello de locataires interdit la communication réseau entre les clients au niveau de cachet d’infrastructure hello. Même si les clients appartiennent toohello même client.
- Les composants de stockage : Isolation via des machines virtuelles de stockage disposant de volumes de stockage affecté tooit. Les volumes de stockage peuvent être affectés à tooone stockage uniquement la machine virtuelle. Un ordinateur virtuel de stockage est affecté tooone exclusivement un seul locataire dans pile d’infrastructure certifiés SAP HANA TDI hello. Par conséquent des volumes de stockage affectés l’ordinateur virtuel de stockage tooa accessibles dans un spécifique et connexe client uniquement. Et ne sont pas visibles entre les clients de déploiement différents hello.
- Serveur ou hôte : unité de serveur ou hôte qui n’est pas partagée entre les clients ou les locataires. Un ordinateur hôte ou un serveur déployé tooa client, est une unité atomique complète calcul affecté tooone seul locataire. **Aucun** partitionnement matériel ou logiciel utilisé ne peut vous conduire, en tant que client, à partager un hôte ou un serveur avec un autre client. Volumes de stockage qui sont assignés toohello stockage virtual machine de client spécifique de hello sont monté toosuch un serveur. Un locataire peut avoir des unités de serveur de réduire une des différentes références SKU exclusivement affectée.
- Au sein d’une SAP HANA sur le marqueur d’infrastructure Azure (grande Instance), plusieurs clients différents sont déployés et isolés contre les uns des autres par des concepts de locataire hello sur le niveau de mise en réseau, stockage et de calcul. 


Ces unités de serveur de système NU sont pris en charge uniquement toorun SAP HANA. couche d’application SAP Hello ou intermédiaires de la charge de travail est en cours d’exécution dans des Machines virtuelles Microsoft Azure. marqueurs d’infrastructure Hello hello SAP HANA en cours d’exécution sur Azure (grande Instance) les unités sont connectés toohello Azure dorsales, par conséquent, que la connectivité à faible latence entre SAP HANA sur des unités de Azure (grande Instance) et les Machines virtuelles Azure est fournie.

Ce document est un des cinq documents, qui couvrent la rubrique hello de HANA SAP sur Azure (grande Instance). Dans ce document, nous accédez via l’architecture de base hello, les responsabilités, les services fournis et sur un niveau élevé via les fonctionnalités de la solution de hello. Pour la plupart des zones de hello, telles que la mise en réseau et de connectivité, hello autres quatre documents couvrent détails et détail. documentation Hello de HANA SAP sur Azure (grande Instance) ne couvre pas les aspects de l’installation de SAP NetWeaver ou déploiement de SAP NetWeaver dans les machines virtuelles Azure. Cette rubrique est couverte dans la documentation spécifique trouvée dans hello même conteneur de la documentation. 


Hello cinq parties de ce guide couvrent hello rubriques suivantes :

- [Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Infrastructure et connectivité à SAP HANA (grandes instances) sur Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Comment tooinstall et configurez SAP HANA (instances de grande taille) sur Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Guide pratique de résolution des problèmes et de surveillance de SAP HANA (grandes instances) sur Azure](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Définitions

Plusieurs définitions communes sont largement utilisées dans hello Architecture et le Guide de déploiement technique. Hello de note suivant les termes du contrat et leurs significations :

- **IaaS :** Infrastructure as a Service
- **PaaS :** Platform as a Service
- **SaaS :** Software as a Service
- **Composant SAP :** une application SAP individuelle telle que ECC, BW, Solution Manager ou EP. Les composants SAP peuvent être basés sur des technologies ABAP ou Java traditionnelles ou une application non basée sur NetWeaver telle que Business Objects.
- **Environnement SAP :** un ou plusieurs composants SAP regroupement logiquement tooperform une fonction d’entreprise, telles que le développement, Choisissons, formation, récupération d’urgence ou de Production.
- **Paysage SAP :** fait référence toohello des ressources SAP entières dans votre environnement informatique. Hello paysage SAP comprend tous les environnements de production et de non-production.
- **Système SAP :** hello combinaison de la couche SGBD et de la couche d’application d’un système de développement ERP SAP système de test SAP BW, système de production CRM SAP, etc.. Les déploiements Azure ne prennent pas en charge la séparation de ces deux couches entre les sites et Azure. Cela signifie qu’un système SAP doit être déployé en local ou dans Azure. Toutefois, vous pouvez déployer hello différents systèmes d’un paysage SAP dans Azure ou localement. Par exemple, vous pouvez déployer systèmes de développement et de test de CRM SAP dans Azure, hello lors du déploiement de hello CRM SAP production système local. SAP HANA sur Azure (Instances de grande taille), il est destiné héberger hello SAP de la couche application de systèmes SAP dans des machines virtuelles Azure et de hello relatives aux instances SAP HANA sur une unité dans le cachet d’Instance est importante HANA hello.
- **Cachet d’Instance volumineux :** une pile d’infrastructure matérielle SAP HANA TDI certifié et dédié toorun des instances de SAP HANA dans Azure.
- **SAP HANA sur Azure (Instances de grande taille) :** nom officiel de l’offre de hello dans Azure toorun HANA instances sur l’interface TDI SAP HANA certifié matériel déployé dans les tampons de grande Instance dans différentes régions Azure. Hello liées terme **HANA grande Instance** est l’abréviation de HANA SAP sur Azure (Instances de grande taille) et est largement utilisé ce guide de déploiement technique.
- **Intersite :** décrit un scénario dans lequel les machines virtuelles sont déployée tooan abonnement Azure qui utilise le site à site, plusieurs sites ou ExpressRoute la connectivité entre les centres de local hello et Azure. Dans la documentation Azure courante, ces types de déploiements sont également décrits comme des scénarios intersites. Hello connexion de hello fait tooextend domaines locaux Active Directory/OpenLDAP locale et DNS sur site dans Azure. Hello local paysage est étendue toohello des ressources Azure Hello un ou plusieurs abonnements Azure. Avoir cette extension, hello machines virtuelles peut être la partie du domaine local de hello. Les utilisateurs du domaine local de hello peuvent accéder aux serveurs de hello et exécuter des services sur ces machines virtuelles (comme les services SGBD). La communication et la résolution de noms entre les machines virtuelles déployées en local et les machines virtuelles déployées dans Azure sont possibles. Tel est le scénario de type hello dans SAP la plupart des ressources sont déployées. Consultez les guides de hello de [planification et conception pour la passerelle VPN](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) et [créer un réseau virtuel avec une connexion de Site à Site à l’aide de hello portail Azure](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations.
- **Locataire :** un client déployé dans le tampon de grande instance HANA est isolé dans un « locataire ». Un locataire est isolé dans hello mise en réseau, stockage et couche de calcul à partir d’autres clients. Par conséquent, cette unités de stockage et de calcul toohello attribué de plusieurs clients ne peuvent pas voir ou communiquent entre eux sur hello HANA grande Instance cachet de niveau. Un client peut choisir toohave des déploiements à plusieurs clients. Même alors, il n’existe aucune communication entre les clients sur hello au niveau du marqueur HANA grande Instance.

Il existe de nombreuses ressources supplémentaires qui ont été publiés dans la rubrique hello du déploiement de la charge de travail SAP sur le cloud public Microsoft Azure. Il est fortement recommandé que toute personne planification et l’exécution d’un déploiement de SAP HANA dans Azure est expérimenté et prenant en charge des principaux de hello de Azure IaaS et déploiement hello des charges de travail SAP sur Azure IaaS. Hello ressources suivantes fournissent des informations supplémentaires et doivent être référencées avant de continuer :


- [Utilisation de solutions SAP sur des machines virtuelles Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Certification

Outre hello NetWeaver certification, SAP requiert un certificat spécial pour SAP HANA toosupport SAP HANA sur certaines infrastructures, telles que Azure IaaS.

Hello core la Note SAP NetWeaver, et du degré de tooa certification de SAP HANA, est [# Note SAP 1928533 – Applications SAP sur Azure : les types pris en charge des produits et de la machine virtuelle Azure](https://launchpad.support.sap.com/#/notes/1928533).

La Note SAP [SAP Note #2316233 - SAP HANA on Microsoft Azure (Large Instances) (Note SAP n° 2316233 - SAP HANA sur Microsoft Azure (grandes instances))](https://launchpad.support.sap.com/#/notes/2316233/E) est également importante. Elle couvre la solution hello décrite dans ce guide. En outre, vous êtes toorun pris en charge SAP HANA dans le type de machine virtuelle de GS5 hello de Azure. [Pour plus d’informations pour ce cas sont publiés sur le site Web SAP hello](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hello SAP HANA sur la solution Azure (Instances de grande taille) visés tooin SAP Remarque #2316233 fournit à Microsoft et les clients SAP hello capacité toodeploy grand SAP Business Suite, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA ou autres charges de travail SAP HANA dans Azure. solution de Hello est basée sur hello SAP-HANA certifié cachet de matériel dédié ([SAP HANA adaptés Datacenter intégration – TDI](https://scn.sap.com/docs/DOC-63140)). En cours d’exécution comme une interface TDI HANA SAP solution configurée vous offre confiance hello de savoir que toutes les applications SAP HANA (y compris SAP Business Suite sur SAP HANA, SAP Business Warehouse (BW) sur SAP HANA, S4/HANA et BW4/HANA) allez toowork sur hello infrastructure de matériel.

Comparés toorunning SAP HANA dans Azure Virtual Machines cette solution présente un avantage : il permet de beaucoup plus grands volumes de mémoire. Si vous souhaitez que cette solution tooenable, il existe quelques aspects clés de toounderstand :

- couche d’application Hello SAP et les applications non-SAP s’exécutent dans Azure Machines virtuelles (VM qui sont hébergés dans les tampons de matériel Azure habituel hello).
- Client infrastructure locale, les centres de données, et les déploiements d’applications sont connectés toohello plateforme de cloud Microsoft Azure via ExpressRoute Azure (recommandé) ou de réseau privé virtuel (VPN, Virtual Private Network). Le répertoire Active Directory (AD) et le DNS sont également étendus dans Azure.
- instance de base de données SAP HANA Hello pour les charges de travail HANA s’exécute sur SAP HANA sur Azure (Instances de grande taille). tampon de grande Instance Hello est connecté dans la mise en réseau Azure, pour les logiciels exécutés dans des machines virtuelles Azure peuvent interagir avec instance HANA de hello en cours d’exécution dans les Instances de grande taille HANA.
- Le matériel de SAP HANA sur Azure (grandes instances) est un matériel dédié fourni dans une Infrastructure as a Service (IaaS) avec SUSE Linux Enterprise Server ou Red Hat Enterprise Linux préinstallé. Comme avec des Machines virtuelles Azure, plus les mises à jour et système d’exploitation de toohello maintenance est de votre responsabilité.
- Installation de HANA ou n’importe quel toorun nécessaires des composants supplémentaires SAP HANA sur des unités d’instances HANA volumineux est votre responsabilité, ainsi que respectifs de toutes les opérations en cours et les administrations de HANA SAP sur Azure.
- En outre les solutions toohello décrites ici, vous pouvez installer les autres composants dans votre abonnement Azure qui se connecte tooSAP HANA sur Azure (Instances de grande taille).  Par exemple, les composants qui permettent la communication avec et/ou directement de base de données SAP HANA toohello (serveurs saut, RDP SAP HANA Studio, les Services de données SAP pour des scénarios SAP BI, ou des solutions d’analyse de réseau).
- Comme dans Azure, les grandes instances HANA prennent en charge des fonctionnalités de haute disponibilité et de récupération d’urgence.

## <a name="architecture"></a>Architecture

À un niveau élevé, hello SAP HANA sur la solution Azure (Instances de grande taille) a couche d’application SAP hello résidant dans la couche de base de données des machines virtuelles Azure et hello résidant sur un matériel TDI SAP configuré situé dans un tampon d’Instance est importante dans hello même région Azure qui est connecté tooAzure IaaS.

> [!NOTE]
> Vous avez besoin de couche d’application SAP toodeploy hello Bonjour même région Azure en tant que couche SGBD SAP de hello. Cette règle est bien documentée dans les informations publiées sur la charge de travail SAP sur Azure. 

Hello architecture globale de HANA SAP sur Azure (Instances de grande taille) fournit une configuration d’un matériel certifié SAP TDI (non virtualisé, bare metal, serveur hautes performances pour la base de données SAP HANA hello) et la possibilité de hello et la flexibilité de Azure tooscale ressources pour hello SAP toomeet de couche application à vos besoins.

![Présentation de l’architecture de SAP HANA sur Azure (grandes instances)](./media/hana-overview-architecture/image1-architecture.png)

architecture Hello indiqué est divisé en trois sections :

- **À droite :** une infrastructure locale exécutant différentes applications dans des centres de données avec les utilisateurs finaux accédant aux applications métier (telles que SAP). Dans l’idéal, cela local infrastructure est ensuite connectée tooAzure avec Azure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Center :** affiche Azure IaaS et, dans ce cas, utilisez des machines virtuelles Azure toohost SAP ou d’autres applications qui utilisent SAP HANA comme un système SGBD. Instances HANA plus petites qui fournissent de fonction avec une mémoire hello machines virtuelles Azure sont déployés dans des machines virtuelles Azure ainsi que leur couche application. En savoir plus sur les [machines virtuelles](https://azure.microsoft.com/services/virtual-machines/).
<br />Mise en réseau Azure est utilisé toogroup des systèmes SAP ainsi que d’autres applications dans des réseaux virtuels Azure (réseaux virtuels). Ces réseaux virtuels vous connecter à des systèmes de site tooon ainsi que les tooSAP HANA sur Azure (Instances de grande taille).
<br />Pour les applications SAP NetWeaver et les bases de données qui sont prises en charge toorun dans Microsoft Azure, consultez [prise en charge Note SAP #1928533 – Applications SAP sur Azure : les types pris en charge des produits et de la machine virtuelle Azure](https://launchpad.support.sap.com/#/notes/1928533). Pour la documentation sur le déploiement des solutions SAP sur Azure, veuillez consulter :

  -  [Utilisation de SAP sur des machines virtuelles Windows](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Utilisation de solutions SAP sur des machines virtuelles Microsoft Azure](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Left :** affiche hello SAP HANA TDI est certifié matériel dans le tampon d’Instance de grande taille de Azure hello. unités d’Instance est importante HANA Hello sont connecté toohello des réseaux virtuels Azure de votre abonnement à l’aide de la même technologie que la connectivité hello de local à Azure de hello.

cachet d’Instance volumineux Azure Hello lui-même combine hello suivant des composants :

- **Calcul :** serveurs qui sont basés sur les processeurs Intel Xeon E7-8890v3 ou Intel Xeon E7-8890v4 qui fournissent la capacité de calcul nécessaires hello et SAP HANA certifié.
- **Réseau :** A unifiée de l’infrastructure réseau haut débit qui interconnexions hello calcul, stockage et les composants de réseau local.
- **Stockage :** une infrastructure de stockage qui est accessible via une structure réseau unifiée. Capacité de stockage spécifique est fourni en fonction de hello spécifiques SAP HANA sur la configuration de Azure (Instances de grande taille) en cours de déploiement (la capacité de stockage est disponible pour un coût mensuel supplémentaire).

Au sein de l’infrastructure d’architecture mutualisée hello de marqueur de grande Instance hello, les clients sont déployés en tant que clients isolés. Au moment du déploiement du client de hello, vous devez tooname un abonnement Azure au sein de votre inscription Azure. Cette hello toobe du cours abonnement Azure, hello HANA volumineux ou des instances va toobe facturée sur. Ces clients ont un abonnement Azure de toohello relation 1:1. Réseau judicieux, qu'il est possible tooaccess une unité d’Instance volumineuse HANA déployé dans un locataire dans une région Azure à partir de réseaux virtuels Azure différents, qui appartiennent toodifferent abonnements Azure. Bien que ces abonnements Azure doivent toobelong toohello même inscription Azure. 

Comme avec les machines virtuelles Azure, SAP HANA sur Azure (grandes instances) est proposé dans plusieurs régions Azure. Dans les fonctionnalités de récupération d’urgence toooffer ordre, vous pouvez choisir tooopt dans. Différents horodatages d’Instance est importante dans une région géographique-politique sont connecté tooeach autres. Par exemple, HANA grande Instance marqueurs dans la région ouest et États-Unis sont connectés via une liaison de réseau dédiée à des fins de hello de réplication de la récupération d’urgence. 

Tout comme vous avez le choix entre différents types de machines virtuelles avec Azure Virtual Machines, vous pouvez choisir parmi différentes références de grandes instances HANA qui sont adaptées aux divers types de charges de travail de SAP HANA. SAP s’applique le taux de socket tooprocessor de mémoire pour les charges de travail variables basées sur des générations de processeur Intel hello, il existe quatre différents types de référence (SKU) proposées :

À compter de juillet 2017, HANA SAP sur Azure (Instances de grande taille) est disponible dans plusieurs configurations dans hello Azure zones de région ouest des États-Unis, est de l’Australie, Sud-est de l’Australie, Europe de l’ouest et Europe du Nord :

| Solution SAP | UC | Mémoire | Storage | Disponibilité |
| --- | --- | --- | --- | --- |
| Optimisée pour OLAP : SAP BW, BW/4HANA<br /> ou SAP HANA pour les charges de travail OLAP génériques | SAP HANA sur Azure S72<br /> - 2 x processeurs Intel® Xeon® E7-8890 v3<br /> 36 cœurs et 72 threads d’UC |  768 Go |  3 To | Disponible |
| --- | SAP HANA sur Azure S144<br /> - 4 x processeurs Intel® Xeon® E7-8890 v3<br /> 72 cœurs et 144 threads d’UC |  1,5 To |  6 To | Plus proposé |
| --- | SAP HANA sur Azure S192<br /> - 4 x processeurs Intel® Xeon® E7-8890 v4<br /> 96 cœurs et 192 threads d’UC |  2 TO |  8 To | Disponible |
| --- | SAP HANA sur Azure S384<br /> - 8 x processeurs Intel® Xeon® E7-8890 v4<br /> 192 cœurs et 384 threads d’UC |  4 TO |  16 TO | TooOrder prêt |
| Optimisée pour OLTP : SAP Business Suite<br /> sur SAP HANA ou S/4HANA (OLTP),<br /> OLTP générique | SAP HANA sur Azure S72m<br /> - 2 x processeurs Intel® Xeon® E7-8890 v3<br /> 36 cœurs et 72 threads d’UC |  1,5 To |  6 To | Disponible |
|---| SAP HANA sur Azure S144m<br /> - 4 x processeurs Intel® Xeon® E7-8890 v3<br /> 72 cœurs et 144 threads d’UC |  3 TO |  12 To | Plus proposé |
|---| SAP HANA sur Azure S192m<br /> - 4 x processeurs Intel® Xeon® E7-8890 v4<br /> 96 cœurs et 192 threads d’UC  |  4 TO |  16 TO | Disponible |
|---| SAP HANA sur Azure S384m<br /> - 8 x processeurs Intel® Xeon® E7-8890 v4<br /> 192 cœurs et 384 threads d’UC |  6,0 To |  18 To | TooOrder prêt |
|---| SAP HANA sur Azure S384xm<br /> - 8 x processeurs Intel® Xeon® E7-8890 v4<br /> 192 cœurs et 384 threads d’UC |  8,0 To |  22 To |  TooOrder prêt |
|---| SAP HANA sur Azure S576<br /> - 12 x processeurs Intel® Xeon® E7-8890 v4<br /> 288 cœurs et 576 threads d’UC |  12,0 To |  28 To | TooOrder prêt |
|---| SAP HANA sur Azure S768<br /> - 16 x processeurs Intel® Xeon® E7-8890 v4<br /> 384 cœurs et 768 threads d’UC |  16,0 To |  36 To | TooOrder prêt |
|---| SAP HANA sur Azure S960<br /> - 20 x processeurs Intel® Xeon® E7-8890 v4<br /> 480 cœurs et 960 threads d’UC |  20,0 To |  46 To | TooOrder prêt |

- Cœurs de processeur = somme de cœurs de processeur non-hyper-threaded de somme hello de processeurs hello d’unité de serveur hello.
- Threads d’UC = somme de threads de calcul fournies par les cœurs de processeur multithread de somme hello de processeurs hello d’unité de serveur hello. Toutes les unités sont configurées par toouse par défaut Hyper-Threading.


différentes configurations ci-dessus qui sont disponibles ou « ne sont proposées plus » Hello sont référencées dans [SAP Support Remarque #2316233 – HANA SAP sur Microsoft Azure (Instances de grande taille)](https://launchpad.support.sap.com/#/notes/2316233/E). les configurations de Hello, qui sont marquées comme « Prêt tooOrder » trouvera dès leur entrée en hello la Note SAP. Cependant, ces références (SKU) de l’instance peut être triée déjà pour hello six différentes régions Azure hello service de l’Instance de grande taille HANA est disponible.

des configurations spécifiques Hello choisies dépendent de la charge de travail, les ressources de processeur et mémoire souhaitée. Il est possible pour hello tooleverage de charge de travail OLTP références (SKU) qui sont optimisés pour les charges de travail OLAP. 

matériel Hello base pour toutes les offres de hello sont certifiés interface TDI SAP HANA. Toutefois, nous faisons une distinction entre les deux différentes classes de matériel, ce qui divise le SKU hello dans :

- S72, S72m, S144, S144m, S192 et S192m, ce qui constitue tooas hello 'I classe de Type' de références (SKU).
- S384, S384m, S384xm, S576, S768 et S960, ce qui constitue tooas hello 'Classe de Type II' des références SKU.

Il est important toonote qui a un horodatage HANA grande Instance complète n’est pas alloué exclusivement pour un seul client &#39; s utiliser. Cela s’applique racks toohello des ressources de calcul et de stockage à l’aide d’une infrastructure réseau déployée dans Azure. Les Instances de grande taille HANA infrastructure, comme Azure, déploie autre client &quot;locataires&quot; qui sont isolés les uns des autres Bonjour suivant trois niveaux :

- Réseau : Isolation via des réseaux virtuels au sein de l’horodatage d’Instance est importante HANA hello.
- Stockage : isolation par le biais de machines virtuelles auxquelles des volumes de stockage sont assignés et qui isolent les volumes de stockage entre les locataires.
- COMPUTE : Attribution dédiée de serveur unités tooa un seul locataire. Aucun partitionnement matériel ou logiciel des unités de serveur. Aucun partage d’une unité de serveur ou hôte unique entre les locataires. 

Par conséquent, les déploiements hello d’unités des Instances de grande taille HANA entre les différents clients ne sont pas visible tooeach autres. Ni peut HANA grandes unités Instance déployée dans différents, les clients communiquent directement au niveau de marqueur HANA grande Instance hello. Seules HANA grande Instance unités au sein d’un client peut communiquer tooeach autre sur hello au niveau du marqueur HANA grande Instance.
Un client déployé dans le tampon de grande Instance hello est assigné tooone judicieux facturation abonnement Azure. Toutefois, wise réseau sont accessibles à partir d’autres abonnements Azure dans des réseaux virtuels Azure hello même inscription Azure. Si vous déployez un autre abonnement Azure Bonjour même région Azure, vous pouvez également choisir tooask pour un locataire HANA grande Instance séparé.

Il existe des différences importantes entre l’exécution de SAP HANA sur les grandes instances HANA et l’exécution de SAP HANA sur les machines virtuelles Azure déployées dans Azure :

- Il n’existe aucune couche Virtualisation pour SAP HANA sur Azure (grandes instances). Vous obtenez des performances hello du matériel sans système d’exploitation sous-jacent de hello.
- Contrairement à Azure, hello SAP HANA sur le serveur Azure (Instances de grande taille) est un client spécifique tooa dédié. Il est impossible qu’une unité de serveur ou hôte fasse l’objet d’un partitionnement matériel ou logiciel. Par conséquent, une unité HANA grande Instance est utilisée en tant qu’attribuée en tant qu’un client tooa ensemble et avec ce tooyou en tant que client. Un redémarrage ou un arrêt du serveur de hello n’entraîne pas automatiquement système d’exploitation de toohello et SAP HANA en cours de déploiement sur un autre serveur. (Pour le Type I classe références (SKU), hello seule exception est si un serveur peut rencontrer des problèmes et redéploiement doit toobe effectuée sur un autre serveur.)
- Contrairement à Azure, où les types de processeur hôte sont sélectionnés pour le ratio prix/performances meilleures de hello, types de processeurs hello choisis pour SAP HANA sur Azure (Instances de grande taille) sont hello plus performants et de ligne de processeur Intel E7v3 et E7v4 hello.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Exécution de plusieurs instances SAP HANA sur une unité de grande instance HANA
Il est possible toohost, et plusieurs instances SAP HANA active sur les unités d’Instance est importante HANA hello. Dans l’ordre toostill offrent des fonctionnalités de hello d’instantanés de stockage, et la récupération d’urgence, une telle configuration requiert un volume défini par instance. À partir de maintenant, les unités d’Instance est importante HANA hello peuvent être subdivisées comme suit :

- S72, S72m, S144, S192 : Par incréments de 256 Go par hello 256 Go plus petit démarrage unité. Différents incréments, 256 Go, 512 Go et ainsi de suite, peuvent comporter toohello combiné de mémoire hello d’unité de hello.
- S144m et S192m : par incréments de 256 Go avec la plus petite unité de 512 Go hello. Différents incréments, 512 Go, 768 Go et ainsi de suite, peuvent comporter toohello combiné de mémoire hello d’unité de hello.
- Type de classe II : par incréments de 512 Go par hello plus petite unité de 2 To de démarrage. Différents incréments, 512 Go, 1 To, 1,5 To et ainsi de suite, peuvent comporter toohello combiné de mémoire hello d’unité de hello.

Voici quelques exemples de ce à quoi pourrait ressembler l’exécution de plusieurs instances SAP HANA :

| SKU | Taille de la mémoire | Taille de stockage | Tailles avec plusieurs bases de données |
| --- | --- | --- | --- |
| S72 | 768 Go | 3 To | 1 x instance HANA de 768 Go<br /> ou 1 x instance de 512 Go + 1 x instance de 256 Go<br /> ou 3 x instances de 256 Go | 
| S72m | 768 Go | 3 To | 3 x instances HANA de 512 Go<br />ou 1 x instance de 512 Go + 1 x instance de 1 To<br />ou 6 x instances de 256 Go<br />ou 1 x instance de 1,5 To | 
| S192m | 4 To | 16 TO | 8 x instances de 512 Go<br />ou 4 x instances de 1 To<br />ou 4 x instances de 512 Go + 2 x instances de 1 To<br />ou 4 x instances de 768 Go + 2 x instances de 512 Go<br />ou 1 x instance de 4 To |
| S384xm | 8 To | 22 To | 4 x instances de 2 To<br />ou 2 x instances de 4 To<br />ou 2 x instances de 3 To + 1 x instance de 2 To<br />ou 2 x instances de 2,5 To + 1 x instance de 3 To<br />ou 1 x instance de 8 To |


Vous obtenez idée de hello. Il existe certainement d’autres variantes. 


## <a name="operations-model-and-responsibilities"></a>Responsabilités et modèle opérationnel

service Hello fourni avec SAP HANA sur Azure (Instances de grande taille) est alignée avec les services Azure IaaS. Vous bénéficiez d’une instance de type grandes instances HANA avec un système d’exploitation installé qui est optimisé pour SAP HANA. Comme avec les machines virtuelles Azure IaaS, la plupart des tâches hello de renforcement hello du système d’exploitation, l’installation des logiciels supplémentaires, vous devez installer HANA, fonctionnement hello HANA et système d’exploitation et la mise à jour hello HANA et système d’exploitation est de votre responsabilité. Microsoft ne vous impose pas les mises à jour du SE, ni de HANA.

![Responsabilités relatives à SAP HANA sur Azure (grandes instances)](./media/hana-overview-architecture/image2-responsibilities.png)

Comme vous pouvez le voir dans le diagramme hello ci-dessus, HANA SAP sur Azure (Instances de grande taille) est une architecture mutualisée Infrastructure en tant qu’une offre de Service. Et, par conséquent, division hello de responsabilité appartient à la limite de système d’exploitation-Infrastructure hello, pourquoi la plupart des. Microsoft est responsable de tous les aspects du service hello ci-dessous ligne hello du système d’exploitation de hello et vous êtes responsable au-dessus de la ligne hello, y compris le système d’exploitation de hello. Méthodes les plus récentes sur site que peuvent reposer pour la conformité, la sécurité, la gestion des applications, base et la gestion du système d’exploitation peuvent donc continuer à toobe utilisé. les systèmes Hello apparaissent comme si elles figurent dans votre réseau à tous les égards.

Toutefois, ce service est optimisé pour SAP HANA, donc de zones où vous et Microsoft doivent les capacités de l’infrastructure sous-jacente toowork toouse ensemble hello pour de meilleurs résultats.

Hello suivant liste fournit plus de détails sur chacune des couches de hello et vos responsabilités :

**Mise en réseau :** tous hello réseaux internes pour le tampon de grande Instance hello SAP HANA, son stockage toohello accès, la connectivité entre les instances hello (pour la montée en puissance parallèle et d’autres fonctions), paysage toohello de connectivité et de connectivité en cours d’exécution tooAzure où la couche d’application SAP hello est hébergé dans Azure Virtual Machines. Il inclut également la connectivité WAN entre les centres de données Azure pour la réplication à des fins de récupération d’urgence. Tous les réseaux sont partitionnées par le client hello et QOS appliqué.

**Stockage :** hello virtualisés partitionnée de stockage pour tous les volumes requis par les serveurs de SAP HANA hello, ainsi que pour les instantanés. 

**Serveurs :** hello dédié de serveurs physiques toorun hello affecté tootenants les bases de données SAP HANA. Hello serveurs Hello Type I classe des références SKU sont abstrait de matériel. Avec ces types de serveurs, la configuration du serveur hello est collectée et conservée dans les profils, peuvent être déplacés d’un matériel physique tooanother de matériel physique. Ce (manuel) déplacement d’un profil par les opérations peut être comparé un peu tooAzure Service de réparation. serveurs Hello Hello SKU de classe de Type II n’offre pas une fonction de ce type.

**SDDC :** centres de logiciel de gestion hello qui sont des données toomanage utilisés en tant qu’entités logicielles défini. Il permet à Microsoft, ressources toopool pour des raisons de performances, la disponibilité et la mise à l’échelle.

**Système d’exploitation :** hello du système d’exploitation que vous choisissez (SUSE Linux ou Red Hat Linux) qui s’exécute sur les serveurs hello. images du système d’exploitation de Hello que vous sont fournies sont des images de hello fournies par hello tooMicrosoft du fournisseur Linux individuel à des fins de hello de SAP HANA en cours d’exécution. Vous êtes toohave requis un abonnement avec le fournisseur de Linux hello pour l’image optimisée de SAP HANA spécifique de hello. Vos responsabilités incluent l’enregistrement auprès du fournisseur de système d’exploitation hello hello. À partir du point de hello de remise par Microsoft, vous êtes responsable de toutes les autres mise à jour corrective du système d’exploitation de Linux hello. Cette mise à jour corrective également inclut les packages supplémentaires qui peuvent être nécessaires pour une installation réussie de SAP HANA (consultez la documentation d’installation HANA de tooSAP et les Notes SAP) et qui n’ont pas été inclus par hello Linux fournisseur spécifique dans leurs SAP HANA images du système d’exploitation optimisés. responsabilité Hello du client de hello inclut également la mise à jour corrective de hello du système d’exploitation qui est associée toomalfunction/optimisation de hello du système d’exploitation et de son matériel de serveur spécifique de pilotes toohello connexes. Toute sécurité ou la mise à jour corrective fonctionnelle de hello du système d’exploitation. Le client est également responsable de la surveillance et de la planification de capacité des éléments suivants :

- Consommation des ressources d’UC
- Consommation de mémoire
- L’espace disque des volumes toofree connexes, e/s et latence
- Trafic en volume du réseau entre la grande instance HANA et la couche Application SAP

infrastructure sous-jacente de Hello des Instances de grande taille HANA fournit des fonctionnalités de sauvegarde et restauration du volume du système d’exploitation hello. L’utilisation de cette fonctionnalité relève également de votre responsabilité.

**Intergiciel (middleware) :** hello SAP HANA Instance, principalement. L’administration, les opérations et la surveillance relèvent de votre responsabilité. Fonctionnalité est fournie qui vous permet de toouse des instantanés de stockage à des fins de récupération d’urgence et de la sauvegarde/restauration. Ces fonctionnalités sont fournies par l’infrastructure de hello. Toutefois, vos responsabilités incluent également la conception d’une architecture haute disponibilité ou de récupération d’urgence avec ces fonctionnalités, leur utilisation et la surveillance de la bonne exécution des captures instantanées de stockage.

**Données :** vos données gérées par SAP HANA et d’autres données telles que les fichiers de sauvegarde situés sur des volumes ou des partages de fichiers. Vos responsabilités incluent l’analyse espace libre du disque et la gestion du contenu hello sur des volumes hello et analyse hello réussite de l’exécution de sauvegardes de volumes de disque et les instantanés de stockage. Toutefois, l’exécution réussie de données de la réplication tooDR sites incombe hello de Microsoft.

**Applications :** hello des instances de l’application SAP ou, en cas d’applications non-SAP, couche d’application hello de ces applications. Vos responsabilités incluent le déploiement, d’administration, les opérations et analyse de ces applications liées toocapacity planification de la consommation des ressources du processeur, la consommation de mémoire, la consommation de stockage Azure et la consommation de bande passante réseau dans Les réseaux virtuels Azure et à partir de réseaux virtuels Azure tooSAP HANA sur Azure (Instances de grande taille).

**WAN :** hello connexions que vous établissez des déploiements de tooAzure local pour les charges de travail. Tous nos clients disposant de grandes instances HANA utilisent Azure ExpressRoute pour la connectivité. Cette connexion ne fait pas partie de hello SAP HANA sur la solution de Azure (Instances de grande taille), donc vous êtes responsable de programme d’installation Bonjour de cette connexion.

**Archive :** vous préférerez peut-être tooarchive des copies de données à l’aide de vos propres méthodes dans les comptes de stockage. L’archivage inclut de la gestion, de la conformité, des coûts et des opérations. Vous êtes chargé de générer des copies de l’archive et des sauvegardes sur Azure et de les stocker d’une manière conforme.

Consultez hello [SLA de HANA SAP sur Azure (Instances de grande taille)](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Dimensionnement

Le dimensionnement des grandes instances HANA n’est pas différent du dimensionnement HANA en général. Existantes et déployé des systèmes, que vous souhaitez toomove à partir d’autres tooHANA SGBDR, SAP fournit des rapports qui s’exécutent sur vos systèmes SAP existants. Si la base de données hello est déplacé tooHANA, ces rapports vérifier les données de hello et calculer les besoins en mémoire pour l’instance HANA hello. Lire hello suivant Notes SAP tooget plus d’informations sur comment toorun ces rapports et comment tooobtain leurs correctifs/versions les plus récentes :

- [Note de support SAP #1793345 - Sizing for SAP Suite on HANA](https://launchpad.support.sap.com/#/notes/1793345) (Dimensionnement de SAP Suite sur HANA)
- [Note de support SAP #1872170 - Suite on HANA and S/4 HANA sizing report](https://launchpad.support.sap.com/#/notes/1872170) (Rapport de dimensionnement de Suite sur HANA et S/4 HANA)
- [Note de support SAP #2121330 - FAQ: SAP BW on HANA Sizing Report](https://launchpad.support.sap.com/#/notes/2121330) (FAQ : Rapport de dimensionnement SAP BW sur HANA)
- [Note de support SAP #1736976 - Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/1736976) (Rapport de dimensionnement de BW sur HANA)
- [Note de support SAP #2296290 - New Sizing Report for BW on HANA](https://launchpad.support.sap.com/#/notes/2296290) (Nouveau rapport de dimensionnement pour BW sur HANA)

Pour les implémentations de champ vert, redimensionnement rapide de SAP est besoins en mémoire toocalculate disponibles de mise en œuvre hello du logiciel SAP par-dessus HANA.

Augmentez la mémoire requise pour HANA comme volume de données augmente, afin que vous souhaitez toobe prenant en charge de la consommation de mémoire hello maintenant et être en mesure de toopredict qu’il est toobe continu dans hello futures. Selon les besoins en mémoire hello, vous pouvez ensuite mapper votre demande dans une des hello HANA grande Instance SKU.

## <a name="requirements"></a>Configuration requise

Cette liste indique la configuration requise pour l’exécution de SAP HANA sur Azure (plus grandes instances).

**Microsoft Azure :**

- Un abonnement Azure qui peut être liée tooSAP HANA sur Azure (Instances de grande taille).
- Contrat de Support Premier Microsoft. Consultez [SAP Support Remarque #2015553 – SAP sur Microsoft Azure : conditions préalables de prise en charge](https://launchpad.support.sap.com/#/notes/2015553) pour des informations spécifiques relatives toorunning SAP dans Azure. À l’aide d’unités de grande instance HANA avec 384 et plus de processeurs, vous devez également tooextend hello tooinclude de contrat Premier Support réponse rapide d’Azure (ARR).
- Connaissance des instances de grande taille HANA hello références (SKU) vous avez besoin après avoir effectué un redimensionnement exercice avec SAP.

**Connectivité réseau :**

- Azure ExpressRoute entre local tooAzure : tooconnect votre tooAzure de centre de données local, tooorder que de créer au moins une connexion de Gbits/s de 1 à partir de votre fournisseur de services Internet. 

**Système d’exploitation :**

- Licences pour SUSE Linux Enterprise Server 12 pour les applications SAP.

> [!NOTE] 
> Hello système d’exploitation livré par Microsoft n’est pas inscrit avec SUSE, ni si elle est connectée avec une instance SMT.

- L’outil de gestion des abonnements SUSE Linux déployé dans Azure sur une machine virtuelle Azure. Cela permet hello pour SAP HANA sur Azure (Instances de grande taille) toobe inscrit et respectivement mis à jour par SUSE (il n’existe aucun accès internet au sein du centre de données d’Instances de grande taille HANA). 
- Licences pour Red Hat Enterprise Linux 6.7 ou 7.2 pour SAP HANA.

> [!NOTE]
> Hello système d’exploitation livré par Microsoft n’est pas inscrit avec Red Hat, et n’est pas informatique connecté tooa Red Hat abonnement Manager Instance.

- Gestionnaire d’abonnements Red Hat déployé dans Azure sur une machine virtuelle Azure. Hello Red Hat abonnement gestionnaire permet hello pour SAP HANA sur Azure (Instances de grande taille) toobe inscrit et respectivement mis à jour par Red Hat (il n’existe aucun accès direct à internet à partir d’au sein de client hello déployé sur le marqueur d’Instance est importante Azure hello).
- SAP requiert toohave prise en charge un contrat avec votre fournisseur de Linux. Cette exigence n’est pas effacée par solution hello d’Instances de grande taille HANA ou hello fait que votre exécution Linux dans Azure. Contrairement à certaines images de la galerie Azure hello Linux, hello service frais n'est pas inclus dans offre hello des Instances de grande taille HANA. Il est de vous un toofulfill hello spécifications du client de SAP concernant les contrats de prise en charge avec le serveur de distribution de Linux hello.   
   - Pour SUSE Linux, recherchez hello exigences de prise en charge de contrat dans [1984787 de # de la Note SAP - SUSE LINUX Enterprise Server 12 : notes d’Installation](https://launchpad.support.sap.com/#/notes/1984787) et [1056161 de # Remarque SAP - SUSE priorité prend en charge pour les applications SAP](https://launchpad.support.sap.com/#/notes/1056161).
   - Pour Red Hat Linux, vous avez besoin toohave hello abonnement approprié niveaux qui incluent la prise en charge et service (met à jour des systèmes d’exploitation de toohello des Instances de grande taille HANA. Red Hat recommande de disposer d’un abonnement « RHEL for SAP Business Applications ». Concernant le support et les services, consultez la [Note de support SAP #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167) (Red Hat Enterprise Linux 7.x : installation et mise à jour) et la [Note de support SAP #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410) (Red Hat Enterprise Linux 6.x : installation et mise à jour) pour en savoir plus.

**Base de données :**

- Licences et composants d’installation logiciels pour SAP HANA (édition Enterprise ou Platform).

**Applications :**

- Les licences et les composants d’installation du logiciel pour toutes les applications SAP connexion tooSAP HANA et les contrats de support SAP.
- Licences et les composants d’installation du logiciel pour toutes les applications non-SAP utilisée dans la relation tooSAP HANA sur l’environnement Azure (Instances de grande taille) et liés des contrats de support.

**Compétences :**

- Expérience et connaissances relatives à Azure IaaS et ses composants.
- Expérience et connaissances relatives au déploiement de charges de travail SAP dans Azure.
- Personnel certifié pour l’installation de SAP HANA.
- SAP architecte compétences toodesign haute disponibilité et récupération d’urgence autour de SAP HANA.

**SAP :**

- Vous devez être un client SAP et disposer d’un contrat de support auprès de SAP
- En particulier pour les implémentations sur hello classe de Type II des références SKU de HANA grande Instance, il est vivement recommandé de tooconsult avec SAP sur les versions de SAP HANA et configurations éventuelles sur la grande taille matériel de montée en puissance parallèle.


## <a name="storage"></a>Storage

disposition de stockage pour SAP HANA sur Azure (Instances de grande taille) Hello est configurée par SAP HANA sur la gestion des services Azure via SAP recommandé, aux instructions hello [besoins de stockage SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) livre blanc.

Instances de grande taille HANA Hello Hello Type I classe fournis avec volume de mémoire hello quatre fois en tant que volume de stockage. Pour type hello classe II d’unités de l’Instance est importante HANA, stockage de hello ne va pas toobe quatre fois plus. unités de Hello sont fournis avec un volume, ce qui est prévu pour le stockage des sauvegardes de journaux de transactions HANA. Obtenir plus de détails dans [comment tooinstall et configurez SAP HANA (instances de grande taille) sur Azure](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Consultez hello tableau en termes d’allocation du stockage suivant. Hello répertorie à peu près capacité hello pour des volumes différents hello fourni avec des unités HANA grande Instance différentes hello.

| Référence SKU de grande instance HANA | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| S72 | 1280 Go | 512 Go | 768 Go | 512 Go |
| S72m | 3 328 Go | 768 Go |1280 Go | 768 Go |
| S192 | 4 608 Go | 1024 Go | 1536 Go | 1024 Go |
| S192m | 11 520 Go | 1536 Go | 1 792 Go | 1536 Go |
| S384 | 11 520 Go | 1536 Go | 1 792 Go | 1536 Go |
| S384m | 12 000 Go | 2 050 Go | 2 050 Go | 2 040 Go |
| S384xm | 16 000 Go | 2 050 Go | 2 050 Go | 2 040 Go |
| S576 | 20 000 Go | 3 100 Go | 2 050 Go | 3 100 Go |
| S768 | 28 000 Go | 3 100 Go | 2 050 Go | 3 100 Go |
| S960 | 36 000 Go | 4 100 Go | 2 050 Go | 4 100 Go |


Volumes déployés réels peuvent varier un peu en fonction de déploiement et les tailles de volume hello tooshow utilisé des outils.

Si vous décomposez une référence SKU de grande instance HANA, voici quelques exemples de division possible :

| Partition de la mémoire en Go | hana/data | hana/log | hana/shared | hana/log/backup |
| --- | --- | --- | --- | --- |
| 256 | 400 Go | 160 Go | 304 Go | 160 Go |
| 512 | 768 Go | 384 Go | 512 Go | 384 Go |
| 768 | 1280 Go | 512 Go | 768 Go | 512 Go |
| 1 024 | 1 792 Go | 640 Go | 1024 Go | 640 Go |
| 1536 | 3 328 Go | 768 Go | 1280 Go | 768 Go |


Ces tailles sont les numéros d’ébauche de volume qui peuvent varier légèrement en fonction de déploiement et outils utilisés toolook volumes de hello. On peut également imaginer d’autres tailles de partition, comme 2,5 To. Ces tailles de stockage est calculées avec une formule similaire que celles utilisées pour les partitions hello ci-dessus. le terme Hello « partitions » n’indique pas que système d’exploitation de hello, la mémoire ou les ressources de processeur sont en aucune façon partitionnées. Il indique uniquement les partitions de stockage pour différentes instances HANA hello, vous souhaiterez peut-être toodeploy sur une unique unité d’Instance est importante HANA. 

Vous comme un client peut avoir besoin pour le stockage de plus, vous avez hello possibilité tooadd toopurchase supplémentaires de stockage en unités de 1 To. Ce stockage supplémentaire peut être ajouté en tant que volume supplémentaire ou peut être utilisé tooextend un ou plusieurs volumes existants de hello. Il n’est pas possible toodecrease les tailles de hello des volumes de hello comme à l’origine déployée et principalement documentées par une ou plusieurs tables hello ci-dessus. Il est également possible toochange les noms de hello des volumes de hello ou montage. les volumes de stockage Hello comme décrit ci-dessus sont des unités de HANA grande Instance toohello attaché en tant que NFS4 volumes.

Vous en tant qu’un client pourrez choisir toouse des instantanés de stockage pour la sauvegarde/restauration et de reprise après sinistre à des fins de récupération. Vous trouverez plus de détails à ce sujet à la page [Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Chiffrement des données au repos
stockage de Hello utilisé pour les Instances de grande taille HANA permet un chiffrement transparent des données de hello tel qu’il est stocké sur des disques hello. Au moment du déploiement d’une unité de Instance HANA volumineux, vous avez hello option toohave ce type de chiffrement est activé. Vous pouvez également choisir toochange tooencrypted volumes après le déploiement hello déjà. déplacement Hello sur les volumes non chiffré de tooencrypted est transparente et ne requiert pas d’un temps d’arrêt. 

Avec hello Type I classe références (SKU), démarrage de hello volume hello numéro d’unité logique est stocké, chiffré. En cas de type hello classe II de références (SKU) de HANA Instances de grande taille, vous devez les LUN de démarrage de hello tooencrypt avec des méthodes de système d’exploitation. 


## <a name="networking"></a>Mise en réseau

architecture Hello de mise en réseau de Azure est le composant clé toosuccessful déploiement d’applications SAP sur les Instances de grande taille HANA. En règle générale, les déploiements SAP HANA sur Azure (grandes instances) ont un plus grand paysage SAP avec plusieurs solutions SAP distinctes et tailles de bases de données variées, une consommation des ressources d’UC et une utilisation de la mémoire différentes. Il est probable que tous les systèmes SAP ne soient pas basés sur SAP HANA, et votre paysage SAP est certainement un hybride qui utilise :

- Des systèmes SAP déployés en local. En raison des tailles de tootheir, ces systèmes actuellement ne peut pas être hébergés dans Azure ; un exemple classique est un système ERP SAP de production en cours d’exécution sur Microsoft SQL Server (en tant que base de données hello) ce qui nécessite plus d’UC ou de fournissent des ressources de mémoire machines virtuelles Azure.
- Des systèmes SAP basés sur SAP HANA déployés en local.
- Des systèmes SAP déployés dans des machines virtuelles Azure. Ces systèmes peuvent être développement, test, bac à sable, ou instances de production pour les applications SAP NetWeaver hello que peuvent déployer avec succès dans Azure (sur des ordinateurs virtuels), en fonction de la demande de mémoire et de la consommation de ressources. Ces systèmes peuvent également être basés sur des bases de données comme SQL Server (consultez [SAP Support Note #1928533 – SAP Applications on Azure: Supported Products and Azure VM types (Note de prise en charge SAP n° 1928533 - Applications SAP sur Azure : Types de machines virtuelles Azure et produits pris en charge)](https://launchpad.support.sap.com/#/notes/1928533/E)) ou SAP HANA (consultez [SAP HANA Certified IaaS Platforms (Plateformes IaaS certifiées SAP HANA)](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- Des serveurs d’applications SAP déployés dans Azure (sur des machines virtuelles) qui utilisent SAP HANA sur Azure (grandes instances) dans les tampons de grande instance Azure.

Tandis qu’un environnement SAP hybride (avec quatre scénarios de déploiement différents ou plus) est typique, il existe de nombreux cas client ayant un paysage SAP s’exécutant intégralement dans Azure. Comme Microsoft Azure Virtual Machines deviennent plus puissants, nombre de hello de clients déplacer toutes leurs solutions SAP sur Azure augmente.

Mise en réseau dans le contexte de hello de systèmes SAP déployé dans Azure Azure n’est pas compliqué. Il est basé sur hello suivant principes :

- Réseaux virtuels Azure (réseaux virtuels) devez toobe connecté toohello Azure ExpressRoute circuit qui se connecte le réseau local tooon.
- Un circuit ExpressRoute connexion locale tooAzure généralement doit avoir une bande passante de 1 Gbit/s ou plus. La bande passante minimale permet une bande passante suffisante pour transférer des données entre les systèmes locaux et les systèmes s’exécutant sur des machines virtuelles Azure (ainsi que des systèmes de tooAzure de connexion à partir des utilisateurs finaux sur site).
- Tous les systèmes SAP dans Azure besoin toobe défini dans toocommunicate de réseaux virtuels Azure entre eux.
- Le répertoire Active Directory et le DNS hébergés en local sont étendus à Azure via ExpressRoute, en local.


> [!NOTE] 
> À partir d’un point de vue facturation, tooone uniquement un seul locataire dans un tampon de grande Instance dans une région Azure spécifique peut être lié à un seul abonnement Azure, et inversement un seul client de tampon de grande Instance peut être lié uniquement tooone abonnement Azure. Ce fait est tooany, pas différent autres objets facturables dans Azure

Déploiement SAP HANA sur Azure (Instances de grande taille) dans plusieurs régions Azure différentes, les résultats dans un toobe client distinct déploiement dans hello cachet d’Instance est importante. Toutefois, vous pouvez exécuter à la fois hello de paysage SAP même tant que ces instances font partie de hello même abonnement Azure. 

> [!IMPORTANT] 
> Seul le déploiement Azure Resource Manager est pris en charge avec SAP HANA sur Azure (grandes instances).

 

### <a name="additional-azure-vnet-information"></a>Informations supplémentaires sur les réseaux virtuels Azure

Dans l’ordre tooconnect un tooExpressRoute de réseau virtuel Azure, une passerelle Azure doit être créée (voir [sur les passerelles de réseau virtuel pour ExpressRoute](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Une passerelle Azure peut être utilisée avec l’infrastructure de tooan ExpressRoute en dehors de Azure (ou tampon d’instance Azure grand tooan), ou tooconnect entre réseaux virtuels Azure (consultez [configurer une connexion au réseau pour le Gestionnaire de ressources à l’aide de PowerShell ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Vous pouvez vous connecter au maximum tooa quatre différentes connexions ExpressRoute hello passerelle Azure tant que ces connexions proviennent différents routeurs MS Enterprise bords (MSEE).  Pour plus d’informations, consultez la page [Infrastructure et connectivité à SAP HANA (grandes instances) sur Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> Hello une passerelle Azure fournit un débit est différent pour les deux cas d’usage (consultez [sur la passerelle du VPN](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). débit maximal de Hello que nous pouvons atteindre avec une passerelle de réseau virtuel est à 10 Gbits/s, à l’aide d’une connexion ExpressRoute. N’oubliez pas que copie de fichiers entre une machine virtuelle de Azure résidant dans un réseau virtuel Azure et d’un système local (comme un flux de copie unique) ne pas atteindre un débit complet hello de passerelle de hello différentes références (SKU). la bande passante complète tooleverage hello de passerelle de réseau virtuel hello, vous devez utiliser plusieurs flux de données ou de la copie des fichiers différents dans des flux parallèles d’un seul fichier.


### <a name="networking-architecture-for-hana-large-instances"></a>Architecture de mise en réseau pour les grandes instances HANA
Hello architecture de mise en réseau pour les Instances de grande taille HANA comme indiqué ci-dessous, peut être divisée en quatre parties :

- Mise en réseau sur site et tooAzure de connexion ExpressRoute. Cette partie est le domaine des clients hello et tooAzure connecté via ExpressRoute. Cela fait partie de hello dans hello partie inférieure droite du graphique hello ci-dessous.
- Mise en réseau Azure brièvement décrite ci-dessus avec des réseaux virtuels Azure, qui ont aussi des passerelles. Il s’agit d’une zone où vous devez les conceptions de toofind hello approprié pour vos exigences d’applications, de sécurité et les exigences de conformité. À l’aide d’Instances de grande taille HANA est un autre point de prendre en compte en termes de nombre de réseaux virtuels et Azure toochoose de références (SKU) de passerelle à partir de. Cela fait partie de hello dans hello coin supérieur droit du graphique de hello.
- Connectivité des grandes instances HANA grâce à la technologie ExpressRoute dans Azure. Cette partie est déployée et gérée par Microsoft. Vous devez toodo comme un client est tooprovide certaines plages d’adresses IP et après le déploiement de hello de vos ressources dans les Instances de grande taille HANA connexion hello ExpressRoute circuit toohello VNet(s) de Azure (consultez [Infrastructure de SAP HANA (instances de grande taille) et connectivité sur Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- Mise en réseau dans les grandes instances HANA, qui est essentiellement transparente pour vous en tant que client.

![Réseau virtuel Azure connecté tooSAP HANA sur Azure (Instances de grande taille) et locales](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

faits Hello que vous utilisez des instances HANA volumineuses ne change pas tooget d’exigence de hello vos ressources locales connectés via ExpressRoute tooAzure. Également, il ne change pas de spécification hello pour avoir un ou plusieurs réseaux virtuels qui exécutent des machines virtuelles de Azure hello quelle couche d’application hello hôte qui se connecte les instances HANA toohello hébergées dans des unités d’Instance est importante HANA. 

déploiements de tooSAP différence Hello dans pure Azure, est fourni avec des faits hello qui :

- Hello HANA grande Instance de votre client de client sont connectés via un autre circuit ExpressRoute dans votre VNet(s) Azure. Dans les conditions de charge ordre tooseparate, tooAzure sur site de hello VNets ExpressRoute liens et des liens entre des réseaux virtuels Azure et HANA grosses instances ne partagent pas hello même routeurs.
- profil de charge de travail Hello entre la couche d’application SAP hello et hello HANA Instance est un caractère différent de nombreuses petites requêtes, et croissance comme données transfère (jeux de résultats) à partir de SAP HANA dans la couche d’application hello.
- Hello architecture de l’application SAP est la latence toonetwork plus sensible à des scénarios classiques où les données obtient échangées entre locaux et Azure.
- passerelle de réseau virtuel Hello possède au moins deux connexions ExpressRoute et les deux connexions partagent la bande passante maximale de hello pour les données entrantes de passerelle de réseau virtuel hello.

latence du réseau Hello expérimentée entre machines virtuelles Azure et HANA grandes unités d’instance peut être supérieure à un ordinateur virtuel en ordinateur virtuel réseau aller-retour temps de latence. Dépend de hello région Azure, les valeurs hello mesurées peuvent dépasser hello 0,7 ms aller-retour latence classée en dessous de la moyenne dans [1100926 de # de la Note SAP - Forum aux questions : des performances réseau](https://launchpad.support.sap.com/#/notes/1100926/E). Néanmoins, les clients ont réussi à déployer des applications SAP de production basées sur SAP HANA avec succès sur des grandes instances SAP HANA. les clients Hello qui déployé signalé améliorations en exécutant leurs applications SAP sur SAP HANA à l’aide d’unités de l’Instance est importante HANA. Toutefois, nous vous conseillons de tester minutieusement vos processus métier dans les grandes instances HANA Azure.
 
Dans l’ordre tooprovide déterministe latence du réseau entre les machines virtuelles Azure et HANA grande Instance, choisissez hello hello SKU de passerelle de réseau virtuel Azure est essentielle. Contrairement aux modèles de trafic hello entre locaux et les machines virtuelles Azure, le modèle de trafic hello entre machines virtuelles Azure et les Instances de grande taille HANA peut développer des rafales petits mais élevées de demandes et toobe de volumes de données transmises. Dans l’ordre toohave ces rafales gérées correctement, nous vous recommandons l’utilisation de hello Hello SKU de passerelle UltraPerformance. Pour hello classe de Type II des références SKU de HANA grande Instance, l’utilisation de hello de passerelle de UltraPerformance hello référence (SKU) en tant que passerelle de réseau virtuel Azure est obligatoire.  

> [!IMPORTANT] 
> Donné hello du trafic réseau global entre hello SAP couches d’application et de base de données, hello uniquement les hautes performances ou UltraPerformance passerelle références (SKU) pour les réseaux virtuels est pris en charge pour la connexion tooSAP HANA sur Azure (Instances de grande taille). Pour l’instance HANA volumineux références (SKU) de Type II, uniquement hello SKU de passerelle UltraPerformance est pris en charge en tant que passerelle de réseau virtuel Azure.



### <a name="single-sap-system"></a>Système SAP unique

infrastructure locale de Hello ci-dessus est connecté via ExpressRoute dans Azure et hello circuit ExpressRoute se connecte à un routeur de périphérie Enterprise (MSEE) Microsoft (consultez [présentation technique d’ExpressRoute](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Une fois établie, cet itinéraire se connecte dans la structure fondamentale de Microsoft Azure hello et toutes les régions Azure sont accessibles.

> [!NOTE] 
> Pour l’exécution de paysages SAP dans Azure, se connecter toohello MSEE toohello le plus proche région Azure dans le paysage SAP de hello. Les tampons de grande Instance Azure sont connectés via dédié MSEE périphériques toominimize latence du réseau entre les machines virtuelles Azure dans les tampons IaaS Azure et d’Instance est importante.

passerelle de réseau virtuel pour hello machines virtuelles de Azure, hébergeant des instances d’application SAP, Hello est connecté toothat circuit ExpressRoute et hello même réseau virtuel est connecté tooa distinct routeur MSEE dédié tooconnecting tooLarge Instance tampons.

Il s’agit d’un exemple simple d’un système SAP unique, où la couche application SAP hello est hébergé dans Azure et base de données SAP HANA hello s’exécute sur SAP HANA sur Azure (Instances de grande taille). hypothèse de Hello est que la bande passante de passerelle réseau virtuel hello de 2 Gbits/s ou 10 Gbits/s débit ne représente pas un goulet d’étranglement.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Plusieurs systèmes SAP ou grands systèmes SAP

Si plusieurs systèmes SAP ou les grands systèmes SAP sont déployées connexion tooSAP HANA sur Azure (Instances de grande taille), &#39; le débit de hello s tooassume raisonnable de passerelle de réseau virtuel hello peut devenir un goulot d’étranglement. Dans ce cas, vous devez les couches d’application hello toosplit dans plusieurs réseaux virtuels de Azure. Il peut également être toocreate pourquoi des réseaux virtuels spéciale qui se connectent à des Instances de grande taille tooHANA pour les cas tels que :

- Effectuer des sauvegardes directement à partir de hello HANA Instances dans les Instances de grande taille HANA tooa machine virtuelle dans Azure qui héberge les partages NFS
- Copie des sauvegardes de grande taille ou d’autres fichiers de HANA grande Instance unités toodisk espace géré dans Azure.

À l’aide des réseaux virtuels distincts que hôte d’ordinateurs virtuels qui gérer le stockage de hello évite impact par un fichier volumineux ou de transfert de données à partir d’Instances de grande taille HANA tooAzure sur hello passerelle de réseau virtuel qui sert de machines virtuelles de hello couche d’application SAP hello en cours d’exécution. 

Pour une architecture réseau plus évolutive :

- Utilisez plusieurs réseaux virtuels Azure pour une couche Application SAP unique, plus grande.
- Déployer un réseau virtuel Azure distincts pour chaque système SAP déployé, toocombining comparé ces systèmes SAP dans des sous-réseaux distincts sous hello même réseau virtuel.

 Une architecture réseau plus évolutive pour SAP HANA sur Azure (grandes instances) :

![Déploiement de la couche Application SAP sur plusieurs réseaux virtuels Azure](./media/hana-overview-architecture/image4-networking-architecture.png)

Déploiement de couche d’application SAP hello ou des composants, sur plusieurs réseaux virtuels Azure comme indiqué ci-dessus, introduit la surcharge de latence inévitable qui s’est produite pendant la communication entre les applications hello hébergées dans les réseaux virtuels Azure. Par défaut, le trafic réseau de hello entre les machines virtuelles Azure situés dans différents réseaux virtuels passent hello routeurs MSEE dans cette configuration. Toutefois, depuis septembre 2016, ce routage peut être optimisé. Hello moyen toooptimize et réduire la latence hello dans les communications entre deux réseaux virtuels sont par des réseaux virtuels Azure d’homologation dans hello même région. Cela est valable même si ces réseaux virtuels appartiennent à des abonnements différents. À l’aide du réseau virtuel Azure homologation, communication hello entre les ordinateurs virtuels dans les deux réseaux virtuels de Azure différents permettre utiliser hello réseau Azure backbone toodirectly communiquent entre eux. Ainsi affichant la latence similaire comme si hello machines virtuelles serait dans hello même réseau virtuel. Alors que le trafic, ciblant des plages d’adresses IP qui sont connectés via une passerelle de réseau virtuel Azure hello est routé via hello passerelle de réseau virtuel individuelle de hello réseau virtuel. Vous pouvez obtenir plus d’informations sur le réseau virtuel Azure homologation dans l’article de hello [réseau virtuel d’homologation](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Routage dans Azure

Deux points importants sont à prendre en compte en matière de routage pour SAP HANA sur Azure (grandes instances) :

1. SAP HANA sur Azure (Instances de grande taille) n’est accessible par les machines virtuelles Azure dans hello dédié ExpressRoute connexion ; pas directement à partir des locaux. Certains clients d’administration et les applications nécessitant un accès direct, telles que SAP Solution Manager est en cours d’exécution en local, ne peut pas se connecter à base de données SAP HANA toohello.

2. SAP HANA sur des unités de Azure (Instances de grande taille) ont une adresse IP à partir de l’adresse de Pool IP serveur hello vous plage en tant que client hello soumis (consultez [SAP HANA (instances de grande taille) et la connectivité sur Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations).  Cette adresse IP est accessible via hello Azure ExpressRoute qui se connecte tooHANA de réseaux virtuels Azure sur Azure (Instances de grande taille) et les abonnements. Hello adresse IP affectée en dehors de cette plage d’adresses de Pool IP du serveur est directement attribué l’unité matérielle à toohello et n’est pas NAT'ed plus, comme c’était le cas de hello dans les déploiements de première hello de cette solution. 

> [!NOTE] 
> Si vous avez besoin de tooconnect tooSAP HANA sur Azure (Instances de grande taille) dans un _l’entrepôt de données_ scénario, où les applications ou les utilisateurs finaux doivent tooconnect base de données SAP HANA toohello (exécution directe), un autre composant du réseau doit être utilisé : un proxy inversé tooroute données, les tooand à partir de. Par exemple, F5 BIG-IP, NGINX avec Traffic Manager déployé dans Azure en tant que solution de routage de trafic/pare-feu virtuelle.

### <a name="internet-connectivity-of-hana-large-instances"></a>Connectivité internet des grandes instances HANA
Les grandes instances HANA ne bénéficient PAS d’une connectivité directe à Internet. Cela limite vos compétences pour, par exemple inscrire image de système d’exploitation hello directement avec le fournisseur du système d’exploitation hello. Par conséquent, vous devrez peut-être toowork avec serveur SLES SMT local ou le Gestionnaire d’abonnement RHEL

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Chiffrement des données entre les machines virtuelles Azure et les grandes instances HANA
Les données transférées entre les grandes instances HANA et les machines virtuelles Azure ne sont pas chiffrées. Toutefois, purement pour exchange hello entre hello côté de HANA DBMS et les applications de base JDBC/ODBC, vous pouvez activer le chiffrement du trafic. Reportez-vous à [cette documentation SAP](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Utilisation d’unités de grande instance HANA dans plusieurs régions

Vous pouvez avoir d’autres raisons de toodeploy HANA SAP sur Azure (Instances de grande taille) dans plusieurs régions Azure, en plus de la récupération d’urgence. Vous pouvez choisir de tooaccess HANA les Instances de grande taille de chacun des ordinateurs virtuels de hello déployés Bonjour différents réseaux virtuels dans des régions hello. Étant donné que les adresses IP hello affecté toohello différentes unités d’Instances de grande taille HANA ne sont pas propagées au-delà de hello réseaux virtuels Azure (qui sont connectés directement via leurs instances de toohello passerelle), il existe un léger modifier toohello conception de réseau virtuel présentée ci-dessus : un Passerelle de réseau virtuel Azure peut gérer des circuits ExpressRoute différents quatre hors MSEEs différents, et chaque réseau virtuel qui est connecté tooone des tampons de grande Instance hello peut être le tampon de grande Instance toohello connectés dans une autre région Azure.

![Réseaux virtuels Azure connecté tooAzure les tampons de grande Instance dans différentes régions Azure](./media/hana-overview-architecture/image8-multiple-regions.png)

Hello ci-dessus figure hello comment les réseaux virtuels Azure différent dans les deux régions sont connectés tootwo des circuits ExpressRoute différents qui sont utilisés tooconnect tooSAP HANA sur Azure (Instances de grande taille) dans les deux régions Azure. les connexions Hello récemment introduit sont des lignes rouges rectangulaire de hello. Avec ces connexions, hors hello réseaux virtuels Azure, les ordinateurs virtuels de hello en cours d’exécution dans un de ces réseaux virtuels peuvent accéder aux unités hello différentes Instances de grande taille HANA déployées dans deux régions de hello. Comme vous le voir dans les graphiques hello ci-dessus, il est supposé que vous avez deux connexions ExpressRoute de local toohello deux régions Azure ; recommandé pour des raisons de la récupération d’urgence.

> [!IMPORTANT] 
> Si plusieurs circuits ExpressRoute sont utilisés, ajoutant au début du chemin d’accès en tant qu’et les paramètres BGP de préférence Local doivent être utilisé tooensure appropriée de routage du trafic.


