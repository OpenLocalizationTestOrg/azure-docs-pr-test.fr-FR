---
title: solutions aaaOracle sur Microsoft Azure | Documents Microsoft
description: "Découvrez les configurations prises en charge et les limitations des solutions Oracle sur Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Solutions Oracle et leur déploiement sur Microsoft Azure
Cet article traite des informations requise toosuccesfully déployer différentes solutions Oracle sur Microsoft Azure. Ces solutions sont basées sur les images de Machine virtuelle publiées par Oracle Bonjour Azure Marketplace. tooget une liste d’images actuellement disponibles, exécutez hello de commande suivante :
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
À compter de la liste de hello 6-16-2017 d’images sont les suivants de hello :
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Ces images sont considérées comme de type BYOL (apportez votre propre licence). Par conséquent, vous serez facturé uniquement pour les frais de calcul, le stockage et de mise en réseau induits par l’exécution d’une machine virtuelle.  Il est supposé vous êtes le logiciel Oracle toouse correctement sous licence et que vous disposez d’un contrat de support actuel en place avec Oracle. Oracle a la garantie mobilité de licence à partir de local tooAzure. Consultez hello publié [Oracle et Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Remarque Pour plus d’informations sur la mobilité de licence. 

Personnes peuvent également choisir toobase leurs solutions sur Créer entièrement dans Azure ou de télécharger des images personnalisées à partir de leurs environnements locaux sur des images personnalisées.

## <a name="support-for-jd-edwards"></a>Prise en charge de JD Edwards
En fonction de note de prise en charge tooOracle [Doc ID 2178595.1](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne version 9.2 et versions ultérieures sont pris en charge sur **offre de cloud de n’importe quel public** qui répond à leurs propres `Minimum Technical Requirements` (MTR).  Vous devez toocreate des images personnalisées qui répondent à leurs spécifications MTR pour la compatibilité des applications du système d’exploitation et logiciels. 

## <a name="oracle-database-virtual-machine-images"></a>Images de machines virtuelles Oracle Database
Oracle prend en charge l’exécution des éditions Standard d’Oracle DB 12.1 dans Azure sur des images de machine virtuelle basées sur Oracle Linux.  Pour des performances optimales hello pour les charges de production de la base de données Oracle sur Azure, image de machine virtuelle que tooproperly taille hello et les disques gérés qui sont sauvegardés par stockage Premium. Pour plus d’informations sur comment tooquickly obtenir une base de données Oracle en cours d’exécution dans Azure à l’aide de hello Oracle publié l’image de machine virtuelle, [recommencez la procédure de démarrage rapide de base de données Oracle hello](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Options de configuration des disques connectés

Disques attachés s’appuient sur hello service de stockage d’objets Blob Azure. En théorie, chaque disque standard peut proposer un maximum de 500 entrées/sorties par seconde (IOPS). Notre offre premium est recommandée pour les charges de travail de base de données hautes performances et pouvez obtenir des e/s de too5000 par disque. Vous pouvez utiliser un seul disque si qui répond à vos performances doit - vous pouvez améliorer les performances IOPS effectives hello si vous utilisez plusieurs disques attachés, répartir les données de la base de données entre eux et ensuite utilisez Oracle Automatic Storage Management (ASM). Pour plus d’informations spécifiques d’Oracle ASM, voir [vue d’ensemble du stockage automatique Oracle](http://www.oracle.com/technetwork/database/index-100339.html). Pour obtenir un exemple de tooinstall et configurer Oracle ASM sur une machine virtuelle de Azure Linux - vous pouvez essayer de hello [installation et configuration d’Oracle Automated Storage Management](configure-oracle-asm.md) didacticiel.

### <a name="oracle-realtime-application-cluster-rac"></a>Cluster d’application en temps réel (RAC) Oracle
Oracle RAC est Échec de hello toomitigate conçue d’un seul nœud dans une configuration de cluster à plusieurs nœuds locaux.  Il s’appuie sur deux technologies locales qui ne sont pas des environnements de cloud public à l’échelle toohyper natif : multidiffusion réseau et disque partagé. Il existe des solutions de tiers créées par des sociétés [tels que FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) qui émuler ces technologies, si vous avez besoin de toodeploy Oracle RAC dans Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Remarques relatives à la haute disponibilité et à la récupération d’urgence
Lorsque vous utilisez des bases de données Oracle dans Azure, vous êtes chargé d’implémenter un tooavoid de solution haute disponibilité et de reprise après sinistre récupération tout temps d’arrêt. 

Pour assurer la haute disponibilité et la récupération d’urgence pour Oracle Database Enterprise Edition (sans RAC) sur Microsoft Azure, vous pouvez utiliser [Data Guard, Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) ou [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), en plaçant deux bases de données sur deux machines virtuelles distinctes. Les deux ordinateurs virtuels doivent être dans hello même [réseau virtuel](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure, ils peuvent les uns aux autres via l’adresse IP persistante privée hello.  En outre, nous vous recommandons de placer des ordinateurs virtuels de hello Bonjour à haute disponibilité même tooallow tooplace Azure distinct les domaines d’erreur et domaines de mise à niveau.  Si vous souhaitez que toohave géo-redondance - vous pouvez avoir ces deux bases de données répliquer entre deux régions différentes et connecter les deux instances de hello avec une passerelle VPN.

Nous avons un didacticiel «[implémenter Oracle DataGuard sur Azure](configure-oracle-dataguard.md)» qui vous guide à travers tootrial de procédure de configuration de base hello cela sur Azure.  

Grâce à Oracle Data Guard, vous pouvez assurer la haute disponibilité du système en plaçant la base de données primaire sur une machine virtuelle et une base de données secondaire (de veille) sur une autre, et en configurant une réplication monodirectionnelle entre ces bases de données. résultat de Hello est accès en lecture toohello copie hello. Avec Oracle GoldenGate, vous pouvez configurer une réplication bidirectionnelle entre deux bases de données hello. toolearn tooset configuration d’une solution de haute disponibilité pour vos bases de données à l’aide de ces outils, voir [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) et [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) documentation sur le site Web de Oracle hello. Si vous avez besoin en lecture-écriture copie de toohello d’accès de base de données hello, vous pouvez utiliser [Oracle Active Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Nous avons un didacticiel «[implémenter Oracle GoldenGate sur Azure](configure-oracle-golden-gate.md)» qui vous guide à travers hello seup base procédure tootrial cela sur Azure.

Bien qu’ils aient une solution haute disponibilité et récupération d’urgence de mise en œuvre dans Azure, vous devez tooensure que vous avez une stratégie de sauvegarde dans un endroit toorestore votre base de données.  Nous avons un didacticiel [sauvegarde et restauration d’une base de données Oracle](oracle-backup-recovery.md) vous guide tout au long de procédure de base hello pour l’établissement d’une sauvegarde consistant.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Images de machines virtuelles Oracle WebLogic Server
* **Le clustering est pris en charge sur la version Enterprise Edition uniquement.** Vous sont concédés sous licence toouse WebLogic clustering uniquement lorsque vous utilisez hello WebLogic Server, Enterprise Edition. N’utilisez pas le clustering avec WebLogic Server Standard Edition.
* **La multidiffusion UDP n’est pas gérée.** Azure prend en charge la monodiffusion UDP, mais ni la diffusion, ni la multidiffusion. WebLogic Server est en mesure de toorely sur les capacités de monodiffusion UDP d’Azure. Pour mieux les résultats monodiffusion UDP, nous recommandons que la taille du cluster hello WebLogic reste statique, ou être conservé avec pas plus de 10 serveurs gérés inclus dans le cluster de hello.
* **WebLogic Server attend hello toobe de ports publics et privés identiques pour T3 accéder (par exemple, lors de l’utilisation d’Enterprise JavaBeans).** Imaginez un scénario à plusieurs niveaux, dans lequel une application de couche de service (EJB) est en cours d’exécution sur un cluster WebLogic Server comprenant deux serveurs gérés ou plus, au sein d’un réseau virtuel nommé **SLWLS**. niveau de client Hello se trouve dans un autre sous-réseau Bonjour même réseau virtuel, un simple programme Java toocall EJB dans la couche de service hello lors de la tentative en cours d’exécution. Puisqu’il est la couche de service nécessaires tooload solde hello, un point de terminaison public avec équilibrage de charge doit toobe créé pour les Machines virtuelles de hello Bonjour cluster WebLogic Server. Si le port privé hello que vous spécifiez est différente de port public de hello (par exemple, 7006 : 7008), une erreur telle que suivante de hello se produit :

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Il s’agit, car pour tout accès T3 à distance, WebLogic Server attend un port d’équilibrage de charge hello et hello géré WebLogic server port toobe hello identiques. Bonjour au-dessus de cas, hello client pour accéder au port 7006 (port d’équilibrage de charge hello) et les serveurs gérés hello écoute 7008 (port privé de hello). Cette restriction porte uniquement sur l’accès T3, et non sur le protocole HTTP.

   tooavoid ce problème, l’utiliser un des hello suivant des solutions de contournement :

  * Utilisez hello même privé et les numéros de port public pour la charge équilibrée des points de terminaison dedicated tooT3 accès.
  * Hello, suivant le paramètre de la machine virtuelle Java lors du démarrage de WebLogic Server sont les suivantes :

         -Dweblogic.rjvm.enableprotocolswitch=true

Pour plus d’informations, voir l’article **860340.1** à l'adresse <http://support.oracle.com>.

* **Limitations relatives à l’équilibrage de charge et au clustering dynamique.** Supposons que vous voulez toouse un cluster dynamique dans WebLogic Server et l’exposez via un seul, public avec équilibrage de charge point de terminaison dans Azure. Cela est possible tant que vous utilisez un numéro de port fixe pour chacune des hello (ne sont pas automatiquement assignés à partir d’une plage) des serveurs gérés et que vous ne démarrez pas plus de serveurs gérés qu’il ne sont administrateur de hello effectue le suivi des machines (autrement dit, pas plus d’un serveur géré par des pointeurs journalisation des accès utilisateur machine). Si votre configuration se traduit par des serveurs WebLogic en cours de démarrage à des ordinateurs virtuels (autrement dit, où plusieurs partage d’instances de WebLogic Server hello même machine virtuelle), il n’est pas possible pour plusieurs de ces instances de WebLogic Server serveurs toobind tooa est donné le numéro de port : hello d’autres utilisateurs sur cet ordinateur virtuel échoue.

   Sur hello autre part, si vous configurez hello admin server tooautomatically affecter des numéros de port unique tooits gérés des serveurs, l’équilibrage de charge n’est pas possible, car Azure ne prend pas en charge le mappage à partir d’un port public unique toomultiple les ports privés, comme ce serait requis pour cette configuration.
* **Exécution de plusieurs instances WebLogic sur une seule machine virtuelle.** En fonction des besoins de votre déploiement, vous pouvez envisager d’option hello de l’exécution de plusieurs instances de WebLogic Server sur hello même machine virtuelle, si la machine virtuelle de hello est suffisante. Par exemple, sur un ordinateur virtuel de taille moyenne, qui contient les deux cœurs, vous pouvez choisir toorun deux instances de WebLogic Server. Notez toutefois que nous recommandons quand même d’éviter d’introduire des points de défaillance uniques dans votre architecture, ce qui serait le cas de hello si vous avez utilisé qu’une seule machine virtuelle qui exécute plusieurs instances de WebLogic Server. L’utilisation d’un minimum de deux machines virtuelles peut s’avérer plus efficace ; chaque machine virtuelle peut alors exécuter plusieurs instances WebLogic Server. Chacune de ces instances de WebLogic Server pourrait toujours être partie hello même cluster. Notez, toutefois, il est actuellement pas possible toouse Azure tooload-solde de points de terminaison qui sont exposés par de tels déploiements WebLogic Server au sein de hello même ordinateur virtuel, car équilibrage de charge Azure requiert toobe d’équilibrage de la charge des serveurs hello réparti machines virtuelles uniques.

## <a name="oracle-jdk-virtual-machine-images"></a>Images de machine virtuelle JDK Oracle
* **Dernières mises à jour de JDK 6 et 7.** Bien que nous recommandions à l’aide de la version de hello dernière version publique et la prise en charge de Java (actuellement Java 8), Azure, JDK 6 et 7 images disponibles. Cela vise pour les applications héritées qui ne sont pas encore prêt toobe mis à niveau tooJDK 8. Bien que les mises à jour tooprevious JDK images peuvent ne plus être disponibles toohello grand public, donné hello Microsoft partenariat avec Oracle, hello JDK 6 et 7 images fournies par Azure sont conçu toocontain une mise à jour plus récente non public qui est normalement proposé par Oracle tooonly un groupe d’Oracle pris en charge par les clients. Nouvelles versions des images JDK hello sera disponibles au fil du temps avec les versions mises à jour de JDK 6 et 7.

   Hello JDK disponible dans cette JDK 6 et 7 images et machines virtuelles de hello et images dérivés, peuvent uniquement être utilisés dans Azure.
* **JDK 64 bits.** images de machine virtuelle Oracle WebLogic Server Hello et des images de machine virtuelle hello JDK Oracle fournies par Azure contiennent hello Édition 64 bits de Windows Server et hello JDK.

## <a name="next-steps"></a>Étapes suivantes
Vous avez maintenant une vue d’ensemble des Solutions Oracle actuelles sur Microsoft Azure. L’étape suivante est toogo et déployer votre première base de données Oracle sur Azure.
- Essayez de hello [créer une base de données Oracle sur Azure](oracle-database-quick-create.md) didacticiel tooget a démarré.
