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
# <a name="sqlfilter-syntax"></a><span data-ttu-id="61368-103">Syntaxe SQLFilter</span><span class="sxs-lookup"><span data-stu-id="61368-103">SQLFilter syntax</span></span>

<span data-ttu-id="61368-104">A *SqlFilter* est une instance de hello [SqlFilter classe](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)et représente une expression de filtre basé sur le langage SQL qui est évaluée par rapport à un [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="61368-104">A *SqlFilter* is an instance of hello [SqlFilter class](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), and represents a SQL language-based filter expression that is evaluated against a [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="61368-105">Un SqlFilter prend en charge un sous-ensemble de la norme de hello SQL-92.</span><span class="sxs-lookup"><span data-stu-id="61368-105">A SqlFilter supports a subset of hello SQL-92 standard.</span></span>  
  
 <span data-ttu-id="61368-106">Cette rubrique répertorie les informations relatives à la syntaxe SQLFilter.</span><span class="sxs-lookup"><span data-stu-id="61368-106">This topic lists details about SqlFilter grammar.</span></span>  
  
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
  
## <a name="arguments"></a><span data-ttu-id="61368-107">Arguments</span><span class="sxs-lookup"><span data-stu-id="61368-107">Arguments</span></span>  
  
-   <span data-ttu-id="61368-108">`<scope>`est une chaîne facultative qui indique la portée hello Hello `<property_name>`.</span><span class="sxs-lookup"><span data-stu-id="61368-108">`<scope>` is an optional string indicating hello scope of hello `<property_name>`.</span></span> <span data-ttu-id="61368-109">Les valeurs autorisées sont `sys` ou `user`.</span><span class="sxs-lookup"><span data-stu-id="61368-109">Valid values are `sys` or `user`.</span></span> <span data-ttu-id="61368-110">Hello `sys` valeur indique l’étendue du système où `<property_name>` est un nom de propriété publique de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="61368-110">hello `sys` value indicates system scope where `<property_name>` is a public property name of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span></span> <span data-ttu-id="61368-111">`user`Indique la portée de l’utilisateur où `<property_name>` est une clé de hello [classe BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="61368-111">`user` indicates user scope where `<property_name>` is a key of hello [BrokeredMessage class](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) dictionary.</span></span> <span data-ttu-id="61368-112">`user`étendue est étendue par défaut de hello si `<scope>` n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="61368-112">`user` scope is hello default scope if `<scope>` is not specified.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="61368-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-113">Remarks</span></span>

<span data-ttu-id="61368-114">Une tentative tooaccess une propriété inexistante système est une erreur, lors d’une propriété de l’utilisateur tooaccess un inexistant tentative n’est pas une erreur.</span><span class="sxs-lookup"><span data-stu-id="61368-114">An attempt tooaccess a non-existent system property is an error, while an attempt tooaccess a non-existent user property is not an error.</span></span> <span data-ttu-id="61368-115">Au lieu de cela, une propriété d’utilisateur inexistante est évaluée en interne en tant que valeur inconnue.</span><span class="sxs-lookup"><span data-stu-id="61368-115">Instead, a non-existent user property is internally evaluated as an unknown value.</span></span> <span data-ttu-id="61368-116">Une valeur inconnue est traitée spécialement lors de l’évaluation de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="61368-116">An unknown value is treated specially during operator evaluation.</span></span>  
  
## <a name="propertyname"></a><span data-ttu-id="61368-117">property_name</span><span class="sxs-lookup"><span data-stu-id="61368-117">property_name</span></span>  
  
```  
<property_name> ::=  
     <identifier>  
     | <delimited_identifier>  
  
<identifier> ::=  
     <regular_identifier> | <quoted_identifier> | <delimited_identifier>  
  
```  
  
### <a name="arguments"></a><span data-ttu-id="61368-118">Arguments</span><span class="sxs-lookup"><span data-stu-id="61368-118">Arguments</span></span>  

 <span data-ttu-id="61368-119">`<regular_identifier>`est une chaîne représentée par hello suivant d’expression régulière :</span><span class="sxs-lookup"><span data-stu-id="61368-119">`<regular_identifier>` is a string represented by hello following regular expression:</span></span>  
  
```  
[[:IsLetter:]][_[:IsLetter:][:IsDigit:]]*  
```  
  
<span data-ttu-id="61368-120">Cela signifie toute chaîne commençant par une lettre et suivie par un(e) ou plusieurs traits de soulignement/lettres/chiffres.</span><span class="sxs-lookup"><span data-stu-id="61368-120">This grammar means any string that starts with a letter and is followed by one or more underscore/letter/digit.</span></span>  
  
<span data-ttu-id="61368-121">`[:IsLetter:]` signifie tout caractère Unicode classé en tant que lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="61368-121">`[:IsLetter:]` means any Unicode character that is categorized as a Unicode letter.</span></span> <span data-ttu-id="61368-122">`System.Char.IsLetter(c)` renvoie `true` si `c` est une lettre Unicode.</span><span class="sxs-lookup"><span data-stu-id="61368-122">`System.Char.IsLetter(c)` returns `true` if `c` is a Unicode letter.</span></span>  
  
<span data-ttu-id="61368-123">`[:IsDigit:]` signifie tout caractère Unicode classé en tant que chiffre décimal.</span><span class="sxs-lookup"><span data-stu-id="61368-123">`[:IsDigit:]` means any Unicode character that is categorized as a decimal digit.</span></span> <span data-ttu-id="61368-124">`System.Char.IsDigit(c)` renvoie `true` si `c` est un chiffre Unicode.</span><span class="sxs-lookup"><span data-stu-id="61368-124">`System.Char.IsDigit(c)` returns `true` if `c` is a Unicode digit.</span></span>  
  
<span data-ttu-id="61368-125">Un `<regular_identifier>` ne peut pas être un mot-clé réservé.</span><span class="sxs-lookup"><span data-stu-id="61368-125">A `<regular_identifier>` cannot be a reserved keyword.</span></span>  
  
<span data-ttu-id="61368-126">`<delimited_identifier>` correspond à toute chaîne placée entre crochets ([]).</span><span class="sxs-lookup"><span data-stu-id="61368-126">`<delimited_identifier>` is any string that is enclosed with left/right square brackets ([]).</span></span> <span data-ttu-id="61368-127">Un crochet droit est représenté par deux crochets droits.</span><span class="sxs-lookup"><span data-stu-id="61368-127">A right square bracket is represented as two right square brackets.</span></span> <span data-ttu-id="61368-128">Hello ci-dessous des exemples de `<delimited_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="61368-128">hello following are examples of `<delimited_identifier>`:</span></span>  
  
```  
[Property With Space]  
[HR-EmployeeID]  
  
```  
  
<span data-ttu-id="61368-129">`<quoted_identifier>` correspond à toute chaîne placée entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="61368-129">`<quoted_identifier>` is any string that is enclosed with double quotation marks.</span></span> <span data-ttu-id="61368-130">Un guillemet double dans l’identificateur est représenté par deux guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="61368-130">A double quotation mark in identifier is represented as two double quotation marks.</span></span> <span data-ttu-id="61368-131">Il est déconseillé de toouse des identificateurs entre guillemets, car elle peut facilement être confondue avec une constante de chaîne.</span><span class="sxs-lookup"><span data-stu-id="61368-131">It is not recommended toouse quoted identifiers because it can easily be confused with a string constant.</span></span> <span data-ttu-id="61368-132">Utilisez si possible un identificateur délimité.</span><span class="sxs-lookup"><span data-stu-id="61368-132">Use a delimited identifier if possible.</span></span> <span data-ttu-id="61368-133">Hello Voici un exemple de `<quoted_identifier>`:</span><span class="sxs-lookup"><span data-stu-id="61368-133">hello following is an example of `<quoted_identifier>`:</span></span>  
  
```  
"Contoso & Northwind"  
```  
  
## <a name="pattern"></a><span data-ttu-id="61368-134">modèle</span><span class="sxs-lookup"><span data-stu-id="61368-134">pattern</span></span>  
  
```  
<pattern> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="61368-135">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-135">Remarks</span></span>
  
<span data-ttu-id="61368-136">`<pattern>` doit être une expression évaluée comme chaîne.</span><span class="sxs-lookup"><span data-stu-id="61368-136">`<pattern>` must be an expression that is evaluated as a string.</span></span> <span data-ttu-id="61368-137">Il est utilisé comme modèle pour hello opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="61368-137">It is used as a pattern for hello LIKE operator.</span></span>      <span data-ttu-id="61368-138">Il peut contenir hello les caractères génériques suivants :</span><span class="sxs-lookup"><span data-stu-id="61368-138">It can contain hello following wildcard characters:</span></span>  
  
-   <span data-ttu-id="61368-139">`%` : toute chaîne de zéro caractère ou plus.</span><span class="sxs-lookup"><span data-stu-id="61368-139">`%`:  Any string of zero or more characters.</span></span>  
  
-   <span data-ttu-id="61368-140">`_` : n’importe quel caractère unique.</span><span class="sxs-lookup"><span data-stu-id="61368-140">`_`: Any single character.</span></span>  
  
## <a name="escapechar"></a><span data-ttu-id="61368-141">escape_char</span><span class="sxs-lookup"><span data-stu-id="61368-141">escape_char</span></span>  
  
```  
<escape_char> ::=  
      <expression>  
```  
  
### <a name="remarks"></a><span data-ttu-id="61368-142">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-142">Remarks</span></span>  

<span data-ttu-id="61368-143">`<escape_char>` doit être une expression évaluée comme chaîne dont la longueur est 1.</span><span class="sxs-lookup"><span data-stu-id="61368-143">`<escape_char>` must be an expression that is evaluated as a string of length 1.</span></span> <span data-ttu-id="61368-144">Il est utilisé comme caractère d’échappement pour hello opérateur LIKE.</span><span class="sxs-lookup"><span data-stu-id="61368-144">It is used as an escape character for hello LIKE operator.</span></span>  
  
 <span data-ttu-id="61368-145">Par exemple, `property LIKE 'ABC\%' ESCAPE '\'` correspond à `ABC%` au lieu d’une chaîne qui commence par `ABC`.</span><span class="sxs-lookup"><span data-stu-id="61368-145">For example, `property LIKE 'ABC\%' ESCAPE '\'` matches `ABC%` rather than a string that starts with `ABC`.</span></span>  
  
## <a name="constant"></a><span data-ttu-id="61368-146">constant</span><span class="sxs-lookup"><span data-stu-id="61368-146">constant</span></span>  
  
```  
<constant> ::=  
      <integer_constant> | <decimal_constant> | <approximate_number_constant> | <boolean_constant> | NULL  
```  
  
### <a name="arguments"></a><span data-ttu-id="61368-147">Arguments</span><span class="sxs-lookup"><span data-stu-id="61368-147">Arguments</span></span>  
  
-   <span data-ttu-id="61368-148">`<integer_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et ne contient pas de décimales.</span><span class="sxs-lookup"><span data-stu-id="61368-148">`<integer_constant>` is a string of numbers that are not enclosed in quotation marks and do not contain decimal points.</span></span> <span data-ttu-id="61368-149">les valeurs Hello sont stockées en tant que `System.Int64` en interne, et suivez hello même plage.</span><span class="sxs-lookup"><span data-stu-id="61368-149">hello values are stored as `System.Int64` internally, and follow hello same range.</span></span>  
  
     <span data-ttu-id="61368-150">Voici quelques exemples de constantes longues :</span><span class="sxs-lookup"><span data-stu-id="61368-150">These are examples of long constants:</span></span>  
  
    ```  
    1894  
    2  
    ```  
  
-   <span data-ttu-id="61368-151">`<decimal_constant>` est une chaîne de nombres qui n’est pas entourée de guillemets et qui contient une décimale.</span><span class="sxs-lookup"><span data-stu-id="61368-151">`<decimal_constant>` is a string of numbers that are not enclosed in quotation marks, and contain a decimal point.</span></span> <span data-ttu-id="61368-152">les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="61368-152">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span>  
  
     <span data-ttu-id="61368-153">Dans une version ultérieure, ce nombre peut être stocké dans des données différentes toosupport exacte numérique sémantique de type, donc vous fiez pas hello faits hello sous-jacent est de type de données `System.Double` pour `<decimal_constant>`.</span><span class="sxs-lookup"><span data-stu-id="61368-153">In a future version, this number might be stored in a different data type toosupport exact number semantics, so you should not rely on hello fact hello underlying data type is `System.Double` for `<decimal_constant>`.</span></span>  
  
     <span data-ttu-id="61368-154">Hello Voici des exemples de constantes décimales :</span><span class="sxs-lookup"><span data-stu-id="61368-154">hello following are examples of decimal constants:</span></span>  
  
    ```  
    1894.1204  
    2.0  
    ```  
  
-   <span data-ttu-id="61368-155">`<approximate_number_constant>` est un nombre écrit de manière scientifique.</span><span class="sxs-lookup"><span data-stu-id="61368-155">`<approximate_number_constant>` is a number written in scientific notation.</span></span> <span data-ttu-id="61368-156">les valeurs Hello sont stockées en tant que `System.Double` en interne et suivre hello même plage/précision.</span><span class="sxs-lookup"><span data-stu-id="61368-156">hello values are stored as `System.Double` internally, and follow hello same range/precision.</span></span> <span data-ttu-id="61368-157">Hello Voici des exemples de constantes de type numérique approximatifs :</span><span class="sxs-lookup"><span data-stu-id="61368-157">hello following are examples of approximate number constants:</span></span>  
  
    ```  
    101.5E5  
    0.5E-2  
    ```  
  
## <a name="booleanconstant"></a><span data-ttu-id="61368-158">boolean_constant</span><span class="sxs-lookup"><span data-stu-id="61368-158">boolean_constant</span></span>  
  
```  
<boolean_constant> :=  
      TRUE | FALSE  
```  
  
### <a name="remarks"></a><span data-ttu-id="61368-159">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-159">Remarks</span></span>  

<span data-ttu-id="61368-160">Constantes booléennes sont représentés par des mots clés de hello **TRUE** ou **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="61368-160">Boolean constants are represented by hello keywords **TRUE** or **FALSE**.</span></span> <span data-ttu-id="61368-161">les valeurs Hello sont stockées en tant que `System.Boolean`.</span><span class="sxs-lookup"><span data-stu-id="61368-161">hello values are stored as `System.Boolean`.</span></span>  
  
## <a name="stringconstant"></a><span data-ttu-id="61368-162">string_constant</span><span class="sxs-lookup"><span data-stu-id="61368-162">string_constant</span></span>  
  
```  
<string_constant>  
```  
  
### <a name="remarks"></a><span data-ttu-id="61368-163">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-163">Remarks</span></span>  

<span data-ttu-id="61368-164">Les constantes de chaîne sont placées entre guillemets simples et incluent tout caractère Unicode valide.</span><span class="sxs-lookup"><span data-stu-id="61368-164">String constants are enclosed in single quotation marks and include any valid Unicode characters.</span></span> <span data-ttu-id="61368-165">Un guillemet simple intégré à une constante de chaîne est représenté par deux guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="61368-165">A single quotation mark embedded in a string constant is represented as two single quotation marks.</span></span>  
  
## <a name="function"></a><span data-ttu-id="61368-166">function</span><span class="sxs-lookup"><span data-stu-id="61368-166">function</span></span>  
  
```  
<function> :=  
      newid() |  
      property(name) | p(name)  
```  
  
### <a name="remarks"></a><span data-ttu-id="61368-167">Remarques</span><span class="sxs-lookup"><span data-stu-id="61368-167">Remarks</span></span>
  
<span data-ttu-id="61368-168">Hello `newid()` fonction renvoie une **System.Guid** généré par hello `System.Guid.NewGuid()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="61368-168">hello `newid()` function returns a **System.Guid** generated by hello `System.Guid.NewGuid()` method.</span></span>  
  
<span data-ttu-id="61368-169">Hello `property(name)` fonction retourne la valeur hello de propriété hello référencée par `name`.</span><span class="sxs-lookup"><span data-stu-id="61368-169">hello `property(name)` function returns hello value of hello property referenced by `name`.</span></span> <span data-ttu-id="61368-170">Hello `name` valeur peut être toute expression valide qui retourne une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="61368-170">hello `name` value can be any valid expression that returns a string value.</span></span>  
  
## <a name="considerations"></a><span data-ttu-id="61368-171">Considérations</span><span class="sxs-lookup"><span data-stu-id="61368-171">Considerations</span></span>
  
<span data-ttu-id="61368-172">Tenez compte de hello suit [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) sémantique :</span><span class="sxs-lookup"><span data-stu-id="61368-172">Consider hello following [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) semantics:</span></span>  
  
-   <span data-ttu-id="61368-173">Les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="61368-173">Property names are case-insensitive.</span></span>  
  
-   <span data-ttu-id="61368-174">Les opérateurs suivent autant que possible la sémantique de conversion implicite C#.</span><span class="sxs-lookup"><span data-stu-id="61368-174">Operators follow C# implicit conversion semantics whenever possible.</span></span>  
  
-   <span data-ttu-id="61368-175">Les propriétés système sont des propriétés publiques exposées dans les instances [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage).</span><span class="sxs-lookup"><span data-stu-id="61368-175">System properties are public properties exposed in [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) instances.</span></span>  
  
    <span data-ttu-id="61368-176">Tenez compte de hello suit `IS [NOT] NULL` sémantique :</span><span class="sxs-lookup"><span data-stu-id="61368-176">Consider hello following `IS [NOT] NULL` semantics:</span></span>  
  
    -   <span data-ttu-id="61368-177">`property IS NULL`est évalué comme étant `true` si des propriétés hello n’existe ou hello la valeur de la propriété est `null`.</span><span class="sxs-lookup"><span data-stu-id="61368-177">`property IS NULL` is evaluated as `true` if either hello property doesn't exist or hello property's value is `null`.</span></span>  
  
### <a name="property-evaluation-semantics"></a><span data-ttu-id="61368-178">Sémantique d’évaluation de la propriété</span><span class="sxs-lookup"><span data-stu-id="61368-178">Property evaluation semantics</span></span>  
  
-   <span data-ttu-id="61368-179">Un tooevaluate tentative d’une propriété inexistante système lève un [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span><span class="sxs-lookup"><span data-stu-id="61368-179">An attempt tooevaluate a non-existent system property throws a [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) exception.</span></span>  
  
-   <span data-ttu-id="61368-180">Une propriété qui n’existe pas est évaluée en interne comme **inconnue**.</span><span class="sxs-lookup"><span data-stu-id="61368-180">A property that does not exist is internally evaluated as **unknown**.</span></span>  
  
 <span data-ttu-id="61368-181">Évaluation « inconnue » dans les opérateurs arithmétiques :</span><span class="sxs-lookup"><span data-stu-id="61368-181">Unknown evaluation in arithmetic operators:</span></span>  
  
-   <span data-ttu-id="61368-182">Pour les opérateurs binaires, si soit hello gauche et/ou droit des opérandes est évalué en tant que **inconnu**, puis le résultat de hello est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="61368-182">For binary operators, if either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
-   <span data-ttu-id="61368-183">Pour les opérateurs unaires, si un opérande est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="61368-183">For unary operators, if an operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="61368-184">Évaluation « inconnue » dans les opérateurs de comparaison binaires :</span><span class="sxs-lookup"><span data-stu-id="61368-184">Unknown evaluation in binary comparison operators:</span></span>  
  
-   <span data-ttu-id="61368-185">Si soit hello gauche et/ou droit des opérandes est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="61368-185">If either hello left and/or right side of operands is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="61368-186">Évaluation « inconnue » dans `[NOT] LIKE` :</span><span class="sxs-lookup"><span data-stu-id="61368-186">Unknown evaluation in `[NOT] LIKE`:</span></span>  
  
-   <span data-ttu-id="61368-187">Si n’importe quel opérande est évalué comme étant **inconnu**, puis le résultat de hello est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="61368-187">If any operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="61368-188">Évaluation « inconnue » dans `[NOT] IN` :</span><span class="sxs-lookup"><span data-stu-id="61368-188">Unknown evaluation in `[NOT] IN`:</span></span>  
  
-   <span data-ttu-id="61368-189">Si hello opérande de gauche est évaluée comme **inconnu**, puis le résultat de hello est **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="61368-189">If hello left operand is evaluated as **unknown**, then hello result is **unknown**.</span></span>  
  
 <span data-ttu-id="61368-190">Évaluation « inconnue » dans l’opérateur **AND** :</span><span class="sxs-lookup"><span data-stu-id="61368-190">Unknown evaluation in **AND** operator:</span></span>  
  
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
  
 <span data-ttu-id="61368-191">Évaluation « inconnue » dans l’opérateur **OR** :</span><span class="sxs-lookup"><span data-stu-id="61368-191">Unknown evaluation in **OR** operator:</span></span>  
  
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
  
### <a name="operator-binding-semantics"></a><span data-ttu-id="61368-192">Sémantique de liaison d’opérateur</span><span class="sxs-lookup"><span data-stu-id="61368-192">Operator binding semantics</span></span>
  
-   <span data-ttu-id="61368-193">Opérateurs de comparaison tels que `>`, `>=`, `<`, `<=`, `!=`, et `=` suivez hello même sémantique que l’opérateur hello c# de liaison de données de type promotions et conversions implicites.</span><span class="sxs-lookup"><span data-stu-id="61368-193">Comparison operators such as `>`, `>=`, `<`, `<=`, `!=`, and `=` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>  
  
-   <span data-ttu-id="61368-194">Les opérateurs arithmétiques tels que `+`, `-`, `*`, `/`, et `%` suivez hello même sémantique que l’opérateur hello c# de liaison de données de type promotions et conversions implicites.</span><span class="sxs-lookup"><span data-stu-id="61368-194">Arithmetic operators such as `+`, `-`, `*`, `/`, and `%` follow hello same semantics as hello C# operator binding in data type promotions and implicit conversions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61368-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61368-195">Next steps</span></span>

- [<span data-ttu-id="61368-196">Classe SqlFilter</span><span class="sxs-lookup"><span data-stu-id="61368-196">SQLFilter class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlfilter)
- [<span data-ttu-id="61368-197">Classe SQLRuleAction</span><span class="sxs-lookup"><span data-stu-id="61368-197">SQLRuleAction class</span></span>](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction)