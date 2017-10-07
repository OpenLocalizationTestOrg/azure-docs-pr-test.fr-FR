---
title: aaaConfigure MPIO pour votre appareil StorSimple | Documents Microsoft
description: "Décrit comment tooconfigure MPIO (Multipath i / o) pour votre appareil StorSimple connectées hôte tooa exécutant Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7796524edc739826ba1e977161fc9988c6d316e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Configuration de Multipath I/O pour votre appareil StorSimple

Ce didacticiel décrit les étapes de hello vous devez suivre tooinstall et utiliser la fonctionnalité MPIO (Multipath i / o) de hello sur un ordinateur hôte exécutant Windows Server 2012 R2 et connecté tooa appareil physique StorSimple. les instructions de Hello dans cet article s’appliquent tooStorSimple 8000 series périphériques physiques uniquement. La fonctionnalité MPIO n’est actuellement pas prise en charge sur StorSimple Cloud Appliance.

Microsoft a créé le support pour la fonctionnalité MPIO (Multipath i / o) de hello dans Windows Server toohelp générer les configurations SAN haute disponibilitées et à tolérance de pannes. MPIO utilise les composants de chemin d’accès physique redondants, cartes, des câbles et commutateurs : toocreate les chemins d’accès logiques entre le serveur de hello et de périphérique de stockage hello. S’il existe une défaillance d’un composant, à l’origine d’un chemin d’accès logique toofail, logique multivoie utilise un autre chemin d’e/s afin que les applications peuvent toujours accéder à leurs données. En outre selon votre configuration, MPIO peut également améliorer les performances en rééquilibrant hello charge sur ces chemins d’accès. Pour plus d’informations, consultez la [Présentation de MPIO](https://technet.microsoft.com/library/cc725907.aspx "Présentation de MPIO and features").

Pour hello haute disponibilité de votre solution StorSimple MPIO doit être configuré sur votre appareil StorSimple. MPIO est installé sur vos serveurs de l’hôte exécutant Windows Server 2012 R2, les serveurs hello peuvent tolérer puis un lien, un réseau ou une défaillance de l’interface.

## <a name="mpio-configuration-summary"></a>Résumé de la configuration MPIO

MPIO est une fonctionnalité facultative sur Windows Server et n’est pas installé par défaut. Il doit être installé en tant que fonctionnalité via le Gestionnaire de serveur.

Suivez ces étapes de tooconfigure MPIO sur votre appareil StorSimple :

* Étape 1 : Installer MPIO sur un hôte Windows hello
* Étape 2 : configurer MPIO pour les volumes StorSimple
* Étape 3 : Monter des volumes StorSimple sur l’ordinateur hôte de hello
* Étape 4 : configurer MPIO pour la haute disponibilité et l’équilibrage de charge

Chacune des étapes précédentes de hello est expliqué dans les sections suivantes de hello.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Étape 1 : Installer MPIO sur un hôte Windows hello

fin de cette fonctionnalité sur votre hôte Windows Server, tooinstall hello suivant la procédure.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO sur l’ordinateur hôte de hello

1. Ouvrez le Gestionnaire de serveur sur votre hôte Windows Server. Par défaut, le Gestionnaire de serveur démarre lorsqu’un membre du groupe des administrateurs de hello ouvre une session sur l’ordinateur tooa qui exécute Windows Server 2012 R2 ou Windows Server 2012. Si hello Gestionnaire de serveur n’est pas déjà ouvert, cliquez sur **Démarrer > Gestionnaire de serveur**.
   
   ![Gestionnaire de serveur](./media/storsimple-configure-mpio-windows-server/IC740997.png)

2. Cliquez sur **Gestionnaire de serveur > Tableau de bord > Ajouter des rôles et fonctionnalités**. Cela démarre hello **Ajout de rôles et fonctionnalités** Assistant.
   
   ![Assistant Ajouter des rôles et fonctionnalités 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. Bonjour **Ajout de rôles et fonctionnalités** Assistant, effectuez hello comme suit :
   
   1. Sur hello **avant de commencer** , cliquez sur **suivant**.
   2. Sur hello **sélectionner le type d’installation** page, acceptez le paramètre par défaut hello **en fonction du rôle ou une fonctionnalité** installation. Cliquez sur **Suivant**.
   
       ![Assistant Ajouter des rôles et fonctionnalités 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   3. Sur hello **serveur de destination sélectionnez** choisissez **sélectionner un serveur de pool de serveurs hello**. Votre serveur hôte doit être détecté automatiquement. Cliquez sur **Suivant**.
   4. Sur hello **sélectionner des rôles de serveur** , cliquez sur **suivant**.
   5. Sur hello **sélectionner des fonctionnalités** , sélectionnez **MPIO**, puis cliquez sur **suivant**.
   
       ![Assistant Ajouter des rôles et fonctionnalités 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   6. Sur hello **confirmer les sélections d’installation** page, confirmer la sélection de hello, puis sélectionnez **redémarrez le serveur de destination hello automatiquement si nécessaire**, comme illustré ci-dessous. Cliquez sur **Installer**.
   
       ![Assistant Ajouter des rôles et fonctionnalités 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   7. Vous êtes informé lorsque hello installation est terminée. Cliquez sur **fermer** Assistant de hello tooclose.
   
       ![Assistant Ajouter des rôles et fonctionnalités 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Étape 2 : configurer MPIO pour les volumes StorSimple

MPIO doit être configuré tooidentify des volumes StorSimple. volumes de StorSimple toorecognize tooconfigure MPIO, effectuer hello comme suit.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure MPIO pour des volumes StorSimple

1. Ouvrez hello **configuration MPIO**. Cliquez sur **Gestionnaire de serveur > Tableau de bord > Outils > MPIO**.
2. Bonjour **propriétés MPIO** boîte de dialogue, sélectionnez hello **découvrir plusieurs chemins** onglet.
3. Sélectionnez **Ajouter la prise en charge des périphériques iSCSI**, puis cliquez sur **Ajouter**.  
   ![Chemins d’accès multiples de détection de propriétés MPIO](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Redémarrez le serveur hello lorsque vous y êtes invité.
5. Bonjour **propriétés MPIO** boîte de dialogue, cliquez sur hello **périphériques MPIO** onglet. Cliquez sur **ajouter**.
    </br>![Propriétés MPIO Périphériques MPIO](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. Bonjour **ajouter la prise en charge MPIO** boîte de dialogue **ID de matériel de périphérique**, entrez votre numéro de série du périphérique. tooget hello accès number, série des appareils de votre service de gestionnaire de périphériques StorSimple. Accédez trop**périphériques > tableau de bord**. numéro de série du périphérique Hello s’affiche dans hello droit **aperçu rapide** volet du tableau de bord du périphérique hello.
    </br>
    ![Ajouter la prise en charge MPIO](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Redémarrez le serveur hello lorsque vous y êtes invité.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Étape 3 : Monter des volumes StorSimple sur l’ordinateur hôte de hello

Une fois MPIO est configuré sur Windows Server, ou les volumes créés sur l’appareil StorSimple hello peuvent être montés et peuvent ainsi profiter de MPIO pour assurer la redondance. toomount un volume, exécutez hello comme suit.

#### <a name="toomount-volumes-on-hello-host"></a>volumes toomount sur l’ordinateur hôte de hello

1. Ouvrez hello **propriétés de l’initiateur iSCSI** fenêtre sur l’hôte du serveur de Windows hello. Cliquez sur **Gestionnaire de serveur > Tableau de bord > Outils > Initiateur iSCSI**.
2. Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue, cliquez sur onglet de découverte hello, puis cliquez sur **détecter un portail cible**.
3. Bonjour **détecter un portail cible** boîte de dialogue, exécutez hello comme suit :
   
   1. Entrez l’adresse IP hello hello port de données de votre appareil StorSimple (par exemple, entrez DATA 0).
   2. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue.
     
     > [!IMPORTANT]
     > **Si vous utilisez un réseau privé pour les connexions iSCSI, entrez hello adresseIP du port de données hello qui est le réseau privé de toohello connecté.**
    
4. Répétez les étapes 2 et 3 pour une deuxième interface réseau (par exemple, DATA 1) sur votre périphérique. N’oubliez pas que ces interfaces doivent être activées pour iSCSI. Pour plus d’informations, consultez [Modification des interfaces réseau](storsimple-8000-modify-device-config.md#modify-network-interfaces).
5. Sélectionnez hello **cibles** onglet Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue. Vous devez voir l’appareil StorSimple hello IQN sous cible **cibles découvertes**.

   ![Onglet Cibles des propriétés de l’initiateur iSCSI](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Cliquez sur **Connect** tooestablish une session iSCSI avec votre appareil StorSimple. A **connecter tooTarget** boîte de dialogue s’affiche.
7. Bonjour **connecter tooTarget** boîte de dialogue, sélectionnez hello **Enable multi-path** case à cocher. Cliquez sur **Avancé**.
8. Bonjour **paramètres avancés** boîte de dialogue, exécutez hello comme suit :
   
   1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez **initiateur Microsoft iSCSI**.
   2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello adresseIP de hôte de hello.
   3. Sur hello **portail cible** la liste déroulante IP, IP hello select de l’interface de l’appareil.
   4. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue.
9. Cliquez sur **Propriétés**. Bonjour **propriétés** boîte de dialogue, cliquez sur **Ajout d’une Session**.
10. Bonjour **connecter tooTarget** boîte de dialogue, sélectionnez hello **Enable multi-path** case à cocher. Cliquez sur **Avancé**.
11. Bonjour **paramètres avancés** boîte de dialogue :

    1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez Microsoft iSCSI Initiator.
    2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello IP adresse correspondant toohello hôte. Dans ce cas, vous vous connectez deux interfaces réseau sur hello appareil tooa seule interface réseau sur l’ordinateur hôte de hello. Par conséquent, cette interface est hello identique à celui fourni pour hello première session.
    3. Sur hello **IP du portail cible** liste déroulante, sélectionnez hello adresseIP pour seconde interface de données hello activé sur le périphérique de hello.
    4. Cliquez sur **OK** boîte de dialogue Propriétés de l’initiateur tooreturn toohello iSCSI. Vous avez ajouté une deuxième cible toohello de session.
12. Ouvrez **gestion de l’ordinateur** en naviguant trop**le Gestionnaire de serveur > tableau de bord > Gestion de l’ordinateur**. Dans le volet gauche de hello, cliquez sur **stockage > Gestion des disques**. volume de Hello créé sur l’appareil StorSimple hello qui sont visibles toothis hôte apparaît sous **gestion des disques** en tant que nouveaux disques.
13. Hello du disque et créez un volume. Au cours du processus de formatage hello, sélectionnez une taille de bloc de 64 Ko.
    
    ![Gestion des disques](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. Sous **gestion des disques**, avec le bouton hello **disque** et sélectionnez **propriétés**.
15. Bonjour modèle StorSimple ### **propriétés Multi-Path** boîte de dialogue, cliquez sur hello **MPIO** onglet.
    
    ![DeviceProp disque à chemins d’accès multiples StorSimple 8100.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. Bonjour **nom DSM** , cliquez sur **détails** et vérifiez que les paramètres de hello sont définies toohello les paramètres par défaut. les paramètres par défaut Hello sont :
    
    * Période de vérification du chemin d’accès = 30
    * Nombre de tentatives = 3
    * Période de suppression d’objets de périphériques physiques = 20
    * Intervalle avant nouvelle tentative = 1
    * Vérification du chemin activée = désactivé.

> [!NOTE]
> **Ne modifiez pas les paramètres par défaut de hello.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Étape 4 : configurer MPIO pour la haute disponibilité et l’équilibrage de charge

Pour les chemins d’accès multiples en fonction haute disponibilité et l’équilibrage de charge, plusieurs sessions doivent être ajoutées manuellement toodeclare hello différents chemins d’accès disponibles. Par exemple, si l’hôte de hello possède deux interfaces connectées tooSAN et hello périphérique possède deux tooSAN connecté interfaces, vous avez besoin de quatre sessions configurées avec des permutations de chemin d’accès appropriées (seules deux sessions seront nécessaires si chaque interface DATA et l’interface de l’hôte est sur un sous-réseau IP différent et n’est pas routable).

**Nous vous recommandons d’avoir au moins 8 sessions parallèles actives entre les appareils hello et votre application hôte.** Cela est possible en activant 4 interfaces réseau sur votre système Windows Server. Utiliser les interfaces réseau physiques ou virtuels interfaces via les technologies de virtualisation de réseau sur le niveau de système d’exploitation ou matériel hello sur votre hôte Windows Server. Avec hello deux interfaces réseau sur l’appareil de hello, cette configuration entraînerait 8 sessions actives. Cette configuration permet d’optimiser le débit d’appareil et cloud hello.

> [!IMPORTANT]
> **Nous vous recommandons de ne pas mélanger les interfaces réseau 1 Gigabit Ethernet et 10 Gigabit Ethernet. Si vous utilisez deux interfaces réseau, les deux interfaces doivent être hello même type.**

Hello procédure suivante décrit comment hébergent des sessions tooadd quand un appareil StorSimple avec deux interfaces réseau est connecté tooa avec deux interfaces réseau. Cela vous donne seulement 4 sessions. Utilisez la même procédure avec un appareil StorSimple avec l’hôte de tooa connecté réseau deux interfaces avec quatre interfaces réseau. Vous devez tooconfigure 8 au lieu de hello 4 sessions décrites ici.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure MPIO pour la haute disponibilité et l’équilibrage de charge

1. Effectuer une découverte de cible de hello : Bonjour **propriétés de l’initiateur iSCSI** la boîte de dialogue hello **découverte** , cliquez sur **découvrir un portail**.
2. Bonjour **connecter tooTarget** boîte de dialogue, entrez l’adresse IP de hello de l’une des interfaces réseau hello.
3. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue.
4. Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue, sélectionnez hello **cibles** onglet, mettez en surbrillance la cible de hello détecté, puis cliquez sur **connexion**. Hello **connecter tooTarget** boîte de dialogue s’affiche.
5. Bonjour **connecter tooTarget** boîte de dialogue :
   
   1. Par défaut de congé hello cible sélectionnée pour **ajouter cette connexion** toohello la liste des cibles favorites. Cela rend les appareil hello tente automatiquement de connexion de hello toorestart chaque redémarrage de cet ordinateur.
   2. Sélectionnez hello **Enable multi-path** case à cocher.
   3. Cliquez sur **Avancé**.
6. Bonjour **paramètres avancés** boîte de dialogue :
   
   1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez **initiateur Microsoft iSCSI**.
   2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello adresseIP de hôte de hello.
   3. Sur hello **IP du portail cible** liste déroulante, adresse IP de hello sélectionnez hello d’interface de données activée sur l’appareil de hello.
   4. Cliquez sur **OK** boîte de dialogue Propriétés de l’initiateur tooreturn toohello iSCSI.
7. Cliquez sur **propriétés**et Bonjour **propriétés** boîte de dialogue, cliquez sur **Ajout d’une Session**.
8. Bonjour **connecter tooTarget** boîte de dialogue, sélectionnez hello **Enable multi-path** case à cocher, puis cliquez sur **avancé**.
9. Bonjour **paramètres avancés** boîte de dialogue :
   
   1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez **initiateur Microsoft iSCSI**.
   2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello adresse IP correspondante toohello seconde interface sur l’ordinateur hôte de hello.
   3. Sur hello **IP du portail cible** liste déroulante, sélectionnez hello adresseIP pour seconde interface de données hello activé sur le périphérique de hello.
   4. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue. Vous avez maintenant ajouté une deuxième cible toohello de session.
10. Répétez la cible de toohello étapes 8 à 10 tooadd supplémentaires sessions (chemins d’accès). Avec deux interfaces sur l’ordinateur hôte de hello et deux sur le périphérique de hello, vous pouvez ajouter un total de quatre sessions.
11. Après avoir ajouté hello souhaité sessions (chemins d’accès), Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue, cible de hello sélectionnez et cliquez sur **propriétés**. Sur l’onglet Sessions de hello Hello **propriétés** boîte de dialogue, notez hello quatre identificateurs de session qui correspondent les permutations de chemin d’accès possibles toohello. toocancel une session, sélectionnez l’identificateur de session hello case à cocher suivante tooa, puis cliquez sur **déconnexion**.
12. appareils tooview présentés dans les sessions, sélectionnez hello **périphériques** hello de tooconfigure onglet stratégie MPIO sur un périphérique sélectionné, cliquez sur **MPIO**. Hello **détails de l’appareil** boîte de dialogue s’affiche. Sur hello **MPIO** onglet, vous pouvez sélectionner hello approprié **stratégie d’équilibrage de charge** paramètres. Vous pouvez également afficher hello **Active** ou **Standby** type de chemin d’accès.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur [à l’aide de hello toomodify du service Gestionnaire de périphériques StorSimple votre configuration de l’appareil StorSimple](storsimple-8000-modify-device-config.md).

