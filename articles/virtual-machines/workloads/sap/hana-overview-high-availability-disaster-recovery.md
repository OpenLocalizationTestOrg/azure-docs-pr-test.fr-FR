---
title: "aaaHigh disponibilité et récupération d’urgence de HANA SAP sur Azure (instances de grande taille) | Documents Microsoft"
description: "Établissez la haute disponibilité et planifiez la récupération d’urgence de SAP HANA sur Azure (grandes instances)."
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
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a>Haute disponibilité et récupération d’urgence de SAP HANA (grandes instances) sur Azure 

La haute disponibilité et la récupération d’urgence constituent des aspects fondamentaux de l’exécution de vos serveurs SAP HANA sur Azure (grandes instances) stratégiques. Son toowork important avec SAP, votre intégrateur système, ou Microsoft tooproperly architectes et implémentez hello stratégie de droite haute-disponibilité/récupération d’urgence. Il est également objectif de point de récupération tooconsider important hello et objectif de temps de récupération, qui sont spécifiques tooyour environnement.

## <a name="high-availability"></a>Haute disponibilité

Microsoft prend en charge les méthodes de haute disponibilité SAP HANA « hors de la zone de hello, » qui incluent :

- **La réplication du stockage :** hello tooreplicate de capacité du système de stockage de tout emplacement tooanother de données (dans, ou distinct, hello même centre de données). SAP HANA opère indépendamment de cette méthode.
- **Réplication du système HANA :** hello de réplication de toutes les données dans le système de SAP HANA SAP HANA tooa distinct. objectif de temps de récupération Hello est réduit grâce à la réplication de données à intervalles réguliers. SAP HANA prend en charge les modes de mémoire et synchrones asynchrones, synchrones (recommandé uniquement pour SAP HANA systèmes qui se trouvent dans hello même centre de données ou inférieur à 100 KM éloignés). Dans la conception actuelle de hello de tampons de grande instance HANA, la réplication de système HANA peut être utilisée pour la haute disponibilité uniquement.
- **Héberger le basculement automatique :** un toouse de solution de récupération après incident local en tant qu’une autre toosystem la réplication. Lorsque hello principal devient indisponible, un ou plusieurs nœuds de SAP HANA en attente sont configurés en mode de montée en puissance parallèle et SAP HANA bascule automatiquement tooanother nœud.

Pour plus d’informations sur la haute disponibilité de SAP HANA, consultez hello SAP informations suivantes :

- [SAP HANA High-Availability Whitepaper (Livre blanc sur la haute disponibilité de SAP HANA)](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [SAP HANA Administration Guide (Guide d’administration de SAP HANA)](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [SAP Academy Video on SAP HANA System Replication (Vidéo SAP Academy sur la réplication du système SAP HANA) ](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [SAP Support Note #1999880 – FAQ on SAP HANA System Replication (Note de support SAP n°1999880 – FAQ sur la réplication du système SAP HANA)](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- [SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment (Note de support SAP n°2165547 – Sauvegarde et restauration SAP HANA dans l’environnement de réplication du système SAP HANA)](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)
- [SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime (Note de support SAP n°1984882 – Utilisation de la réplication du système SAP HANA pour l’échange de matériel avec un temps d’arrêt minime ou nul)](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)

## <a name="disaster-recovery"></a>Récupération d'urgence

SAP HANA sur Azure (grandes instances) est offert dans deux régions Azure d’une région géopolitique. Entre les tampons de grande instance deux hello de deux régions différentes est une connectivité réseau directe pour répliquer les données pendant la récupération d’urgence. la réplication de données de hello Hello est infrastructure de stockage. la réplication de Hello n’est pas effectuée par défaut. Il est fait pour les configurations de client hello classés de la récupération d’urgence hello. Dans la conception actuelle de hello, réplication HANA du système ne peut pas être utilisée pour la récupération d’urgence.

Toutefois, tootake parti hello la récupération d’urgence, vous devez toostart toodesign hello réseau connectivité toohello deux régions différentes Azure. toodo, vous pouvez donc une connexion de circuit ExpressRoute de Azure localement dans votre région Azure principale et une autre connexion de circuit de région de récupération d’urgence tooyour local. Cette mesure s’applique à une situation dans laquelle une région Azure complète, incluant l’emplacement d’un routeur Microsoft Enterprise Edge (MSEE), rencontre un problème.

Comme deuxième mesure, vous pouvez vous connecter à tous les réseaux virtuels Azure qui se connectent tooSAP HANA sur Azure (instances de grande taille) dans un des tooboth de régions hello de ces circuits ExpressRoute. Cette mesure répond à un cas où seule des emplacements de MSEE hello qui se connecte votre emplacement local avec Azure est mis hors service.

Hello figure ci-dessous illustre une configuration optimale hello pour la récupération d’urgence :

![Configuration optimale pour la récupération d’urgence](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

Bonjour cas optimale pour une configuration de la récupération d’urgence du réseau de hello est toohave deux des circuits ExpressRoute à partir de local toohello deux régions différentes Azure. Un circuit passe tooregion #1, une instance de production en cours d’exécution. circuit ExpressRoute de la deuxième Hello passe tooregion #2, certaines instances HANA hors production en cours d’exécution. (Cela est important si une région Azure entière, y compris hello MSEE et tampon de grande instance, sort de la grille de hello.)

Comme deuxième mesure, hello différents réseaux virtuels est connecté toohello des circuits ExpressRoute différents qui sont connecté tooSAP HANA sur Azure (instances de grande taille). Vous pouvez contourner hello emplacement de stockage un MSEE échoue, ou vous réduirez l’objectif de point de récupération de hello pour la récupération d’urgence, comme nous aborderons plus tard.

Hello des spécifications suivantes pour une installation de récupération d’urgence sont :

- Vous devez ordonner SAP HANA sur les références de Azure (instances de grande taille) de hello même taille que votre production références (SKU) et que vous les déployer dans la zone de reprise après sinistre hello. Ces instances peuvent être utilisés toorun test, bac à sable ou des instances de QA HANA.
- Vous devez commander un profil de la récupération d’urgence pour chacune de vos HANA SAP sur Azure (instances de grande taille) références (SKU) que vous souhaitez toorecover dans le site de récupération d’urgence hello, si nécessaire. Cette action entraîne une allocation toohello des volumes de stockage, qui sont la cible de hello de réplication de stockage hello à partir de votre région de production dans la zone de reprise après sinistre hello.

Une fois que vous remplissez hello précédant la configuration requise, il est la réplication de stockage de responsabilité toostart hello. Dans l’infrastructure de stockage hello utilisée pour SAP HANA sur Azure (instances de grande taille), hello la réplication du stockage est instantanés de stockage. réplication de la récupération d’urgence toostart hello, vous devez tooperform :

- Une capture instantanée de votre numéro d’unité logique de démarrage, comme décrit précédemment.
- Une capture instantanée de vos volumes associés à HANA, comme décrit précédemment.

Après avoir exécuté ces captures instantanées, un réplica initial des volumes de hello est amorcé sur des volumes hello qui sont associés à votre profil de récupération d’urgence dans la région de récupération d’urgence hello.

Par la suite, instantané stockage le plus récent hello est utilisé toutes les heures deltas hello tooreplicate qui surviennent sur des volumes de stockage hello.

objectif de point de récupération Hello obtenue avec cette configuration est de 60 minutes too90. tooachieve une amélioration de la reprise de point dans les cas de récupération d’urgence hello, copie hello HANA journal des transactions à partir de SAP HANA sur Azure (instances de grande taille) toohello autre région Azure. tooachieve cet objectif de point de récupération, hello suivant :

1. Sauvegardez hello HANA transaction sauvegarde du journal aussi souvent que possible trop/hana/journaux /.
2. Copiez les sauvegardes de journaux de transactions hello lorsqu’ils sont tooan terminé de machine virtuelle Azure (VM), qui se trouve dans un réseau virtuel qui s’est connecté toohello SAP HANA sur le serveur Azure (instances de grande taille).
3. À partir de cette machine virtuelle, copiez tooa de sauvegarde hello machine virtuelle qui est dans un réseau virtuel dans la zone de reprise après sinistre hello.
4. Conserver des sauvegardes du journal des transactions de hello dans cette région hello machine virtuelle.

En cas de sinistre, une fois le profil de la récupération d’urgence hello a été déployé sur un serveur réel, copier les sauvegardes de journaux de transactions hello à partir de la toohello de machine virtuelle hello HANA SAP sur Azure (instances de grande taille) qui est maintenant hello serveur principal dans la zone de reprise après sinistre hello, et restaurez ces sauvegardes. Cette récupération est possible car l’état de hello de HANA sur des disques de récupération d’urgence hello est celle d’un instantané HANA. Il s’agit de point d’offset hello pour d’autres restaurations du journal des transactions.

## <a name="backup-and-restore"></a>Sauvegarde et restauration

Une des bases de toooperating hello principaux aspects consiste à s’assurer de base de données hello peut être protégé à partir de divers événements graves. Ces événements peuvent être provoqués par quoi que ce soit à partir d’erreurs de l’utilisateur toosimple catastrophes naturelles.

Sauvegarde une base de données hello capacité toorestore il tooany point dans le temps (tel qu’avant la suppression des données critiques, une personne), permet à l’état de restauration tooa qui est aussi proche que possible toohello moyen, elle était avant l’interruption de hello s’est produite.

Pour optimiser les résultats, vous devez effectuer deux types de sauvegardes :

- Sauvegardes de base de données
- Sauvegardes des journaux de transactions

En outre les sauvegardes de base de données toofull effectuées à un niveau de l’application, vous pouvez être encore plus précise en effectuant des sauvegardes et les instantanés de stockage. Effectuer des sauvegardes de journal est également important pour la restauration de la base de données hello (tooempty hello journaux et des transactions déjà validées).

SAP HANA sur Azure (grandes instances) offre deux options de sauvegarde et de restauration :

- Utilisation de vos propres méthodes de sauvegarde. Une fois que vous calculez tooensure suffisamment d’espace disque, effectuer des sauvegardes complètes de base de données et du journal à l’aide des méthodes de sauvegarde de disque (disques toothose). Au fil du temps, les sauvegardes hello sont copié tooan compte de stockage Azure (une fois que vous configurez un serveur de fichiers Azure avec stockage quasiment illimitée), ou utilisent un coffre de sauvegarde Azure ou d’un froid le stockage Azure. Une autre option est toouse un outil de protection des données tierces, telles que Commvault, les sauvegardes de hello toostore une fois qu’ils sont copiés de compte de stockage tooa. Hello, option de sauvegarde personnalisée peut également être nécessaire pour les données qui doit toobe stockée plus longtemps à des fins d’audit et de conformité.
- Utiliser hello de sauvegarde et de restauration qui hello infrastructure sous-jacente de HANA SAP sur Azure (instances de grande taille) fournit. Cette option correspond à la nécessité de hello pour les sauvegardes et rend les sauvegardes manuelles presque obsolète (sauf où les sauvegardes de données sont requises pour des raisons de compatibilité). rest Hello de cette section traite hello sauvegarde et de restauration des fonctionnalités offertes avec HANA (instances de grande taille).

> [!NOTE]
> technologie de capture instantanée Hello qui est utilisée par l’infrastructure sous-jacente de hello de HANA (instances de grande taille) a une dépendance sur les instantanés de SAP HANA. Les captures instantanées SAP HANA ne fonctionnent pas conjointement avec les conteneurs de bases de données SAP HANA mutualisées. Par conséquent, cette méthode de sauvegarde ne peut pas être utilisé toodeploy SAP HANA mutualisée base de données de conteneurs.

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a>Utilisation des captures instantanées de stockage de SAP HANA sur Azure (grandes instances)

infrastructure de stockage Hello sous-jacent HANA SAP sur Azure (instances de grande taille) prend en charge la notion de hello d’un instantané du stockage de volumes. Sauvegarde et restauration d’un volume particulier sont pris en charge, hello suivant considérations :

- Au lieu d’exécuter des sauvegardes de base de données, le système procède à de fréquentes captures instantanées des volumes de stockage.
- instantané de stockage Hello lance un instantané de SAP HANA avant l’exécution de capture instantanée de stockage hello. Cet instantané SAP HANA est le point de programme d’installation de hello pour les restaurations du journal éventuelle après la récupération de l’instantané du stockage hello.
- À un moment hello où les instantanés de stockage hello est exécutée avec succès, instantané de SAP HANA hello est supprimé.
- Sauvegardes de journaux fréquemment et sont stockées dans le volume de sauvegarde de journal hello ou dans Azure.
- Si la base de données hello doit être restauré tooa certain point dans le temps, une demande est faite tooMicrosoft prise en charge de Azure (panne de production) ou SAP HANA sur la gestion des services Azure toorestore tooa certaines instantané du stockage (par exemple, une planifié restauration d’un système de bac à sable état d’origine tooits).
- instantané de SAP HANA Hello qui est inclus dans l’instantané de stockage hello est un point de décalage pour appliquer les sauvegardes du journal qui ont été exécutées et stockées après que hello stockage instantané a été pris.
- Ces sauvegardes de journal sont effectuées toorestore tooa arrière de base de données hello certain point dans le temps.

Sauvegarde de hello en spécifiant\_nom crée un instantané de hello suivant volumes :

- hana/data
- hana/log
- hana/log\_backup (monté en tant que sauvegarde dans hana/log)
- hana/shared

### <a name="storage-snapshot-considerations"></a>Considérations relatives aux captures instantanées de stockage

>[!NOTE]
>Les captures instantanées de stockage ne sont _pas_ fournies gratuitement car elles nécessitent l’allocation d’un espace de stockage supplémentaire.

mécanismes spécifiques de Hello d’instantanés de stockage pour SAP HANA sur Azure (instances de grande taille) sont les suivantes :

- Un instantané de stockage spécifique (ponctuelle hello lorsqu’elle est récupérée) consomme très peu de stockage.
- En tant que les modifications de contenu de données et du contenu de hello dans les données SAP HANA modification des fichiers sur le volume de stockage hello, instantané d’hello doit le contenu de bloc d’origine toostore hello.
- instantané de stockage Hello augmente en taille. Hello plus hello instantané existe, hello plus grande hello stockage snapshot devient.
- Hello plus apportés toohello volume de base de données SAP HANA sur la durée de vie hello d’un instantané du stockage, hello plus grande hello la consommation d’espace d’instantané de stockage hello devient.

SAP HANA sur Azure (instances de grande taille) est fourni avec des tailles de volume fixe pour le volume de données et les journaux de SAP HANA hello. Effectuer des captures instantanées de ces volumes mange à votre espace de volume afin qu’il soit votre instantanés de stockage responsabilité tooschedule (dans hello SAP HANA sur processus Azure [instances de grande taille]).

Hello sections suivantes fournissent des informations pour effectuer ces captures instantanées, y compris les recommandations générales :

- Bien que le matériel de hello peut faire face aux 255 instantanés par volume, nous vous recommandons vivement de rester en dessous de ce nombre.
- Avant d’effectuer des captures instantanées du stockage, surveillez l’espace libre.
- Nombre de hello inférieur d’instantanés de stockage basé sur l’espace libre. Vous devrez peut-être le nombre de hello toolower d’instantanés que vous conservez, ou vous devrez peut-être les volumes tooextend hello. (Vous pouvez commander du stockage supplémentaire par unités de 1 To).
- Lorsque vous exécutez des tâches telles que le déplacement de données dans SAP HANA avec des outils de migration système (en utilisant R3load ou en restaurant des bases de données SAP HANA à partir de sauvegardes), il est fortement déconseillé d’effectuer la moindre capture instantanée de stockage. (Si une migration de système est en cours sur un nouveau système SAP HANA, des instantanés de stockage seraient inutile toobe effectuée.)
- Dans le cadre de réorganisations plus vastes des tables SAP HANA, les captures instantanées de stockage doivent être évitées dans la mesure du possible.
- Les instantanés de stockage sont une fonctionnalités de récupération d’urgence hello tooengaging requis de HANA SAP sur Azure (instances de grande taille).

### <a name="setting-up-storage-snapshots"></a>Configuration des captures instantanées de stockage

1. Assurez-vous que Perl est installé dans le système de d’exploitation Linux hello sur serveur de hello HANA (instances de grande taille).
2. Modifier/etc/ssh/ssh\_ligne de hello config tooadd _Mac hmac-sha1_.
3. Créer un compte d’utilisateur de sauvegarde SAP HANA sur le nœud principal de hello pour chaque instance SAP HANA que vous sont en cours d’exécution (le cas échéant).
4. client de SAP HANA HDB Hello doit être installé sur tous les serveurs (instances de grande taille) de SAP HANA.
5. Sur serveur hello première SAP HANA (instances de grande taille) de chaque région, une clé publique doit être créée hello tooaccess sous-jacent d’infrastructure de stockage qui contrôle la création d’instantanés.
6. Copiez le script hello azure\_hana\_backup.pl à partir de l’emplacement de toohello/scripts de **hdbsql** Hello installation de SAP HANA.
7. Hello de copie HANABackupDetails.txt de fichiers à partir / scripts toohello même emplacement que hello script Perl.
8. Modifier le fichier de HANABackupDetails.txt de hello en fonction des spécifications du client approprié hello.

### <a name="step-1-install-sap-hana-hdbclient"></a>Étape 1 : Installer SAP HANA HDBClient

Hello Linux installé sur SAP HANA sur Azure (instances de grande taille) inclut des dossiers de hello et des scripts d’instantanés de stockage SAP HANA tooexecute nécessaire pour des raisons de sauvegarde et récupération d’urgence. Toutefois, il est votre tooinstall responsabilité SAP HANA HDBclient lors de l’installation SAP HANA. (Microsoft installe ni hello HDBclient ni SAP HANA.)

### <a name="step-2-change-etcsshsshconfig"></a>Étape 2 : Modifier /etc/ssh/ssh\_config

Modifiez /etc/ssh/ssh\_config en ajoutant la ligne _MACs hmac-sha1_ comme indiqué ici :
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a>Étape 3 : Créer une clé publique

Sur hello première SAP HANA sur le serveur de Azure (instances de grande taille) dans chaque région Azure, créez une infrastructure de stockage hello tooaccess toobe de clé publique utilisé afin que vous pouvez créer des instantanés. clé publique de Hello garantit qu’un mot de passe n’est pas toosign requis dans le stockage toohello et que les informations d’identification de mot de passe ne sont pas conservées. Dans Linux sur le serveur SAP HANA (instances de grande taille) de hello, exécutez hello commande toogenerate hello publique clé suivante :
```
  ssh-keygen –t dsa –b 1024
```
nouvel emplacement de Hello est _/root/.ssh/id\_dsa.pub. N’entrez pas un mot de passe réel, sans quoi vous serez tooenter requis, hello phrase secrète chaque fois que vous vous connectez. Au lieu de cela, appuyez sur **entrée** deux fois tooremove hello Entrez exigence de mot de passe pour établir la connexion.

Vérifiez toomake que cette clé publique hello a été résolue comme prévu en modifiant les dossiers too/root/.ssh/, puis d’exécuter hello **ls** commande. Si la clé de hello est présent, vous pouvez le copier en exécutant hello de commande suivante :

![Clé publique copiée par l’exécution de cette commande](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

À ce stade, contactez SAP HANA sur la gestion des services Azure et fournir la clé de hello. Hello représentant du service utilise tooregister de clé publique hello dans hello sous-jacent de l’infrastructure de stockage.

### <a name="step-4-create-an-sap-hana-user-account"></a>Étape 4 : Créer un compte d’utilisateur SAP HANA

Créez un compte d’utilisateur SAP HANA dans SAP HANA Studio à des fins de sauvegarde. Ce compte doit disposer de hello suivant des privilèges : _sauvegarde Admin_ et _lecture de catalogue_. Dans cet exemple, le nom d’utilisateur hello SCADMIN est créé.

![Création d’un utilisateur dans HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a>Étape 5 : Autoriser le compte d’utilisateur SAP HANA hello

Autoriser le compte d’utilisateur SAP HANA hello (toobe utilisé par les scripts de hello sans nécessiter une autorisation chaque fois que hello script est exécuté). Hello commande de SAP HANA `hdbuserstore` permet la création d’une clé utilisateur SAP HANA, qui est stockée sur un ou plusieurs nœuds de SAP HANA hello. clé d’utilisateur Hello permet également hello utilisateur tooaccess SAP HANA sans avoir toomanage les mots de passe à partir de dans hello scripting des processus qui est décrit plus loin.

>[!IMPORTANT]
>Exécution hello après une commande en tant que `_root_`. Sinon, le script de hello ne peut pas fonctionner correctement.

Entrez hello `hdbuserstore` commande comme suit :

![Entrez la commande de hdbuserstore hello](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

Bonjour exemple, où l’utilisateur hello est SCADMIN01 et nom d’hôte hello est lhanad01, commande hello est :
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
Gérez la totalité des scripts à partir d’un seul serveur pour les instances HANA de montée en puissance parallèle. Dans cet exemple, la clé de SAP HANA hello SCADMIN01 doit être modifié pour chaque hôte d’une manière qui reflète l’hôte hello toohello connexes clé. Autrement dit, hello compte de sauvegarde SAP HANA est modifiée avec un numéro d’instance hello Hello HANA DB, **lhanad**. clé de Hello doit avoir des privilèges d’administrateur sur l’ordinateur hôte de hello qu'auquel elle est assignée, et utilisateur de sauvegarde hello pour la montée en puissance parallèle doit avoir accès aux droits tooall SAP HANA instances.
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a>Étape 6 : Copier des éléments à partir du dossier/scripts hello

Suit hello de copie des éléments de hello/répertoire de travail toohello dossier (inclus sur image hello gold d’installation de hello) pour les scripts **hdbsql**. Pour les installations HANA actuelles, il s’agit du répertoire /hana/shared/D01/exe/linuxx86\_64/hdb.
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
Copiez hello éléments suivants s’ils exécutent une montée en puissance parallèle ou OLAP :
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
fichier de HANABackupCustomerDetails.txt Hello est modifiable comme suit pour un déploiement de la montée en puissance parallèle. Il est hello contrôle et fichier de configuration pour le script hello qui exécute des instantanés de stockage hello. Vous devez avoir reçu hello _nom du stockage de sauvegarde_ et _adresse IP de stockage_ à partir de SAP HANA sur la gestion des services Azure lors de vos instances ont été déployés. Vous ne pouvez pas modifier les séquence hello, classement ou l’espacement de toutes les variables hello ou un script de hello ne fonctionne pas correctement.

Pour un déploiement de la montée en puissance parallèle, le fichier de configuration hello ressemble à :
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
Pour une configuration de la montée en puissance parallèle, le fichier de HANABackupCustomerDetailsBW.txt hello ressemble à :
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
>Actuellement, uniquement les informations de nœud 1 sont utilisées dans le script de capture instantanée de stockage hello réel HANA. Nous vous recommandons de tester tooor d’accès de tous les nœuds HANA, afin que, si le nœud de sauvegarde maître hello change, vous avez déjà vérifié que tout autre nœud peut prendre sa place en modifiant les détails hello dans le nœud 1.

toocheck pour les configurations de hello correct dans le fichier de configuration hello ou instances HANA toohello une connectivité, exécutez une des hello scripts suivants :
- Pour une configuration de montée en puissance (indépendamment de la charge de travail SAP) :

 ```
testHANAConnection.pl
```
- Pour une configuration de montée en puissance parallèle :

 ```
testHANAConnectionBW.pl
```

Vous assurer que hello master HANA instance HANA des serveurs d’accès tooall requis. Il n’y aucun script toohello de paramètres, mais vous devez effectuer hello approprié HANABackupCustomerDetails /file HANABackupCustomerDetailsBW pour hello script toorun correctement. Étant donné que seuls hello shell commande codes d’erreur sont renvoyés, il n’est pas possible pour hello script tooerror-Vérifiez chaque instance de. Même dans ce cas, le script de hello fournit des commentaires utiles pour toodouble vérification.

script de hello toorun :
```
 ./testHANAConnection.pl
```
 Si le script de hello obtient correctement état hello d’instance HANA hello, il affiche un message de réussite de connexion de HANA hello.

En outre, un deuxième type est de script, vous pouvez utiliser toosign de capacité toocheck hello master HANA instance serveur dans le stockage toohello. Avant d’exécuter Bonjour azure\_hana\_sauvegarde (\_bw) .pl script, vous devez exécuter le script suivant de hello. Si un volume ne contient aucun instantané, il est impossible toodetermine si le volume de hello est simplement vide ou il est un ssh hello tooobtain de défaillance détails de l’instantané. Pour cette raison, le script de hello exécute deux étapes :

- Il vérifie que cette console de stockage hello est accessible.
- Il crée une capture instantanée de test, ou fictive, pour chaque volume par instance HANA.

Pour cette raison, instance HANA hello est inclus en tant qu’argument. Là encore, il n’est pas possible de tooprovide vérification des erreurs de connexion de stockage hello, mais le script de hello fournit des conseils utiles en cas de l’exécution de hello.

script de Hello est exécuté en tant que :
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
Ou sous la forme :
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
script de Hello affiche également un message que vous êtes en mesure de toosign dans correctement tooyour déployé stockage locataire, qui est axé sur hello unité logique (LUN) qui est utilisés par les instances de serveur hello que vous êtes propriétaire.

Avant d’exécuter des sauvegardes hello premier stockage basé sur un instantané, exécutez toomake scripts hello suivant que cette configuration hello est correcte.

Après avoir exécuté ces scripts, vous pouvez supprimer les instantanés hello en exécutant :
```
./removeTestStorageSnapshot.pl <hana instance>
```
Ou
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a>Étape 7 : Effectuer des captures instantanées à la demande

Effectuez des captures instantanées à la demande (et planifiez des captures instantanées régulières à l’aide de cron) comme décrit ici.

Pour les configurations de montée en puissance parallèle, exécutez hello script suivant :
```
./azure_hana_backup.pl lhanad01 customer 20
```
Pour les configurations de montée en puissance parallèle, exécutez hello script suivant :
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
script de montée en puissance parallèle de Hello effectue certaines toomake de vérification supplémentaire tous les serveurs HANA est accessible, et toutes les instances HANA retournent statut approprié de l’instance hello avant de procéder à la création d’instantanés de stockage ou de SAP HANA.

Hello arguments suivants est requis :

- Hello HANA nécessitant une sauvegarde d’une instance.
- préfixe d’instantané Hello pour la capture instantanée de stockage hello.
- nombre de Hello de toobe instantanés conservé pour un préfixe spécifique de hello.

```
./azure_hana_backup.pl lhanad01 customer 20
```

l’exécution de Hello du script de hello crée un instantané du stockage hello dans ces trois phases distinctes :

- Exécution d’une capture instantanée HANA
- Exécution d’une capture instantanée de stockage
- Supprimer un instantané HANA hello.

Exécutez le script de hello en l’appelant à partir du dossier exécutable hello HDB a été copié à. Il sauvegarde hello au moins la suite des volumes, mais il sauvegarde un volume qui a le nom d’instance SAP HANA hello explicite dans le nom de volume hello.
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
période de rétention Hello est strictement administrée, nombre de hello d’instantanés soumis en tant que paramètre lorsque vous exécutez le script hello (par exemple, 20, tel que décrit précédemment). Par conséquent, hello temps est une fonction de la période d’exécution et hello nombre d’instantanés dans l’appel de hello du script de hello hello. Si hello nombre d’instantanés sont conservés excède hello sont nommés en tant que paramètre dans l’appel de hello du script de hello, hello instantané le plus ancien stockage de cette étiquette (dans notre cas précédent, _personnalisé_) est supprimé avant un nouvel instantané est exécutée. Cela signifie que le nombre de hello que vous donnez comme dernier paramètre d’appel de hello hello est nombre hello vous pouvez utiliser le nombre de hello toocontrol d’instantanés.

>[!NOTE]
>Dès que vous modifiez les étiquette hello, hello commence le comptage à nouveau.

Vous devez tooinclude hello HANA nom de l’instance qui est fournie par SAP HANA sur la gestion des services Azure en tant qu’argument, si elles sont également créer des instantanés dans des environnements à plusieurs nœuds. Dans les environnements à nœud unique, nom hello Hello SAP HANA sur l’unité de Azure (instances de grande taille) est suffisante, mais nom de l’instance HANA hello est toujours recommandé.

En outre, vous pouvez sauvegarder volumes\LUNs de démarrage à l’aide de hello même script. Vous devez sauvegarder votre volume de démarrage au moins une fois lorsque vous exécutez HANA pour la première fois, bien que nous recommandions une planification de sauvegarde hebdomadaire ou nocturne pour le démarrage dans cron. Plutôt que d’ajouter un nom d’instance SAP HANA, insérer _démarrage_ comme hello argument dans le script de hello comme suit :
```
./azure_hana_backup boot customer 20
```
Hello même stratégie de rétention est accordée volume de démarrage toohello également. Utiliser des instantanés à la demande, comme décrit précédemment, pour les cas spéciaux, tels que pendant une mise à niveau SAP Amélioration package (EHP), ou lorsque vous avez besoin de toocreate un instantané de stockage distinct.

Nous vous conseillons d’instantanés de stockage tooperform planifiée à l’aide de cron, et nous vous recommandons d’utiliser hello même générer un script pour toutes les sauvegardes et les besoins de récupération d’urgence (modification hello script entrées toomatch hello différents demandé des temps de sauvegarde). Ces captures sont toutes planifiées différemment dans cron selon leur durée d’exécution : toutes les heures, toutes les 12 heures, une fois par jour ou une fois par semaine. Cette planification cron Hello est conçue toocreate des instantanés de stockage qui correspondent à étiquetage de rétention hello décrit précédemment pour la sauvegarde hors site à long terme. script de Hello inclut tooback de commandes de tous les volumes de production, en fonction de leur fréquence demandée (données et fichiers journaux sont sauvegardés toutes les heures, tandis que le volume de démarrage hello est sauvegardé quotidiennement).

entrées Hello Bonjour cron script suivant exécute chaque heure dix minutes, toutes les 12 heures à hello les dix minutes et tous les jours à hello dix minutes hello. cron Hello travaux sont créés de manière à ce qu’un seul instantané de stockage SAP HANA a lieu pendant toute heure particulière, afin que hello horaires et quotidiennes des sauvegardes ne se produisent pas au hello que même moment (12:10:00). toohelp optimiser votre création de capture instantanée et la réplication, SAP HANA sur la gestion des services Azure fournit hello durée recommandée pour vous toorun vos sauvegardes.

Hello cron de valeur par défaut dans /etc/crontab de planification est la suivante :
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
Volumes HANA hello (sans le volume de démarrage) hello précédente cron pour obtenir des instructions, obtiennent un horaire instantané avec l’étiquette de hello. 66 de ces captures instantanées sont conservées. En outre, les 14 instantanés avec étiquette de 12 heures hello sont conservés. Vous obtenez potentiellement des captures instantanées toutes les heures pendant trois jours, plus des captures instantanées toutes les 12 heures pendant quatre autres jours, soit une semaine complète de captures instantanées.

Planification de cron peut être difficile, car un seul script doit être exécuté à un moment donné, à moins que les scripts de hello sont répartis en plusieurs minutes. Si vous souhaitez que les sauvegardes quotidiennes pour une rétention à long terme, un instantané quotidien est conservé avec un instantané de 12 heures (avec un nombre de rétention de sept chaque) ou instantané de toutes les heures hello est décalé tootake place 10 minutes plus tard. Un seul instantané quotidien est conservé dans le volume de production hello.
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
les fréquences Hello répertoriés ici sont des exemples uniquement. tooderive votre nombre optimal d’instantanés, hello utilisation suivant des critères :

- Exigences en matière d’objectif de délai de récupération pour une récupération dans le temps.
- Utilisation de l’espace
- Exigences en matière d’objectif de point de récupération et d’objectif de délai de récupération pour une récupération d’urgence potentielle.
- Exécution de sauvegardes de base de données complètes HANA pour les disques. Chaque fois qu’une sauvegarde complète de base de données sur des disques, ou _backint_ interface, est effectuée, l’exécution de hello d’instantanés de stockage échoue. Si vous prévoyez des sauvegardes de base de données complète tooexecute au-dessus des instantanés de stockage, assurez-vous que l’exécution de hello d’instantanés de stockage est désactivée pendant ce temps.

>[!IMPORTANT]
> utilisation de Hello d’instantanés de stockage pour les sauvegardes de SAP HANA n’est valide que lorsque les instantanés hello sont exécutées conjointement avec les sauvegardes de journaux de SAP HANA. Ces journaux hello toocover en mesure de sauvegardes besoin toobe des périodes de temps entre les instantanés de stockage hello. Si vous avez défini un toousers engagement d’une récupération limitée dans le temps de 30 jours, vous devez suivant de hello :

- Capacité tooaccess un instantané de stockage est de 30 jours.
- Sauvegardes de journaux contigus sur hello 30 derniers jours.

Dans la plage hello de sauvegardes de journaux, créer un instantané du volume de sauvegarde de journal hello également. Toutefois, être a tooperform que les sauvegardes de journaux régulières afin que vous puissiez :

- Sauvegardes de journaux contigus hello nécessité tooperform les restaurations de point-à-temps.
- Volume de journal hello SAP HANA empêche de manquer d’espace.

Une des étapes de dernière hello est tooschedule journaux de sauvegarde SAP HANA dans SAP HANA Studio. destination de cible de sauvegarde de journal de SAP HANA Hello est hello créée spécialement hana/journal\_volume de sauvegardes avec le point de montage hello de /hana/log/backups.

![Planifier les sauvegardes de journaux SAP HANA dans SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

Vous pouvez choisir d’effectuer des sauvegardes plus fréquemment que toutes les 15 minutes. Certains utilisateurs effectuent même des sauvegardes de journaux toutes les minutes, mais un intervalle _supérieur_ à 15 minutes est déconseillé.

étape finale de Hello est tooperform basée sur un fichier de sauvegarde (après l’installation initiale de hello de SAP HANA) toocreate une entrée de sauvegarde unique qui doit exister dans le catalogue de sauvegarde hello. Dans le cas contraire, SAP HANA ne peut pas lancer vos sauvegardes de journaux spécifiées.

![Créer une basée sur le fichier de sauvegarde toocreate une entrée de sauvegarde unique](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a>Analyse le nombre de hello et la taille des instantanés sur le volume de disque hello

Sur un volume de stockage particulier, vous pouvez surveiller le nombre hello d’instantanés et la consommation du stockage hello d’instantanés. Hello `ls` commande n’affiche pas hello instantané répertoire ou les fichiers. Toutefois, hello commande du système d’exploitation Linux `du` fait, avec hello suivant de commandes :

- `du –sh .snapshot`fournit un total de toutes les captures instantanées dans le répertoire de capture instantanée hello.
- `du –sh --max-depth=1`Répertorie tous les instantanés sont enregistrés dans le dossier de .snapshot hello et hello de chaque instantané.
- `du –hc`Fournit la taille totale de hello utilisé par toutes les captures instantanées.

Utilisez ces toomake commandes assurer que les instantanés hello et sont stockées ne consomment pas tout le stockage sur des volumes hello hello.

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a>Ce qui réduit le nombre hello des captures instantanées sur un serveur

Comme expliqué précédemment, vous pouvez réduire le nombre de hello de certaines étiquettes d’instantanés que vous stockez. deux paramètres de tooinitiate de commande hello une capture instantanée sont un nombre d’étiquette et hello d’instantanés que vous souhaitez que la dernière Hello tooretain.
```
./azure_hana_backup.pl lhanad01 customer 20
```
Dans l’exemple précédent de hello, étiquette de capture instantanée hello est _client_ et le numéro de hello d’instantanés avec cette toobe étiquette conservées _20_. Comme vous avez répondu toodisk la consommation d’espace, vous pourriez nombre de hello tooreduce de captures instantanées stockées. nombre de hello tooreduce d’instantanés est script de hello toorun avec hello dernier paramètre ensemble too5 facilement Hello :
```
./azure_hana_backup.pl lhanad01 customer 5
```
En raison de l’exécution du script hello avec ce paramètre, nombre de hello d’instantanés, y compris hello nouveau stockage, d’instantané est _5_.

 >[!NOTE]
 > Ce script réduit le nombre de hello d’instantanés uniquement si l’instantané précédent le plus récent hello est datant de plus d’une heure. script de Hello ne supprime pas les instantanés datant de moins d’une heure.

Ces restrictions sont les fonctionnalités de récupération d’urgence facultatif toohello connexes offertes.

Si vous ne voulez plus toomaintain un ensemble d’instantanés par ce préfixe, vous pouvez exécuter le script de hello avec _0_ comme hello rétention numéro tooremove tous les instantanés correspondant à ce préfixe. Toutefois, la suppression de tous les instantanés peut affecter fonctionnalités hello de récupération d’urgence.

### <a name="recovering-toohello-most-recent-hana-snapshot"></a>Récupération toohello instantané le plus récent HANA

En cas de hello que vous rencontrez un scénario de production vers le bas, le processus hello de récupération à partir d’un instantané de stockage peut être lancé comme un incident de client avec SAP HANA sur la gestion des services Azure. Un tel scénario d’inattendue peut être une question d’une urgence si les données ont été supprimées de production système hello seule manière et les données de salutation tooretrieve sont la base de données de production toorestore hello.

Sur hello autre part, un point-à-temps de récupération peut être faible urgence et planifié pour les jours à l’avance. Vous pouvez planifier cette récupération avec l’équipe de gestion des services SAP HANA sur Azure au lieu de signaler un problème hautement prioritaire. Par exemple, supposons que vous planifiiez tootry une mise à niveau de hello logiciel SAP en appliquant un nouveau package d’extension et vous puis devez toorevert sauvegarder instantané tooa représentant l’état avant la mise à niveau hello EHP hello.

Avant d’émettre la demande de hello, vous devez toodo certaines tâches de préparation. SAP HANA sur l’équipe de gestion des services Azure, puis gérer les demande de hello et fournir des volumes de hello restaurée. C’est par la suite, tooyou toorestore hello HANA base de données de captures instantanées de hello. Voici comment tooprepare pourquoi demander :

>[!NOTE]
>Votre interface utilisateur peut-être différer des hello suivant des captures d’écran, en fonction de hello version SAP HANA que vous utilisez.

1. Décidez quels toorestore instantané. Que le volume de données/hana hello à restaurer, sauf si vous êtes invité dans le cas contraire.

2. Arrêtez l’instance HANA hello.

 ![Arrêter hello HANA instance](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. Démontage des volumes de données hello sur chaque nœud de la base de données HANA. Hello de restauration de capture instantanée de hello échoue si les volumes de données hello ne sont pas démontés.

 ![Démontage des volumes de données hello sur chaque nœud de la base de données HANA](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. Ouvrez une restauration hello de prise en charge Azure demande tooinstruct d’un instantané spécifique.

 - Pendant la restauration de hello : SAP HANA sur la gestion des services Azure peut vous demander tooattend un tooensure de téléconférence aucune donnée n’est perdue.

 - Après la restauration de hello : SAP HANA sur la gestion des services Azure vous avertit de capture instantanée de stockage hello a été restaurée.

5. Une fois le processus de restauration hello terminée, remontez tous les volumes de données.

 ![Remonter tous les volumes de données](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. Sélectionnez les options de récupération SAP HANA Studio, si elles ne sont pas automatiquement fournies lorsque vous vous reconnectez tooHANA DB via SAP HANA Studio. Hello suivant montre un restauration toohello HANA l’instantané. Un instantané du stockage incorpore un seul instantané HANA, et si vous restaurez le dernier instantané de stockage toohello, il doit être instantané HANA hello le plus récent. (Si vous restaurez tooolder des instantanés de stockage, vous devez toolocate hello HANA en fonction de l’instantané stockage hello hello instantané.)

 ![Sélectionner les options de récupération dans SAP HANA Studio](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. Sélectionnez **restauration hello tooa spécifique de données sauvegarde ou stockage instantané**.

 ![fenêtre de « Type de récupération spécifier » Hello](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. Sélectionnez l’option de **spécification d’une sauvegarde sans catalogue**.

 ![fenêtre de « Emplacement de sauvegarde spécifier » Hello](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. Bonjour **le Type de Destination** liste, sélectionnez **instantané**.

 ![fenêtre de « Spécifier hello sauvegarde tooRecover » Hello](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. Cliquez sur **Terminer** processus de récupération toostart hello.

 ![Cliquez sur « Terminer » le processus de récupération de hello toostart](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. base de données HANA Hello est restaurée et récupérée d’instantané HANA toohello qui est inclus dans l’instantané de stockage hello.

 ![Base de données HANA est instantané HANA toohello restaurée et récupérée](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a>Récupérez l’état le plus récent toohello

Hello processus suivant restaure hello HANA snapshot qui est inclus dans l’instantané de stockage hello. Il restaure ensuite hello transaction journal sauvegardes toohello état le plus récent de la base de données hello avant de restaurer l’instantané du stockage hello.

>[!IMPORTANT]
>Avant de poursuivre, assurez-vous que vous disposez d’une chaîne complète et contiguë de sauvegardes de journaux des transactions. Sans ces sauvegardes, vous ne pouvez pas restaurer l’état actuel de hello de base de données hello.

1. Les étapes 1 à 6 de hello précédant la procédure dans « Recovering toohello HANA instantané le plus récent. »

2. Sélectionnez **récupérer l’état le plus récent hello de base de données tooits**.

 ![Sélectionnez « Restaurer l’état le plus récent hello de base de données tooits »](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. Spécifier l’emplacement hello hello plus récent HANA de sauvegardes de journaux. emplacement de Hello doit toocontain toutes les sauvegardes de journal des transactions HANA à partir de l’état le plus récent hello HANA instantané toohello.

 ![Spécifier l’emplacement de hello hello plus récent HANA de sauvegardes de journaux](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. Sélectionnez une sauvegarde comme base à partir de la base de données toorecover hello. Dans notre exemple, il s’agit d’instantané HANA hello qui était inclus dans l’instantané de stockage hello. (Un seul instantané est répertorié Bonjour suivant capture d’écran).

 ![Sélectionner une sauvegarde comme base à partir de la base de données qui hello toorecover](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. Désactivez hello **utiliser les sauvegardes Delta** case à cocher si deltas n’existent pas entre hello instantané HANA hello et état le plus récent hello.

 ![Désactivez hello « Utiliser les sauvegardes Delta » case à cocher si aucun deltas n’existe](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. Dans l’écran de résumé hello, cliquez sur **Terminer** procédure de restauration toostart hello.

 ![Cliquez sur « Terminer » sur l’écran de résumé hello](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a>Récupération point tooanother dans le temps
point de tooa toorecover dans le temps entre l’instantané HANA hello (inclus dans l’instantané de stockage hello) et l’autre est postérieure à la récupération de point-à-temps, de capture instantanée hello HANA hello suivant :

1. Assurez-vous que vous disposez de toutes les sauvegardes de journaux de transaction de hello HANA instantané toohello pendant laquelle vous souhaitez que toorecover.
2. Commencer la procédure hello sous « Recovering toohello état le plus récent. »
3. Dans l’étape 2 de la procédure hello, Bonjour **spécifier le Type de récupération** fenêtre, sélectionnez **suivant de toohello de base de données de récupération hello point dans le temps**, spécifiez hello point dans le temps, puis effectuez les étapes 3 à 6.

## <a name="monitoring-hello-execution-of-snapshots"></a>Surveillance de l’exécution de hello d’instantanés

Vous avez besoin de l’exécution de hello toomonitor d’instantanés de stockage. script Hello qui exécute un instantané du stockage écrit le fichier de sortie tooa, puis l’enregistre toohello même emplacement que les scripts Perl hello. Un fichier distinct est créé pour chaque capture instantanée. sortie Hello de chaque fichier montre clairement hello différentes phases hello instantané s’exécute :

- Recherche d’un instantané de volumes hello nécessitant toocreate
- Recherche d’instantanés hello obtenues à partir de ces volumes.
- La suppression éventuelle existant instantanés toomatch hello nombre d’instantanés que vous avez spécifié
- Création d’une capture instantanée HANA
- Création d’instantanés de stockage hello sur les volumes de hello
- Suppression hello HANA instantané
- Changement de nom hello plus récente d’instantanés trop**.0**

étape la plus importante du script de hello Hello est la suivante :
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
À partir de cet exemple, vous pouvez voir comment les enregistrements de script hello hello la création de hello HANA instantané. Dans les cas de montée en puissance parallèle hello, ce processus est lancé sur le nœud principal de hello. nœud maître de Hello lance la création de synchrone de hello d’instantanés hello sur chacun des nœuds de travail hello. Instantané de stockage hello est extraite. Après l’exécution réussie de hello d’instantanés de stockage hello, instantané HANA hello est supprimé.
