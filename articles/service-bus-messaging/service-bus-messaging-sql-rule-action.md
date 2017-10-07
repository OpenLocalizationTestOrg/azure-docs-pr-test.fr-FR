---
title: "référence de la syntaxe aaaSQLRuleAction dans Azure | Documents Microsoft"
description: Informations sur la syntaxe SQLRuleAction.
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
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 8ef281f942847bcc535b83a5ffb30d03539734f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sqlruleaction-syntax"></a>Syntaxe SQLRuleAction

A *SqlRuleAction* est une instance de hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe et ensemble représente des actions écrites en langage SQL en fonction de syntaxe qui est effectuée sur un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).   
  
Cette rubrique fournit des détails sur hello grammaire action de règle SQL.  
  
```  
<statements> ::=
    <statement> [, ...n]  
  
```  
  
```  
<statement> ::=
    <action> [;]
    Remarks
    -------
    Semicolon is optional.  
  
```  
  
```  
<action> ::=
    SET <property> = <expression>
    REMOVE <property>  
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
  
### <a name="remarks"></a>Remarques  

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
  
     Hello Voici des exemples de constantes de type long :  
  
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
  
Constantes booléennes sont représentés par des mots clés de hello `TRUE` ou `FALSE`. les valeurs Hello sont stockées en tant que `System.Boolean`.  
  
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

- JEU est utilisé toocreate une nouvelle valeur d’hello, propriété ou de la mise à jour, d’une propriété existante.
- SUPPRESSION est utilisé tooremove une propriété.
- JEU effectue une conversion implicite si possible lorsque le type d’expression hello et type de propriété existant hello sont différents.
- L’action échoue s’il est fait référence à des propriétés de système inexistantes.
- L’action réussit s’il est fait référence à des propriétés d’utilisateur inexistantes.
- Une propriété inexistante utilisateur est évaluée comme « Inconnu », en interne, suivant hello même sémantique que [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) lors de l’évaluation des opérateurs.

## <a name="next-steps"></a>Étapes suivantes

- [Classe SQLRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [Classe SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
