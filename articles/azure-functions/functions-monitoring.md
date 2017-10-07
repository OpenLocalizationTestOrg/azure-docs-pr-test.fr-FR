---
title: aaaMonitoring les fonctions Azure | Documents Microsoft
description: "Découvrez comment toomonitor vos fonctions de Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Surveillance d’Azure Functions

## <a name="overview"></a>Vue d'ensemble 


Hello **moniteur** onglet pour chaque fonction vous permet de tooreview chaque exécution d’une fonction.

![Onglet Surveiller d’Azure Functions](./media/functions-monitoring/monitor-tab.png) 

Une exécution permet de durée hello tooreview, les données d’entrée, les erreurs et les fichiers journaux associés. Cela est utile pour le débogage et l’optimisation de vos fonctions.


> [!IMPORTANT]
> Lorsque vous utilisez hello [consommation plan d’hébergement](functions-overview.md#pricing) pour les fonctions d’Azure, hello **analyse** vignette dans le panneau de vue d’ensemble des applications de la fonction hello n’affiche pas les données. Il s’agit, car la plate-forme de hello s’adapter dynamiquement et gère les instances de calcul pour vous, ces mesures ne sont pas significatives sur un plan de la consommation. toomonitor hello l’utilisation de vos applications de fonction, vous devez utiliser à la place des conseils de hello dans cet article.
> 
> Hello suivant capture d’écran montre un exemple :
> 
> ![La surveillance sur le panneau de ressources principal hello](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Surveillance en temps réel

L’analyse en temps réel est disponible en cliquant sur **flux d’événements en direct**, comme indiqué ci-dessous. 

![Option de flux d’événements pour l’onglet de surveillance hello de Live](./media/functions-monitoring/monitor-tab-live-event-stream.png)

flux d’événements en direct de Hello est représentés graphiquement dans un nouvel onglet de navigateur, comme indiqué ci-dessous. 

![Exemple de flux de données d’événement en direct](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Il existe un problème connu qui peut provoquer votre toobe toofail de données remplie. Si vous rencontrez cela, vous devrez peut-être les flux d’événements live tooclose hello navigateur onglet contenant hello, puis cliquez sur **flux d’événements live** tooallow nouveau il tooproperly remplir vos données de flux de données d’événement. 

flux d’événements en direct de Hello sera graphique hello suit les statistiques de votre fonction :

* Exécutions démarrées par seconde
* Exécutions réussies par seconde
* Exécutions ayant échoué par seconde
* Temps d’exécution moyen en millisecondes.

Ces statistiques sont en temps réel, mais hello réel de graphiques de données de l’exécution de hello peut avoir environ dix secondes de latence.






## <a name="monitoring-log-files-from-a-command-line"></a>Analyse des fichiers journaux à partir d’une ligne de commande


Vous pouvez diffuser la session de ligne de commande de tooa de fichiers journaux sur une station de travail à l’aide de hello Azure Interface de ligne de commande (CLI) ou PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Analyse des fichiers du journal application fonction hello CLI d’Azure

tooget démarré, [installer hello CLI d’Azure](../cli-install-nodejs.md)

Connectez-vous à votre compte Azure utilisant hello commande ou l’un des hello autres options traitées, [connecter tooAzure de hello CLI d’Azure](../xplat-cli-connect.md).

    azure login

Mode de gestion de Service Azure CLI (ASM) tooenable de commande de suivante de hello utilisation :.

    azure config mode asm

Si vous avez plusieurs abonnements, utilisez hello suivant toolist de commandes vos abonnements et le jeu hello abonnement toohello abonnement actuel qui contient votre application de la fonction.

    azure account list
    azure account set <subscriptionNameOrId>

Hello commande suivante est diffusés journaux hello de votre ligne de commande toohello fonction application :

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Analyse des fichiers journaux Function App avec PowerShell

tooget démarré, [installer et configurer Azure PowerShell](/powershell/azure/overview).

Ajoutez votre compte Azure en exécutant hello de commande suivante :

    PS C:\> Add-AzureAccount

Si vous avez plusieurs abonnements, vous pouvez les répertorier par nom avec hello suivant commande toosee si hello correct de l’abonnement est hello actuellement sélectionné en fonction de `IsCurrent` propriété :

    PS C:\> Get-AzureSubscription

Si vous devez tooset hello abonnement actif toohello un contenant votre application de la fonction, utilisez hello de commande suivante :

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Session PowerShell flux hello journaux tooyour avec hello de commande suivante :

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Pour plus d’informations, consultez trop[Comment : diffuser des journaux pour les applications web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources :

* [Test d’une fonction](functions-test-a-function.md)
* [Mettre à l’échelle une fonction](functions-scale.md)

