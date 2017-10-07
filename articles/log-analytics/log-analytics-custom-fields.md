---
title: champs aaaCustom dans le journal Analytique | Documents Microsoft
description: "fonction de champs personnalisés Hello d’Analytique de journal vous permet de toocreate vos propres champs de recherche à partir des données OMS qui ajoute des propriétés toohello d’un enregistrement collectée.  Cet article décrit le processus de hello toocreate un champ personnalisé et fournit une description détaillée avec un exemple d’événement."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Champs personnalisés dans Log Analytics
Hello **les champs personnalisés** fonctionnalité d’Analytique de journal vous permet de tooextend des enregistrements existants dans le référentiel d’OMS hello en ajoutant vos propres champs de recherche.  Les champs personnalisés sont remplis automatiquement à partir des données extraites d’autres propriétés hello même enregistrement.

![Vue d’ensemble des champs personnalisés](media/log-analytics-custom-fields/overview.png)

Par exemple, hello exemple d’enregistrement ci-dessous a des données utiles dans la description de l’événement hello.  L’extraction de ces données dans des propriétés séparées les rend disponibles pour des opérations de tri et de filtrage.

![Bouton Recherche dans les journaux](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> Bonjour Preview, vous êtes limité too100 des champs personnalisés dans votre espace de travail.  Cette limite pourra être relevée lorsque cette fonction sera disponible dans le commerce.
> 
> 

## <a name="creating-a-custom-field"></a>Création d’un champ personnalisé
Lorsque vous créez un champ personnalisé, Analytique de journal doit comprendre le toopopulate toouse de données sa valeur.  Elle utilise une technologie de Microsoft Research appelée FlashExtract tooquickly identifier ces données.  Au lieu de vous obliger tooprovide des instructions explicites, Analytique des journaux en apprend plus sur les données de salutation souhaité tooextract à partir d’exemples que vous fournissez.

Hello les sections suivantes fournit la procédure de hello pour la création d’un champ personnalisé.  Fin de cet article est une procédure pas à pas d’une extraction de l’exemple hello.

> [!NOTE]
> champ personnalisé de Hello est rempli en tant que les enregistrements correspondant hello spécifiés sont ajoutés toohello magasin de données OMS, il s’affiche uniquement sur les enregistrements recueillis après la création du champ personnalisé hello.  champ personnalisé de Hello n’est pas ajouté toorecords qui sont déjà dans le magasin de données hello lors de sa création.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Étape 1 : identifier les enregistrements qui auront le champ personnalisé de hello
première étape de Hello est enregistrements hello tooidentify qui obtiennent le champ personnalisé de hello.  Vous démarrez avec un [recherche de journal standard](log-analytics-log-searches.md) , puis sélectionnez un tooact d’enregistrement en tant que modèle de hello apprendra Analytique de journal.  Lorsque vous spécifiez que vous allez tooextract données dans un champ personnalisé, hello **Assistant Extraction de champs** est ouvert lorsque vous validez et affinez les critères de hello.

1. Accédez trop**recherche de journal** et utiliser un [interroger les enregistrements de hello tooretrieve](log-analytics-log-searches.md) qui auront le champ personnalisé de hello.
2. Sélectionnez un enregistrement qu’Analytique de journal utilisera tooact en tant que modèle pour extraire des champs de données toopopulate hello personnalisés.  Vous allez identifier les données que vous souhaitez tooextract à partir de cet enregistrement et Analytique de journal utilisera cet information toodetermine hello logique toopopulate hello champ personnalisé pour tous les enregistrements similaires de salutation.
3. Cliquez sur hello bouton toohello gauche de n’importe quelle propriété de texte Hello enregistrement et sélectionnez **extraire des champs de**.
4. Hello **Assistant Extraction de champs est ouverte**, et enregistrement hello vous avez sélectionné s’affiche dans hello **exemple principal** colonne.  champ personnalisé de Hello sera défini pour les enregistrements ayant hello mêmes valeurs dans les propriétés de hello qui sont sélectionnées.  
5. Si la sélection de hello n’est pas exactement ce que vous souhaitez, sélectionnez les critères de hello toonarrow des champs supplémentaires.  Commande toochange hello valeurs de champs pour les critères de hello, vous devez annuler et sélectionnez un autre enregistrement correspondant aux critères de hello souhaité.

### <a name="step-2---perform-initial-extract"></a>Étape 2 : effectuer l’extraction initiale.
Une fois que vous avez identifié les enregistrements hello qui auront le champ personnalisé de hello, vous identifiez les données de salutation que vous souhaitez tooextract.  Analytique de journal utilise des modèles similaires cette tooidentify informations enregistrements similaires.  Dans l’étape suivante hello vous être en mesure de toovalidate les résultats hello et fournir davantage d’informations pour toouse Analytique de journal dans son analyse.

1. Mettez en surbrillance de texte hello dans l’exemple d’enregistrement hello que vous souhaitez le champ personnalisé de toopopulate hello.  Vous obtiendrez avec un tooprovide de boîte de dialogue un nom pour l’extraction initiale hello champ et tooperform hello.  Hello caractères  **\_CF** sont ajoutés automatiquement.
2. Cliquez sur **extraire** tooperform une analyse d’enregistrements collectés.  
3. Hello **Résumé** et **résultats de la recherche** sections affichent les résultats de hello de hello extrait pour que vous puissiez vérifier sa précision.  **Résumé** affiche hello critères utilisés tooidentify enregistrements et le nombre de chacune des valeurs de données hello identifiés.  **Résultats de la recherche** fournit une liste détaillée des enregistrements correspondant aux critères de hello.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Étape 3 : vérifier l’exactitude de l’extrait de hello et créer le champ personnalisé
Une fois que vous avez effectué l’extraction initiale de hello, Analytique des journaux affiche ses résultats en fonction des données qui ont déjà été recueillies.  Si hello résultats semblent corrects vous pouvez créer des champs personnalisés de hello sans aucune tâche supplémentaire.  Si ce n’est pas le cas, vous pouvez affiner les résultats hello pour qu’Analytique des journaux puisse améliorer sa logique.

1. Si des valeurs de l’extraction initiale de hello ne sont pas correctes, puis cliquez sur hello **modifier** enregistrement inexactes icône suivant tooan et sélectionnez **modifier cette sélection** de sélection de commande toomodify hello.
2. entrée Hello est copié toohello **des exemples supplémentaires** section sous hello **exemple principal**.  Vous pouvez ajuster la mise en surbrillance hello ici toohelp Analytique de journal comprendre sélection hello, il y a lieu.
3. Cliquez sur **extraire** toouse ce tooevaluate informations nouvelle tous hello existant enregistre.  résultats de Hello peuvent être modifiés pour les enregistrements que vous venez de modifier à partir de nouvelles informations de hello.
4. Continuer tooadd corrections jusqu'à ce que tous les enregistrements de hello extraire correctement identifient hello données toopopulate hello nouveau champ personnalisé.
5. Cliquez sur **enregistrer l’extraction** lorsque vous êtes satisfait des résultats de hello.  Hello champ personnalisé est maintenant défini, mais il ne sera pas ajouté les enregistrements tooany encore.
6. Attend de nouveaux enregistrements hello correspondant spécifié critères toobe collectées et puis relancez la recherche de journal hello. Nouveaux enregistrements doivent avoir le champ personnalisé de hello.
7. Utiliser hello de champ personnalisé comme toute autre propriété d’enregistrement.  Vous pouvez l’utiliser tooaggregate et regrouper les données et même utiliser tooproduce nouvelles perspectives.

## <a name="viewing-custom-fields"></a>Affichage de champs personnalisés
Vous pouvez afficher une liste de tous les champs personnalisés dans votre groupe d’administration hello **paramètres** vignette du tableau de bord OMS hello.  Sélectionnez **Données** puis **Champs personnalisés** pour obtenir la liste de tous les champs personnalisés dans votre espace de travail.  

![Champs personnalisés](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Suppression d’un champ personnalisé
Il existe deux façons tooremove un champ personnalisé.  Hello est tout d’abord hello **supprimer** option pour chaque champ lors de l’affichage de la liste complète hello comme décrit ci-dessus.  Bonjour autre méthode est tooretrieve qu'un toohello de bouton hello enregistrement, puis cliquez sur à gauche de champ de hello.  menu de Hello aura un champ personnalisé d’option tooremove hello.

## <a name="sample-walkthrough"></a>Exemple de procédure pas à pas
Hello suivante section décrit un exemple complet de la création d’un champ personnalisé.  Cet exemple extrait le nom du service hello dans des événements Windows qui indiquent un changement d’état de service.  Il s’appuie sur des événements créés par le Gestionnaire de contrôle de Service dans le journal système de hello sur les ordinateurs Windows.  Si vous souhaitez toofollow cet exemple, vous devez être [collecte les événements d’informations pour le journal système hello](log-analytics-data-sources-windows-events.md).

Nous entrez hello suivant tooreturn de requête tous les événements du Gestionnaire de contrôle Service ayant un ID d’événement 7036 qui est l’événement hello qui indique le service démarre ou s’arrête.

![Interroger](media/log-analytics-custom-fields/query.png)

Ensuite, nous sélectionnons un enregistrement ayant l’ID d’événement 7036.

![Enregistrement source](media/log-analytics-custom-fields/source-record.png)

Nous voulons le nom du service hello qui s’affiche dans hello **RenderedDescription** propriétés et sélectionnez hello bouton suivant toothis.

![Extraire des champs](media/log-analytics-custom-fields/extract-fields.png)

Hello **Assistant Extraction de champs** est ouvert et hello **EventLog** et **EventID** les champs sélectionnés dans hello **exemple principal** colonne.  Cela indique que ce champ personnalisé hello est défini pour les événements du journal système de hello avec un ID d’événement 7036.  Cela suffit superflue tooselect tous les autres champs.

![Exemple principal](media/log-analytics-custom-fields/main-example.png)

Nous mettre en surbrillance le nom hello du service hello Bonjour **RenderedDescription** propriété et utiliser **Service** nom du service tooidentify hello.  champ personnalisé de Hello sera appelé **Service_CF**.

![Titre du champ](media/log-analytics-custom-fields/field-title.png)

Nous constatons que le nom service hello est identifié correctement pour certains enregistrements, mais pas pour d’autres.   Hello **résultats de la recherche** montrent qu’une partie du nom hello hello **carte de Performance WMI** n’a pas été sélectionné.  Hello **Résumé** montre quatre enregistrements avec **DPRMA** service inclus à tort un terme supplémentaire et deux enregistrements identifiés **programme d’installation de Modules** au lieu de **Le programme d’installation de Windows Modules**.  

![Résultats de la recherche](media/log-analytics-custom-fields/search-results-01.png)

Nous allons commencer par hello **carte de Performance WMI** enregistrement.  Cliquez sur son icône de modification, puis sur **Modifier cette mise en surbrillance**.  

![Modifier la mise en surbrillance](media/log-analytics-custom-fields/modify-highlight.png)

Nous augmentons mot hello de hello mise en surbrillance tooinclude **WMI** , puis réexécutez hello extrait.  

![Exemple supplémentaire](media/log-analytics-custom-fields/additional-example-01.png)

Nous pouvons voir que hello entrées pour **carte de Performance WMI** ont été corrigées et Analytique de journal utilisé également ce enregistrements hello toocorrect des informations de **le programme d’installation de Windows Module**.  Nous pouvons voir Bonjour **Résumé** section qui **DPMRA** est toujours pas identifié correctement.

![Résultats de la recherche](media/log-analytics-custom-fields/search-results-02.png)

Nous faire défiler enregistrement tooa avec hello service DPMRA et que vous utilisez hello même processus toocorrect enregistrer.

![Exemple supplémentaire](media/log-analytics-custom-fields/additional-example-02.png)

 Si nous exécutons d’extraction de hello, nous pouvons voir que tous les résultats sont désormais corrects.

![Résultats de la recherche](media/log-analytics-custom-fields/search-results-03.png)

Nous pouvons voir que **Service_CF** est créé mais n’est pas encore ajouté tooany enregistrements.

![Nombre initial](media/log-analytics-custom-fields/initial-count.png)

Une fois que du temps écoulé new les événements sont collectés, nous pouvons voir que qui hello **Service_CF** champ est maintenant ajouté toorecords qui correspondent aux critères de notre.

![Résultats finaux](media/log-analytics-custom-fields/final-results.png)

Nous pouvons à présent utiliser champ personnalisé de hello comme toute autre propriété de l’enregistrement.  tooillustrate, nous créons une requête qui regroupe par hello nouvelle **Service_CF** tooinspect champ les services qui sont hello plus actifs.

![Regrouper par requête](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toobuild les requêtes à l’aide des champs personnalisés pour les critères.
* Surveillez les [fichiers journaux personnalisés](log-analytics-data-sources-custom-logs.md) que vous analysez à l’aide de champs personnalisés.

