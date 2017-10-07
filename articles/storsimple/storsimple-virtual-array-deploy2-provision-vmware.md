---
title: aaaProvision StorSimple Virtual Array dans VMware | Documents Microsoft
description: "Ce deuxième didacticiel de déploiement de StorSimple Virtual Array implique la configuration d'un appareil virtuel dans VMware."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Déploiement de StorSimple Virtual Array - Configuration dans VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel décrit comment tooprovision et connectez-vous tooa StorSimple Virtual Array sur un système hôte exécutant VMware ESXi 5.5 et versions ultérieures. Cet article s’applique à déploiement toohello de StorSimple des réseaux virtuels dans le portail Azure et hello Microsoft Azure Government Cloud.

Vous devez tooprovision de privilèges d’administrateur et que vous connectez un appareil virtuel tooa. le programme d’installation de configuration et initiale Hello peut prendre environ 10 minutes toocomplete.

## <a name="provisioning-prerequisites"></a>Configuration des composants requis
Hello conditions préalables tooprovision un appareil virtuel sur un système hôte VMware ESXi 5.5 en cours d’exécution et ci-dessus, sont les suivantes.

### <a name="for-hello-storsimple-device-manager-service"></a>Pourquoi le service du Gestionnaire de périphériques StorSimple
Avant de commencer, assurez-vous que :

* Vous avez effectué toutes les étapes de hello dans [portail hello de préparation pour StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Vous avez téléchargé l’image d’appareil virtuel hello pour VMware à partir de hello portail Azure. Pour plus d’informations, consultez **étape 3 : image de périphérique virtuel téléchargement hello** de [portail hello de préparation pour le guide de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Pour un appareil virtuel StorSimple hello
Avant de déployer un appareil virtuel, assurez-vous que :

* Vous avez accès tooa hôte système exécutant Hyper-V (2008 R2 ou version ultérieure) que peut être utilisé tooa configurer un périphérique.
* système d’hôte Hello est en mesure de toodedicate hello suivant tooprovision de ressources de votre appareil virtuel :

  * Un minimum de 4 cœurs.
  * Au moins 8 Go de RAM. Si vous envisagez d’unité de stockage tooconfigure hello virtuelle en tant que serveur de fichiers, 8 Go prend en charge moins de 2 millions de fichiers. Vous avez besoin de 16 Go de RAM toosupport 2-4 millions de fichiers.
  * Une interface réseau.
  * Un disque virtuel de 500 Go pour les données système.

### <a name="for-hello-network-in-datacenter"></a>Pour le réseau hello dans le centre de données
Avant de commencer, assurez-vous que :

* Vous avez consulté hello réseau exigences toodeploy un appareil virtuel StorSimple et réseau de centre de données hello configuré conformément aux exigences de hello. 

## <a name="step-by-step-provisioning"></a>Configuration étape par étape
tooprovision et connecter un appareil virtuel tooa, vous devez hello tooperform comme suit :

1. Assurez-vous que le système hôte de hello dispose suffisamment ressources toomeet hello virtuel minimales requises.
2. Configurez un appareil virtuel dans votre hyperviseur.
3. Démarrer un appareil virtuel hello et obtenir l’adresse IP de hello.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Étape 1 : Vérifier que le système hôte répond aux exigences minimales de l’appareil virtuel
toocreate un appareil virtuel, vous devez :

* Système d’hôte tooa accès exécutant VMware ESXi Server 5.5 et versions ultérieures.
* Client VMware vSphere sur votre hôte ESXi de système toomanage hello.

  * Un minimum de 4 cœurs.
  * Au moins 8 Go de RAM. Si vous envisagez d’unité de stockage tooconfigure hello virtuelle en tant que serveur de fichiers, 8 Go prend en charge moins de 2 millions de fichiers. Vous avez besoin de 16 Go de RAM toosupport 2-4 millions de fichiers.
  * Une interface réseau connecté réseau toohello capable de routage du trafic tooInternet. Hello minimale de bande passante Internet doit être 5 tooallow Mbits/s pour une utilisation optimale du périphérique de hello.
  * Un disque virtuel de 500 Go pour les données.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Étape 2 : Configuration d'un appareil virtuel dans l'hyperviseur
Effectuer hello suivant les étapes tooprovision un appareil virtuel dans votre hyperviseur.

1. Copier l’image du périphérique virtuel hello sur votre système. Vous avez téléchargé cette image virtuelle via hello portail Azure.

   1. Assurez-vous que vous avez téléchargé le dernier fichier d’image hello. Si vous avez téléchargé précédemment les image hello, téléchargez-le à nouveau tooensure que vous avez la dernière image de hello. image plus récente de Hello possède deux fichiers (au lieu d’un).
   2. Prenez note de l’emplacement hello où vous avez copié les images hello que vous utilisez cette image plus loin dans la procédure de hello.

2. Ouvrez une session dans toohello server ESXi à l’aide du client de vSphere hello. Vous devez toocreate de privilèges d’administrateur toohave une machine virtuelle.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. Dans le client de vSphere hello, dans la section d’inventaire hello dans le volet gauche de hello, sélectionnez hello ESXi serveur.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Télécharger le serveur de ESXi toohello hello VMDK. Accédez toohello **Configuration** onglet dans le volet de droite hello. Sous **Matériel**, sélectionnez **Stockage**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. Bonjour avec le bouton droit volet, sous **banques de données**, sélectionnez hello banque de données où vous souhaitez hello de tooupload VMDK. banque de données Hello doit avoir suffisamment d’espace libre pour hello du système d’exploitation et des disques de données.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Cliquez avec le bouton droit et sélectionnez **Parcourir les magasins de données**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Une fenêtre **Navigateur du magasin de données** s’ouvre.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Dans la barre d’outils hello, cliquez sur ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icône toocreate un nouveau dossier. Spécifiez le nom du dossier hello et prenez note de celui-ci. Vous utiliserez ce nom de dossier plus tard lors de la création d'une machine virtuelle (recommandée). Cliquez sur **OK**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Hello nouveau dossier apparaît dans le volet gauche de hello Hello **navigateur du magasin de données**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Cliquez sur icône de téléchargement hello ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) et sélectionnez **télécharger le fichier**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Parcourir et pointez les fichiers VMDK toohello que vous avez téléchargé. Il existe deux fichiers. Sélectionnez un tooupload de fichier.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Cliquez sur **Ouvrir**. téléchargement de Hello de toohello de fichier VMDK hello spécifié banque de données démarre. Il peut prendre plusieurs minutes pour tooupload de fichier hello.
13. Une fois le téléchargement de hello est terminé, vous voir fichier hello hello le magasin de données dans le dossier hello créé.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Maintenant télécharger hello toohello du fichier VMDK deuxième même magasin de données.
14. Retourne la fenêtre du client toohello vSphere. Sélectionnez le serveur ESXi, cliquez avec le bouton droit et choisissez **Nouvelle machine virtuelle**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Une fenêtre **Créer une machine virtuelle** s'affiche. Sur hello **Configuration** page, sélectionnez hello **personnalisé** option. Cliquez sur **Suivant**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Sur hello **nom et l’emplacement** , spécifiez le nom hello de votre machine virtuelle. Ce nom doit correspondre au nom de dossier hello (meilleure pratique) spécifié à l’étape 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Sur hello **stockage** , sélectionnez une banque de données que vous souhaitez toouse tooprovision votre machine virtuelle.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Sur hello **Version de Machine virtuelle** page, sélectionnez **Version de Machine virtuelle : 8**. Versions 8 too11 sont toutes prises en charge.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Sur hello **système d’exploitation invité** page, sélectionnez hello **système d’exploitation invité** en tant que **Windows**. Pour **Version**, dans la liste déroulante de hello, sélectionnez **Microsoft Windows Server 2012 (64 bits)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Sur hello **unités centrales** page, ajuster hello **nombre de sockets virtuels** et **nombre de noyaux par socket virtuel** afin que hello **nombre Total de cœurs**est de 4 (ou plus). Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Sur hello **mémoire** , spécifiez 8 Go (ou plus) de RAM. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Sur hello **réseau** , spécifiez le nombre de hello des interfaces réseau de hello. Hello minimum requis est une interface réseau.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Sur hello **contrôleur SCSI** page, acceptez la valeur par défaut hello **contrôleur SAS de logique LSI**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Sur hello **sélectionnez un disque** choisissez **utiliser un disque virtuel existant**. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Sur hello **sélectionner un disque existant** sous **chemin d’accès du fichier de disque**, cliquez sur **Parcourir**. Cette opération ouvre une boîte de dialogue **Parcourir les magasins de données** . Accédez emplacement toohello où vous avez téléchargé hello VMDK. Vous voyez maintenant qu’un seul fichier dans le magasin de données hello comme hello deux fichiers que vous avez téléchargé au départ ont été fusionnées. Sélectionnez le fichier de hello et cliquez sur **OK**. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Sur hello **Options avancées** page, accepter la valeur par défaut hello et cliquez sur **suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Sur hello **tooComplete prêt** passez en revue tous les paramètres de hello associés de machine virtuelle hello. Vérifiez **modifier les paramètres d’ordinateur virtuel hello avant la fin de**. Cliquez sur **Continuer**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Sur hello **propriétés des Machines virtuelles** page hello **matériel** onglet, recherchez matériels des périphériques hello. Sélectionnez **Nouveau disque dur**. Cliquez sur **Ajouter**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Une fenêtre **Ajout de matériel** apparaît. Sur hello **Type d’appareil** sous **choisir un type hello du périphérique que vous souhaitez tooadd**, sélectionnez **disque**, puis cliquez sur **suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Sur hello **sélectionnez un disque** choisissez **créer un nouveau disque virtuel**. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Sur hello **créer un disque** , changez hello **taille du disque** too500 Go (ou plus). 500 Go est au minimum le hello, vous pouvez toujours configurer un disque plus volumineux. Notez que vous ne peut pas développer ou réduire disque hello configuré qu’une seule fois. Pour plus d’informations sur la taille de hello tooprovision de disque, consultez la section de dimensionnement de hello Bonjour [document de pratiques meilleures](storsimple-ova-best-practices.md). Sous **Configuration du disque**, sélectionnez **Allocation dynamique**. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Sur hello **Options avancées** page, acceptez la valeur par défaut hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Sur hello **tooComplete prêt** passez en revue les options de disque hello. Cliquez sur **Terminer**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Retourner la page de propriétés de l’ordinateur virtuel toohello. Un nouveau disque dur est ajouté tooyour virtual machine. Cliquez sur **Terminer**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Avec votre machine virtuelle sélectionnée dans le volet droit de hello, accédez à toohello **Résumé** onglet. Passez en revue les paramètres hello pour votre machine virtuelle.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Votre machine virtuelle est désormais configurée. étape suivante de Hello est toopower sur cet ordinateur et obtenir l’adresse IP de hello.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Étape 3 : Démarrer un appareil virtuel hello et obtenir une adresse IP de hello
Effectuer hello suivant les étapes toostart votre appareil virtuel et se connecter tooit.

#### <a name="toostart-hello-virtual-device"></a>APPAREIL virtuel toostart hello
1. Démarrer un appareil virtuel hello. Dans vSphere hello Configuration Manager, dans le volet gauche de hello, sélectionnez votre appareil et avec le bouton droit toobring menu contextuel de hello. Sélectionnez **Alimentation** puis **Mise sous tension**. Cette opération met votre machine virtuelle sous tension. Vous pouvez afficher l’état de hello en bas de hello **tâches récentes** volet du client de vSphere hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. tâches de configuration Hello prendra quelques minutes toocomplete. Une fois que l’appareil de hello est en cours d’exécution, accédez à toohello **Console** onglet. Envoyer Ctrl + Alt + Suppr toolog toohello appareil. Vous pouvez également, pointez le curseur de hello dans la fenêtre de console hello et appuyez sur Ctrl + Alt + insertion. Hello utilisateur par défaut est *StorSimpleAdmin* et mot de passe hello *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire à la première ouverture de session hello. Vous êtes un mot de passe hello toochange demandées.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Entrez un mot de passe contenant au moins 8 caractères. mot de passe Hello doit contenir 3 des 4 de ces conditions : les caractères majuscules, minuscules, numériques et spéciaux. Entrez à nouveau tooconfirm de mot de passe hello il. Vous serez averti que ce mot de passe hello a changé.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Une fois le mot de passe hello est modifié avec succès, un appareil virtuel hello peut redémarrer. Attendez que hello redémarrage toocomplete. console Windows PowerShell de Hello du périphérique de hello peut-être s’afficher avec une barre de progression.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Les étapes 6 à 8 s’appliquent uniquement lors de l’amorçage dans un environnement non DHCP. Si vous êtes dans un environnement DHCP, ignorez ces étapes et accédez toostep 9. Si vous avez démarré la configuration de votre appareil dans un environnement non-DHCP, vous verrez hello suivant l’écran.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Ensuite, configurez le réseau de hello.
7. Hello d’utilisation `Get-HcsIpAddress` commande des interfaces réseau de toolist hello activés sur votre appareil virtuel. Si votre appareil dispose d’une seule interface réseau activée, le nom affecté toothis interface de hello par défaut est `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Hello d’utilisation `Set-HcsIpAddress` réseau de hello tooconfigure applet de commande. Voici un exemple :

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Après hello l’installation initiale est terminée et les appareils hello a démarré, vous verrez le texte de bannière du périphérique hello. Prenez note de l’adresse IP de hello et l’URL de hello affichés dans le dispositif hello toomanage hello bannière texte. Vous utiliserez cette IP adresse tooconnect toohello interface utilisateur web de votre appareil virtuel et hello complète local et d’inscription.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Facultatif) Effectuez cette étape uniquement si vous déployez votre appareil dans hello gouvernement Cloud. Vous serez désormais activer le mode d’United States traitement Standard FIPS (Federal Information) hello sur votre appareil. norme de Hello FIPS 140 définit les algorithmes de chiffrement approuvés pour une utilisation par les systèmes d’ordinateur gouvernement fédéral nous pour une protection des données sensibles hello.

    1. mode FIPS hello tooenable, exécutez hello suivant l’applet de commande :

        `Enable-HcsFIPSMode`
    2. Redémarrer votre périphérique après avoir activé le mode FIPS hello afin que les validations de chiffrement hello prennent effet.

       > [!NOTE]
       > Vous pouvez activer ou désactiver le mode FIPS sur votre appareil. Appareil de hello en alternance entre le mode FIPS et non-FIPS n’est pas pris en charge.
       >
       >

Si votre appareil ne satisfait pas la configuration minimale requise de hello, vous verrez une erreur dans le texte de bannière hello (voir ci-dessous). Vous devez configuration de l’appareil toomodify hello afin qu’il puisse les ressources adéquates toomeet hello configuration minimale requise. Vous pouvez ensuite redémarrer et connecter toohello appareil. Consultez toohello configuration minimale requise dans [étape 1 : Assurez-vous que système hôte de hello respecte les exigences de périphérique virtuel minimale](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Si vous êtes confronté à une autre erreur lors de la configuration initiale de hello à l’aide de l’interface utilisateur de web local hello, consultez toohello suivant du flux de travail :

* Exécutez les tests de diagnostic trop[résoudre les problèmes d’installation de l’interface utilisateur web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Générez un package de journaux et affichez les fichiers journaux](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Étapes suivantes
* [Configurer StorSimple Virtual Array comme un serveur de fichiers](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurer StorSimple Virtual Array comme un serveur iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
