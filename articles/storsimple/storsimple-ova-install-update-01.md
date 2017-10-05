---
title: "Installation de mises à jour sur une instance StorSimple Virtual Array | Microsoft Docs"
description: "Décrit comment utiliser l’interface utilisateur web de StorSimple Virtual Array pour installer des mises à jour à l’aide du portail et de la méthode des correctifs logiciels"
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
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Installation de mises à jour sur votre instance StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Cet article décrit les étapes requises pour installer des mises à jour sur votre instance StorSimple Virtual Array à l’aide de l’interface utilisateur web locale et du Portail Azure Classic. Pour maintenir votre instance StorSimple Virtual Array à jour, vous devez appliquer des mises à jour ou des correctifs logiciels. 

N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil. Étant donné que StorSimple Virtual Array est un appareil à nœud unique, les E/S en cours seront interrompues et votre appareil subira des temps d’arrêt. 

Avant d’appliquer une mise à jour, nous vous recommandons de mettre les volumes ou les partages hors connexion sur l’ordinateur hôte puis sur l’appareil. Vous réduisez ainsi toute possibilité d’altération des données.

> [!IMPORTANT]
> Si vous utilisez Update 0.1 ou les versions logicielles GA, vous devez appliquer la méthode de correctif logiciel par le biais de l’interface utilisateur web locale pour installer Update 0.3. Si vous utilisez Update 0.2, nous vous recommandons d’installer les mises à jour au moyen du Portail Azure Classic.
> 
> 

## <a name="use-the-local-web-ui"></a>Utilisation de l’interface utilisateur web locale
La procédure de mise à jour à l’aide de l’interface utilisateur web locale se déroule en deux étapes :

* Téléchargement de la mise à jour ou du correctif
* Installation de la mise à jour ou du correctif

### <a name="download-the-update-or-the-hotfix"></a>Téléchargement de la mise à jour ou du correctif
Procédez comme suit pour télécharger la mise à jour logicielle à partir du Catalogue Microsoft Update.

#### <a name="to-download-the-update-or-the-hotfix"></a>Pour téléchargement la mise à jour ou le correctif
1. Démarrez Internet Explorer et accédez à [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Si vous utilisez le catalogue Microsoft Update pour la première fois sur cet ordinateur, cliquez sur **Installer** lorsque vous êtes invité à installer le module complémentaire Catalogue Microsoft Update.
3. Dans la zone de recherche du Catalogue Microsoft Update, entrez le numéro KB (Base de connaissances) du correctif que vous souhaitez télécharger. Entrez **3182061** pour Update 0.3, puis cliquez sur **Rechercher**.
   
    La liste des correctifs s’affiche, par exemple **StorSimple Virtual Array Update 0.3**.
   
    ![Rechercher dans le catalogue](./media/storsimple-ova-install-update-01/download1.png)
4. Cliquez sur **Add**. La mise à jour est ajoutée au panier.
5. Cliquez sur **Afficher le panier**.
6. Cliquez sur **Télécharger**. Spécifiez ou **recherchez** l’emplacement local où vous voulez effectuer les téléchargements. Les mises à jour sont téléchargées à l’emplacement spécifié et placées dans un sous-dossier portant le même nom que la mise à jour. Ce dossier peut également être copié sur un partage réseau accessible à partir de l’appareil.
7. Ouvrez le dossier copié ; vous devriez voir un fichier de package autonome de mise à jour Microsoft `WindowsTH-KB3011067-x64`. Ce fichier est utilisé pour installer la mise à jour ou le correctif logiciel.

### <a name="install-the-update-or-the-hotfix"></a>Installation de la mise à jour ou du correctif
Avant l'installation de la mise à jour ou du correctif, vérifiez que la mise à jour ou le correctif est téléchargé(e) localement sur votre ordinateur hôte ou accessible via un partage réseau. 

Cette méthode permet d’installer les mises à jour sur un appareil exécutant les versions logicielles GA ou Update 0.1. Cette procédure prend moins de 2 minutes. Effectuez les opérations suivantes pour installer la mise à jour ou le correctif logiciel.

#### <a name="to-install-the-update-or-the-hotfix"></a>Pour installer la mise à jour ou le correctif
1. Dans l’interface utilisateur web locale, accédez à **Maintenance** > **Mise à jour logicielle**.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update1m.png)
2. Dans le **chemin d’accès au fichier de mise à jour**, entrez le nom du fichier de mise à jour ou de correctif. Vous pouvez également accéder au fichier d'installation de la mise à jour ou du correctif si celui-ci est placé sur un partage réseau. Cliquez sur **Appliquer**.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update2m.png)
3. Un avertissement s’affiche. Puisqu’il s’agit d’un appareil à nœud unique, l’application de la mise à jour entraîne le redémarrage de l’appareil et provoque un temps d’arrêt. Cliquez sur l’icône en forme de coche.
   
   ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update3m.png)
4. La mise à jour démarre. Une fois l’appareil correctement mis à jour, il est redémarré. L’interface utilisateur locale n’est pas accessible pendant cet intervalle.
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update5m.png)
5. Une fois le redémarrage effectué, vous êtes redirigé vers la page **Se connecter** . Pour vérifier que le logiciel de l’appareil a été mis à jour, accédez à **Maintenance** > **Mise à jour logicielle** dans l’interface utilisateur web locale. La version du logiciel doit être **10.0.0.0.0.10288.0** pour Update 0.3.
   
   > [!NOTE]
   > L’affichage des versions logicielles diffère légèrement entre l’interface utilisateur web locale et le portail Azure Classic. Par exemple, la même version est signalée par **10.0.0.0.0.10288** dans l’interface utilisateur web locale et par **10.0.10288.0** sur le Portail Azure Classic. 
   > 
   > 
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a>Utilisation du portail Azure Classic
Si vous utilisez Update 0.2, nous vous recommandons d’installer les mises à jour par le biais du Portail Azure Classic. La procédure du portail oblige l’utilisateur à rechercher et télécharger les mises à jour avant de les installer. Cette procédure prend environ sept minutes. Effectuez les opérations suivantes pour installer la mise à jour ou le correctif logiciel.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Une fois l’installation terminée (lorsque l’état du travail atteint 100 %), accédez à **Appareils > Maintenance > Mises à jour logicielles**. La version du logiciel doit être 10.0.10288.0.

![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

