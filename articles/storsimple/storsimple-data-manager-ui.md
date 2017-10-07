---
title: aaaMicrosoft Azure StorSimple Data Manager UI | Documents Microsoft
description: "Décrit comment toouse StorSimple Data Manager, repérez l’interface utilisateur (aperçu privé)"
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
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Gérer à l’aide du service de données de StorSimple Manager hello UI (aperçu privé)

Cet article explique comment vous pouvez utiliser hello transformation des données StorSimple Data Manager UI tooperform sur les données résidant sur les périphériques série StorSimple 8000 hello. Hello données transformées peuvent ensuite être consommées par d’autres services Azure comme Azure Media Services, Azure HDInsight, Azure Machine Learning et Azure Search. 


## <a name="use-storsimple-data-transformation"></a>Utiliser la transformation des données StorSimple

Hello Data StorSimple Manager est ressource hello dans lequel la Transformation de données peut être instanciée. Hello service de Transformation de données vous permet de déplacer des données à partir de votre tooblobs de périphérique StorSimple local dans le stockage Azure. Par conséquent, dans le flux de travail, vous devez les détails de hello toospecify sur vos données StorSimple hello et des appareils d’intérêt que vous souhaitez le compte de stockage toomove toohello.

### <a name="create-a-storsimple-data-manager-service"></a>Créer un service StorSimple Data Manager

Effectuer hello suivant les étapes toocreate un service de données de StorSimple Manager.

1. toocreate un service de données de StorSimple Manager, accédez trop[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Cliquez sur hello  **+**  icône et recherche pour le Gestionnaire de données StorSimple. Cliquez sur votre service StorSimple Data Manager, puis sur **Créer**.

3. Si votre abonnement est activé pour la création de ce service, vous consultez hello suivant du panneau.

    ![Créer une ressource StorSimple Data Manager](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Entrez les entrées hello et cliquez sur **créer**. Hello spécifié l’emplacement doit être hello qui héberge vos comptes de stockage et votre service StorSimple Manager. Actuellement, seules les États-Unis de l’Ouest et l’Europe de l’Ouest sont prises en charge. Par conséquent, votre service StorSimple Manager, service Manager de données et hello compte de stockage associé doit être dans des régions hello précédent pris en charge. Cela prend environ un service de hello toocreate minute.

### <a name="create-a-data-transformation-job-definition"></a>Créer une définition de travail de transformation de données

Dans un service de données de StorSimple Manager, vous devez toocreate une définition de tâche de transformation de données. Une définition de travail spécifie les détails de données hello qui vous intéressez le déplacement dans un compte de stockage dans le format natif hello. 

Effectuer hello suivant les étapes toocreate une nouvelle définition de tâche de transformation de données.

1.  Accédez à service toohello que vous avez créé. Cliquez sur **+ Définition du travail**.

    ![Cliquez sur +Définition du travail](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. nouveau panneau de définition de tâche Hello s’ouvre. Attribuez un nom à votre définition de travail, puis cliquez sur **Source**. Bonjour **configurer la source de données** panneau, spécifiez les détails de hello de votre appareil StorSimple, hello des données d’intérêt.

    ![Créer une définition de travail](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Dans la mesure où il s’agit d’un nouveau service Data Manager, aucun référentiel de données n’est configuré. tooadd votre StorSimple Manager en tant que référentiel de données, cliquez sur **ajouter un nouveau** dans hello dropdown de référentiel de données, puis cliquez sur **ajouter un référentiel de données**.

4. Choisissez **Manager pour la série StorSimple 8000** comme référentiel de hello tapez et entrez les propriétés hello de votre **StorSimple Manager**. Pourquoi **Id de ressource** champ, vous devez tooenter hello avant hello **:** dans la clé d’inscription de hello de votre StorSimple manager.

    ![Créer une source de données](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Une fois l’opération terminée, cliquez sur **OK**. Votre référentiel de données est enregistré, et cette instance StorSimple Manager peut être réutilisée dans d’autres définitions de travail, sans nouvelle saisie de ces paramètres. Il prend quelques secondes après avoir cliqué sur **OK** pour hello tooshow StorSimple Manager haut dans la liste déroulante de hello.

6.  Bonjour **configurer la source de données** panneau, entrez le nom de l’appareil hello et hello nom volume de vos données d’intérêt.

7.  Bonjour **filtre** sous-section, entrez le répertoire racine hello qui contient vos données d’intérêt (ce champ doit commencer par un `\`). Les filtres de fichiers s’ajoutent également ici.

8.  service de transformation de données Hello fonctionne sur les données de salutation toohello Azure sont transmies via des instantanés. Lors de l’exécution de cette tâche, vous pouvez choisir tootake une sauvegarde chaque fois que cette tâche est exécutée (toowork sur les données les plus récentes) ou toouse hello dernière sauvegarde existant dans le cloud de hello (si vous travaillez sur des données archivées).

    ![Nouveaux détails de la source de données](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Ensuite, les paramètres de cible de hello doivent toobe configuré. Il existe 2 types de cibles prises en charge : les comptes de stockage Azure et les comptes Azure Media Services. Choisissez les comptes de stockage tooput fichiers dans des objets BLOB dans ce compte. Choisissez le compte media services tooput fichiers en actifs dans ce compte. Là encore, nous devons tooadd un référentiel. Dans la liste déroulante de hello, sélectionnez **ajouter un nouveau** , puis **configurer les paramètres**.

    ![Créer un récepteur de données](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. Ici, vous pouvez sélectionner type hello du référentiel tooadd et hello autres paramètres associés au référentiel de hello. Dans les deux cas, une file d’attente de stockage est créé lors de la tâche de hello s’exécute. Cette file d’attente est renseignée avec des messages sur les objets blob transformés, au fur et à mesure de leur mise à disposition. nom de Hello de cette file d’attente est hello identique au nom de la définition de la tâche hello hello. Si vous sélectionnez **Media Services** en tant que type de référentiel hello, puis vous pouvez également entrer informations d’identification du compte de stockage dans lequel la file d’attente hello est créé.

    ![Détails sur le nouveau récepteur de données](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Après avoir ajouté un référentiel de données hello (qui prend quelques secondes), vous trouverez les référentiel hello dans la liste déroulante hello hello **nom du compte cible**.  Choisissez la cible hello dont vous avez besoin.

12. Cliquez sur **OK** toocreate définition de la tâche hello. Votre définition de travail est désormais configurée. Vous pouvez utiliser cette définition de tâche plusieurs fois via l’interface utilisateur de hello.

    ![Ajouter une définition de travail](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Exécuter la définition de la tâche hello

Chaque fois que vous avez besoin de toomove données StorSimple toohello compte de stockage que vous avez spécifié dans la définition de la tâche hello, vous devez tooinvoke il. Il existe une certaine flexibilité lors de la modification des paramètres de hello chaque fois que vous appelez le travail de hello. étapes de Hello sont les suivantes :

1. Sélectionnez votre service de données de StorSimple Manager et accédez trop**analyse**. Cliquez sur **Exécuter maintenant**.

    ![Déclencher la définition de travail](./media/storsimple-data-manager-ui/run-now.png)

2. Choisissez la définition de la tâche hello que vous souhaitez toorun. Cliquez sur **des paramètres d’exécution** toomodify tous les paramètres que vous pouvez toochange pour cet exécution du travail.

    ![Exécuter les paramètres de travail](./media/storsimple-data-manager-ui/run-settings.png)

3. Cliquez sur **OK** puis cliquez sur **exécuter** toolaunch votre travail. toomonitor cette tâche, l’accédez toohello **travaux** page votre gestionnaire de données de StorSimple.

    ![Liste et état des travaux](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. Dans toomonitoring Ajout Bonjour **travaux** panneau, vous pouvez également écouter sur file d’attente de stockage hello dans lequel un message est ajouté chaque fois qu’un fichier est déplacé à partir du compte de stockage StorSimple toohello.


## <a name="next-steps"></a>Étapes suivantes

[Utilisez des tâches de gestionnaire de données de StorSimple .NET SDK toolaunch](storsimple-data-manager-dotnet-jobs.md).
