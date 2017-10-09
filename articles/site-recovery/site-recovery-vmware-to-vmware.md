---
title: aaaReplicate les ordinateurs virtuels VMware ou site tooanother de serveurs physiques (portail Azure classic) | Documents Microsoft
description: Utilisez cet article tooreplicate les ordinateurs virtuels VMware ou Windows/Linux serveurs physiques tooa site secondaire avec Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Répliquer locaux des ordinateurs virtuels VMware ou serveurs physiques tooa secondaire dans le portail Azure classic de hello

## <a name="overview"></a>Vue d'ensemble
InMage Scout dans Azure Site Recovery assure une réplication en temps réel entre des sites VMware locaux. InMage Scout est inclus dans les abonnements au service Azure Site Recovery. 

## <a name="prerequisites"></a>Composants requis
**Compte Azure**: vous devez disposer d’un compte [Microsoft Azure](https://azure.microsoft.com/) . Vous pouvez commencer avec une [version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/). [En savoir plus](https://azure.microsoft.com/pricing/details/site-recovery/) sur la tarification Site Recovery.

## <a name="step-1-create-a-vault"></a>Étape 1 : Créer un coffre
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur Nouveau > Gestion > Sauvegarde et récupération de sites (OMS). Vous pouvez également cliquer sur Parcourir > Coffre Recovery Services > Ajouter.
3. Dans **nom** spécifier un coffre de hello tooidentify nom convivial. Si vous avez plusieurs abonnements, sélectionnez-en un.
4. Dans **Groupe de ressources**, créez un groupe de ressources Azure ou sélectionnez un groupe existant. Spécifiez un champs toocomplete requis de région Azure.
5. Dans **emplacement**, sélectionnez hello région géographique pour le coffre hello. les régions toocheck pris en charge, consultez [tarification d’Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Si vous souhaitez tooquickly accès hello coffre à partir du tableau de bord de hello cliquez sur le code confidentiel toodashboard et puis cliquez sur Créer.
7. coffre Hello apparaîtra sur hello du tableau de bord > toutes les ressources, et sur hello les principaux Services de récupération coffres de panneau.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Étape 2 : Configurer le coffre hello et télécharger les composants InMage Scout
1. Dans Panneau de coffres des Services de récupération hello sélectionner votre coffre de sauvegarde et cliquez sur paramètres.
2. Dans **Paramètres** > **Prise en main**, cliquez sur **Site Recovery** > Étape 1 : **Préparer l’infrastructure** > **Objectif de la protection**.
3. Dans **objectif de Protection** sélectionnez toorecovery site et sélectionnez Oui, avec VMware vSphere hyperviseur. Puis cliquez sur OK.
4. Dans **le programme d’installation Scout**, cliquez sur téléchargement toodownload InMage Scout 8.0.1 GA la clé d’inscription et de logiciels. les fichiers d’installation Hello pour hello tous les composants requis sont dans un fichier .zip téléchargée de hello.

## <a name="step-3-install-component-updates"></a>Étape 3 : Installer les mises à jour de composants
En savoir plus sur hello de la dernière version [mises à jour](#updates). Vous allez installer les fichiers de mise à jour hello sur des serveurs Bonjour suivant l’ordre :

1. Serveur RX, s'il existe
2. Serveurs de configuration
3. Serveurs de traitement
4. Serveurs cibles maîtres
5. Serveurs vContinuum
6. Serveur source (Windows et Linux)

Installez les mises à jour hello comme suit :

1. Télécharger hello [mettre à jour](https://aka.ms/asr-scout-update5) fichier .zip. Ce fichier .zip contient hello fichiers suivants :

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * UA update 4 bits pour RHEL5, OL5, OL6, SUSE 10, SUSE 11 : UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Extrayez les fichiers .zip hello.<br>
3. **Pour le serveur de RX hello**: copie **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** server de RX toohello et extrayez-le. Bonjour extrait le dossier, exécutez **/installer**.<br>
4. **Pour le serveur de processus/serveur de configuration hello**: copie **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello serveur de configuration et le serveur de traitement. Double-cliquez sur toorun il.<br>
5. **Pour le serveur cible maître de Windows hello**: tooupdate hello unifiée de l’agent, copie **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** serveur cible maître de toohello. Double-cliquez dessus toorun il. Notez que hello unifiée de l’agent est également applicable toohello source serveur si la source n’est pas mis à jour jusqu’au Update4. Vous devez installer il sur serveur de source de hello ainsi, comme indiqué plus loin dans cette liste.<br>
6. **Pour le serveur de v-continuum hello**: copie **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello v-continuum serveur.  Assurez-vous que vous avez fermé Assistant v-continuum de hello. Double-cliquez sur hello fichier toorun dessus.<br>
7. **Pour le serveur cible maître de Linux hello**: tooupdate hello unifiée de l’agent, copie **UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello cible serveur maître et l’extraire. Bonjour extrait le dossier, exécutez **/installer**.<br>
8. **Pour le serveur de source de Windows hello**: il est inutile agent tooinstall 5 de la mise à jour sur la source si soruce se trouve déjà sur update4. Si elle est inférieure à update4, appliquer l’agent de mise à jour 5 hello.
tooupdate hello unifiée de l’agent, copie **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** serveur de source toohello. Double-cliquez dessus toorun il. <br>
9. **Pour le serveur de source de Linux hello**: tooupdate hello unifiée de l’agent, copiez la version correspondante UA toohello Linux du serveur de fichiers et extrayez-le. Bonjour extrait le dossier, exécutez **/installer**.  Exemple : Pour serveur de RHEL 6.7 64 bits, copiez **UA_RHEL6-64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello serveur et l’extraire. Bonjour extrait le dossier, exécutez **/installer**.

## <a name="step-4-set-up-replication"></a>Étape 4 : Configurer la réplication
1. Configurer la réplication entre la source de hello et cible VMware sites.
2. Pour obtenir des instructions, utilisez hello documentation InMage Scout est téléchargée avec le produit de hello. Ou bien, vous pouvez accéder à la documentation de hello comme suit :

   * [Notes de publication](https://aka.ms/asr-scout-release-notes)
   * [Matrice de compatibilité](https://aka.ms/asr-scout-cm)
   * [Guide d’utilisation](https://aka.ms/asr-scout-user-guide)
   * [Guide d’utilisation de RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Guide d'installation rapide](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Mises à jour
### <a name="azure-site-recovery-scout-801-update-5"></a>Azure Site Recovery Scout 8.0.1 Update 5
Scout Update 5 est une mise à jour cumulative. Il possède tous les correctifs hello de mise à jour 1 jusqu’au update4 et en suivant les nouveaux correctifs et améliorations.
Les correctifs qui sont ajoutés à partir de la récupération automatique du système Scout update4 tooupdate5 sont des composants de cible et v-continuum tooMaster spécifique. Si tous vos serveurs source, cible maître, serveur de Configuration, serveur de processus et RX se trouvent déjà sur ASR Scout update4 puis vous devez tooapply mettre à jour 5 uniquement sur le serveur cible maître. 

**Prise en charge de nouvelles plateformes**
* SUSE Linux Enterprise Server 11 Service Pack 4(SP4)

> [!NOTE]
> SLES 11 SP4 64 bits  **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** est fourni avec le package Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Téléchargez le package Scout GA à partir du portail, comme indiqué à [l’étape 1](#step-1-create-a-vault).
>

**Résolutions de bogues et améliorations**

* Augmenter la fiabilité de la prise en charge de Cluster Windows
    * Quelquefois fixe certaines hello P2V MSCS disques de cluster deviennent RAW après la récupération
    * Récupération de cluster MSCS de P2V fixed-échoue en raison de l’incompatibilité d’ordre toodisk
    * Corrigé : échec de l’opération d’ajout de disques au cluster MSCS en raison d’une disparité au niveau de la taille du disque.
    * Corrigé : échec de vérification de la préparation au mappage du cluster MSCS source avec RDM LUN lors de la vérification de la taille.
    * Protection des clusters fixed-unique nœud échoue en raison du problème d’incompatibilité de tooSCSI 
    * Fixed-Protégez à nouveau de hello P2V Windows cluster server échoue si les disques de cluster cible sont présents. 
    
* Au cours de la protection de la restauration automatique, si le serveur cible maître sélectionné n’est pas sur hello même ESXi serveur comme qui Hello protégé ordinateur source (durant une protection) vers l’avant, puis v-continuum récupère MT incorrect de hello lors de la récupération de la restauration automatique et échoue par la suite d’opération de récupération.

> [!NOTE]
> 
> * Au-dessus des correctifs P2V cluster est applicable tooonly ces cluster MSCS physique fraîchement protégés avec ASR Scout update5. correctifs de cluster tooavail hello sur hello déjà protégés dans le cluster MSCS de P2V avec les anciennes mises à jour, vous devez toofollow hello mise à niveau étapes mentionnées dans la section de hello 12, mise à niveau protégé P2V MSCS cluster tooScout Update5 de [ASR Scout version Notes](https://aka.ms/asr-scout-release-notes).
> 
> * Protégez à nouveau de cluster MSCS physique peut réutiliser les disques existants de cible uniquement si au moment de hello de reprotection, hello même ensemble de disques sont actifs sur chaque cluster hello nœuds qu’ils étaient lorsque initialement protégées. Si non, il n’y a des étapes manuelles comme indiqué dans la section 12 de [ASR Scout Release Notes](https://aka.ms/asr-scout-release-notes) trop déplacer hello cible côté disques toohello correct de banque de données chemin d’accès toore-utilisez les pendant la recréation de protection. Si vous protégez de nouveau cluster MSCS de hello en mode de P2V sans suivre les étapes de mise à niveau il sera créer nouveau disque sur le serveur de ESXi hello cible. Vous devez toomanually delete hello ancien des disques à partir de la banque de données hello.
> 
> * Chaque fois que la source SLES11 ou SLES11 avec n’importe quel serveur du service pack a été redémarré correctement, puis un doit marquer manuellement hello **racine** des paires de réplication pour re-synchronisation du disque car il ne sera pas informé dans CX UI. Si vous n’est pas ' marque hello racine disque de resynchronisation, vous pouvez voir les problèmes d’intégrité (DI) des données.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Azure Site Recovery Scout 8.0.1 Update 4
Scout Update 4 est une mise à jour cumulative. Il possède tous les correctifs hello de mise à jour 1 jusqu’au update3 et en suivant les nouveaux correctifs et améliorations.

**Prise en charge de nouvelles plateformes**

* Ajout de la prise en charge pour vCenter/vSphere 6.0, 6.1 et 6.2
* Ajout de la prise en charge des systèmes d’exploitation Linux suivants :
  * Red Hat Enterprise Linux (RHEL) 7.0, 7.1 et 7.2
  * CentOS 7.0, 7.1 et 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64 bits **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** est fourni avec le package Scout GA de base **InMage_Scout_Standard_8.0.1 GA.zip**. Téléchargez le package Scout GA à partir du portail, comme indiqué à [l’étape 1](#step-1-create-a-vault).
>
>

**Résolutions de bogues et améliorations**

* Arrêt amélioré la gestion de la suivante Linux OSes et clones tooprevent indésirables re-synchronisation des problèmes.
  * Red Hat Enterprise Linux (RHEL) 6.x
  * Oracle Linux (OL) 6.x
* Pour Linux, restreindre l’accès complet du dossier autorisations dans le répertoire d’installation unifiée de l’agent sont désormais uniquement toohello d’utilisateur local.
* Concernant le problème d’expiration de Windows lors de l’émission d’un signet de cohérence distribué commun sur les applications distribuées très chargées telles que les clusters SQL et SharePoint.
* Ajout d’un correctif lié aux journaux dans le programme d’installation de base CX.
* Lien de téléchargement de VMware vCLI 6.0 est ajouté tooWindows programme d’installation de la base principale cible.
* Ajout de plusieurs vérifications et journaux pour les modifications de configuration réseau pendant le basculement et les tests de récupération d’urgence.
* Les informations de rétention d’un certain temps ne sont pas signalé toohello CX.  
* Pour un cluster physique, l’opération de redimensionnement du volume via l’Assistant vContinuum échoue lors de la réduction du volume source.
* Échoué avec l’erreur « Signature de disque n’a pas pu toofind hello » de la protection du cluster lorsque le disque de cluster est disque PRDM.
* Blocage du serveur de transport cxps en raison de l’exception hors limites.
* Le nom du serveur et les colonnes IP sont à présent redimensionnables dans la page d’installation push de l’Assistant vContinuum.
* Améliorations de l’API RX
  * Fournit les cinq derniers points de cohérence communs disponibles (balises Only Guaranteed).
  * Fournit des détails de l’espace libre et de la capacité pour tous les hello périphériques protégés.
  * Fournit l’état du pilote Scout sur le serveur source.

> [!NOTE]
> * Le package de base **InMage_Scout_Standard_8.0.1_GA.zip** a maintenant mis à jour le programme d’installation de base CX **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** et le programme d’installation de base du serveur cible maître Windows **InMage_Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Pour toutes les nouvelles installations, utilisez les nouveaux bits GA du serveur cible maître Windows et CX.
> * Vous pouvez directement appliquer l’Update4 à 8.0.1 GA.
> * serveur de configuration Hello et RX des mises à jour ne peut pas être annulées après que elles sont appliquées sur le système de hello.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Azure Site Recovery Scout 8.0.1 Update 3
Mise à jour 3 inclut des éléments suivants de hello améliorations et correctifs de bogues :

* serveur de configuration Hello et RX échouent le coffre Site Recovery tooregister toohello lorsqu’ils sont derrière le proxy de hello.
* Hello nombre d’heures hello objectif de point de récupération (RPO) n’est pas remplie pas mise à jour dans le rapport d’intégrité de hello.
* serveur de configuration Hello n’est pas synchronisé avec RX lorsque les détails matériels hello ESX ou détails du réseau contient des caractères UTF-8.
* Les contrôleurs de domaine Windows Server 2008 R2 échouent tooboot après la récupération.
* La synchronisation hors connexion ne fonctionne pas comme prévu.
* Après le basculement de la machine virtuelle (VM), suppression de la paire de réplication se bloque dans hello CX UI pendant une longue période, et les utilisateurs ne peut pas terminer la restauration automatique hello ou opération de reprise.
* Ensemble des opérations de capture instantanée sont effectuent en cohérence hello ont été optimisées toohelp réduire application déconnecte tels que des clients SQL.
* performances Hello de l’outil de cohérence hello (VACP.exe) a été améliorée en réduisant l’utilisation de la mémoire hello qui est requise pour créer des instantanés de Windows.
* les défaillances du service d’installation poussée de Hello lorsque le mot de passe hello est supérieure à 16 caractères.
* v-continuum n’est pas la vérification et demander de nouvelles informations d’identification de vCenter lorsque les informations d’identification hello sont modifiées.
* Sur Linux, Gestionnaire de cache cible maître hello (cachemgr) ne télécharge pas les fichiers hello serveur de processus, ce qui entraîne la limitation de paire de réplication.
* Ordre des disques de cluster (MSCS) hello basculement physique est même ne Hello pas sur tous les nœuds de hello, la réplication n’est pas définie pour certaines des volumes de cluster hello.
  <br/>Notez que le cluster hello doit parti de tootake toobe reprotégée de ce correctif.  
* Fonctionnalité SMTP ne fonctionne pas comme prévu après que RX est mis à niveau à partir de Scout 7.1 tooScout 8.0.1.
* Plus les statistiques ont été ajoutés dans le journal de hello pour hello rollback tootrack hello durée de l’opération a pris toocomplete il.
* Prise en charge a été ajoutée pour les systèmes d’exploitation Linux sur le serveur de source de hello :
  * Red Hat Enterprise Linux (RHEL) 6 Update 7
  * CentOS 6 Update 7
* Hello CX et l’interface utilisateur RX affiche désormais notification hello pour paire hello, qui passe en mode de bitmap.
* Hello des correctifs de sécurité suivants ont été ajoutés dans RX :

| **Description du problème** | **Procédures de mise en œuvre** |
| --- | --- |
| Contournement de l’autorisation par falsification de paramètres |Utilisateurs toonon applicables à accès restreint. |
| Falsification de requête intersite |Concept de jeton de page implémenté hello, qui génère de façon aléatoire pour chaque page. <br/>En voici le résultat observable : <li> Il existe une seule connexion instance pour hello même utilisateur.</li><li>Actualisation de la page ne fonctionne pas--il redirige toohello le tableau de bord.</li> |
| Téléchargement de fichiers malveillants |Extensions de fichiers restreint toocertain. Extensions autorisées : 7z, aiff, asf, avi, bmp, csv, doc, docx, fla, flv, gif, gz, gzip, jpeg, jpg, log, mid, mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar, tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml et zip. |
| Scripts intersites permanents |Ajout des validations des entrées. |

> [!NOTE]
> * Toutes les mises à jour de Site Recovery sont cumulatives. Mise à jour 3 a tous les correctifs hello de mise à jour 1 et 2 de la mise à jour. Vous pouvez directement appliquer l’Update3 à 8.0.1 GA.
> * serveur de configuration Hello et RX des mises à jour ne peut pas être annulées après que elles sont appliquées sur le système de hello.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Azure Site Recovery Scout 8.0.1 Update 2 (Update 03Dec15)
Les révisions apportées dans Update 2 sont les suivantes :

* **Serveur de configuration**: correctif pour un problème qui empêchait la fonctionnalité de contrôle gratuite hello 31 jours de fonctionner comme prévu lorsque hello serveur de configuration a été enregistré dans la récupération de Site.
* **L’agent unifiée**: correctif pour un problème de mise à jour 1 qui a entraîné la mise à jour hello ne pas installé sur le serveur cible maître de hello lorsqu’il a été mis à niveau à partir de la version 8.0 too8.0.1.

### <a name="azure-site-recovery-scout-801-update-1"></a>Azure Site Recovery Scout 8.0.1 Update 1
Mise à jour 1 inclut des éléments suivants de hello correctifs de bogues et de nouvelles fonctionnalités :

* 31 jours de protection gratuite par instance de serveur. Cela vous permet de fonctionnalité tootest ou de configurer une preuve de concept.
  * Toutes les opérations sur le serveur hello, y compris le basculement et restauration, sont libres pour hello premier des 31 derniers jours, à partir de heure hello tout d’abord un serveur protégé avec Scout de récupération de Site.
  * À partir de hello 32nd jour et les versions ultérieures, chaque serveur protégé serez facturé au taux d’instances standard hello pour le site d’appartenant à un client Microsoft Azure Site Recovery protection tooa.
  * À tout moment, nombre hello des serveurs protégés qui sont actuellement en cours facturé est disponible sur la page de tableau de bord hello du coffre Azure Site Recovery de hello.
* Ajout de la prise en charge de vSphere vCLI (Command-Line Interface) 5.5 Update 2.
* Prend désormais en charge pour les systèmes d’exploitation Linux sur le serveur de source de hello :
  * RHEL 6 Update 6
  * RHEL 5 Update 11
  * CentOS 6 Update 6
  * CentOS 5 Update 11
* Correctifs de bogues hello de tooaddress suivants :
  * Échec de l’inscription du coffre pour serveur de configuration hello ou RX.
  * Les volumes de cluster n’apparaissent pas comme prévu quand les machines virtuelles en cluster sont à nouveau protégées lors de leur reprise.
  * La restauration automatique échoue lorsque le serveur cible maître de hello est hébergé sur un autre serveur ESXi à partir de machines virtuelles de production de local hello.
  * Autorisations de fichier de configuration sont modifiées lorsque vous mettez à niveau too8.0.1, ce qui affecte les opérations de protection et.
  * seuil de resynchronisation Hello n’est pas appliquée comme prévu, ce qui aboutit tooinconsistent comportement de la réplication.
  * paramètres de RPO Hello ne s’affichent pas correctement dans l’interface de serveur de configuration hello. valeur de données Hello non compressé affiche incorrectement les valeur de hello compressé.
  * l’opération de suppression Hello ne supprime pas comme prévu dans l’Assistant de v-continuum hello et la réplication n’est pas supprimée de l’interface de serveur de configuration hello.
  * Dans l’Assistant de v-continuum hello, disque de hello est automatiquement non sélectionnée lorsque vous cliquez sur **détails** dans la vue de disque hello au cours de la protection des machines virtuelles MSCS.
  * Au cours de hello physique-à-virtuel (P2V) donc services HP requis, tels que CIMnotify et CqMgHost, ne sont pas toomanual déplacé dans la récupération de l’ordinateur virtuel. Cela allonge la durée de démarrage.
  * Protection des machines virtuelles Linux échoue lorsqu’il y a plus de 26 disques sur le serveur cible maître de hello.

## <a name="next-steps"></a>Étapes suivantes
Publier des questions sur hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
