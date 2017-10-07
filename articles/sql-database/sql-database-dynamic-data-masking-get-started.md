---
title: "masquage des données dynamiques de base de données SQL aaaAzure | Documents Microsoft"
description: "Masquage dynamique des données de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>Masquage de données dynamiques dans une base de données SQL

Masquage dynamique des données de base de données SQL limite l’exposition des données sensibles en les masquant aux utilisateurs privilèges toonon. 

Masquage dynamique des données permet d’empêcher les données toosensitive de tout accès non autorisé en activant les clients toodesignate combien de tooreveal des données sensibles hello avec un impact minimal sur la couche d’application hello. Il s’agit d’une fonctionnalité basée sur des stratégies de sécurité qui masque les données sensibles hello hello jeu de résultats d’une requête sur des champs de base de données désignée données hello hello de base de données ne sont pas modifiées.

Par exemple, un représentant du service à un centre d’appels peut identifier des appelants par quelques chiffres de leur numéro de carte de crédit, mais ces éléments ne doivent pas être entièrement les données exposées toohello représentant du service. Une règle de masquage peut être définie que tous les masques de mais hello les quatre derniers chiffres de n’importe quel numéro de carte de crédit dans le jeu de résultats hello de toutes les requêtes. Autre exemple, un masque de données approprié peut être défini tooprotect informations d’identification personnelle (PII) données, afin qu’un développeur peut interroger les environnements de production aux fins de dépannage sans violer les réglementations de conformité.

## <a name="sql-database-dynamic-data-masking-basics"></a>Principes fondamentaux du masquage de données dynamiques de base de données SQL
Permet de paramétrer une stratégie Bonjour de masquage dynamique des données portail Azure en sélectionnant hello masquage dynamique des données opération dans votre Panneau de configuration de base de données SQL ou le panneau des paramètres.

### <a name="dynamic-data-masking-permissions"></a>Autorisations du masquage des données dynamiques
Masquage dynamique des données peuvent être configuré par l’administrateur de base de données Azure hello, un administrateur de serveur ou des rôles de responsable de la sécurité.

### <a name="dynamic-data-masking-policy"></a>Stratégie de masquage des données dynamiques
* **Utilisateurs SQL exclus du masquage** : ensemble d’utilisateurs de SQL ou résultats de la requête identités AAD qui obtiennent des données non masquées Bonjour SQL. Les utilisateurs disposant des privilèges d’administrateur sont toujours exclus du masquage et voir les données d’origine de salutation sans un masque.
* **Règles de masquage** -un ensemble de règles qui définissent hello désigné toobe de champs masqué et hello masquage de fonction qui est utilisée. Hello désigné des champs peut être défini à l’aide d’un nom de schéma de base de données, le nom de la table et le nom de la colonne.
* **Fonctions de masquage** -un ensemble de méthodes qui contrôlent l’exposition de hello de données pour différents scénarios.

| Fonction de masquage | Logique de masquage |
| --- | --- |
| **Par défaut** |**Complète des données toohello en fonction de masquage de types Hello désignés champs**<br/><br/>• Utilisez XXXX ou moins de x si hello hello champ est inférieure à 4 caractères pour les types de données string (nchar, ntext, nvarchar).<br/>• Utilisez la valeur zéro pour les types de données numériques (bigint, bit, decimal, int, money, numeric, smallint, smallmoney, tinyint, float, real).<br/>• Utilisez 01-01-1900 pour les types de données date/heure (date, datetime2, datetime, datetimeoffset, smalldatetime, time).<br/>• SQL variant, hello valeur par défaut de type en cours de hello est utilisé.<br/>• Pour du document XML hello <masked/> est utilisé.<br/>• Utilisez une valeur vide pour les types de données spéciaux (table timestamp, hierarchyid, GUID, binary, image, varbinary spatial). |
| **Carte de crédit** |**Méthode de masquage, qui expose hello les quatre derniers chiffres de hello désigné des champs** et ajoute une chaîne constante en tant que préfixe sous forme de hello d’une carte de crédit.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **E-mail** |**Méthode de masquage, qui expose la première lettre de hello et remplace le domaine du hello avec XXX.com** à l’aide d’un préfixe de chaîne constante sous forme de hello d’une adresse de messagerie.<br/><br/>aXX@XXXX.com |
| **Nombre aléatoire** |**Méthode de masquage, qui génère un nombre aléatoire** selon toohello sélectionné des limites et les types de données réelles. Si hello désigné des limites est égal, hello fonction de masquage est un nombre constant.<br/><br/>![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Texte personnalisé** |**Méthode, qui expose hello premiers et derniers caractères de masquage** et ajoute une chaîne de remplissage personnalisée au milieu de hello. Si la chaîne d’origine de hello est plus courte que suffixe et le préfixe de hello exposée, uniquement les hello chaîne de remplissage est utilisé. <br/>préfixe[remplissage]suffixe<br/><br/>![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Champs recommandés toomask
Hello moteur de recommandations DDM, indicateurs de certains champs de votre base de données en tant que champs potentiellement sensibles, ce qui peuvent être de bons candidats pour les masques. Dans Panneau de masquage dynamique des données la hello dans le portail de hello, vous verrez hello recommandé de colonnes de votre base de données. Vous devez toodo est cliquez sur **ajouter un masque** pour une ou plusieurs colonnes, puis **enregistrer** tooapply un masque pour ces champs.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Configuration du masquage des données dynamiques pour votre base de données à l’aide des cmdlets Powershell
Voir [Cmdlets de la base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Configuration du masquage des données dynamiques pour votre base de données à l’aide de l’API REST
Voir [Opérations pour les bases de données SQL Azure](https://msdn.microsoft.com/library/dn505719.aspx).

