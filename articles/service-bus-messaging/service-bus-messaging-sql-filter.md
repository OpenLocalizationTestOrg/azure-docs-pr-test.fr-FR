---
title: "référence de la syntaxe SQLFilter de Bus de Service d’aaaAzure | Documents Microsoft"
description: "Informations sur la syntaxe relative à SQLFilter."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: ea49d42e343a6b324eb34c7831ff6be2855346e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlfilter-syntax"></a>Syntaxe SQLFilter

A *SqlFilter* est une instance de hello [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)et représente une expression de filtre basé sur le langage SQL qui est évaluée par rapport à un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). Un SqlFilter prend en charge un sous-ensemble de la norme de hello SQL-92.  
  
 Cette rubrique répertorie les informations relatives à la syntaxe SQLFilter.  
  
```  
<predicate ::=  
      { NOT <predicate> }  
      | <predicate> AND <predicate>  
      | <predicate> OR <predicate>  
      | <expression> { = | <> | != | > | >= | < | <= } <expression>  
      | <property> IS [NOT] NULL  
      | <expression> [NOT] IN ( <expression> [, ...n] )  
      | <expression> [NOT] LIKE <pattern> [ESCAPE <escape_char>]  
      | EXISTS ( <property> )  
      | ( <predicate> )  
  
```  
  
```  
<expression> ::=  
      <constant>   
      | <function>  
      | <property>  
      | <expression> { + | - | * | / | % } <expression>  
      | { + | - } <expression>  
      | ( <expression> )  
  
```  
  
```  
<property> :=   
       [<scope> .] <property_name>  
  
```  
  
## <a name="arguments"></a>Arguments  
  
-   `<scope>`est une chaîne facultative qui indique la portée hello Hello `<property_name>`. Les valeurs autorisées sont `sys` ou `user`. Hello `sys` valeur indique l’étendue du système où `<property_name>` est un nom de propriété publique de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage). `user`Indique la portée de l’utilisateur où `<property_name>` est une clé de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionnaire. `user`étendue est étendue par défaut de hello si `<scope>` n’est pas spécifié.  
  
## <a name="remarks"></a>Remarques

Une tentative tooaccess une propriété inexistante système est une erreur, lors d’une propriété de l’utilisateur tooaccess un inexistant tentative n’est pas une erreur. Au lieu de cela, une propriété d’utilisateur inexistante est évaluée en interne en tant que valeur inconnue. Une valeur inconnue est traitée spécialement lors de l’évaluation de l’opérateur.  
  
## <a name="propertyname"></a>property_name  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a>Arguments  

 `<regular_identifier>`est une chaîne représentée par hello suivant d’expression régulière :  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
Cela signifie toute chaîne commençant par une lettre et suivie par un(e) ou plusieurs traits de soulignement/lettres/chiffres.  
  
`[:IsLetter:]` signifie tout caractère Unicode classé en tant que lettre Unicode. `System.Char.IsLetter(c)` renvoie `true` si `c` est une lettre Unicode.  
  
`[:IsDigit:]` signifie tout caractère Unicode classé en tant que chiffre décimal. `System.Char.IsDigit(c)` renvoie `true` si `c` est un chiffre Unicode.  
  
Un `<regular_identifier>` ne peut pas être un mot-clé réservé.  
  
`<delimited_identifier>` correspond à toute chaîne placée entre crochets ([]). Un crochet droit est représenté par deux crochets droits. Hello ci-dessous des exemples de `<delimited_identifier>`:  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
`<quoted_identifier>` correspond à toute chaîne placée entre guillemets doubles. Un guillemet double dans l’identificateur est représenté par deux guillemets doubles. Il est déconseillé de toouse des identificateurs entre guillemets, car elle peut facilement être confondue avec une constante de chaîne. Utilisez si possible un identificateur délimité. Hello Voici un exemple de `<quoted_identifier>`:  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a>modèle  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Remarques
  
`<pattern>` doit être une expression évaluée comme chaîne. Il est utilisé comme modèle pour hello opérateur LIKE.      Il peut contenir hello les caractères génériques suivants :  
  
-   `%` : toute chaîne de zéro caractère ou plus.  
  
-   `_` : n’importe quel caractère unique.  
  
## <a name="escapechar"></a>escape_char  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a>Remarques  

`<escape_char>` doit être une expression évaluée comme chaîne dont la longueur est 1. Il est utilisé comme caractère d’échappement pour hello opérateur LIKE.  
  
 Par exemple, `property LIKE 'ABC\%' ESCAPE '\'` correspond à `ABC%` au lieu d’une chaîne qui commence par `ABC`.  
  
## <a name="constant"></a>constant  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a>Arguments  
  
-   `<integer_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et ne contient pas de décimales. les valeurs Hello sont stockées en tant que `System.Int64` en interne, et suivez hello même plage.  
  
     Voici quelques exemples de constantes longues :  
  
    ```  
    1894  
    2  
    ```  
  
-   `<decimal_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et qui contient une décimale. les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision.  
  
     Dans une version ultérieure, ce nombre peut être stocké dans des données différentes toosupport exacte numérique sémantique de type, donc vous fiez pas hello faits hello sous-jacent est de type de données `System.Double` pour `<decimal_constant>`.  
  
     Hello Voici des exemples de constantes décimales :  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   `<approximate_number_constant>` est un nombre écrit de manière scientifique. les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision. Hello Voici des exemples de constantes de type numérique approximatifs :  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a>boolean_constant  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a>Remarques  

Constantes booléennes sont représentés par des mots clés de hello **TRUE** ou **FALSE**. les valeurs Hello sont stockées en tant que `System.Boolean`.  
  
## <a name="stringconstant"></a>string_constant  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a>Remarques  

Les constantes de chaîne sont placées entre guillemets simples et incluent tout caractère Unicode valide. Un guillemet simple intégré à une constante de chaîne est représenté par deux guillemets simples.  
  
## <a name="function"></a>function  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a>Remarques
  
Hello `newid()` fonction renvoie une **System.Guid** généré par hello `System.Guid.NewGuid()` (méthode).  
  
Hello `property(name)` fonction retourne la valeur hello de propriété hello référencée par `name`. Hello `name` valeur peut être toute expression valide qui retourne une valeur de chaîne.  
  
## <a name="considerations"></a>Considérations
  
Tenez compte de hello suit [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) sémantique :  
  
-   Les noms de propriété respectent la casse.  
  
-   Les opérateurs suivent autant que possible la sémantique de conversion implicite C#.  
  
-   Les propriétés système sont des propriétés publiques exposées dans les instances [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).  
  
    Tenez compte de hello suit `IS [NOT] NULL` sémantique :  
  
    -   `property IS NULL`est évalué comme étant `true` si des propriétés hello n’existe ou hello la valeur de la propriété est `null`.  
  
### <a name="property-evaluation-semantics"></a>Sémantique d’évaluation de la propriété  
  
-   Un tooevaluate tentative d’une propriété inexistante système lève un [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.  
  
-   Une propriété qui n’existe pas est évaluée en interne comme **inconnue**.  
  
 Évaluation « inconnue » dans les opérateurs arithmétiques :  
  
-   Pour les opérateurs binaires, si soit hello gauche et/ou droit des opérandes est évalué en tant que **inconnu**, puis le résultat de hello est **inconnu**.  
  
-   Pour les opérateurs unaires, si un opérande est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.  
  
 Évaluation « inconnue » dans les opérateurs de comparaison binaires :  
  
-   Si soit hello gauche et/ou droit des opérandes est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.  
  
 Évaluation « inconnue » dans `[NOT] LIKE` :  
  
-   Si n’importe quel opérande est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.  
  
 Évaluation « inconnue » dans `[NOT] IN` :  
  
-   Si hello opérande de gauche est évaluée comme **inconnu**, puis le résultat de hello est **inconnu**.  
  
 Évaluation « inconnue » dans l’opérateur **AND** :  
  
```  
+---+---+---+---+  
|AND| T | F | U |  
+---+---+---+---+  
| T | T | F | U |  
+---+---+---+---+  
| F | F | F | F |  
+---+---+---+---+  
| U | U | F | U |  
+---+---+---+---+  
```  
  
 Évaluation « inconnue » dans l’opérateur **OR** :  
  
```  
+---+---+---+---+  
|OR | T | F | U |  
+---+---+---+---+  
| T | T | T | T |  
+---+---+---+---+  
| F | T | F | U |  
+---+---+---+---+  
| U | T | U | U |  
+---+---+---+---+  
```  
  
### <a name="operator-binding-semantics"></a>Sémantique de liaison d’opérateur
  
-   Opérateurs de comparaison tels que `>`, `>=`, `<`, `<=`, `!=`, et `=` suivez hello même sémantique que l’opérateur hello c# de liaison de données de type promotions et conversions implicites.  
  
-   Les opérateurs arithmétiques tels que `+`, `-`, `*`, `/`, et `%` suivez hello même sémantique que l’opérateur hello c# de liaison de données de type promotions et conversions implicites.

## <a name="next-steps"></a>Étapes suivantes

- [Classe SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [Classe SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)