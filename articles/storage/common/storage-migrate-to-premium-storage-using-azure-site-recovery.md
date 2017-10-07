---
title: "aaaMigrating tooAzure stockage Premium à l’aide d’Azure Site Recovery (disques non managés) | Documents Microsoft"
description: "Migrez votre tooAzure d’ordinateurs virtuels existants stockage Premium à l’aide de la récupération de Site (disques non managés)."
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: 2c82fffaa38baeeb4a676748125bd85d6e0500f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery-unmanaged-disks"></a>Migration tooPremium de stockage à l’aide d’Azure Site Recovery (disques non managées)

Le [stockage Premium Azure](storage-premium-storage.md) offre une prise en charge des disques haute performance et à faible latence pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S. Hello de ce guide vise toohelp utilisateurs migrent leurs disques de machine virtuelle à partir d’un tooa de compte de stockage Standard dans un compte de stockage Premium à l’aide de [Azure Site Recovery](../../site-recovery/site-recovery-overview.md).

Récupération de site est un service Azure qui contribue tooyour continuité et la stratégie de récupération d’urgence en coordonnant hello réplication des serveurs physiques locaux et les machines virtuelles toohello cloud (Azure) ou centre de données secondaire tooa. En cas de pannes dans votre emplacement principal, vous basculez les applications tookeep toohello emplacement secondaire et les charges de travail disponibles. Vous ne parvenez pas emplacement principal d’arrière tooyour lorsqu’elle retourne toonormal opération. Récupération de site fournit des exercices de récupération d’urgence toosupport basculements de test sans affecter les environnements de production. Vous pouvez exécuter des basculements avec une perte de données minimale (en fonction de la fréquence de réplication) pour les sinistres inattendus. Dans le scénario hello de migration tooPremium stockage, vous pouvez utiliser hello [basculement en mode de récupération de Site](../../site-recovery/site-recovery-failover.md) dans Azure Site Recovery toomigrate cible disques tooa compte de stockage Premium.

Nous vous recommandons de migrer tooPremium stockage à l’aide de récupération de Site, car cette option fournit un temps mort minimal et permet d’éviter l’exécution manuelle de hello de copie de disques et de création de nouveaux ordinateurs virtuels. Site Recovery copie systématiquement vos disques et crée de nouvelles machines virtuelles pendant le basculement. Site Recovery prend en charge différents types de basculement avec très peu de temps d'arrêt ou aucun temps d'arrêt. tooplan la perte de données de temps d’arrêt et l’estimation, consultez hello [Types de basculement](../../site-recovery/site-recovery-failover.md) table en cours de récupération de Site. Si vous [préparer des ordinateurs virtuels de tooAzure tooconnect après le basculement](../../site-recovery/vmware-walkthrough-overview.md), vous devez être en mesure de tooconnect toohello machine virtuelle Azure à l’aide du protocole RDP après le basculement.

![][1]

## <a name="azure-site-recovery-components"></a>Composants Azure Site Recovery

Il s’agit de composants de Site Recovery hello qui sont pertinentes toothis de scénario de migration.

* Un **serveur de configuration** est une machine virtuelle Azure qui coordonne la communication et gère les processus de réplication et de récupération des données. Sur cet ordinateur virtuel, vous allez exécuter un serveur de configuration d’installation unique fichier tooinstall hello et un composant supplémentaire, appelé serveur de processus, comme une passerelle de réplication. En savoir plus sur la [configuration requise du serveur](../../site-recovery/vmware-walkthrough-overview.md). Serveur de configuration seulement doit toobe configuré qu’une seule fois et peut être utilisé pour toutes les migrations toohello même région.

* **Serveur de processus** une passerelle de réplication qui reçoit les données de réplication à partir de la source de machines virtuelles optimise les données hello avec la mise en cache, la compression et le chiffrement, et il envoie le compte de stockage tooa. Il gère l’installation push du toosource de service hello mobilité des machines virtuelles et effectue une détection automatique de la source de machines virtuelles. serveur de processus par défaut Hello est installé sur le serveur de configuration hello. Vous pouvez déployer tooscale de serveurs de processus autonomes supplémentaires à votre déploiement. En savoir plus sur les [meilleures pratiques de déploiement de serveur de processus](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) et le [déploiement de serveurs de processus supplémentaires](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Serveur de traitement seulement doit toobe configuré qu’une seule fois et peut être utilisé pour toutes les migrations toohello même région.

* **Service de mobilité** est un composant qui est déployé sur chaque machine virtuelle standard vous souhaitez tooreplicate. Il capture les écritures de données hello standard pour machine virtuelle et les transfère un serveur de processus toohello. En savoir plus sur la [configuration requise pour les machines répliquées](../../site-recovery/vmware-walkthrough-overview.md).

Ce graphique montre comment ces composants interagissent.

![][15]

> [!NOTE]
> Récupération de site ne prend pas en charge la migration hello de disques des espaces de stockage.

Pour obtenir des composants supplémentaires pour d’autres scénarios, consultez trop[architecture du scénario](../../site-recovery/vmware-walkthrough-overview.md).

## <a name="azure-essentials"></a>Éléments principaux d’Azure

Ceux-ci sont hello exigences d’Azure pour ce scénario de migration.

* Un abonnement Azure
* Un toostore de compte de stockage Azure Premium des données répliquées
* Un réseau virtuel Azure (VNet) de toowhich machines virtuelles se connecte lorsqu’elles sont créées lors du basculement. réseau virtuel Azure Hello doit être dans hello même région que hello un dans le hello Site Recovery s’exécute
* Un compte de stockage Azure Standard dans les journaux de réplication toostore. Il peut s’agir hello même compte de stockage comme des disques hello machine virtuelle en cours de migration

## <a name="prerequisites"></a>Composants requis

* Comprendre les composants du scénario de migration pertinentes hello Bonjour précédant la section
* Planifier le temps mort par apprentissage sur hello [basculement en mode de récupération de Site](../../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Configuration et étapes de la migration

Vous pouvez utiliser la récupération de Site toomigrate machines virtuelles Azure IaaS entre régions ou au sein de la même région. Hello instructions suivantes ont été adaptées pour ce scénario de migration à partir de l’article de hello [répliquer des machines virtuelles VMware ou serveurs physiques tooAzure](../../site-recovery/vmware-walkthrough-overview.md). Veuillez suivre les liens de hello pour les étapes détaillées dans les instructions toohello supplémentaires dans cet article.

1. **Créer un coffre Recovery Services**. Créer et gérer le coffre Site Recovery hello via hello [portail Azure](https://portal.azure.com). Cliquez sur **Nouveau** > **Gestion** > **Sauvegarde** et **Récupération de sites (OMS)**. Vous pouvez également sélectionner **Parcourir** > **Coffres Recovery Services** > **Ajouter**. Machines virtuelles seront région répliquées toohello que vous spécifiez dans cette étape. Pour les besoins de hello de migration Bonjour même région, région de hello sélectionnez où se trouvent vos machines virtuelles source et les comptes de stockage source. 

2. Hello étapes suivantes vous aider à **Choisissez vos objectifs de protection**.

    2a. Sur hello où vous souhaitez que le serveur de configuration de hello de tooinstall de machine virtuelle, ouvrez hello [portail Azure](https://portal.azure.com). Accédez trop**les coffres de Services de récupération** > **paramètres**. Sous **Paramètres**, sélectionnez **Site Recovery**. Sous **Site Recovery**, sélectionnez **Étape 1 : Préparez l'infrastructure**. Sous **Préparer l'infrastructure**, sélectionnez **Objectif de protection**.

    ![][2]

    2b. Sous **objectif de Protection**hello la première liste déroulante, dans Sélectionnez **tooAzure**. Dans la liste déroulante de la deuxième hello, sélectionnez **non virtualisé,**, puis cliquez sur **OK**.

    ![][3]

3. Hello étapes suivantes vous aider à **configurer hello source environnement (serveur de configuration)**.

    3a. Télécharger hello **installation unifiée d’Azure Site Recovery** et hello **clé d’inscription du coffre** par va de toohello **Prepare infrastructure**  >  **Préparation source** > **ajouter un serveur** panneau. Vous devez hello le programme d’installation de coffre d’enregistrement clé toorun hello unifiée. clé de Hello est valide pendant 5 jours après que l’avoir généré.

    ![][4]

    3b. Ajouter un serveur de Configuration Bonjour **ajouter un serveur** panneau.

    ![][5]

    3c. Sur hello machine virtuelle que vous utilisez en tant que serveur de configuration hello, exécutez le serveur de configuration de hello tooinstall le programme d’installation unifié et serveur de processus hello. Vous pouvez guident des captures d’écran hello [ici](../../site-recovery/vmware-walkthrough-overview.md) installation de hello toocomplete. Vous pouvez faire référence toohello suivant des captures d’écran pour les étapes spécifiées pour ce scénario de migration.

    Dans **avant de commencer**, sélectionnez **installer le serveur de configuration hello et serveur de processus**.

    ![][6]

    3d. Dans **inscription**, recherchez et sélectionnez la clé d’inscription de hello vous avez téléchargé à partir du coffre de hello.

    ![][7]

    3e. Dans **détails de l’environnement**, indiquez si vous souhaitez tooreplicate les ordinateurs virtuels VMware. Pour ce scénario de migration, choisissez **non**.

    ![][8]

    3f. Une fois l’installation de hello est terminée, vous verrez hello **serveur de Configuration de Microsoft Azure Site Recovery** fenêtre. Utilisez hello **gérer les comptes** onglet compte hello toocreate récupération de Site peut utiliser pour la découverte automatique. (Dans un scénario de hello sur la protection des machines physiques, configurez le compte de hello n’est pas approprié, mais vous devez tooenable compte au moins un de hello comme suit. Dans ce cas, vous pouvez nommer hello et mot de passe en tant qu’un). Hello d’utilisation **inscription du coffre** le fichier d’informations d’identification coffre onglet tooupload hello.

    ![][9]

4. **Configuration d’environnement cible de hello**. Cliquez sur **Prepare infrastructure** > **cible**et spécifiez le modèle de déploiement hello souhaité toouse pour les machines virtuelles après le basculement. Vous pouvez choisir **Classique** ou **Resource Manager**, en fonction de votre scénario.

    ![][10]

    Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles. Notez que si vous utilisez un compte de stockage Premium pour les données répliquées, vous devez tooset une réplication de toostore de compte de stockage Standard supplémentaire des journaux.

5. **Configurer les paramètres de réplication**. Veuillez suivre [configurer les paramètres de réplication](../../site-recovery/vmware-walkthrough-overview.md) tooverify votre serveur de configuration est correctement associé à la stratégie de réplication hello que vous créez.

6. **Planification de la capacité**. Hello d’utilisation [Planificateur de capacité](../../site-recovery/site-recovery-capacity-planner.md) tooaccurately estimation de bande passante réseau, de stockage et autres exigences toomeet a besoin de la réplication. Lorsque vous avez terminé, sélectionnez **Oui** dans **Avez-vous effectué une planification de la capacité ?**

    ![][11]

7. Hello étapes suivantes vous aider à **installer le service mobilité et activer la réplication**.

    7a. Vous pouvez choisir trop[installation push](../../site-recovery/vmware-walkthrough-overview.md) tooyour source machines virtuelles ou trop[installer manuellement le service mobilité](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) sur votre source de machines virtuelles. Vous trouverez exigence hello d’installation push et de chemin d’accès de hello du programme d’installation manuelle de hello dans lien hello fourni. Si vous effectuez une installation manuelle, vous devrez peut-être toouse un serveur de configuration hello interne IP adresse toofind.

    ![][12]

    Hello basculé VM aura deux disques temporaires : un dans hello principal machine virtuelle et hello autres créé lors de la configuration de hello de machine virtuelle dans la région de récupération hello. disque temporaire de hello tooexclude avant la réplication, installer le service de mobilité hello avant d’activer la réplication. toolearn en savoir plus sur la façon dont tooexclude hello disque temporaire, consultez trop[exclure les disques de la réplication](../../site-recovery/vmware-walkthrough-overview.md).

    7b. À présent, activez la réplication comme suit :
      * Cliquez sur **Répliquer l’application** > **Source**. Une fois que vous avez activé la réplication pour hello première fois, cliquez sur + répliquer dans la réplication de tooenable hello coffre pour des ordinateurs supplémentaires.
      * À l’étape 1, configurez la source en tant que votre serveur de processus.
      * À l’étape 2, spécifiez le modèle de déploiement hello après le basculement, un toomigrate de compte de stockage Premium pour, journaux de toosave d’un compte de stockage Standard et un toofail de réseau virtuel à.
      * À l’étape 3, ajouter des ordinateurs virtuels protégés par adresse IP (vous devrez peut-être une toofind d’adresse IP interne les).
      * À l’étape 4, configurez les propriétés de hello en sélectionnant des comptes hello définies précédemment sur le serveur de processus hello.
      * À l’étape 5, choisissez la stratégie de réplication hello que précédemment créé, définir des paramètres de réplication.
      Cliquez sur **OK** pour activer la réplication.

    > [!NOTE]
    > Lorsqu’une machine virtuelle Azure est désallouée et démarrée à nouveau, il n’existe aucune garantie qu’il recevra hello la même adresse IP. Si hello adresseIP du serveur de processus/serveur de configuration hello ou hello protégé modification de machines virtuelles Azure, la réplication hello dans ce scénario peut ne pas fonctionne correctement.

    ![][13]

    Lorsque vous concevez votre environnement de stockage Azure, nous vous recommandons d’utiliser des comptes de stockage distincts pour chaque machine virtuelle dans un groupe à haute disponibilité. Nous recommandons de suivre les meilleures pratiques de hello dans la couche de stockage hello trop[utiliser plusieurs comptes de stockage pour chaque groupe à haute disponibilité](../../virtual-machines/windows/manage-availability.md). Distribution des comptes de stockage VM disques toomultiple vous aide à la disponibilité du stockage tooimprove et distribue les hello d’e/s sur une infrastructure de stockage Azure hello. Si vos machines virtuelles sont dans un ensemble de disponibilité, au lieu de répliquer les disques de tous les ordinateurs virtuels dans un compte de stockage, nous vous recommandons la migration de plusieurs machines virtuelles plusieurs fois, afin que les machines virtuelles hello hello même groupe à haute disponibilité ne partagent pas un compte de stockage unique. Hello d’utilisation **activer la réplication** tooset panneau d’un compte de stockage de destination pour chaque machine virtuelle, à la fois. Vous pouvez choisir un modèle de déploiement après le basculement selon les besoins de tooyour. Si vous choisissez le Gestionnaire de ressources (RM) en tant que votre modèle de déploiement après le basculement, vous pouvez basculer un tooan RM VM machine virtuelle du Gestionnaire de ressources, ou vous pouvez basculer un tooan classique de la machine virtuelle RM VM.

8. **Exécuter un test de basculement**. toocheck si la réplication est terminée, cliquez sur votre Site Recovery, puis **paramètres** > **répliquées des éléments**. Vous verrez un état de hello et pourcentage de votre processus de réplication. Après la réplication initiale est terminée, exécutez toovalidate de Test de basculement de votre stratégie de réplication. Pour obtenir des instructions détaillées de test de basculement, consultez trop[exécuter un test de basculement en mode de récupération de Site](../../site-recovery/vmware-walkthrough-overview.md). Vous pouvez voir État hello du test de basculement dans **paramètres** > **travaux** > **YOUR_FAILOVER_PLAN_NAME**. Dans Panneau de hello, vous verrez une répartition des étapes de hello et les résultats de réussite/échec. Si le test de basculement hello échoue à tout moment, cliquez sur le message d’erreur hello étape toocheck hello. Assurez-vous que vos machines virtuelles et la stratégie de réplication requise hello avant d’exécuter un basculement. Lecture [tooAzure de Test de basculement en mode de récupération de Site](../../site-recovery/site-recovery-test-failover-to-azure.md) pour plus d’informations et des instructions de test de basculement.

9. **Exécutez un basculement**. Au terme de test de basculement hello, exécuter un basculement toomigrate votre tooPremium disques stockage et répliquer les instances de machine virtuelle hello. Veuillez suivre hello détaillée des étapes de [exécuter un basculement](../../site-recovery/site-recovery-failover.md#run-a-failover). Veillez à sélectionner **arrêter de machines virtuelles et synchroniser les données les plus récentes hello** toospecify que Site Recovery doit essayer tooshut machines virtuelles de hello protégé vers le bas et de synchroniser les données de hello afin que hello version la plus récente des données de hello est basculée. Si vous ne sélectionnez pas cette option, ou tentative de hello ne réussit pas hello basculement sera hello plus récentes disponibles point de récupération pour hello machine virtuelle. Récupération de site crée une instance de machine virtuelle dont le type est hello identique ou similaire tooa VM de compatible avec le stockage Premium. Vous pouvez vérifier les performances hello et les prix des diverses instances de machine virtuelle en accédant trop[tarification des Machines virtuelles Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) ou [tarification des Machines virtuelles Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Étapes de post-migration

1. **Configurer la disponibilité de toohello machines virtuelles répliquée définie éventuellement**. Récupération de site ne prend pas en charge la migration de machines virtuelles, ainsi que le groupe à haute disponibilité hello. En fonction de déploiement hello de votre machine virtuelle répliquée, procédez d’une des manières de hello :
  * Pour un ordinateur virtuel créé à l’aide du modèle de déploiement classique hello : ajouter hello VM toohello groupe à haute disponibilité hello portail Azure. Pour des instructions détaillées, consultez trop[ajouter un ensemble de disponibilité tooan machine virtuelle existante](../../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Pour le modèle de déploiement du Gestionnaire de ressources hello : enregistrer votre configuration de machine virtuelle de hello, puis supprimez et recréez les machines virtuelles de hello dans hello à haute disponibilité. toodo utilisez donc script hello sur [définir Resource Manager ordinateurs virtuels à haute disponibilité Azure](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Vérifier la limitation hello de ce script et planifier des temps d’arrêt avant d’exécuter le script de hello.

2. **Supprimer les anciennes machines virtuelles et les anciens disques**. Avant de supprimer ces, assurez-vous que les disques Premium hello sont cohérents avec les disques sources et hello que nouvelles machines virtuelles effectuer hello même fonctionner en tant que source de hello machines virtuelles. Dans le modèle de déploiement du Gestionnaire de ressources (RM) hello, supprimer hello machine virtuelle et de supprimer des disques de hello à partir de vos comptes de stockage source Bonjour portail Azure. Dans le modèle de déploiement classique de hello, vous pouvez supprimer hello machine virtuelle et les disques dans le portail classique de hello ou le portail Azure. S’il existe un problème dans le hello disque n’est pas supprimé même si vous avez supprimé hello machine virtuelle, consultez [résoudre les erreurs lorsque vous supprimez les disques durs virtuels](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Infrastructure d’Azure Site Recovery hello propre**. Si la récupération de Site n’est plus nécessaire, vous pouvez nettoyer son infrastructure en supprimant les éléments répliqués, serveur de configuration hello et hello stratégie de récupération, puis en supprimant le coffre Azure Site Recovery hello.

## <a name="troubleshooting"></a>Résolution des problèmes

* [Surveiller et résoudre les problèmes de protection pour les machines virtuelles et les serveurs physiques](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Forum Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Étapes suivantes

Consultez hello suivant des ressources pour des scénarios spécifiques pour la migration des ordinateurs virtuels :

* [Migrer des machines virtuelles Azure entre les comptes de stockage](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Créez et téléchargez un tooAzure le disque dur virtuel de Windows Server.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migration d’ordinateurs virtuels à partir d’Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Consultez également hello suivant toolearn ressources plus d’informations sur le stockage Azure et les Machines virtuelles Azure :

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
