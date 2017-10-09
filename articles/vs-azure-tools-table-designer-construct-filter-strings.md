---
title: "aaaConstructing les chaînes de filtre pour le Concepteur de tables hello | Documents Microsoft"
description: "Construction de chaînes de filtrage pour le Concepteur de tables hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Construction de chaînes de filtrage pour hello Concepteur de tables
## <a name="overview"></a>Vue d'ensemble
toofilter des données dans une table Azure qui est affiché dans hello Visual Studio **Concepteur de tables**, créer une chaîne de filtrage et d’entrer dans le champ de filtre hello. syntaxe de la chaîne Hello filtre est défini par hello WCF Data Services et est semblable tooa clause SQL WHERE, mais est envoyé toohello service de Table via une requête HTTP. Hello **Concepteur de tables** handles hello encodage pour vous, c’est le cas toofilter sur une valeur de propriété de votre choix, vous devez entrer uniquement le nom de propriété hello, opérateur de comparaison, valeur des critères, et éventuellement, un opérateur booléen dans hello filtrer champ. Vous n’avez pas besoin de l’option de requête tooinclude hello $filter comme vous le feriez si vous construisiez une URL table de hello tooquery via hello [référence API REST des Services stockage](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Hello WCF Data Services sont basés sur hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Pour plus d’informations sur l’option de requête système hello filtre (**$filter**), consultez hello [spécifications OData URI Conventions](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Opérateurs de comparaison
Hello opérateurs logiques suivants sont pris en charge pour tous les types de propriété :

| Opérateur logique | Description | Exemple de chaîne de filtrage |
| --- | --- | --- |
| eq |Égal à |Ville eq 'Redmond' |
| gt |Supérieur à |Prix gt 20 |
| ge |Supérieur ou égal trop|Prix ge 10 |
| lt |Inférieur à |Prix lt 20 |
| le |Inférieur ou égal à |Prix le 100 |
| ne |Non égal à |Ville ne 'Londres' |
| and |and |Prix le 200 and prix gt 3,5 |
| ou |ou |Prix le 3,5 or prix gt 200 |
| not |not |not isAvailable |

Lors de la construction d’une chaîne de filtrage, hello règles suivantes sont importantes :

* Utilisez hello opérateurs logiques toocompare une valeur de la propriété tooa. Notez qu’il n’est pas possible de toocompare une valeur dynamique tooa de propriété ; côté « un » de l’expression de hello doit être une constante.
* Toutes les parties de la chaîne de filtrage hello respectent la casse.
* valeur de constante Hello doit être de hello même type de propriété hello dans l’ordre des résultats valides de hello filtre tooreturn. Pour plus d’informations sur les types de propriété pris en charge, consultez [hello de présentation des modèle de données de Service de Table](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filtrage par propriété de chaîne
Lorsque vous filtrez sur les propriétés de chaîne, placez la constante de chaîne hello dans des guillemets simples.

Hello suivant des exemples de filtres de hello **PartitionKey** et **RowKey** propriétés ; non clés supplémentaires propriétés peuvent également être ajoutées à chaîne de filtrage toohello :

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Vous pouvez placer chaque expression de filtrage entre parenthèses, même si cela n’est pas obligatoire :

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Notez que hello service de Table ne prend pas en charge les requêtes à caractères génériques, et elles ne sont pas prises en charge dans le Concepteur de tables de hello soit. Toutefois, vous pouvez effectuer à l’aide des opérateurs de comparaison sur le préfixe de votre choix hello de correspondance de préfixe. Hello exemple suivant retourne des entités avec une propriété LastName commençant par le lettre hello 'A' :

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filtrage par propriété numérique
toofilter sur un entier ou un nombre à virgule flottante, spécifiez le nombre hello sans guillemets.

Cet exemple retourne toutes les entités dont la propriété Age a une valeur supérieure à 30 :

    Age gt 30

Cet exemple retourne toutes les entités avec une propriété AmountDue dont la valeur est inférieur ou égal à too100.25 :

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filtrage par propriété booléenne
toofilter sur une valeur booléenne, spécifiez **true** ou **false** sans guillemets.

Hello exemple suivant retourne toutes les entités où hello propriété IsActive a la valeur trop**true**:

    IsActive eq true

Vous pouvez également écrire cette expression de filtre sans opérateur logique de hello. Dans l’exemple suivant de hello, hello service de Table retournera également toutes les entités où IsActive est **true**:

    IsActive

tooreturn toutes les entités où IsActive est false, vous pouvez utiliser ne Hello pas opérateur :

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filtrage par propriété DateTime
toofilter sur une valeur DateTime, spécifiez hello **datetime** (mot clé), suivi d’une constante de date/heure hello dans des guillemets simples. constante de date/heure de Hello doit être au format UTC combiné, comme décrit dans [mise en forme des valeurs de propriété DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Bonjour à l’exemple suivant retourne des entités où propriété CustomerSince de hello est égal tooJuly 10, 2008 :

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
