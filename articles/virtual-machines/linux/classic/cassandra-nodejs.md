---
title: aaaRun Cassandra avec Linux sur Azure | Documents Microsoft
description: "Comment toorun un Cassandra de cluster sur Linux dans des Machines virtuelles Azure à partir d’une application Node.js"
services: virtual-machines-linux
documentationcenter: nodejs
author: tomarcher
manager: routlaw
editor: 
tags: azure-service-management
ms.assetid: 30de1f29-e97d-492f-ae34-41ec83488de0
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 381ca301bbe88d3740cf182f9c44fada5b9ba7cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-cassandra-with-linux-on-azure-and-accessing-it-from-nodejs"></a>Exécution de Cassandra avec Linux sur Azure et accès au cluster depuis Node.js
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Consultez des modèles Resource Manager pour [Datastax Enterprise](https://azure.microsoft.com/documentation/templates/datastax) et [Cluster Spark et Cassandra sur CentOS](https://azure.microsoft.com/documentation/templates/spark-and-cassandra-on-centos/).

## <a name="overview"></a>Vue d'ensemble
Microsoft Azure est une plateforme de cloud ouverte qui exécute des logiciels Microsoft et non-Microsoft tels que des systèmes d’exploitation, serveurs d’applications, intergiciels de messagerie, ainsi que des bases de données SQL et NoSQL à partir de modèles commerciaux et open source. La création de services résilients sur des clouds publics, y compris Azure, nécessite une planification soignée et une architecture délibérée pour les serveurs d'applications et les niveaux de stockage. L'architecture de stockage distribuée de Cassandra aide naturellement à créer des systèmes hautement disponibles qui offrent une tolérance de panne en cas de défaillance de cluster. Cassandra est une base de données NoSQL à l'échelle du cloud maintenue par Apache Software Foundation à l'adresse cassandra.apache.org ; Cassandra est écrit en Java et s'exécute donc sur Windows, ainsi que sur les plateformes Linux.

Hello de cet article concerne les déploiement de Cassandra tooshow sur Ubuntu sous la forme d’un cluster unique et plusieurs centre de données en exploitant des Machines virtuelles Microsoft Azure et des réseaux virtuels. Hello déploiement de cluster pour les charges de production optimisée est hors de portée de cet article car elle nécessite la configuration du nœud de disques multiples, toosupport hello de modélisation des données et conception de la topologie en anneau approprié nécessaire à la réplication, la cohérence des données, débit et exigences de haute disponibilité.

Cette prend l’article un tooshow approche fondamentaux les conséquences de la construction hello cluster de Cassandra comparées Docker, Chef ou Puppet, ce qui peut rendre hello déploiement de l’infrastructure beaucoup plus simple.  

## <a name="hello-deployment-models"></a>Hello modèles de déploiement
Mise en réseau de Microsoft Azure permet de déployer des clusters privés isolés, la sécurité du réseau de granularité fine tooattain restreint l’accès de hello qui peut être hello.  Étant donné que cet article est sur l’affichage de déploiement de Cassandra hello fondamentalement, nous nous concentrerons pas sur le niveau de cohérence hello et conception de stockage optimal hello pour le débit. Voici la liste hello de configuration réseau requise pour notre cluster hypothétique :

* Les systèmes externes ne peuvent pas accéder à la base de données Cassandra depuis Azure ou en dehors d'Azure
* Cluster de Cassandra a toobe derrière un équilibreur de charge pour le trafic thrift
* Déployez les nœuds Cassandra en deux groupes dans chaque centre de données pour améliorer la disponibilité du cluster
* Verrouiller les cluster hello ainsi qu’uniquement de la batterie de serveurs d’application a base de données access toohello directement
* Aucun point de terminaison de réseau public autre que SSH
* Chaque nœud Cassandra a besoin d'une adresse IP interne fixe

Cassandra peut être déployé tooa une seule région Azure ou des régions toomultiple selon la nature hello distribuée de charge de travail hello. Modèle de déploiement de plusieurs régions peut être optimisées tooserve les utilisateurs finaux proche tooa particulier geography via hello même infrastructure Cassandra. Nœud intégré réplication prend en charge du Cassandra de la synchronisation de hello de multimaître écrit provenant de plusieurs centres de données et présente une vue cohérente de hello données tooapplications. Déploiement de plusieurs régions peut également aider à atténuation des risques hello d’interruption de service Azure hello plus large. La topologie de réplication et de cohérence paramétrable de Cassandra permet de répondre à divers besoins des applications en matière d'objectif de point de récupération.

### <a name="single-region-deployment"></a>Déploiement dans une seule région
Nous allons commencer par un déploiement de la même région et à partir des retours récolte hello dans la création d’un modèle de plusieurs région. Réseau virtuel Windows Azure sera les sous-réseaux utilisés toocreate isolé afin que les exigences de sécurité réseau hello mentionnés ci-dessus peuvent être satisfaites.  Hello est décrite dans la création du déploiement de région de hello utilise Ubuntu 14.04 LTS et Cassandra 2.08 ; Toutefois, les processus hello peuvent facilement être adoptée toohello autres variantes de Linux. Hello Voici quelques-unes des caractéristiques du système de déploiement de région de hello hello.  

**Haute disponibilité :** hello Cassandra des nœuds dans la Figure 1 sont déployés de hello tootwo disponibilité définit afin que les nœuds de hello sont réparties entre plusieurs domaines d’erreur pour la haute disponibilité. Machines virtuelles annotées avec chaque groupe à haute disponibilité est too2 mappé les domaines d’erreur.  Microsoft Azure utilise hello concept de toomanage de domaine d’erreur non planifié vers le bas (par exemple, les pannes de matériel ou logiciel) temps concept hello du domaine de mise à niveau (par exemple, un hôte ou invité du système d’exploitation mise à jour corrective/mises à niveau, mises à niveau de l’application) permet de gérer planifiée temps d’arrêt. Consultez [la récupération d’urgence et haute disponibilité pour les Applications Azure](http://msdn.microsoft.com/library/dn251004.aspx) pour rôle hello de domaines d’erreur et de mise à niveau à la réalisation d’une haute disponibilité.

![Déploiement dans une seule région](./media/cassandra-nodejs/cassandra-linux1.png)

Figure 1 : Déploiement dans une seule région

Notez qu’au moment de hello de rédaction de cet article, Azure n’autorise pas mappage explicite de hello d’un groupe de machines virtuelles tooa domaine d’erreur spécifique ; Par conséquent, même avec le modèle de déploiement hello indiqué dans la Figure 1, il est statistiquement probable que tous les ordinateurs virtuels hello peut-être tootwo mappé les domaines d’erreur au lieu de quatre.

**L’équilibrage de la charge du trafic de Thrift :** bibliothèques du client à l’intérieur du serveur web de hello Thrift connectent toohello cluster via un équilibreur de charge interne. Cette procédure est hello de l’ajout du sous-réseau de hello charge interne équilibrage toohello « données » (voir Figure 1) dans le contexte de hello du service de cloud hello qui héberge hello Cassandra cluster. Une fois que l’équilibrage de charge interne hello est défini, chaque nœud nécessite toobe de point de terminaison à charge équilibrée hello ajoutés avec des annotations d’un jeu d’équilibrage de charge avec précédemment hello nom d’équilibrage de charge définis. Consultez [Équilibrage de la charge interne Azure ](../../../load-balancer/load-balancer-internal-overview.md)pour plus de détails.

**Valeurs de départ de cluster :** il est important de tooselect hello la plupart des nœuds hautement disponible pour les valeurs initiales comme hello nouveaux nœuds communiqueront avec topologie de semences nœuds toodiscover hello du cluster de hello. Un seul nœud à partir de chaque groupe à haute disponibilité est désigné comme valeur initiale nœuds tooavoid point de défaillance unique.

**Facteur de réplication et le niveau de cohérence :** génération de haute disponibilité et les données durabilité de Cassandra se caractérise par hello facteur de réplication (RF - nombre de copies de chaque ligne stockée dans le cluster de hello) et le niveau de cohérence (nombre de réplicas toobe lus/écrits avant de retourner l’appelant de toohello résultat hello). Facteur de réplication est spécifié pendant hello création de l’espace de clés (similaire tooa base de données relationnelle), tandis que le niveau de cohérence hello est spécifié lors de l’exécution de requête CRUD hello. Consultez la documentation Cassandra sur [configuration pour la cohérence](http://www.datastax.com/documentation/cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) pour les détails de la cohérence et la formule hello pour le calcul du quorum.

Cassandra prend en charge deux types de modèles de l’intégrité des données, la cohérence et la cohérence éventuelle ; Hello facteur de réplication et niveau de cohérence ensemble déterminent si les données de salutation sera cohérentes dès qu’une opération d’écriture est terminée ou qu’il sera finalement cohérente. Par exemple, en spécifiant QUORUM car hello que niveau de cohérence sera toujours garantit la cohérence de données lors de n’importe quel niveau de cohérence, en dessous du nombre de hello de toobe réplicas écrite sous la forme tooattain nécessaire QUORUM (par exemple, un) entraîne finalement cohérente des données.

cluster à 8 nœuds Hello illustrée ci-dessus, avec un facteur de réplication de 3 et QUORUM (2 nœuds sont lues ou écrites par souci de cohérence) au niveau de cohérence de lecture/écriture, peuvent survivre hello théorique une perte d’à hello 1 nœud par la réplication de groupe avant le démarrage de l’application hello détection d’échec de hello. Cela suppose que tous les espaces de clé hello ont bien équilibrés des demandes de lecture/écriture.  Hello Voici les paramètres hello que nous allons utiliser pour le cluster de hello déployé :

Configuration de cluster Cassandra à une seule région :

| Paramètre de cluster | Valeur | Remarques |
| --- | --- | --- |
| Nombre de nœuds (N) |8 |Nombre total de nœuds de cluster de hello |
| Facteur de réplication (RF) |3 |Nombre de réplicas d'une ligne donnée |
| Niveau de cohérence (écriture) |QUORUM[(RF/2) +1) = 2] hello result Hello formule est arrondie vers le bas |Écrit la plupart des 2 réplicas à hello avant hello est envoyée toohello appelant ; réplica 3e est écrit de manière cohérente. |
| Niveau de cohérence (lecture) |QUORUM [(RF/2) + 1 = 2] résultat hello de formule de hello est arrondi vers le bas |Lit 2 réplicas avant l’envoi de l’appelant toohello de réponse. |
| Stratégie de réplication |NetworkTopologyStrategy voir [Réplication des données](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) dans la documentation de Cassandra pour plus d’informations |Comprend la topologie de déploiement hello et place les réplicas sur les nœuds afin que tous les réplicas hello ne se retrouver sur hello même rack |
| Snitch |GossipingPropertyFileSnitch voir [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) dans la documentation de Cassandra pour plus d’informations |NetworkTopologyStrategy utilise un concept de topologie de snitch toounderstand hello. GossipingPropertyFileSnitch donne un meilleur contrôle lors du mappage de chaque centre de toodata de nœud et le rack. cluster de Hello utilise ensuite les discussions toopropagate ces informations. Cela est beaucoup plus simple dans dynamique tooPropertyFileSnitch relatif de la configuration IP |

**Considérations relatives à Microsoft Azure pour le cluster Cassandra :** les fonctionnalités de machines virtuelles Microsoft Azure utilisent le stockage d’objets blob Azure pour la persistance des disques ; le stockage Azure enregistre trois réplicas de chaque disque pour une durabilité élevée. Cela signifie que chaque ligne de données insérées dans une table Cassandra est déjà stocké dans 3 réplicas et par conséquent, la cohérence des données est déjà pris en charge même si hello facteur de réplication (RF) est 1. Hello principal problème avec le facteur de réplication en cours de 1 est qu’application hello connaissent des interruptions de service même si un seul nœud Cassandra échoue. Toutefois, si un nœud est arrêté pour les problèmes hello (matérielles, défaillances du système) reconnus par le contrôleur de structure Azure, il configure un nouveau nœud dans son emplacement à l’aide de hello même les disques de stockage. Configuration d’un nouveau nœud tooreplace hello ancien une peut prendre quelques minutes.  De même pour les activités de maintenance planifiée tels que les modifications du système d’exploitation invité, Cassandra met à niveau et modification de l’application contrôleur de structure Azure effectue des mises à niveau des nœuds de hello de propagées dans le cluster de hello.  Mise à niveau propagée également peut prendre quelques nœuds à la fois et par conséquent, cluster de hello peut rencontrer des interruption de courte durée pour plusieurs partitions. Toutefois, les données de hello ne seront pas perdues en raison de la redondance de stockage Azure toohello intégrée.  

Pour les systèmes déployés tooAzure ne nécessitant pas de haute disponibilité (par exemple, 99,9 environ qui est équivalent too8.76 heures/année ; consultez [haute disponibilité](http://en.wikipedia.org/wiki/High_availability) pour plus d’informations) vous pouvez être en mesure de toorun avec RF = 1 et le niveau de cohérence = 1.  Pour les applications aux exigences de haute disponibilité, RF = 3 et niveau de cohérence = QUORUM tolérée hello indisponibilité de l’un des nœuds hello des réplicas de hello. RF = 1 dans les déploiements traditionnels (par exemple, local) ne peut pas être utilisé en raison de la perte de données toohello dues à des problèmes tels que des défaillances de disque.   

## <a name="multi-region-deployment"></a>Déploiement dans plusieurs régions
Réplication center-bases de données et le modèle de cohérence décrites ci-dessus permettent de déploiement de plusieurs régions hello en dehors de la zone de hello sans hello du Cassandra besoin pour les outils externes. Cela est très différente de bases de données relationnelles traditionnels hello où le programme d’installation de hello pour la mise en miroir de base de données pour les écritures multimaîtres peut être complexe. Cassandra dans une région multi configurée peut aider les scénarios d’utilisation de hello notamment hello suivantes :

**Déploiement basé sur la proximité :** applications mutualisées, avec le mappage clair d’utilisateurs du client-à-région, peut être bénéficié par temps de latence faible du cluster hello plusieurs régions. Par exemple un apprentissage de gestion des systèmes pour l’établissement d’enseignement peuvent déployer un cluster de distribuée dans est des États-Unis et ouest des États-Unis régions tooserve hello respectifs campus pour transactionnelle, ainsi que d’analytique. les données de salutation peuvent être cohérentes localement à hello temps lectures et écritures et peuvent être cohérentes entre les deux régions hello. Il existe d’autres exemples, tels que la distribution multimédia ou le commerce électronique, et tout ce qui répond aux demandes des bases d’utilisateurs concentrées géographiquement constitue un bon cas d’utilisation pour ce modèle de déploiement.

**Haute disponibilité :** la redondance est un facteur clé dans l’obtention de la haute disponibilité des logiciels et du matériel ; pour plus d’informations, consultez Création de systèmes de cloud fiables sur Microsoft Azure. Sur Microsoft Azure, hello seule méthode fiable d’assurer la redondance est en déployant un cluster de plusieurs région. Applications peuvent être déployées en mode actif / actif ou actif / passif, et si l’une des régions de hello est arrêté, Azure Traffic Manager peut rediriger la région active toohello de trafic.  Avec le déploiement de région de hello, si la disponibilité de hello est 99,9, un déploiement de deux régions peut atteindre un disponibilité de 99,9999 calculée par la formule de hello : (1-(1-0.999) * (1-0,999)) * 100) ; hello au-dessus de papier pour plus d’informations, consultez.

**Récupération d’urgence :** un cluster Cassandra à plusieurs régions, conçu correctement, peut résister aux pannes catastrophiques d’un centre de données. Si une région est arrêté, les régions tooother hello application déployée peuvent démarrer desservant les utilisateurs finaux de hello. Comme les autres implémentations de continuité d’activité commerciale, application hello possède toobe à tolérance de perte de données résultant des données hello dans pipeline asynchrone de hello. Toutefois, Cassandra permet de récupération de hello plus intensifs à heure hello effectuée par le processus de récupération de base de données traditionnelle. Figure 2 montre un modèle de déploiement de plusieurs régions classique hello avec huit nœuds dans chaque région. Les deux régions sont des images de mise en miroir de l’autre pour hello même de symétrie ; conceptions de monde réel dépendent du type de charge de travail hello (par exemple, transactionnelle ou d’analyse), RPO, RTO, la cohérence des données et des exigences de disponibilité.

![déploiement dans plusieurs régions](./media/cassandra-nodejs/cassandra-linux2.png)

Figure 2 : Déploiement de Cassandra dans plusieurs régions

### <a name="network-integration"></a>Intégration réseau
Jeux d’ordinateurs virtuels, réseaux tooprivate déployé sur les deux régions communique avec d’autres à l’aide d’un tunnel VPN. tunnel VPN de Hello connecte deux passerelles logiciel mis en service pendant le processus de déploiement de réseau hello. Les deux régions ont une architecture réseau similaire en termes de sous-réseaux « web » et « données » ; Mise en réseau Azure permet de créer de hello des sous-réseaux si nécessaire et appliquer des ACL selon les besoins de sécurité réseau. Lors de la conception de topologie de cluster hello inter données center communication latence et hello impact économique de hello réseau trafic besoin toobe pris en compte.

### <a name="data-consistency-for-multi-data-center-deployment"></a>Cohérence des données pour le déploiement dans plusieurs centres de données
Distribué toobe du besoin de déploiements prenant en charge de l’impact de topologie de cluster hello sur le débit et la haute disponibilité. Hello RF et niveau de cohérence toobe besoin sélectionné de telle sorte que hello quorum ne dépend de la disponibilité hello de tous les centres de données hello.
Pour un système qui a besoin de cohérence élevée, un LOCAL_QUORUM pour le niveau de cohérence (pour les écritures et lectures) permet de garantir que hello local lectures et écritures sont satisfaites à partir de hello local nœuds tandis que les données sont répliquées de manière asynchrone les centres de données distants toohello.  Le tableau 2 récapitule la configuration hello détails pour le cluster de plusieurs régions hello décrites plus loin dans hello écrire des.

**Configuration de cluster Cassandra à deux régions**

| Paramètre de cluster | Valeur | Remarques |
| --- | --- | --- |
| Nombre de nœuds (N) |8 + 8 |Nombre total de nœuds de cluster de hello |
| Facteur de réplication (RF) |3 |Nombre de réplicas d'une ligne donnée |
| Niveau de cohérence (écriture) |LOCAL_QUORUM [(sum(RF)/2) +1) = 4] résultat hello de formule de hello est arrondi vers le bas |2 nœuds seront écrits toohello premier centre de données de façon synchrone ; Hello 2 des nœuds supplémentaires nécessaires pour le quorum seront écrit en mode asynchrone toohello 2e centre de données. |
| Niveau de cohérence (lecture) |LOCAL_QUORUM ((RF/2) + 1) = 2 résultat hello de formule de hello est arrondi vers le bas |Requêtes de lecture sont satisfaites à partir de la seule région ; 2 nœuds sont lues avant hello est envoyée arrière toohello client. |
| Stratégie de réplication |NetworkTopologyStrategy voir [Réplication des données](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureDataDistributeReplication_c.html) dans la documentation de Cassandra pour plus d’informations |Comprend la topologie de déploiement hello et place les réplicas sur les nœuds afin que tous les réplicas hello ne se retrouver sur hello même rack |
| Snitch |GossipingPropertyFileSnitch voir [Snitches](http://www.datastax.com/documentation/cassandra/2.0/cassandra/architecture/architectureSnitchesAbout_c.html) dans la documentation de Cassandra pour plus d’informations |NetworkTopologyStrategy utilise un concept de topologie de snitch toounderstand hello. GossipingPropertyFileSnitch donne un meilleur contrôle lors du mappage de chaque centre de toodata de nœud et le rack. cluster de Hello utilise ensuite les discussions toopropagate ces informations. Cela est beaucoup plus simple dans dynamique tooPropertyFileSnitch relatif de la configuration IP |

## <a name="hello-software-configuration"></a>Hello CONFIGURATION logicielle
Hello les versions logicielles suivantes est utilisée lors du déploiement de hello :

<table>
<tr><th>Logiciel</th><th>Source</th><th>Version</th></tr>
<tr><td>JRE    </td><td>[JRE 8](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) </td><td>8U5</td></tr>
<tr><td>JNA    </td><td>[JNA](https://github.com/twall/jna) </td><td> 3.2.7</td></tr>
<tr><td>Cassandra</td><td>[Apache Cassandra 2.0.8](http://www.apache.org/dist/cassandra/2.0.8/apache-cassandra-2.0.8-bin.tar.gz)</td><td> 2.0.8</td></tr>
<tr><td>Ubuntu    </td><td>[Microsoft Azure](https://azure.microsoft.com/) </td><td>14.04 LTS</td></tr>
</table>

Téléchargement de l’environnement JRE requérant acceptation manuelle de la licence d’Oracle, de déploiement de hello toosimplify tous hello bureau toohello de logiciels requis pour le téléchargement ultérieurement dans l’image de modèle d’Ubuntu hello que nous allons créer un cluster de toohello précurseur de téléchargement déploiement.

Téléchargez hello au-dessus de logiciel dans un répertoire de téléchargement connue (par exemple, %TEMP%/downloads sur Windows ou ~/Downloads sur la plupart des distributions Linux ou Mac) sur l’ordinateur local de hello.

### <a name="create-ubuntu-vm"></a>CRÉATION D’UNE MACHINE VIRTUELLE UBUNTU
Dans cette étape du processus de hello, nous allons créer Ubuntu image avec hello les logiciels requis afin que hello image peut être réutilisée pour la configuration de plusieurs nœuds Cassandra.  

#### <a name="step-1-generate-ssh-key-pair"></a>ÉTAPE 1 : Génération de la paire de clés SSH
Azure a besoin d’une clé publique PEM ou DER encodé à hello mise en service de temps de X509. Générer une paire de clés publique/privée à l’aide d’instructions hello situées à la tooUse SSH avec Linux sur Azure. Si vous planifiez toouse putty.exe sous la forme d’un client SSH sur Windows ou Linux, vous avez tooconvert hello PEM encodé format de tooPPK clé privée RSA à l’aide de puttygen.exe ; Vous trouverez des instructions correspondantes Hello Bonjour au-dessus de page web.

#### <a name="step-2-create-ubuntu-template-vm"></a>ÉTAPE 2 : Création du modèle de machine virtuelle Ubuntu
modèle de hello toocreate machine virtuelle, connectez-vous à hello Azure hello portail et l’utilisation classique suivant séquence : cliquez sur Nouveau, COMPUTE, MACHINE virtuelle, de galerie, UBUNTU, Ubuntu Server 14.04 LTS, puis cliquez sur la flèche vers la droite hello. Pour obtenir un didacticiel décrivant comment toocreate un VM Linux, consultez Créer une Machine virtuelle exécutant Linux.

Entrez hello après les informations sur l’écran hello « configuration d’ordinateur virtuel » #1 :

<table>
<tr><th>Nom du champ              </td><td>       Valeur du champ               </td><td>         Remarques                </td><tr>
<tr><td>Date de sortie de la version    </td><td> Sélectionnez une date dans la liste déroulante hello</td><td></td><tr>
<tr><td>Nom de machine virtuelle    </td><td> cass-template                   </td><td> Il s’agit hostname hello Hello machine virtuelle </td><tr>
<tr><td>Niveau                     </td><td> STANDARD                           </td><td> Laissez la valeur par défaut de hello              </td><tr>
<tr><td>TAILLE appropriée                     </td><td> A1                              </td><td>Sélectionnez hello que machine virtuelle basée sur hello e/s a besoin ; Pour cela, laissez par défaut de hello </td><tr>
<tr><td> Nouveau nom d'utilisateur             </td><td> localadmin                       </td><td> Dans Ubuntu 12.xx et versions ultérieures, « admin » est un nom d'utilisateur réservé.</td><tr>
<tr><td> Authentification         </td><td> Clic sur la case à cocher                 </td><td>Activez cette option si vous souhaitez toosecure avec une clé SSH </td><tr>
<tr><td> CERTIFICAT             </td><td> nom de fichier du certificat de clé publique hello </td><td> Utiliser hello de clé publique générée précédemment</td><tr>
<tr><td> Nouveau mot de passe    </td><td> Mot de passe fort </td><td> </td><tr>
<tr><td> Confirmer le mot de passe    </td><td> Mot de passe fort </td><td></td><tr>
</table>

Entrez hello après les informations sur l’écran hello « configuration d’ordinateur virtuel » #2 :

<table>
<tr><th>Nom du champ             </th><th> Valeur du champ                       </th><th> Remarques                                 </th></tr>
<tr><td> SERVICE CLOUD    </td><td> Créer un nouveau service de cloud computing    </td><td>Le service cloud est un conteneur qui calcule des ressources telles que des machines virtuelles</td></tr>
<tr><td> Nom du cloud Service DNS    </td><td>ubuntu-template.cloudapp.net    </td><td>Donnez un nom d'équilibrage de charge non spécifique à la machine.</td></tr>
<tr><td> Région/Groupe d'affinités/Réseau virtuel </td><td>    Ouest des États-Unis    </td><td> Sélectionnez une région à partir de laquelle vos applications web, accéder au cluster de Cassandra hello</td></tr>
<tr><td>Compte de stockage </td><td>    Utiliser la valeur par défaut    </td><td>Utiliser le compte de stockage par défaut hello ou un compte de stockage créés au préalable dans une région particulière</td></tr>
<tr><td>Groupe à haute disponibilité </td><td>    Aucun </td><td>    Laissez cette valeur vide</td></tr>
<tr><td>Points de terminaison    </td><td>Utiliser la valeur par défaut </td><td>    La configuration SSH hello par défaut </td></tr>
</table>

Cliquez sur la flèche droite, hello par défaut sur l’écran hello #3 et cliquez sur hello « vérification » bouton toocomplete hello VM processus d’approvisionnement. Après quelques minutes, hello machine virtuelle avec le nom « ubuntu-modèle hello » doit être dans un état « en cours d’exécution ».

### <a name="install-hello-necessary-software"></a>INSTALLER les logiciels nécessaires de hello
#### <a name="step-1-upload-tarballs"></a>ÉTAPE 1 : Téléchargement de tarballs
À l’aide du protocole scp ou pscp, hello de copie précédemment téléchargé logiciel trop ~ / répertoire téléchargements à l’aide de hello suivant le format de commande :

##### <a name="pscp-server-jre-8u5-linux-x64targz-localadminhk-cas-templatecloudappnethomelocaladmindownloadsserver-jre-8u5-linux-x64targz"></a>pscp server-jre-8u5-linux-x64.tar.gz localadmin@hk-cas-template.cloudapp.net:/home/localadmin/downloads/server-jre-8u5-linux-x64.tar.gz
Répétez hello au-dessus de commande pour JRE ainsi que pour les bits de Cassandra hello.

#### <a name="step-2-prepare-hello-directory-structure-and-extract-hello-archives"></a>ÉTAPE 2 : Préparation de la structure de répertoire hello et extraire les archives hello
Se connecter à la machine virtuelle de hello et créer la structure de répertoire hello et extraire le logiciel en tant que super utilisateur à l’aide d’un script d’interpréteur de commandes hello ci-dessous :

    #!/bin/bash
    CASS_INSTALL_DIR="/opt/cassandra"
    JRE_INSTALL_DIR="/opt/java"
    CASS_DATA_DIR="/var/lib/cassandra"
    CASS_LOG_DIR="/var/log/cassandra"
    DOWNLOADS_DIR="~/downloads"
    JRE_TARBALL="server-jre-8u5-linux-x64.tar.gz"
    CASS_TARBALL="apache-cassandra-2.0.8-bin.tar.gz"
    SVC_USER="localadmin"

    RESET_ERROR=1
    MKDIR_ERROR=2

    reset_installation ()
    {
       rm -rf $CASS_INSTALL_DIR 2> /dev/null
       rm -rf $JRE_INSTALL_DIR 2> /dev/null
       rm -rf $CASS_DATA_DIR 2> /dev/null
       rm -rf $CASS_LOG_DIR 2> /dev/null
    }
    make_dir ()
    {
       if [ -z "$1" ]
       then
          echo "make_dir: invalid directory name"
          exit $MKDIR_ERROR
       fi

       if [ -d "$1" ]
       then
          echo "make_dir: directory already exists"
          exit $MKDIR_ERROR
       fi

       mkdir $1 2>/dev/null
       if [ $? != 0 ]
       then
          echo "directory creation failed"
          exit $MKDIR_ERROR
       fi
    }

    unzip()
    {
       if [ $# == 2 ]
       then
          tar xzf $1 -C $2
       else
          echo "archive error"
       fi

    }

    if [ -n "$1" ]
    then
       SVC_USER=$1
    fi

    reset_installation
    make_dir $CASS_INSTALL_DIR
    make_dir $JRE_INSTALL_DIR
    make_dir $CASS_DATA_DIR
    make_dir $CASS_LOG_DIR

    #unzip JRE and Cassandra
    unzip $HOME/downloads/$JRE_TARBALL $JRE_INSTALL_DIR
    unzip $HOME/downloads/$CASS_TARBALL $CASS_INSTALL_DIR

    #Change hello ownership toohello service credentials

    chown -R $SVC_USER:$GROUP $CASS_DATA_DIR
    chown -R $SVC_USER:$GROUP $CASS_LOG_DIR
    echo "edit /etc/profile tooadd JRE toohello PATH"
    echo "installation is complete"


Si vous collez ce script dans la fenêtre de vim, rendre chariot de hello tooremove que retour ('\r ») à l’aide de hello de commande suivante :

    tr -d '\r' <infile.sh >outfile.sh

#### <a name="step-3-edit-etcprofile"></a>Étape 3 : Modification de etc/profile
Ajouter suivant hello à fin de hello :

    JAVA_HOME=/opt/java/jdk1.8.0_05
    CASS_HOME= /opt/cassandra/apache-cassandra-2.0.8
    PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$CASS_HOME/bin
    export JAVA_HOME
    export CASS_HOME
    export PATH

#### <a name="step-4-install-jna-for-production-systems"></a>Étape 4 : Installation de JNA pour les systèmes de production
Séquence de commandes suivante de hello utilisation : suivant de hello commande installation jna-3.2.7.jar et jna-platform-3.2.7.jar too/usr/share.java répertoire sudo apt-get installera libjna java

Créez des liens symboliques dans le répertoire $CASS_HOME/lib pour que le script de démarrage Cassandra puisse trouver ces fichiers JAR :

    ln -s /usr/share/java/jna-3.2.7.jar $CASS_HOME/lib/jna.jar

    ln -s /usr/share/java/jna-platform-3.2.7.jar $CASS_HOME/lib/jna-platform.jar

#### <a name="step-5-configure-cassandrayaml"></a>Étape 5 : Configuration de cassandra.yaml
Modifiez cassandra.yaml sur chaque configuration d’ordinateur virtuel tooreflect requise par tous les ordinateurs virtuels de hello [nous sera le modifier lors de la configuration réelle hello] :

<table>
<tr><th>Nom du champ   </th><th> Valeur  </th><th>    Remarques </th></tr>
<tr><td>nom_cluster </td><td>    « CustomerService »    </td><td> Utiliser le nom hello qui reflète votre déploiement</td></tr>
<tr><td>listen_address    </td><td>[laissez cette valeur vide]    </td><td> Supprimez « localhost » </td></tr>
<tr><td>rpc_addres   </td><td>[laissez cette valeur vide]    </td><td> Supprimez « localhost » </td></tr>
<tr><td>valeurs initiales    </td><td>« 10.1.2.4, 10.1.2.6, 10.1.2.8 »    </td><td>Liste de toutes les adresses IP hello sont désignés comme valeurs initiales.</td></tr>
<tr><td>endpoint_snitch </td><td> org.apache.cassandra.locator.GossipingPropertyFileSnitch </td><td> Il est utilisé par hello NetworkTopologyStrateg inférence hello centre de données et rack hello Hello machine virtuelle</td></tr>
</table>

#### <a name="step-6-capture-hello-vm-image"></a>Étape 6 : Capturer l’image de machine virtuelle hello
Connectez-vous à l’ordinateur virtuel de hello à l’aide du nom d’hôte hello (hk-autorités de certification-template.cloudapp.net) et la clé privée SSH hello créé précédemment. Consultez Comment tooUse SSH avec Linux sur Azure pour plus d’informations sur comment toolog à l’aide de hello commande ssh ou putty.exe.

Exécutez hello suivant la séquence d’image de hello toocapture actions :

##### <a name="1-deprovision"></a>1. annulation du déploiement
Utilisez la commande hello « sudo waagent – deprovision + utilisateur » tooremove d’informations sur l’ordinateur virtuel instance spécifiques. Consultez pour [comment tooCapture une Machine virtuelle Linux](capture-image.md) tooUse en tant que modèle plus d’informations sur les processus de capture d’image hello.

##### <a name="2-shutdown-hello-vm"></a>2 : hello d’arrêt machine virtuelle
Assurez-vous que l’ordinateur virtuel hello est mis en surbrillance, puis cliquez sur lien d’arrêt hello à partir de la barre de commandes bas hello.

##### <a name="3-capture-hello-image"></a>3 : image de capture hello
Assurez-vous que l’ordinateur virtuel hello est mis en surbrillance, puis cliquez sur lien CAPTURE hello à partir de la barre de commandes bas hello. Dans l’écran suivant de hello, donnez un nom d’IMAGE (par exemple, hk-cas-2-08-ub-14-04-2014071), approprié à la DESCRIPTION de l’IMAGE, cliquez sur processus de CAPTURE hello « vérification » marque toofinish hello.

Cette opération prendra quelques secondes et l’image de hello doit être disponible dans la section Mes IMAGES de galerie d’images hello. machine virtuelle de la source Hello est automatiquement supprimé une fois l’image de hello est capturée. 

## <a name="single-region-deployment-process"></a>Processus de déploiement dans une seule région
**Étape 1 : Créer le réseau virtuel de hello** connecter hello portail Azure et créez un réseau virtuel (classique) avec des attributs hello illustré hello tableau suivant. Consultez [créer un réseau virtuel (classiques) à l’aide de hello portail Azure](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) pour les étapes détaillées du processus de hello.      

<table>
<tr><th>Nom d'attribut de machine virtuelle</th><th>Valeur</th><th>Remarques</th></tr>
<tr><td>Name</td><td>vnet-cass-west-us</td><td></td></tr>
<tr><td>Région</td><td>Ouest des États-Unis</td><td></td></tr>
<tr><td>Serveurs DNS</td><td>Aucun</td><td>Ignorez cet attribut, car nous n'utilisons pas de serveur DNS</td></tr>
<tr><td>Espace d'adressage</td><td>10.1.0.0/16</td><td></td></tr>    
<tr><td>Adresse IP de départ</td><td>10.1.0.0</td><td></td></tr>    
<tr><td>CIDR </td><td>/16 (65531)</td><td></td></tr>
</table>

Ajoutez hello suivant sous-réseaux :

<table>
<tr><th>Nom</th><th>Adresse IP de départ</th><th>CIDR</th><th>Remarques</th></tr>
<tr><td>web</td><td>10.1.1.0</td><td>/24 (251)</td><td>Sous-réseau pour la batterie de serveurs web hello</td></tr>
<tr><td>données</td><td>10.1.1.0</td><td>/24 (251)</td><td>Sous-réseau pour les nœuds de base de données hello</td></tr>
</table>

Données et les sous-réseaux Web peuvent être protégés par le biais des groupes de sécurité réseau couverture hello qui est hors de portée pour cet article.  

**Étape 2 : Configurer les Machines virtuelles** à l’aide d’image hello créé précédemment, nous créer hello suivant des machines virtuelles dans le cloud de hello serveur « hk-c-svc-ouest » et lier les sous-réseaux toohello comme indiqué ci-dessous :

<table>
<tr><th>Nom de la machine    </th><th>Sous-réseau    </th><th>Adresse IP    </th><th>Groupe à haute disponibilité</th><th>Contrôleur de domaine ou rack</th><th>Initial ?</th></tr>
<tr><td>hk-c1-west-us    </td><td>données    </td><td>10.1.2.4    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1 </td><td>Oui</td></tr>
<tr><td>hk-c2-west-us    </td><td>données    </td><td>10.1.2.5    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack1    </td><td>Non </td></tr>
<tr><td>hk-c3-west-us    </td><td>données    </td><td>10.1.2.6    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Oui</td></tr>
<tr><td>hk-c4-west-us    </td><td>données    </td><td>10.1.2.7    </td><td>hk-c-aset-1    </td><td>dc =WESTUS rack =rack2    </td><td>Non </td></tr>
<tr><td>hk-c5-west-us    </td><td>données    </td><td>10.1.2.8    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Oui</td></tr>
<tr><td>hk-c6-west-us    </td><td>données    </td><td>10.1.2.9    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack3    </td><td>Non </td></tr>
<tr><td>hk-c7-west-us    </td><td>données    </td><td>10.1.2.10    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Oui</td></tr>
<tr><td>hk-c8-west-us    </td><td>données    </td><td>10.1.2.11    </td><td>hk-c-aset-2    </td><td>dc =WESTUS rack =rack4    </td><td>Non </td></tr>
<tr><td>hk-w1-west-us    </td><td>web    </td><td>10.1.1.4    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/A</td></tr>
<tr><td>hk-w2-west-us    </td><td>web    </td><td>10.1.1.5    </td><td>hk-w-aset-1    </td><td>                       </td><td>N/A</td></tr>
</table>

La création de hello au-dessus de la liste des machines virtuelles requiert hello suivant processus :

1. Création d'un service cloud vide dans une région particulière
2. Créer une machine virtuelle à partir de l’image capturée précédemment de hello et en l’attachant toohello de réseau virtuel créé précédemment. Répétez cette étape pour tous les ordinateurs virtuels de hello
3. Ajouter un service cloud toohello d’équilibrage de charge interne et en l’attachant sous-réseau de toohello « données »
4. Pour chaque machine virtuelle créée précédemment, ajoutez un point de terminaison à charge équilibrée pour le trafic via un équilibreur de charge interne à charge équilibrée ensemble connecté toohello créé précédemment thrift

Hello au-dessus de processus peut être exécutée à l’aide du portail Azure classic ; utiliser un ordinateur Windows (utilisez un ordinateur virtuel sur Azure si vous n’avez pas machine virtuelle Windows tooa accès), utilisez, hello suivant tooprovision de script PowerShell toutes les machines 8 virtuelles automatiquement.

**Liste 1 : script PowerShell pour l’approvisionnement des machines virtuelles**

        #Tested with Azure Powershell - November 2014
        #This powershell script deployes a number of VMs from an existing image inside an Azure region
        #Import your Azure subscription into hello current Powershell session before proceeding
        #hello process: 1. create Azure Storage account, 2. create virtual network, 3.create hello VM template, 2. crate a list of VMs from hello template

        #fundamental variables - change these tooreflect your subscription
        $country="us"; $region="west"; $vnetName = "your_vnet_name";$storageAccount="your_storage_account"
        $numVMs=8;$prefix = "hk-cass";$ilbIP="your_ilb_ip"
        $subscriptionName = "Azure_subscription_name";
        $vmSize="ExtraSmall"; $imageName="your_linux_image_name"
        $ilbName="ThriftInternalLB"; $thriftEndPoint="ThriftEndPoint"

        #generated variables
        $serviceName = "$prefix-svc-$region-$country"; $azureRegion = "$region $country"

        $vmNames = @()
        for ($i=0; $i -lt $numVMs; $i++)
        {
           $vmNames+=("$prefix-vm"+($i+1) + "-$region-$country" );
        }

        #select an Azure subscription already imported into Powershell session
        Select-AzureSubscription -SubscriptionName $subscriptionName -Current
        Set-AzureSubscription -SubscriptionName $subscriptionName -CurrentStorageAccountName $storageAccount

        #create an empty cloud service
        New-AzureService -ServiceName $serviceName -Label "hkcass$region" -Location $azureRegion
        Write-Host "Created $serviceName"

        $VMList= @()   # stores hello list of azure vm configuration objects
        #create hello list of VMs
        foreach($vmName in $vmNames)
        {
           $VMList += New-AzureVMConfig -Name $vmName -InstanceSize ExtraSmall -ImageName $imageName |
           Add-AzureProvisioningConfig -Linux -LinuxUser "localadmin" -Password "Local123" |
           Set-AzureSubnet "data"
        }

        New-AzureVM -ServiceName $serviceName -VNetName $vnetName -VMs $VMList

        #Create internal load balancer
        Add-AzureInternalLoadBalancer -ServiceName $serviceName -InternalLoadBalancerName $ilbName -SubnetName "data" -StaticVNetIPAddress "$ilbIP"
        Write-Host "Created $ilbName"
        #Add add hello thrift endpoint toohello internal load balancer for all hello VMs
        foreach($vmName in $vmNames)
        {
            Get-AzureVM -ServiceName $serviceName -Name $vmName |
                Add-AzureEndpoint -Name $thriftEndPoint -LBSetName "ThriftLBSet" -Protocol tcp -LocalPort 9160 -PublicPort 9160 -ProbePort 9160 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ilbName |
                Update-AzureVM

            Write-Host "created $vmName"     
        }

**Étape 3 : Configuration de Cassandra sur chaque machine virtuelle**

Se connecter à la machine virtuelle de hello et hello suivants :

* Modifiez $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello centre et rack propriétés de données :
  
       dc =EASTUS, rack =rack1
* Modifier des nœuds de valeur initiale cassandra.yaml tooconfigure comme indiqué ci-dessous :
  
       Seeds: "10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10"

**Étape 4 : Démarrer des machines virtuelles de hello et tester hello de cluster**

Ouvrez une session sur un des nœuds hello (par exemple, hk-c1-ouest-us) et en exécution hello suivant l’état du cluster de hello hello de toosee la commande :

       nodetool –h 10.1.2.4 –p 7199 status

Vous devez voir hello affichage similaire toohello une ci-dessous pour un cluster à 8 nœuds :

<table>
<tr><th>État</th><th>Adresse    </th><th>charger    </th><th>Jetons    </th><th>Appartenance </th><th>ID de l'hôte    </th><th>Rack</th></tr>
<tr><th>UN    </td><td>10.1.2.4     </td><td>87,81 Ko    </td><td>256    </td><td>38,0%    </td><td>GUID (supprimé)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.5     </td><td>41,08 Ko    </td><td>256    </td><td>68,9 %    </td><td>GUID (supprimé)</td><td>rack1</td></tr>
<tr><th>UN    </td><td>10.1.2.6     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.7     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack2</td></tr>
<tr><th>UN    </td><td>10.1.2.8     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.9     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack3</td></tr>
<tr><th>UN    </td><td>10.1.2.10     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack4</td></tr>
<tr><th>UN    </td><td>10.1.2.11     </td><td>55,29 Ko    </td><td>256    </td><td>68,8 %    </td><td>GUID (supprimé)</td><td>rack4</td></tr>
</table>

## <a name="test-hello-single-region-cluster"></a>Hello de test Cluster région unique
Utilisez hello suivant du cluster de hello tootest comme suit :

1. À l’aide d’applet de commande Get-AzureInternalLoadbalancer hello Powershell commande, obtenir adresse hello d’équilibreur de charge interne hello (par exemple)  10.1.2.101). syntaxe Hello de commande hello est indiqué ci-dessous : Get-AzureLoadbalancer – ServiceName « hk-c-svc-ouest-us » [affiche les détails de hello d’équilibrage de charge interne hello, ainsi que son adresse IP]
2. Connectez-vous à la batterie de serveurs web hello machine virtuelle (par exemple, hk-w1-ouest-us) à l’aide de Putty ou ssh
3. Exécutez $CASS_HOME/bin/cqlsh 10.1.2.101 9160
4. Hello suivant CQL commandes tooverify si hello cluster fonctionne, utilisez :
   
     CREATE KEYSPACE customers_ks WITH REPLICATION = { ’class’ : ’SimpleStrategy’, ’replication_factor’ : 3 };   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, ’John’, ’Doe’);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, ’Jane’, ’Doe’);
   
     SELECT * FROM Customers;

Vous devez voir un affichage comme hello une ci-dessous :

<table>
  <tr><th> customer_id </th><th> firstname </th><th> Lastname </th></tr>
  <tr><td> 1 </td><td> John </td><td> Doe </td></tr>
  <tr><td> 2 </td><td> Jane </td><td> Doe </td></tr>
</table>

Notez que cet espace de clés hello créé à l’étape 4 utilise SimpleStrategy avec un replication_factor de 3. SimpleStrategy est recommandé pour les déploiements de centre de données unique, tandis que NetworkTopologyStrategy est recommandé pour les déploiements de plusieurs centres de données. Un replication_factor égal à 3 procure une tolérance des échecs de nœuds.

## <a id="tworegion"></a>Processus de déploiement de plusieurs régions
Sera tirer parti du déploiement de région de hello s’est terminé et répétez hello même processus pour l’installation de la région deuxième hello. Hello principale différence entre hello unique et le déploiement de plusieurs régions est de configurer un tunnel VPN hello pour les communications entre région ; Nous démarre l’installation réseau de hello, configurer des machines virtuelles de hello et configurer Cassandra.

### <a name="step-1-create-hello-virtual-network-at-hello-2nd-region"></a>Étape 1 : Créer hello réseau virtuel à hello 2e région
Connectez-vous à hello portail Azure classic et créer un réseau virtuel à afficher des attributs hello dans la table de hello. Consultez [configurer un réseau virtuel uniquement dans le portail Azure classic de hello](../../../virtual-network/virtual-networks-create-vnet-classic-pportal.md) pour les étapes détaillées du processus de hello.      

<table>
<tr><th>Nom de l'attribut    </th><th>Valeur    </th><th>Remarques</th></tr>
<tr><td>Name    </td><td>vnet-cass-east-us</td><td></td></tr>
<tr><td>Région    </td><td>Est des États-Unis</td><td></td></tr>
<tr><td>Serveurs DNS        </td><td></td><td>Ignorez cet attribut, car nous n'utilisons pas de serveur DNS</td></tr>
<tr><td>Configurer un réseau VPN de point à site</td><td></td><td>        Ignorez cet attribut</td></tr>
<tr><td>Configurer un réseau VPN de site à site</td><td></td><td>        Ignorez cet attribut</td></tr>
<tr><td>Espace d'adressage    </td><td>10.2.0.0/16</td><td></td></tr>
<tr><td>Adresse IP de départ    </td><td>10.2.0.0    </td><td></td></tr>
<tr><td>CIDR    </td><td>/16 (65531)</td><td></td></tr>
</table>

Ajoutez hello suivant sous-réseaux :

<table>
<tr><th>Nom    </th><th>Adresse IP de départ    </th><th>CIDR    </th><th>Remarques</th></tr>
<tr><td>web    </td><td>10.2.1.0    </td><td>/24 (251)    </td><td>Sous-réseau pour la batterie de serveurs web hello</td></tr>
<tr><td>données    </td><td>10.2.2.0    </td><td>/24 (251)    </td><td>Sous-réseau pour les nœuds de base de données hello</td></tr>
</table>


### <a name="step-2-create-local-networks"></a>Étape 2 : Création des réseaux locaux
Un réseau Local sur le réseau virtuel Azure est un espace d’adressage de proxy qui mappe tooa site distant, y compris un cloud privé ou une autre région Azure. Cet espace d’adressage proxy est tooa dépendant de passerelle à distance pour le routage réseau toohello mise en réseau à droite des destinations. Consultez [configurer un réseau virtuel de tooVNet connexion](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) pour obtenir des instructions sur l’établissement de connexions de réseau virtuel à réseau virtuel hello.

Créez deux réseaux locaux par hello les détails suivants :

| Nom de réseau | Adresse de la passerelle VPN | Espace d'adressage | Remarques |
| --- | --- | --- | --- |
| hk-lnet-map-to-east-us |23.1.1.1 |10.2.0.0/16 |Lors de la création du réseau Local de hello donner à un espace réservé adresse de passerelle. adresse de passerelle réel Hello est complétée une fois la passerelle de hello est créée. Assurez-vous qu’espace d’adressage hello correspond exactement au hello respectif réseau à distance ; Dans ce cas hello réseau virtuel créé dans hello la région est des États-Unis. |
| hk-lnet-map-to-west-us |23.2.2.2 |10.1.0.0/16 |Lors de la création du réseau Local de hello donner à un espace réservé adresse de passerelle. adresse de passerelle réel Hello est complétée une fois la passerelle de hello est créée. Assurez-vous qu’espace d’adressage hello correspond exactement au hello respectif réseau à distance ; Dans ce cas hello réseau virtuel créé dans hello la région ouest des États-Unis. |

### <a name="step-3-map-local-network-toohello-respective-vnets"></a>Étape 3 : Carte réseau « Local » toohello respectifs réseaux virtuels
À partir de hello portail Azure classic, sélectionnez chaque réseau virtuel, cliquez sur « Configurer », vérifiez « Se connecter toohello réseau local », puis hello des réseaux locaux par hello les détails suivants :

| Réseau virtuel | Réseau local |
| --- | --- |
| hk-vnet-west-us |hk-lnet-map-to-east-us |
| hk-vnet-east-us |hk-lnet-map-to-west-us |

### <a name="step-4-create-gateways-on-vnet1-and-vnet2"></a>Étape 4 : Création des passerelles sur VNET1 et VNET2
À partir du tableau de bord hello de deux réseaux virtuels hello, cliquez sur Créer une passerelle qui déclenchera le processus de configuration de la passerelle du VPN hello. Après que quelques minutes hello du tableau de bord de chaque réseau virtuel doit afficher une adresse de passerelle réel hello.

### <a name="step-5-update-local-networks-with-hello-respective-gateway-addresses"></a>Étape 5 : Mise à jour « Local » des réseaux avec des adresses hello respectifs « passerelle »
Modifier les deux passerelles hello réseaux locaux tooreplace hello espace réservé passerelle IP adresse avec l’adresse IP réelle de hello Hello simplement mis en service. Utilisez hello après mappage :

<table>
<tr><th>Réseau local    </th><th>Passerelle de réseau virtuel</th></tr>
<tr><td>hk-lnet-map-to-east-us </td><td>Passerelle de hk-vnet-west-us</td></tr>
<tr><td>hk-lnet-map-to-west-us </td><td>Passerelle de hk-vnet-east-us</td></tr>
</table>

### <a name="step-6-update-hello-shared-key"></a>Étape 6 : Mettre à jour la clé partagée de hello
Hello utilisez Powershell script tooupdate hello IPSec clé de chaque passerelle VPN [clé de l’exploration utilisez hello pour les deux passerelles hello] suivante : Set-AzureVNetGatewayKey - VNetName hk-réseau virtuel-east-us - LocalNetworkSiteName hk-lnet-map-to-west-us - SharedKey D9E76BKK Set-AzureVNetGatewayKey - VNetName des hk-lnet-map-to-east-us des LocalNetworkSiteName - hk-réseau virtuel-ouest-us - SharedKey D9E76BKK

### <a name="step-7-establish-hello-vnet-to-vnet-connection"></a>Étape 7 : Hello au réseau de connexion
À partir de la hello portail Azure classic, utilisez le menu de « Tableau de bord » hello de deux connexions de passerelle à passerelle tooestablish hello réseaux virtuels. Utilisez des éléments de menu « Se connecter » hello dans la barre d’outils du bas hello. Après quelques minutes tableau de bord hello doit afficher les détails de connexion hello sous forme graphique.

### <a name="step-8-create-hello-virtual-machines-in-region-2"></a>Étape 8 : Créer des machines virtuelles de hello dans la région #2
Créez l’image d’Ubuntu hello comme décrit dans le déploiement de région #1 à hello suivante même étapes ou copiez hello image VHD fichier toohello compte de stockage Azure situé dans la région #2 et image de hello. Utiliser cette image et créer hello suivant la liste des machines virtuelles dans un service cloud hk-c-svc-east-us :

| Nom de la machine | Sous-réseau | Adresse IP | Groupe à haute disponibilité | Contrôleur de domaine ou rack | Initial ? |
| --- | --- | --- | --- | --- | --- |
| hk-c1-east-us |données |10.2.2.4 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Oui |
| hk-c2-east-us |données |10.2.2.5 |hk-c-aset-1 |dc =EASTUS rack =rack1 |Non |
| hk-c3-east-us |données |10.2.2.6 |hk-c-aset-1 |dc =EASTUS rack =rack2 |Oui |
| hk-c5-east-us |données |10.2.2.8 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Oui |
| hk-c6-east-us |données |10.2.2.9 |hk-c-aset-2 |dc =EASTUS rack =rack3 |Non |
| hk-c7-east-us |données |10.2.2.10 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Oui |
| hk-c8-east-us |données |10.2.2.11 |hk-c-aset-2 |dc =EASTUS rack =rack4 |Non |
| hk-w1-east-us |web |10.2.1.4 |hk-w-aset-1 |N/A |N/A |
| hk-w2-east-us |web |10.2.1.5 |hk-w-aset-1 |N/A |N/A |

Suivez hello mêmes instructions en tant que région #1 mais utilisent l’espace d’adressage 10.2.xxx.xxx.

### <a name="step-9-configure-cassandra-on-each-vm"></a>Étape 9 : Configuration de Cassandra sur chaque machine virtuelle
Se connecter à la machine virtuelle de hello et hello suivants :

1. Modifier $CASS_HOME/conf/cassandra-rackdc.properties toospecify hello centre et rack propriétés des données au format de hello : dc = EASTUS rack = racks 1
2. Modifier des nœuds de valeur initiale cassandra.yaml tooconfigure : semences : « 10.1.2.4,10.1.2.6,10.1.2.8,10.1.2.10,10.2.2.4,10.2.2.6,10.2.2.8,10.2.2.10 »

### <a name="step-10-start-cassandra"></a>Étape 10 : Démarrage de Cassandra
Connectez-vous à chaque machine virtuelle et démarrer Cassandra en arrière-plan de hello en exécutant hello de commande suivante : $CASS_HOME/bin/cassandra

## <a name="test-hello-multi-region-cluster"></a>Hello de test plusieurs régions Cluster
À ce stade Cassandra a été déployé too16 des nœuds avec 8 nœuds dans chaque région Azure. Ces nœuds sont Bonjour même cluster en vertu du nom de cluster commun hello et la configuration du nœud de valeur initiale hello. Utilisez hello suivant du cluster de processus tootest hello :

### <a name="step-1-get-hello-internal-load-balancer-ip-for-both-hello-regions-using-powershell"></a>Étape 1 : Obtenir une adresse IP équilibreur de charge interne de hello pour les deux régions hello à l’aide de PowerShell
* Get-AzureInternalLoadbalancer -ServiceName « hk-c-svc-west-us »
* Get-AzureInternalLoadbalancer -ServiceName « hk-c-svc-east-us »  
  
    Notez les adresses IP de hello (par exemple, ouest - 10.1.2.101, east - 10.2.2.101) affiché.

### <a name="step-2-execute-hello-following-in-hello-west-region-after-logging-into-hk-w1-west-us"></a>Étape 2 : Exécution suivante de hello dans la région Ouest hello après la connexion à hk-w1-ouest-us
1. Exécutez $CASS_HOME/bin/cqlsh 10.1.2.101 9160
2. Exécutez hello suivant les commandes du CQL :
   
     CREATE KEYSPACE customers_ks   WITH REPLICATION = { ’class’ : ’NetworkToplogyStrategy’, ’WESTUS’ : 3, ’EASTUS’ : 3};   USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, ’John’, ’Doe’);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, ’Jane’, ’Doe’);   SELECT * FROM Customers;

Vous devez voir un affichage comme hello une ci-dessous :

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

### <a name="step-3-execute-hello-following-in-hello-east-region-after-logging-into-hk-w1-east-us"></a>Étape 3 : Exécutez la commande suivante hello dans la région de hello est après la connexion à hk-w1-east-us :
1. Exécutez $CASS_HOME/bin/cqlsh 10.2.2.101 9160
2. Exécutez hello suivant les commandes du CQL :
   
     USE customers_ks;   CREATE TABLE Customers(customer_id int PRIMARY KEY, firstname text, lastname text);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES(1, ’John’, ’Doe’);   INSERT INTO Customers(customer_id, firstname, lastname) VALUES (2, ’Jane’, ’Doe’);   SELECT * FROM Customers;

Vous devez voir hello même afficher comme vu pour la région Ouest hello :

| customer_id | firstname | Lastname |
| --- | --- | --- |
| 1 |John |Doe |
| 2 |Jane |Doe |

Exécuter certaines insertions plus et que celles obtenir répliquée toowest-nous dans le cadre du cluster de hello.

## <a name="test-cassandra-cluster-from-nodejs"></a>Test de cluster Cassandra à partir de Node.js
À l’aide d’un des ordinateurs virtuels Linux de hello créé précédemment dans le niveau de « web » hello, nous exécutera une simples Node.js script tooread précédemment insérée les données de salutation

**Étape 1 : Installation de Node.js et du client Cassandra**

1. Installez Node.js et npm
2. Installez le package de nœud « cassandra-client » à l'aide de npm
3. Exécutez hello script invite hello qui affiche la chaîne json hello hello récupérée données suivant :
   
        var pooledCon = require('cassandra-client').PooledConnection;
        var ksName = "custsupport_ks";
        var cfName = "customers_cf";
        var hostList = ['internal_loadbalancer_ip:9160'];
        var ksConOptions = { hosts: hostList,
                             keyspace: ksName, use_bigints: false };
   
        function createKeyspace(callback){
           var cql = 'CREATE KEYSPACE ' + ksName + ' WITH strategy_class=SimpleStrategy AND strategy_options:replication_factor=1';
           var sysConOptions = { hosts: hostList,  
                                 keyspace: 'system', use_bigints: false };
           var con = new pooledCon(sysConOptions);
           con.execute(cql,[],function(err) {
           if (err) {
             console.log("Failed toocreate Keyspace: " + ksName);
             console.log(err);
           }
           else {
             console.log("Created Keyspace: " + ksName);
             callback(ksConOptions, populateCustomerData);
           }
           });
           con.shutdown();
        }
   
        function createColumnFamily(ksConOptions, callback){
          var params = ['customers_cf','custid','varint','custname',
                        'text','custaddress','text'];
          var cql = 'CREATE COLUMNFAMILY ? (? ? PRIMARY KEY,? ?, ? ?)';
        var con =  new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) {
                 console.log("Failed toocreate column family: " + params[0]);
                 console.log(err);
              }
              else {
                 console.log("Created column family: " + params[0]);
                 callback();
              }
          });
          con.shutdown();
        }
   
        //populate Data
        function populateCustomerData() {
           var params = ['John','Infinity Dr, TX', 1];
           updateCustomer(ksConOptions,params);
   
           params = ['Tom','Fermat Ln, WA', 2];
           updateCustomer(ksConOptions,params);
        }
   
        //update will also insert hello record if none exists
        function updateCustomer(ksConOptions,params)
        {
          var cql = 'UPDATE customers_cf SET custname=?,custaddress=? where custid=?';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,params,function(err) {
              if (err) console.log(err);
              else console.log("Inserted customer : " + params[0]);
          });
          con.shutdown();
        }
   
        //read hello two rows inserted above
        function readCustomer(ksConOptions)
        {
          var cql = 'SELECT * FROM customers_cf WHERE custid IN (1,2)';
          var con = new pooledCon(ksConOptions);
          con.execute(cql,[],function(err,rows) {
              if (err)
                 console.log(err);
              else
                 for (var i=0; i<rows.length; i++)
                    console.log(JSON.stringify(rows[i]));
            });
           con.shutdown();
        }
   
        //exectue hello code
        createKeyspace(createColumnFamily);
        readCustomer(ksConOptions)

## <a name="conclusion"></a>Conclusion
Microsoft Azure est une plateforme flexible qui permet d’utiliser hello Microsoft ainsi que des logiciels open source comme illustré dans cet exercice. Les clusters Cassandra hautement disponibles peuvent être déployés sur un centre de données via hello répartissant hello des nœuds de cluster sur plusieurs domaines d’erreur. Les clusters Cassandra peuvent également être déployés dans plusieurs régions Azure géographiquement distantes afin de protéger les systèmes contre les sinistres. Azure et vous permet d’ensemble Cassandra hello construction de hautement évolutive, hautement disponible et de services cloud récupérable d’urgence nécessitent par l’internet aujourd'hui l’échelle des services.  

## <a name="references"></a>Références
* [http://cassandra.apache.org](http://cassandra.apache.org)
* [http://www.datastax.com](http://www.datastax.com)
* [http://www.nodejs.org](http://www.nodejs.org)

