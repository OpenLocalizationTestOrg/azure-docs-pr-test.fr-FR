---
title: "vue d’ensemble du Gestionnaire de données Azure StorSimple aaaMicrosoft | Documents Microsoft"
description: "Fournit une vue d’ensemble de hello transmet au service StorSimple Data Manager (version préliminaire privée)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Vue d’ensemble de StorSimple Data Manager (version préliminaire privée)

## <a name="overview"></a>Vue d'ensemble

Microsoft Azure StorSimple est une solution de stockage cloud hybride adresses hello complexités de couramment associées à des partages de fichiers de données non structurées. StorSimple utilise le stockage cloud comme une extension de hello solution locale et reconnaît automatiquement les données sur un stockage local hello et de stockage cloud. Protection des données, d’intégrer local et les instantanés cloud, hello inutile une immense infrastructure de stockage. Archivage et récupération d’urgence est également transparente avec cloud hello agissant comme un emplacement hors site.

Hello data transformation services que nous vous présentons dans ce document, permet un accès tooseamlessly vous hello StorSimple des données dans le cloud de hello. Ce service fournit des données de tooextract d’API à partir de StorSimple et présenter tooother Azure services dans des formats qui peuvent être facilement consommées. formats de Hello pris en charge dans cette version d’évaluation sont des objets BLOB Windows Azure et des éléments multimédias Azure Media Services. Cette transformation permet de vous tooeasily câble des services tels que les données toooperate Azure Media Services, Azure HDInsight, Azure Machine Learning et Azure Search sur l’appareil local de série StorSimple 8000.

Le diagramme de blocs général ci-dessous illustre cela.

![Diagramme général](./media//storsimple-data-manager-overview/high-level-diagram.png)

Ce document explique comment s’inscrire à la version préliminaire privée de ce service. Elle explique également comment vous pouvez utiliser ce service toowrite les applications qui utilisent des données de StorSimple et d’autres services Azure dans le cloud de hello.

## <a name="sign-up-for-data-manager-preview"></a>Inscription à la version préliminaire de Data Manager
Avant de vous inscrivez pour le service de gestionnaire de données hello, passez en revue hello suivant des conditions préalables.

### <a name="prerequisites"></a>Composants requis

Cet exercice suppose que vous disposiez :
* d’un abonnement Azure actif ;
* accès tooa inscrit l’appareil de série StorSimple 8000
* tous les hello clés associées aux appareils de hello StorSimple 8000.

### <a name="sign-up"></a>Inscription

Hello Data StorSimple Manager est en aperçu privé. Effectuez hello suivant toosign étapes pour une version préliminaire limitée de ce service :

1.  Se connecter à hello portail Azure avec l’extension de données de StorSimple Manager hello à : [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Utilisez toolog de vos informations d’identification Azure dans.

2.  Cliquez sur hello  **+**  icône toocreate un service. Cliquez sur **stockage** puis cliquez sur **voir tous les** dans le panneau hello qui s’ouvre.

    ![Rechercher l’icône de StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Icône du Gestionnaire de données de StorSimple hello s’affiche.

    ![Sélectionner l’icône de StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Cliquez sur l’icône de StorSimple Data Manager, puis sur **Créer**. Choisir l’abonnement hello que vous souhaitez tooenable pour la version préliminaire limitée de hello, puis sur **Inscrivez-moi !**

    ![Inscription](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Envoie une demande tooonboard vous. Nous vous intégrerons dès que possible. Une fois votre abonnement activé, vous pouvez créer un service StorSimple Data Manager.

6. tooeasily accéder au service de données de StorSimple Manager hello, cliquez sur hello étoile toopin il tooyour favoris.

    ![Accéder à StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Étapes suivantes

[Utilisez l’interface utilisateur de gestionnaire de données StorSimple tootransform vos données](storsimple-data-manager-ui.md).
