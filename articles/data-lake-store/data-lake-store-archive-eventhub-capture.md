---
title: "aaaCapture des données à partir de concentrateurs d’événements dans Azure Data Lake Store | Documents Microsoft"
description: "Données de toocapture utilisation Azure Data Lake Store à partir des concentrateurs d’événements"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Données de toocapture utilisation Azure Data Lake Store à partir des concentrateurs d’événements

Découvrez comment toouse données toocapture de Azure Data Lake Store reçues par Azure Event Hubs.

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md).

*  **Un espace de noms Event Hubs**. Pour obtenir des instructions, consultez [Créer un espace de noms Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Assurez-vous que le compte Data Lake Store de hello et espace de noms de concentrateurs d’événements hello sont Bonjour même abonnement Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Affecter des autorisations tooEvent concentrateurs

Dans cette section, vous créez un dossier dans le compte de hello où vous souhaitez toocapture les données de hello de concentrateurs d’événements. Vous également affectez des autorisations tooEvent concentrateurs afin qu’il peut écrire des données dans un compte Data Lake Store. 

1. Ouvrez hello Data Lake Store compte sur lequel vous souhaitez toocapture les données à partir de concentrateurs d’événements, puis cliquez sur **Explorateur de données**.

    ![Explorateur de données Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorateur de données Data Lake Store")

2.  Cliquez sur **nouveau dossier** , puis entrez un nom pour le dossier dans lequel les données de salutation toocapture.

    ![Créer un dossier dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Créer un dossier dans Data Lake Store")

3. Affecter des autorisations au niveau de la racine de hello Hello Data Lake Store. 

    a. Cliquez sur **Explorateur de données**, sélectionnez racine hello hello compte Data Lake Store, puis cliquez sur **accès**.

    ![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Affecter des autorisations pour la racine du compte Data Lake Store")

    b. Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`. 

    ![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour la racine du compte Data Lake Store")
    
    Cliquez sur **Sélectionner**.

    c. Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**. Définissez **autorisations** trop**Execute**. Définissez **ajouter à** trop**ce dossier et tous les enfants**. Définissez **ajouter en tant que** trop**une entrée d’autorisation accès et une entrée d’autorisation par défaut**.

    ![Affecter des autorisations pour la racine du compte Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Affecter des autorisations pour la racine du compte Data Lake Store")

    Cliquez sur **OK**.

4. Affecter des autorisations pour le dossier hello sous le compte Data Lake Store où vous souhaitez que les données de toocapture.

    a. Cliquez sur **Explorateur de données**, sélectionnez le dossier de hello Bonjour compte Data Lake Store, puis cliquez sur **accès**.

    ![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Affecter des autorisations pour le dossier Data Lake Store")

    b. Sous **Accès**, cliquez sur **Ajouter**, cliquez sur **Sélectionner un utilisateur ou un groupe**, puis recherchez `Microsoft.EventHubs`. 

    ![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Affecter des autorisations pour le dossier Data Lake Store")
    
    Cliquez sur **Sélectionner**.

    c. Sous **Affecter des autorisations**, cliquez sur **Sélectionner des autorisations**. Définissez **autorisations** trop**lecture, écriture,** et **Execute**. Définissez **ajouter à** trop**ce dossier et tous les enfants**. Enfin, définissez **ajouter en tant que** trop**une entrée d’autorisation accès et une entrée d’autorisation par défaut**.

    ![Affecter des autorisations pour le dossier Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Affecter des autorisations pour le dossier Data Lake Store")
    
    Cliquez sur **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Configurer le service Event Hubs toocapture data tooData Lake Store

Dans cette section, vous allez créer un Event Hub dans un espace de noms Event Hubs. Vous configurez également hello concentrateur d’événements toocapture données tooan compte Azure Data Lake Store. Cette section part du principe que vous avez déjà créé un espace de noms Event Hubs.

2. À partir de hello **vue d’ensemble** volet de l’espace de noms hello concentrateurs d’événements, cliquez sur **+ concentrateur d’événements**.

    ![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Créer un Event Hub")

3. Fournissez suivant de hello valeurs tooconfigure toocapture des concentrateurs d’événements data Lake tooData Store.

    ![Créer un Event Hub](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Créer un Event Hub")

    a. Fournissez un nom pour hello concentrateur d’événements.
    
    b. Pour ce didacticiel, définissez **nombre de partitions** et **rétention des messages** toohello les valeurs par défaut.
    
    c. Définissez **Capture** trop**sur**. Ensemble hello **fenêtre de temps** (fréquence toocapture) et **taille de fenêtre** (toocapture de taille de données). 
    
    d. Pour **capturer le fournisseur**, sélectionnez **Azure Data Lake Store** et sélectionnez hello hello Data Lake Store que vous avez créé précédemment. Pour **le chemin d’accès de données Lake**, entrez le nom hello du dossier hello créé Bonjour compte Data Lake Store. Vous devez uniquement le dossier de toohello tooprovide hello chemin d’accès relatif.

    e. Laissez hello **formats de nom de fichier de capture exemple** toohello par défaut. Cette option détermine la structure de dossiers de hello est créé sous le dossier de capture hello.

    f. Cliquez sur **Créer**.

## <a name="test-hello-setup"></a>Programme d’installation de test hello

Vous pouvez maintenant tester la solution de hello en envoyant des données toohello concentrateur d’événements Azure. Suivez les instructions de hello à [envoyer des événements de concentrateurs d’événements tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Une fois que vous démarrez l’envoi de données de hello, consultez données hello dans Data Lake Store à l’aide de la structure de dossiers hello spécifié. Par exemple, vous voyez une structure de dossiers, comme indiqué dans hello suivant capture d’écran, dans votre Data Lake Store.

![Exemple de données EventHub dans Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemple de données EventHub dans Data Lake Store")

> [!NOTE]
> Même si vous n’avez pas les messages entrants dans les concentrateurs d’événements, les concentrateurs d’événements écrit des fichiers vides avec uniquement les en-têtes hello dans hello compte Data Lake Store. Hello fichiers sont écrits à hello même intervalle de temps que vous avez fourni lors de la création de concentrateurs d’événements hello.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Analyse des données dans Data Lake Store

Une fois les données de salutation Data Lake Store, vous pouvez exécuter des tâches analytiques tooprocess et faites vos données de hello. Consultez [USQL Avro exemple](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sur la façon de toodo ce à l’aide d’Analytique de LAC de données Azure.
  

## <a name="see-also"></a>Voir aussi
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Copier des données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
