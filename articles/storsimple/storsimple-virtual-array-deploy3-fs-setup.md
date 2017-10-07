---
title: aaaSet des StorSimple Virtual Array en tant que serveur de fichiers | Documents Microsoft
description: "Ce didacticiel tiers dans le déploiement de StorSimple Virtual Array fait en sorte que vous tooset d’un périphérique virtuel en tant que serveur de fichiers."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Déploiement de StorSimple Virtual Array - Configuration comme un serveur de fichiers via le portail Azure
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Introduction
Cet article décrit comment tooperform la configuration initiale, inscrire votre serveur de fichiers StorSimple, le programme d’installation complète hello appareil et créer et connecter les partages tooSMB. Il s’agit hello dernier article de la série de hello des didacticiels de déploiement requis toocompletely déployer votre tableau virtuel en tant que serveur de fichiers ou un serveur iSCSI.

processus d’installation et la configuration Hello peut prendre environ 10 minutes toocomplete. les informations de Hello dans cet article s’appliquent uniquement toohello déploiement Hello StorSimple Virtual Array. Pour le déploiement de hello de périphériques de série StorSimple 8000, accédez à : [déployer votre appareil de série StorSimple 8000 Update 2 en cours d’exécution](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Configuration requise
Avant de configurer votre solution StorSimple Virtual Array, assurez-vous que :

* Vous avez configuré un groupe virtuel et le tooit connecté en tant que hello détaillée dans [configurer un tableau virtuel StorSimple dans Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [configurer un tableau virtuel StorSimple dans VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* Vous avez la clé d’inscription hello du service de gestionnaire de périphériques StorSimple hello que vous avez créé des tableaux de virtuel StorSimple toomanage. Pour plus d’informations, consultez [étape 2 : clé d’inscription Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) pour StorSimple Virtual Array.
* S’il s’agit de hello deuxième ou ultérieures tableau virtuel que vous inscrivez avec un service de gestionnaire de périphériques StorSimple existant, vous devez disposer de clé de chiffrement de données de service hello. Cette clé a été générée lorsque le premier périphérique de hello a été correctement inscrit auprès de ce service. Si vous avez perdu cette clé, consultez [Get hello clé de chiffrement](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) pour votre StorSimple Virtual Array.

## <a name="step-by-step-setup"></a>Configuration étape par étape
Utilisez hello suivi tooset des instructions détaillées et configurer votre StorSimple Virtual Array.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Étape 1 : Terminer web locale de hello le programme d’installation de l’interface utilisateur et inscrire votre appareil
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello le programme d’installation et inscrire un appareil hello
1. Ouvrez une fenêtre de navigateur et se connecter à l’interface utilisateur de web local toohello. Entrez :
   
   `https://<ip-address of network interface>`
   
   Utilisez les URL de connexion hello indiqué à l’étape précédente de hello. Vous voyez une erreur indiquant qu’il existe un problème avec le certificat de sécurité du site Web de hello. Cliquez sur **continuer la page Web de toothis**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Connexion toohello web de l’interface utilisateur de votre tableau virtuel en tant que **StorSimpleAdmin**. Entrez le mot de passe administrateur de périphérique hello que vous avez modifié à l’étape 3 : tableau virtuel de démarrage hello dans [configurer un tableau virtuel StorSimple dans Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou dans [configurer un tableau virtuel StorSimple dans VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Vous accédez toohello **accueil** page. Cette page décrit hello divers paramètres requis tooconfigure et inscrire hello tableau virtuel avec le service du Gestionnaire de périphériques StorSimple hello. Hello **paramètres réseau**, **les paramètres de proxy Web**, et **paramètres** sont facultatifs. Hello uniquement les paramètres requis sont **paramètres de périphérique** et **paramètres de Cloud**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. Bonjour **paramètres réseau** page sous **interfaces réseau**, DATA 0 sera automatiquement configuré pour vous. Chaque interface réseau est défini par son adresse IP par défaut tooget automatiquement (DHCP). Par conséquent, une adresse IP, un sous-réseau et une passerelle sont automatiquement attribués (pour IPv4 et IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Si vous avez ajouté plusieurs interfaces réseau lors de la configuration de hello du périphérique de hello, vous pouvez les configurer ici. Notez que vous pouvez configurer votre interface réseau en IPv4 uniquement ou en IPv4 et IPv6. Les configurations en IPv6 uniquement ne sont pas prises en charge.
5. Serveurs DNS sont requis car elles sont utilisées lorsque votre appareil tente toocommunicate avec des fournisseurs de services de stockage cloud tooresolve votre périphérique par nom lorsque configuré comme un serveur de fichiers. Bonjour **paramètres réseau** page sous hello **serveurs DNS**:
   
   1. Un serveur DNS principal et un serveur secondaire sont automatiquement configurés. Si vous choisissez tooconfigure des adresses IP statiques, vous pouvez spécifier des serveurs DNS. Pour une haute disponibilité, nous vous recommandons de configurer un serveur DNS principal et un serveur secondaire.
   2. Cliquez sur **appliquer** tooapply et valider les paramètres de réseau hello.
6. Bonjour **paramètres de périphérique** page :
   
   1. Affecter une valeur unique **nom** tooyour appareil. Ce nom peut contenir 1 à 15 caractères ainsi que des lettres, des chiffres et des traits d'union.
   2. Cliquez sur hello **serveur de fichiers** icône ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) pour hello **Type** d’appareil que vous créez. Un serveur de fichiers vous permettra de dossiers de toocreate partagé.
   3. Que votre appareil est un serveur de fichiers, vous devez le domaine de tooa appareil toojoin hello. Entrez un **nom de domaine**.
   4. Cliquez sur **Apply**.
7. Une boîte de dialogue s’affiche. Entrez vos informations d’identification de domaine dans un format spécifié de hello. Cliquez sur une icône de coche hello. informations d’identification de domaine Hello sont vérifiées. Vous voyez un message d’erreur si les informations d’identification hello sont incorrectes.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Cliquez sur **Apply**. Cela s’applique et valider les paramètres de périphérique hello.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Assurez-vous que votre tableau virtuel est dans sa propre unité d’organisation (UO) pour Active Directory et aucun objet de stratégie de groupe (GPO) est appliqué tooit ou héritée. Stratégie de groupe peut-être installer des applications, telles que le logiciel antivirus sur hello StorSimple Virtual Array. L’installation des logiciels supplémentaires n’est pas prise en charge et peut entraîner une corruption de toodata. 
   > 
   > 
9. (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   Bonjour **proxy Web** page :
   
   1. Approvisionnement hello **URL du proxy Web** dans ce format : *http://&lt;adresse IP de l’hôte ou le nom de domaine complet&gt;: numéro de Port*. Notez que les URL HTTPS ne sont pas prises en charge.
   2. Définissez **Authentification** sur la valeur **De base** ou **Aucune**.
   3. Si l’authentification, vous devez également tooprovide un **nom d’utilisateur** et **mot de passe**.
   4. Cliquez sur **Apply**. Cela valider et appliquer les paramètres de proxy web hello configuré.
10. (Facultatif) Configurez les paramètres d’heure hello pour votre appareil, telles que de fuseau horaire et hello les serveurs NTP principal et secondaire. Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    Bonjour **paramètres** page :
    
    1. Dans la liste déroulante de hello, sélectionnez hello **fuseau horaire** basés sur l’emplacement géographique de hello dans le hello appareil est en cours de déploiement. fuseau horaire votre appareil Hello par défaut est PST. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
    2. Spécifiez un **serveur NTP principal** pour votre appareil ou acceptez la valeur par défaut hello time.windows.com. Vérifiez que votre réseau permet toopass de trafic NTP à partir de votre toohello de centre de données Internet.
    3. (Facultatif) Spécifiez un **serveur NTP secondaire** pour votre appareil.
    4. Cliquez sur **Apply**. Cela valider et appliquer les paramètres de temps hello configuré.
11. Configurer les paramètres de cloud hello pour votre appareil. Dans cette étape, vous allez effectuer la configuration de l’appareil local hello et puis inscrire les appareils hello auprès du service Gestionnaire de périphériques StorSimple.
    
    1. Entrez hello **clé d’inscription de Service** que vous avez obtenu [étape 2 : clé d’inscription Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) pour StorSimple Virtual Array.
    2. S’il s’agit de votre premier périphérique de l’inscription auprès de ce service, vous aurez par hello **clé de chiffrement de données de Service**. Copiez-la et enregistrez-la en lieu sûr. Cette clé est requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service du Gestionnaire de périphériques StorSimple. 
       
       Si ce n’est pas hello premier appareil que vous inscrivez auprès de ce service, vous devez tooprovide hello clé de chiffrement. Pour plus d’informations, consultez tooget hello [clé de chiffrement de données de service](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) sur votre ordinateur local de l’interface utilisateur web.
    3. Cliquez sur **S'inscrire**. Appareil de hello redémarre. Vous devrez peut-être toowait 2-3 minutes avant hello appareil correctement inscrit. Après le redémarrage de l’appareil de hello, vous serez dirigé toohello connexion dans la page.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Retour toohello portail Azure. Accédez trop**toutes les ressources**, recherchez votre service de gestionnaire de périphériques StorSimple.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Bonjour filtrées, sélectionnez votre service StorSimple le Gestionnaire de périphériques et puis accédez trop**Gestion > appareils**. Bonjour **périphériques** panneau, vérifiez que l’appareil hello toohello service connecté et qu’il a l’état de hello **prêt tooset des**.
    
    ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Étape 2 : Configuration hello en tant que serveur de fichiers
Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com/) toocomplete hello requis le programme d’installation de périphérique.

#### <a name="tooconfigure-hello-device-as-file-server"></a>Appareil de hello tooconfigure en tant que serveur de fichiers
1. Service de gestionnaire de périphériques StorSimple tooyour et puis trop **Gestion > appareils**. Bonjour **périphériques** panneau, appareil hello sélectionnez vous venez de créer. Ce périphérique apparaît en tant que **prêt tooset des**.
   
   ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Cliquez sur périphérique de hello et vous verrez un message de bannière indiquant que cet appareil hello est toosetup prêt.
   
    ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Cliquez sur **configurer** sur la barre de commandes hello. Cela ouvre hello **configurer** panneau. Bonjour **configurer** panneau, hello suivant :
   
    1. nom de serveur de fichiers Hello est remplie automatiquement.
    
    2. Assurez-vous que le chiffrement de stockage cloud hello est défini trop**activé**. Cela chiffre toutes les données de hello sont envoyées toohello cloud. 
    
    3. Une clé AES de 256 bits est utilisée avec la clé hello défini par l’utilisateur de chiffrement. Spécifier une clé de 32 caractères et entrer tooconfirm de clé hello il. Enregistrement hello clé dans une application de gestion de clés pour référence ultérieure.
    
    4. Cliquez sur **configurer les paramètres requis** informations d’identification de compte de stockage toospecify toobe utilisé avec votre appareil. Si aucune information d’identification du compte de stockage n’est configurée, cliquez sur **Ajouter nouveau**. **Vérifiez que compte de stockage hello que vous utilisez prend en charge les objets BLOB de blocs. Les objets blob de pages ne sont pas pris en charge.** En savoir plus sur [les objets blob de blocs et de pages](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. Bonjour **ajouter un informations d’identification du compte de stockage** panneau, hello suivant : 

    1. Choisissez l’abonnement actuel si le compte de stockage hello est Bonjour même abonnement que le service de hello. Spécifiez l’autre est le stockage de hello compte est en dehors de l’abonnement au service hello. 
    
    2. À partir de la liste déroulante de hello, choisissez un compte de stockage existant. 
    
    3. emplacement de Hello est rempli automatiquement en fonction de hello spécifié compte de stockage. 
    
    4. Activer SSL tooensure un canal de communication réseau sécurisée entre les appareils hello et de cloud de hello.
    
    5. Cliquez sur **ajouter** tooadd d’informations d’identification du compte de ce stockage. 
   
        ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Une fois que les informations d’identification de compte de stockage hello sont correctement créée, hello **configurer** panneau sera mise à jour toodisplay hello spécifié des informations d’identification du compte de stockage. Cliquez sur **Configurer**.
   
   ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Vous pouvez constater qu’un serveur de fichiers est en cours de création. Une fois que le serveur de fichiers hello est créé avec succès, vous serez averti.
   
   ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   état du périphérique Hello modifiera également trop**Online**.
   
   ![Configurer un serveur de fichiers](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   Vous pouvez passer tooadd un partage.

## <a name="step-3-add-a-share"></a>Étape 3 : Ajout d’un partage
Effectuer hello comme suit dans hello [portail Azure](https://portal.azure.com/) toocreate un partage.

#### <a name="toocreate-a-share"></a>toocreate un partage
1. Sélectionnez l’appareil de serveur de fichiers hello vous avez configuré dans hello précédant l’étape et cliquez sur **...**  (ou avec le bouton droit). Dans le menu contextuel de hello, sélectionnez **ajouter partage**. Vous pouvez également cliquer sur **+ ajouter un partage** sur la barre de commandes de périphérique hello.
   
   ![Ajouter un partage](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Spécifiez hello suivant les paramètres de partage :

    1. Nom unique pour votre partage. nom de Hello doit être une chaîne qui contient des caractères too127 3.
    
    2. Facultatif **Description** pour partage de hello. description de Hello aidera à identifier les propriétaires de partage hello.
    
    3. A **Type** pour le partage de hello. type de Hello peut être **à plusieurs niveaux** ou **attaché localement**, étant hiérarchisé hello par défaut. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un partage **épinglé localement** . Pour toutes les autres données, sélectionnez un partage **à plusieurs niveaux** .
    Un partage attaché localement est approvisionné et garantit que les données de salutation principal sur le partage de hello restent local toohello appareil et ne pas déborder toohello cloud. Un partage hiérarchisé sur hello autre part est alloué. Lorsque vous créez un partage hiérarchisé, 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello. Par exemple, si vous avez configuré un volume de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données. À son tour, cela implique que si vous manquez tout l’espace local hello sur l’appareil de hello, vous ne pouvez pas configurer un partage hiérarchisé.
   
    4. Bonjour **valeur par défaut toutes les autorisations** champ, affecter hello autorisations toohello utilisateur ou groupe hello qui accède à ce partage. Spécifier le nom hello de hello utilisateur ou un groupe d’utilisateurs hello  *john@contoso.com*  format. Nous vous recommandons d’utiliser un tooaccess des privilèges d’administrateur utilisateur groupe (au lieu d’un seul utilisateur) tooallow ces partages. Une fois que vous avez affecté des autorisations hello ici, vous pouvez ensuite utiliser l’Explorateur de fichiers toomodify ces autorisations.
   
    5. Cliquez sur **ajouter** partage de hello toocreate. 
    
        ![Ajouter un partage](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Vous êtes informé que la création du partage hello est en cours d’exécution.
   
        ![Ajouter un partage](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Une fois que le partage de hello est créé par hello spécifié des paramètres, hello **partages** panneau met à jour de nouveau partage de tooreflect hello. Par défaut, analyse et sauvegarde sont activées pour le partage de hello.
   
    ![Ajouter un partage](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Étape 4 : Connecter toohello partage
Vous devez désormais tooconnect tooone ou plus d’actions que vous avez créé à l’étape précédente de hello. Effectuez ces étapes sur votre tooyour hôte connecté de Windows Server StorSimple Virtual Array.

#### <a name="tooconnect-toohello-share"></a>partage de toohello tooconnect
1. Appuyez sur ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + r. Dans la fenêtre Exécuter hello, spécifiez hello *&#92; &#92;&lt; nom de serveur de fichiers&gt;*  comme chemin d’accès de hello, en remplaçant *nom de serveur de fichiers* avec appareil de hello nom vous attribué tooyour serveur de fichiers. Cliquez sur **OK**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. L’Explorateur de fichiers s’affiche. Vous devez maintenant être partages hello en mesure de toosee que vous avez créé en tant que dossiers. Sélectionnez et double-cliquez sur un contenu de hello tooview partage (dossier).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Vous pouvez maintenant ajouter des partages de fichiers toothese et effectuer une sauvegarde.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment toouse hello interface utilisateur web locale trop[administrer votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

