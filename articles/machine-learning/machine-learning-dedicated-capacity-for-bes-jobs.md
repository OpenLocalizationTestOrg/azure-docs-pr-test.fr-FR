---
title: "aaaDedicated capacité pour les tâches d’exécution Service Machine Learning lot | Documents Microsoft"
description: "Vue d’ensemble du service Azure Batch pour les travaux Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Service Azure Batch pour les travaux Machine Learning

Le traitement du Pool de traitement par lots d’apprentissage machine prévoit hello Azure Machine Learning Batch Execution Service gérée par le client de mise à l’échelle. Lot classique pour l’apprentissage de traitement s’effectue dans une architecture mutualisée, le numéro de hello limites de travaux simultanés, vous pouvez soumettre et travaux est en attente sur une base in-first-out. Cette incertitude signifie que vous ne pouvez pas prédire précisément à quel moment votre travail sera exécuté.

Le traitement par lots Pool vous permet de pools toocreate sur lequel vous pouvez soumettre des traitements par lots. Contrôle de taille hello du pool de hello et toowhich pool hello travail est envoyé. Votre travail BES s’exécute dans son propre traitement espace fournissant des performances de traitement prévisibles et le hello capacité toocreate pools de ressources qui correspondant la charge de traitement toohello que vous envoyez.

## <a name="how-toouse-batch-pool-processing"></a>Comment le traitement du Pool de traitement par lots toouse

Configuration du Pool de traitement par lot n’est pas actuellement disponible via hello portail Azure. toouse Pool de traitement par lots de traitement, vous devez :

-   Appelez CSS toocreate un compte de Pool de traitement par lots et obtenir une URL de Service du Pool et une clé d’autorisation
-   créer un service web et un plan de facturation basés sur un nouveau Resource Manager.

toocreate votre compte, appelez le Support technique et Service clientèle Microsoft et fournir votre ID d’abonnement. CSS fonctionneront avec vous toodetermine hello capacité appropriée pour votre scénario. CSS configure ensuite votre compte avec un nombre maximal de pools, vous pouvez créer et nombre maximal de machines virtuelles (VM) que vous pouvez placer dans chaque pool de hello hello. Une fois votre compte configuré, vous recevez l’URL de service du pool et une clé d’autorisation.

Après la création de votre compte, vous utiliser hello URL du Service de Pool et l’autorisation tooperform clé pool opérations de gestion sur votre Pool de traitement par lots.

![Architecture de service du pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Pour créer des pools par l’appel d’opération de créer un Pool de hello d’URL de service du pool hello que tooyou CSS fourni. Lorsque vous créez un pool, spécifiez le nombre hello de machines virtuelles et les URL de hello de hello swagger.json d’un nouveau gestionnaire de ressources en fonction de service web Machine Learning. Ce service web est fourni association de facturation tooestablish hello. Hello service du Pool de traitement par lots utilise le pool de hello hello swagger.json tooassociate avec un plan de facturation. Vous pouvez exécuter n’importe quel BES service web, les deux nouveau gestionnaire de ressources en fonction et classique, cliquez sur le pool de hello.

Vous pouvez utiliser n’importe quel service web d’en fonction du nouveau gestionnaire de ressources, mais sachez que facturation hello pour les travaux de hello sont facturées par rapport au plan de facturation hello associé au service. Vous souhaiterez toocreate un service web et la facturation nouveau plan spécialement pour l’exécution des travaux du Pool de traitement par lots.

Pour plus d’informations sur la création de services web, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Une fois que vous avez créé un pool, vous envoyez hello BES à l’aide de la tâche hello URL des demandes de lot pour le service web de hello. Vous pouvez choisir toosubmit il tooa pool ou tooclassic le traitement par lots. toosubmit un tooBatch Pool de traitement, vous ajoutez hello suivant le corps de la demande du travail envoi de paramètre toohello :

« AzureBatchPoolId »:« &lt;ID du pool&gt; »

Si vous n’ajoutez pas de paramètre hello, travail de hello est exécuté dans un environnement de processus de lot classique hello. Si le pool de hello a des ressources disponibles, hello commence immédiatement. Si le pool de hello n’a pas de libérer des ressources, votre travail est en file d’attente jusqu'à ce qu’une ressource est disponible.

Si vous trouvez que vous atteignez régulièrement vos pools de capacité hello, et que vous devez augmenter sa capacité, vous pouvez appeler CSS et manipuler un tooincrease représentatif de vos quotas.

Exemple de demande :

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Considérations relatives à l’utilisation du traitement par pool Batch

Pool de traitement par lot est un service facturable toujours actif et qu’elle vous tooassociate il avec un gestionnaire de ressources en fonction de plan de facturation. Vous êtes facturé uniquement pour nombre de hello d’heures de calcul pool de hello est en cours d’exécution ; quel que soit le nombre de hello des tâches exécutées au cours de ce pool de temps. Si vous créez un pool, vous êtes facturé pour les heures de calcul hello de chaque ordinateur virtuel dans le pool de hello jusqu'à ce que le pool de hello est supprimé, même si aucune tâche de traitement par lots n’est en cours d’exécution dans le pool de hello. Facturation des machines virtuelles de hello démarre lorsqu’ils ont terminé la mise en service et s’arrête lorsqu’ils ont été supprimés. Vous pouvez utiliser un des plans hello trouvés sur hello [page de tarification de Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).

Exemple de facturation :

Si vous créez un pool Batch comprenant 2 machines virtuelles et le supprimez après 24 heures, votre plan de facturation est débité de 48 heures de calcul quel que soit le nombre de travaux exécutés pendant cette période.

Si vous créez un pool Batch comportant 4 machines virtuelles et le supprimez après 12 heures, votre plan de facturation est également débité de 48 heures de calcul.

Nous vous recommandons d’interroger les hello travail état toodetermine lors de l’achèvement des travaux. Lorsque tous vos travaux terminés, appelez hello redimensionnement d’un Pool opération tooset hello nombre de machines virtuelles dans hello pool toozero. Si vous êtes court sur des ressources et vous devez toocreate un nouveau pool, par exemple toobill par rapport à un autre plan de facturation, vous pouvez supprimer le pool de hello à la place lorsque tous vos travaux de l’exécution est terminée.


| **Utilisez le traitement par pool Batch si**    | **Utilisez le traitement par lots classique si**  |
|---|---|
|Vous devez toorun un grand nombre de travaux<br>Ou<br/>Vous devez tooknow vos tâches s’exécutent immédiatement<br/>Ou<br/>Vous avez besoin d’un débit garanti. Par exemple, vous devez toorun un nombre de travaux dans un laps de temps donné et devez tooscale votre toomeet de ressources de calcul des besoins.    | Vous exécutez quelques travaux<br/>and<br/> Vous n’avez pas besoin hello travaux toorun immédiatement |
