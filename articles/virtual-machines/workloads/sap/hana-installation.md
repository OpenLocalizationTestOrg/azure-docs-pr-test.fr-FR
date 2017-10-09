---
title: aaaInstall SAP HANA sur SAP HANA sur Azure (Instances de grande taille) | Documents Microsoft
description: Comment tooinstall SAP HANA sur une SAP HANA sur Azure (grande Instance).
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
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
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Comment tooinstall et configurez SAP HANA (instances de grande taille) sur Azure

Voici quelques définitions importantes de tooknow avant de lire ce guide. Dans [Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture), nous avons présenté deux classes différentes d’unités de grande instance HANA avec :

- S72, S72m, S144, S144m, S192 et S192m, ce qui constitue tooas hello 'I classe de Type' de références (SKU).
- S384, S384m, S384xm, S576, S768 et S960, ce qui constitue tooas hello 'Classe de Type II' des références SKU.

spécificateur de classe Hello est toobe continu utilisée tout au long de hello HANA grande Instance documentation tooeventually font référence toodifferent fonctionnalités et les besoins en fonction des références (SKU) Instance volumineux HANA.

Nous utilisons fréquemment les autres définitions suivantes :
- **Cachet d’Instance volumineux :** une pile d’infrastructure matérielle SAP HANA TDI certifié et dédié toorun des instances de SAP HANA dans Azure.
- **SAP HANA sur Azure (Instances de grande taille) :** nom officiel de l’offre de hello dans Azure toorun HANA instances sur l’interface TDI SAP HANA certifié matériel déployé dans les tampons de grande Instance dans différentes régions Azure. Hello liées terme **HANA grande Instance** est l’abréviation de HANA SAP sur Azure (Instances de grande taille) et est largement utilisé ce guide de déploiement technique.


installation Bonjour de SAP HANA est votre responsabilité, et vous pouvez démarrer l’activité hello après la remise d’une nouvelle SAP HANA sur le serveur Azure (Instances de grande taille). Et une fois la connectivité hello entre votre VNet(s) d’Azure et les hello HANA grande Instance ou les unités a été établie. 

> [!Note]
> Par la stratégie SAP, installation Bonjour de SAP HANA doit être effectuée par une personne certifié tooperform les installations SAP HANA. Une personne a passé l’examen d’associer des technologies certifié SAP hello, examens de certification d’Installation de SAP HANA, ou par un intégrateur système certifié SAP (SI).

Vérifiez de nouveau, en particulier lors de la planification tooinstall HANA 2.0, [SAP Support Remarque #2235581 - SAP HANA : prise en charge des systèmes d’exploitation](https://launchpad.support.sap.com/#/notes/2235581/E) dans l’ordre toomake que ce hello de système d’exploitation est pris en charge par hello SAP HANA release vous décidé tooinstall. Vous réalisez que hello système d’exploitation pris en charge pour HANA 2.0 n’est plus restreint que hello du système d’exploitation pris en charge pour HANA 1.0. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Premières étapes après la réception hello HANA grande Instance ou les unités

**Première étape** après la réception hello HANA grande Instance et ayant établi des instances toohello connectivité et d’accès, est tooregister hello du système d’exploitation de l’instance hello avec votre fournisseur de système d’exploitation. Cette étape inclut l’inscription de votre système d’exploitation de Linux SUSE dans une instance de SUSE SMT dont vous avez besoin toohave déployé dans une machine virtuelle dans Azure. unité d’Instance est importante HANA Hello peut se connecter à instance SMT toothis (voir plus loin dans cette documentation). Ou votre système d’exploitation RedHat doit toobe inscrit avec hello Red Hat abonnement Manager, vous devez tooconnect à. Consultez également la section Remarques de ce [document](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Cette étape est également nécessaire toobe toopatch en mesure de hello du système d’exploitation. Une tâche qui se trouve dans la responsabilité hello du client de hello. Pour SUSE, documentation tooinstall et configurera SMT [ici](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Deuxième étape** est toocheck pour les nouveaux correctifs et des correctifs de la version du système d’exploitation spécifique hello/version. Vérifiez si le niveau de correctif logiciel hello Hello HANA grande Instance sur l’état le plus récent hello. En fonction de minutage de système d’exploitation versions des correctifs et modifications toohello image que Microsoft permettre déployer, il peut arriver où correctifs les plus récents hello ne peuvent pas être inclus. Par conséquent, il est une étape obligatoire après la prise en charge une unité HANA grande Instance, toocheck si des correctifs de sécurité, de fonctionnalités, de disponibilité et de performances ont été publiées dans le même temps par le fournisseur Linux hello et doivent toobe appliqué.

**Troisième étape** est toocheck out hello Notes SAP appropriées pour l’installation et la configuration de SAP HANA sur hello spécifique du système d’exploitation/version. En raison de tooSAP de recommandations ou des modifications toochanging Notes ou des configurations qui sont dépendantes de scénarios d’installation individuels, Microsoft ne seront pas toujours en mesure de toohave une unité HANA grande Instance configurée parfaitement. Par conséquent, il est obligatoire pour vous en tant que client, tooread hello Notes SAP connexe tooSAP HANA sur votre version de Linux exacte. Également vérifier les configurations hello de hello du système d’exploitation/version nécessaire et appliquer les paramètres de configuration hello où ne pas déjà fait.

Dans spécifique, vérifiez hello paramètres suivants et ajustée par la suite à :

- net.core.rmem_max = 16777216
- net.core.wmem_max = 16777216
- net.core.rmem_default = 16777216
- net.core.wmem_default = 16777216
- net.core.optmem_max = 16777216
- net.ipv4.tcp_rmem = 65536 16777216 16777216
- net.ipv4.tcp_wmem = 65536 16777216 16777216

À partir de SLES12 SP1 et RHEL 7.2, ces paramètres doivent être définis dans un fichier de configuration dans le répertoire de /etc/sysctl.d hello. Par exemple, un fichier de configuration avec le nom hello 91-NetApp-HANA.conf doit être créé. Pour les versions plus anciennes de SLES et RHEL, ces paramètres doivent être définis dans /etc/sysctl.conf.

Pour RHEL toutes les versions et à partir de SLES12, hello 
- sunrpc.tcp_slot_table_entries = 128

doit être défini dans /etc/modprobe.d/sunrpc-local.conf. Si le fichier de hello n’existe pas, il devez d’abord créer en ajoutant hello entrée suivante : 
- options sunrpc tcp_max_slot_table_entries=128

**Quatrième étape** toocheck hello système fois de votre unité d’Instance volumineux HANA. les instances de Hello sont déployées avec un fuseau horaire système qui représentent l’emplacement hello Hello de région Azure hello dans que HANA grand tampon d’Instance se trouve. Vous êtes libre toochange hello heure du système ou du fuseau horaire d’instances hello que vous êtes propriétaire. Cette opération et classement d’autres instances dans votre locataire, être préparé que vous avez besoin de fuseau horaire tooadapt hello hello qui vient d’être remis instances. Opérations de Microsoft n’ont aucune insights dans le fuseau horaire du système hello que vous configurez avec des instances de hello après le transfert de hello. Par conséquent, les instances qui vient d’être déployés ne sont pas définies dans hello même fuseau horaire que hello un, vous avez choisi. Par conséquent, il vous incombe en tant que client toocheck et si nécessaire adapter le fuseau horaire de hello des instances hello remis. 

**Cinquième étape** est toocheck etc/hosts. Comme les panneaux hello obtient remis, ils ont différentes adresses IP affectées à différentes fins (voir la section suivante). Vérifiez hello etc/hosts, fichier. Dans les cas où les unités sont ajoutées à un client, ne prévoyez pas toohave etc./hôtes des systèmes hello nouvellement déployé dûment avec des adresses IP hello précédemment livré systèmes. Il est donc vous en tant que paramètres de client toocheck hello correct, qu’une instance qui vient d’être déployée peut interagir et résoudre les noms de hello précédemment déployées d’unités de dans votre client. 

## <a name="networking"></a>Mise en réseau
Nous supposons que vous avez suivi les recommandations hello dans la conception de vos réseaux virtuels Azure et de connexion de ces Instances de grande taille de réseaux virtuels toohello HANA comme décrit dans ces documents :

- [Vue d’ensemble et architecture de SAP HANA (grandes instances) sur Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Infrastructure et connectivité à SAP HANA (grandes instances) sur Azure](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Il existe certaines informations dignes de toomention sur la mise en réseau de hello des unités hello. Chaque unité HANA grande Instance est fourni avec deux ou trois adresses IP qui sont attribuées tootwo ou trois ports de carte réseau de l’unité de hello. Trois adresses IP sont utilisées dans les configurations de montée en puissance parallèle HANA et le scénario de réplication du système HANA hello. Une des adresses IP de hello affecté toohello carte réseau de l’unité de hello est hors hello pool d’adresse IP du serveur qui a été décrite dans hello [vue d’ensemble de SAP HANA (grande Instance) et l’Architecture sur Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

distribution Hello pour les unités de deux adresses IP attribuées doit ressembler à :

- eth0.xx doit avoir une adresse IP qui est en dehors de la plage d’adresses de Pool IP du serveur que vous avez soumis tooMicrosoft de hello. Cette adresse IP doit être utilisée pour la gestion dans/etc/hosts de hello du système d’exploitation.
- eth1.xx doit avoir une adresse IP qui est utilisée pour la communication tooNFS. Par conséquent, ces adresses exécuter **pas** devez toobe mis à jour dans les hôtes/etc. ordre tooallow instance tooinstance du trafic au sein de client de hello.

Une configuration à deux adresses IP ne convient pas aux déploiements de réplication système HANA ou aux montées en charge HANA. Si avoir deux adresses IP uniquement et que vous souhaitiez toodeploy une telle configuration, contactez SAP HANA sur la gestion des services Azure tooget une troisième adresse IP dans un réseau local virtuel affecté tiers. Pour les unités HANA grande Instance ayant trois adresses IP sont affectées sur trois ports de carte réseau, hello l’utilisation des règles suivantes s’appliquent :

- eth0.xx doit avoir une adresse IP qui est en dehors de la plage d’adresses de Pool IP du serveur que vous avez soumis tooMicrosoft de hello. Par conséquent, cette adresse IP ne doit pas être utilisée de maintenance dans/etc/hosts de hello du système d’exploitation.
- eth1.xx doit avoir une adresse IP qui est utilisée pour le stockage de tooNFS de communication. Ce type d’adresse ne doit donc pas être mis à jour dans le fichier etc/hosts.
- eth2.xx doivent être exclusivement utilisé toobe mis à jour dans etc/hosts pour la communication entre différentes instances de hello. Ces adresses serait également des adresses IP hello nécessitant toobe conservée dans les configurations de montée en puissance parallèle HANA en tant qu’adresses IP que HANA utilise pour la configuration entre les nœuds de hello.



## <a name="storage"></a>Storage

disposition de stockage pour SAP HANA sur Azure (Instances de grande taille) Hello est configurée par SAP HANA sur la gestion des services Azure via SAP recommandé de lignes de repère comme documenté dans [besoins de stockage SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) livre blanc. Hello taille approximative des volumes différents de hello avec hello différents HANA grandes Instances références (SKU) obtenu documentées dans [vue d’ensemble de SAP HANA (grande Instance) et l’Architecture sur Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

conventions d’affectation de noms de Hello hello des volumes de stockage sont répertoriées dans hello tableau suivant :

| Utilisation du stockage | Nom du montage | Nom du volume | 
| --- | --- | ---|
| Données HANA | /hana/data/SID/mnt0000<m> | Adresse IP du stockage:/hana_data_SID_mnt00001_tenant_vol |
| Journal HANA | /Hana/log/SID/mnt0000<m> | Adresse IP du stockage:/hana_log_SID_mnt00001_tenant_vol |
| Sauvegarde de fichier journal HANA | HANA/log/backups | Adresse IP du stockage:/hana_log_backups_SID_mnt00001_tenant_vol |
| HANA partagé | /Hana/Shared/SID | Adresse IP du stockage:/hana_shared_SID_mnt00001_tenant_vol/shared |
| /usr/sap | /usr/SAP/SID | Adresse IP du stockage:/hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Où SID = hello HANA instance ID système 

Et tenant est une énumération interne des opérations lors du déploiement d’un client.

Comme vous pouvez le voir, HANA partagé et usr/sap partagent hello même volume. nomenclature Hello de points de montage hello inclut-il hello ID système des instances HANA hello, ainsi que nombre de montage hello. Dans les déploiements avec montée en puissance parallèle, il n’existe qu’un seul montage, par exemple mnt00001. Dans un déploiement avec montée en puissance parallèle vous devriez voir un nombre de montages équivalent au nombre de nœuds worker et principaux. Pour un environnement de montée en puissance parallèle hello, les données, les journaux, les volumes de sauvegarde de journal sont nœud tooeach partagé et attachées dans la configuration de montée en puissance parallèle hello. Pour les configurations d’exécution de plusieurs instances SAP, un ensemble différent de volumes est unité d’Instance est importante HAN toohello créé et attaché.

Quand vous lisez hello et recherchez une unité HANA grande Instance, vous gardez à l’esprit que les unités hello livrés avec le volume de disque plutôt pas mal HANA/données et qu’un volume HANA / / sauvegarde de journal. Hello pourquoi nous dimensionné hello HANA/données tellement importante parce que nous proposons pour vous en tant que client sont à l’aide de captures instantanées de stockage hello hello même volume de disque. Cela signifie que hello plus des instantanés de stockage que vous effectuez, hello davantage d’espace utilisé par les instantanés de vos volumes de stockage. volume HANA / / sauvegarde de journal Hello n’est pas le volume pensée toobe hello tooput les sauvegardes de base de données dans. Elle est dimensionnée toobe utilisé comme volume de sauvegarde pour les sauvegardes de journaux de transactions hello HANA. Dans les futures versions de stockage de hello instantané des instantanés libre-service, que nous cibleront cette toohave volume spécifique plus fréquents. Et avec celles plus fréquemment le site de récupération d’urgence de réplications toohello si vous le souhaitez toooption dans pour la fonctionnalité de récupération d’urgence hello fournie par l’infrastructure d’Instance est importante HANA hello. Pour plus de détails, voir [Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

En outre toohello stockage fourni, vous pouvez acheter par incréments de 1 To de capacité de stockage supplémentaire. Ce stockage supplémentaire peut être ajouté en tant que nouveaux volumes tooa HANA les Instances de grande taille.

Lors de l’intégration avec SAP HANA sur la gestion des services Azure, hello le client spécifie un ID d’utilisateur (UID) et l’ID de groupe (GID) pour le groupe d’utilisateur et sapsys sidadm hello (ex : 1000,500) il n’est nécessaire lors de l’installation de système de SAP HANA de hello, ces mêmes valeurs sont utilisées. Que vous le souhaitez toodeploy plusieurs instances HANA sur une unité, vous obtenez plusieurs ensembles de volumes (un ensemble pour chaque instance). Par conséquent, au moment du déploiement, vous devez toodefine :

- Hello SID de différentes instances HANA hello (sidadm est dérivée hors il).
- Tailles de mémoire des différentes instances HANA hello. Étant donné que la taille de la mémoire par les instances hello définit la taille hello des volumes de hello dans chaque ensemble de volumes spécifique.

Selon les recommandations de fournisseur de stockage hello montage options suivantes est configurée pour tous les volumes montés (exclut les LUN de démarrage) :

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

Ces points sont configurés dans/etc/fstab, comme indiqué dans hello suivant graphics de montage :

![fstab des volumes montés dans l’unité de grande instance HANA](./media/hana-installation/image1_fstab.PNG)

sortie Hello de hello commande df -h sur une unité S72m HANA grande Instance ressemble à :

![fstab des volumes montés dans l’unité de grande instance HANA](./media/hana-installation/image2_df_output.PNG)


contrôleur de stockage Hello et de nœuds dans les tampons de grande Instance hello sont synchronisés tooNTP serveurs. Avec vous synchronisation hello SAP HANA sur les unités de Azure (Instances de grande taille) et de machines virtuelles Azure par rapport à un serveur NTP, il ne doit y avoir aucun problème de dérive beaucoup de temps entre hello des unités de calcul dans Azure ou grande Instance marqueurs et l’infrastructure de hello.

Dans l’ordre toooptimize SAP HANA toohello espace de stockage utilisé en dessous, vous devez également définir hello SAP HANA configuration paramètres suivants :

- max_parallel_io_requests 128
- async_read_submit on
- async_write_submit_active on
- async_write_submit_blocks all
 
Pour les versions de SAP HANA 1.0 des tooSPS12, ces paramètres peuvent être définis lors de l’installation de hello de base de données SAP HANA hello, comme décrit dans [2267798 de # de la Note SAP - Configuration de base de données SAP HANA de hello](https://launchpad.support.sap.com/#/notes/2267798)

Vous pouvez également configurer les paramètres de hello après l’installation de base de données SAP HANA hello aide hello hdbparam framework. 

SAP HANA 2.0, le framework de hdbparam hello a été déconseillée. En conséquence les paramètres hello doivent être définis à l’aide de commandes SQL. Pour plus d’informations, consultez la [Note de support SAP #2399079 : Elimination of hdbparam in HANA 2](https://launchpad.support.sap.com/#/notes/2399079) (Suppression de hbdparam dans HANA 2).


## <a name="operating-system"></a>Système d’exploitation

Espace d’échange de hello remis l’image de système d’exploitation a la valeur Go too2 selon toohello [SAP Support Remarque #1999997 - Forum aux questions : SAP HANA mémoire](https://launchpad.support.sap.com/#/notes/1999997/E). Tout autre paramètre souhaité besoins toobe vous définissez en tant que client.

[SUSE Linux Enterprise Server 12 SP1 pour les Applications SAP](https://www.suse.com/products/sles-for-sap/hana) est hello de distribution de Linux installé pour SAP HANA sur Azure (Instances de grande taille). Cette distribution particulier fournit des fonctionnalités spécifiques à la SAP &quot;prédéfinies hello&quot; (y compris les paramètres prédéfinis pour l’exécution de SAP sur SLES efficacement).

Consultez [ressource de bibliothèque/publications](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) sur le site Web SUSE hello et [SAP sur SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) sur hello SAP Communauté réseau (SCN) pour plusieurs ressources utiles concernant toodeploying SAP HANA SLES (y compris hello configuration de la haute disponibilité, les opérations de tooSAP spécifique de renforcement de sécurité, etc.).

Autres liens utilies concernant SAP sur SUSE :

- [SAP HANA sur le site SUSE Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE)
- [Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113) (Meilleure pratique pour SAP : Réplication de la file d’attente – SAP NetWeaver sur Linux Enterprise 12).
- [ClamSAP - SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (ClamSAP – Protection antivirus SLES pour SAP, y compris SLES 12 for les applications SAP).

SAP tooimplementing applicable de prise en charge des Notes SAP HANA sur SLES 12 :

- [Note de support SAP #1944799 relative aux instructions SAP HANA pour l’installation du système d’exploitation SLES](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html).
- [Note de support SAP #2205917 relative aux paramètres de système d’exploitation SAP HANA DB recommandés pour SLES 12 ainsi que les application SAP](https://launchpad.support.sap.com/#/notes/2205917/E).
- [Note de support SAP #1984787 relative à SUSE Linux Enterprise Server 12 : notes d’installation](https://launchpad.support.sap.com/#/notes/1984787).
- [Note de support SAP #171356 relative aux logiciels SAP sur Linux : informations générales](https://launchpad.support.sap.com/#/notes/1984787).
- [Note de support SAP #1391070 relative aux solutions Linux UUID](https://launchpad.support.sap.com/#/notes/1391070).

[Red Hat Enterprise Linux pour SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) est une autre offre permettant l’exécution de SAP HANA sur les grandes instances HANA. RHEL 6.7 et 7.2 sont disponibles. 

Autres liens SAP utiles relatifs à Red Hat :
- [Site de SAP HANA sur Red Hat Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

SAP tooimplementing applicable de prise en charge des Notes SAP HANA sur Red Hat :

- [Note de support SAP #2009879 relative aux instructions SAP HANA pour les systèmes d’exploitation Red Hat Enterprise Linux (RHEL)](https://launchpad.support.sap.com/#/notes/2009879/E).
- [Note de support SAP #2292690 relative à SAP HANA DB : paramètres de système d’exploitation recommandés pour RHEL 7](https://launchpad.support.sap.com/#/notes/2292690).
- [Note de support SAP #2247020 relative à SAP HANA DB : paramètres de système d’exploitation recommandés pour RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020).
- [Note de support SAP #1391070 relative aux solutions Linux UUID](https://launchpad.support.sap.com/#/notes/1391070).
- [Note de support SAP #2228351 relative à Linux : SAP HANA Database SPS 11 révision 110 (ou plus) sur RHEL 6 ou SLES 11](https://launchpad.support.sap.com/#/notes/2228351).
- [Note de support SAP #2397039 relative à la FAQ : SAP sur RHEL](https://launchpad.support.sap.com/#/notes/2397039).
- [Note de support SAP #1496410 relative à Red Hat Enterprise Linux 6.x : installation et mise à niveau](https://launchpad.support.sap.com/#/notes/1496410).
- [Note de support SAP #2002167 relative à Red Hat Enterprise Linux 7.x : installation et mise à niveau](https://launchpad.support.sap.com/#/notes/2002167).

## <a name="time-synchronization"></a>Synchronisation temporelle

Applications SAP repose sur hello architecture de SAP NetWeaver sont sensibles sur les différences de temps pour les différents composants qui composent hello hello système SAP. ABAP SAP court vide avec le titre d’erreur hello de ZDATE\_grande\_temps\_DIFF sont probablement familier, que ces images courts apparaissent lorsque hello heure système sur différents serveurs ou ordinateurs virtuels est trop éloignées dérive.

Pour SAP HANA sur Azure (Instances de grande taille), la synchronisation de l’heure dans Azure ne &#39; t appliquer toohello les unités de calcul dans les tampons de grande Instance hello. Cette synchronisation ne concerne pas les applications SAP qui s’exécutent sur des machines virtuelles Azure natives, car Azure garantit la bonne synchronisation de l’heure des systèmes. Par conséquent, les instances en cours d’exécution sur les Instances de grande taille HANA de base de données une fois serveur doit être configuré qui peut être utilisé par les serveurs d’applications SAP s’exécutant sur des machines virtuelles Azure et hello SAP HANA. infrastructure de stockage Hello dans les tampons de grande Instance est l’heure de synchronisation avec les serveurs NTP.

## <a name="setting-up-smt-server-for-suse-linux"></a>Configuration de serveur SMT pour SUSE Linux
Des Instances SAP HANA volumineux n’avez pas une connexion directe toohello Internet. Par conséquent, il n’est pas un processus simple de tooregister comme unités avec le fournisseur du système d’exploitation hello et toodownload et appliquer des correctifs. Dans les cas de hello de SUSE Linux, une solution peut être tooset d’un serveur SMT dans une machine virtuelle Azure. Alors que hello machine virtuelle Azure doit toobe hébergé dans un réseau virtuel Azure, qui est connecté toohello HANA grande Instance. Avec cet un serveur SMT, unité d’Instance est importante HANA hello peut inscrire et télécharger des correctifs. 

SUSE fournit un guide plus étoffé sur son [outil de gestion des abonnement pour SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Comme condition préalable pour l’installation de hello d’un serveur SMT qui remplit la tâche hello pour HANA grande Instance, vous devez :

- Un réseau virtuel Azure qui est connecté toohello circuit de HANA grande Instance ER.
- un compte SUSE associé à une organisation, Alors que l’organisation de hello doivent toohave certains abonnement SUSE valide.

### <a name="installation-of-smt-server-on-azure-vm"></a>Installation du serveur SMT sur une machine virtuelle Azure

Dans cette étape, vous installez serveur SMT de hello dans une machine virtuelle Azure. première mesure de Hello est toolog dans toohello [clientèle SUSE](https://scc.suse.com/)

Comme vous êtes connecté, accédez tooOrganization--> informations d’identification de l’organisation. Dans cette section, vous devez rechercher hello des informations d’identification nécessaire tooset serveur SMT de hello.

troisième étape de Hello est tooinstall une machine virtuelle Linux de SUSE Bonjour réseau virtuel Azure. toodeploy hello machine virtuelle, prenez une image de la galerie de SLES 12 SP2 de Azure. Dans le processus de déploiement hello, ne définissez pas un nom DNS et n’utilisent pas d’adresses IP statiques comme indiqué dans cette capture d’écran

![Déploiement de machine virtuelle pour le serveur SMT](./media/hana-installation/image3_vm_deployment.png)

Hello machine virtuelle déployée a une machine virtuelle plus petite et a obtenu l’adresse IP interne hello Bonjour réseau virtuel de Azure de 10.34.1.4. Nom de machine virtuelle de hello était smtserver. Après l’installation de hello, hello connectivité toohello HANA grande instance unité (s) a été activé. Dépend de la façon dont vous avez organisé la résolution de noms vous devrez peut-être résolution tooconfigure d’unités de HANA grande Instance hello etc./hôtes Hello machine virtuelle Azure. Ajouter une machine virtuelle qui est en train de toobe utilisé des correctifs de hello toohold de toohello disque supplémentaire. disque de démarrage Hello lui-même peut être trop petite. Dans les cas de hello présentés ici, disque de hello a été monté trop/srv/www/htdocs comme indiqué dans hello suivant capture d’écran. Un disque de 100 Go devrait suffire.

![Déploiement de machine virtuelle pour le serveur SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Se connecter ou les unités toohello HANA grande Instance, à conserver/etc/hosts et vérifier si vous pouvez atteindre hello machine virtuelle Azure qui est supposé server SMT hello toorun réseau hello.

Une fois cette vérification est effectuée avec succès, vous devez toolog dans toohello machine virtuelle Azure qui doit s’exécuter serveur SMT de hello. Si vous utilisez toolog putty dans toohello machine virtuelle, vous devez tooexecute cette séquence de commandes dans la fenêtre d’interpréteur de commandes :

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

Après avoir exécuté ces commandes, redémarrez vos paramètres de hello tooactivate bash. Ensuite, démarrez YaST.

Dans YAST, accédez à tooSoftware Maintenance et recherchez smt. Sélectionnez smt, qui bascule automatiquement tooyast2-smt comme indiqué ci-dessous

![SMT dans YaST](./media/hana-installation/image5_smt_in_yast.PNG)


Accepter la sélection pour l’installation sur hello smtserver hello. Une fois installé, consultez configuration du serveur SMT toohello et entrez des informations d’identification d’organisation de hello de hello clientèle SUSE vous extrait précédemment. Hello URL du serveur SMT aussi entrer votre nom d’hôte de la machine virtuelle Azure. Dans cette démonstration, il a été https://smtserver tel qu’affiché dans le graphique suivant de hello.

![Configuration du serveur SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Étape suivante, vous devez tootest si hello connexion toohello SUSE client Center fonctionne. Comme le hello suivant des graphiques, dans le cas de démonstration hello, il n’a fonctionné.

![Test de connexion tooSUSE clientèle](./media/hana-installation/image7_test_connect.png)

Une fois hello SMT le programme d’installation démarre, vous devez tooprovide un mot de passe de base de données. S’agissant d’une nouvelle installation, vous devez toodefine ce mot de passe comme indiqué dans le graphique suivant de hello.

![Définir le mot de passe pour la base de données](./media/hana-installation/image8_define_db_passwd.PNG)

interaction suivante de Hello que vous avez est lorsqu’un certificat est créé. Passer par la boîte de dialogue hello, comme le montre l’illustration suivante et l’étape de hello doit continuer.

![Créer un certificat pour le serveur SMT](./media/hana-installation/image9_certificate_creation.PNG)

Il peut y avoir quelques minutes passées à l’étape de hello de « Vérification de la synchronisation exécuter » à fin hello de configuration de hello. Après l’installation de hello et la configuration de serveur SMT de hello, vous devez rechercher le référentiel de répertoire hello sous hello montage point /srv/www/htdocs/plus des sous-répertoires dans le référentiel. 

Redémarrez le serveur SMT hello et ses services associés avec ces commandes.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Télécharger des packages sur le serveur SMT

Une fois toutes les hello redémarrage des services, sélectionnez hello packages appropriés dans la gestion de SMT à l’aide de Yast. sélection du package Hello dépend sur l’image de système d’exploitation hello du serveur d’Instance est importante HANA hello et non hello SLES libérer ou version de hello machine virtuelle en cours d’exécution hello SMT server. Vous trouverez ci-dessous un exemple d’écran de sélection hello.

![Sélectionner des packages](./media/hana-installation/image10_select_packages.PNG)

Une fois que vous avez terminé avec la sélection du package hello, vous devez la copie initiale de toostart hello du serveur de SMT hello sélectionnez packages toohello que vous configurez. Cette copie est déclenchée dans le shell de hello à l’aide de hello commande smt miroir comme indiqué ci-dessous


![Télécharger les packages tooSMT serveur](./media/hana-installation/image11_download_packages.PNG)

Comme ci-dessus, les packages hello doivent obtenir copiés dans les répertoires de hello créés sous hello montage point /srv/www/htdocs. Ce processus peut prendre un certain temps. Dépend du nombre de packages vous sélectionnez, elle peut prendre tooone heure ou plus.
Comme la fin de ce processus, vous devez le programme d’installation de toomove toohello SMT client. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Configuration du client SMT hello sur des unités de l’Instance est importante HANA

Dans ce cas, Hello clients sont unités d’Instance est importante HANA hello. installation du serveur SMT Hello copiées hello script clientSetup4SMT.sh hello machine virtuelle Azure. Copiez ce script sur toohello unité HANA grande Instance tooconnect tooyour SMT serveur. Démarrer le script de hello avec l’option -h de hello et attribuez-lui comme paramètre de nom de votre serveur SMT hello. Dans ce exemple, il s’agit de smtserver.

![Configurer un client SMT](./media/hana-installation/image12_configure_client.PNG)

Il peut y avoir un scénario où hello chargement du certificat hello du serveur hello par client de hello a réussi, mais échec de l’inscription de hello comme indiqué ci-dessous.

![L’inscription du client échoue](./media/hana-installation/image13_registration_failed.PNG)

En cas d’échec de l’inscription de hello, lire ce [SUSE prend en charge le document](https://www.suse.com/de-de/support/kb/doc/?id=7006024) et suivez les étapes de hello y.

> [!IMPORTANT] 
> En tant que nom de serveur, vous devez nom de hello tooprovide Hello machine virtuelle, dans ce cas smtserver, sans le nom de domaine complet de hello. Simplement hello VM nom fonctionne. 

Une fois ces étapes ont été exécutées, vous devez hello tooexecute commande suivante sur l’unité d’Instance est importante HANA hello

```
SUSEConnect –cleanup
```

> [!Note] 
> Dans nos tests nous avons toujours eu toowait quelques minutes après cette étape. Hello clientSetup4SMT.sh de l’exécution immédiate, après avoir hello mesures correctives sont décrits dans hello l’article SUSE, s’est terminée avec des messages que certificat hello n’est pas encore être valid. Une attente de 5 à 10 minutes, puis l’exécution de clientSetup4SMT.sh a abouti à une configuration réussie du client.

Si vous avez rencontré le problème hello que vous avez besoin en suivant les étapes de l’article de hello SUSE hello de toofix, vous devez à nouveau clientSetup4SMT.sh toorestart sur l’unité d’Instance est importante HANA hello. L’opération devrait à présent aboutir correctement, comme indiqué ci-dessous.

![Inscription du client réussie](./media/hana-installation/image14_finish_client_config.PNG)

Cette étape, vous avez configuré client SMT hello hello HANA grande Instance unité tooconnect sur le serveur SMT de hello que vous avez installé Bonjour Azure VM. Vous pouvez maintenant prendre « zypper des » ou les correctifs de tooinstall du système d’exploitation « zypper dans » Instances de grande taille tooHANA ou installer des packages supplémentaires. Il est entendu que vous pouvez obtenir uniquement les correctifs que vous avez téléchargé avant sur le serveur SMT de hello.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Exemple d’installation de SAP HANA sur des grandes instances HANA
Cette section illustre comment tooinstall SAP HANA sur une unité HANA grande Instance. état de démarrage Hello nous avons ressembler à :

- Vous avez fournies à Microsoft tous les toodeploy de données hello vous une Instance de grande taille SAP HANA.
- Vous avez reçu hello SAP HANA grande Instance à partir de Microsoft.
- Vous avez créé un réseau virtuel Azure qui n’est connecté tooyour sur site réseau.
- Connecté de circuit de ExpressRotue hello pour les Instances de grande taille HANA toohello même réseau virtuel Azure.
- Vous avez installé une machine virtuelle Azure que vous utilisez comme serveur intermédiaire pour les grandes instances HANA.
- Vérifiez que vous pouvez vous connecter de l’unité de hello saut boîte tooyour HANA grande Instance et vice versa vous effectué.
- Vous avez coché si tous hello les packages et correctifs sont installés.
- Vous lisez les notes SAP de hello et documentation concernant l’installation de HANA sur hello du système d’exploitation vous utilisez et vérifié que la mise en production HANA hello de choix est pris en charge sur la version de hello du système d’exploitation.

Ce qui est affiché dans les séquences suivants hello est téléchargement hello de hello HANA installation packages toohello saut zone machine virtuelle, dans ce cas en cours d’exécution sur un système d’exploitation Windows, copie hello d’unité d’Instance est importante HANA hello packages toohello et séquence hello du programme d’installation hello.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Téléchargement de bits d’installation hello SAP HANA
Étant donné que les unités d’Instance est importante HANA hello n’ont pas une connexion directe toohello internet, vous ne peut pas télécharger directement les packages d’installation hello de toohello SAP HANA grande Instance virtuelle. tooovercome hello manquant connectivité directe à internet, vous devez zone passer de hello. Vous téléchargez hello packages toohello saut zone machine virtuelle.

Dans l’ordre toodownload hello HANA les packages d’installation, vous avez besoin d’un utilisateur S SAP ou autre utilisateur, ce qui permet de vous tooaccess hello SAP Marketplace. Une fois connecté, parcourez cette séquence d’écrans :

Accédez trop[SAP Service Marketplace](https://support.sap.com/en/index.html) > cliquez sur Télécharger le logiciel > Installations et mise à niveau > par un Index alphabétique > sous H – SAP HANA Platform Edition > SAP HANA plateforme Édition 2.0 > Installation > hello de téléchargement fichiers suivants

![Télécharger les packages d’installation de HANA](./media/hana-installation/image16_download_hana.PNG)

Dans les cas de démonstration hello, nous avons téléchargé les packages d’installation SAP HANA 2.0. Sous hello saut Azure VM, vous développez les archives à extraction automatique hello dans l’annuaire hello comme indiqué ci-dessous.

![Extraire les packages d’installation de HANA](./media/hana-installation/image17_extract_hana.PNG)

Que les archives hello sont extraits, copiez directory hello créée par extraction de hello, dans les cas de hello ci-dessus 51052030, toohello une unité instance HANA volumineux en volume de /hana/shared hello dans un répertoire que vous avez créé.

> [!Important]
> Ne pas copier des packages d’installation hello dans la racine de hello ou numéro d’unité logique de démarrage depuis et l’espace limité doit toobe utilisé par d’autres processus.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Installation de SAP HANA sur l’unité d’Instance est importante HANA hello
Dans l’ordre tooinstall SAP HANA, vous devez toolog dans en tant qu’utilisateur racine. Racine seulement possède suffisamment tooinstall autorisations SAP HANA.
Hello première chose toodo est autorisations tooset répertoire hello copiée dans hana/partagé. autorisations de Hello doivent tooset comme

```
chmod –R 744 <Installation bits folder>
```

Si vous souhaitez tooinstall SAP HANA à l’aide de hello graphique le programme d’installation, hello gtk2 package besoins toobe installé sur les Instances de grande taille HANA hello. Vérifier si elle est installée avec la commande hello

```
rpm –qa | grep gtk2
```

Dans d’autres étapes, nous sommes montrant le programme d’installation de SAP HANA hello avec interface utilisateur graphique de hello. Étape suivante, aller dans le répertoire d’installation hello et accédez au sous-répertoire de hello HDB_LCM_LINUX_X86_64. Démarrer

```
./hdblcmgui 
```
en dehors de ce répertoire. Maintenant vous êtes obtention guidé par une séquence d’écrans où vous avez besoin des données de salutation tooprovide pour l’installation de hello. Dans les cas de hello présentés ici, nous allons l’installation de serveur de base de données SAP HANA hello et les composants du client SAP HANA hello. Par conséquent, notre sélection est « SAP HANA Database » (Base de données SAP HANA), comme illustré ci-dessous.

![Sélectionner HANA dans l’installation](./media/hana-installation/image18_hana_selection.PNG)

Dans l’écran suivant de hello, vous choisissez option de hello 'Installer le nouveau système'

![Sélectionner une nouvelle installation de HANA](./media/hana-installation/image19_select_new.PNG)

Après cette étape, vous devez tooselect entre plusieurs composants supplémentaires qui peuvent être installées en outre serveur de base de données SAP HANA toohello.

![Sélectionner des composants supplémentaires HANA](./media/hana-installation/image20_select_components.PNG)

Fins hello de cette documentation, nous avons choisi hello SAP HANA Client et hello SAP HANA Studio. Nous avons également installé une instance de montée en puissance parallèle. dans l’écran suivant de hello, vous devez donc toochoose 'Hôte unique System' 

![Sélectionner un installation avec montée en puissance parallèle](./media/hana-installation/image21_single_host.PNG)

Dans l’écran suivant de hello, vous devez tooprovide des données

![Fournir le SID de SAP HANA](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> En tant qu’ID de système HANA (SID), vous devez tooprovide hello même SID, que vous avez fourni Microsoft lors de la commande de déploiement d’Instance est importante HANA hello. Choix d’un SID différent accélère l’installation de hello échouer en raison de problèmes d’autorisation tooaccess sur des volumes différents hello

Répertoire d’installation vous utilisez Active de /hana/shared hello. Dans l’étape suivante de hello, vous devez les emplacements de hello tooprovide hello HANA fichiers de données et les fichiers journaux hello HANA


![Fournir l’emplacement du journal de HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Vous devez définir que les données et fichiers journaux hello volumes fournie déjà avec les points de montage hello contenant hello SID que vous avez choisi dans la sélection de l’écran hello avant cet écran. Si le SID de hello incompatible avec hello un écran hello avant, vous avez tapé, revenir en arrière et ajuster hello SID toohello valeur vous sur les points de montage hello.

Dans l’étape suivante de hello, passez en revue le nom d’hôte hello et finalement la corriger. 

![Réviser le nom d’hôte](./media/hana-installation/image24_review_host_name.PNG)

Dans l’étape suivante de hello, vous devez également les données tooretrieve tooMicrosoft attribué lors de la commande de déploiement d’Instance est importante HANA hello. 

![Fournir l’UID et le GID de l’utilisateur système](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Vous devez tooprovide hello même ID d’utilisateur système et ID de groupe d’utilisateurs comme vous avez fourni Microsoft comme ordre de déploiement hello. Si vous ne parvenez pas toogive hello très mêmes ID, installation Bonjour de SAP HANA sur l’unité d’Instance est importante HANA hello échoue.

Dans les deux écrans hello, qui nous montrons pas dans cette documentation, vous devez mot de passe tooprovide hello pour l’utilisateur du système de base de données SAP HANA hello hello mot de passe pour hello sapadm, qui est utilisé pour hello l’Agent hôte SAP qui sont installées dans le cadre de hello instance de base de données SAP HANA Hello.

Après avoir défini un mot de passe hello, un écran de confirmation s’affiche. Vérifiez toutes les données hello répertoriés et poursuivre l’installation de hello. Atteindre un écran de progression documents hello la progression de l’installation, comme un hello ci-dessous

![Vérifier la progression de l’installation](./media/hana-installation/image27_show_progress.PNG)

Comme hello installation terminée, vous devez une image comme hello suivant un

![L’installation est terminée](./media/hana-installation/image28_install_finished.PNG)

À ce stade, instance de SAP HANA hello doit être opérationnel et prêt pour l’utilisation. Vous devez être en mesure de tooconnect des tooit à partir de SAP HANA Studio. Assurez-vous également que vous recherchez les correctifs les plus récents de SAP HANA hello et appliquez ces correctifs.
























































 







 




