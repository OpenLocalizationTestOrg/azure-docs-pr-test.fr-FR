---
title: "aaaInstall mise à jour 0,6 sur StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Virtual Array web UI tooapply mises à jour à l’aide de hello méthode Azure de portail et le correctif logiciel"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a>Installation d’Update 0.6 sur StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Cet article décrit hello étapes tooinstall obligatoire la mise à jour 0,6 sur votre tableau virtuel StorSimple via l’interface utilisateur de web locale hello et hello portail Azure. Vous appliquez tookeep des mises à jour ou correctifs logiciels hello votre tableau virtuel StorSimple mis à jour.

Avant d’appliquer une mise à jour, nous recommandons de prendre de volumes de hello ou partages en mode hors connexion sur hello hébergent tout d’abord et puis hello appareil. Vous réduisez ainsi toute possibilité d’altération des données. Une fois hello volumes ou partages sont hors connexion, vous devez également prendre un manuel de sauvegarde de l’appareil de hello.

> [!IMPORTANT]
> - Mise à jour 0,6 correspond trop**10.0.10293.0** version du logiciel sur votre appareil. Pour plus d’informations sur les nouveautés de cette mise à jour, accédez trop[notes de publication pour la mise à jour 0,6](storsimple-virtual-array-update-06-release-notes.md).
>
> - Si vous exécutez la mise à jour 0,2 ou une version ultérieure, nous recommandons que vous installez des mises à jour de la hello via hello portail Azure. Si vous exécutez la mise à jour 0.1 ou les versions des logiciels GA, vous devez utiliser la méthode de correctif logiciel hello via tooinstall de l’interface utilisateur web locale hello mise à jour 0,6.
>
> - N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil. Étant donné que hello StorSimple Virtual Array est un périphérique de nœud unique, l’interruption des e/s en cours d’exécution et indisponibilité de votre appareil.

## <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure

Si l’exécution de Update 0,2 et versions ultérieures, nous vous recommandons d’installer via hello portail Azure, les mises à jour. procédure de portail Hello requiert hello utilisateur tooscan, télécharger, puis installer les mises à jour hello. Cette procédure prend environ 7 minutes toocomplete. Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Après avoir hello l’installation est terminée, accédez tooyour service du Gestionnaire de périphériques StorSimple. Sélectionnez **périphériques** puis sélectionnez et cliquez sur périphérique hello vous venez de mettre à jour. Accédez trop**Paramètres > Gérer > mises à jour de l’appareil**. version du logiciel Hello affiché doit être **10.0.10293.0**.

## <a name="use-hello-local-web-ui"></a>Utiliser l’interface utilisateur de web locale hello

Il existe deux étapes lors de l’utilisation de l’interface utilisateur de web local hello :

* Télécharger la mise à jour hello ou un correctif logiciel de hello
* Installer la mise à jour hello ou un correctif logiciel de hello

### <a name="download-hello-update-or-hello-hotfix"></a>Télécharger la mise à jour hello ou un correctif logiciel de hello

Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>correctif de mise à jour ou hello de hello toodownload

1. Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Si vous utilisez hello catalogue Microsoft Update pour hello première fois sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.

3. Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload. Entrez **4023268** pour Update 0.6, puis cliquez sur **Rechercher**.
   
    Hello correctif liste s’affiche, par exemple, **mise à jour de tableau virtuel StorSimple 0,6**.
   
    ![Rechercher dans le catalogue](./media/storsimple-virtual-array-install-update-06/download1.png)

4. Cliquez sur **Télécharger**.

5. Vous devez voir cinq toodownload de fichiers. Téléchargez tous ces tooa dossier des fichiers. dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.

6. Ouvrez le dossier hello dans lequel se trouvent les fichiers hello.
    ![Fichiers dans le package de hello](./media/storsimple-virtual-array-install-update-06/update06folder.png)

    Vous voyez :
    -  Un fichier de package autonome Microsoft `WindowsTH-KB3011067-x64`. Ce fichier est un logiciel de périphérique de hello tooupdate utilisé.
    - Un fichier de package d’agent de surveillance de Genève `GenevaMonitoringAgentPackageInstaller`. Ce fichier est utilisé tooupdate hello analyse et Diagnostics (MDS) agent du service. Double-cliquez sur le fichier cab de hello. Un _.msi_ s’affiche. Fichier de sélection hello, avec le bouton droit, puis **extraire** fichier de hello. Vous utilisez hello _.msi_ l’agent de fichiers tooupdate hello.

        ![Extraire le fichier de mise à jour de l’agent de MDS](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > Il est inutile l’agent MDS tooupdate hello si vous exécutez la mise à jour de StorSimple 0,5 (0.0.10293.0).

    - Trois fichiers qui contiennent des mises à jour de sécurité Windows critiques (`windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64` et `windows8.1-kb4019213-x64`).


### <a name="install-hello-update-or-hello-hotfix"></a>Installer la mise à jour hello ou un correctif logiciel de hello

Installation de mise à jour ou le correctif logiciel toohello préalable, assurez-vous que vous avez mise à jour hello ou hello correctif téléchargé localement sur votre ordinateur hôte ou accessible via un partage réseau.

Utiliser les mises à jour tooinstall cette méthode sur un périphérique exécutant GA ou mettre à jour les versions des logiciels 0,1. Cette procédure prend environ 12 minutes toocomplete. Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>correctif de mise à jour ou hello de hello tooinstall

1. Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **mise à jour logicielle**. Prenez note de la version du logiciel hello qui vous sont en cours d’exécution. Si vous exécutez **10.0.10290.0**, vous n’avez pas besoin d’un agent MDS hello tooupdate à l’étape 6.
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. Dans **chemin d’accès du fichier de mise à jour**, entrez le nom du fichier de mise à jour hello hello ou hello correctif logiciel. Vous pouvez également parcourir le fichier d’installation de mise à jour ou le correctif logiciel toohello si placé sur un partage réseau. Cliquez sur **Apply**.
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Un avertissement s’affiche. Donné hello tableau virtuel est un périphérique à nœud unique, une fois la mise à jour hello, redémarrage du périphérique hello et il est temps d’arrêt. Cliquez sur une icône de coche hello.
   
   ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. mise à jour Hello démarre. Une fois que l’appareil de hello est correctement mise à jour, il redémarre. Hello d’interface utilisateur locale n’est pas accessible dans cette durée.
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Après le redémarrage de hello est terminée, vous accédez toohello **connectez-vous** page. tooverify logiciel du périphérique hello a mis à jour, dans le site web local hello l’interface utilisateur, consultez trop**Maintenance** > **mise à jour logicielle**. version du logiciel Hello affiché doit être **10.0.0.0.0.10293** pour la mise à jour 0,6.
   
   > [!NOTE]
   > Nous signaler les versions des logiciels hello d’une manière légèrement différente dans l’interface utilisateur de web locale hello et hello portail Azure. Hello, par exemple, les rapports de l’interface utilisateur web locale **10.0.0.0.0.10293** et hello rapports portails Azure **10.0.10293.0** pour hello même version.
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. Ignorez cette étape si vous exécutiez StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) avant d’appliquer cette mise à jour. Note de la version du logiciel hello ont été apportées à l’étape 1 avant de commencer tooupdate. Si vous exécutiez Update 0.5, votre agent MDS est déjà à jour.

    Si vous exécutez une version de logiciel préalable tooUpdate 0,5, étape suivante de hello pour vous est l’agent de tooupdate hello MDS. Bonjour **mise à jour logicielle** page, aller toohello **chemin d’accès du fichier de mise à jour** et parcourir toohello `GenevaMonitoringAgentPackageInstaller.msi` fichier. Répétez les étapes 2 à 4. Après le redémarrage de l’unité de stockage virtuelle hello, connectez-vous à l’interface utilisateur de web locale hello.

7. Répétez l’étape 2 à 4 de la sécurité tooinstall hello Windows résout à l’aide de fichiers `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, et `windows8.1-kb4019213-x64`. unité de stockage virtuelle Hello redémarre après chaque installation, et vous devez toosign dans l’interface utilisateur de web locale hello.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

