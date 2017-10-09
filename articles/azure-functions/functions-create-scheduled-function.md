---
title: "aaaCreate une fonction qui s’exécute sur une planification dans Azure | Documents Microsoft"
description: "Découvrez comment toocreate une fonction dans Azure s’exécute selon une planification que vous définissez."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Créez une fonction dans Azure, qui est déclenchée par un minuteur

Découvrez comment toouse Azure fonctions toocreate une fonction qui s’exécute sur une planification que vous définissez.

![Créer l’application de la fonction Bonjour portail Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

+ Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Création d’une application Azure Function

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function App créée avec succès.](./media/functions-create-first-azure-function/function-app-create-success.png)

Ensuite, créez une fonction dans hello une nouvelle application de fonction.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Créer une fonction déclenchée par un minuteur

1. Développez votre application de la fonction et cliquez sur hello  **+**  bouton ensuite trop**fonctions**. S’il s’agit de hello première fonction dans votre application de la fonction, sélectionnez **fonction personnalisée**. Cela affiche le jeu complet de hello des modèles de fonction.

    ![Page de démarrage rapide de fonctions Bonjour portail Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Sélectionnez hello **TimerTrigger** modèle pour le langage de votre choix. Utilisez ensuite les paramètres de hello comme spécifié dans la table de hello :

    ![Créer une fonction de minuteur déclenché Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Paramètre | Valeur suggérée | Description |
    |---|---|---|
    | **Nommer votre fonction** | TimerTriggerCSharp1 | Définit le nom hello de votre fonction de minuteur déclenché. |
    | **[Planification](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Un champ de six [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui planifie votre toorun fonction toutes les minutes. |

2. Cliquez sur **Créer**. Une fonction est créée dans le langage que vous avez choisi et s’exécute chaque minute.

3. Vérifier l’exécution en consultant les informations de traçage écrites toohello journaux.

    ![Fonctions visionneuse du journal Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Maintenant, vous pouvez modifier la planification de la fonction hello afin qu’elle s’exécute moins souvent, par exemple une fois par heure. 

## <a name="update-hello-timer-schedule"></a>Planification de mise à jour hello du minuteur

1. Développez votre fonction et cliquez sur **Intégrer**. Il s’agit où vous définissez l’entrée et de sortie liaisons de votre fonction et également définissez la planification de hello. 

2. Entrez une nouvelle valeur de **Planification** de `0 0 */1 * * *`, puis cliquez sur **Enregistrer**.  

![Fonctions mettre à jour la planification du minuteur Bonjour portail Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Vous disposez maintenant d’une fonction qui s’exécute toutes les heures. 

## <a name="clean-up-resources"></a>Supprimer des ressources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous avez créé une fonction qui s’exécute selon une planification.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Pour en savoir plus sur les déclencheurs de minuteur, consultez la page [Planifier l’exécution de code avec Azure Functions](functions-bindings-timer.md).