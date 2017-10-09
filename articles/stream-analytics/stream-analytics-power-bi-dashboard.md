---
title: tableau de bord BI aaaPower sur Azure flux Analytique | Documents Microsoft
description: "Utiliser une en temps réel en continu Power BI du tableau de bord toogather business intelligence et analyser les données de volume élevé d’une tâche de flux de données Analytique."
keywords: "tableau de bord d’analyse, tableau de bord en temps réel"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics et Power BI : tableau de bord d’analyse en temps réel pour les données de streaming
Analytique de flux de données Azure vous permet de parti tootake de hello des outils d’analyse décisionnelle, [Microsoft Power BI](https://powerbi.com/). Dans cet article, vous allez découvrir comment créer des outils d’analyse décisionnelle en utilisant Power BI comme sortie pour vos travaux Azure Stream Analytics. Vous apprendrez également comment toocreate et utiliser un tableau de bord en temps réel.

Cet article reprend à partir de hello flux Analytique [la détection des fraudes en temps réel](stream-analytics-real-time-fraud-detection.md) didacticiel. Il s’appuie sur les flux de travail hello créé dans ce didacticiel et ajoute une sortie afin que vous pouvez visualiser les appels téléphoniques frauduleux qui sont détectés par une tâche Analytique de diffusion en continu de Power BI. 

Vous pouvez visionner [une vidéo](https://www.youtube.com/watch?v=SGUpT-a99MA) illustrant ce scénario.


## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous avez hello suivantes :

* Un compte Azure.
* Un compte pour Power BI. Vous pouvez utiliser un compte professionnel ou un compte scolaire.
* Une version complète de hello [la détection des fraudes en temps réel](stream-analytics-real-time-fraud-detection.md) didacticiel. didacticiel de Hello inclut une application qui génère des métadonnées de l’appel de téléphone fictifs. Didacticiel de hello, vous créez un hub d’événements et d’envoyez hello concentrateur d’événements d’appel téléphonique données toohello de diffusion en continu. Vous écrivez une requête qui détecte les appels frauduleux (appels de hello même nombre à hello même moment dans différents emplacements). 


## <a name="add-power-bi-output"></a>Ajouter une sortie Power BI
Dans le didacticiel de détection de fraude en temps réel hello, hello est affiché tooAzure stockage d’objets Blob. Dans cette section, vous ajoutez une sortie qui envoie des informations tooPower BI.

1. Bonjour portail Azure, ouvrez tâche Analytique de diffusion en continu hello que vous avez créé précédemment. Si vous avez utilisé le nom suggéré de hello, hello est nommée `sa_frauddetection_job_demo`.

2. Sélectionnez hello **sorties** zone au milieu de hello de tableau de bord projet hello, puis sélectionner **+ ajouter**.

3. Pour **Alias de sortie**, entrez `CallStream-PowerBI`. Vous pouvez utiliser un autre nom. Si vous le faites, prenez note de celui-ci, car vous devez les nom hello plus tard. 

4. Dans **Récepteur**, sélectionnez **Power BI**.

   ![Créer une sortie pour Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Cliquez sur **Autoriser**.

    Une fenêtre s’ouvre dans laquelle vous pouvez indiquer vos informations d’identification Azure pour un compte professionnel ou scolaire. 

    ![Entrez les informations d’identification pour l’accès tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Entrez vos informations d’identification. N’oubliez pas ensuite, lorsque vous entrez vos informations d’identification, vous êtes également en train de tooaccess de travail autorisation toohello Analytique de diffusion en continu votre zone Power BI.

7. Lorsque vous êtes renvoyé toohello **nouvelle sortie** panneau, entrez hello informations suivantes :

    * **Espace de travail de groupe**: sélectionnez un espace de travail dans votre locataire Power BI où vous souhaitez toocreate hello dataset.
    * **Nom du jeu de données** : entrez `sa-dataset`. Vous pouvez utiliser un autre nom. Le cas échéant, prenez-en note pour l’utiliser ultérieurement.
    * **Nom de la table** : entrez `fraudulent-calls`. Actuellement, une sortie Power BI des travaux Stream Analytics ne peut avoir qu’une table dans un jeu de données.

    ![Espace de travail PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Si Power BI dispose d’un jeu de données et la table qui a hello mêmes noms que hello celles que vous spécifiez dans la tâche de flux de données Analytique hello, hello des groupes existants est remplacé.
    > Nous vous recommandons de ne pas créer explicitement ce jeu de données et cette table dans votre compte Power BI. Ils sont créés automatiquement lorsque vous lancez votre tâche de flux de données Analytique et hello programmée de sortie pompage dans Power BI. Si votre requête de travail ne renvoie aucun résultat, table et hello dataset ne sont pas créés.
    >

8. Cliquez sur **Créer**.

jeu de données Hello est créée avec hello suivant les paramètres :

* **defaultRetentionPolicy : BasicFIFO** : données FIFO avec un maximum de 200 000 lignes.
* **defaultMode : pushStreaming**: hello le jeu de données prend en charge la diffusion en continu des vignettes et traditionnels basée sur l’état des éléments visuels (aussi appelé) push).

Pour le moment, vous ne pouvez pas créer de jeux de données avec d’autres indicateurs.

Pour plus d’informations sur les jeux de données Power BI, consultez hello [API REST Power BI](https://msdn.microsoft.com/library/mt203562.aspx) référence.


## <a name="write-hello-query"></a>Écrire des requêtes de hello

1. Fermer hello **sorties** panneau et le panneau de tâche toohello retour.

2. Cliquez sur hello **requête** boîte. 

3. Entrez hello suivant la requête. Cette requête est toohello jointure réflexive requête similaire que vous avez créé dans le didacticiel de détection des fraudes hello. Bonjour différence est que cette requête envoie toohello des résultats de la nouvelle sortie que vous avez créé (`CallStream-PowerBI`). 

    >[!NOTE]
    >Si vous n’avez pas nommé hello entrée `CallStream` dans le didacticiel de détection des fraudes hello, remplacez par votre nom de `CallStream` Bonjour **FROM** et **joindre** clauses de requête de hello.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Cliquez sur **Enregistrer**.


## <a name="test-hello-query"></a>Tester la requête hello
Cette étape est facultative, mais recommandée. 

1. Si l’application de TelcoStreaming hello n’est pas en cours d’exécution, démarrez-le en procédant comme suit :

    * Ouvrez une fenêtre de commandes.
    * Atteindre le dossier toohello où hello telcogenerator.exe et les fichiers modifiés telcodatagen.exe.config sont.
    * Exécutez hello de commande suivante :

            telcodatagen.exe 1000 .2 2

2. Bonjour **requête** panneau, cliquez sur toohello suivant de points hello `CallStream` d’entrée, puis sélectionnez **les exemples de données à partir de l’entrée**.

3. Spécifiez que vous souhaitez une valeur de trois minutes de données, puis cliquez sur **OK**. Patientez jusqu'à ce que vous êtes averti que les données de salutation ont été échantillonnées.

4. Cliquez sur **Test** et vérifiez que vous obtenez des résultats.


## <a name="run-hello-job"></a>Exécuter la tâche de hello

1. Assurez-vous que cette application de TelcoStreaming hello est en cours d’exécution.

2. Fermer hello **requête** panneau.

3. Dans le panneau de tâche hello, cliquez sur **Démarrer**.

    ![Démarrer la tâche de flux de données Analytique hello](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

Votre tâche Analytique de diffusion en continu commence la recherche d’appels frauduleuses dans les flux entrants hello. travail de Hello crée hello le jeu de données et de table dans Power BI et commence à envoyer des données sur toothem d’appels frauduleux hello.


## <a name="create-hello-dashboard-in-power-bi"></a>Créer un tableau de bord hello dans Power BI

1. Accédez trop[Powerbi.com](https://powerbi.com) et connectez-vous avec votre compte professionnel ou scolaire. Si la requête de traitement de flux de données Analytique hello génère des résultats, vous consultez que votre jeu de données est déjà créée :

    ![Jeu de données de diffusion en continu dans Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. Dans votre espace de travail, cliquez sur **+&nbsp;Créer**.

    ![bouton créer de Hello dans l’espace de travail Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Créez un tableau de bord et nommez-le `Fraudulent Calls`.

    ![Créer un tableau de bord et lui donner un nom dans l’espace de travail Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. En haut de hello de fenêtre hello, cliquez sur **ajouter une vignette**, sélectionnez **données de STREAMING personnalisées**, puis cliquez sur **suivant**.

    ![Jeu de données de streaming personnalisé](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. Sous **VOS JEUX DE DONNÉES**, sélectionnez votre jeu de données, puis cliquez sur **Suivant**.

    ![Votre jeu de données de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. Sous **Type de visualisation**, sélectionnez **carte**, puis dans hello **champs** liste, sélectionnez **fraudulentcalls**.

    ![Détails de la visualisation de la nouvelle vignette](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Cliquez sur **Suivant**.

8. Renseignez les détails de la vignette, par exemple un titre et un sous-titre.

    ![Titre et sous-titre de la nouvelle vignette](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Cliquez sur **Apply**.

    Nous avons à présent un compteur de fraudes.

    ![Compteur de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Suivez hello étapes tooadd à nouveau une vignette (à partir de l’étape 4). Cette fois-ci, hello suivant :

    * Si vous obtenez trop**Type de visualisation**, sélectionnez **graphique en courbes**. 
    * Ajoutez un axe, puis sélectionnez **windowend**. 
    * Ajoutez une valeur, puis sélectionnez **fraudulentcalls**.
    * Pour **toodisplay de fenêtre de temps**, sélectionnez hello les 10 dernières minutes.

    ![Créer une vignette pour le graphique en courbes](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Cliquez sur **Suivant**, ajoutez un titre et un sous-titre, puis cliquez sur **Appliquer**.

    tableau de bord Power BI Hello permet à présent deux vues de données sur les appels frauduleux détectée Bonjour de diffusion en continu de données.

    ![Tableau de bord Power BI complété affichant deux vignettes pour les appels frauduleux](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>En savoir plus sur Power BI

Ce didacticiel montre comment toocreate seulement certains types de visualisations pour un jeu de données. Power BI peut vous aider à créer d’autres outils d’analyse décisionnelle clients pour votre organisation. Pour plus d’informations, consultez hello suivant des ressources :

* Pour un autre exemple d’un tableau de bord Power BI, regardez hello [prise en main de Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vidéo.
* Pour plus d’informations sur la configuration Analytique de diffusion en continu de la tâche tooPower de sortie BI et à l’aide de groupes Power BI, passez en revue les hello [Power BI](stream-analytics-define-outputs.md#power-bi) section Hello [génère des flux de données Analytique](stream-analytics-define-outputs.md) l’article. 
* Pour plus d’informations sur l’utilisation de Power BI en général, consultez [Tableaux de bord dans Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>En savoir plus sur les limites et les meilleures pratiques
Actuellement, Power BI peut être appelé environ une fois par seconde. Les éléments visuels de streaming prennent en charge des paquets de 15 Ko. En outre, l’échec de diffusion en continu des éléments visuels (mais push continue toowork). En raison de ces limitations, Power BI se prête plus naturellement toocases où Analytique de flux de données Azure procède à une réduction significative des données de charge. Nous vous recommandons d’utiliser une fenêtre bascule ou saut fenêtre tooensure que push de données est au plus un push par seconde, et que votre requête arrive au sein des exigences de débit hello.

Vous pouvez utiliser hello suivant équation toocompute hello valeur toogive votre fenêtre en secondes :

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Par exemple :

* Vous disposez de 1 000 appareils qui envoient des données à des intervalles d’une seconde.
* Vous utilisez hello Power BI Pro référence (SKU) qui prend en charge 1 000 000 lignes par heure.
* Vous souhaitez durée hello toopublish moyenne des données par périphérique tooPower BI.

Par conséquent, les équations hello devient :

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

Avec cette configuration, vous pouvez modifier les éléments suivants toohello de requête d’origine hello :

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Renouveler une autorisation
Si un mot de passe hello a changé depuis la création ou de dernière authentification de votre travail, vous devez tooreauthenticate votre compte Power BI. Si l’authentification multifacteur Azure est configurée sur votre client Azure Active Directory (Azure AD), vous devez également toorenew d’autorisation de Power BI toutes les deux semaines. Si vous ne renouvelez pas, vous pouvez constater les symptômes, par exemple l’absence de sortie de la tâche ou un `Authenticate user error` dans les journaux des opérations de hello.

De même, si un travail démarre après que hello jeton a expiré, une erreur se produit et hello travail échoue. tooresolve ce problème, arrêtez tâche hello qui s’exécute et accédez tooyour Power BI de sortie. perte de données tooavoid, sélectionnez hello **renouveler l’autorisation** lier, puis redémarrez votre travail à partir de hello **heure du dernier arrêt**.

Après l’actualisation de l’autorisation de hello avec Power BI, une alerte verte s’affiche dans tooreflect de zone d’autorisation hello que hello problème soit résolu.

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
