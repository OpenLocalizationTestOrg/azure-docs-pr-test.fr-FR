---
title: "aaaStorSimple Virtual Array d’urgence récupération et basculement d’unités | Documents Microsoft"
description: "En savoir plus sur la façon toofailover votre StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 3c1f9c62-af57-4634-a0d8-435522d969aa
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5f125efd1ffb94489cdfa7cfaafae7d57cc10131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-and-device-failover-for-your-storsimple-virtual-array-via-azure-portal"></a>Basculement d'appareil et récupération d'urgence pour votre StorSimple Virtual Array via le portail Azure

## <a name="overview"></a>Vue d'ensemble
Cet article décrit la récupération d’urgence hello pour Microsoft Azure StorSimple Virtual tableau est notamment hello détaillée étapes toofail sur l’unité de stockage virtuelle tooanother. Un basculement vous permet de toomove vos données à partir d’un *source* appareil dans hello datacenter tooa *cible* appareil. Hello appareil cible peut être situé dans hello même ou à un emplacement géographique différent. basculement de l’appareil Hello est pour l’ensemble de l’unité hello. Pendant le basculement, modification des données de cloud hello pour appareil de source de hello toothat de la propriété de l’appareil cible de hello.

Cet article est applicable tooStorSimple tableaux virtuels uniquement. toofail sur un appareil de 8000 série, accédez trop[appareil basculement et récupération d’urgence de votre appareil StorSimple](storsimple-device-failover-disaster-recovery.md).

## <a name="what-is-disaster-recovery-and-device-failover"></a>En quoi consistent la récupération d’urgence et le basculement d’appareil ?

Dans un scénario de récupération d’urgence, périphérique principal de hello cesse de fonctionner. Dans ce scénario, vous pouvez déplacer les données de cloud hello associées hello ayant échoué tooanother un périphérique. Vous pouvez utiliser le périphérique principal de hello comme hello *source* et spécifiez un autre périphérique en tant que hello *cible*. Ce processus est référencé tooas hello *basculement*. Pendant le basculement, toutes les hello volumes ou partages hello à partir de l’appareil source de hello changent de propriétaire et sont transférés toohello du périphérique cible. Aucun filtrage de données de hello n’est autorisé.

Récupération d’urgence est modélisée en tant qu’une restauration complète de l’appareil à l’aide de la chaleur hello – base mappage aux niveaux et de suivi. Une carte de chaleur est définie en assignant un toohello de valeur de chaleur données en fonction de lecture et d’écriture de modèles. Cette chaleur mapper puis niveaux hello tout d’abord la plus faible chaleur données segments toohello dans le cloud tout en conservant les segments de données hello chaleur élevée (plus utilisé) de niveau de local hello. Pendant une récupération d’urgence, StorSimple utilise toorestore de carte de chaleur hello de réalimenter les données hello du cloud de hello. Appareil de Hello extrait tous les volumes/partages hello dans la dernière sauvegarde de récente hello (comme déterminé en interne) et effectue une restauration à partir de cette sauvegarde. unité de stockage virtuelle Hello orchestre tout processus de récupération d’urgence hello.

> [!IMPORTANT]
> Appareil de source de Hello est supprimé à fin hello de basculement de l’appareil et par conséquent, une restauration automatique n’est pas pris en charge.
> 
> 

Récupération d’urgence est orchestrée via la fonctionnalité de basculement d’appareil hello et est lancée à partir de hello **périphériques** panneau. Ce panneau classifie tous les hello StorSimple périphériques connectés tooyour périphérique le service StorSimple Manager. Pour chaque périphérique, vous pouvez voir le nom convivial de hello, état, la capacité configurée et maximale, type et modèle.

## <a name="prerequisites-for-device-failover"></a>Configuration requise pour le basculement d'appareil

### <a name="prerequisites"></a>Composants requis

Pour un basculement de l’appareil, vérifiez que hello suivant les conditions préalables sont remplies :

* Appareil de source de Hello doit toobe dans un **désactivé** état.
* Hello appareil cible doit tooshow des comme **prêt tooset des** Bonjour portail Azure. Configurer un tableau virtuel de la cible de hello capacité identique ou supérieure. Tooconfigure de l’interface utilisateur web locale hello et correctement tableau virtuel de hello cible.
  
  > [!IMPORTANT]
  > N’essayez pas de tooconfigure hello virtuel périphérique enregistré via le service de hello. Aucune configuration de périphérique ne doit être effectuée via le service de hello.
  > 
  > 
* Appareil de Hello cible ne peut pas avoir hello même nom en tant que périphérique de source de hello.
* Hello périphérique source et cible ont toobe hello du même type. Vous pouvez uniquement basculer vers un tableau virtuel configuré en tant que fichier tooanother fichier server. Hello même a la valeur true pour un serveur iSCSI.
* Pour un récupération d’urgence du serveur de fichiers, nous recommandons que vous joignez hello cible appareil toohello même domaine comme source de hello. Cette configuration garantit que les autorisations de partage hello sont résolues automatiquement. Uniquement hello basculement tooa appareil cible Bonjour même domaine.
* unités cibles disponibles de Hello pour la récupération d’urgence sont les appareils sur lesquels hello même ou de capacité supérieure comparé toohello appareil. Hello périphériques qui sont connecté tooyour de service, mais ne répondent pas aux hello suffisamment d’espace n’est pas disponibles en tant que périphériques cibles.

### <a name="other-considerations"></a>Autres points à considérer

* Pour un basculement planifié 
  
  * Nous vous recommandons d’effectuer tous les volumes de hello ou de partages sur l’appareil en mode hors connexion de hello source.
  * Nous recommandons que vous effectuez une sauvegarde de l’appareil de hello et poursuivez la perte de données hello basculement toominimize. 
* Pour un basculement non planifié, appareil de hello utilise les données les plus récentes toorestore sauvegarde hello hello.

### <a name="device-failover-prechecks"></a>Vérifications préalables au basculement de l’appareil

Avant de hello que commence de récupération d’urgence, appareil de hello effectue prechecks. Ces vérifications permettent d’éliminer les risques de survenue d’erreurs une fois la récupération d’urgence commencée. Hello prechecks sont les suivantes :

* Validation du compte de stockage hello.
* Vérification de la tooAzure de connectivité cloud hello.
* Vérification de l’espace disponible sur le périphérique cible de hello.
* Vérification de la validité des noms ACR du volume de l’appareil source
  
  * d’un serveur iSCSI
  * Validité du nom IQN (moins de 220 caractères)
  * Validité des mots de passe CHAP (12 à 16 caractères)

Si un de hello précédant prechecks échoue, vous ne peut pas poursuivre hello récupération d’urgence. Vous devez résoudre ces problèmes, puis réessayer d’exécuter la récupération d’urgence.

Après que hello récupération d’urgence est terminé avec succès, la propriété hello des données du cloud hello sur périphérique source de hello est équipement toohello transférés. Appareil de source de Hello puis n’est plus disponible dans le portail de hello. Accès tooall hello volumes/partages sur l’appareil source de hello est bloqué et équipement hello devient actif.

> [!IMPORTANT]
> Bien que l’appareil de hello n’est plus disponible, hello virtuels que vous avez configuré sur le système hôte de hello toujours consomme des ressources. Une fois que hello récupération d’urgence est correctement terminée, vous pouvez supprimer cet ordinateur virtuel à partir de votre système hôte.
> 
> 

## <a name="fail-over-tooa-virtual-array"></a>Basculer le tableau de virtuel tooa

Avant d’exécuter cette procédure, nous vous recommandons d’approvisionner, de configurer et d’inscrire un autre StorSimple Virtual Array auprès de votre service StorSimple Device Manager.

> [!IMPORTANT]
> 
> * Vous ne pouvez pas basculer à partir d’un appareil StorSimple 8000 series appareil tooa 1200 virtuel.
> * Vous pouvez basculer à partir d’un traitement Standard FIPS (Federal Information) activé périphérique virtuel tooanother FIPS activé périphérique ou tooa non-FIPS déployé dans le portail d’administration hello.


Effectuer hello suivant les étapes toorestore hello appareil tooa cible un appareil virtuel StorSimple.

1. Approvisionner et configurer un appareil cible qui répond à hello [configuration requise pour le basculement de l’appareil](#prerequisites). Terminer la configuration de l’appareil via l’interface utilisateur de web locale hello hello et inscrire le service du Gestionnaire de périphériques StorSimple tooyour. Si la création d’un serveur de fichiers, accédez à toostep 1 de [configuré en tant que serveur de fichiers](storsimple-virtual-array-deploy3-fs-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device). Si la création d’un serveur iSCSI, accédez à toostep 1 de [configuré en tant que serveur iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md#step-1-complete-the-local-web-ui-setup-and-register-your-device).

2. Prendre les volumes/partages hors connexion sur l’ordinateur hôte de hello. tootake hello volumes/partages hors connexion, consultez toohello des instructions spécifiques au système d’exploitation pour l’hôte de hello. S’il y a pas déjà en mode hors connexion, vous devez tootake tous les hello volumes/partages hors connexion sur l’appareil de hello en procédant comme suit de hello.
   
    1. Accédez trop**périphériques** panneau et sélectionnez votre appareil.
   
    2. Accédez trop**Paramètres > Gérer > partages** (ou **Paramètres > Gérer > Volumes**). 
   
    3. Sélectionnez un partage/volume, cliquez avec le bouton droit et sélectionnez **Mettre hors connexion**. 
   
    4. Lorsque vous êtes invité à confirmer l’opération, vérifiez **je comprends impact hello de mise hors connexion de ce partage.** 
   
    5. Cliquez sur **Mettre hors connexion**.

3. Dans votre service StorSimple le Gestionnaire de périphériques, accédez trop**Gestion > appareils**. Bonjour **périphériques** panneau, sélectionnez et cliquez sur votre appareil source.

4. Dans le **tableau de bord de votre appareil**, cliquez sur **Désactiver**.

5. Bonjour **Deactivate** panneau, vous êtes invité à confirmer l’opération. La désactivation d’appareil est une opération *définitive* qui ne peut pas être annulée. Vous est également tootake relancée vos partages/volumes hors connexion sur l’ordinateur hôte de hello. Tapez tooconfirm de nom de périphérique hello et cliquez sur **Deactivate**.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover1.png)
6. désactivation de Hello démarre. Vous recevrez une notification après que la désactivation de hello est terminée avec succès.
   
    ![](./media/storsimple-virtual-array-failover-dr/failover2.png)
7. Sur la page de périphériques hello, état de l’appareil hello est maintenant modifier trop**désactivé**.
    ![](./media/storsimple-virtual-array-failover-dr/failover3.png)
8. Bonjour **périphériques** panneau, sélectionnez et cliquez sur périphérique source désactivés de hello pour le basculement. 
9. Bonjour **tableau de bord périphérique** panneau, cliquez sur **basculer**. 
10. Bonjour **basculer appareil** panneau, hello suivant :
    
    1. Hello source appareil est automatiquement renseigné. Notez la taille totale des données de hello pour appareil de source de hello. taille des données Hello doit être inférieur à la capacité disponible de hello sur le périphérique cible de hello. Examinez les détails de hello associés avec périphérique source de hello comme nom de l’appareil, capacité totale et noms hello de partages hello ayant basculé.

    2. Dans la liste déroulante de hello de périphériques disponibles, choisissez un **appareil cible**. Seuls les appareils hello ayant une capacité sont affichés dans la liste déroulante de hello.

    3. Vérifiez que **je comprends que cette opération échoue sur l’unité cible de données toohello**. 

    4. Cliquez sur **Effectuer un basculement**.
    
        ![](./media/storsimple-virtual-array-failover-dr/failover4.png)
11. Un travail de basculement est lancé et vous recevez une notification. Accédez trop**périphériques > travaux** toomonitor hello basculement.
    
     ![](./media/storsimple-virtual-array-failover-dr/failover5.png)
12. Bonjour **travaux** panneau, vous voyez un travail de basculement créé pour le périphérique de source de hello. Ce travail effectue prechecks de récupération d’urgence hello.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover6.png)
    
     Une fois hello DR prechecks sont réussies, travail de basculement hello génèrera des travaux de restauration pour chaque volume/partage qui existe sur votre appareil source.
    
    ![](./media/storsimple-virtual-array-failover-dr/failover7.png)
13. Une fois le basculement de hello terminée, accédez toohello **périphériques** panneau.
    
    1. Sélectionnez et cliquez sur l’appareil StorSimple hello qui a été utilisé en tant que périphérique cible de hello pour les processus de basculement hello.
    2. Accédez trop**Paramètres > Administration > partages** (ou **Volumes** si le serveur iSCSI). Bonjour **partages** panneau, vous pouvez afficher tous les partages de hello (volumes) à partir de l’ancien périphérique de hello.
        ![](./media/storsimple-virtual-array-failover-dr/failover9.png)
14. Vous devez trop[créer un alias DNS](https://support.microsoft.com/kb/168322) afin que tous les hello les applications qui essaient de tooconnect peut obtenir toohello redirigé nouveau périphérique.

## <a name="errors-during-dr"></a>Erreurs lors de la récupération d'urgence

**Panne de connectivité cloud pendant la récupération d'urgence**

Si la connectivité de cloud hello est interrompue après la récupération d’urgence a démarré et avant la restauration de l’unité hello est terminée, hello récupération d’urgence échoue. Vous recevez une notification d’échec. équipement Hello pour la récupération d’urgence est marqué comme *inutilisable.* Vous ne pouvez pas utiliser hello même appareil cible pour le service DRs futures.

**Aucun appareil cible compatible**

Si les appareils cibles disponibles hello ne disposez pas de suffisamment d’espace, vous consultez un effet de toohello erreur qu’il n’y a aucun appareil cible compatible.

**Échecs des vérifications préalables**

Si un des hello prechecks n’est pas satisfait, vous verrez les échecs precheck.

## <a name="business-continuity-disaster-recovery-bcdr"></a>Continuité d’activité et récupération d’urgence (Business Continuity Disaster Recovery - BCDR)

Un scénario de récupération d’urgence d’entreprise la continuité des activités se produit lorsque le centre de données Azure entier hello cesse de fonctionner. Cela peut affecter votre service de gestionnaire de périphériques StorSimple et hello associés appareils StorSimple.

S’il existe des appareils StorSimple qui ont été inscrits juste avant un incident, ces appareils StorSimple peut-être toobe supprimé. Après sinistre de hello, vous pouvez recréer et configurer ces appareils.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la façon trop[administrer votre tableau virtuel StorSimple à l’aide de l’interface utilisateur de web local hello](storsimple-ova-web-ui-admin.md).

