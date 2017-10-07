---
title: "Gestionnaire d’instantanés StorSimple avec les appareils aaaManage | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Snapshot Manager MMC enfichable tooconnect et gérer les appareils StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Utilisez le Gestionnaire d’instantanés StorSimple tooconnect et gérer les appareils StorSimple
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser des nœuds Bonjour Gestionnaire d’instantanés StorSimple **étendue** volet tooverify importé des données de l’appareil StorSimple et actualiser les périphériques de stockage connectés. En outre, lorsque vous cliquez sur hello **périphériques** nœud, vous pouvez afficher la liste des périphériques connectés et les informations d’état correspondantes dans hello **résultats** volet.

![Appareils connectés](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Figure 1 : Appareil connecté du Gestionnaire d’instantanés StorSimple** 

Selon votre **vue** sélections, hello **résultats** volet affiche hello suivant des informations sur chaque appareil. (Pour plus d’informations sur la configuration d’une vue, consultez trop[menu Affichage](storsimple-use-snapshot-manager.md#view-menu).

| Colonne de résultats | Description |
|:--- |:--- |
| Nom |nom Hello du périphérique hello tel que configuré dans hello portail Azure classic |
| Modèle |numéro de modèle Hello du périphérique de hello |
| Version |Hello version de hello logiciel installé sur l’appareil de hello |
| État |Si l’appareil de hello est disponible |
| Dernière synchronisation |Date et heure lors de la dernière synchronisation de hello du périphérique |
| Numéro de série |numéro de série Hello pour appareil de hello |

Si vous cliquez sur hello **périphériques** nœud Bonjour **étendue** , vous pouvez sélectionner à partir de hello suivant des actions :

* Ajout ou remplacement d’un appareil
* Connexion d’un appareil et vérification des importations
* Actualisation des appareils connectés

Si vous cliquez sur hello **périphériques** nom de nœud et avec le bouton droit puis un appareil Bonjour **résultats** , vous pouvez sélectionner à partir de hello suivant des actions :

* Authentification d’un appareil
* Affichage des détails sur l’appareil
* Actualisation d’un appareil
* Suppression de la configuration d’un appareil
* Modification du mot de passe d’un appareil

> [!NOTE]
> Toutes ces actions sont également disponibles dans hello **Actions** volet.


Ce didacticiel explique comment toouse tooconnect de gestionnaire d’instantanés StorSimple et gérer des appareils et d’effectuer hello tâches suivantes :

* Ajout ou remplacement d’un appareil
* Connexion d’un appareil et vérification des importations
* Actualisation des appareils connectés
* Authentification d’un appareil
* Affichage des détails sur l’appareil
* Actualisation d’un appareil
* Suppression de la configuration d’un appareil
* Modification d’un mot de passe expiré d’appareil
* Remplacement d’un appareil défaillant

> [!NOTE]
> Pour obtenir des informations générales sur l’utilisation d’interface de gestionnaire d’instantanés StorSimple hello, accédez trop[interface utilisateur de gestionnaire d’instantanés StorSimple](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Ajout ou remplacement d’un appareil
Utilisez hello suivant la procédure tooadd ou remplacer un appareil StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd ou remplacer un appareil
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, avec le bouton hello **périphériques** nœud, puis cliquez sur **configurer un appareil**. Hello **configurer un appareil** boîte de dialogue s’affiche.
   
    ![Configurer un appareil StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. Bonjour **périphérique** zone de liste déroulante, sélectionnez hello adresseIP de périphérique de hello ou un périphérique virtuel. 
4. Bonjour **mot de passe** zone de texte, de type hello Gestionnaire d’instantanés StorSimple un mot de passe que vous avez créé pour appareil de hello en hello portail Azure classic. Cliquez sur **OK**. Gestionnaire d’instantanés StorSimple recherche le périphérique hello que vous avez identifié. 
   
   * Si l’appareil de hello est disponible, le Gestionnaire d’instantanés StorSimple ajoute une connexion.
   * Si l’appareil de hello est indisponible pour une raison quelconque, le Gestionnaire d’instantanés StorSimple retourne un message d’erreur. Cliquez sur **OK** tooclose hello du message d’erreur, puis cliquez sur **Annuler** tooclose hello **configurer un appareil** boîte de dialogue.

## <a name="connect-a-device-and-verify-imports"></a>Connexion d’un appareil et vérification des importations
Utilisez hello suivant la procédure tooconnect un appareil StorSimple et vérifiez que les groupes de volumes existants qui sont associés à des sauvegardes sont importés.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect un appareil et vérifier les importations
1. tooconnect un tooStorSimple appareil Gestionnaire d’instantanés, suivez les instructions de hello dans Ajouter ou remplacer un appareil. Lorsqu’il connecte tooa périphérique, le Gestionnaire d’instantanés StorSimple répond comme suit :
   
   * Si l’appareil de hello est indisponible pour une raison quelconque, le Gestionnaire d’instantanés StorSimple retourne un message d’erreur. 
   
   * Si l’appareil de hello est disponible, le Gestionnaire d’instantanés StorSimple ajoute une connexion. Lorsque vous sélectionnez le périphérique de hello, il apparaît dans hello **résultats** volet, et le champ d’état hello indique que ce périphérique hello **disponible**. Gestionnaire d’instantanés StorSimple importe tous les groupes de volumes configurés pour appareil de hello, sous réserve que les sauvegardes soient associées aux groupes de volumes hello. Les stratégies de sauvegarde ne sont pas importées. Les groupes de volumes qui ne sont associés à aucune sauvegarde ne sont pas importés.
2. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
3. Nœud supérieur de clic droit hello Bonjour **étendue** volet, puis cliquez sur **activer/désactiver l’affichage des importations**.
   
    ![Sélectionner Basculer l’affichage des importations](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Hello **activer/désactiver l’affichage des importations** boîte de dialogue s’affiche, indiquant hello état hello importé les groupes de volumes et les sauvegardes. Cliquez sur **OK**.

Une fois les sauvegardes et les groupes de volumes hello importation réussie, vous pouvez utiliser Gestionnaire d’instantanés StorSimple toomanage leur, exactement comme vous le feriez groupes de volumes et sauvegardes que vous avez créé et configuré avec Gestionnaire d’instantanés StorSimple. 

## <a name="refresh-connected-devices"></a>Actualisation des appareils connectés
Utilisez hello suivant la procédure toosynchronize hello connecté StorSimple appareils auprès de StorSimple Snapshot Manager.

#### <a name="toorefresh-connected-devices"></a>toorefresh les périphériques connectés
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, avec le bouton droit **périphériques**, puis cliquez sur **actualiser les périphériques**. Cette opération synchronise hello connecté appareils auprès de StorSimple Snapshot Manager afin que vous pouvez afficher les groupes de volumes hello et des sauvegardes, y compris les ajouts les plus récents. 
   
    ![Actualiser les appareils StorSimple hello](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Hello **actualiser les périphériques** action récupère les nouveaux groupes de volumes et les sauvegardes associées depuis les périphériques connectés. Contrairement aux hello **rescanner les volumes** action disponible pour hello **Volumes** nœud, **actualiser les périphériques** ne pas restaurer le Registre de sauvegarde hello.

## <a name="authenticate-a-device"></a>Authentification d’un appareil
Utilisez hello suivant la procédure tooauthenticate un appareil StorSimple auprès de StorSimple Snapshot Manager.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate un appareil
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur **périphériques**.
3. Bonjour **résultats** volet, cliquez sur le nom hello du périphérique de hello, puis cliquez sur **authentifier**.
4. Hello **authentifier** boîte de dialogue s’affiche. Tapez le mot de passe de périphérique hello, puis cliquez sur **OK**.
   
    ![Boîte de dialogue Authentifier](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Affichage des détails sur l’appareil
Utilisez hello suivant la procédure tooview hello plus d’informations d’un appareil StorSimple et, si nécessaire, resynchroniser l’appareil hello avec Gestionnaire d’instantanés StorSimple.

#### <a name="tooview-and-resynchronize-device-details"></a>Détails de l’appareil tooview et se resynchronisent
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur **périphériques**.
3. Bonjour **résultats** volet, cliquez sur le nom hello du périphérique de hello, puis cliquez sur **détails**.

4 hello **détails de l’appareil** boîte de dialogue s’affiche. Cette zone affiche le nom de hello, modèle, version, numéro de série, état, cible iSCSI nom qualifié (IQN) et dernière synchronisation date et l’heure.

* Cliquez sur **Resync** appareil de hello toosynchronize.
* Cliquez sur **OK** ou **Annuler** boîte de dialogue tooclose hello.
  
  ![Informations sur l’appareil](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Actualisation d’un appareil
Utilisez hello suivant la procédure tooresynchronize un appareil StorSimple individuel avec Gestionnaire d’instantanés StorSimple.

#### <a name="toorefresh-a-device"></a>toorefresh un appareil
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple. 
2. Bonjour **étendue** volet, cliquez sur **périphériques**. 
3. Bonjour **résultats** volet, cliquez sur le nom hello du périphérique de hello, puis cliquez sur **actualiser l’appareil**. Appareil de hello se synchronise avec Gestionnaire d’instantanés StorSimple.

## <a name="delete-a-device-configuration"></a>Suppression de la configuration d’un appareil
Utilisez hello suivant procédure toodelete une configuration de l’appareil StorSimple individuelle à partir de gestionnaire d’instantanés StorSimple.

#### <a name="toodelete-a-device-configuration"></a>toodelete une configuration d’appareil
1. Cliquez sur icône du bureau de hello toostart Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur **périphériques**. 
3. Bonjour **résultats** volet, cliquez sur le nom hello du périphérique de hello, puis cliquez sur **supprimer**. 
4. Hello message suivant s’affiche. Cliquez sur **Oui** toodelete hello configuration ou cliquez sur **non** toocancel la suppression hello.
   
    ![Supprimer la configuration de l’appareil](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Modification d’un mot de passe expiré d’appareil
Vous devez entrer un mot de passe de tooauthenticate un appareil StorSimple auprès de StorSimple Snapshot Manager. Vous configurez ce mot de passe lorsque vous utilisez hello Windows PowerShell interface tooset périphérique de hello. Toutefois, le mot de passe hello peut expirer. Dans ce cas, vous pouvez utiliser le mot de passe hello toochange de portail classique Azure hello. Puis, car l’appareil de hello a été configuré dans Gestionnaire d’instantanés StorSimple avant l’expiration du mot de passe hello, vous devez authentifier de nouveau l’appareil hello dans Gestionnaire d’instantanés StorSimple.

#### <a name="toochange-hello-expired-password"></a>mot de passe expiré toochange hello
1. Bonjour portail Azure classic, démarrez le service StorSimple Manager hello.
2. Cliquez sur **périphériques** > **configurer** pour appareil de hello.
3. Faites défiler toohello section du Gestionnaire d’instantanés StorSimple. Entrez un mot de passe comportant entre 14 et 15 caractères. Assurez-vous que ce mot de passe hello contient une combinaison de caractères en majuscules, minuscules, numériques et spéciaux.
4. Entrez de nouveau tooconfirm de mot de passe hello il.
5. Cliquez sur **enregistrer** bas hello de page de hello.

#### <a name="toore-authenticate-hello-device"></a>toore-authentifier hello périphérique
1. Démarrez le Gestionnaire d’instantanés StorSimple.
2. Bonjour **étendue** volet, cliquez sur **périphériques**. Une liste des périphériques configurés apparaît dans hello **résultats** volet.
3. Sélectionnez le périphérique de hello, avec le bouton droit, puis cliquez sur **authentifier**.
4. Bonjour **authentifier** fenêtre, entrez le nouveau mot de passe hello.
5. Sélectionnez le périphérique de hello, avec le bouton droit et sélectionnez **actualisation périphérique**. Appareil de hello se synchronise avec Gestionnaire d’instantanés StorSimple.

## <a name="replace-a-failed-device"></a>Remplacement d’un appareil défaillant
Si un appareil StorSimple échoue et est remplacé par un périphérique de secours (basculement), hello utilisation suivant les étapes tooconnect le mode et toohello nouveau périphérique hello sauvegardes associées.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa nouveau périphérique après basculement
1. Reconfigurer hello iSCSI connexion toohello le nouveau périphérique. Pour obtenir des instructions, consultez trop « étape 7 : monter, initialiser et formatez un volume » dans [déployer l’appareil StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Si l’appareil StorSimple nouveau hello a hello même adresse IP que hello ancien, vous pouvez être ancienne configuration de tooconnect en mesure de hello.


1. Arrêter hello Service de gestion StorSimple de Microsoft :
   
   1. Démarrez le Gestionnaire de serveur.
   2. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   3. Sur hello **Services** fenêtre, sélectionnez hello **Microsoft StorSimple Management Service**.
   4. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **arrêter le service de hello**.
2. Supprimer l’ancien périphérique hello configuration informations toohello connexes :
   
   1. Dans l’Explorateur de fichiers, accédez à tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Supprimez les fichiers hello dans le dossier BACatalog de hello.
3. Redémarrez hello Service de gestion StorSimple de Microsoft :
   
   1. Sur hello du tableau de bord Gestionnaire de serveur, sur hello **outils** menu, sélectionnez **Services**.
   2. Sur hello **Services** fenêtre, sélectionnez hello **Microsoft StorSimple Management Service**.
   3. Bonjour avec le bouton droit volet, sous **Microsoft StorSimple Management Service**, cliquez sur **redémarrer hello service**.
4. Démarrez le Gestionnaire d’instantanés StorSimple.
5. tooconfigure hello nouveau StorSimple périphérique hello terminé les étapes à l’étape 2 : connecter un appareil StorSimple dans [déployer le Gestionnaire d’instantanés StorSimple](storsimple-snapshot-manager-deployment.md).
6. Nœud de niveau supérieur avec le bouton hello Bonjour **étendue** volet (Gestionnaire d’instantanés StorSimple dans l’exemple de hello), puis cliquez sur **activer/désactiver l’affichage des importations**. 
7. Un message s’affiche lorsque hello importé des groupes de volumes et sauvegardes sont visibles dans Gestionnaire d’instantanés StorSimple. Cliquez sur **OK**.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser le Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* Découvrez comment trop[tooview de gestionnaire d’instantanés StorSimple et gérer les volumes](storsimple-snapshot-manager-manage-volumes.md).

