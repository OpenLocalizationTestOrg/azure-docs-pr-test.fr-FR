---
title: "partage de fichiers aaaAutomate StorSimple la récupération d’urgence avec Azure Site Recovery | Documents Microsoft"
description: "Décrit les étapes de hello et meilleures pratiques pour la création d’une solution de récupération d’urgence pour les partages de fichiers hébergé sur le stockage Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Solution de récupération d’urgence automatisée à l’aide d’Azure Site Recovery pour les partages de fichiers hébergés sur StorSimple
## <a name="overview"></a>Vue d'ensemble
Microsoft Azure StorSimple est une solution de stockage cloud hybride adresses hello complexités de couramment associées à des partages de fichiers de données non structurées. StorSimple utilise le stockage cloud comme une extension de hello solution locale et reconnaît automatiquement les données sur le stockage local et le stockage cloud. Protection des données, d’intégrer local et les instantanés cloud, hello inutile une immense infrastructure de stockage.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) est un service Azure offrant des capacités de récupération d’urgence (DR) en coordonnant la réplication, le basculement et la récupération des machines virtuelles. Azure Site Recovery prend en charge un certain nombre de technologies de réplication tooconsistently répliquer, protéger et basculer en toute transparence les machines virtuelles et les applications de nuages tooprivate/public ou hébergés.

À l’aide d’Azure Site Recovery, réplication d’ordinateur virtuel et fonctionnalités de capture instantanée de cloud StorSimple, vous pouvez protéger des environnement de serveur hello complet du fichier. Dans l’événement hello d’une interruption de service, vous pouvez utiliser un toobring clic vos partages de fichiers en ligne dans Azure en quelques minutes.

Ce document explique en détail comment créer une solution de récupération d’urgence pour vos partages de fichiers hébergés sur le système de stockage StorSimple, et comment effectuer des basculements planifiés/non planifiés/de test à l’aide d’un plan de récupération d’urgence accessible en un clic. Fondamentalement, il montre comment vous pouvez modifier hello un Plan de récupération dans votre tooenable de coffre Azure Site Recovery StorSimple basculements durant les scénarios de reprise après sinistre. Il décrit également les configurations prises en charge et les conditions requises préalables. Ce document suppose que vous êtes familiarisé avec les concepts de base hello des architectures d’Azure Site Recovery et StorSimple.

## <a name="supported-azure-site-recovery-deployment-options"></a>Options de déploiement Azure Site Recovery prises en charge
Les clients peuvent déployer des serveurs de fichiers en tant que serveurs physiques ou en tant que machines virtuelles exécutés sur Hyper-V ou VMware, avant de créer des partages de fichiers à partir des volumes issus du stockage StorSimple. Azure Site Recovery peut protéger les deux déploiements physiques et virtuels de tooeither un tooAzure ou un site secondaire. Ce document fournit des détails d’une solution de récupération d’urgence avec Azure comme site de récupération hello pour un ordinateur virtuel hébergé sur Hyper-V du serveur de fichiers et partages de fichiers sur le stockage StorSimple. Autres scénarios dans le serveur de fichiers hello machine virtuelle est sur un VM VMware ou d’un ordinateur physique peuvent être implémentés de la même façon.

## <a name="prerequisites"></a>Composants requis
Implémentation d’une solution de récupération d’urgence d’un clic qui utilise Azure Site Recovery pour les partages de fichiers hébergés sur le stockage StorSimple a hello suivant des conditions préalables :

* Machine virtuelle du serveur de fichiers Windows Server 2012 R2 en local hébergée sur une machine virtuelle Hyper-V ou VMware ou sur un ordinateur physique
* Périphérique de stockage StorSimple local enregistré auprès d’Azure StorSimple Manager
* Dispositif de StorSimple de Cloud créés dans le Gestionnaire de Azure StorSimple hello (Cela peut être conservée en état d’arrêt)
* Partages de fichiers sur des volumes hello configurés sur le périphérique de stockage StorSimple hello
* [Coffre Azure Site Recovery Services](../site-recovery/site-recovery-vmm-to-vmm.md) créé dans un abonnement Microsoft Azure.

En outre, si Azure est un site de récupération, exécutez hello [Azure Virtual Machine Readiness Assessment tool](http://azure.microsoft.com/downloads/vm-readiness-assessment/) sur tooensure d’ordinateurs virtuels qu’ils sont compatibles avec les machines virtuelles Azure et Azure Site Recovery services.

les problèmes de latence tooavoid (ce qui peuvent entraîner des coûts plus élevés), assurez-vous que vous créez votre solution de Cloud StorSimple compte automation, et que les comptes de stockage dans hello même région.

## <a name="enable-dr-for-storsimple-file-shares"></a>Activer la récupération d’urgence pour les partages de fichiers StorSimple
Chaque composant de hello local a besoin d’un environnement toobe protégé tooenable terminer la réplication et récupération. Cette section décrit comment :

* configurer la réplication Active Directory et DNS (facultatif) ;
* Utiliser la protection d’Azure Site Recovery tooenable hello du serveur de fichiers machine virtuelle
* activer la protection des volumes StorSimple ;
* Configurer le réseau de hello

### <a name="set-up-active-directory-and-dns-replication-optional"></a>configurer la réplication Active Directory et DNS (facultatif) ;
Si vous souhaitez hello tooprotect ordinateurs Active Directory et DNS pour qu’ils soient disponibles sur le site de récupération d’urgence de hello, vous devez tooexplicitly les protéger (de sorte que les serveurs de fichiers hello sont accessibles après le basculement avec l’authentification). Il existe deux options recommandées en fonction de la complexité de hello de l’environnement local du client de l’hello.

#### <a name="option-1"></a>Option 1 :
Si le client de hello comporte un petit nombre d’applications, un seul contrôleur de domaine pour l’ensemble du hello site local et est en cas d’échec sur l’ensemble du site hello, il est recommandé à l’aide d’ordinateur de contrôleur de domaine Azure Site Recovery réplication tooreplicate hello site secondaire de tooa (c’est applicable pour le site à site et de site vers Azure).

#### <a name="option-2"></a>Option 2 :
Si hello client comporte un grand nombre d’applications, une forêt Active Directory est en cours d’exécution et basculement un peu d’applications à la fois, nous vous recommandons de configurer le contrôleur de domaine supplémentaire sur le site de récupération d’urgence de hello (soit un site secondaire ou dans Azure).

Reportez-vous trop[solution de récupération d’urgence automatisée pour Active Directory et DNS à l’aide d’Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) pour obtenir des instructions lors de la disposition d’un contrôleur de domaine sur le site de récupération d’urgence de hello. Pour le reste de hello de ce document, nous allons supposer qu'un contrôleur de domaine est disponible sur le site de récupération d’urgence hello.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Utiliser la protection d’Azure Site Recovery tooenable hello du serveur de fichiers machine virtuelle
Cette étape nécessite que vous préparez l’environnement de serveur de fichiers local hello, créez et préparez un coffre Azure Site Recovery et activez la protection des fichiers de machine virtuelle de hello.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>environnement de serveur de fichiers local hello tooprepare
1. Ensemble hello **contrôle de compte d’utilisateur** trop**ne jamais m’avertir**. Cela est nécessaire afin que vous pouvez utiliser les cibles iSCSI hello Azure automation scripts tooconnect après échec par Azure Site Recovery.

   1. Appuyez sur la touche de Windows hello + Q et recherchez **UAC**.
   2. Sélectionnez **Modifier les paramètres du contrôle de compte d’utilisateur**.
   3. Hello faites glisser la barre bas toohello vers **ne jamais m’avertir**.
   4. Cliquez sur **OK**, puis sélectionnez **Oui** à l’invite.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Installez hello Agent de machine virtuelle sur chaque serveur de fichiers hello machines virtuelles. Cela est nécessaire afin que vous pouvez exécuter des scripts d’automatisation Azure sur hello basculé de machines virtuelles.

   1. [Télécharger l’agent de hello](http://aka.ms/vmagentwin) trop`C:\\Users\\<username>\\Downloads`.
   2. Ouvrez Windows PowerShell en mode d’administrateur (exécuter en tant qu’administrateur) et entrez hello commande toonavigate toohello téléchargement emplacement suivant :

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > nom de fichier Hello peut varier en fonction de la version de hello.
      >
      >
3. Cliquez sur **Suivant**.
4. Accepter hello **termes du contrat de** puis cliquez sur **suivant**.
5. Cliquez sur **Terminer**.
6. Créez des partages de fichiers à l’aide de volumes issus du stockage StorSimple. Pour plus d’informations, consultez [utiliser hello StorSimple Manager service toomanage volumes](storsimple-manage-volumes.md).

   1. Sur vos machines virtuelles locales, appuyez sur la touche de Windows hello + Q et recherchez **iSCSI**.
   2. Sélectionnez **Initiateur iSCSI**.
   3. Sélectionnez hello **Configuration** nom de l’initiateur hello onglet et la copie.
   4. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
   5. Sélectionnez hello **StorSimple** onglet, puis sélectionnez hello Service StorSimple Manager qui contient l’unité physique de hello.
   6. Créez un ou plusieurs conteneurs de volumes, puis créez un ou plusieurs volumes (Ces volumes sont pour les partages de fichier hello sur le serveur de fichiers hello machines virtuelles). Copier le nom de l’initiateur hello et donner un nom approprié pour les enregistrements de contrôle d’accès de hello lorsque vous créez des volumes hello.
   7. Sélectionnez hello **configurer** onglet et notez les adresse IP de hello du périphérique de hello.
   8. Sur vos machines virtuelles local, accédez à toohello **initiateur iSCSI** à nouveau et entrez hello IP Bonjour section de connexion rapide. Cliquez sur **connexion rapide** (hello appareil doit maintenant être connecté).
   9. Ouvrez hello portail Azure et sélectionnez hello **Volumes et périphériques** onglet. Cliquez sur **Configuration automatique**. volume Hello que vous venez de créer doit apparaître.
   10. Dans le portail de hello, sélectionnez hello **périphériques** onglet, puis sélectionnez **créer un nouveau périphérique virtuel.** (Créer un périphérique virtuel) (celui-ci sera utilisé si un basculement se produit). Ce nouveau périphérique virtuel peut être conservé dans un état hors connexion de tooavoid des coûts supplémentaires. tootake hello toohello hors connexion, accédez de périphérique virtuel **virtuels** section hello Portal et arrêtez-le.
   11. Revenir en arrière toohello local machines virtuelles et ouvrez Gestion des disques (appuyez sur la touche de Windows hello + X et sélectionnez **gestion des disques**).
   12. Vous remarquerez quelques disques supplémentaires (selon le nombre de hello de volumes que vous avez créé). Avec le bouton hello premier, sélectionnez **initialiser le disque**, puis sélectionnez **OK**. Avec le bouton hello **non alloué** section, sélectionnez **nouveau Volume Simple**, lui attribuer une lettre de lecteur et terminer l’Assistant de hello.
   13. Répétez l’étape l pour tous les disques hello. Vous pouvez maintenant voir tous les disques hello sur **ce PC** Bonjour l’Explorateur Windows.
   14. Utilisez hello File and Storage Services rôle toocreate partages de fichiers sur ces volumes.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate et préparer un coffre Azure Site Recovery
Consultez toohello [documentation Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget main d’Azure Site Recovery avant de protéger le serveur de fichiers hello machine virtuelle.

#### <a name="tooenable-protection"></a>protection de tooenable
1. Déconnecter hello iSCSI cible (s) à partir de hello local machines virtuelles que vous souhaitez tooprotect via Azure Site Recovery :

   1. Appuyez sur la touche Windows + Q et lancez une recherche sur **iSCSI**.
   2. Sélectionnez **Configurer l’initiateur iSCSI**.
   3. Déconnectez l’appareil StorSimple hello que vous avez connecté précédemment. Sinon, vous pouvez basculer hors tension du serveur de fichiers hello pendant quelques minutes lors de l’activation de la protection.

   > [!NOTE]
   > Cela entraîne toobe de partages de fichiers hello temporairement indisponible.
   >
   >
2. [Activer la protection des machines virtuelles](../site-recovery/site-recovery-hyper-v-site-to-azure.md) hello serveur de fichiers VM à partir du portail d’Azure Site Recovery hello.
3. Lors de la synchronisation initiale des hello démarre, vous pouvez reconnecter cible de hello à nouveau. Accédez initiateur iSCSI de toohello, sélectionnez l’appareil StorSimple hello, puis cliquez sur **connexion**.
4. Lorsque la synchronisation de hello est terminée et état de hello de hello VM **protégé**, sélectionnez hello machine virtuelle, sélectionnez hello **configurer** onglet et mettre à jour le réseau hello Hello machine virtuelle en conséquence (il s’agit hello réseau Ce hello basculé de machines virtuelles feront partie de). Si le réseau de hello n’apparaît pas, cela signifie que la synchronisation hello continue.

### <a name="enable-protection-of-storsimple-volumes"></a>activer la protection des volumes StorSimple ;
Si vous n’avez pas sélectionné de hello **activer une sauvegarde par défaut pour ce volume** option pour les volumes StorSimple hello, accédez trop**les stratégies de sauvegarde** dans hello service StorSimple Manager et créer une sauvegarde appropriée stratégie pour tous les volumes hello. Nous vous recommandons de définir fréquence hello de sauvegardes toohello point de récupération (RPO) que vous aimeriez toosee pour l’application hello.

### <a name="configure-hello-network"></a>Configurer le réseau de hello
Pour le serveur de fichiers hello machine virtuelle, configurez les paramètres réseau dans Azure Site Recovery afin que les réseaux d’ordinateurs virtuels hello sont réseau de récupération d’urgence toohello jointe correct après le basculement.

Vous pouvez sélectionner hello VM Bonjour **éléments répliqués** onglet Paramètres de réseau tooconfigure hello, comme indiqué dans hello après l’illustration.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Créer un plan de récupération
Vous pouvez créer un plan de récupération dans le processus de basculement ASR tooautomate hello hello des partages de fichiers. Si une interruption se produit, vous pouvez mettre des partages de fichiers hello dans quelques minutes, avec un seul clic. tooenable cette automatisation, vous devez un compte Azure automation.

#### <a name="toocreate-an-automation-account"></a>toocreate un compte Automation
1. Accédez toohello portail Azure &gt; **Automation** section.
2. Cliquez sur le bouton **+ Ajouter** pour ouvrir le panneau ci-dessous.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Nom : entrez le nom d’un nouveau compte Automation
   * Abonnement : choisissez l’abonnement
   * Groupe de ressources : sélectionnez un groupe de ressources existant ou créez-en un
   * Emplacement - choisir l’emplacement, conservez-le dans hello même géographique/région le hello StorSimple Appliance de Cloud et les comptes de stockage ont été créés.
   * Créer un compte d’identification Azure : sélectionnez l’option **Oui**.

3. Accédez à compte Automation de toohello, cliquez sur **Runbooks** &gt; **parcourir la galerie** tooimport tous hello requis procédures opérationnelles dans un compte d’automatisation hello.
4. Ajouter hello suivant les procédures opérationnelles en recherchant **la récupération d’urgence** balise dans la galerie de hello :

   * Clean up of StorSimple volumes after Test Failover (TFO) (Nettoyer les volumes StorSimple après le test de basculement (TFO))
   * Fail over StorSimple volume containers (Basculer des conteneurs de volumes StorSimple)
   * Mount volumes on StorSimple device after failover (Monter les volumes sur l’appareil StorSimple après le basculement)
   * Uninstall custom script extension in Azure VM (Désinstaller l’extension de script personnalisée dans la machine virtuelle Azure)
   * Start StorSimple Virtual Appliance (Démarrer l’appliance virtuelle StorSimple)

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Publier tous les scripts hello en sélectionnant hello runbook dans le compte d’automatisation hello et cliquez sur **modifier** &gt; **publier** , puis **Oui** toohello vérification Message. Après cette étape, hello **Runbooks** onglet s’affiche comme suit :

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. Dans un compte automation hello, sélectionnez hello **actifs** onglet &gt; cliquez sur **Variables** &gt; **ajouter une variable** et ajoutez hello suivant des variables. Vous pouvez choisir tooencrypt ces ressources. Ces variables sont spécifiques au plan de récupération. Si la récupération du plan (que vous allez créer à l’étape suivante de hello) le nom est le plan de test, puis vos variables doivent être StorSimRegKey de plan de test, plan de test-AzureSubscriptionName et ainsi de suite.

   * *RecoveryPlanName***- StorSimRegKey**: clé d’inscription de hello pourquoi le service StorSimple Manager.
   * *RecoveryPlanName***- AzureSubscriptionName**: nom hello Hello abonnement Azure.
   * *RecoveryPlanName***- ResourceName**: nom hello Hello StorSimple ressource qui a l’appareil StorSimple hello.
   * *RecoveryPlanName***- DeviceName**: périphérique hello a toobe basculé.
   * *RecoveryPlanName***- VolumeContainers**: une chaîne séparée par des virgules de conteneurs de volumes présents sur l’appareil hello nécessitant toobe a échoué ; par exemple, volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: hello StorSimple Cloud sur le hello conteneurs sont toobe a échoué sur.
   * *RecoveryPlanName***- TargetDeviceDnsName**: nom du service de l’appareil cible de hello hello (cela figurent dans hello **Machine virtuelle** section : nom du service hello est hello même comme hello Nom DNS).
   * *RecoveryPlanName***- StorageAccountName**: nom du compte de stockage dans le script de hello hello (qui a toorun sur hello basculé VM) sera stocké. Cela peut être n’importe quel compte de stockage qui a un script de hello espace toostore temporairement.
   * *RecoveryPlanName***- StorageAccountKey**: clé d’accès hello hello au-dessus de compte de stockage.
   * *RecoveryPlanName***- ScriptContainer**: nom hello du conteneur hello dans le hello script est stocké dans le cloud de hello. Si le conteneur de hello n’existe pas, il sera créé.
   * *RecoveryPlanName***- VMGUIDS**: lors de la protection d’une machine virtuelle, Azure Site Recovery assigne chaque machine virtuelle un identificateur unique qui fournit des détails hello Hello a échoué sur l’ordinateur virtuel. tooobtain hello VMGUID, sélectionnez hello **Services de récupération** onglet et cliquez sur **élément protégé** &gt; **groupes de Protection** &gt; **Machines** &gt; **propriétés**. Si vous avez plusieurs machines virtuelles, puis ajoutez hello GUID sous forme de chaîne séparée par des virgules.
   * *RecoveryPlanName***- AutomationAccountName** hello – nom du compte d’automatisation hello dans lequel vous avez ajouté hello runbooks et ressources de hello.

  Par exemple, si hello nom hello du plan de récupération est fileServerpredayRP, votre **informations d’identification** & **Variables** onglets doivent apparaître comme suit après avoir ajouté tous les composants de hello.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Accédez toohello **Services de récupération** section et le coffre Azure Site Recovery hello select que vous avez créé précédemment.
8. Sélectionnez hello **Plans de récupération (Site Recovery)** option à partir de **gérer** groupe et créez un plan de récupération comme suit :

   a.  Cliquez sur le bouton **+ Plan de récupération**, qui affiche le panneau ci-dessous.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Entrez un nom de plan de récupération, choisissez les valeurs du modèle Source, Cible et Déploiement.

   c.  Sélectionnez les ordinateurs virtuels de hello hello groupe de protection que vous souhaitez tooinclude dans un plan de récupération hello et cliquez sur **OK** bouton.

   d.  Sélectionnez le plan de récupération que vous avez créé précédemment, cliquez sur **personnaliser** bouton Vue Personnalisation du plan de récupération tooopen hello.

   e.  Cliquez avec le bouton droit sur **Arrêt de tous les groupes** et cliquez sur **Add pre action (Ajouter action antérieure)**.

   f.  Ouvre insérer le panneau d’action, entrez un nom, sélectionnez **côté principal** option où toorun option, sélectionnez le compte Automation (dans lequel vous avez ajouté les runbooks hello), puis hello  **Basculement-StorSimple--conteneurs de volumes** runbook.

   g.  Cliquez avec le bouton droit sur **groupe 1 : Démarrer** et cliquez sur **ajouter les éléments protégés** option, puis sélectionnez les machines virtuelles hello qui sont toobe protégé dans le plan de récupération hello et cliquez sur **Ok** bouton. Facultatif, s’il s’agit déjà des machines virtuelles sélectionnées.

   h.  Cliquez avec le bouton droit sur **groupe 1 : Démarrer** et cliquez sur **valider action** option, puis ajoutez tous les hello suivantes des scripts :

   * Start-StorSimple-Virtual-Appliance runbook
   * Fail over-StorSimple-volume-containers runbook
   * Mount-volumes-after-failover runbook
   * Uninstall-custom-script-extension runbook

   i.  Ajouter une action manuelle après hello ci-dessus 4 scripts hello même **groupe 1 : POST-étapes** section. Cette action est point hello à laquelle vous pouvez vérifier que tout fonctionne correctement. Cette action doit toobe ajouté uniquement en tant que partie du Test de basculement (donc uniquement sélectionner hello **Test de basculement** case à cocher).

   j.  Après l’action manuelle de hello, ajoutez hello **nettoyage** à l’aide de script hello la même procédure que celle utilisée pour hello autres runbooks. **Enregistrer** plan de récupération hello.

    > [!NOTE]
    > Lorsque vous exécutez un test de basculement, vous devez vérifier tous les éléments à l’étape de l’action manuelle hello, car les volumes StorSimple hello qui avaient été clonés sur l’appareil cible de hello seront supprimées dans le cadre de nettoyage de hello après que l’action manuelle de hello est terminée.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Exécution d’un test de basculement
Consultez toohello [Solution de récupération d’urgence de Active Directory](../site-recovery/site-recovery-active-directory.md) guide d’accompagnement pour des considérations spécifiques tooActive active pendant le basculement de test hello. le programme d’installation locale de Hello n’est pas perturbé tout cas de basculement test hello. Hello volumes StorSimple qui étaient attachées toohello local machine virtuelle sont clonée toohello StorSimple Appliance de Cloud sur Azure. Un ordinateur virtuel à des fins de test est placée dans Azure et hello volumes clonés sont attaché toohello machine virtuelle.

#### <a name="tooperform-hello-test-failover"></a>test de basculement tooperform hello
1. Bonjour portail Azure, sélectionnez votre archivage site recovery.
2. Cliquez sur le plan de récupération hello créé pour le serveur de fichiers hello machine virtuelle.
3. Cliquez sur **Test de basculement**.
4. Sélectionnez toowhich de réseau virtuel Azure hello que machines virtuelles Azure sont connectées après que le basculement se produit.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés, ou sur hello **tâche de Test de basculement** dans le nom de l’archivage &gt; **travaux** &gt; **les tâches de récupération de Site**.
6. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure &gt; **virtuels**. Vous pouvez effectuer vos validations.
7. Une fois les validations hello terminées, cliquez sur **Validations complète**. Cette hello de nettoyage va Volumes StorSimple et arrêt hello StorSimple Appliance de Cloud.
8. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans l’enregistrement de commentaires et d’enregistrer toutes les observations associées hello test de basculement. Cette opération supprimera la machine virtuelle hello qui ont été créés pendant le test de basculement.

## <a name="perform-a-planned-failover"></a>Exécuter un basculement planifié
   Lors d’un basculement planifié, hello local serveur de fichiers que machine virtuelle est arrêté normalement et un cloud de prise d’instantané de sauvegarde de volumes hello sur l’appareil StorSimple. des volumes StorSimple Hello sont a échoué sur le périphérique virtuel toohello, un réplica de machine virtuelle est placée sur Azure, et les volumes de hello sont attaché toohello machine virtuelle.

#### <a name="tooperform-a-planned-failover"></a>tooperform un basculement planifié
1. Bonjour portail Azure, sélectionnez **services de récupération** coffre &gt; **plans de récupération (récupération de Site)** &gt; **recoveryplan_name** créé pour serveur de fichiers Hello machine virtuelle.
2. Dans le panneau de plan de récupération hello, cliquez sur **plus** &gt; **le basculement planifié**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. Sur hello **confirmer le basculement planifié** panneau, choisissez la source de hello et emplacements cibles et réseau cible sélectionnez et cliquez sur le processus de basculement hello de hello cocher icône ✓ toostart.
4. Une fois créés, les ordinateurs virtuels de réplication sont en attente de validation. Cliquez sur **valider** toocommit hello basculement.
5. Une fois la réplication terminée, les ordinateurs virtuels hello démarrent à l’emplacement secondaire de hello.

## <a name="perform-a-failover"></a>Effectuer un basculement
Pendant un basculement non planifié, les volumes StorSimple hello sont basculés périphérique virtuel toohello, un réplica de machine virtuelle est porté sur Azure, et les volumes de hello sont attaché toohello machine virtuelle.

#### <a name="tooperform-a-failover"></a>tooperform un basculement
1. Bonjour portail Azure, sélectionnez **services de récupération** coffre &gt; **plans de récupération (récupération de Site)** &gt; **recoveryplan_name** créé pour serveur de fichiers Hello machine virtuelle.
2. Dans le panneau de plan de récupération hello, cliquez sur **plus** &gt; **basculement**.  
3. Sur hello **confirmer le basculement** panneau, choisissez la source de hello et cibler des emplacements.
4. Sélectionnez **arrêter des machines virtuelles et synchroniser les données les plus récentes hello** toospecify que Site Recovery doit essayer tooshut la machine virtuelle de hello protégé et de synchroniser les données de hello afin que hello version la plus récente des données de hello basculé.
5. Après le basculement de hello, hello virtuels sont dans un état d’attente de validation. Cliquez sur **valider** toocommit hello basculement.


## <a name="perform-a-failback"></a>Effectuer une restauration automatique
Pendant une restauration automatique, les conteneurs de volumes StorSimple sont basculés unité physique de toohello précédent après qu’une sauvegarde est effectuée.

#### <a name="tooperform-a-failback"></a>tooperform une restauration automatique
1. Bonjour portail Azure, sélectionnez **services de récupération** coffre &gt; **plans de récupération (Site Recovery)** &gt; **recoveryplan_name** créé pour serveur de fichiers Hello machine virtuelle.
2. Dans le panneau de plan de récupération hello, cliquez sur **plus** &gt; **basculement planifié**.  
3. Choisissez les emplacements source et cible hello, synchronisation des données appropriée sélectionnez hello et options de création de machine virtuelle.
4. Cliquez sur **OK** bouton du processus de restauration automatique toostart hello.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Meilleures pratiques
### <a name="capacity-planning-and-readiness-assessment"></a>Planification de la capacité et évaluation de la préparation
#### <a name="hyper-v-site"></a>Site Hyper-V
Hello d’utilisation [outil utilisateur Capacity planner](http://www.microsoft.com/download/details.aspx?id=39057) toodesign hello serveur, de stockage et une infrastructure réseau pour votre environnement de réplica Hyper-V.

#### <a name="azure"></a>Microsoft Azure
Vous pouvez exécuter hello [Azure Virtual Machine Readiness Assessment tool](http://azure.microsoft.com/downloads/vm-readiness-assessment/) sur tooensure d’ordinateurs virtuels qu’ils sont compatibles avec les machines virtuelles Azure et Azure Site Recovery Services. Hello Readiness Assessment Tool vérifie les configurations des machines virtuelles et vous avertit lorsque des configurations ne sont pas compatibles avec Azure. Par exemple, il émet un avertissement dans le cas d’un lecteur C: supérieur à 127 Go.

La planification de la capacité comporte au moins deux processus importants :

* Mappage des locaux des ordinateurs virtuels Hyper-V tooAzure tailles des machines virtuelles (par exemple, A6, A7, A8 et A9).
* Détermination de hello nécessaire à la bande passante Internet.

## <a name="limitations"></a>Limites
* Actuellement, l’appareil StorSimple uniquement 1 peut être basculée (tooa unique StorSimple Appliance de Cloud). scénario Hello d’un serveur de fichiers qui s’étend sur plusieurs périphériques StorSimple n’est pas encore pris en charge.
* Si vous obtenez une erreur lors de l’activation de la protection d’un ordinateur virtuel, assurez-vous que vous avez déconnecté cibles iSCSI de hello.
* Tous les conteneurs de volumes hello qui ont été regroupés en raison des stratégies de sauvegarde de fractionnement entre les conteneurs de volumes basculeront ensemble.
* Tous les volumes hello dans les conteneurs de volumes hello choisie sont basculés.
* Volumes qui s’ajoutent toomore de 64 To ne peut pas être basculé, car la capacité maximale de hello d’une solution de Cloud StorSimple unique est de 64 To.
* Si le basculement planifiés de hello échoue et hello ordinateurs virtuels sont créés dans Azure, puis effectuez pas nettoyer les hello des machines virtuelles. Effectuez plutôt une restauration automatique. Si vous supprimez des machines virtuelles de hello puis hello local de machines virtuelles ne peut pas être activées à nouveau.
* Après un basculement, si vous n’êtes pas en mesure de toosee des volumes hello, passez les machines virtuelles de toohello, ouvrez Gestion des disques, réanalyser les disques hello et les mettre en ligne.
* Dans certains cas, les lettres de lecteur hello dans le site de récupération d’urgence hello peuvent être différents de celui hello lettres locales. Si cela se produit, vous devez problème hello correct de toomanually après que hello basculement est terminé.
* L’authentification multifacteur doit être désactivée pour hello Azure d’informations d’identification qui sont entrée dans le compte d’automatisation hello comme un élément multimédia. Si ce type d’authentification n’est pas désactivé, les scripts ne seront pas autorisées toorun automatiquement et plan de récupération hello échouera.
* Délai d’attente de travail de basculement : hello StorSimple script expire si basculement hello de conteneurs de volumes prend plus de temps que la limite d’Azure Site Recovery hello par script (actuellement 120 minutes).
* Délai d’attente de travail de sauvegarde : hello StorSimple script expire si la sauvegarde hello de volumes prend plus de temps que la limite d’Azure Site Recovery hello par script (actuellement 120 minutes).

  > [!IMPORTANT]
  > Exécution hello sauvegarde manuellement à partir de hello portail Azure et puis exécutez à nouveau le plan de récupération hello.

* Cloner le délai d’attente de la tâche : hello StorSimple script expire si hello le clonage des volumes prend plus de temps que la limite d’Azure Site Recovery hello par script (actuellement 120 minutes).
* Erreur de synchronisation de temps : hello StorSimple génère des erreurs indiquant que les sauvegardes hello ont échoué, même si la sauvegarde de hello a réussi dans le portail de hello. Des causes possibles de ce peuvent être que heure de cet appareil StorSimple hello est peut-être pas synchronisé avec hello heure actuelle dans le fuseau horaire de hello.

  > [!IMPORTANT]
  > Hello appliance heure de synchronisation avec hello heure actuelle dans le fuseau horaire de hello.

* Erreur de basculement d’application : hello StorSimple script peut échouer s’il existe un basculement de l’application lorsque le plan de récupération hello est en cours d’exécution.

  > [!IMPORTANT]
  > Réexécutez le plan de récupération hello après que basculement d’application hello est terminé.


## <a name="summary"></a>Résumé
Utilisez Azure Site Recovery pour créer un plan de récupération d’urgence automatisée complet pour une machine virtuelle du serveur de fichiers comportant des partages de fichiers sur le stockage StorSimple. Vous pouvez opérer le basculement de hello en quelques secondes à partir de n’importe où dans hello des événements d’une interruption de service et obtenir l’application hello opérationnel en quelques minutes.
