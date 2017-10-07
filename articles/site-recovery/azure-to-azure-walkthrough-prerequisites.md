---
title: "aaaBefore commencer la réplication des machines virtuelles Azure tooanother région | Des documents Microsoft"
description: "Résume les étapes hello vous devez tootake avant de répliquer les machines virtuelles Azure entre les régions Azure, à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Étape 2 : avant de commencer

Une fois que vous avez consulté hello [architecture](azure-to-azure-walkthrough-architecture.md) pour la réplication des machines virtuelles (VM) entre les régions Azure avec [Azure Site Recovery](site-recovery-overview.md), utilisez cette configuration requise tooverify de l’article. 

- Lorsque vous avez terminé l’article de hello, vous devez avoir un effacement de ce qui est nécessaire de déploiement de hello toomake de travail et avez effectué les étapes de configuration requise hello.
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> La réplication de machines virtuelles Azure est actuellement disponible en préversion.



## <a name="support-recommendations"></a>Recommandations de prise en charge

Tableau de hello revue ci-dessous.

**Composant** | **Prérequis**
--- | ---
**Coffre Recovery Services** | Nous vous recommandons de créer un coffre de Services de récupération dans la cible de hello région Azure que vous souhaitez toouse pour la récupération d’urgence. Par exemple, si vous souhaitez tooreplicate source machines virtuelles dans États-Unis tooCentral des États-Unis, vous pouvez créer hello coffre dans le centre des États-Unis.
**Abonnement Azure** | Votre abonnement Azure doit être activé toocreate machines virtuelles, dans emplacement cible de hello que vous souhaitez toouse comme région de récupération d’urgence hello. Contactez le support technique tooenable hello quota requis.
**Capacité de la région cible** | Dans la cible de hello région Azure, abonnement de hello doit avoir une capacité suffisante pour les ordinateurs virtuels, les comptes de stockage et les composants réseau.
**Stockage** | Hello d’utilisation [conseils de stockage](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) pour votre source de machines virtuelles Azure, les problèmes de performances tooavoid.<br/><br/> Comptes de stockage doivent être Bonjour même région que le coffre hello.<br/><br/> Vous ne peut pas répliquer toopremium des comptes dans le centre et de l’Inde du Sud.<br/><br/> Si vous déployez la réplication avec des paramètres par défaut de hello, Site Recovery crée les comptes de stockage hello requis en fonction de la configuration de la source hello. Si vous personnalisez des paramètres, suivez hello [objectifs d’évolutivité pour les disques de machine virtuelle](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Mise en réseau** | Vous devez tooallow la connectivité sortante à partir de machines virtuelles Azure, pour des plages d’adresse IP/URL spécifiques.<br/><br/> Comptes de réseau doivent être Bonjour même région que le coffre hello. 
**Microsoft Azure** | Assurez-vous que tous les certificats racine dernières hello se trouvent sur hello Windows/Linux Azure VM. S’ils ne sont pas, vous ne serez en mesure de tooregister hello machine virtuelle en cours de récupération de Site, en raison de contraintes de sécurité.
**Compte d’utilisateur Azure** | Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’une machine virtuelle Azure.

Obtenir une liste complète des exigences de prise en charge dans hello [matrice de prise en charge](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Définir les autorisations sur le compte de hello

1. En savoir plus sur hello [autorisations](site-recovery-role-based-linked-access-control.md) nécessaire pour la réplication.
2. Suivez ces [instructions](../active-directory/role-based-access-control-configure.md#add-access) tooadd autorisations.


## <a name="verify-target-resources"></a>Vérifier les ressources cibles

1. Activer votre abonnement Azure de tooallow vous VMs toocreate Bonjour cibler la région toouse pour la récupération d’urgence que vous souhaitez toouse comme région de récupération d’urgence hello. Contactez le support technique tooenable hello quota requis.
2. Assurez-vous que votre abonnement a suffisamment tooenable ressources machines virtuelles avec des tailles qui correspondent à votre source de machines virtuelles. Par défaut, lorsque la valeur de la réplication, Site Recovery récupère hello même taille pour hello cibler les ordinateurs virtuels ou hello taille la plus proche possible. En savoir plus sur la [résolution des problèmes](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) liés aux ressources cibles.

## <a name="verify-azure-vm-certificates"></a>Vérifier les certificats des machines virtuelles Azure

1. Vérifiez que tous les certificats racine de la dernière hello sont présents sur les Windows hello ou vous souhaitez tooreplicate les machines virtuelles Linux. Si les certificats racine dernières hello ne sont pas présents, hello machine virtuelle ne peut pas être inscrit tooSite récupération en raison de contraintes de toosecurity.
2. Pour les machines virtuelles Windows, procédez comme hello suivant :

    - Installez tous les hello dernières mises à jour Windows sur hello VM afin que tous les certificats racine de hello approuvé sont sur l’ordinateur de hello.
    - Dans un environnement déconnecté, suivez hello standard Windows Update processus/certificat mise à jour de processus dans votre organisation, les certificats racine dernières tooget hello et mis à jour la liste CRL sur des machines virtuelles de hello.
3. Pour les machines virtuelles Linux, suivez les instructions de hello fournie par votre liste de révocation de certificats plus récente hello sur hello machine virtuelle Linux distributeur tooget hello plus récente des certificats racine approuvés. En savoir plus sur la [résolution des problèmes](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) liés aux certificats racines approuvés.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 3 : planifier la mise en réseau](azure-to-azure-walkthrough-network.md) tooset la connectivité sortante.
