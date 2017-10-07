---
title: "aaaStream des données à partir de l’Analytique des flux de données dans Data Lake Store | Documents Microsoft"
description: "Utiliser des données de toostream Analytique de flux de données Azure dans Azure Data Lake Store"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Diffuser des données à partir d’un objet blob Azure Storage dans Data Lake Store à l’aide d’Azure Stream Analytics
Dans cet article, vous allez apprendre comment toouse Azure Data Lake stocker comme sortie pour un travail d’Analytique de flux de données Azure. Cet article décrit un scénario simple qui lit les données d’un objet blob de stockage Azure (entrée) et les écritures hello tooData de data Lake Store (sortie).

> [!NOTE]
> À ce stade, la création et la configuration de Data Lake Store génère pour les flux de données Analytique est pris en charge uniquement dans hello [portail classique Azure](https://manage.windowsazure.com). Par conséquent, certaines parties de ce didacticiel utilise hello portail classique Azure.
>
>

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Compte Stockage Azure**. Vous allez utiliser un conteneur d’objets blob à partir de ces données tooinput de compte pour une tâche de flux de données Analytique. Pour ce didacticiel, vous possédez un compte de stockage nommé **storageforasa** et un conteneur dans le compte de hello appelé **storageforasacontainer**. Une fois que vous avez créé le conteneur de hello, téléchargez un tooit de fichier de données exemple. 
  
* **Compte Azure Data Lake Store**. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md). Imaginons que vous ayez un compte Data Lake Store nommé **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Créer un objet blob Stream Analytics
Pour commencer, vous allez créez une tâche Stream Analytics qui inclut une source d’entrée et une destination de sortie. Pour ce didacticiel, source de hello est un conteneur d’objets blob Azure et destination de hello Data Lake Store.

1. Ouverture de session toohello [Azure Portal](https://portal.azure.com).

2. Dans le volet gauche de hello, cliquez sur **des tâches de flux de données Analytique**, puis cliquez sur **ajouter**.

    ![Création d’un travail Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Création d’un travail Stream Analytics")

    > [!NOTE]
    > Vérifiez que vous créez un travail Bonjour même région que le compte de stockage hello ou occasionnent des frais supplémentaires de déplacement des données entre les régions.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Créer une entrée d’objet Blob pour le travail de hello

1. Page de hello ouvert pour la tâche de flux de données Analytique hello, hello volet de gauche, cliquez sur hello **entrées** onglet, puis cliquez sur **ajouter**.

    ![Ajouter un travail d’entrée tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "d’ajouter un travail d’entrée tooyour")

2. Sur hello **nouvelle entrée** panneau, fournir hello valeurs suivantes.

    ![Ajouter un travail d’entrée tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "d’ajouter un travail d’entrée tooyour")

    * Pour **alias d’entrée**, entrez un nom unique pour l’entrée de tâche hello.
    * Pour **Type de source**, sélectionnez **Flux de données**.
    * Pour **Source**, sélectionnez **Stockage d’objets blob**.
    * Pour **Abonnement**, sélectionnez **Utiliser l'objet blob de stockage de l'abonnement actuel**.
    * Pour **compte de stockage**, sélectionnez le compte de stockage hello que vous avez créé dans le cadre des conditions préalables de hello. 
    * Pour **conteneur**, sélectionnez conteneur hello que vous avez créé dans hello sélectionné compte de stockage.
    * Pour **Format de sérialisation de l’événement**, sélectionnez **CSV**.
    * Pour **Délimiteur**, sélectionnez **tabulation**.
    * Pour **Encodage**, sélectionnez **UTF-8**.

    Cliquez sur **Créer**. portail de Hello maintenant ajoute l’entrée de hello et teste hello connexion tooit.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Créez une sortie Data Lake Store pour le travail de hello

1. Page hello pour la tâche de flux de données Analytique hello, cliquez sur hello **sorties** onglet, puis cliquez sur **ajouter**.

    ![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.1.png "d’ajouter un travail tooyour de sortie")

2. Sur hello **nouvelle sortie** panneau, fournir hello valeurs suivantes.

    ![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.2.png "d’ajouter un travail tooyour de sortie")

    * Pour **alias de sortie**, saisissez un un nom unique pour la sortie de tâche hello. Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis Data Lake Store.
    * Pour **Récepteur**, sélectionnez **Data Lake Store**.
    * Vous serez invité à tooauthorize accéder au compte tooData Lake Store. Cliquez sur **Autoriser**.

3. Sur hello **nouvelle sortie** lames, continuer hello tooprovide valeurs suivantes.

    ![Ajouter un travail de tooyour sortie](./media/data-lake-store-stream-analytics/create.output.3.png "d’ajouter un travail tooyour de sortie")

    * Pour **nom de compte**, sélectionnez compte de Data Lake Store hello créé déjà où vous souhaitez toobe de sortie de tâche hello envoyé à.
    * Pour **motif de préfixe de chemin d’accès**, entrez un toowrite de chemin d’accès du fichier vos fichiers au sein de hello spécifié compte Data Lake Store.
    * Pour **format de Date**, si vous avez utilisé un jeton de date dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés.
    * Pour **format d’heure**, si vous avez utilisé un jeton de temps dans le chemin d’accès du préfixe hello, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés.
    * Pour **Format de sérialisation de l’événement**, sélectionnez **CSV**.
    * Pour **Délimiteur**, sélectionnez **tabulation**.
    * Pour **Encodage**, sélectionnez **UTF-8**.
    
    Cliquez sur **Créer**. portail de Hello maintenant ajoute la sortie de hello et teste hello connexion tooit.
    
## <a name="run-hello-stream-analytics-job"></a>Exécuter la tâche de flux de données Analytique hello

1. toorun une tâche de flux de données Analytique, vous devez exécuter une requête à partir de hello **requête** onglet. Pour ce didacticiel, vous pouvez exécuter l’exemple de requête hello en remplaçant des espaces réservés de hello avec hello travail alias d’entrée et de sortie, comme indiqué dans la capture d’écran hello ci-dessous.

    ![Exécutez une requête](./media/data-lake-store-stream-analytics/run.query.png "Exécuter une requête")

2. Cliquez sur **enregistrer** de haut hello d’écran hello, puis de hello **vue d’ensemble** , cliquez sur **Démarrer**. Dans la boîte de dialogue hello, sélectionnez **heure personnalisé**, puis définissez hello date et heure actuelles.

    ![Définir l’heure du travail](./media/data-lake-store-stream-analytics/run.query.2.png "Définir l’heure du travail")

    Cliquez sur **Démarrer** tâche hello de toostart. Il peut prendre le travail hello toostart tooa deux minutes.

3. données de salutation tootrigger hello travail toopick à partir de l’objet blob de hello, copiez un conteneur d’objets blob toohello fichier exemple données. Vous pouvez obtenir un exemple de fichier de données à partir de hello [référentiel Git de LAC de données Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Pour ce didacticiel, nous allons copier hello fichier **vehicle1_09142014.csv**. Vous pouvez utiliser différents clients, tels que [Azure Storage Explorer](http://storageexplorer.com/), conteneur d’objets blob tooa tooupload données.

4. À partir de hello **vue d’ensemble** sous l’onglet sous **analyse**, voir la façon dont les données de hello ont été traitées.

    ![Surveiller la tâche](./media/data-lake-store-stream-analytics/run.query.3.png "Surveiller la tâche")

5. Enfin, vous pouvez vérifier que les données de sortie de tâche hello soient disponibles dans le compte Data Lake Store de hello. 

    ![Vérifier la sortie](./media/data-lake-store-stream-analytics/run.query.4.png "Vérifier la sortie")

    Dans le volet de l’Explorateur de données hello, notez que hello sortie le chemin d’accès du dossier tooa écrit comme spécifié dans hello Data Lake Store les paramètres de sortie (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Voir aussi
* [Créer un toouse du cluster HDInsight Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
