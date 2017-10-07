---
title: "aaaAdd données d’entrée des tâches de flux de données Analytique tooyour | Documents Microsoft"
description: "Découvrez comment toohook d’un tooyour de source de données Analytique de flux de travail en diffusion en continu de données d’entrée à partir des données de concentrateurs d’événements ou une référence à partir du stockage d’objets BLOB."
keywords: "entrée de données, données de diffusion en continu"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a>Ajout d’une diffusion en continu données d’entrée ou de référence données tooa flux Analytique tâche
Découvrez comment toohook d’un tooyour de source de données Analytique de flux de travail en diffusion en continu de données d’entrée à partir des données de concentrateurs d’événements ou une référence à partir du stockage d’objets Blob.

Les tâches de flux de données Analytique Azure peuvent être connecté tooone données d’entrée ou plus d’informations, dont chacune définit une source de données existante du tooan de connexion. Comme les données sont envoyées de source de données toothat, il est consommé par la tâche de flux de données Analytique hello et traité en temps réel en tant que la diffusion en continu de données. Flux de données Analytique a integration de première classe avec [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) et [le stockage Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) au sein et en dehors de l’abonnement de la tâche hello.

Cet article est une étape Bonjour [Analytique de flux de données d’apprentissage](/documentation/learning-paths/stream-analytics/).

## <a name="data-input-streaming-data-and-reference-data"></a>Entrée de données : données de référence et données de diffusion en continu
Il existe deux types d’entrées dans Stream Analytics : les flux de données et les données de référence.

* **Flux de données**: tâches de flux de données Analytique doivent inclure au moins un données flux d’entrée toobe consommé et transformés par la tâche de hello. Le stockage d’objets blob Azure et Azure Event Hubs sont pris en charge en tant que sources d’entrée de flux de données. Les concentrateurs d’événements Azure sont toocollect utilisés les flux d’événements de périphériques connectés, les services et applications. Le stockage d'objets blob Azure peut être utilisé comme source d'entrée pour la réception de données en bloc en tant que flux.  
* **Données de référence**: Stream Analytics prend en charge un deuxième type d'entrée auxiliaire appelé données de référence.  En tant que toodata exécutée en mouvement, ces données sont statiques ou de ralentissement de la modification.  Il est généralement utilisé pour effectuer des recherches et les corrélations avec des flux de données toocreate un jeu de données plus riche.  Stockage d’objets Blob Azure est actuellement hello pris en charge uniquement la source d’entrée pour les données de référence.  

tooadd une tâche de flux de données Analytique tooyour d’entrée :

1. Bonjour portail Azure, cliquez sur **entrées** puis cliquez sur **ajouter une entrée** dans votre tâche de flux de données Analytique.
   
    ![Portail Azure Classic - ajouter une entrée.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    Bonjour portail Azure, cliquez sur hello **entrées** vignette dans votre tâche de flux de données Analytique.  
   
    ![Portail Azure - ajouter une entrée de données.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. Spécifiez le type hello d’entrée de hello : soit **flux de données** ou **données de référence**.
   
    ![Ajouter les données correctes hello d’entrée, en continu ou référence](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Ajouter les données correctes hello d’entrée, en continu ou référence](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. Si vous créez une entrée de flux de données, spécifiez le type de source de hello pour l’entrée de hello.  Cet étape peut être ignorée lors de la création de Données de référence car seul le stockage d'objets Blob est pris en charge à ce stade.
   
    ![Ajouter une entrée de données de diffusion en continu](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Ajouter une entrée de données de diffusion en continu](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. Fournissez un nom convivial pour cette entrée dans hello zone Alias d’entrée.  Ce nom sera utilisé dans la requête de votre travail plus tard dans l’entrée de toohello toorefer.
   
    Renseignez les autres hello hello connexion requise propriétés tooconnect tooyour de source de données. Ces champs varient selon le type d'entrée et le type de source, et sont définis en détail [ici](stream-analytics-create-a-job.md).  
   
    ![Ajouter une entrée de données de hub d’événements](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. Spécifiez les paramètres de sérialisation hello pour les données d’entrée hello :
   
   * toomake que vos requêtes fonctionnent comme de hello vous le souhaitez, spécifier hello **Format de sérialisation d’événements** des données entrantes.  Les formats de sérialisation pris en charge sont JSON, CSV et Avro.
   * Vérifiez que hello **codage** pour les données de salutation.  UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.
     
     ![Paramètres de sérialisation des données pour l’entrée de données hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Paramètres de sérialisation des données pour l’entrée de données hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. À l’issue de la création d’entrée de hello, flux de données Analytique vérifiera qu’il peut se connecter source d’entrée de toohello.  Vous pouvez afficher l’état hello Hello opération de tester la connexion dans le hub de Notification hello.
   
    ![Tester la connexion de hello de diffusion en continu des données d’entrée](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Tester la connexion de hello de diffusion en continu des données d’entrée](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a>Obtenir de l'aide sur les entrées de données de diffusion en continu
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

