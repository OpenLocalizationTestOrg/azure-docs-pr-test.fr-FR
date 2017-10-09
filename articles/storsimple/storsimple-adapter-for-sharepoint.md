---
title: aaaInstall adaptateur StorSimple pour SharePoint | Documents Microsoft
description: "Décrit comment tooinstall et configurer ou supprimer hello adaptateur StorSimple pour SharePoint dans une batterie de serveurs SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Installer et configurer hello adaptateur StorSimple pour SharePoint
## <a name="overview"></a>Vue d'ensemble
Hello adaptateur StorSimple pour SharePoint est un composant qui vous permet de fournir un stockage Microsoft Azure StorSimple flexible et batteries de serveurs de tooSharePoint de protection des données. Vous pouvez utiliser le contenu d’objet BLOB (Binary Large) hello adaptateur toomove de périphérique de stockage cloud toohello Microsoft Azure StorSimple hybride hello SQLServer : bases de données de contenu.

Hello adaptateur StorSimple pour SharePoint fonctionne comme un fournisseur de stockage d’objets BLOB distants (RBS) et utilise hello toostore de fonctionnalité de stockage d’objets BLOB distants SQL Server contenu SharePoint non structuré (sous forme de hello d’objets BLOB) sur un serveur de fichiers qui est sauvegardé par un appareil StorSimple.

> [!NOTE]
> Hello adaptateur StorSimple pour SharePoint prend en charge le stockage d’objets BLOB distant (RBS) SharePoint Server 2010. Il ne prend pas en charge SharePoint Server 2010 External BLOB Storage (EBS).


* hello de toodownload l’adaptateur StorSimple pour SharePoint, accédez trop[l’adaptateur StorSimple pour SharePoint] [ 1] Bonjour Microsoft Download Center.
* Pour plus d’informations sur la planification de RBS et RBS limitations, consultez trop[décider toouse RBS dans SharePoint 2013] [ 2] ou [planifier RBS (SharePoint Server 2010)] [3].

Hello reste de cette vue d’ensemble décrit brièvement rôle hello de hello adaptateur StorSimple pour SharePoint et hello capacité de SharePoint et des limites de performances que vous devez être conscient d’avant d’installer et configurer l’adaptateur hello. Après avoir pris connaissance de ces informations, consultez trop[l’adaptateur StorSimple pour l’installation de SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin configuration de l’adaptateur hello.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Avantages de StorSimple Adapter for SharePoint
Dans un site SharePoint, le contenu est stocké comme des données BLOB non structurées dans une ou plusieurs bases de données de contenu. Par défaut, ces bases de données sont hébergées sur les ordinateurs qui exécutent SQL Server et se trouvent dans la batterie de serveurs SharePoint hello. Les objets blob peuvent rapidement augmenter en taille, consommant ainsi une grande quantité de stockage local. Pour cette raison, vous pourriez toofind solution de stockage moins onéreuse un autre. SQL Server fournit une technologie appelée l’objet Blob de stockage distants (RBS) qui vous permet de stocker le contenu de l’objet BLOB dans le système de fichiers hello, en dehors de la base de données SQL Server hello. Avec RBS, objets BLOB peuvent résider dans le système de fichiers hello hello sur ordinateur sur lequel SQL Server est en cours d’exécution, ou qu’elles puissent être stockées dans le système de fichiers hello sur un autre serveur.

RBS nécessite que vous utilisez un fournisseur RBS, par exemple hello adaptateur StorSimple pour SharePoint, tooenable RBS dans SharePoint. Hello adaptateur StorSimple pour SharePoint fonctionne avec RBS, vous permettant de déplacer server de tooa d’objets BLOB sauvegardé par le système de Microsoft Azure StorSimple hello. Microsoft Azure StorSimple stocke ensuite les données d’objet BLOB hello localement ou dans le cloud de hello, basée sur l’utilisation. Objets BLOB très actifs (généralement référencé tooas niveau 1 ou des données à chaud) résident localement. Les données moins sollicitées et les données résident dans le cloud de hello. Une fois que vous activez RBS sur une base de données de contenu, tout nouveau contenu BLOB créé dans SharePoint est stocké sur l’appareil StorSimple hello et non dans la base de données de contenu hello.

implémentation de Microsoft Azure StorSimple Hello de RBS offre hello avantages suivants :

* Par déplacement BLOB tooa contenu distinct d’un serveur, vous pouvez réduire la charge de requête de hello sur SQL Server, ce qui peut améliorer la réactivité de SQL Server. 
* Azure StorSimple utilise la déduplication et compression de la taille des données tooreduce.
* Azure StorSimple assure la protection des données dans l’écran hello locaux et les instantanés cloud. En outre, si vous placez la base de données hello lui-même sur l’appareil StorSimple hello, vous pouvez sauvegarder la base de données de contenu hello et les objets BLOB ensemble dans un moyen cohérent d’incident. (Déplacement hello contenu de la base de données toohello est uniquement pris en charge pour l’appareil de série StorSimple 8000 hello. Cette fonctionnalité n'est pas prise en charge pour la série de hello 5000 ou 7000.)
* Azure StorSimple inclut des fonctionnalités de récupération d'urgence, notamment le basculement, la récupération de fichier et de volume (y compris une récupération test) et la restauration rapide des données.
* Vous pouvez utiliser le logiciel de récupération de données, tels que Kroll Ontrack PowerControls, avec des instantanés StorSimple BLOB tooperform au niveau de l’élément de récupération de données de contenu SharePoint. (Ce logiciel de récupération des données est vendu séparement).
* Hello adaptateur StorSimple pour SharePoint connecte au portail d’Administration centrale de SharePoint hello, ce qui vous toomanage à votre solution SharePoint à partir d’un emplacement central.

Déplacement de système de fichiers BLOB toohello contenu peut fournir des autres économies et les avantages. Par exemple, à l’aide de RBS peut réduire les besoins hello onéreux de niveau 1 et, car il réduit la base de données de contenu hello, RBS peut réduire nombre hello des bases de données requis dans la batterie de serveurs SharePoint hello. Toutefois, les autres facteurs, tels que les limites de taille de base de données et de la quantité de hello de contenu non RBS, peuvent également affecter des besoins de stockage. Pour plus d’informations sur les coûts de hello et avantages de l’utilisation de RBS, consultez [planifier RBS (SharePoint Foundation 2010)] [ 4] et [décider toouse RBS dans SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limites de capacité et de performances
Avant d’envisager l’utilisation de RBS dans votre solution SharePoint, vous devez connaître de hello testé performances et les limites de capacité de SharePoint Server 2010 et SharePoint Server 2013, et comment ces limites sont reliés les performances de tooacceptable. Pour plus d'informations, consultez la rubrique [Limites des logiciels et limites pour SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Consultez les rubriques suivantes de hello avant de configurer RBS :

* Assurez-vous que cette taille totale hello Hello contenu (taille hello d’une base de données) et de la taille de hello de n’importe quel externalisés associés ne dépasse pas la limite de taille RBS hello pris en charge par SharePoint. Cette limite est de 200 Go. 
  
    **base de données de contenu toomeasure et taille des objets BLOB**
  
  1. Exécutez cette requête sur hello WFE d’Administration centrale. Démarrer hello SharePoint Management Shell et entrez hello suivant la taille de hello de tooget de commande Windows PowerShell de bases de données de contenu hello :
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Cette étape Obtient la taille hello de base de données de contenu hello sur le disque de hello.
  2. Exécutez une des hello suivant des requêtes SQL dans SQL Management Studio sur boîte hello SQL server sur chaque base de données de contenu et ajoutez le nombre de toohello hello résultat obtenu à l’étape 1.
     
     Dans les bases de données de contenu SharePoint 2013, entrez :
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     Dans les bases de données de contenu SharePoint 2010, entrez :
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Cette étape Obtient la taille hello Hello objets BLOB qui ont été externalisées.
* Nous vous recommandons de stocker tout le contenu BLOB et base de données localement sur l’appareil StorSimple hello. l’appareil StorSimple Hello est un cluster à deux nœuds pour la haute disponibilité. Placement des bases de données de contenu hello et des objets BLOB sur l’appareil StorSimple hello offre une haute disponibilité.
  
    Utilisez traditionnel SQL Server migration meilleures pratiques toomove hello contenu de la base de données toohello appareil StorSimple. Déplacer la base de données hello uniquement une fois que tout le contenu à partir de la base de données hello BLOB a été déplacé toohello partage de fichiers via RBS. Si vous choisissez l’appareil StorSimple toohello toomove hello contenu de la base de données, nous vous recommandons de configurer stockage de base de données de contenu hello sur périphérique hello comme volume principal.
* Dans Microsoft Azure StorSimple, si vous utilisez des volumes hiérarchisés, il n’existe aucun moyen tooguarantee contenu stocké localement sur l’appareil StorSimple hello ne sera pas tooMicrosoft hiérarchisé stockage cloud Azure. Par conséquent, nous recommandons d’utiliser des volumes StorSimple épinglés localement conjointement avec SharePoint RBS. Cela garantit que tout le contenu BLOB reste localement sur l’appareil StorSimple hello et n’est pas déplacé tooMicrosoft Azure.
* Si vous ne stockez pas les bases de données de contenu hello sur l’appareil StorSimple hello, utilisez traditionnel SQL Server haute disponibilité meilleures pratiques qui prennent en charge RBS. La gestion de clusters SQL Server prend en charge RBS, ce qui n’est pas le cas de la mise en miroir SQL Server. 

> [!WARNING]
> Si vous n’avez pas activé RBS, il est déconseillé de déplacement de l’appareil StorSimple hello contenu de la base de données toohello. Il s'agit d'une configuration non testée.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Installation de StorSimple Adapter for SharePoint
Avant de pouvoir installer hello adaptateur StorSimple pour SharePoint, vous devez configurer l’appareil StorSimple hello et vérifiez que la batterie de serveurs SharePoint hello et l’instanciation de SQL Server remplissent toutes les conditions préalables. Ce didacticiel décrit la configuration requise, ainsi que les procédures d’installation et de mise à niveau de hello adaptateur StorSimple pour SharePoint.

## <a name="configure-prerequisites"></a>Configuration préalable requise
Avant de pouvoir installer hello adaptateur StorSimple pour SharePoint, assurez-vous que l’appareil StorSimple hello, batterie de serveurs SharePoint et l’instanciation de SQL Server répondent aux hello suivant des conditions préalables.

### <a name="system-requirements"></a>Conditions requises pour le système
Hello adaptateur StorSimple pour SharePoint fonctionne avec hello suivant les configurations matérielle et logicielle :

* Système d’exploitation pris en charge – Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2
* Versions SharePoint prises en charge – SharePoint Server 2010 ou SharePoint Server 2013
* Versions SQL Server prises en charge – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition ou SQL Server 2012 Enterprise Edition
* Appareils StorSimple pris en charge – StorSimple série 8000, StorSimple série 7000 ou StorSimple série 5000.

### <a name="storsimple-device-configuration-prerequisites"></a>Conditions préalables à la configuration de l’appareil StorSimple
l’appareil StorSimple Hello est un périphérique de bloc et doit donc utiliser un serveur de fichiers sur lequel les données de salutation peuvent être hébergées. Nous vous recommandons d’utiliser un serveur distinct plutôt que sur un serveur existant à partir de la batterie de serveurs SharePoint hello. Ce serveur de fichiers doit être sur hello même réseau local (LAN) en tant qu’ordinateur de SQL Server hello qui hôtes hello contenu bases de données.

> [!TIP]
> * Si vous configurez votre batterie de serveurs SharePoint pour la haute disponibilité, vous devez déployer le serveur de fichiers hello pour la haute disponibilité également.
> * Si vous ne stockez pas la base de données de contenu hello sur l’appareil StorSimple hello, utilisez traditionnel haute disponibilité meilleures pratiques qui prennent en charge RBS. La gestion de clusters SQL Server prend en charge RBS, ce qui n’est pas le cas de la mise en miroir SQL Server. 


Assurez-vous que votre appareil StorSimple est correctement configuré et que toosupport des volumes votre déploiement SharePoint sont configurés et sont accessibles à partir de votre ordinateur SQL Server. Accédez trop[déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md) si vous n’avez pas encore déployé et configuré votre périphérique StorSimple. Notez l’adresse IP de hello de l’appareil StorSimple hello ; vous en aurez besoin lors de l’adaptateur StorSimple pour l’installation de SharePoint.

En outre, assurez-vous que toobe de volume hello utilisé pour l’externalisation des objets BLOB remplit hello suivant les exigences :

* volume de Hello doit être formaté avec une taille d’unité d’allocation de 64 Ko.
* Votre serveur web frontal (WFE) et les serveurs d’applications doivent être en mesure de tooaccess des volumes de hello via un chemin d’accès UNC Universal Naming Convention ().
* batterie de serveurs SharePoint Hello doit être configuré toowrite toohello volume.

> [!NOTE]
> Une fois que vous installez et configurez l’adaptateur hello, externalisation des objets BLOB doit passer par l’appareil StorSimple hello (appareil de hello présenter hello volumes tooSQL serveur et gérer les niveaux de stockage hello). Vous ne pouvez pas utiliser d'autres cibles pour l'externalisation blob.


Si vous envisagez de toouse Gestionnaire d’instantanés StorSimple tootake instantanés Hello BLOB et que vous la base de données des données, être tooinstall que gestionnaire d’instantanés StorSimple sur le serveur de base de données hello afin qu’il puisse utiliser hello tooimplement de Service SQL Writer hello Windows Volume Shadow Copy Service (VSS).

> [!IMPORTANT]
> Gestionnaire d’instantanés StorSimple ne prend pas en charge hello enregistreur VSS de SharePoint et ne peut pas prendre des instantanés cohérents au niveau applicatif des données SharePoint. Dans un scénario SharePoint, StorSimple Snapshot Manager fournit uniquement des sauvegardes cohérentes après incident.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Conditions préalables à la configuration d’une batterie de serveurs SharePoint
Assurez-vous que votre batterie de serveurs SharePoint est correctement configurée, comme suit :

* Vérifiez que votre batterie de serveurs SharePoint est dans un état sain et vérifiez hello suivantes :
* Tous les serveurs WFE SharePoint et serveurs d’applications inscrits dans la batterie de serveurs hello sont en cours d’exécution et peuvent être exécutée sur serveur hello sur lequel vous allez installer hello adaptateur StorSimple pour SharePoint.
* Hello service du minuteur SharePoint (SPTimerV3 ou SPTimerV4) est en cours d’exécution sur chaque serveur Web frontal et le serveur d’applications.
* À la fois hello service du minuteur SharePoint et pool d’applications IIS hello sous lequel hello Administration centrale de SharePoint site est en cours d’exécution ont des privilèges d’administrateur.
* Assurez-vous que Internet Explorer Enhanced Security Context (IE ESC) est désactivé. Suivez ces étapes de toodisable IE ESC :
  
  1. Fermez toutes les instances d'Internet Explorer.
  2. Hello de démarrer le Gestionnaire de serveur.
  3. Dans le volet gauche de hello, cliquez sur **serveur Local**.
  4. Sur hello avec le bouton droit volet, ensuite trop**la Configuration de sécurité renforcée d’Internet Explorer**, cliquez sur **sur**.
  5. Sous **Administrateurs**, cliquez sur **Désactivé**.
  6. Cliquez sur **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Conditions préalables pour Remote BLOB Storage (RBS)
Assurez-vous que vous utilisez une version SQL Server prise en charge. Uniquement hello versions suivantes sont prises en charge et en mesure de toouse RBS :

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

Objets BLOB peut être externalisés que sur uniquement les volumes hello unité StorSimple présente tooSQL Server. Aucune autre cible n'est prise en charge pour l’externalisation blob.

Lorsque vous avez terminé toutes les étapes de configuration requise, consultez trop[hello d’installation de l’adaptateur StorSimple pour SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Installer hello adaptateur StorSimple pour SharePoint
Utilisez hello suivant les étapes tooinstall hello adaptateur StorSimple pour SharePoint. Si vous réinstallez le logiciel de hello, consultez [mise à niveau ou réinstaller hello adaptateur StorSimple pour SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). temps Hello requis pour l’installation de hello dépend du nombre total de hello de bases de données SharePoint dans votre batterie de serveurs SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Configuration de RBS
Après avoir installé hello adaptateur StorSimple pour SharePoint, configurer RBS, comme décrit dans la procédure de hello.

> [!TIP]
> Hello adaptateur StorSimple pour SharePoint s’intègre dans la page de l’Administration centrale de SharePoint de hello, ce qui permet de RBS toobe activés ou désactivés sur chaque base de données contenu dans la batterie de serveurs SharePoint hello. Toutefois, l’activation ou la désactivation de RBS sur la base de données de contenu hello entraîne une réinitialisation d’IIS, qui, selon votre configuration de batterie de serveurs, peut interrompre momentanément la disponibilité de hello hello SharePoint web frontal (WFE). (Les facteurs tels que hello utilisation d’un équilibrage de charge frontal, la charge de travail de serveur actuelle hello et ainsi de suite, peuvent limiter ou cette indisponibilité.) tooprotect les utilisateurs à partir d’une interruption de service, nous vous recommandons d’activer ou de désactiver RBS uniquement durant une fenêtre de maintenance planifiée.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Configuration du nettoyage de mémoire
Lorsque les objets sont supprimés à partir d’un site SharePoint, ils ne sont pas automatiquement supprimés de hello volume de stockage RBS. Au lieu de cela, un asynchrone, programme de maintenance en arrière-plan supprime des objets BLOB orphelins de magasin de fichiers hello. Administrateurs système peuvent planifier ce processus toorun régulièrement ou ils peuvent démarrer chaque fois que nécessaire.

Ce programme de maintenance (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) est automatiquement installé sur tous les serveurs WFE SharePoint et serveurs d'applications lorsque vous activez RBS. programme de Hello est installé dans hello l’emplacement suivant : *lecteur de démarrage*: \Program Files\Microsoft stockage d’objets Blob distants SQL 10.50\Maintainer\

Pour plus d’informations sur la configuration et à l’aide du programme de maintenance hello, consultez [mettre à jour de RBS dans SharePoint Server 2013][8].

> [!IMPORTANT]
> programme de chargé de maintenance RBS Hello est gourmande en ressources. Vous devez la planifier toorun uniquement pendant les périodes de faible activité sur la batterie de serveurs SharePoint hello.


### <a name="delete-orphaned-blobs-immediately"></a>Suppression immédiate des objets blob orphelins
Si vous devez immédiatement toodelete orphelin BLOB, vous pouvez utiliser hello suivant les instructions. Notez que ces instructions sont un exemple de comment cela peut être fait dans un environnement SharePoint 2013 avec hello suivant des composants :

* nom de base de données de contenu Hello est WSS_Content.
* nom du serveur SQL Hello est SHRPT13-SQL12\SHRPT13.
* nom de l’application web Hello est SharePoint – 80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Mettre à niveau ou réinstaller hello adaptateur StorSimple pour SharePoint
Utilisez hello suivant SharePoint server tooupgrade de procédure et puis réinstallez l’adaptateur StorSimple pour la mise à niveau de SharePoint ou toosimply ou adaptateur hello dans une batterie de serveurs SharePoint existante.

> [!IMPORTANT]
> Passez en revue les informations suivantes avant de tenter de tooupgrade de hello vos logiciels SharePoint et/ou de la mise à niveau ou réinstaller hello adaptateur StorSimple pour SharePoint :
> 
> * Tous les fichiers qui ont été préalablement déplacés de stockage tooexternal via RBS ne seront pas disponible jusqu'à la fin de la réinstallation de hello et hello fonctionnalité RBS est activé. toolimit utilisateur impact, toute mise à niveau ou la réinstallation pendant une fenêtre de maintenance planifiée.
> * Durée Hello pour hello mise à niveau/réinstallation peut varier en fonction du nombre total de hello de bases de données SharePoint dans la batterie de serveurs SharePoint hello.
> * Une fois hello mise à niveau/réinstallation terminée, vous devez tooenable RBS pour les bases de données de contenu hello. Consultez [Configuration de RBS](#configure-rbs) pour plus d'informations.
> * Si vous configurez RBS pour une batterie de serveurs SharePoint qui possède un très grand nombre de bases de données (plus de 200), hello **Administration centrale de SharePoint** page peut expirer. Si cela se produit, actualisez la page de hello. Cela n’affecte pas le processus de configuration hello.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Suppression de StorSimple Adapter pour SharePoint
Hello procédures suivantes décrire comment toomove hello BLOB sauvegarde les bases de données toohello SQL Server, puis désinstallez hello adaptateur StorSimple pour SharePoint. 

> [!IMPORTANT]
> Vous avez toomove hello BLOB toohello précédent contenus bases de données avant de désinstaller le logiciel de l’adaptateur hello.


### <a name="before-you-begin"></a>Avant de commencer
Collecter hello informations suivantes avant de déplacer les données de salutation sauvegarder les bases de données de contenu de SQL Server toohello et commencent le processus de suppression de carte hello :

* Hello les noms de toutes les bases de données hello pour lesquelles RBS est activé.
* chemin d’accès UNC de Hello Hello configuré le magasin d’objets BLOB

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Déplacer hello BLOB toohello arrière bases de données
Avant de désinstaller hello adaptateur StorSimple pour le logiciel SharePoint, vous devez migrer tous hello objets BLOB qui ont été externalisés toohello précédent contenus bases de données SQL. Si vous essayez de toouninstall hello adaptateur StorSimple pour SharePoint avant de déplacer toutes les bases contenus hello BLOB toohello arrière, hello message d’avertissement suivant s’affiche.

![Message d'avertissement](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove hello BLOB toohello précédent contenus bases de données
1. Chacun des objets de hello externalisé télécharger.
2. Ouvrez hello **Administration centrale de SharePoint** page et parcourir trop**paramètres système**.
3. Sous **Azure StorSimple**, cliquez sur **Configuration de l'adaptateur StorSimple**.
4. Sur hello **configurer l’adaptateur StorSimple** , cliquez sur hello **désactiver** situé sous chacune des bases de données contenu hello que vous souhaitez tooremove à partir du stockage d’objets BLOB externe. 
5. Supprimer les objets hello à partir de SharePoint et les télécharger à nouveau.

Vous pouvez également utiliser hello Microsoft` RBS Migrate()` applet de commande PowerShell inclus avec SharePoint. Pour plus d'informations, consultez [Migration du contenu vers ou à partir de RBS](https://technet.microsoft.com/library/ff628255.aspx).

Après le déplacement de base de données contenu hello BLOB toohello précédent, atteindre l’étape suivante de toohello : [désinstaller l’adaptateur hello](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Désinstaller l’adaptateur hello
Après avoir déplacé hello BLOB toohello précédent contenus bases de données SQL, utilisez une des hello suivant options toouninstall hello adaptateur StorSimple pour SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>carte de toouse hello installation programme toouninstall hello
1. Utilisez un compte avec toolog de privilèges d’administrateur sur le serveur toohello web frontal (WFE).
2. Double-cliquez sur hello adaptateur StorSimple pour le programme d’installation de SharePoint. Hello Assistant Installation démarre.
   
    ![Assistant d'installation](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Cliquez sur **Suivant**. Hello suivant page s’affiche.
   
    ![Page de suppression de l'Assistant d'installation](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Cliquez sur **supprimer** processus de suppression tooselect hello. Hello suivant page s’affiche.
   
    ![Page de confirmation de l'Assistant d'installation](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Cliquez sur **supprimer** la suppression de tooconfirm hello. Hello suivant page de progression s’affiche.
   
    ![Page de progression de l'Assistant d'installation](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Lors de la suppression de hello est terminée, la page Terminer de hello s’affiche. Cliquez sur **Terminer** tooclose hello Assistant installation.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>adaptateur hello toouninstall toouse hello le panneau de configuration
1. Ouvrez le panneau de configuration de hello, puis cliquez sur **programmes et fonctionnalités**.
2. Sélectionnez **StorSimple Adapter pour SharePoint**, puis cliquez sur **Désinstaller**.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx
