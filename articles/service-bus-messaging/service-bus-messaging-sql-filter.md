---
title: "Informations de référence sur la syntaxe de SQLFilter dans Azure Service Bus | Microsoft Docs"
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
ms.openlocfilehash: 3aaec8f9b6a3bbcf814f771405c3b589de6f7ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sqlfilter-syntax"></a><span data-ttu-id="233d1-103">Syntaxe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="233d1-103">SQLFilter syntax</span></span>

<span data-ttu-id="233d1-104">*SqlFilter* est une instance de la [classe SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) et représente une expression de filtre basée sur le langage SQL évaluée par rapport à un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="233d1-104">A *SqlFilter* is an instance of the [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="233d1-105">L’instance SqlFilter prend en charge un sous-ensemble de la norme SQL-92.</span><span class="sxs-lookup"><span data-stu-id="233d1-105">A SqlFilter supports a subset of the SQL-92 standard.</span></span>  
  
 <span data-ttu-id="233d1-106">Cette rubrique répertorie les informations relatives à la syntaxe SQLFilter.</span><span class="sxs-lookup"><span data-stu-id="233d1-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="233d1-107">Arguments</span><span class="sxs-lookup"><span data-stu-id="233d1-107">Arguments</span></span>  
  
-   <span data-ttu-id="233d1-108">`<scope>` est une chaîne facultative qui indique la portée de `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="233d1-108">`<scope>` is an optional string indicating the scope of the `<property_name>`.</span></span> <span data-ttu-id="233d1-109">Les valeurs autorisées sont `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="233d1-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="233d1-110">La valeur `sys` indique la portée du système où `<property_name>` est un nom de propriété publique de la [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="233d1-110">The `sys` value indicates system scope where `<property_name>` is a public property name of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="233d1-111">`user` indique la portée de l’utilisateur où `<property_name>` est une clé du dictionnaire de la [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="233d1-111">`user` indicates user scope where `<property_name>` is a key of the [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="233d1-112">La portée de l’`user` est l’étendue par défaut si `<scope>` n’est pas défini.</span><span class="sxs-lookup"><span data-stu-id="233d1-112">`user` scope is the default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="233d1-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-113">Remarks</span></span>

<span data-ttu-id="233d1-114">Une tentative d’accès à une propriété inexistante du système est une erreur, tandis qu’une tentative d’accès à une propriété d’utilisateur inexistante n’est pas une erreur.</span><span class="sxs-lookup"><span data-stu-id="233d1-114">An attempt to access a non-existent system property is an error, while an attempt to access a non-existent user property is not an error.</span></span> <span data-ttu-id="233d1-115">Au lieu de cela, une propriété d’utilisateur inexistante est évaluée en interne en tant que valeur inconnue.</span><span class="sxs-lookup"><span data-stu-id="233d1-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="233d1-116">Une valeur inconnue est traitée spécialement lors de l’évaluation de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="233d1-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="233d1-117">property_name</span><span class="sxs-lookup"><span data-stu-id="233d1-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="233d1-118">Arguments</span><span class="sxs-lookup"><span data-stu-id="233d1-118">Arguments</span></span>  

 <span data-ttu-id="233d1-119">`<regular_identifier>` est une chaîne est représentée par l’expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="233d1-119">`<regular_identifier>` is a string represented by the following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="233d1-120">Cela signifie toute chaîne commençant par une lettre et suivie par un(e) ou plusieurs traits de soulignement/lettres/chiffres.</span><span class="sxs-lookup"><span data-stu-id="233d1-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="233d1-121">`[:IsLetter:]` signifie tout caractère Unicode classé en tant que lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="233d1-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="233d1-122">`System.Char.IsLetter(c)` renvoie `true` si `c` est une lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="233d1-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="233d1-123">`[:IsDigit:]` signifie tout caractère Unicode classé en tant que chiffre décimal.</span><span class="sxs-lookup"><span data-stu-id="233d1-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="233d1-124">`System.Char.IsDigit(c)` renvoie `true` si `c` est un chiffre Unicode.</span><span class="sxs-lookup"><span data-stu-id="233d1-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="233d1-125">Un `<regular_identifier>` ne peut pas être un mot-clé réservé.</span><span class="sxs-lookup"><span data-stu-id="233d1-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="233d1-126">`<delimited_identifier>` correspond à toute chaîne placée entre crochets ([]).</span><span class="sxs-lookup"><span data-stu-id="233d1-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="233d1-127">Un crochet droit est représenté par deux crochets droits.</span><span class="sxs-lookup"><span data-stu-id="233d1-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="233d1-128">Voici quelques exemples de `<delimited_identifier>` :</span><span class="sxs-lookup"><span data-stu-id="233d1-128">The following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="233d1-129">`<quoted_identifier>` correspond à toute chaîne placée entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="233d1-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="233d1-130">Un guillemet double dans l’identificateur est représenté par deux guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="233d1-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="233d1-131">Il est déconseillé d’utiliser des identificateurs entre guillemets, qui peuvent être facilement confondus avec une constante de chaîne.</span><span class="sxs-lookup"><span data-stu-id="233d1-131">It is not recommended to use quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="233d1-132">Utilisez si possible un identificateur délimité.</span><span class="sxs-lookup"><span data-stu-id="233d1-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="233d1-133">Vous trouverez ci-dessous un exemple de `<quoted_identifier>` :</span><span class="sxs-lookup"><span data-stu-id="233d1-133">The following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="233d1-134">modèle</span><span class="sxs-lookup"><span data-stu-id="233d1-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="233d1-135">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-135">Remarks</span></span>
  
<span data-ttu-id="233d1-136">`<pattern>` doit être une expression évaluée comme chaîne.</span><span class="sxs-lookup"><span data-stu-id="233d1-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="233d1-137">Il est utilisé comme modèle pour l’opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="233d1-137">It is used as a pattern for the LIKE operator.</span></span>      <span data-ttu-id="233d1-138">Il peut contenir les caractères génériques suivants :</span><span class="sxs-lookup"><span data-stu-id="233d1-138">It can contain the following wildcard characters:</span></span>  
  
-   <span data-ttu-id="233d1-139">`%` : toute chaîne de zéro caractère ou plus.</span><span class="sxs-lookup"><span data-stu-id="233d1-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="233d1-140">`_` : n’importe quel caractère unique.</span><span class="sxs-lookup"><span data-stu-id="233d1-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="233d1-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="233d1-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="233d1-142">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-142">Remarks</span></span>  

<span data-ttu-id="233d1-143">`<escape_char>` doit être une expression évaluée comme chaîne dont la longueur est 1.</span><span class="sxs-lookup"><span data-stu-id="233d1-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="233d1-144">Il est utilisé comme caractère d’échappement pour l’opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="233d1-144">It is used as an escape character for the LIKE operator.</span></span>  
  
 <span data-ttu-id="233d1-145">Par exemple, `property LIKE 'ABC\%' ESCAPE '\'` correspond à `ABC%` au lieu d’une chaîne qui commence par `ABC`.</span><span class="sxs-lookup"><span data-stu-id="233d1-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="233d1-146">constant</span><span class="sxs-lookup"><span data-stu-id="233d1-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="233d1-147">Arguments</span><span class="sxs-lookup"><span data-stu-id="233d1-147">Arguments</span></span>  
  
-   <span data-ttu-id="233d1-148">`<integer_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et ne contient pas de décimales.</span><span class="sxs-lookup"><span data-stu-id="233d1-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="233d1-149">Les valeurs sont stockées en tant que `System.Int64` en interne et suivent la même plage.</span><span class="sxs-lookup"><span data-stu-id="233d1-149">The values are stored as `System.Int64` internally, and follow the same range.</span></span>  
  
     <span data-ttu-id="233d1-150">Voici quelques exemples de constantes longues :</span><span class="sxs-lookup"><span data-stu-id="233d1-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="233d1-151">`<decimal_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et qui contient une décimale.</span><span class="sxs-lookup"><span data-stu-id="233d1-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="233d1-152">Les valeurs sont stockées en tant que `System.Double` en interne et suivent la même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="233d1-152">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span>  
  
     <span data-ttu-id="233d1-153">Dans une version ultérieure, ce nombre pourrait être stocké dans un autre type de données pour prendre en charge la sémantique de nombre exacte. Vous n’aurez donc pas à compter sur le fait que le type de données sous-jacent soit `System.Double` pour `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="233d1-153">In a future version, this number might be stored in a different data type to support exact number semantics, so you should not rely on the fact the underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="233d1-154">Voici quelques exemples de constantes décimales :</span><span class="sxs-lookup"><span data-stu-id="233d1-154">The following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="233d1-155">`<approximate_number_constant>` est un nombre écrit de manière scientifique.</span><span class="sxs-lookup"><span data-stu-id="233d1-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="233d1-156">Les valeurs sont stockées en tant que `System.Double` en interne et suivent la même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="233d1-156">The values are stored as `System.Double` internally, and follow the same range/precision.</span></span> <span data-ttu-id="233d1-157">Voici des exemples de constantes numériques approximatives :</span><span class="sxs-lookup"><span data-stu-id="233d1-157">The following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="233d1-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="233d1-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="233d1-159">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-159">Remarks</span></span>  

<span data-ttu-id="233d1-160">Les constantes booléennes sont représentées par les mots-clés **TRUE** ou **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="233d1-160">Boolean constants are represented by the keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="233d1-161">Les valeurs sont stockées en tant que `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="233d1-161">The values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="233d1-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="233d1-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="233d1-163">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-163">Remarks</span></span>  

<span data-ttu-id="233d1-164">Les constantes de chaîne sont placées entre guillemets simples et incluent tout caractère Unicode valide.</span><span class="sxs-lookup"><span data-stu-id="233d1-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="233d1-165">Un guillemet simple intégré à une constante de chaîne est représenté par deux guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="233d1-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="233d1-166">function</span><span class="sxs-lookup"><span data-stu-id="233d1-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="233d1-167">Remarques</span><span class="sxs-lookup"><span data-stu-id="233d1-167">Remarks</span></span>
  
<span data-ttu-id="233d1-168">La fonction `newid()` renvoie un **System.Guid** généré par la méthode `System.Guid.NewGuid()`.</span><span class="sxs-lookup"><span data-stu-id="233d1-168">The `newid()` function returns a **System.Guid** generated by the `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="233d1-169">La fonction `property(name)` renvoie la valeur de la propriété référencée par `name`.</span><span class="sxs-lookup"><span data-stu-id="233d1-169">The `property(name)` function returns the value of the property referenced by `name`.</span></span> <span data-ttu-id="233d1-170">La valeur `name` peut être toute expression valide renvoyant une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="233d1-170">The `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="233d1-171">Considérations</span><span class="sxs-lookup"><span data-stu-id="233d1-171">Considerations</span></span>
  
<span data-ttu-id="233d1-172">Tenez compte de la sémantique [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) suivante :</span><span class="sxs-lookup"><span data-stu-id="233d1-172">Consider the following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="233d1-173">Les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="233d1-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="233d1-174">Les opérateurs suivent autant que possible la sémantique de conversion implicite C#.</span><span class="sxs-lookup"><span data-stu-id="233d1-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="233d1-175">Les propriétés système sont des propriétés publiques exposées dans les instances [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="233d1-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="233d1-176">Examinez la sémantique `IS [NOT] NULL` suivante :</span><span class="sxs-lookup"><span data-stu-id="233d1-176">Consider the following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="233d1-177">`property IS NULL` est évalué comme `true` Si la propriété n’existe pas ou si la valeur de la propriété est `null`.</span><span class="sxs-lookup"><span data-stu-id="233d1-177">`property IS NULL` is evaluated as `true` if either the property doesn't exist or the property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="233d1-178">Sémantique d’évaluation de la propriété</span><span class="sxs-lookup"><span data-stu-id="233d1-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="233d1-179">Toute tentative pour évaluer une propriété de système qui n’existe pas lève une exception [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception).</span><span class="sxs-lookup"><span data-stu-id="233d1-179">An attempt to evaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="233d1-180">Une propriété qui n’existe pas est évaluée en interne comme **inconnue**.</span><span class="sxs-lookup"><span data-stu-id="233d1-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="233d1-181">Évaluation « inconnue » dans les opérateurs arithmétiques :</span><span class="sxs-lookup"><span data-stu-id="233d1-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="233d1-182">Pour les opérateurs binaires, si le côté gauche et/ou droit des opérandes est évalué comme **inconnu**, le résultat est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="233d1-182">For binary operators, if either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
-   <span data-ttu-id="233d1-183">Pour les opérateurs unaires, si un opérande est évalué comme **inconnu**, le résultat est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="233d1-183">For unary operators, if an operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="233d1-184">Évaluation « inconnue » dans les opérateurs de comparaison binaires :</span><span class="sxs-lookup"><span data-stu-id="233d1-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="233d1-185">Si l’opérande de gauche ou de droite est évalué comme **inconnu**, le résultat est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="233d1-185">If either the left and/or right side of operands is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="233d1-186">Évaluation « inconnue » dans `[NOT] LIKE` :</span><span class="sxs-lookup"><span data-stu-id="233d1-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="233d1-187">Si un opérande est évalué comme **inconnu**, le résultat est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="233d1-187">If any operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="233d1-188">Évaluation « inconnue » dans `[NOT] IN` :</span><span class="sxs-lookup"><span data-stu-id="233d1-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="233d1-189">Si l’opérande gauche est évalué comme **inconnu**, le résultat est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="233d1-189">If the left operand is evaluated as **unknown**, then the result is **unknown**.</span></span>  
  
 <span data-ttu-id="233d1-190">Évaluation « inconnue » dans l’opérateur **AND** :</span><span class="sxs-lookup"><span data-stu-id="233d1-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="233d1-191">Évaluation « inconnue » dans l’opérateur **OR** :</span><span class="sxs-lookup"><span data-stu-id="233d1-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="233d1-192">Sémantique de liaison d’opérateur</span><span class="sxs-lookup"><span data-stu-id="233d1-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="233d1-193">Les opérateurs de comparaison, tels que `>`, `>=`, `<`, `<=`, `!=`, et `=` suivent la même sémantique que la liaison d’opérateur C# dans les promotions de type de données et les conversions implicites.</span><span class="sxs-lookup"><span data-stu-id="233d1-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="233d1-194">Les opérateurs arithmétiques, tels que `+`, `-`, `*`, `/`, et `%` suivent la même sémantique que la liaison d’opérateur C# dans les promotions de type de données et les conversions implicites.</span><span class="sxs-lookup"><span data-stu-id="233d1-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow the same semantics as the C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="233d1-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="233d1-195">Next steps</span></span>

- [<span data-ttu-id="233d1-196">Classe SqlFilter</span><span class="sxs-lookup"><span data-stu-id="233d1-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="233d1-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="233d1-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)