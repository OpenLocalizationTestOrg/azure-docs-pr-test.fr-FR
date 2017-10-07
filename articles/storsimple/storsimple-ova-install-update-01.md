---
title: "mises à jour aaaInstall sur un tableau virtuel StorSimple | Documents Microsoft"
description: "Décrit comment tooapply de l’interface utilisateur web toouse hello StorSimple Virtual Array met à jour à l’aide de la méthode de portail et le correctif logiciel hello"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Installation de mises à jour sur votre instance StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Cet article décrit les mises à jour de hello étapes tooinstall requis sur votre tableau virtuel StorSimple via l’interface utilisateur de web locale hello et hello portail Azure classic. Vous devez tookeep des mises à jour ou correctifs logiciels tooapply votre tableau virtuel StorSimple mis à jour. 

N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil. Étant donné que hello StorSimple Virtual Array est un périphérique de nœud unique, l’interruption des e/s en cours d’exécution et indisponibilité de votre appareil. 

Avant d’appliquer une mise à jour, nous recommandons de prendre de volumes de hello ou partages en mode hors connexion sur hello hébergent tout d’abord et puis hello appareil. Vous réduisez ainsi toute possibilité d’altération des données.

> [!IMPORTANT]
> Si vous exécutez la mise à jour 0.1 ou les versions des logiciels GA, vous devez utiliser la méthode de correctif logiciel de hello via la mise à jour l’interface utilisateur tooinstall 0,3 pour hello web local. Si vous exécutez la mise à jour 0,2, nous vous recommandons d’installer les mises à jour hello via hello portail Azure classic.
> 
> 

## <a name="use-hello-local-web-ui"></a>Utiliser l’interface utilisateur de web locale hello
Il existe deux étapes lors de l’utilisation de l’interface utilisateur de web local hello :

* Télécharger la mise à jour hello ou un correctif logiciel de hello
* Installer la mise à jour hello ou un correctif logiciel de hello

### <a name="download-hello-update-or-hello-hotfix"></a>Télécharger la mise à jour hello ou un correctif logiciel de hello
Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>correctif de mise à jour ou hello de hello toodownload
1. Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.
3. Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload. Entrez **3182061** pour Update 0.3, puis cliquez sur **Rechercher**.
   
    Hello correctif liste s’affiche, par exemple, **mise à jour de tableau virtuel StorSimple 0,3**.
   
    ![Rechercher dans le catalogue](./media/storsimple-ova-install-update-01/download1.png)
4. Cliquez sur **Add**. mise à jour Hello est ajouté toohello du panier d’achat.
5. Cliquez sur **Afficher le panier**.
6. Cliquez sur **Télécharger**. Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear. Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier portant le même nom qu’une mise à jour hello de hello. dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.
7. Ouvrez hello copié le dossier, vous devriez voir un fichier de Package autonome Microsoft `WindowsTH-KB3011067-x64`. Ce fichier est mise à jour de tooinstall utilisé hello ou un correctif logiciel.

### <a name="install-hello-update-or-hello-hotfix"></a>Installer la mise à jour hello ou un correctif logiciel de hello
Installation de mise à jour ou le correctif logiciel toohello préalable, assurez-vous que vous avez mise à jour hello ou hello correctif téléchargé localement sur votre ordinateur hôte ou accessible via un partage réseau. 

Utiliser les mises à jour tooinstall cette méthode sur un périphérique exécutant GA ou mettre à jour les versions des logiciels 0,1. Cette procédure est inférieure à 2 minutes toocomplete. Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>correctif de mise à jour ou hello de hello tooinstall
1. Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **mise à jour logicielle**.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update1m.png)
2. Dans **chemin d’accès du fichier de mise à jour**, entrez le nom du fichier de mise à jour hello hello ou hello correctif logiciel. Vous pouvez également parcourir le fichier d’installation de mise à jour ou le correctif logiciel toohello si placé sur un partage réseau. Cliquez sur **Apply**.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update2m.png)
3. Un avertissement s’affiche. Étant donné ce est un périphérique à nœud unique, après la mise à jour hello, redémarrage du périphérique hello et il est temps d’arrêt. Cliquez sur une icône de coche hello.
   
   ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update3m.png)
4. mise à jour Hello démarre. Une fois que l’appareil de hello est correctement mise à jour, il redémarre. Hello d’interface utilisateur locale n’est pas accessible dans cette durée.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update5m.png)
5. Après le redémarrage de hello est terminée, vous accédez toohello **connectez-vous** page. tooverify logiciel du périphérique hello a mis à jour, dans le site web local hello l’interface utilisateur, consultez trop**Maintenance** > **mise à jour logicielle**. version du logiciel Hello affiché doit être **10.0.0.0.0.10288.0** pour la mise à jour 0.3.
   
   > [!NOTE]
   > Nous signaler les versions des logiciels hello d’une manière légèrement différente dans l’interface utilisateur de web locale hello et hello portail Azure classic. Hello, par exemple, les rapports de l’interface utilisateur web locale **10.0.0.0.0.10288** et hello des rapports de portail classiques Azure **10.0.10288.0** pour hello même version. 
   > 
   > 
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Utilisez hello portail Azure classic
Si vous exécutez la mise à jour 0,2, nous vous recommandons d’installer mises à jour via le portail Azure classic de hello. procédure de portail Hello requiert hello utilisateur tooscan, télécharger, puis installer les mises à jour hello. Cette procédure prend environ 7 minutes toocomplete. Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Hello après l’installation est terminée (comme indiqué par l’état du travail à 100 %), accédez trop**appareils > Maintenance > mises à jour logicielles**. version du logiciel Hello affiché doit être 10.0.10288.0.

![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

