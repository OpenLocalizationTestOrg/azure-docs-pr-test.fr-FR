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
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="94822-103">Construction de chaînes de filtrage pour hello Concepteur de tables</span><span class="sxs-lookup"><span data-stu-id="94822-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="94822-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="94822-104">Overview</span></span>
<span data-ttu-id="94822-105">toofilter des données dans une table Azure qui est affiché dans hello Visual Studio **Concepteur de tables**, créer une chaîne de filtrage et d’entrer dans le champ de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="94822-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="94822-106">syntaxe de la chaîne Hello filtre est défini par hello WCF Data Services et est semblable tooa clause SQL WHERE, mais est envoyé toohello service de Table via une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="94822-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="94822-107">Hello **Concepteur de tables** handles hello encodage pour vous, c’est le cas toofilter sur une valeur de propriété de votre choix, vous devez entrer uniquement le nom de propriété hello, opérateur de comparaison, valeur des critères, et éventuellement, un opérateur booléen dans hello filtrer champ.</span><span class="sxs-lookup"><span data-stu-id="94822-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="94822-108">Vous n’avez pas besoin de l’option de requête tooinclude hello $filter comme vous le feriez si vous construisiez une URL table de hello tooquery via hello [référence API REST des Services stockage](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="94822-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="94822-109">Hello WCF Data Services sont basés sur hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="94822-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="94822-110">Pour plus d’informations sur l’option de requête système hello filtre (**$filter**), consultez hello [spécifications OData URI Conventions](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="94822-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="94822-111">Opérateurs de comparaison</span><span class="sxs-lookup"><span data-stu-id="94822-111">Comparison Operators</span></span>
<span data-ttu-id="94822-112">Hello opérateurs logiques suivants sont pris en charge pour tous les types de propriété :</span><span class="sxs-lookup"><span data-stu-id="94822-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="94822-113">Opérateur logique</span><span class="sxs-lookup"><span data-stu-id="94822-113">Logical operator</span></span> | <span data-ttu-id="94822-114">Description</span><span class="sxs-lookup"><span data-stu-id="94822-114">Description</span></span> | <span data-ttu-id="94822-115">Exemple de chaîne de filtrage</span><span class="sxs-lookup"><span data-stu-id="94822-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94822-116">eq</span><span class="sxs-lookup"><span data-stu-id="94822-116">eq</span></span> |<span data-ttu-id="94822-117">Égal à</span><span class="sxs-lookup"><span data-stu-id="94822-117">Equal</span></span> |<span data-ttu-id="94822-118">Ville eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="94822-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="94822-119">gt</span><span class="sxs-lookup"><span data-stu-id="94822-119">gt</span></span> |<span data-ttu-id="94822-120">Supérieur à</span><span class="sxs-lookup"><span data-stu-id="94822-120">Greater than</span></span> |<span data-ttu-id="94822-121">Prix gt 20</span><span class="sxs-lookup"><span data-stu-id="94822-121">Price gt 20</span></span> |
| <span data-ttu-id="94822-122">ge</span><span class="sxs-lookup"><span data-stu-id="94822-122">ge</span></span> |<span data-ttu-id="94822-123">Supérieur ou égal trop</span><span class="sxs-lookup"><span data-stu-id="94822-123">Greater than or equal too</span></span>|<span data-ttu-id="94822-124">Prix ge 10</span><span class="sxs-lookup"><span data-stu-id="94822-124">Price ge 10</span></span> |
| <span data-ttu-id="94822-125">lt</span><span class="sxs-lookup"><span data-stu-id="94822-125">lt</span></span> |<span data-ttu-id="94822-126">Inférieur à</span><span class="sxs-lookup"><span data-stu-id="94822-126">Less than</span></span> |<span data-ttu-id="94822-127">Prix lt 20</span><span class="sxs-lookup"><span data-stu-id="94822-127">Price lt 20</span></span> |
| <span data-ttu-id="94822-128">le</span><span class="sxs-lookup"><span data-stu-id="94822-128">le</span></span> |<span data-ttu-id="94822-129">Inférieur ou égal à</span><span class="sxs-lookup"><span data-stu-id="94822-129">Less than or equal</span></span> |<span data-ttu-id="94822-130">Prix le 100</span><span class="sxs-lookup"><span data-stu-id="94822-130">Price le 100</span></span> |
| <span data-ttu-id="94822-131">ne</span><span class="sxs-lookup"><span data-stu-id="94822-131">ne</span></span> |<span data-ttu-id="94822-132">Non égal à</span><span class="sxs-lookup"><span data-stu-id="94822-132">Not equal</span></span> |<span data-ttu-id="94822-133">Ville ne 'Londres'</span><span class="sxs-lookup"><span data-stu-id="94822-133">City ne 'London'</span></span> |
| <span data-ttu-id="94822-134">and</span><span class="sxs-lookup"><span data-stu-id="94822-134">and</span></span> |<span data-ttu-id="94822-135">and</span><span class="sxs-lookup"><span data-stu-id="94822-135">And</span></span> |<span data-ttu-id="94822-136">Prix le 200 and prix gt 3,5</span><span class="sxs-lookup"><span data-stu-id="94822-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="94822-137">ou</span><span class="sxs-lookup"><span data-stu-id="94822-137">or</span></span> |<span data-ttu-id="94822-138">ou</span><span class="sxs-lookup"><span data-stu-id="94822-138">Or</span></span> |<span data-ttu-id="94822-139">Prix le 3,5 or prix gt 200</span><span class="sxs-lookup"><span data-stu-id="94822-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="94822-140">not</span><span class="sxs-lookup"><span data-stu-id="94822-140">not</span></span> |<span data-ttu-id="94822-141">not</span><span class="sxs-lookup"><span data-stu-id="94822-141">Not</span></span> |<span data-ttu-id="94822-142">not isAvailable</span><span class="sxs-lookup"><span data-stu-id="94822-142">not isAvailable</span></span> |

<span data-ttu-id="94822-143">Lors de la construction d’une chaîne de filtrage, hello règles suivantes sont importantes :</span><span class="sxs-lookup"><span data-stu-id="94822-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="94822-144">Utilisez hello opérateurs logiques toocompare une valeur de la propriété tooa.</span><span class="sxs-lookup"><span data-stu-id="94822-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="94822-145">Notez qu’il n’est pas possible de toocompare une valeur dynamique tooa de propriété ; côté « un » de l’expression de hello doit être une constante.</span><span class="sxs-lookup"><span data-stu-id="94822-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="94822-146">Toutes les parties de la chaîne de filtrage hello respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="94822-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="94822-147">valeur de constante Hello doit être de hello même type de propriété hello dans l’ordre des résultats valides de hello filtre tooreturn.</span><span class="sxs-lookup"><span data-stu-id="94822-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="94822-148">Pour plus d’informations sur les types de propriété pris en charge, consultez [hello de présentation des modèle de données de Service de Table](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="94822-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="94822-149">Filtrage par propriété de chaîne</span><span class="sxs-lookup"><span data-stu-id="94822-149">Filtering on String Properties</span></span>
<span data-ttu-id="94822-150">Lorsque vous filtrez sur les propriétés de chaîne, placez la constante de chaîne hello dans des guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="94822-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="94822-151">Hello suivant des exemples de filtres de hello **PartitionKey** et **RowKey** propriétés ; non clés supplémentaires propriétés peuvent également être ajoutées à chaîne de filtrage toohello :</span><span class="sxs-lookup"><span data-stu-id="94822-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="94822-152">Vous pouvez placer chaque expression de filtrage entre parenthèses, même si cela n’est pas obligatoire :</span><span class="sxs-lookup"><span data-stu-id="94822-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="94822-153">Notez que hello service de Table ne prend pas en charge les requêtes à caractères génériques, et elles ne sont pas prises en charge dans le Concepteur de tables de hello soit.</span><span class="sxs-lookup"><span data-stu-id="94822-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="94822-154">Toutefois, vous pouvez effectuer à l’aide des opérateurs de comparaison sur le préfixe de votre choix hello de correspondance de préfixe.</span><span class="sxs-lookup"><span data-stu-id="94822-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="94822-155">Hello exemple suivant retourne des entités avec une propriété LastName commençant par le lettre hello 'A' :</span><span class="sxs-lookup"><span data-stu-id="94822-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="94822-156">Filtrage par propriété numérique</span><span class="sxs-lookup"><span data-stu-id="94822-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="94822-157">toofilter sur un entier ou un nombre à virgule flottante, spécifiez le nombre hello sans guillemets.</span><span class="sxs-lookup"><span data-stu-id="94822-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="94822-158">Cet exemple retourne toutes les entités dont la propriété Age a une valeur supérieure à 30 :</span><span class="sxs-lookup"><span data-stu-id="94822-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="94822-159">Cet exemple retourne toutes les entités avec une propriété AmountDue dont la valeur est inférieur ou égal à too100.25 :</span><span class="sxs-lookup"><span data-stu-id="94822-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="94822-160">Filtrage par propriété booléenne</span><span class="sxs-lookup"><span data-stu-id="94822-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="94822-161">toofilter sur une valeur booléenne, spécifiez **true** ou **false** sans guillemets.</span><span class="sxs-lookup"><span data-stu-id="94822-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="94822-162">Hello exemple suivant retourne toutes les entités où hello propriété IsActive a la valeur trop**true**:</span><span class="sxs-lookup"><span data-stu-id="94822-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="94822-163">Vous pouvez également écrire cette expression de filtre sans opérateur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="94822-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="94822-164">Dans l’exemple suivant de hello, hello service de Table retournera également toutes les entités où IsActive est **true**:</span><span class="sxs-lookup"><span data-stu-id="94822-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="94822-165">tooreturn toutes les entités où IsActive est false, vous pouvez utiliser ne Hello pas opérateur :</span><span class="sxs-lookup"><span data-stu-id="94822-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="94822-166">Filtrage par propriété DateTime</span><span class="sxs-lookup"><span data-stu-id="94822-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="94822-167">toofilter sur une valeur DateTime, spécifiez hello **datetime** (mot clé), suivi d’une constante de date/heure hello dans des guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="94822-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="94822-168">constante de date/heure de Hello doit être au format UTC combiné, comme décrit dans [mise en forme des valeurs de propriété DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="94822-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="94822-169">Bonjour à l’exemple suivant retourne des entités où propriété CustomerSince de hello est égal tooJuly 10, 2008 :</span><span class="sxs-lookup"><span data-stu-id="94822-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
