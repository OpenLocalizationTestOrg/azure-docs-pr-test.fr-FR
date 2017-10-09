---
title: aaaAutomate Analytique de journal Azure traite avec Microsoft Flow
description: "Découvrez comment vous pouvez utiliser Microsoft Flow tooquickly automatiser des processus reproductibles à l’aide du connecteur d’Analytique des journaux Azure hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Automatiser les processus d’Analytique de journal avec le connecteur de hello pour Microsoft Flow
[Microsoft Flow](https://ms.flow.microsoft.com) vous permet de toocreate automatisée de flux de travail à l’aide des centaines d’actions pour une multitude de services. Sortie d’une action peut être utilisée en tant que tooanother d’entrée, ce qui permet une intégration toocreate entre différents services.  connecteur d’Analytique des journaux Azure Hello pour Microsoft Flow vous permettent aux workflows toobuild qui incluent des données récupérées par les recherches de journal dans le journal Analytique.

Par exemple, vous pouvez utiliser des données de journal Analytique Microsoft Flow toouse dans une notification par courrier électronique à partir d’Office 365, créer un bogue dans Visual Studio Team Services ou publier un message de marge.  Vous pouvez déclencher un flux de travail à l’aide d’un calendrier ou d’une action d’un service connecté, telle que la réception d’un e-mail ou d’un tweet.  


> [!NOTE]
> connecteur d’Analytique des journaux Azure Hello pour Microsoft Flow nécessite votre espace de travail mis à niveau de toobe toohello nouveau Analytique de journal langage de requête. Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).  

didacticiel Hello dans cet article vous montre comment toocreate un flux qui envoie automatiquement hello les résultats d’une recherche de journal Analytique de journal par courrier électronique, qu’un exemple de comment vous pouvez utiliser le journal Analytique dans Microsoft Flow. 


## <a name="step-1-create-a-flow"></a>Étape 1 : Créer un flux
1. Connectez-vous trop[Microsoft Flow](http://flow.microsoft.com), puis sélectionnez **flux Mes**.
2. Cliquez sur **+ Créer entièrement**.

## <a name="step-2-create-a-trigger-for-your-flow"></a>Étape 2 : Créer un déclencheur pour votre flux
1. Cliquez sur **Rechercher dans l’ensemble des connecteurs et des déclencheurs**.
2. Type **planification** dans la zone de recherche hello.
3. Sélectionnez **Planifier**, puis **Planification - Récurrence**.
4. Bonjour **fréquence** zone Sélectionnez **jour** et Bonjour **intervalle** , entrez **1**.<br><br>![Boîte de dialogue du déclencheur Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>Étape 3 : Ajouter une action Log Analytics
1. Cliquez sur **+ Nouvelle étape**, puis sur **Ajouter une action**.
2. Recherchez **Log Analytics**.
3. Cliquez sur **Azure Log Analytics – Exécuter la requête et visualiser les résultats**.<br><br>![Fenêtre d’exécution de la requête Log Analytics](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Étape 4 : Configurer l’action d’Analytique de journal hello

1. Spécifiez les détails de hello pour votre espace de travail, y compris hello abonnement ID, groupe de ressources et le nom de l’espace de travail.
2. Ajouter hello suivant Analytique de journal requête toohello **requête** fenêtre.  Ceci est un exemple de requête. Vous pouvez donc la remplacer par n’importe quelle autre requête retournant des données.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. Sélectionnez **HTML Table** pour hello **Type de graphique**.<br><br>![Action Log Analytics](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>Étape 5 : Configurer la messagerie de hello flux toosend

1. Cliquez sur **Nouvelle étape**, puis sur **+ Ajouter une action**.
2. Recherchez **Office 365 Outlook**.
3. Cliquez sur **Office 365 Outlook – Envoyer un message électronique**.<br><br>![Fenêtre de sélection d’Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)

4. Spécifiez l’adresse de messagerie hello d’un destinataire Bonjour **à** fenêtre et un objet de messagerie hello dans **sujet**.
5. Cliquez n’importe où dans hello **corps** boîte.  La fenêtre **Contenu dynamique** s’ouvre avec les valeurs des actions précédentes.  
6. Sélectionnez **Corps**.  Il s’agit de résultats hello de requête hello Bonjour action d’Analytique de journal.
6. Cliquez sur **Afficher les options avancées**.
7. Bonjour **HTML** boîte, sélectionnez **Oui**.<br><br>![Fenêtre de configuration d’e-mail Office 365](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>Étape 6 : Enregistrer et tester votre flux
1. Bonjour **nom de flux** zone, ajouter un nom pour votre flux, puis cliquez sur **créer un flux**.<br><br>![Enregistrer le flux](media/log-analytics-flow-tutorial/flow06.png)
2. flux de Hello est maintenant créé et s’exécute après un jour planification hello spécifiée. 
3. flux de hello tooimmediately test, cliquez sur **exécuter maintenant** , puis **exécuter flux**.<br><br>![Exécuter le flux](media/log-analytics-flow-tutorial/flow07.png)
3. Lorsque les flux hello est terminée, vérifiez les messages hello du destinataire hello que vous avez spécifié.  Vous devez avoir reçu un message électronique avec une similaire toohello suivant du corps :<br><br>![Exemple de message électronique](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur les [recherches dans les journaux avec Log Analytics](log-analytics-log-search-new.md).
- Découvrez [Microsoft Flow](https://ms.flow.microsoft.com).



