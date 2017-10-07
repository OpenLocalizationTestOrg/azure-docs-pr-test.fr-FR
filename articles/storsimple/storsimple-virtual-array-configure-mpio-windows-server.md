---
title: "aaaConfigure MPIO sur l’ordinateur hôte connecté tooStorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment tooconfigure MPIO d’e/s (o) pour votre StorSimple Virtual Array connectées hôte tooa exécutant Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Configurer MPIO sur un hôte Windows Server pour hello StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment appliquer les paramètres de configuration spécifiques pour les volumes StorSimple uniquement tooinstall, fonctionnalité Multipath i/o (MPIO) sur votre hôte Windows Server et puis vérifiez MPIO pour des volumes StorSimple. procédure de Hello suppose que votre tableau virtuel StorSimple 1200 avec deux interfaces réseau hôte de Windows Server connectés tooa avec deux interfaces réseau. les informations de Hello contenues dans cet article s’appliquent uniquement toohello de tableau virtuel. Pour plus d’informations sur les périphériques série StorSimple 8000, accédez trop[configuration de MPIO pour StorSimple hôte](storsimple-configure-mpio-windows-server.md). 

fonctionnalité MPIO de Hello dans les configurations de stockage hautement disponible et à tolérance de pannes de Windows Server vous aide à build. MPIO utilise les composants de chemin d’accès physique redondants, cartes, des câbles et commutateurs : toocreate les chemins d’accès logiques entre le serveur de hello et de périphérique de stockage hello. S’il existe une défaillance d’un composant, à l’origine d’un chemin d’accès logique toofail, logique multivoie utilise un autre chemin d’e/s afin que les applications peuvent toujours accéder à leurs données. En outre selon votre configuration, MPIO peut également améliorer les performances par l’équilibrage de charge hello entre ces chemins d’accès. Pour plus d’informations, consultez la [Présentation de MPIO](https://technet.microsoft.com/library/cc725907.aspx "Présentation de MPIO and features").

Pour hello haute disponibilité de votre solution StorSimple, configurer MPIO sur hello Windows Server hôtes tooyour connecté StorSimple Virtual Array (modèle 1200). les serveurs hôtes Hello peuvent ensuite tolérer un lien, un réseau ou une défaillance de l’interface. 

Vous devez toofollow ces tooconfigure étapes MPIO : 

* Conditions préalables à la configuration
* Étape 1 : Installer MPIO sur un hôte Windows hello
* Étape 2 : configurer MPIO pour les volumes StorSimple
* Étape 3 : Monter des volumes StorSimple sur l’ordinateur hôte de hello

Hello étapes ci-dessus sont toutes décrites dans les sections suivantes de hello.

## <a name="prerequisites"></a>Composants requis
Cette section détaille hello configuration requise pour l’hôte du serveur de Windows hello et votre tableau virtuel.

### <a name="on-windows-server-host"></a>Sur l’hôte Windows Server
* Assurez-vous que votre hôte Windows Server possède 2 interfaces réseau activées.

### <a name="on-storsimple-virtual-array"></a>Sur le tableau virtuel StorSimple
* unité de stockage virtuelle Hello doit être configurée comme un serveur iSCSI. toolearn, voir [tableau virtuel en tant que serveur iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Une ou plusieurs interfaces réseau doivent être activés sur le tableau de hello.   
* interfaces réseau de Hello sur votre tableau virtuel doivent être accessibles à partir de l’hôte du serveur de Windows hello.
* Un ou plusieurs volumes doivent être créés sur votre baie virtuelle StorSimple. toolearn, voir [ajouter un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) sur votre tableau virtuel StorSimple. Dans cette procédure, nous avons créé des 3 volumes (1 localement épinglés et 2 volumes hiérarchisés comme indiqué ci-dessous) sur l’unité de stockage virtuelle hello.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Configuration matérielle pour le tableau virtuel StorSimple
figure Hello ci-dessous montre la configuration matérielle de hello pour la haute disponibilité et l’équilibrage de charge de gestion multivoie pour votre hôte Windows Server et le StorSimple Virtual Array est utilisé dans cette procédure.

![configuration matérielle mpio](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Comme indiqué dans hello précédant figure :

* Votre tableau virtuel StorSimple approvisionné sur Hyper-V est un appareil actif à nœud unique configuré comme un serveur iSCSI.
* Deux interfaces de réseau virtuel sont activées sur votre baie. Dans hello local interface utilisateur web de votre tableau virtuel, vérifiez que les deux interfaces réseau sont activés en naviguant trop**paramètres réseau** comme indiqué ci-dessous :
  
    ![Interfaces réseau activées sur 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Notez les adresses de hello IPv4 Hello activé (Ethernet, Ethernet 2 par défaut) d’interfaces réseau et enregistrement pour une utilisation ultérieure sur l’ordinateur hôte de hello.
* Deux interfaces réseau sont activées sur votre hôte Windows Server. Si hello connecté des interfaces pour l’hôte et le tableau se trouvent sur hello même sous-réseau, les chemins de 4 accès sera alors disponible. C’était le cas de hello dans cette procédure. Toutefois, si chaque interface réseau sur l’interface de tableau et l’hôte hello est sur un sous-réseau IP différent (et non routables), puis les chemins d’accès seulement 2 sera disponibles.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Étape 1 : Installer MPIO sur un hôte Windows hello
MPIO est une fonctionnalité facultative sur Windows Server et n’est pas installé par défaut. Il doit être installé en tant que fonctionnalité via le Gestionnaire de serveur. fin de cette fonctionnalité sur votre hôte Windows Server, tooinstall hello suivant la procédure.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Étape 2 : configurer MPIO pour les volumes StorSimple
MPIO doit les volumes StorSimple tooidentify toobe configuré. volumes de StorSimple toorecognize tooconfigure MPIO, effectuer hello comme suit.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Étape 3 : Monter des volumes StorSimple sur l’ordinateur hôte de hello
Une fois MPIO est configuré sur Windows Server, ou les volumes créés sur le tableau de StorSimple hello peuvent être montés et peuvent effectuer tirer parti de MPIO pour assurer la redondance. toomount un volume, exécutez hello comme suit.

#### <a name="toomount-volumes-on-hello-host"></a>volumes toomount sur l’ordinateur hôte de hello
1. Ouvrez hello **propriétés de l’initiateur iSCSI** fenêtre sur l’hôte du serveur de Windows hello. Accédez trop**le Gestionnaire de serveur > tableau de bord > Outils > initiateur iSCSI**.
2. Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue, cliquez sur **découverte**, puis cliquez sur **détecter un portail cible**.
3. Bonjour **détecter un portail cible** boîte de dialogue zone, hello suivant :
   
    1. Entrez l’adresse hello d’interface réseau activée de la première hello sur votre tableau virtuel StorSimple. Par défaut, il s’agit d’ **Ethernet**. 
    2. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue.
     
    > [!IMPORTANT]
    > Si vous utilisez un réseau privé pour les connexions iSCSI, entrez hello adresseIP du port de données hello qui est le réseau privé de toohello connecté.
     
4. Répétez les étapes 2 et 3 pour une deuxième interface réseau (par exemple, Ethernet 2) sur votre baie. 
5. Sélectionnez hello **cibles** onglet Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue. Pour votre baie virtuelle, vous devez voir la surface de chaque volume en tant que cible sous **Cibles découvertes**. Dans ce cas, trois cibles (volumes toothree correspondants) seraient découvertes.
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Cliquez sur **Connect** tooestablish une session iSCSI avec votre StorSimple Virtual Array. A **connecter tooTarget** boîte de dialogue s’affiche. Sélectionnez hello **Enable multi-path** case à cocher. Cliquez sur **Avancé**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. Bonjour **paramètres avancés** boîte de dialogue zone, hello suivant :                                        
   
    1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez **initiateur Microsoft iSCSI**.
    2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello adresseIP de hôte de hello.
    3. Sur hello **portail cible** la liste déroulante IP, IP hello select de l’interface du tableau.
    4. Cliquez sur **OK** tooreturn toohello **propriétés de l’initiateur iSCSI** boîte de dialogue.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Cliquez sur **Propriétés**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. Bonjour **propriétés** boîte de dialogue, cliquez sur **Ajout d’une Session**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. Bonjour **connecter tooTarget** boîte de dialogue, sélectionnez hello **Enable multi-path** case à cocher. Cliquez sur **Avancé**.
11. Bonjour **paramètres avancés** boîte de dialogue :                                        
    
    1. Sur hello **adaptateur Local** la liste déroulante, sélectionnez Microsoft iSCSI Initiator.

    2. Sur hello **IP de l’initiateur** liste déroulante, sélectionnez hello IP adresse correspondant toohello hôte. Dans ce cas, vous vous connectez deux interfaces réseau sur hello tableau tooa seule interface réseau sur l’ordinateur hôte de hello. Par conséquent, cette interface est hello identique à celui fourni pour hello première session.

    3. Sur hello **IP du portail cible** liste déroulante, sélectionnez hello adresseIP pour seconde interface de données hello activé sur le tableau de hello.

    4. Cliquez sur **OK** boîte de dialogue Propriétés de l’initiateur tooreturn toohello iSCSI. Vous avez ajouté une deuxième cible toohello de session.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Après avoir ajouté hello souhaité sessions (chemins d’accès), Bonjour **propriétés de l’initiateur iSCSI** boîte de dialogue, cible de hello sélectionnez et cliquez sur **propriétés**. Sur l’onglet Sessions de hello Hello **propriétés** boîte de dialogue, notez hello quatre identificateurs de session qui correspondent les permutations de chemin d’accès possibles toohello. toocancel une session, sélectionnez l’identificateur de session hello case à cocher suivante tooa, puis cliquez sur **déconnexion**.

    6. appareils tooview présentés dans les sessions, sélectionnez hello **périphériques** hello de tooconfigure onglet stratégie MPIO sur un périphérique sélectionné, cliquez sur **MPIO**.

    7. Hello **détails** boîte de dialogue s’affiche. Sur hello **MPIO** onglet, vous pouvez sélectionner hello approprié **stratégie d’équilibrage de charge** paramètres. Vous pouvez également afficher hello **Active** ou **Standby** type de chemin d’accès.
12. Répétez la cible de toohello étapes 8 à 11 tooadd supplémentaires sessions (chemins d’accès). Avec deux interfaces sur l’ordinateur hôte de hello et deux sur l’unité de stockage virtuelle hello, vous pouvez ajouter un total de quatre sessions pour chaque cible. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Vous devez toorepeat ces étapes pour chaque volume (surfaces en tant que cible).
    
    ![mpio15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Ouvrez **gestion de l’ordinateur** en naviguant trop**le Gestionnaire de serveur > tableau de bord > Gestion de l’ordinateur**. Dans le volet gauche de hello, cliquez sur **stockage > Gestion des disques**. Hello ou les volumes créés sur hello StorSimple Virtual Array qui sont visibles toothis hôte apparaissent sous **gestion des disques** en tant que nouveaux disques.
15. Hello du disque et créez un volume. Au cours du processus de formatage hello, sélectionnez une taille d’unité d’allocation (AUS) de 64 Ko. Répétez le processus de hello pour tous les volumes disponibles hello.
    
    ![Gestion des disques](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. Sous **gestion des disques**, avec le bouton hello **disque** et sélectionnez **propriétés**.
17. Bonjour **propriétés Multi-Path** boîte de dialogue, cliquez sur hello **MPIO** onglet.
    
    ![Propriétés du disque](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. Bonjour **nom DSM** , cliquez sur **détails** et vérifiez que les paramètres de hello sont définies toohello les paramètres par défaut. les paramètres par défaut Hello sont :
    
    * Période de vérification du chemin d’accès = 30
    * Nombre de tentatives = 3
    * Période de suppression d’objets de périphériques physiques = 20
    * Intervalle avant nouvelle tentative = 1
    * Vérification du chemin activée = désactivé.
    
    > [!NOTE]
    > **Ne modifiez pas les paramètres par défaut de hello.**
   
## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [à l’aide de hello tooadminister du service Gestionnaire de périphériques StorSimple votre StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).

