---
title: "aaaHow tooBuild planifications complexes et Avancé de périodicité avec Azure Scheduler"
description: "Comment les planifications de complexe tooBuild et Avancé de périodicité avec Azure Scheduler"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Comment les planifications de complexe tooBuild et Avancé de périodicité avec Azure Scheduler
## <a name="overview"></a>Vue d'ensemble
Au cœur de hello d’un planificateur Azure travail est hello *planification*. planification de Hello détermine quand et comment hello planificateur exécute le travail de hello.

Azure Scheduler vous permet de toospecify à usage unique et périodique des planifications différentes pour un travail. Les planifications *à usage unique* se déclenchent une seule fois à un moment précis. Il s’agit en fait de planifications *récurrentes* qui ne s’exécutent qu’une seule fois. Les planifications récurrentes se déclenchent selon une fréquence prédéfinie.

Grâce à cette flexibilité, Azure Scheduler vous permet de prendre en charge un large éventail de scénarios professionnels :

* Nettoyage périodique des données : par exemple, tous les jours, supprimer tous les tweets de plus de 3 mois
* Archivage – par exemple, chaque mois, le service toobackup d’historique de facturation par émission de données
* Demandes de données externes : par exemple, toutes les 15 minutes, extraire un nouveau bulletin météorologique NOAA pour le ski.
* Traitement des images – par exemple, tous les jours ouvrables, pendant les heures creuses, utilisez cloud informatique toocompress images téléchargement dans la journée

Dans cet article, nous traitons d'exemples de travaux que vous pouvez créer avec Azure Scheduler. Nous fournissons des données JSON hello qui décrit chaque planification. Si vous utilisez hello [API REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx), vous pouvez utiliser ce même JSON pour [création d’un travail Azure Scheduler](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Scénarios pris en charge
Hello de que nombreux exemples dans cette rubrique illustrent transversales hello des scénarios Azure Scheduler prend en charge. Généralement, les exemples suivants illustrent comment les planifications toocreate pour nombreux modèles de comportement, y compris ceux hello ci-dessous :

* Exécuter une seule fois à une date et une heure spécifiques
* Exécuter et répéter un nombre de fois explicites
* Exécuter immédiatement et répéter
* Exécuter et répéter tous/toutes les *n* minutes, heures, jours, semaines ou mois, en commençant à un moment spécifique
* Exécuter et répéter selon une fréquence hebdomadaire ou mensuelle, mais uniquement des jours spécifiques, des jours spécifiques de la semaine ou des jours spécifiques du mois
* Exécuter et répéter à plusieurs reprises dans une période : par exemple, le dernier vendredi et lundi de chaque mois, ou à 5h15 et 17h15 chaque jour

## <a name="dates-and-datetimes"></a>Dates et dates/heures
Les dates dans les travaux Azure Scheduler suivent hello [ISO-8601 spécification](http://en.wikipedia.org/wiki/ISO_8601) et inclure uniquement les dates hello.

Références de date-heure dans les travaux Azure Scheduler suivent hello [ISO-8601 spécification](http://en.wikipedia.org/wiki/ISO_8601) et incluent des parties de date et heure. Une Date-heure qui ne spécifie pas un décalage UTC est supposée toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Procédure : Utiliser JSON et l'API REST pour la création de planifications
un calendrier simple à l’aide de toocreate hello [API REST d’Azure Scheduler](https://msdn.microsoft.com/library/mt629143), d’abord [enregistrer votre abonnement avec un fournisseur de ressources](https://msdn.microsoft.com/library/azure/dn790548.aspx) (nom du fournisseur hello pour le planificateur est  *Microsoft.Scheduler*), puis [créer une collection de travaux](https://msdn.microsoft.com/library/mt629159.aspx)et enfin [créer un travail](https://msdn.microsoft.com/library/mt629145.aspx). Lorsque vous créez une tâche, vous pouvez spécifier la planification et l’utilisation de JSON comme un extrait ci-dessous hello de périodicité :

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Vue d'ensemble : Notions fondamentales du schéma de travail
Hello tableau suivant fournit une vue d’ensemble de toorecurrence de hello principaux éléments connexes et la planification d’un travail :

| **Nom JSON** | **Description** |
|:--- |:--- |
| ***startTime*** |*startTime* est une Date-Heure. Pour les planifications simples, *startTime* est la première occurrence de hello et pour les planifications complexes, hello travail démarre sans tôt *startTime*. |
| ***recurrence*** |Hello *périodicité* objet spécifie les règles de récurrence pour le travail de hello et hello périodicité hello seront exécutera. objet de récurrence Hello prend en charge les éléments de hello *fréquence, intervalle, l’heure de fin, le nombre,* et *planification*. Si *périodicité* est défini, *fréquence* est requis ; hello d’autres éléments de *périodicité* sont facultatives. |
| ***frequency*** |Hello *fréquence* chaîne représentant l’unité de fréquence hello après le hello travail se répète. Les valeurs prises en charge sont *« minute », « hour », « day », « week »* ou *« month ».* |
| ***interval*** |Hello *intervalle* est un entier positif et indique l’intervalle de salutation pour hello *fréquence* qui détermine la fréquence à laquelle hello exécution de la tâche. Par exemple, si *intervalle* est 3 et *fréquence* est « semaine », le travail de hello se répète toutes les 3 semaines. Azure Scheduler prend en charge un *intervalle* maximum de 18 mois pour la fréquence mensuelle, 78 semaines pour la fréquence hebdomadaire ou 548 jours pour la fréquence quotidienne. Pour l’heure et la fréquence de minutes, plage de hello pris en charge est 1 < = *intervalle* < = 1000. |
| ***endTime*** |Hello *endTime* chaîne spécifie hello date-heure qui hello au-delà de travail ne doit pas exécuter. Il n’est pas valide toohave un *endTime* Bonjour passées. Si aucun *endTime* ou count est spécifié, le travail de hello s’exécute à l’infini. Les deux *endTime* et *nombre* ne peut pas être inclus pour hello même travail. |
| ***count*** |<p>Hello *nombre* est un entier positif (supérieur à zéro) qui spécifie le nombre de hello de ce travail doit s’exécuter avant la fin.</p><p>Hello *nombre* représente hello le nombre de fois où le travail de hello s’exécute avant étant déterminé comme étant terminée. Par exemple, pour une tâche qui est exécutée quotidiennement avec *nombre* 5 et date de début de lundi, le travail de hello se termine après l’exécution le vendredi. Si hello démarrer date est hello précédente, l’exécution de la première de hello est calculée à partir de l’heure de création de hello.</p><p>Si aucun *endTime* ou *nombre* est spécifié, le travail de hello s’exécute à l’infini. Les deux *endTime* et *nombre* ne peut pas être inclus pour hello même travail.</p> |
| ***schedule*** |Un travail avec une fréquence spécifiée modifie sa périodicité selon une planification périodique. Un objet *schedule* contient des modifications basées sur des minutes, heures, jours de la semaine, jour du mois et numéro de semaine. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Vue d'ensemble : Valeurs par défaut, limites et exemples du schéma de travail
Après cette introduction, examinons chacun de ces éléments en détail.

| **Nom JSON** | **Type de valeur** | **Obligatoire ?** | **Valeur par défaut** | **Valeurs valides** | **Exemple** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |Chaîne |Non |Aucun |Dates-Heures ISO-8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Object |Non |Aucun |Objet de périodicité |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |Chaîne |Oui |Aucun |"minute", "hour", "day", "week", "month" |<code>"frequency" : "hour"</code> |
| ***interval*** |Number |Non |1 |1 too1000. |<code>"interval":10</code> |
| ***endTime*** |String |Non |Aucun |Valeur de date-heure qui représente une heure Bonjour future |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Number |Non |Aucun |>= 1 |<code>"count": 5</code> |
| ***schedule*** |Object |Non |Aucun |Objet de planification |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Présentation approfondie : *startTime*
tableau de suivant de Hello captures comment *startTime* contrôle la manière dont un travail est exécuté.

| **valeur startTime** | **Aucune périodicité** | **Périodicité. Aucune planification** | **Périodicité avec planification** |
|:--- |:--- |:--- |:--- |
| **Aucune heure de début** |Exécuter une fois immédiatement |Exécuter une fois immédiatement. Les exécutions suivantes sont basées sur le calcul à partir de la dernière exécution |<p>Exécuter une fois immédiatement</p><p>Les exécutions suivantes sont basées sur la planification de périodicité</p> |
| **Heure de début dans le passé** |Exécuter une fois immédiatement |<p>Calculer la première exécution ultérieure après l’heure de début, puis l’exécuter à ce moment</p><p>Les exécutions suivantes sont basées sur le calcul à partir de la dernière exécution</p><p>Consultez l’exemple après ce tableau pour obtenir une explication supplémentaire</p> |<p>Démarre la tâche *ne plus tôt que* hello spécifié à l’heure de début. première occurrence de Hello est basée sur la planification de hello calculée à partir de l’heure de début hello</p><p>Les exécutions suivantes sont basées sur la planification de périodicité</p> |
| **Heure de début dans le futur ou à l'heure actuelle** |Exécuter une fois à l'heure de début spécifiée |<p>Exécuter une fois à l'heure de début spécifiée</p><p>Les exécutions suivantes sont basées sur le calcul à partir de la dernière exécution</p> |<p>Démarre la tâche *ne plus tôt que* hello spécifié à l’heure de début. première occurrence de Hello est basée sur la planification de hello calculée à partir de l’heure de début hello</p><p>Les exécutions suivantes sont basées sur la planification de périodicité</p> |

Examinons un exemple de ce qui se passe où *startTime* est Bonjour passé, avec *périodicité* , mais qu’aucun *planification*.  Supposons que hello heure actuelle est 2015-04-08 13:00, *startTime* est 2015-04-07 14:00, et *périodicité* est tous les 2 jours (défini avec *fréquence*: jour et *intervalle*: 2.) Notez que hello *startTime* est Bonjour passées et se produit avant l’heure actuelle de hello

Dans ces conditions, hello *première exécution* sera 2015-04-09 à 14:00\. moteur de planification Hello calcule les occurrences de l’exécution à partir de l’heure de début hello.  Toutes les instances Bonjour passées sont ignorés. moteur de Hello utilise instance hello suivante qui se produit dans hello futures.  Dans ce cas, *startTime* étant 2015-04-07 à 2 h 00, hello instance suivante est 2 jours à partir de ce moment, ce qui est 2015-04-09 à 2 h 00.

Notez que la première exécution de hello serait hello même même si hello startTime 2015-04-05 14:00 ou 2015-04-01 14:00\. Après la première exécution de hello, les exécutions suivantes sont calculées à l’aide de hello prévue : ils seraient 2015-04-11 à 14 h 00, puis 04-2015-13, à 2 h 00, puis 2015-04-15 à 2 h 00, etc..

Enfin, lorsqu’une tâche a une planification, si heures ou minutes ne sont pas définis dans la planification hello, ils les heures de toohello par défaut et/ou de minutes de la première exécution de hello, respectivement.

## <a name="deep-dive-schedule"></a>Présentation approfondie : *schedule*
D’une part, une *planification* pouvez *limite* hello du nombre d’exécutions du travail.  Par exemple, si un travail avec une fréquence de « mois » a un *planification* qui s’exécute sur un seul jour 31, la tâche de hello s’exécute en uniquement ces mois qui ont un 31<sup>st</sup> jour.

Hello de d’autre part, une *planification* peut également *développez* hello du nombre d’exécutions du travail. Par exemple, si un travail avec une fréquence de « mois » a un *planification* que s’exécute sur les jours du mois 1 et 2, hello travail s’exécute sur hello 1<sup>st</sup> et 2<sup>nd</sup> jours du mois hello au lieu d’une seule fois une mois.

Si plusieurs éléments de calendrier sont spécifiés, ordre de hello d’évaluation est de hello plus grande toosmallest – numéro de semaine, jour du mois, jour, heure et minute.

Hello tableau suivant décrit les *planification* éléments en détail.

| **Nom JSON** | **Description** | **Valeurs valides** |
|:--- |:--- |:--- |
| **minutes** |Minutes d’heure hello quels hello d’exécution des travaux |<ul><li>Entier, ou</li><li>Tableau d’entiers</li></ul> |
| **hours** |Heures de la journée hello quels hello d’exécution des travaux |<ul><li>Entier, ou</li><li>Tableau d’entiers</li></ul> |
| **weekDays** |Jours de travail de hello hello semaine seront exécutera. Peut uniquement être spécifié avec une fréquence hebdomadaire. |<ul><li>« Lundi », « mardi» , « mercredi », « jeudi », « vendredi », « samedi » ou « dimanche »</li><li>Tableau de chacun des hello au-dessus des valeurs de (taille maximale de tableau 7)</li></ul>*Ne* respectant pas la casse |
| **monthlyOccurrences** |Détermine les jours de travail de hello hello mois seront exécute. Peut uniquement être spécifié avec une fréquence mensuelle. |<ul><li>Tableau d’objets monthlyOccurrence :</li></ul> <pre>{ "day": *day*,<br />  "occurrence":*occurrence*<br />}</pre><p> *jour* est jour hello du travail de hello hello semaine s’exécutera, par exemple, {dimanche} est tous les dimanches du mois de hello. Obligatoire.</p><p>Est de l’occurrence *occurrence* du jour hello au mois de hello, par exemple, {dimanche, -1} est hello dernier dimanche du mois de hello. facultatif.</p> |
| **monthDays** |Jours de travail de hello hello mois s’exécutera. Peut uniquement être spécifié avec une fréquence mensuelle. |<ul><li>Toute valeur < = -1 et > = -31.</li><li>Toute valeur >= 1 et <= 31.</li><li>Un tableau composé des valeurs ci-dessus</li></ul> |

## <a name="examples-recurrence-schedules"></a>Exemples : planifications de périodicité
Hello Voici différents exemples de planifications de périodicité : en mettant l’accent sur l’objet de planification hello et ses sous-éléments.

planifications ci-dessous tous Hello supposent que hello *intervalle* a la valeur too1\. En outre, un doit partent du principe fréquence de droite hello dans conformément toowhat est hello *planification* – par exemple, une ne peut pas utiliser la fréquence de « day » et a une modification de « jour du mois » dans la planification de hello. Ces restrictions sont décrites ci-dessus.

| **Exemple** | **Description** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Exécution à 5h tous les jours. Azure Scheduler correspond à chaque valeur dans les « heures » avec chaque valeur dans les « minutes », une par une, toocreate une liste de toutes les heures hello travail quels hello est toobe exécuter. |
| <code>{"minutes":[15], "hours":[5]}</code> |Exécution à 5h15 tous les jours. |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Exécution à 5h15 et 17h15 tous les jours. |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Exécution à 5h15, 5h45, 17h15 et 17h45 tous les jours |
| <code>{"minutes":[0,15,30,45]}</code> |Exécution toutes les 15 minutes. |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Exécution toutes les heures. Ce travail s'exécute toutes les heures. minute de Hello est contrôlé par hello *startTime*, le cas échéant, ou si aucun n’est spécifié, par heure de création de hello. Par exemple, si hello heure de début ou heure de création (selon le cas) est 12:25 PM, les travaux hello seront exécuteront à 25 00:01:25, 02:25,..., 23:25. Bonjour planification est équivalent toohaving un travail avec *fréquence* de « heure », un *intervalle* de 1 et aucun *planification*. Hello différence est que cette planification peut être utilisée avec différents *fréquence* et *intervalle* toocreate autres travaux trop. Par exemple, si hello *fréquence* « mois », planification de hello est exécutés uniquement une fois par mois au lieu de tous les jours si *fréquence* ont été « jour » |
| <code>{minutes:[0]}</code> |Exécuter toutes les heures sur hello heure. Cette tâche s’exécute également toutes les heures, mais sur les heures hello (par exemple, 12 h, AM de 1, 2 heures du matin, etc..) Il s’agit de travail tooa équivalent avec une fréquence de « heure », une heure de début avec zéro minute et aucune planification si la fréquence de hello ont été « jour », mais si la fréquence de hello ont été « semaine » ou « mois », planification de hello exécuterait qu’un seul jour, une semaine ou le mois, un jour respectivement. |
| <code>{"minutes":[15]}</code> |Exécution 15 minutes après l'heure toutes les heures. Exécution toutes les heures, à partir de 00h15, 1h15, 2h15, etc. et se terminant à 22h15 et 23h15. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Exécution à 17h le samedi chaque semaine. |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Exécution à 17h le lundi, mercredi et vendredi chaque semaine. |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Exécution à 17h15 et 17h45 le lundi, mercredi et vendredi chaque semaine. |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Exécution à 5h et 17h le lundi, mercredi et vendredi chaque semaine. |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Exécution à 5h15, 5h45, 17h15 et 17h45 le lundi, mercredi et vendredi chaque semaine. |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Exécution toutes les 15 minutes les jours de semaine. |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Exécution toutes les 15 minutes les jours de semaine entre 9h et 16h45. |
| <code>{"weekDays":["sunday"]}</code> |Exécution le dimanche à l'heure de début. |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Exécution le mardi et le jeudi à l'heure de début. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Exécuter à 8 h 00 sur hello 28 jours de chaque mois (en supposant que la fréquence du mois) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Exécuter à 8 h 00 sur hello dernier jour du mois de hello. Si vous souhaitez que toorun une tâche sur hello dernier jour du mois, utilisez -1 au lieu de jour 28, 29, 30 ou 31. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Exécuter à 8 h 00 sur hello premier et dernier jour de chaque mois |
| <code>{monthDays":[1,-1]}</code> |Exécutez sur hello premier et dernier jour de chaque mois à l’heure de début |
| <code>{monthDays":[1,14]}</code> |Exécutez sur hello First et quatorzième jour de chaque mois à l’heure de début |
| <code>{monthDays":[2]}</code> |Exécutez sur hello Second jour de hello mois à l’heure de début |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Exécution le premier vendredi de chaque mois à 5h. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Exécution le premier vendredi de chaque mois à l'heure de début. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Exécution le troisième vendredi à partir de la fin du mois, chaque mois, à l'heure de début. |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Exécution le premier et le dernier vendredi de chaque mois à 5h15. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Exécution le premier et le dernier vendredi de chaque mois à l'heure de début. |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Exécution le cinquième vendredi de chaque mois à l'heure de début. S’il existe aucune vendredi cinquième dans un mois, ceci ne s’exécute ne pas, car il est planifiée toorun vendredi cinquième uniquement. Vous pouvez envisager d’utiliser -1 au lieu de 5 occurrence de hello si vous souhaitez que le travail de hello toorun sur hello produisent dernier vendredi du mois de hello. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Exécuter toutes les 15 Minutes dernier vendredi de hello mois |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Exécuter à 5 h 15, 5 h 45, 17:15 h 00 et 5 h 45 sur hello 3e mercredi de chaque mois |

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité d’Azure Scheluler](scheduler-high-availability-reliability.md)

 [Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler](scheduler-limits-defaults-errors.md)

 [Authentification sortante d’Azure Scheluler](scheduler-outbound-authentication.md)

