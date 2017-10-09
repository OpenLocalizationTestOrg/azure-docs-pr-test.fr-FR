---
title: aaaBack portail classique de DPM les charges de travail tooAzure | Documents Microsoft
description: "Un toobacking introduction des serveurs DPM à l’aide du service de sauvegarde Azure hello"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: System Center Data Protection Manager, Data Protection Manager, sauvegarde DPM
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Préparation de tooback des tooAzure les charges de travail avec DPM
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (Classic)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Classic)](backup-azure-dpm-introduction-classic.md)
>
>

Cet article fournit une tooprotect de Microsoft Azure Backup introduction toousing vos serveurs de System Center Data Protection Manager (DPM) et les charges de travail. En le lisant, vous comprendrez :

* le fonctionnement de la sauvegarde du serveur Azure DPM ;
* conditions préalables de Hello tooachieve une meilleure expérience de sauvegarde
* Hello a rencontré des erreurs courantes et comment toodeal avec eux
* Scénarios pris en charge

System Center DPM sauvegarde les données des fichiers et des applications. Données sauvegardées tooDPM peuvent être stockées sur une bande, sur disque, ou sauvegardées tooAzure avec Microsoft Azure Backup. DPM interagit avec Azure Backup comme suit :

* **DPM déployé comme un serveur physique ou sur site virtual machine** : si DPM est déployé comme serveur physique ou comme machine virtuelle Hyper-V local que vous pouvez sauvegarder des données tooan de Azure Backup vault en outre toodisk et sauvegarde sur bande.
* **DPM déployé comme une machine virtuelle Azure** : depuis la mise à jour 3 de System Center 2012 R2, DPM peut être déployé comme une machine virtuelle Azure. Si DPM est déployé comme une machine virtuelle Azure, que vous pouvez sauvegarder des disques de données tooAzure jointe toohello une machine virtuelle Azure de DPM, ou vous pouvez décharger le stockage de données hello en le sauvegardant tooan le coffre Azure Backup.

## <a name="why-backup-your-dpm-servers"></a>Pourquoi sauvegarder vos serveurs DPM ?
Hello entreprise de l’utilisation d’Azure Backup pour sauvegarder des serveurs DPM principaux avantages :

* Pour le déploiement du DPM local, vous pouvez utiliser sauvegarde Azure comme un tootape de déploiement autre toolong à long terme.
* Pour les déploiements DPM dans Azure, Azure Backup permet le stockage toooffload d’hello disque Azure, ce qui vous tooscale en stockant les données plus anciennes dans Azure Backup et les données sur le disque.

## <a name="how-does-dpm-server-backup-work"></a>Comment fonctionne la sauvegarde d'un serveur DPM ?
tooback une machine virtuelle, la première d’un instantané de point-à-temps des données de hello est nécessaire. heure planifiée de Hello Azure Backup service lance hello travail de sauvegarde à hello et déclencheurs hello extension de sauvegarde tootake un instantané. coordonnées d’extension de sauvegarde Hello avec hello dans l’invité VSS tooachieve cohérence de service et appelle l’API de capture instantanée de blob de hello Hello service de stockage Azure une fois que la cohérence a été atteint. Cela est fait tooget un instantané cohérent de disques hello de machine virtuelle de hello, sans avoir tooshut vers le bas.

Après la réalisation de la capture instantanée de hello, les données de salutation sont transférées par hello Azure Backup service toohello coffre de sauvegarde. service de Hello s’occupe d’identification et de transférer uniquement les blocs de hello qui ont changé depuis la dernière sauvegarde de la hello optimiser le stockage de sauvegardes hello et de réseau. Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé. Ce point de récupération peut être consulté dans hello portail Azure classic.

> [!NOTE]
> Pour les machines virtuelles Linux, seule une sauvegarde cohérente au niveau des fichiers est possible.
>
>

## <a name="prerequisites"></a>Composants requis
Préparez tooback Azure sauvegarde des données DPM comme suit :

1. **Créez un coffre de sauvegarde**. Si vous n’avez pas créé un coffre de sauvegarde dans votre abonnement, consultez hello Azure portail version de cet article - [préparer tooback des tooAzure les charges de travail avec DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
  > Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
  >- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
  >- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
  >

2. **Télécharger les informations d’identification de coffre** — dans Azure Backup, certificat de gestion de hello téléchargement vous avez créé le coffre toohello.
3. **Installez hello Agent Azure Backup et inscrivez auprès hello** : à partir de Azure Backup, installez l’agent de hello sur chaque serveur DPM et inscrivez le serveur DPM hello dans le coffre de sauvegarde hello.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Spécifications (et limitations)
* DPM peut s'exécuter en tant que serveur physique ou machine virtuelle Hyper-V installée sur System Center 2012 SP1 ou System Center 2012 R2. DPM peut également s'exécuter en tant que machine virtuelle Azure sur System Center 2012 R2 avec au moins le correctif cumulatif 3 pour DPM 2012 R2, ou en tant que machine virtuelle Windows dans VMWare sur System Center 2012 R2 avec au moins le correctif cumulatif 5.
* Si vous exécutez DPM avec System Center 2012 SP1, vous devez installer le correctif cumulatif 2 pour System Center Data Protection Manager SP1. Cela est nécessaire avant de pouvoir installer hello Azure Backup Agent.
* le serveur DPM Hello doit avoir Windows PowerShell et .net Framework 4.5 est installé.
* DPM peut sauvegarder la plupart des charges de travail tooAzure sauvegarde. Pour obtenir la liste complète de ce qui a pris en charge Voir hello Azure Backup prend en charge les éléments ci-dessous.
* Impossible de récupérer les données stockées dans Azure Backup avec l’option de « copier tootape » hello.
* Vous devez avoir un compte Azure avec fonctionnalité Azure Backup hello est activée. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. En savoir plus sur la [tarification d'Azure Backup](https://azure.microsoft.com/pricing/details/backup/).
* À l’aide d’Azure Backup nécessite hello toobe de l’Agent Azure Backup installé sur les serveurs hello souhaité tooback des. Chaque serveur doit avoir au moins 10 % de la taille de hello des données hello sont en cours de sauvegarde, disponible en tant qu’espace de stockage local. Par exemple, la sauvegarde de 100 Go de données nécessite un minimum de 10 Go d’espace libre dans l’emplacement de fichier temporaire hello. Hello minimale est de 10 %, 15 % de toobe d’espace libre de stockage local utilisé pour l’emplacement du cache hello est recommandée.
* Bonjour, stockage d’archivage Azure, les données seront stockées. Il n’existe aucun montant de toohello limite de données, que vous pouvez sauvegarder le coffre Azure Backup tooan mais taille hello d’une source de données (par exemple un ordinateur virtuel ou une base de données) ne doit pas dépasser 54,400 Go.

Ces types de fichiers sont pris en charge pour tooAzure de sauvegarde :

* Chiffré (sauvegardes complètes uniquement)
* Compressé (sauvegardes incrémentielles prises en charge)
* Partiellement alloué (sauvegardes incrémentielles prises en charge)
* Compressé et partiellement alloué (traité comme partiellement alloué)

Et les types suivants ne sont pas pris en charge :

* Les serveurs sur des systèmes de fichiers respectant la casse ne sont pas pris en charge.
* Liens physiques (ignorés)
* Points d'analyse (ignorés)
* Chiffré et compressé (ignoré)
* Chiffré et partiellement alloué (ignoré)
* Flux compressé
* Flux partiellement alloué

> [!NOTE]
> À partir de System Center 2012 DPM avec SP1 et versions ultérieures, vous pouvez sauvegarder des charges de travail protégés par tooAzure DPM à l’aide de Microsoft Azure Backup.
>
>
