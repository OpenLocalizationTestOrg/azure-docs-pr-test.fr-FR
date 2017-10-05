---
title: "Référence relative à la syntaxe SQLRuleAction dans Azure | Microsoft Docs"
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
ms.openlocfilehash: 7379b7f58563675f28d77928d933c0d9c7992e71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlruleaction-syntax"></a><span data-ttu-id="408a8-103">Syntaxe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="408a8-103">SQLRuleAction syntax</span></span>

<span data-ttu-id="408a8-104">*SqlRuleAction* est une instance de la classe [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) et représente un ensemble d’actions écrites selon une syntaxe basée sur le langage SQL effectuées par rapport à un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="408a8-104">A *SqlRuleAction* is an instance of the [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) class, and represents set of actions written in SQL-language based syntax that is performed against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span>   
  
<span data-ttu-id="408a8-105">Cette rubrique répertorie les informations relatives à la syntaxe de l’action de règle SQL.</span><span class="sxs-lookup"><span data-stu-id="408a8-105">This topic lists details about the SQL rule action grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="408a8-106">Arguments</span><span class="sxs-lookup"><span data-stu-id="408a8-106">Arguments</span></span>  
  
-   <span data-ttu-id="408a8-107">`<scope>` est une chaîne facultative qui indique la portée de `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="408a8-107">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="408a8-108">Les valeurs autorisées sont `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="408a8-108">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="408a8-109">La valeur `sys` indique la portée du système où `<property_name>` est un nom de propriété publique de la [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="408a8-109">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="408a8-110">`user` indique la portée de l’utilisateur où `<property_name>` est une clé du dictionnaire de la [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="408a8-110">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage Class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="408a8-111">La portée de l’`user` est l’étendue par défaut si `<scope>` n’est pas défini.</span><span class="sxs-lookup"><span data-stu-id="408a8-111">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
### <a name="remarks"></a><span data-ttu-id="408a8-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-112">Remarks</span></span>  

<span data-ttu-id="408a8-113">Une tentative d’accès à une propriété inexistante du système est une erreur, tandis qu’une tentative d’accès à une propriété d’utilisateur inexistante n’est pas une erreur.</span><span class="sxs-lookup"><span data-stu-id="408a8-113">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="408a8-114">Au lieu de cela, une propriété d’utilisateur inexistante est évaluée en interne en tant que valeur inconnue.</span><span class="sxs-lookup"><span data-stu-id="408a8-114">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="408a8-115">Une valeur inconnue est traitée spécialement lors de l’évaluation de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="408a8-115">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="408a8-116">property_name</span><span class="sxs-lookup"><span data-stu-id="408a8-116">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="408a8-117">Arguments</span><span class="sxs-lookup"><span data-stu-id="408a8-117">Arguments</span></span>  
 <span data-ttu-id="408a8-118">`<regular_identifier>` est une chaîne est représentée par l’expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="408a8-118">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
 <span data-ttu-id="408a8-119">Cela signifie toute chaîne commençant par une lettre et suivie par un(e) ou plusieurs traits de soulignement/lettres/chiffres.</span><span class="sxs-lookup"><span data-stu-id="408a8-119">This means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
 <span data-ttu-id="408a8-120">`[:IsLetter:]` signifie tout caractère Unicode classé en tant que lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="408a8-120">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="408a8-121">`System.Char.IsLetter(c)` renvoie `true` si `c` est une lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="408a8-121">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
 <span data-ttu-id="408a8-122">`[:IsDigit:]` signifie tout caractère Unicode classé en tant que chiffre décimal.</span><span class="sxs-lookup"><span data-stu-id="408a8-122">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="408a8-123">`System.Char.IsDigit(c)` renvoie `true` si `c` est un chiffre Unicode.</span><span class="sxs-lookup"><span data-stu-id="408a8-123">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
 <span data-ttu-id="408a8-124">Un `<regular_identifier>` ne peut pas être un mot-clé réservé.</span><span class="sxs-lookup"><span data-stu-id="408a8-124">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
 <span data-ttu-id="408a8-125">`<delimited_identifier>` correspond à toute chaîne placée entre crochets ([]).</span><span class="sxs-lookup"><span data-stu-id="408a8-125">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="408a8-126">Un crochet droit est représenté par deux crochets droits.</span><span class="sxs-lookup"><span data-stu-id="408a8-126">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="408a8-127">Voici quelques exemples de `<delimited_identifier>` :</span><span class="sxs-lookup"><span data-stu-id="408a8-127">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
 <span data-ttu-id="408a8-128">`<quoted_identifier>` correspond à toute chaîne placée entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="408a8-128">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="408a8-129">Un guillemet double dans l’identificateur est représenté par deux guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="408a8-129">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="408a8-130">Il est déconseillé d’utiliser des identificateurs entre guillemets, qui peuvent être facilement confondus avec une constante de chaîne.</span><span class="sxs-lookup"><span data-stu-id="408a8-130">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="408a8-131">Utilisez si possible un identificateur délimité.</span><span class="sxs-lookup"><span data-stu-id="408a8-131">Use a delimited identifier if possible.</span></span> <span data-ttu-id="408a8-132">Vous trouverez ci-dessous un exemple de `<quoted_identifier>` :</span><span class="sxs-lookup"><span data-stu-id="408a8-132">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="408a8-133">modèle</span><span class="sxs-lookup"><span data-stu-id="408a8-133">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="408a8-134">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-134">Remarks</span></span>
  
 <span data-ttu-id="408a8-135">`<pattern>` doit être une expression évaluée comme chaîne.</span><span class="sxs-lookup"><span data-stu-id="408a8-135">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="408a8-136">Il est utilisé comme modèle pour l’opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="408a8-136">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="408a8-137">Il peut contenir les caractères génériques suivants :</span><span class="sxs-lookup"><span data-stu-id="408a8-137">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="408a8-138">`%` : toute chaîne de zéro caractère ou plus.</span><span class="sxs-lookup"><span data-stu-id="408a8-138">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="408a8-139">`_` : n’importe quel caractère unique.</span><span class="sxs-lookup"><span data-stu-id="408a8-139">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="408a8-140">escape_char</span><span class="sxs-lookup"><span data-stu-id="408a8-140">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="408a8-141">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-141">Remarks</span></span>
  
 <span data-ttu-id="408a8-142">`<escape_char>` doit être une expression évaluée comme chaîne dont la longueur est 1.</span><span class="sxs-lookup"><span data-stu-id="408a8-142">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="408a8-143">Il est utilisé comme caractère d’échappement pour l’opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="408a8-143">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="408a8-144">Par exemple, `property LIKE 'ABC\%' ESCAPE '\'` correspond à `ABC%` au lieu d’une chaîne qui commence par `ABC`.</span><span class="sxs-lookup"><span data-stu-id="408a8-144">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="408a8-145">constant</span><span class="sxs-lookup"><span data-stu-id="408a8-145">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="408a8-146">Arguments</span><span class="sxs-lookup"><span data-stu-id="408a8-146">Arguments</span></span>  
  
-   <span data-ttu-id="408a8-147">`<integer_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et ne contient pas de décimales.</span><span class="sxs-lookup"><span data-stu-id="408a8-147">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="408a8-148">Les valeurs sont stockées en tant que `System.Int64` en interne et suivent la même plage.</span><span class="sxs-lookup"><span data-stu-id="408a8-148">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="408a8-149">Voici quelques exemples de constantes longues :</span><span class="sxs-lookup"><span data-stu-id="408a8-149">The following are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="408a8-150">`<decimal_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et qui contient une décimale.</span><span class="sxs-lookup"><span data-stu-id="408a8-150">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="408a8-151">Les valeurs sont stockées en tant que `System.Double` en interne et suivent la même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="408a8-151">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="408a8-152">Dans une version ultérieure, ce nombre pourrait être stocké dans un autre type de données pour prendre en charge la sémantique de nombre exacte. Vous n’aurez donc pas à compter sur le fait que le type de données sous-jacent soit `System.Double` pour `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="408a8-152">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="408a8-153">Voici quelques exemples de constantes décimales :</span><span class="sxs-lookup"><span data-stu-id="408a8-153">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="408a8-154">`<approximate_number_constant>` est un nombre écrit de manière scientifique.</span><span class="sxs-lookup"><span data-stu-id="408a8-154">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="408a8-155">Les valeurs sont stockées en tant que `System.Double` en interne et suivent la même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="408a8-155">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="408a8-156">Voici des exemples de constantes numériques approximatives :</span><span class="sxs-lookup"><span data-stu-id="408a8-156">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="408a8-157">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="408a8-157">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="408a8-158">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-158">Remarks</span></span>
  
<span data-ttu-id="408a8-159">Les constantes booléennes sont représentées par les mots clés `TRUE` ou `FALSE`.</span><span class="sxs-lookup"><span data-stu-id="408a8-159">Boolean constants are represented by the keywords `TRUE` or `FALSE`.</span></span> <span data-ttu-id="408a8-160">Les valeurs sont stockées en tant que `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="408a8-160">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="408a8-161">string_constant</span><span class="sxs-lookup"><span data-stu-id="408a8-161">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="408a8-162">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-162">Remarks</span></span>
  
<span data-ttu-id="408a8-163">Les constantes de chaîne sont placées entre guillemets simples et incluent tout caractère Unicode valide.</span><span class="sxs-lookup"><span data-stu-id="408a8-163">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="408a8-164">Un guillemet simple intégré à une constante de chaîne est représenté par deux guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="408a8-164">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="408a8-165">function</span><span class="sxs-lookup"><span data-stu-id="408a8-165">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="408a8-166">Remarques</span><span class="sxs-lookup"><span data-stu-id="408a8-166">Remarks</span></span>  

<span data-ttu-id="408a8-167">La fonction `newid()` renvoie un **System.Guid** généré par la méthode `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="408a8-167">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="408a8-168">La fonction `property(name)` renvoie la valeur de la propriété référencée par `name`.</span><span class="sxs-lookup"><span data-stu-id="408a8-168">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="408a8-169">La valeur `name` peut être toute expression valide renvoyant une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="408a8-169">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="408a8-170">Considérations</span><span class="sxs-lookup"><span data-stu-id="408a8-170">Considerations</span></span>

- <span data-ttu-id="408a8-171">SET est utilisé pour créer une nouvelle propriété ou mettre à jour la valeur d’une propriété existante.</span><span class="sxs-lookup"><span data-stu-id="408a8-171">SET is used to create a new property or update the value of an existing property.</span></span>
- <span data-ttu-id="408a8-172">REMOVE permet de supprimer une propriété.</span><span class="sxs-lookup"><span data-stu-id="408a8-172">REMOVE is used to remove a property.</span></span>
- <span data-ttu-id="408a8-173">SET effectue si possible une conversion implicite lorsque le type d’expression et le type de propriété existant sont différents.</span><span class="sxs-lookup"><span data-stu-id="408a8-173">SET performs implicit conversion if possible when the expression type and the existing property type are different.</span></span>
- <span data-ttu-id="408a8-174">L’action échoue s’il est fait référence à des propriétés de système inexistantes.</span><span class="sxs-lookup"><span data-stu-id="408a8-174">Action fails if non-existent system properties were referenced.</span></span>
- <span data-ttu-id="408a8-175">L’action réussit s’il est fait référence à des propriétés d’utilisateur inexistantes.</span><span class="sxs-lookup"><span data-stu-id="408a8-175">Action does not fail if non-existent user properties were referenced.</span></span>
- <span data-ttu-id="408a8-176">Une propriété d’utilisateur inexistante est évaluée comme « Inconnue » en interne, suivant la même sémantique que [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) lors de l’évaluation des opérateurs.</span><span class="sxs-lookup"><span data-stu-id="408a8-176">A non-existent user property is evaluated as "Unknown" internally, following the same semantics as [SQLFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) when evaluating operators.</span></span>

## <a name="next-steps"></a><span data-ttu-id="408a8-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="408a8-177">Next steps</span></span>

- [<span data-ttu-id="408a8-178">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="408a8-178">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)
- [<span data-ttu-id="408a8-179">Classe SqlFilter</span><span class="sxs-lookup"><span data-stu-id="408a8-179">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
