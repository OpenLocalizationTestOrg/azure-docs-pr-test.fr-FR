---
title: aaaProvision StorSimple Virtual Array dans Hyper-V | Documents Microsoft
description: "Ce deuxième didacticiel de déploiement de StorSimple Virtual Array implique la configuration d’un tableau virtuel dans Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Déploiement de StorSimple Virtual Array - Configuration dans Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel explique comment tooprovision un virtuel StorSimple tableau sur un système hôte exécutant Hyper-V sur Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. Cet article s’applique à déploiement toohello de StorSimple des réseaux virtuels dans le portail Azure et Microsoft Azure Government Cloud.

Vous devez tooprovision de privilèges d’administrateur et que vous configurez un groupe virtuel. le programme d’installation de configuration et initiale Hello peut prendre environ 10 minutes toocomplete.

## <a name="provisioning-prerequisites"></a>Configuration des composants requis
Vous trouverez ici hello conditions préalables tooprovision un tableau virtuel sur un système hôte exécutant Hyper-V sur Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Pourquoi le service du Gestionnaire de périphériques StorSimple
Avant de commencer, assurez-vous que :

* Vous avez effectué toutes les étapes de hello dans [portail hello de préparation pour StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).
* Vous avez téléchargé l’image du tableau virtuel hello pour Hyper-V à partir de hello portail Azure. Pour plus d’informations, consultez **étape 3 : image du tableau virtuel téléchargement hello** de [portail hello de préparation pour le guide de StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > Hello logiciel s’exécutant sur hello StorSimple Virtual Array ne peut être utilisé avec hello service du Gestionnaire de périphériques StorSimple.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Pourquoi StorSimple Virtual Array
Avant de déployer un tableau virtuel, assurez-vous que :

* Vous avez accès tooa hôte système exécutant Hyper-V sur Windows Server 2008 R2 ou version ultérieure que peut être utilisé tooa configurer un périphérique.
* système d’hôte Hello est en mesure de toodedicate hello suivant tooprovision de ressources de votre tableau virtuel :

  * Un minimum de 4 cœurs.
  * Au moins 8 Go de RAM. Si vous envisagez d’unité de stockage tooconfigure hello virtuelle en tant que serveur de fichiers, 8 Go prend en charge moins de 2 millions de fichiers. Vous avez besoin de 16 Go de RAM toosupport 2-4 millions de fichiers.
  * Une interface réseau.
  * Un disque virtuel de 500 Go pour les données.

### <a name="for-hello-network-in-hello-datacenter"></a>Pour le réseau hello dans le centre de données hello
Avant de commencer, examinez hello mise en réseau des exigences toodeploy un tableau virtuel StorSimple et configurer le réseau de centre de données hello en conséquence. Pour plus d’informations, consultez la [Configuration requise du réseau pour StorSimple Virtual Array](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Configuration étape par étape
tooprovision et connecter les groupe virtuel tooa, que vous devez hello tooperform comme suit :

1. Assurez-vous que le système hôte de hello dispose suffisamment toomeet hello minimale tableau virtuel besoins en ressources.
2. Configurez un tableau virtuel dans votre hyperviseur.
3. Démarrer le tableau de virtuel hello et obtenir l’adresse IP de hello.

Chacune de ces étapes est expliquée dans les sections suivantes de hello.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Étape 1 : Vérifiez que système hôte de hello répond aux exigences de la baie virtuelle minimale
toocreate un tableau virtuel, vous devez :

* rôle de Hello Hyper-V est installé sur Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 SP1.
* Microsoft Hyper-V Manager sur un client Microsoft Windows connecté toohello hôte.

Assurez-vous que hello matériel (système de l’hôte) sur lequel vous créez une unité de stockage virtuelle hello sous-jacent est hello en mesure de toodedicate suivant array virtuel tooyour de ressources :

* Un minimum de 4 cœurs.
* Au moins 8 Go de RAM. Si vous envisagez d’unité de stockage tooconfigure hello virtuelle en tant que serveur de fichiers, 8 Go prend en charge moins de 2 millions de fichiers. Vous avez besoin de 16 Go de RAM toosupport 2-4 millions de fichiers.
* Une interface réseau.
* Un disque virtuel de 500 Go pour les données système.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Étape 2 : Configurer un tableau virtuel dans l’hyperviseur
Effectuer hello suivant les étapes tooprovision un appareil dans votre hyperviseur.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision un tableau virtuel
1. Sur votre hôte Windows Server, copiez le disque local hello tableau virtuel image tooa. Vous avez téléchargé cette image (fichiers VHD ou VHDX) via hello portail Azure. Prenez note de l’emplacement hello où vous avez copié les images hello que vous utilisez cette image plus loin dans la procédure de hello.
2. Ouvrez le **Gestionnaire de serveur**. Dans hello coin supérieur droit, cliquez sur **outils** et sélectionnez **Gestionnaire Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Si vous exécutez Windows Server 2008 R2, ouvrez hello Gestionnaire Hyper-V. Dans le Gestionnaire de serveur, cliquez sur **Rôles > Hyper-V > Gestionnaire Hyper-V**.
3. Dans **Gestionnaire Hyper-V**, dans le volet d’étendue hello, avec le bouton droit de votre menu de contexte système nœud tooopen hello, puis cliquez sur **nouveau** > **Machine virtuelle**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. Sur hello **avant de commencer** page Hello l’Assistant Nouvel ordinateur virtuel, cliquez sur **suivant**.
5. Sur hello **spécifier le nom et l’emplacement** , fournissez un **nom** de votre tableau virtuel. Cliquez sur **Suivant**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. Sur hello **spécifier la génération** page, choisissez le type d’image de périphérique de hello, puis cliquez sur **suivant**. Cette page ne s’affiche pas si vous utilisez Windows Server 2008 R2.

   * Choisissez **Génération 2** si vous avez téléchargé une image .vhdx pour Windows Server 2012 ou version ultérieure.
   * Choisissez **Génération 1** si vous avez téléchargé une image .vhdx pour Windows Server 2008 R2 ou version ultérieure.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. Sur hello **affecter la mémoire** , spécifiez un **mémoire de démarrage** d’au moins **Mo 8192**, n’activez la mémoire dynamique, puis cliquez sur **suivant**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. Sur hello **configurer le réseau** page, spécifiez hello commutateur virtuel qui est connecté toohello Internet, puis sur **suivant**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. Sur hello **connecter un disque dur virtuel** choisissez **utiliser un disque dur virtuel existant**, spécifier l’emplacement de hello d’image du tableau virtuel hello (.vhdx ou .vhd), puis cliquez sur **suivant**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Hello de révision **Résumé** puis cliquez sur **Terminer** toocreate hello virtual machine.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. configuration minimale requise toomeet hello, vous devez 4 cœurs. les processeurs virtuels tooadd 4, sélectionnez votre système hôte Bonjour **Gestionnaire Hyper-V** fenêtre. Dans la droite hello sous la liste de hello **Machines virtuelles**, localisez l’ordinateur virtuel de hello vous venez de créer. Sélectionnez et cliquez sur le nom d’ordinateur hello et sélectionnez **paramètres**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. Sur hello **paramètres** page, dans le volet gauche du hello, cliquez sur **processeur**. Dans le volet droit du hello, définissez **nombre de processeurs virtuels** too4 (ou plus). Cliquez sur **Apply**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. configuration minimale requise toomeet hello, vous devez également tooadd un disque de données virtuel de 500 Go. Bonjour **paramètres** page :

    1. Dans le volet gauche de hello, sélectionnez **contrôleur SCSI**.
    2. Dans le volet droit de hello, sélectionnez **dur,** et cliquez sur **ajouter**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. Sur hello **disque dur** page, sélectionnez hello **disque dur virtuel** , puis cliquez sur **nouveau**. Hello **Assistant du nouveau disque dur virtuel** démarre.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. Sur hello **avant de commencer** page Hello virtuel Assistant nouveau disque dur, cliquez sur **suivant**.
16. Sur hello **page Choisir un Format de disque**, acceptez l’option par défaut hello **VHDX** format. Cliquez sur **Suivant**. Cet écran ne s’affiche pas si vous exécutez Windows Server 2008 R2.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. Sur hello **page Choisir un Type de disque**, définir le type de disque dur virtuel en tant que **expansion dynamique** (recommandé). **Taille fixe** disque fonctionnera, mais vous devrez peut-être toowait beaucoup de temps. Nous vous recommandons de ne pas utiliser hello **Differencing** option. Cliquez sur **Suivant**. Dans Windows Server 2012 R2 et Windows Server 2012, **expansion dynamique** est l’option par défaut de hello tandis que dans Windows Server 2008 R2, est par défaut de hello **une taille fixe**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. Sur hello **spécifier le nom et l’emplacement** , fournissez un **nom** ainsi que **emplacement** (vous pouvez parcourir tooone) pour le disque de données hello. Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. Sur hello **configurer un disque** page, l’option de sélection hello **créer un nouveau disque dur virtuel vide** et spécifier la taille de hello en tant que **500 Go** (ou plus). 500 Go est au minimum le hello, vous pouvez toujours configurer un disque plus volumineux. Notez que vous ne peut pas développer ou réduire disque hello configuré qu’une seule fois. Pour plus d’informations sur la taille de hello tooprovision de disque, consultez la section de dimensionnement de hello Bonjour [document de pratiques meilleures](storsimple-ova-best-practices.md). Cliquez sur **Suivant**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. Sur hello **Résumé** , examinez les détails de hello de votre disque de données virtuel, si vous satisfait, cliquez sur **Terminer** disque de hello toocreate. Hello Assistant se ferme et un disque dur virtuel est ajouté tooyour machine.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Retourner toohello **paramètres** page. Cliquez sur **OK** tooclose hello **paramètres** page et renvoyer la fenêtre du Gestionnaire de tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Étape 3 : Démarrer l’unité de stockage virtuelle hello et obtenir une adresse IP de hello
Effectuer hello suivant les étapes toostart votre tableau virtuel et se connecter tooit.

#### <a name="toostart-hello-virtual-array"></a>tableau de toostart hello virtuel
1. Démarrer le tableau de virtuel hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Une fois que l’appareil de hello est en cours d’exécution, sélectionnez hello appareil avec le bouton droit et cliquez sur Sélectionner **connexion**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Vous avez peut-être toowait 5 à 10 minutes pour toobe de périphérique hello prêt. Un message d’état s’affiche sur la progression de hello tooindicate hello console. Une fois les appareils hello sont prêt, passez trop**Action**. Appuyez sur `Ctrl + Alt + Delete` toolog dans le tableau de virtuel toohello. Hello utilisateur par défaut est *StorSimpleAdmin* et mot de passe hello *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire à la première ouverture de session hello. Vous êtes un mot de passe hello toochange demandées.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Entrez un mot de passe contenant au moins 8 caractères. Hello mot de passe doit satisfaire au moins 3 hors hello suivant les exigences de 4 : caractères majuscules, minuscules, numériques et spéciaux. Entrez à nouveau tooconfirm de mot de passe hello il. Vous êtes informé de que ce mot de passe hello a changé.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Une fois le mot de passe hello est modifié avec succès, unité de stockage virtuelle hello peut redémarrer. Attendez que hello périphérique toostart.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    console Windows PowerShell de Hello du périphérique de hello s’affiche avec une barre de progression.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Les étapes 6 à 8 s’appliquent uniquement lors de l’amorçage dans un environnement non DHCP. Si vous êtes dans un environnement DHCP, ignorez ces étapes et accédez toostep 9. Si vous avez démarré la configuration de votre appareil dans un environnement non-DHCP, vous verrez hello suivant l’écran.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Ensuite, configurez le réseau de hello.
7. Hello d’utilisation `Get-HcsIpAddress` commande des interfaces réseau de toolist hello activés sur votre tableau virtuel. Si votre appareil dispose d’une seule interface réseau activée, le nom affecté toothis interface de hello par défaut est `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Hello d’utilisation `Set-HcsIpAddress` réseau de hello tooconfigure applet de commande. Consultez hello l’exemple suivant :

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Après hello l’installation initiale est terminée et les appareils hello a démarré, vous verrez le texte de bannière du périphérique hello. Prenez note de l’adresse IP de hello et l’URL de hello affichés dans le dispositif hello toomanage hello bannière texte. Utilisez cette IP adresse tooconnect toohello interface utilisateur web de votre tableau virtuel et hello complète local et d’inscription.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Facultatif) Effectuez cette étape uniquement si vous déployez votre appareil dans hello gouvernement Cloud. Vous serez désormais activer le mode d’United States traitement Standard FIPS (Federal Information) hello sur votre appareil. norme de Hello FIPS 140 définit les algorithmes de chiffrement approuvés pour une utilisation par les systèmes d’ordinateur gouvernement fédéral nous pour une protection des données sensibles hello.

    1. mode FIPS hello tooenable, exécutez hello suivant l’applet de commande :

        `Enable-HcsFIPSMode`
    2. Redémarrer votre périphérique après avoir activé le mode FIPS hello afin que les validations de chiffrement hello prennent effet.

       > [!NOTE]
       > Vous pouvez activer ou désactiver le mode FIPS sur votre appareil. Appareil de hello en alternance entre le mode FIPS et non-FIPS n’est pas pris en charge.
       >
       >

Si votre appareil ne satisfait pas la configuration minimale requise de hello, vous consultez hello suivant d’erreur dans le texte de bannière hello (voir ci-dessous). Modifier la configuration de l’appareil hello afin que hello ordinateur dispose des ressources adéquates toomeet hello configuration minimale requise. Vous pouvez ensuite redémarrer et connecter toohello appareil. Consultez toohello configuration minimale requise dans [étape 1 : Assurez-vous que système hôte de hello respecte les exigences de tableau virtuel minimale](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Si vous êtes confronté à une autre erreur lors de la configuration initiale de hello à l’aide de l’interface utilisateur de web local hello, consultez toohello suivant du flux de travail :

* Exécutez les tests de diagnostic trop[résoudre les problèmes d’installation de l’interface utilisateur web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Générez un package de journaux et affichez les fichiers journaux](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Étapes suivantes
* [Configurer StorSimple Virtual Array comme un serveur de fichiers](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurer StorSimple Virtual Array comme un serveur iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
