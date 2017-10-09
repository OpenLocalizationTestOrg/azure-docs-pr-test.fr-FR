---
title: "programme d’installation du serveur iSCSI Azure StorSimple Virtual Array aaaMicrosoft | Documents Microsoft"
description: "Décrit comment inscrire votre serveur d’iSCSI StorSimple tooperform le programme d’installation initiale et terminer l’installation de l’appareil."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Déploiement de StorSimple Virtual Array - Configuration d’un serveur iSCSI via le portail Azure

![flux du processus d'installation iscsi](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel de déploiement s’applique toohello Microsoft Azure StorSimple Virtual Array. Ce didacticiel explique comment tooperform hello initiale le programme d’installation, inscrire votre serveur iSCSI StorSimple, le programme d’installation complète hello appareil, puis créer, monter, initialiser et formater des volumes sur votre tableau virtuel StorSimple configuré comme un serveur iSCSI. 

Décrit des procédures Hello prennent ici environ 30 minutes toocomplete de heure de too1. les informations de Hello publiées dans cet article s’appliquent tooStorSimple tableaux virtuels uniquement.

## <a name="setup-prerequisites"></a>Configuration requise

Avant de configurer votre solution StorSimple Virtual Array, assurez-vous que :

* Vous avez configuré un tableau virtuel et connectés tooit comme décrit dans [déployer StorSimple Virtual Array - configurer un tableau virtuel dans Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) ou [déployer StorSimple Virtual Array - configurer un tableau virtuel dans les environnements VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Vous avez la clé d’inscription hello de hello service Gestionnaire de périphériques StorSimple que vous avez créé toomanage vos réseaux virtuels StorSimple. Pour plus d’informations, consultez **étape 2 : clé d’inscription Get hello** dans [déployer StorSimple Virtual Array - préparer le portail de hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* S’il s’agit de hello deuxième ou ultérieures tableau virtuel que vous inscrivez avec un service de gestionnaire de périphériques StorSimple existant, vous devez disposer de clé de chiffrement de données de service hello. Cette clé a été générée lorsque le premier périphérique de hello a été correctement inscrit auprès de ce service. Si vous avez perdu cette clé, consultez **Get hello clé de chiffrement** dans [utilisez hello tooadminister de l’interface utilisateur Web de votre tableau virtuel StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Configuration étape par étape

Utiliser hello suivre des instructions détaillées tooset et configurer votre tableau virtuel StorSimple :

* [Étape 1 : Terminer web locale de hello le programme d’installation de l’interface utilisateur et inscrire votre appareil](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Étape 2 : Hello complète requise le programme d’installation de périphérique](#step-2-complete-the-required-device-setup)
* [Étape 3 : Ajout d’un volume](#step-3-add-a-volume)
* [Étape 4 : Montage, initialisation et formatage d’un volume](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Étape 1 : Terminer web locale de hello le programme d’installation de l’interface utilisateur et inscrire votre appareil

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello le programme d’installation et inscrire un appareil hello

1. Ouvrez une fenêtre de navigateur. tooconnect le type d’interface utilisateur web toohello :
   
    `https://<ip-address of network interface>`
   
    Utilisez les URL de connexion hello indiqué à l’étape précédente de hello. Vous verrez un message d’erreur signalant qu’il existe un problème avec le certificat de sécurité du site Web de hello. Cliquez sur **continuer toothis web page**.
   
    ![erreur de certificat de sécurité](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Connexion toohello web de l’interface utilisateur de votre appareil virtuel en tant que **StorSimpleAdmin**. Entrez le mot de passe administrateur de périphérique hello que vous avez modifié à l’étape 3 : démarrer un appareil virtuel hello dans [déployer StorSimple Virtual Array - configurer un appareil virtuel dans Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [déployer StorSimple Virtual Array - Configurer un périphérique virtuel dans VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![page de connexion](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Vous serez dirigé toohello **accueil** page. Cette page décrit hello divers paramètres requis tooconfigure et inscrire hello périphérique virtuel avec le service du Gestionnaire de périphériques StorSimple hello. Notez que hello **paramètres réseau**, **les paramètres de proxy Web**, et **paramètres** sont facultatifs. Hello uniquement les paramètres requis sont **paramètres de périphérique** et **paramètres de Cloud**.
   
    ![page d'accueil](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. Sur hello **paramètres réseau** page sous **interfaces réseau**, DATA 0 sera automatiquement configuré pour vous. Chaque interface réseau a la valeur par défaut tooget une adresse IP automatiquement (DHCP). Par conséquent, une adresse IP, un sous-réseau et une passerelle seront automatiquement attribués (pour IPv4 et IPv6).
   
    Lorsque vous planifiez toodeploy votre appareil en tant que serveur iSCSI (stockage de bloc tooprovision), nous vous conseillons de désactiver hello **obtenir adresse IP automatiquement** option et configurer des adresses IP statiques.
   
    ![page des paramètres réseau](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Si vous avez ajouté plusieurs interfaces réseau lors de la configuration de hello du périphérique de hello, vous pouvez les configurer ici. Notez que vous pouvez configurer votre interface réseau en IPv4 uniquement ou en IPv4 et IPv6. Les configurations en IPv6 uniquement ne sont pas prises en charge.
5. Serveurs DNS sont requis car elles sont utilisées lorsque votre appareil tente toocommunicate avec des fournisseurs de services de stockage cloud tooresolve votre périphérique par nom si elle est configurée comme un serveur de fichiers. Sur hello **paramètres réseau** page sous hello **serveurs DNS**:
   
   1. Un serveur DNS principal et un serveur secondaire seront définis automatiquement. Si vous choisissez tooconfigure des adresses IP statiques, vous pouvez spécifier des serveurs DNS. Pour une haute disponibilité, nous vous recommandons de configurer un serveur DNS principal et un serveur secondaire.
   2. Cliquez sur **Apply**. Cela s’applique et valider les paramètres de réseau hello.
6. Sur hello **paramètres de périphérique** page :
   
   1. Affecter une valeur unique **nom** tooyour appareil. Ce nom peut contenir 1 à 15 caractères ainsi que des lettres, des chiffres et des traits d'union.
   2. Cliquez sur hello **serveur iSCSI** icône ![icône du serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) pour hello **Type** d’appareil que vous créez. Un serveur iSCSI vous permettra de stockage par blocs tooprovision.
   3. Spécifiez si vous souhaitez que cette toobe appareil appartenant à un domaine. Si votre appareil est un serveur iSCSI, puis de joindre les domaine hello est facultative. Si vous décidez de votre domaine tooa du serveur iSCSI toonot jointure, cliquez sur **appliquer**, attendez hello toobe de paramètres appliqué et ignorez l’étape suivante de toohello.
      
       Si vous souhaitez que le domaine de tooa appareil toojoin hello. Entrez un **nom de domaine**, puis cliquez sur **Appliquer**.
      
      > [!NOTE]
      > Si la jointure de domaine de votre tooa du serveur iSCSI, assurez-vous que votre tableau virtuel est dans sa propre unité d’organisation (UO) pour Microsoft Azure Active Directory et aucun objet de stratégie de groupe (GPO) sont appliqué tooit.
      > 
      > 
   4. Une boîte de dialogue s’affiche. Entrez vos informations d’identification de domaine dans un format spécifié de hello. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). informations d’identification de domaine Hello seront vérifiées. Vous verrez un message d’erreur si les informations d’identification hello sont incorrectes.
      
       ![credentials](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Cliquez sur **Apply**. Cela s’applique et valider les paramètres de périphérique hello.
7. (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici.
   
    ![configuration du proxy web](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    Sur hello **proxy Web** page :
   
   1. Approvisionnement hello **URL du proxy Web** dans ce format : *http://host-IP adresse* ou *FDQN:Port nombre*. Notez que les URL HTTPS ne sont pas prises en charge.
   2. Définissez **Authentification** sur la valeur **De base** ou **Aucune**.
   3. Si vous utilisez l’authentification, vous devez également tooprovide un **nom d’utilisateur** et **mot de passe**.
   4. Cliquez sur **Apply**. Cela valider et appliquer les paramètres de proxy web hello configuré.
8. (Facultatif) Configurez les paramètres d’heure hello pour votre appareil, telles que de fuseau horaire et hello les serveurs NTP principal et secondaire. Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud.
   
    ![paramètres horaires](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    Sur hello **paramètres** page :
   
   1. Dans la liste déroulante hello, sélectionnez hello **fuseau horaire** basés sur l’emplacement géographique de hello dans le hello appareil est en cours de déploiement. fuseau horaire votre appareil Hello par défaut est PST. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
   2. Spécifiez un **serveur NTP principal** pour votre appareil ou acceptez la valeur par défaut hello time.windows.com. Vérifiez que votre réseau permet toopass de trafic NTP à partir de votre toohello de centre de données Internet.
   3. (Facultatif) Spécifiez un **serveur NTP secondaire** pour votre appareil.
   4. Cliquez sur **Apply**. Cela valider et appliquer les paramètres de temps hello configuré.
9. Configurer les paramètres de cloud hello pour votre appareil. Dans cette étape, vous allez effectuer la configuration de l’appareil local hello et puis inscrire les appareils hello auprès du service Gestionnaire de périphériques StorSimple.
   
   1. Entrez hello **clé d’inscription de Service** que vous avez obtenu **étape 2 : clé d’inscription Get hello** dans [déployer StorSimple Virtual Array - préparer hello Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Si ce n’est pas hello premier appareil que vous inscrivez auprès de ce service, vous devez tooprovide hello **clé de chiffrement de données de Service**. Cette clé est requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service du Gestionnaire de périphériques StorSimple. Pour plus d’informations, consultez trop[Get hello clé de chiffrement](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) sur votre ordinateur local de l’interface utilisateur web.
   3. Cliquez sur **S'inscrire**. Appareil de hello redémarre. Vous devrez peut-être toowait 2-3 minutes avant hello appareil correctement inscrit. Après le redémarrage de l’appareil de hello, vous serez dirigé toohello connexion dans la page.
      
      ![enregistrer un appareil](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Retour toohello portail Azure.
11. Accédez toohello **périphériques** Panneau de votre service. Si vous avez beaucoup de ressources, cliquez sur **Toutes les ressources**, cliquez sur votre nom de service (recherchez-le si nécessaire), puis cliquez sur **Appareils**.
12. Sur hello **périphériques** panneau, vérifiez que cet appareil hello toohello service connecté en vérifiant hello état. état du périphérique Hello doit être **prêt tooset des**.
    
    ![enregistrer un appareil](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Étape 2 : Configuration hello en tant que serveur iSCSI

Effectuer hello Bonjour le programme d’installation de toocomplete portail Azure hello requis appareil comme suit.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>Appareil de hello tooconfigure en tant que serveur iSCSI

1. Service de gestionnaire de périphériques StorSimple tooyour et puis trop**Gestion > appareils**. Bonjour **périphériques** panneau, appareil hello sélectionnez vous venez de créer. Ce périphérique apparaît en tant que **prêt tooset des**.
   
    ![Configurer l’appareil en tant que serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Cliquez sur périphérique de hello et vous verrez un message de bannière indiquant que cet appareil hello est toosetup prêt.
   
    ![Configurer l’appareil en tant que serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Cliquez sur **configurer** sur la barre de commandes de périphérique hello. Cela ouvre hello **configurer** panneau. Bonjour **configurer** panneau, hello suivant :
   
   * nom du serveur iSCSI Hello est remplie automatiquement.
   * Assurez-vous que le chiffrement de stockage cloud hello est défini trop**activé**. Cela garantit que les données de salutation envoyées à partir de hello appareil toohello cloud sont chiffrées.
   * Spécifiez une clé de chiffrement de 32 caractères et enregistrez-la dans une application de gestion des clés pour référence ultérieure.
   * Sélectionnez un toobe de compte de stockage utilisé avec votre appareil. Dans cet abonnement, vous pouvez sélectionner un compte de stockage existant, ou vous pouvez cliquer sur **ajouter** toochoose un compte à partir d’un autre abonnement.
     
     ![Configurer l’appareil en tant que serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Cliquez sur **configurer** toocomplete configurer le serveur iSCSI hello.
   
    ![Configurer l’appareil en tant que serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Vous serez averti que la création du serveur iSCSI hello est en cours d’exécution. Une fois que le serveur iSCSI hello est correctement créé, hello **périphériques** panneau est mis à jour et l’état du périphérique hello correspondante est **Online**.
   
    ![Configurer l’appareil en tant que serveur iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Étape 3 : Ajout d’un volume

1. Bonjour **périphériques** panneau, appareil hello sélectionnez vous venez de configurer en tant que serveur iSCSI. Cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **Ajout du volume**. Vous pouvez également cliquer sur **+ ajouter un volume** à partir de la barre de commandes hello. Cela ouvre hello **Ajout du volume** panneau.
   
    ![Ajout d’un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. Bonjour **Ajout du volume** panneau, hello suivant :
   
   * Bonjour **nom de Volume** , entrez un nom unique pour votre volume. nom de Hello doit être une chaîne qui contient des caractères too127 3.
   * Bonjour **Type** déroulante liste, spécifiez si toocreate un **à plusieurs niveaux** ou **attaché localement** volume. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez **Volume** **attaché localement**. Pour toutes les autres données, sélectionnez **Volume** **hiérarchisé**.
   * Bonjour **capacité** Indiquez la taille de hello du volume de hello. Un volume hiérarchisé doit être compris entre 500 Go et 5 To, tandis qu’un volume attaché doit être compris entre 50 Go et 500 Go.
     
     Un volume attaché localement est approvisionné et garantit que les données de salutation principal dans le volume de hello restent sur l’appareil de hello et ne pas déborder toohello cloud.
     
     Un volume hiérarchisé sur hello autre part est alloué. Lorsque vous créez un volume hiérarchisé, environ 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello. Par exemple, si vous avez configuré un volume de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données. Cela implique à son tour est que si vous manquez tout l’espace local hello sur le périphérique de hello, vous ne pouvez pas configurer un partage hiérarchisé (car hello 10 % ne sera pas disponible).
     
     ![Ajout d’un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Cliquez sur **connecté des ordinateurs hôtes**, sélectionnez un accès contrôle enregistrement (ACR) correspondante toohello initiateur iSCSI que vous souhaitez tooconnect toothis volume, puis cliquez sur **sélectionnez**. <br><br> 
3. tooadd un nouvel hôte connecté, cliquez sur **ajouter un nouveau**, entrez un nom pour l’hôte de hello et son iSCSI nom qualifié (IQN), puis cliquez sur **ajouter**. Si vous n’avez pas hello IQN, passez trop[obtenir de l’annexe a : hello IQN d’un hôte Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Ajout d’un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Lorsque vous avez terminé de configurer votre volume, cliquez sur **OK**. Un volume est créé par hello spécifié les paramètres et que vous voyez une notification. Par défaut, sauvegarde et surveillance seront activées pour le volume de hello.
   
     ![Ajout d’un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm qui hello volume a été a été créé correctement, accédez toohello **Volumes** panneau. Vous devez voir volume hello répertorié.
   
   ![Ajout d’un volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Étape 4 : Montage, initialisation et formatage d’un volume

Effectuer hello suivant les étapes toomount, initialiser et formater vos volumes StorSimple sur un ordinateur hôte Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, initialiser et formater un volume

1. Ouvrez hello **initiateur iSCSI** application sur le serveur approprié de hello.
2. Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **découverte** , cliquez sur **découvrir un portail**.
   
    ![Découvrir un portail](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. Bonjour **détecter un portail cible** boîte de dialogue, fournir l’adresse IP de hello de votre interface réseau iSCSI, puis cliquez sur **OK**.
   
    ![Adresse IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **cibles** localiser hello, onglet **découverts cibles**. (Chaque volume sera une cible de découverte). état du périphérique Hello doit apparaître en tant que **inactif**.
   
    ![cibles découvertes](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Sélectionnez un appareil cible, puis cliquez sur **Connecter**. Une fois hello est connecté, état de hello doit également modifier**connecté**. (Pour plus d’informations sur l’utilisation de l’initiateur iSCSI Microsoft hello, consultez [installation et configuration de Microsoft iSCSI Initiator][1].
   
    ![sélectionner un appareil cible](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. Sur votre hôte Windows, appuyez sur la touche de Logo Windows hello + X, puis cliquez sur **exécuter**.
7. Bonjour **exécuter** boîte de dialogue, tapez **Diskmgmt.msc**. Cliquez sur **OK**et hello **gestion des disques** boîte de dialogue s’affiche. volet de droite Hello affichera les volumes hello sur votre ordinateur hôte.
8. Bonjour **gestion des disques** fenêtre hello volumes montés s’affichent comme illustré hello après l’illustration. Cliquez sur hello découverts volume (cliquez sur le nom du disque hello), puis cliquez sur **Online**.
   
    ![Gestion des disques](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Cliquez avec le bouton droit et sélectionnez **Initialiser le disque**.
   
    ![initialiser le disque 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Dans la boîte de dialogue hello, sélectionnez hello disques tooinitialize, puis cliquez sur **OK**.
    
    ![initialiser le disque 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. l’Assistant Nouveau Volume Simple Hello démarre. Sélectionnez une taille de disque, puis cliquez sur **Suivant**.
    
    ![assistant nouveau volume 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Affecter un volume de toohello de lettre de lecteur, puis cliquez sur **suivant**.
    
    ![assistant nouveau volume 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Entrez le volume de hello paramètres tooformat hello. **Sur Windows Server, seul le système NTFS est pris en charge.** Définissez too64K de taille unité hello d’allocation. Nommez votre volume. Il est recommandé pour ce nom de volume nom toobe identiques toohello que vous avez indiqué dans votre tableau virtuel StorSimple. Cliquez sur **Suivant**.
    
    ![assistant nouveau volume 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Vérifiez les valeurs hello pour le volume, puis cliquez sur **Terminer**.
    
    ![assistant nouveau volume 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    les volumes de Hello s’affichent en tant que **Online** sur hello **gestion des disques** page.
    
    ![volumes en ligne](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toouse hello interface utilisateur web locale trop[administrer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Annexe a : hello de Get IQN d’un hôte Windows Server

Effectuer hello suivant les étapes tooget hello iSCSI nom qualifié (IQN) d’un hôte Windows qui exécute Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>tooget hello IQN d’un hôte Windows

1. Démarrez l’initiateur iSCSI Microsoft hello sur votre hôte Windows.
2. Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **Configuration** , sélectionnez et copiez les chaîne hello de hello **nom de l’initiateur** champ.
   
    ![iSCSI Initiator Properties](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Enregistrez cette chaîne.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



