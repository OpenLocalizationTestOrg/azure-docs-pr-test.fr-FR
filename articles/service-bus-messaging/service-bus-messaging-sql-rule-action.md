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
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="7a57f-103">Syntaxe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="7a57f-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="7a57f-104">A *SqlRuleAction* est une instance de hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classe et ensemble représente des actions écrites en langage SQL en fonction de syntaxe qui est effectuée sur un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="7a57f-104">A *SqlRuleAction* is an instance of hello [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="7a57f-105">Cette rubrique fournit des détails sur hello grammaire action de règle SQL.</span><span class="sxs-lookup"><span data-stu-id="7a57f-105">This topic lists details about hello SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="7a57f-106">Arguments</span><span class="sxs-lookup"><span data-stu-id="7a57f-106">Arguments</span></span>  
  
-   <span data-ttu-id="7a57f-107">`<scope>`est une chaîne facultative qui indique la portée hello Hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-107">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="7a57f-108">Les valeurs autorisées sont `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="7a57f-109">Hello `sys` valeur indique l’étendue du système où `<property_name>` est un nom de propriété publique de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="7a57f-109">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="7a57f-110">`user`Indique la portée de l’utilisateur où `<property_name>` est une clé de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="7a57f-110">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="7a57f-111">`user`étendue est étendue par défaut de hello si `<scope>` n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="7a57f-111">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-112">Remarks</span></span>  

<span data-ttu-id="7a57f-113">Une tentative tooaccess une propriété inexistante système est une erreur, lors d’une propriété de l’utilisateur tooaccess un inexistant tentative n’est pas une erreur.</span><span class="sxs-lookup"><span data-stu-id="7a57f-113">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="7a57f-114">Au lieu de cela, une propriété d’utilisateur inexistante est évaluée en interne en tant que valeur inconnue.</span><span class="sxs-lookup"><span data-stu-id="7a57f-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="7a57f-115">Une valeur inconnue est traitée spécialement lors de l’évaluation de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="7a57f-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="7a57f-116">property_name</span><span class="sxs-lookup"><span data-stu-id="7a57f-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="7a57f-117">Arguments</span><span class="sxs-lookup"><span data-stu-id="7a57f-117">Arguments</span></span>  
 <span data-ttu-id="7a57f-118">`<regular_identifier>`est une chaîne représentée par hello suivant d’expression régulière :</span><span class="sxs-lookup"><span data-stu-id="7a57f-118">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="7a57f-119">Cela signifie toute chaîne commençant par une lettre et suivie par un(e) ou plusieurs traits de soulignement/lettres/chiffres.</span><span class="sxs-lookup"><span data-stu-id="7a57f-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="7a57f-120">`[:IsLetter:]` signifie tout caractère Unicode classé en tant que lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="7a57f-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="7a57f-121">`System.Char.IsLetter(c)` renvoie `true` si `c` est une lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="7a57f-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="7a57f-122">`[:IsDigit:]` signifie tout caractère Unicode classé en tant que chiffre décimal.</span><span class="sxs-lookup"><span data-stu-id="7a57f-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="7a57f-123">`System.Char.IsDigit(c)` renvoie `true` si `c` est un chiffre Unicode.</span><span class="sxs-lookup"><span data-stu-id="7a57f-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="7a57f-124">Un `<regular_identifier>` ne peut pas être un mot-clé réservé.</span><span class="sxs-lookup"><span data-stu-id="7a57f-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="7a57f-125">`<delimited_identifier>` correspond à toute chaîne placée entre crochets ([]).</span><span class="sxs-lookup"><span data-stu-id="7a57f-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="7a57f-126">Un crochet droit est représenté par deux crochets droits.</span><span class="sxs-lookup"><span data-stu-id="7a57f-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="7a57f-127">Hello ci-dessous des exemples de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="7a57f-127">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="7a57f-128">`<quoted_identifier>` correspond à toute chaîne placée entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="7a57f-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="7a57f-129">Un guillemet double dans l’identificateur est représenté par deux guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="7a57f-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="7a57f-130">Il est déconseillé de toouse des identificateurs entre guillemets, car elle peut facilement être confondue avec une constante de chaîne.</span><span class="sxs-lookup"><span data-stu-id="7a57f-130">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="7a57f-131">Utilisez si possible un identificateur délimité.</span><span class="sxs-lookup"><span data-stu-id="7a57f-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="7a57f-132">Hello Voici un exemple de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="7a57f-132">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="7a57f-133">modèle</span><span class="sxs-lookup"><span data-stu-id="7a57f-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-134">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-134">Remarks</span></span>
  
 <span data-ttu-id="7a57f-135">`<pattern>` doit être une expression évaluée comme chaîne.</span><span class="sxs-lookup"><span data-stu-id="7a57f-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="7a57f-136">Il est utilisé comme modèle pour hello opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="7a57f-136">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="7a57f-137">Il peut contenir hello les caractères génériques suivants :</span><span class="sxs-lookup"><span data-stu-id="7a57f-137">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="7a57f-138">`%` : toute chaîne de zéro caractère ou plus.</span><span class="sxs-lookup"><span data-stu-id="7a57f-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="7a57f-139">`_` : n’importe quel caractère unique.</span><span class="sxs-lookup"><span data-stu-id="7a57f-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="7a57f-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="7a57f-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-141">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-141">Remarks</span></span>
  
 <span data-ttu-id="7a57f-142">`<escape_char>` doit être une expression évaluée comme chaîne dont la longueur est 1.</span><span class="sxs-lookup"><span data-stu-id="7a57f-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="7a57f-143">Il est utilisé comme caractère d’échappement pour hello opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="7a57f-143">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="7a57f-144">Par exemple, `property LIKE 'ABC\%' ESCAPE '\'` correspond à `ABC%` au lieu d’une chaîne qui commence par `ABC`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="7a57f-145">constant</span><span class="sxs-lookup"><span data-stu-id="7a57f-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="7a57f-146">Arguments</span><span class="sxs-lookup"><span data-stu-id="7a57f-146">Arguments</span></span>  
  
-   <span data-ttu-id="7a57f-147">`<integer_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et ne contient pas de décimales.</span><span class="sxs-lookup"><span data-stu-id="7a57f-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="7a57f-148">les valeurs Hello sont stockées en tant que `System.Int64` en interne, et suivez hello même plage.</span><span class="sxs-lookup"><span data-stu-id="7a57f-148">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="7a57f-149">Hello Voici des exemples de constantes de type long :</span><span class="sxs-lookup"><span data-stu-id="7a57f-149">hello following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="7a57f-150">`<decimal_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et qui contient une décimale.</span><span class="sxs-lookup"><span data-stu-id="7a57f-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="7a57f-151">les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="7a57f-151">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="7a57f-152">Dans une version ultérieure, ce nombre peut être stocké dans des données différentes toosupport exacte numérique sémantique de type, donc vous fiez pas hello faits hello sous-jacent est de type de données `System.Double` pour `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-152">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="7a57f-153">Hello Voici des exemples de constantes décimales :</span><span class="sxs-lookup"><span data-stu-id="7a57f-153">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="7a57f-154">`<approximate_number_constant>` est un nombre écrit de manière scientifique.</span><span class="sxs-lookup"><span data-stu-id="7a57f-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="7a57f-155">les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="7a57f-155">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="7a57f-156">Hello Voici des exemples de constantes de type numérique approximatifs :</span><span class="sxs-lookup"><span data-stu-id="7a57f-156">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="7a57f-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="7a57f-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-158">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-158">Remarks</span></span>
  
<span data-ttu-id="7a57f-159">Constantes booléennes sont représentés par des mots clés de hello `TRUE` ou `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-159">Boolean constants are represented by hello keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="7a57f-160">les valeurs Hello sont stockées en tant que `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-160">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="7a57f-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="7a57f-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-162">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-162">Remarks</span></span>
  
<span data-ttu-id="7a57f-163">Les constantes de chaîne sont placées entre guillemets simples et incluent tout caractère Unicode valide.</span><span class="sxs-lookup"><span data-stu-id="7a57f-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="7a57f-164">Un guillemet simple intégré à une constante de chaîne est représenté par deux guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="7a57f-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="7a57f-165">function</span><span class="sxs-lookup"><span data-stu-id="7a57f-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="7a57f-166">Remarques</span><span class="sxs-lookup"><span data-stu-id="7a57f-166">Remarks</span></span>  

<span data-ttu-id="7a57f-167">Hello `newid()` fonction renvoie une **System.Guid** généré par hello `System.Guid.NewGuid()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="7a57f-167">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="7a57f-168">Hello `property(name)` fonction retourne la valeur hello de propriété hello référencée par `name`.</span><span class="sxs-lookup"><span data-stu-id="7a57f-168">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="7a57f-169">Hello `name` valeur peut être toute expression valide qui retourne une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="7a57f-169">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="7a57f-170">Considérations</span><span class="sxs-lookup"><span data-stu-id="7a57f-170">Considerations</span></span>

- <span data-ttu-id="7a57f-171">JEU est utilisé toocreate une nouvelle valeur d’hello, propriété ou de la mise à jour, d’une propriété existante.</span><span class="sxs-lookup"><span data-stu-id="7a57f-171">SET is used toocreate a new property or update hello value of an existing property.</span></span>
- <span data-ttu-id="7a57f-172">SUPPRESSION est utilisé tooremove une propriété.</span><span class="sxs-lookup"><span data-stu-id="7a57f-172">REMOVE is used tooremove a property.</span></span>
- <span data-ttu-id="7a57f-173">JEU effectue une conversion implicite si possible lorsque le type d’expression hello et type de propriété existant hello sont différents.</span><span class="sxs-lookup"><span data-stu-id="7a57f-173">SET performs implicit conversion if possible when hello expression type and hello existing property type are different.</span></span>
- <span data-ttu-id="7a57f-174">L’action échoue s’il est fait référence à des propriétés de système inexistantes.</span><span class="sxs-lookup"><span data-stu-id="7a57f-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="7a57f-175">L’action réussit s’il est fait référence à des propriétés d’utilisateur inexistantes.</span><span class="sxs-lookup"><span data-stu-id="7a57f-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="7a57f-176">Une propriété inexistante utilisateur est évaluée comme « Inconnu », en interne, suivant hello même sémantique que [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) lors de l’évaluation des opérateurs.</span><span class="sxs-lookup"><span data-stu-id="7a57f-176">A non-existent user property is evaluated as "Unknown" internally, following hello same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a57f-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a57f-177">Next steps</span></span>

- [<span data-ttu-id="7a57f-178">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="7a57f-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="7a57f-179">Classe SqlFilter</span><span class="sxs-lookup"><span data-stu-id="7a57f-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
