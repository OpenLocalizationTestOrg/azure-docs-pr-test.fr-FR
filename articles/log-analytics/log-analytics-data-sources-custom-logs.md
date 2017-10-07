---
title: "aaaCollect personnalisée se connecte Analytique des journaux OMS | Documents Microsoft"
description: "Log Analytics peut collecter des événements dans des fichiers texte sur des ordinateurs Windows et Linux.  Cet article décrit comment toodefine un nouveau journal personnalisé et les détails des enregistrements de hello créent dans le référentiel d’OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Journaux personnalisés dans Log Analytics
source de données de journaux personnalisés Hello dans Analytique de journal vous permet de toocollect les événements à partir des fichiers texte sur les ordinateurs Windows et Linux. De nombreuses applications journaux informations tootext au lieu de services de journalisation standard tels que le journal des événements Windows ou Syslog.  Une fois collectées, vous pouvez analyser chaque enregistrement de journal hello dans les champs de tooindividual à l’aide de hello [les champs personnalisés](log-analytics-custom-fields.md) fonctionnalité de journal Analytique.

![Collecte de journaux personnalisés](media/log-analytics-data-sources-custom-logs/overview.png)

toobe de fichiers de journal Hello collectée doit correspondre à hello suivant des critères.

- journal de Hello doit avoir une seule entrée par ligne ou utiliser un horodatage correspondant hello suivantes met en forme au début de hello de chaque entrée.

    AAAA-MM-JJ HH:MM:SS <br>M/J/AAAA HH:MM:SS AM/PM <br>Mois JJ,AAAA HH:MM:SS

- fichier de journal Hello ne doit pas autoriser d’où les fichiers hello sont remplacé par de nouvelles entrées mises à jour circulaires.
- fichier de journal de Hello doit utiliser l’encodage ASCII ou UTF-8.  Les autres formats, par exemple UTF-16, ne sont pas pris en charge.

>[!NOTE]
>S’il existe des entrées en double dans le fichier journal de hello, Analytique de journal collectera les.  Toutefois, les résultats de recherche hello seront incohérents où affichent les résultats du filtrage hello plus d’événements que le nombre de résultats hello.  Il sera important de valider hello journal toodetermine si l’application hello qui le crée à l’origine de ce comportement et de corriger si possible avant de créer la définition de la collection hello journal personnalisé.  
>
  
## <a name="defining-a-custom-log"></a>Définition d’un journal personnalisé
Utilisez hello suivant la procédure toodefine un fichier journal personnalisé.  Faites défiler vers la fin de toohello de cet article pour une procédure pas à pas d’un exemple d’ajout d’un journal personnalisé.

### <a name="step-1-open-hello-custom-log-wizard"></a>Étape 1. Ouvrez hello Assistant de journal personnalisé
Hello Assistant journal personnalisé s’exécute dans le portail OMS est hello et vous permet de toodefine un nouveau toocollect de journal personnalisé.

1. Dans le portail OMS : hello, accédez trop**paramètres**.
2. Cliquez sur **Données** puis sur **Journaux personnalisés**.
3. Par défaut, toutes les modifications de configuration sont automatiquement récupérées tooall agents.  Pour les agents de Linux, un fichier de configuration est envoyé toohello Fluentd de collecteurs de données.  Si vous le souhaitez toomodify ce fichier manuellement sur chaque agent Linux, puis hello désactivez case à cocher *appliquer ci-dessous les machines Linux configuration toomy*.
4. Cliquez sur **ajouter +** tooopen hello Assistant de journal personnalisé.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Étape 2. Télécharger et analyser un exemple de journal
Vous commencez par télécharger un exemple de journal personnalisées de hello.  Assistant de Hello analyser et afficher les entrées de hello dans ce fichier pour vous toovalidate.  Analytique de journal utilisera un délimiteur hello que vous spécifiez tooidentify chaque enregistrement.

**Nouvelle ligne** est le délimiteur par défaut de hello et est utilisé pour les fichiers journaux qui ont une seule entrée par ligne.  Si la ligne de hello commence par une date et heure dans un des formats disponibles de hello, vous pouvez ensuite spécifier un **Timestamp** délimiteur qui prend en charge les entrées qui s’étendent sur plusieurs lignes.

Si un délimiteur de timestamp est utilisé, puis de la propriété TimeGenerated de hello de chaque enregistrement stocké dans OMS contiendra hello date/heure spécifié pour cette entrée dans le fichier journal de hello.  Si un nouveau délimiteur de ligne est utilisé, TimeGenerated est remplie avec la date et l’heure que le journal Analytique collectées entrée de hello.

> [!NOTE]
> Analytique de journal traite actuellement hello date/heure collecté à partir d’un journal à l’aide d’un délimiteur de timestamp comme UTC.  Ce sera bientôt horaire toouse modifiées hello sur l’agent de hello.
>
>

1. Cliquez sur **Parcourir** et recherchez le fichier d’exemple tooa.  Notez que ce bouton peut s’appeler **Choisir un fichier** dans certains navigateurs.
2. Cliquez sur **Suivant**.
3. Pour télécharger hello fichier liste hello enregistrements et qu’il identifie Hello Assistant de journal personnalisé.
4. Modifier séparateur hello tooidentify utilisé un nouvel enregistrement et délimiteur hello select qui identifie mieux enregistrements hello dans votre fichier journal.
5. Cliquez sur **Suivant**.

### <a name="step-3-add-log-collection-paths"></a>Étape 3. Ajouter des chemins de collecte de journaux
Vous devez définir un ou plusieurs chemins sur agent hello qui permet de localiser les journaux personnalisés hello.  Vous pouvez fournir un chemin d’accès spécifique et le nom de fichier journal de hello, ou vous pouvez spécifier un chemin d’accès avec un caractère générique pour le nom de hello.  Ce mécanisme prend en charge les applications qui créent un fichier par jour ou lorsqu’un fichier atteint une certaine taille.  Vous pouvez également fournir plusieurs chemins d’accès pour un fichier journal.

Par exemple, une application peut créer un fichier journal par jour avec la date hello inclus dans le nom hello comme dans log20100316.txt. Un modèle d’un journal de ce type peut être *journal\*.txt* qui serait d’utiliser tooany journal après l’application hello de noms de schéma.

Hello tableau suivant fournit des exemples de modèles valides toospecify différents fichiers journaux.

| Description | Chemin |
|:--- |:--- |
| Tous les fichiers sous *C:\Logs* avec l’extension .txt sur l’agent Windows |C:\Logs\\\*.txt |
| Tous les fichiers sous *C:\Logs* avec un nom commençant par log et portant l’extension .txt sur l’agent Windows |C:\Logs\log\*.txt |
| Tous les fichiers sous */var/log/audit* avec l’extension .txt sur l’agent Linux |/var/log/audit/*.txt |
| Tous les fichiers sous */var/log/audit* avec un nom commençant par log et portant l’extension .txt sur l’agent Linux |/var/log/audit/log\*.txt |

1. Sélectionnez toospecify Windows ou Linux, le format de chemin d’accès que vous ajoutez.
2. Tapez le chemin d’accès de hello et cliquez sur hello  **+**  bouton.
3. Répétez les processus hello pour les chemins d’accès supplémentaires.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Étape 4. Fournissez un nom et une description pour le journal de hello
Hello nom que vous spécifiez sera être utilisé pour le type de journal hello comme décrit ci-dessus.  Il se termine toujours par _CL toodistinguish elle en tant qu’un journal personnalisé.

1. Tapez un nom pour le journal de hello.  Hello  **\_CL** suffixe est fourni automatiquement.
2. Si vous le souhaitez, renseignez le champ **Description**.
3. Cliquez sur **suivant** définition de journal personnalisé toosave hello.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Étape 5. Valider des journaux personnalisés hello sont collectés
Cela peut prendre jusqu'à tooan heure initiale des données hello à partir d’un nouveau tooappear de journal personnalisé dans le journal Analytique.  Il va commencer à collecter les entrées de hello journaux trouvent dans le chemin d’accès hello spécifié à partir du point de hello que vous hello défini journal personnalisé.  Il conserve pas les entrées de hello que vous avez téléchargé lors de la création du journal personnalisé hello, mais il collecte des entrées déjà existantes dans les fichiers journaux hello qui localise.

Une fois que le journal Analytique commence la collecte de journal personnalisé de hello, ses enregistrements sera disponibles avec une recherche de journal.  Utiliser le nom hello que vous avez donné de journal personnalisée hello hello **Type** dans votre requête.

> [!NOTE]
> Si hello RawData propriété est absent de la recherche de hello, vous pouvez peut-être tooclose et rouvrez votre navigateur.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Étape 6. Analyser les entrées de journal personnalisées hello
entrée de journal complet Hello est stockée dans une propriété unique appelée **RawData**.  Vous souhaiterez certainement que tooseparate hello différents éléments d’informations dans chaque entrée dans les propriétés individuelles stockées dans l’enregistrement de hello.  Cela à l’aide de hello [les champs personnalisés](log-analytics-custom-fields.md) fonctionnalité de journal Analytique.

La procédure détaillée pour l’analyse d’entrée de journal personnalisée hello n’est pas indiquée ici.  Reportez-vous toohello [les champs personnalisés](log-analytics-custom-fields.md) documentation pour obtenir des informations.

## <a name="disabling-a-custom-log"></a>Désactivation d’un journal personnalisé
Vous ne pouvez pas supprimer une définition de journal personnalisé une fois qu’elle a été créée, mais vous pouvez la désactiver en supprimant tous ses chemins de regroupement.

1. Dans le portail OMS : hello, accédez trop**paramètres**.
2. Cliquez sur **Données** puis sur **Journaux personnalisés**.
3. Cliquez sur **détails** toodisable de définition de journal personnalisé toohello suivant.
4. Supprimez chacun des chemins d’accès de la collection hello pour la définition de journal personnalisées hello.

## <a name="data-collection"></a>Collecte des données
Log Analytics collecte les nouvelles entrées de chaque journal personnalisé toutes les 5 minutes environ.  l’agent de Hello enregistre sa place dans chaque fichier journal qu’il collecte à partir de.  Si l’agent de hello est mis hors connexion pendant une période de temps, puis Analytique de journal collectent des entrées d’où il s’était arrêté, même si ces entrées ont été créées lors de l’agent de hello est hors connexion.

contenu entier de Hello hello d’entrée de journal est écrites tooa de propriété unique appelée **RawData**.  Vous pouvez l’analyser dans plusieurs propriétés qui peuvent être analysées et traitées séparément en définissant [des champs personnalisés](log-analytics-custom-fields.md) après avoir créé les journal personnalisé hello.

## <a name="custom-log-record-properties"></a>Propriétés d’enregistrement de journal personnalisé
Les enregistrements de journal personnalisées ont un type avec le nom du journal hello que vous fournissez et hello propriétés Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| TimeGenerated |Date et heure auxquelles l’enregistrement de hello ont été collectées par Analytique de journal.  Si le journal de hello utilise un délimiteur de temps il s’agit de heure hello collecté à partir de l’entrée de hello. |
| SourceSystem |Type d’enregistrement de hello de l’agent a été collecté à partir de. <br> Ops Manager : Agent Windows. Connexion directe ou System Center Operations Manager <br> Linux – Tous les agents Linux |
| RawData |Recherche en texte intégral de hello collectées entrée. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents de gestion de System Center Operations.  Pour les autres agents, il s’agit d’AOI-\<workspace ID\> |

## <a name="log-searches-with-custom-log-records"></a>Recherches de journal avec des enregistrements de journal personnalisé
Les enregistrements de journaux personnalisés sont stockés dans le référentiel d’OMS hello comme enregistrements à partir de toute autre source de données.  Ils ont un type correspondant au nom hello que vous fournissez lorsque vous définissez le journal de hello, vous pouvez utiliser la propriété de Type hello dans vos enregistrements de tooretrieve recherche collectés à partir d’un journal spécifique.

Hello tableau suivant fournit des exemples de recherches de journal qui extrait des enregistrements de journaux personnalisés.

| Interroger | Description |
|:--- |:--- |
| Type=MyApp_CL |Tous les événements du fichier journal nommé MyApp_CL. |
| Type=MyApp_CL Severity_CF=error |Tous les événements d’un journal personnalisé nommé MyApp_CL avec la valeur *error* dans le champ personnalisé nommé *Severity_CF*. |

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.

> | Interroger | Description |
|:--- |:--- |
| MyApp_CL |Tous les événements du fichier journal nommé MyApp_CL. |
| MyApp_CL &#124; where Severity_CF=="error" |Tous les événements d’un journal personnalisé nommé MyApp_CL avec la valeur *error* dans le champ personnalisé nommé *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Exemple de procédure d’ajout d’un journal personnalisé
Hello suivante section décrit un exemple de création d’un journal personnalisé.  exemple de journal Hello collecté a une seule entrée sur chaque ligne commençant par une date et heure et puis délimitée par des virgules pour le message, l’état et code.  Plusieurs exemples d’entrée sont présentés ci-dessous.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Télécharger et analyser un exemple de journal
Nous fournir un des fichiers de journaux hello et que vous pouvez voir les événements hello qui sera être en cours.  Dans ce cas, le délimiteur Nouvelle ligne suffit.  Si une seule entrée dans le journal de hello peut couvrir plusieurs lignes Cependant, un séparateur d’horodatage doit toobe utilisé.

![Télécharger et analyser un exemple de journal](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Ajouter des chemins de collecte de journaux
les fichiers journaux Hello se situeront dans *C:\MyApp\Logs*.  Un nouveau fichier sera créé chaque jour avec un nom qui inclut la date de hello dans le modèle de hello *appYYYYMMDD.log*.  Le format adapté à ce fichier journal est *C:\MyApp\Logs\\\\*.log*.

![Chemin de collecte de journaux](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Fournissez un nom et une description pour le journal de hello
Nous utilisons le nom *MyApp_CL* et complétons le champ **Description**.

![Nom du journal](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Valider des journaux personnalisés hello sont collectés
Nous utilisons une requête de *Type = MyApp_CL* tooreturn tous les enregistrements de journaux seront collectés de hello.

![Requête de journal sans aucun champ personnalisé](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Analyser les entrées de journal personnalisées hello
Nous utilisons hello toodefine de champs personnalisés *EventTime*, *Code*, *état*, et *Message* champs et nous pouvons voir différence hello Bonjour enregistrements qui sont retournés par la requête de hello.

![Requête de journal avec des champs personnalisés](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [des champs personnalisés](log-analytics-custom-fields.md) tooparse les entrées de hello de journal personnalisées de hello dans les champs tooindividual.
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.
