---
title: "Azure AD Connect sync : Référence aux fonctions | Microsoft Docs"
description: "Référence d’expressions d’approvisionnement déclaratif dans Azure AD Connect Sync."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="8094d-103">Azure AD Connect Sync : Référence aux fonctions</span><span class="sxs-lookup"><span data-stu-id="8094d-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="8094d-104">Dans Azure AD Connect, les fonctions servent à manipuler une valeur d’attribut pendant la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="8094d-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="8094d-105">La syntaxe des fonctions s’exprime selon le format suivant : </span><span class="sxs-lookup"><span data-stu-id="8094d-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="8094d-106">Si une fonction est surchargée et accepte plusieurs syntaxes, toutes les syntaxes valides sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="8094d-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="8094d-107">Les fonctions sont fortement typées et vérifient que le type passé correspond au type documenté.</span><span class="sxs-lookup"><span data-stu-id="8094d-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="8094d-108">Une erreur est renvoyée si le type ne correspond pas.</span><span class="sxs-lookup"><span data-stu-id="8094d-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="8094d-109">Les types s’expriment avec la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="8094d-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="8094d-110">**bin** : binaire</span><span class="sxs-lookup"><span data-stu-id="8094d-110">**bin** – Binary</span></span>
* <span data-ttu-id="8094d-111">**bool** : booléen</span><span class="sxs-lookup"><span data-stu-id="8094d-111">**bool** – Boolean</span></span>
* <span data-ttu-id="8094d-112">**dt** : date/heure UTC</span><span class="sxs-lookup"><span data-stu-id="8094d-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="8094d-113">**enum** : énumération des constantes connues</span><span class="sxs-lookup"><span data-stu-id="8094d-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="8094d-114">**exp** : expression, qui est censée correspondre à une valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="8094d-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="8094d-115">**mvbin** : binaire à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="8094d-116">**mvstr** : chaîne à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="8094d-117">**mvref** : référence à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="8094d-118">**num** : numérique</span><span class="sxs-lookup"><span data-stu-id="8094d-118">**num** – Numeric</span></span>
* <span data-ttu-id="8094d-119">**ref** : référence</span><span class="sxs-lookup"><span data-stu-id="8094d-119">**ref** – Reference</span></span>
* <span data-ttu-id="8094d-120">**str** : chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-120">**str** – String</span></span>
* <span data-ttu-id="8094d-121">**var** : variante de (quasiment) tout autre type</span><span class="sxs-lookup"><span data-stu-id="8094d-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="8094d-122">**void** : ne retourne aucune valeur</span><span class="sxs-lookup"><span data-stu-id="8094d-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="8094d-123">Les fonctions ayant pour type **mvbin**, **mvstr** et **mvref** ne peuvent fonctionner que sur les attributs à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="8094d-124">Les fonctions avec **bin**, **str** et **ref** fonctionnent sur des attributs à valeur unique et à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="8094d-125">Référence des fonctions</span><span class="sxs-lookup"><span data-stu-id="8094d-125">Functions Reference</span></span>
| <span data-ttu-id="8094d-126">Liste des fonctions</span><span class="sxs-lookup"><span data-stu-id="8094d-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8094d-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="8094d-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="8094d-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="8094d-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="8094d-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="8094d-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="8094d-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="8094d-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="8094d-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="8094d-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="8094d-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="8094d-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="8094d-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="8094d-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="8094d-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="8094d-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="8094d-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8094d-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="8094d-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="8094d-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="8094d-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="8094d-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="8094d-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="8094d-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="8094d-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="8094d-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="8094d-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="8094d-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="8094d-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="8094d-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="8094d-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="8094d-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="8094d-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="8094d-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="8094d-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="8094d-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="8094d-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="8094d-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="8094d-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="8094d-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="8094d-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="8094d-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="8094d-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="8094d-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="8094d-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="8094d-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="8094d-150">**Conversion**</span><span class="sxs-lookup"><span data-stu-id="8094d-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="8094d-151">CBool</span><span class="sxs-lookup"><span data-stu-id="8094d-151">CBool</span></span>](#cbool) |[<span data-ttu-id="8094d-152">CDate</span><span class="sxs-lookup"><span data-stu-id="8094d-152">CDate</span></span>](#cdate) |[<span data-ttu-id="8094d-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="8094d-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="8094d-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="8094d-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="8094d-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="8094d-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8094d-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="8094d-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8094d-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="8094d-158">CNum</span><span class="sxs-lookup"><span data-stu-id="8094d-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="8094d-159">CRef</span><span class="sxs-lookup"><span data-stu-id="8094d-159">CRef</span></span>](#cref) |[<span data-ttu-id="8094d-160">CStr</span><span class="sxs-lookup"><span data-stu-id="8094d-160">CStr</span></span>](#cstr) |[<span data-ttu-id="8094d-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="8094d-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="8094d-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="8094d-163">**Date / Heure**</span><span class="sxs-lookup"><span data-stu-id="8094d-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="8094d-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="8094d-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="8094d-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="8094d-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="8094d-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="8094d-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="8094d-167">Now</span><span class="sxs-lookup"><span data-stu-id="8094d-167">Now</span></span>](#now) | |
| [<span data-ttu-id="8094d-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="8094d-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="8094d-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="8094d-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="8094d-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="8094d-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="8094d-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="8094d-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="8094d-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="8094d-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="8094d-173">**Evaluation**</span><span class="sxs-lookup"><span data-stu-id="8094d-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="8094d-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="8094d-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="8094d-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="8094d-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="8094d-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="8094d-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="8094d-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="8094d-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="8094d-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="8094d-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="8094d-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="8094d-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="8094d-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="8094d-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="8094d-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="8094d-182">IsString</span><span class="sxs-lookup"><span data-stu-id="8094d-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="8094d-183">**Mathématique**</span><span class="sxs-lookup"><span data-stu-id="8094d-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="8094d-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="8094d-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="8094d-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="8094d-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="8094d-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="8094d-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="8094d-187">**Multi-valued**</span><span class="sxs-lookup"><span data-stu-id="8094d-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="8094d-188">Contains</span><span class="sxs-lookup"><span data-stu-id="8094d-188">Contains</span></span>](#contains) |[<span data-ttu-id="8094d-189">Count</span><span class="sxs-lookup"><span data-stu-id="8094d-189">Count</span></span>](#count) |[<span data-ttu-id="8094d-190">Item</span><span class="sxs-lookup"><span data-stu-id="8094d-190">Item</span></span>](#item) |[<span data-ttu-id="8094d-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="8094d-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="8094d-192">Join</span><span class="sxs-lookup"><span data-stu-id="8094d-192">Join</span></span>](#join) |[<span data-ttu-id="8094d-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="8094d-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="8094d-194">Split</span><span class="sxs-lookup"><span data-stu-id="8094d-194">Split</span></span>](#split) | | |
| <span data-ttu-id="8094d-195">**Flux de programme**</span><span class="sxs-lookup"><span data-stu-id="8094d-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="8094d-196">Error</span><span class="sxs-lookup"><span data-stu-id="8094d-196">Error</span></span>](#error) |[<span data-ttu-id="8094d-197">IIF</span><span class="sxs-lookup"><span data-stu-id="8094d-197">IIF</span></span>](#iif) |[<span data-ttu-id="8094d-198">Sélection</span><span class="sxs-lookup"><span data-stu-id="8094d-198">Select</span></span>](#select) |[<span data-ttu-id="8094d-199">Switch</span><span class="sxs-lookup"><span data-stu-id="8094d-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="8094d-200">Where</span><span class="sxs-lookup"><span data-stu-id="8094d-200">Where</span></span>](#where) |[<span data-ttu-id="8094d-201">With</span><span class="sxs-lookup"><span data-stu-id="8094d-201">With</span></span>](#with) | | | |
| <span data-ttu-id="8094d-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="8094d-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="8094d-203">GUID</span><span class="sxs-lookup"><span data-stu-id="8094d-203">GUID</span></span>](#guid) |[<span data-ttu-id="8094d-204">InStr</span><span class="sxs-lookup"><span data-stu-id="8094d-204">InStr</span></span>](#instr) |[<span data-ttu-id="8094d-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="8094d-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="8094d-206">LCase</span><span class="sxs-lookup"><span data-stu-id="8094d-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="8094d-207">Left</span><span class="sxs-lookup"><span data-stu-id="8094d-207">Left</span></span>](#left) |[<span data-ttu-id="8094d-208">Len</span><span class="sxs-lookup"><span data-stu-id="8094d-208">Len</span></span>](#len) |[<span data-ttu-id="8094d-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="8094d-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="8094d-210">Mid</span><span class="sxs-lookup"><span data-stu-id="8094d-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="8094d-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="8094d-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="8094d-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="8094d-212">PadRight</span></span>](#padright) |[<span data-ttu-id="8094d-213">PCase</span><span class="sxs-lookup"><span data-stu-id="8094d-213">PCase</span></span>](#pcase) |[<span data-ttu-id="8094d-214">Replace</span><span class="sxs-lookup"><span data-stu-id="8094d-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="8094d-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="8094d-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="8094d-216">Right</span><span class="sxs-lookup"><span data-stu-id="8094d-216">Right</span></span>](#right) |[<span data-ttu-id="8094d-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="8094d-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="8094d-218">Trim</span><span class="sxs-lookup"><span data-stu-id="8094d-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="8094d-219">UCase</span><span class="sxs-lookup"><span data-stu-id="8094d-219">UCase</span></span>](#ucase) |[<span data-ttu-id="8094d-220">Word</span><span class="sxs-lookup"><span data-stu-id="8094d-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="8094d-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="8094d-221">BitAnd</span></span>
<span data-ttu-id="8094d-222">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-222">**Description:**</span></span>  
<span data-ttu-id="8094d-223">la fonction BitAnd définit des bits spécifiés sur une valeur.</span><span class="sxs-lookup"><span data-stu-id="8094d-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="8094d-224">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="8094d-225">value1, value2 : valeurs numériques qui doivent être liées par AND.</span><span class="sxs-lookup"><span data-stu-id="8094d-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="8094d-226">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-226">**Remarks:**</span></span>  
<span data-ttu-id="8094d-227">Cette fonction convertit les deux paramètres de la représentation binaire et définit un bit sur :</span><span class="sxs-lookup"><span data-stu-id="8094d-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="8094d-228">0 - si un des bits, ou les deux bits correspondants dans *masque* et *indicateur* ont pour valeur 0</span><span class="sxs-lookup"><span data-stu-id="8094d-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="8094d-229">1 - si les deux bits correspondants sont définis sur 1.</span><span class="sxs-lookup"><span data-stu-id="8094d-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="8094d-230">En d’autres termes, elle renvoie 0 dans tous les cas, sauf si les bits correspondants de ces deux paramètres sont définis sur 1.</span><span class="sxs-lookup"><span data-stu-id="8094d-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="8094d-231">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="8094d-232">Renvoie 7, car les valeurs hexadécimales « F » ET « F7 » donnent cette valeur.</span><span class="sxs-lookup"><span data-stu-id="8094d-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="8094d-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="8094d-233">BitOr</span></span>
<span data-ttu-id="8094d-234">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-234">**Description:**</span></span>  
<span data-ttu-id="8094d-235">La fonction BitOr définit des bits spécifiés sur une valeur.</span><span class="sxs-lookup"><span data-stu-id="8094d-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="8094d-236">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="8094d-237">value1, value2 : valeurs numériques qui doivent être liées par OR</span><span class="sxs-lookup"><span data-stu-id="8094d-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="8094d-238">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-238">**Remarks:**</span></span>  
<span data-ttu-id="8094d-239">Cette fonction convertit les deux paramètres en la représentation binaire et définit un bit sur 1 si l’un des bits ou les deux bits correspondants dans le masque et l’indicateur ont pour valeur 1, ou sur 0 si les deux bits correspondants ont la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="8094d-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="8094d-240">En d’autres termes, elle renvoie 1 dans tous les cas, sauf si les bits correspondants de ces deux paramètres ont pour valeur 0.</span><span class="sxs-lookup"><span data-stu-id="8094d-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="8094d-241">CBool</span><span class="sxs-lookup"><span data-stu-id="8094d-241">CBool</span></span>
<span data-ttu-id="8094d-242">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-242">**Description:**</span></span>  
<span data-ttu-id="8094d-243">La fonction CBool renvoie une valeur booléenne basée sur l’expression évaluée.</span><span class="sxs-lookup"><span data-stu-id="8094d-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="8094d-244">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="8094d-245">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-245">**Remarks:**</span></span>  
<span data-ttu-id="8094d-246">Si l’expression renvoie une valeur autre que zéro, CBool renvoie la valeur True, sinon elle renvoie False.</span><span class="sxs-lookup"><span data-stu-id="8094d-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="8094d-247">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="8094d-248">Retourne True si les attributs ont la même valeur.</span><span class="sxs-lookup"><span data-stu-id="8094d-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="8094d-249">CDate</span><span class="sxs-lookup"><span data-stu-id="8094d-249">CDate</span></span>
<span data-ttu-id="8094d-250">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-250">**Description:**</span></span>  
<span data-ttu-id="8094d-251">La fonction CDate renvoie une valeur DateTime UTC à partir d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="8094d-252">DateTime n’est pas un type d’attribut natif dans Sync, mais il est utilisé par certaines fonctions.</span><span class="sxs-lookup"><span data-stu-id="8094d-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="8094d-253">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="8094d-254">Valeur : chaîne comportant une date, une heure, et éventuellement, un fuseau horaire</span><span class="sxs-lookup"><span data-stu-id="8094d-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="8094d-255">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-255">**Remarks:**</span></span>  
<span data-ttu-id="8094d-256">La chaîne renvoyée est toujours au format UTC.</span><span class="sxs-lookup"><span data-stu-id="8094d-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="8094d-257">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="8094d-258">Renvoie une valeur DateTime à partir de l’heure de début de l’employé.</span><span class="sxs-lookup"><span data-stu-id="8094d-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="8094d-259">Renvoie une valeur DateTime représentant « 2013-01-11 12:00 AM ».</span><span class="sxs-lookup"><span data-stu-id="8094d-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="8094d-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="8094d-260">CertExtensionOids</span></span>
<span data-ttu-id="8094d-261">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-261">**Description:**</span></span>  
<span data-ttu-id="8094d-262">Retourne les valeurs OID de toutes les extensions critiques d’un objet certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="8094d-263">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="8094d-264">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-265">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="8094d-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="8094d-266">CertFormat</span></span>
<span data-ttu-id="8094d-267">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-267">**Description:**</span></span>  
<span data-ttu-id="8094d-268">Retourne le nom du format de ce certificat X.509v3.</span><span class="sxs-lookup"><span data-stu-id="8094d-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="8094d-269">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="8094d-270">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-271">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="8094d-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="8094d-272">CertFriendlyName</span></span>
<span data-ttu-id="8094d-273">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-273">**Description:**</span></span>  
<span data-ttu-id="8094d-274">Retourne l’alias associé à un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="8094d-275">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="8094d-276">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-277">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="8094d-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="8094d-278">CertHashString</span></span>
<span data-ttu-id="8094d-279">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-279">**Description:**</span></span>  
<span data-ttu-id="8094d-280">Retourne la valeur de hachage SHA1 du certificat x.509v.3 sous forme de chaîne hexadécimale.</span><span class="sxs-lookup"><span data-stu-id="8094d-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="8094d-281">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="8094d-282">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-283">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="8094d-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="8094d-284">CertIssuer</span></span>
<span data-ttu-id="8094d-285">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-285">**Description:**</span></span>  
<span data-ttu-id="8094d-286">Retourne le nom de l’autorité de certification qui a émis le certificat x.509v.3.</span><span class="sxs-lookup"><span data-stu-id="8094d-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="8094d-287">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="8094d-288">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-289">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="8094d-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="8094d-290">CertIssuerDN</span></span>
<span data-ttu-id="8094d-291">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-291">**Description:**</span></span>  
<span data-ttu-id="8094d-292">Retourne le nom unique de l’émetteur de certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="8094d-293">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="8094d-294">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-295">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="8094d-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="8094d-296">CertIssuerOid</span></span>
<span data-ttu-id="8094d-297">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-297">**Description:**</span></span>  
<span data-ttu-id="8094d-298">Retourne l’OID de l’émetteur de certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="8094d-299">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="8094d-300">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-301">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="8094d-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="8094d-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="8094d-303">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-303">**Description:**</span></span>  
<span data-ttu-id="8094d-304">Retourne les informations d’algorithme de clé du certificat x.509v.3 sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="8094d-305">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8094d-306">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-307">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="8094d-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="8094d-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="8094d-309">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-309">**Description:**</span></span>  
<span data-ttu-id="8094d-310">Retourne les paramètres d’algorithme de clé du certificat x.509v.3 sous forme de chaîne hexadécimale.</span><span class="sxs-lookup"><span data-stu-id="8094d-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="8094d-311">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8094d-312">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-313">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="8094d-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="8094d-314">CertNameInfo</span></span>
<span data-ttu-id="8094d-315">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-315">**Description:**</span></span>  
<span data-ttu-id="8094d-316">Retourne le nom du sujet et de l’émetteur d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="8094d-317">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="8094d-318">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-319">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="8094d-320">X509NameType : valeur X509NameType du sujet.</span><span class="sxs-lookup"><span data-stu-id="8094d-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="8094d-321">includesIssuerName : true pour inclure le nom de l’émetteur ; sinon, false.</span><span class="sxs-lookup"><span data-stu-id="8094d-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="8094d-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="8094d-322">CertNotAfter</span></span>
<span data-ttu-id="8094d-323">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-323">**Description:**</span></span>  
<span data-ttu-id="8094d-324">Retourne la date en heure locale après laquelle un certificat n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="8094d-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="8094d-325">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="8094d-326">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-327">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="8094d-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="8094d-328">CertNotBefore</span></span>
<span data-ttu-id="8094d-329">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-329">**Description:**</span></span>  
<span data-ttu-id="8094d-330">Retourne la date en heure locale à partir de laquelle un certificat devient valide.</span><span class="sxs-lookup"><span data-stu-id="8094d-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="8094d-331">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="8094d-332">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-333">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="8094d-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="8094d-334">CertPublicKeyOid</span></span>
<span data-ttu-id="8094d-335">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-335">**Description:**</span></span>  
<span data-ttu-id="8094d-336">Retourne l’OID de la clé publique du certificat x.509v.3.</span><span class="sxs-lookup"><span data-stu-id="8094d-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="8094d-337">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="8094d-338">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-339">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="8094d-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="8094d-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="8094d-341">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-341">**Description:**</span></span>  
<span data-ttu-id="8094d-342">Retourne l’OID des paramètres de clé publique du certificat x.509v.3.</span><span class="sxs-lookup"><span data-stu-id="8094d-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="8094d-343">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="8094d-344">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-345">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="8094d-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="8094d-346">CertSerialNumber</span></span>
<span data-ttu-id="8094d-347">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-347">**Description:**</span></span>  
<span data-ttu-id="8094d-348">Retourne le numéro de série du certificat X.509v3.</span><span class="sxs-lookup"><span data-stu-id="8094d-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="8094d-349">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="8094d-350">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-351">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="8094d-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="8094d-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="8094d-353">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-353">**Description:**</span></span>  
<span data-ttu-id="8094d-354">Retourne l’OID de l’algorithme utilisé pour créer la signature d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="8094d-355">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="8094d-356">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-357">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="8094d-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="8094d-358">CertSubject</span></span>
<span data-ttu-id="8094d-359">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-359">**Description:**</span></span>  
<span data-ttu-id="8094d-360">Obtient le nom unique du sujet du certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="8094d-361">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="8094d-362">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-363">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="8094d-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="8094d-364">CertSubjectNameDN</span></span>
<span data-ttu-id="8094d-365">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-365">**Description:**</span></span>  
<span data-ttu-id="8094d-366">Retourne le nom unique du sujet du certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="8094d-367">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="8094d-368">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-369">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="8094d-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="8094d-370">CertSubjectNameOid</span></span>
<span data-ttu-id="8094d-371">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-371">**Description:**</span></span>  
<span data-ttu-id="8094d-372">Retourne l’OID du nom du sujet d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="8094d-373">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="8094d-374">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-375">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="8094d-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="8094d-376">CertThumbprint</span></span>
<span data-ttu-id="8094d-377">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-377">**Description:**</span></span>  
<span data-ttu-id="8094d-378">Retourne l’empreinte d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="8094d-379">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8094d-380">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-381">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="8094d-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="8094d-382">CertVersion</span></span>
<span data-ttu-id="8094d-383">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-383">**Description:**</span></span>  
<span data-ttu-id="8094d-384">Retourne la version de format X.509 d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="8094d-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="8094d-385">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8094d-386">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-387">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="8094d-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-388">CGuid</span></span>
<span data-ttu-id="8094d-389">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-389">**Description:**</span></span>  
<span data-ttu-id="8094d-390">La fonction CGuid convertit la représentation sous forme de chaîne d’un GUID en sa représentation binaire.</span><span class="sxs-lookup"><span data-stu-id="8094d-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="8094d-391">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="8094d-392">Une chaîne rédigée au format suivant : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="8094d-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="8094d-393">Contains</span><span class="sxs-lookup"><span data-stu-id="8094d-393">Contains</span></span>
<span data-ttu-id="8094d-394">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-394">**Description:**</span></span>  
<span data-ttu-id="8094d-395">La fonction Contains détecte une chaîne à l’intérieur d’un attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="8094d-396">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-396">**Syntax:**</span></span>  
<span data-ttu-id="8094d-397">`num Contains (mvstring attribute, str search)` - sensible à la casse</span><span class="sxs-lookup"><span data-stu-id="8094d-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="8094d-398">`num Contains (mvref attribute, str search)` - sensible à la casse</span><span class="sxs-lookup"><span data-stu-id="8094d-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="8094d-399">attribut : attribut à valeurs multiples à rechercher.</span><span class="sxs-lookup"><span data-stu-id="8094d-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="8094d-400">recherche : chaîne à rechercher dans l’attribut.</span><span class="sxs-lookup"><span data-stu-id="8094d-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="8094d-401">Casetype : CaseInsensitive ou CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="8094d-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="8094d-402">Renvoie l’indice dans l’attribut à plusieurs valeurs où la chaîne a été trouvée.</span><span class="sxs-lookup"><span data-stu-id="8094d-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="8094d-403">Si la chaîne est introuvable, la valeur renvoyée est 0.</span><span class="sxs-lookup"><span data-stu-id="8094d-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="8094d-404">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-404">**Remarks:**</span></span>  
<span data-ttu-id="8094d-405">Pour les attributs de chaîne à valeurs multiples, la recherche détecte des sous-chaînes dans les valeurs.</span><span class="sxs-lookup"><span data-stu-id="8094d-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="8094d-406">Pour les attributs de référence, la chaîne recherchée doit correspondre exactement à la valeur pour être considérée comme une correspondance.</span><span class="sxs-lookup"><span data-stu-id="8094d-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="8094d-407">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="8094d-408">Si l’attribut proxyAddresses a une adresse de messagerie principale (indiquée par « SMTP : »), cette fonction renvoie l’attribut proxyAddress. Sinon, elle renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="8094d-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="8094d-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="8094d-409">ConvertFromBase64</span></span>
<span data-ttu-id="8094d-410">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-410">**Description:**</span></span>  
<span data-ttu-id="8094d-411">La fonction ConvertFromBase64 convertit la valeur encodée en base64 en chaîne régulière.</span><span class="sxs-lookup"><span data-stu-id="8094d-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="8094d-412">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-412">**Syntax:**</span></span>  
<span data-ttu-id="8094d-413">`str ConvertFromBase64(str source)` - part du principe que l’encodage utilisé est Unicode</span><span class="sxs-lookup"><span data-stu-id="8094d-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="8094d-414">source : chaîne encodée Base64</span><span class="sxs-lookup"><span data-stu-id="8094d-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="8094d-415">En codage : Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="8094d-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="8094d-416">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="8094d-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="8094d-417">Les deux exemples renvoient «*Hello world!*»</span><span class="sxs-lookup"><span data-stu-id="8094d-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="8094d-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8094d-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="8094d-419">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-419">**Description:**</span></span>  
<span data-ttu-id="8094d-420">La fonction ConvertFromUTF8Hex convertit la valeur encodée hexadécimale UTF8 spécifiée en chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="8094d-421">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="8094d-422">source : chaîne encodée sur 2 octets UTF8</span><span class="sxs-lookup"><span data-stu-id="8094d-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="8094d-423">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-423">**Remarks:**</span></span>  
<span data-ttu-id="8094d-424">La différence entre cette fonction et ConvertFromBase64(,UTF8) est que le résultat est convivial pour l’attribut DN.</span><span class="sxs-lookup"><span data-stu-id="8094d-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="8094d-425">Ce format est utilisé par Azure Active Directory en tant que nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="8094d-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="8094d-426">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="8094d-427">Renvoie «*Hello world!*».</span><span class="sxs-lookup"><span data-stu-id="8094d-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="8094d-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="8094d-428">ConvertToBase64</span></span>
<span data-ttu-id="8094d-429">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-429">**Description:**</span></span>  
<span data-ttu-id="8094d-430">La fonction ConvertToBase64 convertit une chaîne en chaîne Unicode base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="8094d-431">Convertit la valeur d’un tableau d’entiers en sa représentation sous forme de chaîne équivalente encodée avec des chiffres en base 64.</span><span class="sxs-lookup"><span data-stu-id="8094d-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="8094d-432">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="8094d-433">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="8094d-434">Renvoie « SABlAGwAbABvACAAdwBvAHIAbABkACEA ».</span><span class="sxs-lookup"><span data-stu-id="8094d-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="8094d-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="8094d-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="8094d-436">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-436">**Description:**</span></span>  
<span data-ttu-id="8094d-437">La fonction ConvertToUTF8Hex convertit une chaîne en valeur hexadécimale encodée UTF8.</span><span class="sxs-lookup"><span data-stu-id="8094d-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="8094d-438">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="8094d-439">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-439">**Remarks:**</span></span>  
<span data-ttu-id="8094d-440">Le format de sortie de cette fonction est utilisé par Azure Active Directory en tant que format d’attribut de nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="8094d-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="8094d-441">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="8094d-442">Renvoie 48656C6C6F20776F726C6421.</span><span class="sxs-lookup"><span data-stu-id="8094d-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="8094d-443">Count</span><span class="sxs-lookup"><span data-stu-id="8094d-443">Count</span></span>
<span data-ttu-id="8094d-444">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-444">**Description:**</span></span>  
<span data-ttu-id="8094d-445">La fonction Count renvoie le nombre d’éléments dans un attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="8094d-446">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="8094d-447">CNum</span><span class="sxs-lookup"><span data-stu-id="8094d-447">CNum</span></span>
<span data-ttu-id="8094d-448">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-448">**Description:**</span></span>  
<span data-ttu-id="8094d-449">La fonction CNum prend une chaîne et renvoie un type de données numérique.</span><span class="sxs-lookup"><span data-stu-id="8094d-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="8094d-450">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="8094d-451">CRef</span><span class="sxs-lookup"><span data-stu-id="8094d-451">CRef</span></span>
<span data-ttu-id="8094d-452">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-452">**Description:**</span></span>  
<span data-ttu-id="8094d-453">Convertit une chaîne en attribut de référence.</span><span class="sxs-lookup"><span data-stu-id="8094d-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="8094d-454">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="8094d-455">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="8094d-456">CStr</span><span class="sxs-lookup"><span data-stu-id="8094d-456">CStr</span></span>
<span data-ttu-id="8094d-457">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-457">**Description:**</span></span>  
<span data-ttu-id="8094d-458">La fonction CStr convertit en un type de données de chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="8094d-459">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="8094d-460">valeur : peut être une valeur numérique, un attribut de référence ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="8094d-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="8094d-461">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="8094d-462">Peut renvoyer « cn=Joe,dc=contoso,dc=com ».</span><span class="sxs-lookup"><span data-stu-id="8094d-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="8094d-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="8094d-463">DateAdd</span></span>
<span data-ttu-id="8094d-464">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-464">**Description:**</span></span>  
<span data-ttu-id="8094d-465">Renvoie un objet Date contenant une date à laquelle un intervalle de temps spécifié a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="8094d-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="8094d-466">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="8094d-467">intervalle : expression de chaîne correspondant l’intervalle de temps que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="8094d-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="8094d-468">La chaîne doit avoir une des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8094d-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="8094d-469">yyyy Année</span><span class="sxs-lookup"><span data-stu-id="8094d-469">yyyy Year</span></span>
  * <span data-ttu-id="8094d-470">q Trimestre</span><span class="sxs-lookup"><span data-stu-id="8094d-470">q Quarter</span></span>
  * <span data-ttu-id="8094d-471">m Mois</span><span class="sxs-lookup"><span data-stu-id="8094d-471">m Month</span></span>
  * <span data-ttu-id="8094d-472">y Jour de l’année</span><span class="sxs-lookup"><span data-stu-id="8094d-472">y Day of year</span></span>
  * <span data-ttu-id="8094d-473">s Jour</span><span class="sxs-lookup"><span data-stu-id="8094d-473">d Day</span></span>
  * <span data-ttu-id="8094d-474">w Jour de la semaine</span><span class="sxs-lookup"><span data-stu-id="8094d-474">w Weekday</span></span>
  * <span data-ttu-id="8094d-475">ww Semaine</span><span class="sxs-lookup"><span data-stu-id="8094d-475">ww Week</span></span>
  * <span data-ttu-id="8094d-476">h Heure</span><span class="sxs-lookup"><span data-stu-id="8094d-476">h Hour</span></span>
  * <span data-ttu-id="8094d-477">n Minute</span><span class="sxs-lookup"><span data-stu-id="8094d-477">n Minute</span></span>
  * <span data-ttu-id="8094d-478">s Seconde</span><span class="sxs-lookup"><span data-stu-id="8094d-478">s Second</span></span>
* <span data-ttu-id="8094d-479">valeur : nombre d’unités que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="8094d-479">value: The number of units you want to add.</span></span> <span data-ttu-id="8094d-480">Elle peut être positive (pour obtenir des dates dans le futur) ou négative (pour obtenir des dates dans le passé).</span><span class="sxs-lookup"><span data-stu-id="8094d-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="8094d-481">date : DateTime représentant la date à laquelle l’intervalle est ajouté.</span><span class="sxs-lookup"><span data-stu-id="8094d-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="8094d-482">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="8094d-483">Ajoute 3 mois et renvoie une valeur DateTime représentant « 2001-04-01 ».</span><span class="sxs-lookup"><span data-stu-id="8094d-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="8094d-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="8094d-484">DateFromNum</span></span>
<span data-ttu-id="8094d-485">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-485">**Description:**</span></span>  
<span data-ttu-id="8094d-486">La fonction DateFromNum convertit une valeur au format de date AD en un type DateTime.</span><span class="sxs-lookup"><span data-stu-id="8094d-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="8094d-487">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="8094d-488">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="8094d-489">Renvoie une valeur DateTime représentant 2012-01-01 23:00:00.</span><span class="sxs-lookup"><span data-stu-id="8094d-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="8094d-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="8094d-490">DNComponent</span></span>
<span data-ttu-id="8094d-491">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-491">**Description:**</span></span>  
<span data-ttu-id="8094d-492">La fonction DNComponent renvoie la valeur d’un composant de nom de domaine spécifié en partant de la gauche.</span><span class="sxs-lookup"><span data-stu-id="8094d-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="8094d-493">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="8094d-494">dn : attribut de référence à interpréter</span><span class="sxs-lookup"><span data-stu-id="8094d-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="8094d-495">ComponentNumber : composant du nom de domaine à renvoyer</span><span class="sxs-lookup"><span data-stu-id="8094d-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="8094d-496">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="8094d-497">Si dn est « cn=Joe,ou=… », la fonction renvoie Joe.</span><span class="sxs-lookup"><span data-stu-id="8094d-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="8094d-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="8094d-498">DNComponentRev</span></span>
<span data-ttu-id="8094d-499">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-499">**Description:**</span></span>  
<span data-ttu-id="8094d-500">La fonction DNComponentRev renvoie la valeur d’un composant de nom de domaine spécifié en partant de la droite (fin).</span><span class="sxs-lookup"><span data-stu-id="8094d-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="8094d-501">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="8094d-502">dn : attribut de référence à interpréter</span><span class="sxs-lookup"><span data-stu-id="8094d-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="8094d-503">ComponentNumber - composant du nom de domaine à retourner</span><span class="sxs-lookup"><span data-stu-id="8094d-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="8094d-504">Options : contrôleur de domaine – ignorer tous les composants avec « dc = »</span><span class="sxs-lookup"><span data-stu-id="8094d-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="8094d-505">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-505">**Example:**</span></span>  
<span data-ttu-id="8094d-506">Si le nom de domaine est « cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com », alors</span><span class="sxs-lookup"><span data-stu-id="8094d-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="8094d-507">Renvoient US.</span><span class="sxs-lookup"><span data-stu-id="8094d-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="8094d-508">Error</span><span class="sxs-lookup"><span data-stu-id="8094d-508">Error</span></span>
<span data-ttu-id="8094d-509">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-509">**Description:**</span></span>  
<span data-ttu-id="8094d-510">La fonction Error sert à renvoyer une erreur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8094d-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="8094d-511">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="8094d-512">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="8094d-513">Si l’attribut accountName n’est pas présent, renvoie une erreur sur l’objet.</span><span class="sxs-lookup"><span data-stu-id="8094d-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="8094d-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="8094d-514">EscapeDNComponent</span></span>
<span data-ttu-id="8094d-515">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-515">**Description:**</span></span>  
<span data-ttu-id="8094d-516">La fonction EscapeDNComponent prend un composant de nom de domaine et l’isole pour qu’il puisse être représenté dans l’annuaire LDAP.</span><span class="sxs-lookup"><span data-stu-id="8094d-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="8094d-517">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="8094d-518">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="8094d-519">Permet de s’assurer que l’objet peut être créé dans un annuaire LDAP, même si l’attribut displayName comporte des caractères d’échappement dans LDAP.</span><span class="sxs-lookup"><span data-stu-id="8094d-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="8094d-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="8094d-520">FormatDateTime</span></span>
<span data-ttu-id="8094d-521">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-521">**Description:**</span></span>  
<span data-ttu-id="8094d-522">La fonction FormatDateTime sert à mettre en forme une valeur DateTime en chaîne dans le format spécifié.</span><span class="sxs-lookup"><span data-stu-id="8094d-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="8094d-523">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="8094d-524">valeur : valeur au format DateTime</span><span class="sxs-lookup"><span data-stu-id="8094d-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="8094d-525">format : chaîne représentant le format à convertir.</span><span class="sxs-lookup"><span data-stu-id="8094d-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="8094d-526">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-526">**Remarks:**</span></span>  
<span data-ttu-id="8094d-527">Vous trouverez les valeurs de format possibles ici : [Formats de date/heure définis par l’utilisateur (fonction Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="8094d-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="8094d-528">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="8094d-529">Renvoie comme résultat « 2007-12-25 ».</span><span class="sxs-lookup"><span data-stu-id="8094d-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="8094d-530">Peut donner comme résultat « 20140905081453.0Z ».</span><span class="sxs-lookup"><span data-stu-id="8094d-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="8094d-531">GUID</span><span class="sxs-lookup"><span data-stu-id="8094d-531">GUID</span></span>
<span data-ttu-id="8094d-532">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-532">**Description:**</span></span>  
<span data-ttu-id="8094d-533">La fonction GUID génère un nouveau GUID aléatoire.</span><span class="sxs-lookup"><span data-stu-id="8094d-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="8094d-534">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="8094d-535">IIF</span><span class="sxs-lookup"><span data-stu-id="8094d-535">IIF</span></span>
<span data-ttu-id="8094d-536">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-536">**Description:**</span></span>  
<span data-ttu-id="8094d-537">La fonction IIF renvoie une valeur parmi un ensemble de valeurs possibles en fonction d’une condition spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8094d-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="8094d-538">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="8094d-539">condition : toute valeur ou expression qui peut être évaluée à true ou false.</span><span class="sxs-lookup"><span data-stu-id="8094d-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="8094d-540">valueIfTrue : la valeur renvoyée si la condition prend la valeur true.</span><span class="sxs-lookup"><span data-stu-id="8094d-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="8094d-541">valueIfFalse : la valeur renvoyée si la condition prend la valeur false.</span><span class="sxs-lookup"><span data-stu-id="8094d-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="8094d-542">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="8094d-543">Renvoie l’alias d’un utilisateur avec le préfixe « t- » si l’utilisateur est stagiaire. Sinon, l’alias reste inchangé.</span><span class="sxs-lookup"><span data-stu-id="8094d-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="8094d-544">InStr</span><span class="sxs-lookup"><span data-stu-id="8094d-544">InStr</span></span>
<span data-ttu-id="8094d-545">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-545">**Description:**</span></span>  
<span data-ttu-id="8094d-546">La fonction InStr recherche la première occurrence d’une sous-chaîne dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="8094d-547">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="8094d-548">stringcheck : chaîne à rechercher</span><span class="sxs-lookup"><span data-stu-id="8094d-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="8094d-549">stringmatch : chaîne à trouver</span><span class="sxs-lookup"><span data-stu-id="8094d-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="8094d-550">start : position de départ pour trouver la sous-chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="8094d-551">compare : vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="8094d-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="8094d-552">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-552">**Remarks:**</span></span>  
<span data-ttu-id="8094d-553">Renvoie la position à laquelle la sous-chaîne a été trouvée, ou 0 si elle est introuvable.</span><span class="sxs-lookup"><span data-stu-id="8094d-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="8094d-554">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="8094d-555">Prend la valeur 5.</span><span class="sxs-lookup"><span data-stu-id="8094d-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="8094d-556">Prend la valeur 7.</span><span class="sxs-lookup"><span data-stu-id="8094d-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="8094d-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="8094d-557">InStrRev</span></span>
<span data-ttu-id="8094d-558">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-558">**Description:**</span></span>  
<span data-ttu-id="8094d-559">La fonction InStrRev recherche la dernière occurrence d’une sous-chaîne dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="8094d-560">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="8094d-561">stringcheck : chaîne à rechercher</span><span class="sxs-lookup"><span data-stu-id="8094d-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="8094d-562">stringmatch : chaîne à trouver</span><span class="sxs-lookup"><span data-stu-id="8094d-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="8094d-563">start : position de départ pour trouver la sous-chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="8094d-564">compare : vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="8094d-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="8094d-565">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-565">**Remarks:**</span></span>  
<span data-ttu-id="8094d-566">Renvoie la position à laquelle la sous-chaîne a été trouvée, ou 0 si elle est introuvable.</span><span class="sxs-lookup"><span data-stu-id="8094d-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="8094d-567">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="8094d-568">Renvoie 7.</span><span class="sxs-lookup"><span data-stu-id="8094d-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="8094d-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="8094d-569">IsBitSet</span></span>
<span data-ttu-id="8094d-570">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-570">**Description:**</span></span>  
<span data-ttu-id="8094d-571">La fonction IsBitSet vérifie si un bit est ou non défini.</span><span class="sxs-lookup"><span data-stu-id="8094d-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="8094d-572">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="8094d-573">value : valeur numérique évaluée. flag : valeur numérique contenant le bit à évaluer</span><span class="sxs-lookup"><span data-stu-id="8094d-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="8094d-574">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="8094d-575">Renvoie True, car le bit « 4 » est défini dans la valeur hexadécimale « F ».</span><span class="sxs-lookup"><span data-stu-id="8094d-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="8094d-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="8094d-576">IsDate</span></span>
<span data-ttu-id="8094d-577">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-577">**Description:**</span></span>  
<span data-ttu-id="8094d-578">La fonction IsDate prend la valeur True si l’expression peut être évaluée à un type DateTime.</span><span class="sxs-lookup"><span data-stu-id="8094d-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="8094d-579">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="8094d-580">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-580">**Remarks:**</span></span>  
<span data-ttu-id="8094d-581">Permet de déterminer si CDate() peut aboutir.</span><span class="sxs-lookup"><span data-stu-id="8094d-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="8094d-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="8094d-582">IsCert</span></span>
<span data-ttu-id="8094d-583">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-583">**Description:**</span></span>  
<span data-ttu-id="8094d-584">Retourne la valeur true si les données brutes peuvent être sérialisées en un objet certificat .NET X509Certificate2.</span><span class="sxs-lookup"><span data-stu-id="8094d-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="8094d-585">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="8094d-586">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="8094d-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="8094d-587">Le tableau d’octets peut contenir des données X.509 codées en binaire (DER) ou en Base64.</span><span class="sxs-lookup"><span data-stu-id="8094d-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="8094d-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="8094d-588">IsEmpty</span></span>
<span data-ttu-id="8094d-589">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-589">**Description:**</span></span>  
<span data-ttu-id="8094d-590">La fonction IsEmpty prend la valeur True si l’attribut est présent dans CS ou MV mais qu’il est évalué à une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="8094d-591">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="8094d-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-592">IsGuid</span></span>
<span data-ttu-id="8094d-593">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-593">**Description:**</span></span>  
<span data-ttu-id="8094d-594">La fonction IsGuid renvoie la valeur True si la chaîne peut être convertie en GUID.</span><span class="sxs-lookup"><span data-stu-id="8094d-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="8094d-595">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="8094d-596">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-596">**Remarks:**</span></span>  
<span data-ttu-id="8094d-597">Un GUID est défini en tant que chaîne en fonction de l’un de ces modèles : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.</span><span class="sxs-lookup"><span data-stu-id="8094d-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="8094d-598">Utilisé pour déterminer si CGuid() peut aboutir.</span><span class="sxs-lookup"><span data-stu-id="8094d-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="8094d-599">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="8094d-600">Si StrAttribute est au format GUID, renvoie une représentation binaire. Sinon, renvoie la valeur Null.</span><span class="sxs-lookup"><span data-stu-id="8094d-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="8094d-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="8094d-601">IsNull</span></span>
<span data-ttu-id="8094d-602">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-602">**Description:**</span></span>  
<span data-ttu-id="8094d-603">La fonction IsNull renvoie true si l’expression correspond à la valeur Null.</span><span class="sxs-lookup"><span data-stu-id="8094d-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="8094d-604">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="8094d-605">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-605">**Remarks:**</span></span>  
<span data-ttu-id="8094d-606">Dans le cas d’un attribut, la valeur Null est exprimée par l’absence de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="8094d-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="8094d-607">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="8094d-608">Renvoie True si l’attribut est absent dans CS ou MV.</span><span class="sxs-lookup"><span data-stu-id="8094d-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="8094d-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="8094d-609">IsNullOrEmpty</span></span>
<span data-ttu-id="8094d-610">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-610">**Description:**</span></span>  
<span data-ttu-id="8094d-611">La fonction IsNullOrEmpty renvoie la valeur true si l’expression a pour valeur Null ou s’il s’agit d’une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="8094d-612">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="8094d-613">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-613">**Remarks:**</span></span>  
<span data-ttu-id="8094d-614">Dans le cas d’un attribut, cela donne la valeur True si l’attribut est absent ou est présent mais qu’il s’agit d’une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="8094d-615">L’inverse de cette fonction est nommé IsPresent.</span><span class="sxs-lookup"><span data-stu-id="8094d-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="8094d-616">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="8094d-617">Renvoie True si l’attribut est absent dans CS ou MV ou s’il s’agit d’une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="8094d-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="8094d-618">IsNumeric</span></span>
<span data-ttu-id="8094d-619">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-619">**Description:**</span></span>  
<span data-ttu-id="8094d-620">La fonction IsNumeric renvoie une valeur booléenne indiquant si une expression peut être évaluée en tant que type de nombre.</span><span class="sxs-lookup"><span data-stu-id="8094d-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="8094d-621">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="8094d-622">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-622">**Remarks:**</span></span>  
<span data-ttu-id="8094d-623">Permet de déterminer si CNum() peut parvenir à analyser l’expression.</span><span class="sxs-lookup"><span data-stu-id="8094d-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="8094d-624">IsString</span><span class="sxs-lookup"><span data-stu-id="8094d-624">IsString</span></span>
<span data-ttu-id="8094d-625">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-625">**Description:**</span></span>  
<span data-ttu-id="8094d-626">La fonction IsString prend la valeur True si l’expression peut être évaluée en tant que type de chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="8094d-627">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="8094d-628">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-628">**Remarks:**</span></span>  
<span data-ttu-id="8094d-629">Permet de déterminer si CStr() peut parvenir à analyser l’expression.</span><span class="sxs-lookup"><span data-stu-id="8094d-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="8094d-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="8094d-630">IsPresent</span></span>
<span data-ttu-id="8094d-631">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-631">**Description:**</span></span>  
<span data-ttu-id="8094d-632">La fonction IsPresent renvoie true si l’expression correspond à une chaîne qui n’a pas la valeur Null et n’est pas vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="8094d-633">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="8094d-634">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-634">**Remarks:**</span></span>  
<span data-ttu-id="8094d-635">L’inverse de cette fonction est appelé IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="8094d-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="8094d-636">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="8094d-637">Item</span><span class="sxs-lookup"><span data-stu-id="8094d-637">Item</span></span>
<span data-ttu-id="8094d-638">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-638">**Description:**</span></span>  
<span data-ttu-id="8094d-639">La fonction Item renvoie un élément à partir d’une chaîne/d’un attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="8094d-640">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="8094d-641">attribute : attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="8094d-642">index : index vers un élément dans la chaîne à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="8094d-643">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-643">**Remarks:**</span></span>  
<span data-ttu-id="8094d-644">la fonction Item est utile si utilisée avec la fonction Contains, car cette dernière renvoie l’index à un élément de l’attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="8094d-645">Génère une erreur si l’index est hors limites.</span><span class="sxs-lookup"><span data-stu-id="8094d-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="8094d-646">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="8094d-647">Renvoie l’adresse de messagerie principale.</span><span class="sxs-lookup"><span data-stu-id="8094d-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="8094d-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="8094d-648">ItemOrNull</span></span>
<span data-ttu-id="8094d-649">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-649">**Description:**</span></span>  
<span data-ttu-id="8094d-650">La fonction ItemOrNull renvoie un élément à partir d’une chaîne/d’un attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="8094d-651">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="8094d-652">attribute : attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="8094d-653">index : index vers un élément dans la chaîne à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="8094d-654">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-654">**Remarks:**</span></span>  
<span data-ttu-id="8094d-655">La fonction ItemOrNull est utile avec la fonction Contains, car cette dernière renvoie l’index à un élément de l’attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="8094d-656">Renvoie une valeur Null si l’index est hors limites.</span><span class="sxs-lookup"><span data-stu-id="8094d-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="8094d-657">Join</span><span class="sxs-lookup"><span data-stu-id="8094d-657">Join</span></span>
<span data-ttu-id="8094d-658">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-658">**Description:**</span></span>  
<span data-ttu-id="8094d-659">La fonction Join prend une chaîne à valeurs multiples et renvoie une chaîne à valeur unique avec le séparateur spécifié inséré entre chaque élément.</span><span class="sxs-lookup"><span data-stu-id="8094d-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="8094d-660">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="8094d-661">attribute : attribut à valeurs multiples contenant des chaînes à joindre.</span><span class="sxs-lookup"><span data-stu-id="8094d-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="8094d-662">délimiter : toute chaîne utilisée pour séparer les sous-chaînes dans la chaîne renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="8094d-663">En cas d’omission, le caractère espace (" ") est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8094d-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="8094d-664">Si le délimiteur est une chaîne de longueur nulle ("") ou Nothing, tous les éléments de la liste sont concaténés sans délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="8094d-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="8094d-665">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="8094d-665">**Remarks**</span></span>  
<span data-ttu-id="8094d-666">Il existe une parité entre les fonctions Join et Split.</span><span class="sxs-lookup"><span data-stu-id="8094d-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="8094d-667">La fonction Join prend un tableau de chaînes et les joint à l’aide d’une chaîne de délimiteur, pour renvoyer une chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="8094d-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="8094d-668">La fonction Split accepte une chaîne et la sépare au niveau du délimiteur, pour renvoyer un tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="8094d-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="8094d-669">Toutefois, la principale différence est que Join peut concaténer des chaînes avec n’importe quelle chaîne de délimiteur, Split peut uniquement séparer des chaînes à l’aide d’un délimiteur de caractère unique.</span><span class="sxs-lookup"><span data-stu-id="8094d-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="8094d-670">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="8094d-671">Peut retourner : « SMTP:john.doe@contoso.com,smtp:jd@contoso.com »</span><span class="sxs-lookup"><span data-stu-id="8094d-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="8094d-672">LCase</span><span class="sxs-lookup"><span data-stu-id="8094d-672">LCase</span></span>
<span data-ttu-id="8094d-673">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-673">**Description:**</span></span>  
<span data-ttu-id="8094d-674">La fonction LCase convertit tous les caractères d’une chaîne en minuscules.</span><span class="sxs-lookup"><span data-stu-id="8094d-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="8094d-675">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="8094d-676">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="8094d-677">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="8094d-678">Left</span><span class="sxs-lookup"><span data-stu-id="8094d-678">Left</span></span>
<span data-ttu-id="8094d-679">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-679">**Description:**</span></span>  
<span data-ttu-id="8094d-680">La fonction Left renvoie un nombre spécifié de caractères en partant de la gauche d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="8094d-681">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="8094d-682">string : chaîne à partir de laquelle les caractères sont renvoyés</span><span class="sxs-lookup"><span data-stu-id="8094d-682">string: the string to return characters from</span></span>
* <span data-ttu-id="8094d-683">NumChars : nombre identifiant le nombre de caractères à retourner du début (à gauche) de la chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="8094d-684">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-684">**Remarks:**</span></span>  
<span data-ttu-id="8094d-685">Chaîne contenant les numChars premiers caractères de la chaîne :</span><span class="sxs-lookup"><span data-stu-id="8094d-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="8094d-686">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8094d-687">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8094d-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8094d-688">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-688">If string is null, return empty string.</span></span>

<span data-ttu-id="8094d-689">Si la chaîne contient moins de caractères que le nombre spécifié dans numChars, une chaîne identique à la chaîne (c’est-à-dire, contenant tous les caractères du paramètre 1) est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="8094d-690">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="8094d-691">Renvoie « Joh ».</span><span class="sxs-lookup"><span data-stu-id="8094d-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="8094d-692">Len</span><span class="sxs-lookup"><span data-stu-id="8094d-692">Len</span></span>
<span data-ttu-id="8094d-693">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-693">**Description:**</span></span>  
<span data-ttu-id="8094d-694">La fonction Len renvoie le nombre de caractères contenus dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="8094d-695">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="8094d-696">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="8094d-697">Renvoie 8.</span><span class="sxs-lookup"><span data-stu-id="8094d-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="8094d-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="8094d-698">LTrim</span></span>
<span data-ttu-id="8094d-699">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-699">**Description:**</span></span>  
<span data-ttu-id="8094d-700">La fonction LTrim supprime les espaces blancs situés au début d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="8094d-701">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="8094d-702">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="8094d-703">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="8094d-704">Mid</span><span class="sxs-lookup"><span data-stu-id="8094d-704">Mid</span></span>
<span data-ttu-id="8094d-705">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-705">**Description:**</span></span>  
<span data-ttu-id="8094d-706">La fonction Mid renvoie un nombre donné de caractères à partir d’une position spécifiée dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="8094d-707">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="8094d-708">string : chaîne à partir de laquelle les caractères sont renvoyés</span><span class="sxs-lookup"><span data-stu-id="8094d-708">string: the string to return characters from</span></span>
* <span data-ttu-id="8094d-709">start : nombre identifiant la position de départ dans la chaîne à partir de laquelle les caractères sont renvoyés</span><span class="sxs-lookup"><span data-stu-id="8094d-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="8094d-710">NumChars : nombre identifiant le nombre de caractères à retourner à partir de la position dans la chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="8094d-711">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-711">**Remarks:**</span></span>  
<span data-ttu-id="8094d-712">Renvoie numChars caractères à partir de la position de départ dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="8094d-713">Chaîne contenant numChars caractères à partir de la position de départ dans la chaîne :</span><span class="sxs-lookup"><span data-stu-id="8094d-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="8094d-714">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8094d-715">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8094d-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8094d-716">Si start > la longueur de la chaîne, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8094d-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="8094d-717">Si start < = 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8094d-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="8094d-718">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-718">If string is null, return empty string.</span></span>

<span data-ttu-id="8094d-719">S’il ne reste pas numChars caractères dans la chaîne à partir de la position de départ, autant de caractères que possible sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="8094d-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="8094d-720">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="8094d-721">Renvoie « hn Do ».</span><span class="sxs-lookup"><span data-stu-id="8094d-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="8094d-722">Renvoie « Doe ».</span><span class="sxs-lookup"><span data-stu-id="8094d-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="8094d-723">Now</span><span class="sxs-lookup"><span data-stu-id="8094d-723">Now</span></span>
<span data-ttu-id="8094d-724">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-724">**Description:**</span></span>  
<span data-ttu-id="8094d-725">La fonction Now renvoie une valeur DateTime indiquant la date et l’heure actuelles qui correspondent à la date et à l’heure système de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8094d-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="8094d-726">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="8094d-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="8094d-727">NumFromDate</span></span>
<span data-ttu-id="8094d-728">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-728">**Description:**</span></span>  
<span data-ttu-id="8094d-729">La fonction NumFromDate renvoie une date au format de date AD.</span><span class="sxs-lookup"><span data-stu-id="8094d-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="8094d-730">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="8094d-731">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="8094d-732">Renvoie 129699324000000000.</span><span class="sxs-lookup"><span data-stu-id="8094d-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="8094d-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="8094d-733">PadLeft</span></span>
<span data-ttu-id="8094d-734">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-734">**Description:**</span></span>  
<span data-ttu-id="8094d-735">La fonction PadLeft remplit par la gauche une chaîne sur une longueur spécifiée à l’aide d’un caractère de remplissage fourni.</span><span class="sxs-lookup"><span data-stu-id="8094d-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="8094d-736">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="8094d-737">string : chaîne à remplir.</span><span class="sxs-lookup"><span data-stu-id="8094d-737">string: the string to pad.</span></span>
* <span data-ttu-id="8094d-738">length : entier représentant la longueur de chaîne souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8094d-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="8094d-739">padCharacter : chaîne constituée d’un seul caractère à utiliser comme caractère de remplissage</span><span class="sxs-lookup"><span data-stu-id="8094d-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="8094d-740">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-740">**Remarks:**</span></span>

* <span data-ttu-id="8094d-741">Si la longueur de chaîne est inférieure à la longueur length, padCharacter est ajouté à plusieurs reprises au début (à gauche) de la chaîne jusqu’à ce qu’à atteindre la longueur length.</span><span class="sxs-lookup"><span data-stu-id="8094d-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="8094d-742">PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.</span><span class="sxs-lookup"><span data-stu-id="8094d-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="8094d-743">Si la longueur de chaîne est égale ou supérieure à la longueur length, la chaîne est renvoyée inchangée.</span><span class="sxs-lookup"><span data-stu-id="8094d-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="8094d-744">Si la longueur de la chaîne est supérieure ou égale à la longueur length, une chaîne identique est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="8094d-745">Si la longueur de chaîne est inférieure à la longueur length, une nouvelle chaîne de longueur souhaitée est retournée, et contient une chaîne remplie avec un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="8094d-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="8094d-746">Si la chaîne est null, la fonction retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="8094d-747">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="8094d-748">Renvoie « 000000User ».</span><span class="sxs-lookup"><span data-stu-id="8094d-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="8094d-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="8094d-749">PadRight</span></span>
<span data-ttu-id="8094d-750">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-750">**Description:**</span></span>  
<span data-ttu-id="8094d-751">La fonction PadRight remplit par la droite une chaîne sur une longueur spécifiée à l’aide d’un caractère de remplissage fourni.</span><span class="sxs-lookup"><span data-stu-id="8094d-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="8094d-752">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="8094d-753">string : chaîne à remplir.</span><span class="sxs-lookup"><span data-stu-id="8094d-753">string: the string to pad.</span></span>
* <span data-ttu-id="8094d-754">length : entier représentant la longueur de chaîne souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8094d-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="8094d-755">padCharacter : chaîne constituée d’un seul caractère à utiliser comme caractère de remplissage</span><span class="sxs-lookup"><span data-stu-id="8094d-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="8094d-756">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-756">**Remarks:**</span></span>

* <span data-ttu-id="8094d-757">Si la longueur de chaîne est inférieure à la longueur length, padCharacter est ajouté à plusieurs reprises à la fin (à droite) de la chaîne jusqu’à ce qu’à atteindre la longueur length.</span><span class="sxs-lookup"><span data-stu-id="8094d-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="8094d-758">PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.</span><span class="sxs-lookup"><span data-stu-id="8094d-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="8094d-759">Si la longueur de chaîne est égale ou supérieure à la longueur length, la chaîne est renvoyée inchangée.</span><span class="sxs-lookup"><span data-stu-id="8094d-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="8094d-760">Si la longueur de la chaîne est supérieure ou égale à la longueur length, une chaîne identique est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="8094d-761">Si la longueur de chaîne est inférieure à la longueur length, une nouvelle chaîne de longueur souhaitée est retournée, et contient une chaîne remplie avec un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="8094d-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="8094d-762">Si la chaîne est null, la fonction retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="8094d-763">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="8094d-764">Renvoie « User000000 ».</span><span class="sxs-lookup"><span data-stu-id="8094d-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="8094d-765">PCase</span><span class="sxs-lookup"><span data-stu-id="8094d-765">PCase</span></span>
<span data-ttu-id="8094d-766">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-766">**Description:**</span></span>  
<span data-ttu-id="8094d-767">La fonction PCase met en majuscule le premier caractère de chaque mot délimité par un espace dans une chaîne, et tous les autres caractères sont convertis en minuscules.</span><span class="sxs-lookup"><span data-stu-id="8094d-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="8094d-768">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="8094d-769">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-769">**Remarks:**</span></span>

* <span data-ttu-id="8094d-770">Cette fonction ne fournit pas pour le moment de casse appropriée pour convertir un mot qui est entièrement en majuscules, par exemple un sigle.</span><span class="sxs-lookup"><span data-stu-id="8094d-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="8094d-771">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="8094d-772">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="8094d-773">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="8094d-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="8094d-774">RandomNum</span></span>
<span data-ttu-id="8094d-775">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-775">**Description:**</span></span>  
<span data-ttu-id="8094d-776">La fonction RandomNum renvoie un nombre aléatoire dans un intervalle spécifié.</span><span class="sxs-lookup"><span data-stu-id="8094d-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="8094d-777">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="8094d-778">start : nombre identifiant la limite inférieure de la valeur aléatoire à générer</span><span class="sxs-lookup"><span data-stu-id="8094d-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="8094d-779">end : nombre identifiant la limite supérieure de la valeur aléatoire à générer</span><span class="sxs-lookup"><span data-stu-id="8094d-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="8094d-780">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="8094d-781">Peut renvoyer 734.</span><span class="sxs-lookup"><span data-stu-id="8094d-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="8094d-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="8094d-782">RemoveDuplicates</span></span>
<span data-ttu-id="8094d-783">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-783">**Description:**</span></span>  
<span data-ttu-id="8094d-784">La fonction RemoveDuplicates prend une chaîne à valeurs multiples et vérifie que chaque valeur est unique.</span><span class="sxs-lookup"><span data-stu-id="8094d-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="8094d-785">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="8094d-786">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="8094d-787">Renvoie un attribut proxyAddress expurgé duquel toutes les valeurs en double ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="8094d-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="8094d-788">Replace</span><span class="sxs-lookup"><span data-stu-id="8094d-788">Replace</span></span>
<span data-ttu-id="8094d-789">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-789">**Description:**</span></span>  
<span data-ttu-id="8094d-790">La fonction Replace remplace toutes les occurrences d’une chaîne par une autre chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="8094d-791">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="8094d-792">string : chaîne dans laquelle les caractères sont remplacés.</span><span class="sxs-lookup"><span data-stu-id="8094d-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="8094d-793">OldValue : chaîne à rechercher et remplacer.</span><span class="sxs-lookup"><span data-stu-id="8094d-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="8094d-794">NewValue : chaîne de remplacement.</span><span class="sxs-lookup"><span data-stu-id="8094d-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="8094d-795">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-795">**Remarks:**</span></span>  
<span data-ttu-id="8094d-796">La fonction reconnaît les monikers spéciaux suivants :</span><span class="sxs-lookup"><span data-stu-id="8094d-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="8094d-797">\n – Nouvelle ligne</span><span class="sxs-lookup"><span data-stu-id="8094d-797">\n – New Line</span></span>
* <span data-ttu-id="8094d-798">\r – Retour chariot</span><span class="sxs-lookup"><span data-stu-id="8094d-798">\r – Carriage Return</span></span>
* <span data-ttu-id="8094d-799">\t – Tabulation</span><span class="sxs-lookup"><span data-stu-id="8094d-799">\t – Tab</span></span>

<span data-ttu-id="8094d-800">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="8094d-801">Remplace CRLF par une virgule et un espace, et peut générer « One Microsoft Way, Redmond, WA, USA ».</span><span class="sxs-lookup"><span data-stu-id="8094d-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="8094d-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="8094d-802">ReplaceChars</span></span>
<span data-ttu-id="8094d-803">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-803">**Description:**</span></span>  
<span data-ttu-id="8094d-804">La fonction ReplaceChars remplace toutes les occurrences des caractères trouvés dans la chaîne ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="8094d-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="8094d-805">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="8094d-806">string : chaîne dans laquelle les caractères sont remplacés.</span><span class="sxs-lookup"><span data-stu-id="8094d-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="8094d-807">ReplacePattern : chaîne contenant un dictionnaire avec des caractères à remplacer.</span><span class="sxs-lookup"><span data-stu-id="8094d-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="8094d-808">Le format est {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN}, source étant le caractère à rechercher et la cible, la chaîne à remplacer.</span><span class="sxs-lookup"><span data-stu-id="8094d-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="8094d-809">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-809">**Remarks:**</span></span>

* <span data-ttu-id="8094d-810">La fonction prend chaque occurrence de sources définies et la remplace par les cibles.</span><span class="sxs-lookup"><span data-stu-id="8094d-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="8094d-811">La source doit être exactement un caractère (unicode).</span><span class="sxs-lookup"><span data-stu-id="8094d-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="8094d-812">La source ne peut pas être vide ou dépasser un caractère (erreur d’analyse).</span><span class="sxs-lookup"><span data-stu-id="8094d-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="8094d-813">La cible peut comporter plusieurs caractères, par exemple ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="8094d-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="8094d-814">La cible peut être vide, indiquant que le caractère doit être supprimé.</span><span class="sxs-lookup"><span data-stu-id="8094d-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="8094d-815">La source respecte la casse et il doit s’agir d’une correspondance exacte.</span><span class="sxs-lookup"><span data-stu-id="8094d-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="8094d-816">La , (Virgule) et : (deux-points) sont des caractères réservés et ne peuvent pas être remplacés avec cette fonction.</span><span class="sxs-lookup"><span data-stu-id="8094d-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="8094d-817">Les espaces et autres caractères blancs dans la chaîne ReplacePattern sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="8094d-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="8094d-818">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="8094d-819">Renvoie Raksmorgas.</span><span class="sxs-lookup"><span data-stu-id="8094d-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="8094d-820">Renvoie « ONeil », l’apostrophe est définie comme étant à supprimer.</span><span class="sxs-lookup"><span data-stu-id="8094d-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="8094d-821">Right</span><span class="sxs-lookup"><span data-stu-id="8094d-821">Right</span></span>
<span data-ttu-id="8094d-822">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-822">**Description:**</span></span>  
<span data-ttu-id="8094d-823">La fonction Right renvoie un nombre spécifié de caractères en partant de la droite (fin) d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="8094d-824">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="8094d-825">string : chaîne à partir de laquelle les caractères sont renvoyés</span><span class="sxs-lookup"><span data-stu-id="8094d-825">string: the string to return characters from</span></span>
* <span data-ttu-id="8094d-826">numChars : nombre identifiant le nombre de caractères à retourner à partir de la fin (à droite) de la chaîne</span><span class="sxs-lookup"><span data-stu-id="8094d-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="8094d-827">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-827">**Remarks:**</span></span>  
<span data-ttu-id="8094d-828">Les numChars caractères sont renvoyés à partir de la dernière position de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="8094d-829">Chaîne contenant les numChars derniers caractères de la chaîne :</span><span class="sxs-lookup"><span data-stu-id="8094d-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="8094d-830">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="8094d-831">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8094d-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="8094d-832">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-832">If string is null, return empty string.</span></span>

<span data-ttu-id="8094d-833">Si la chaîne contient un nombre de caractères inférieur au nombre spécifié dans numChars, une chaîne identique est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="8094d-834">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="8094d-835">Renvoie « Doe ».</span><span class="sxs-lookup"><span data-stu-id="8094d-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="8094d-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="8094d-836">RTrim</span></span>
<span data-ttu-id="8094d-837">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-837">**Description:**</span></span>  
<span data-ttu-id="8094d-838">La fonction RTrim supprime les espaces blancs situés à la fin d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="8094d-839">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="8094d-840">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="8094d-841">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="8094d-842">Sélectionnez</span><span class="sxs-lookup"><span data-stu-id="8094d-842">Select</span></span>
<span data-ttu-id="8094d-843">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-843">**Description:**</span></span>  
<span data-ttu-id="8094d-844">Traite toutes les valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) selon la fonction spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8094d-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="8094d-845">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="8094d-846">item : représente un élément de l’attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="8094d-847">attribute : l’attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="8094d-848">expression : expression qui retourne une collection de valeurs</span><span class="sxs-lookup"><span data-stu-id="8094d-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="8094d-849">condition : toute fonction pouvant traiter un élément de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8094d-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="8094d-850">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="8094d-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="8094d-851">Retourne toutes les valeurs de l’attribut à valeurs multiples otherPhone après suppression des traits d’union (-).</span><span class="sxs-lookup"><span data-stu-id="8094d-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="8094d-852">Split</span><span class="sxs-lookup"><span data-stu-id="8094d-852">Split</span></span>
<span data-ttu-id="8094d-853">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-853">**Description:**</span></span>  
<span data-ttu-id="8094d-854">La fonction Split prend une chaîne séparée par un délimiteur et en fait une chaîne à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="8094d-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="8094d-855">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="8094d-856">value : chaîne contenant un caractère délimiteur pour assurer la séparation.</span><span class="sxs-lookup"><span data-stu-id="8094d-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="8094d-857">delimiter : caractère unique à utiliser comme délimiteur.</span><span class="sxs-lookup"><span data-stu-id="8094d-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="8094d-858">limit : nombre maximal de valeurs qu’il est possible de renvoyer.</span><span class="sxs-lookup"><span data-stu-id="8094d-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="8094d-859">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="8094d-860">Renvoie une chaîne à valeurs multiples avec 2 éléments utiles pour l’attribut proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="8094d-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="8094d-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="8094d-861">StringFromGuid</span></span>
<span data-ttu-id="8094d-862">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-862">**Description:**</span></span>  
<span data-ttu-id="8094d-863">La fonction StringFromGuid prend un GUID binaire et le convertit en chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="8094d-864">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="8094d-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="8094d-865">StringFromSid</span></span>
<span data-ttu-id="8094d-866">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-866">**Description:**</span></span>  
<span data-ttu-id="8094d-867">La fonction StringFromSid convertit en chaîne un tableau d’octets contenant un identificateur de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8094d-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="8094d-868">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="8094d-869">Switch</span><span class="sxs-lookup"><span data-stu-id="8094d-869">Switch</span></span>
<span data-ttu-id="8094d-870">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-870">**Description:**</span></span>  
<span data-ttu-id="8094d-871">La fonction Switch est utilisée pour renvoyer une valeur unique en fonction des conditions évaluées.</span><span class="sxs-lookup"><span data-stu-id="8094d-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="8094d-872">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="8094d-873">expr : expression de variante à évaluer.</span><span class="sxs-lookup"><span data-stu-id="8094d-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="8094d-874">value : valeur à retourner si l’expression correspondante a la valeur True.</span><span class="sxs-lookup"><span data-stu-id="8094d-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="8094d-875">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-875">**Remarks:**</span></span>  
<span data-ttu-id="8094d-876">La liste d’arguments de la fonction Switch se compose de paires d’expressions et de valeurs.</span><span class="sxs-lookup"><span data-stu-id="8094d-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="8094d-877">Les expressions sont évaluées de gauche à droite et la valeur associée à la première expression à évoluer à True est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="8094d-878">Si les parties ne sont pas correctement couplées, une erreur d’exécution se produit.</span><span class="sxs-lookup"><span data-stu-id="8094d-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="8094d-879">Par exemple, si expr1 est True, Switch renvoie la valeur1.</span><span class="sxs-lookup"><span data-stu-id="8094d-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="8094d-880">Si expr-1 est False, mais expr-2 est True, Switch renvoie la valeur 2, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="8094d-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="8094d-881">Switch ne renvoie rien si :</span><span class="sxs-lookup"><span data-stu-id="8094d-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="8094d-882">Aucune des expressions n’est vraie.</span><span class="sxs-lookup"><span data-stu-id="8094d-882">None of the expressions are True.</span></span>
* <span data-ttu-id="8094d-883">La première expression True possède une valeur correspondante Null.</span><span class="sxs-lookup"><span data-stu-id="8094d-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="8094d-884">Switch évalue toutes les expressions, même si elle n’en renvoie qu’une.</span><span class="sxs-lookup"><span data-stu-id="8094d-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="8094d-885">Pour cette raison, il est conseillé de surveiller les éventuels effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="8094d-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="8094d-886">Par exemple, si l’évaluation d’une expression entraîne une division par zéro, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="8094d-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="8094d-887">La valeur peut être également la fonction Error qui renvoie une chaîne personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8094d-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="8094d-888">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="8094d-889">Renvoie la langue parlée dans certaines grandes villes ; sinon, renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="8094d-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="8094d-890">Trim</span><span class="sxs-lookup"><span data-stu-id="8094d-890">Trim</span></span>
<span data-ttu-id="8094d-891">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-891">**Description:**</span></span>  
<span data-ttu-id="8094d-892">La fonction Trim supprime les espaces blancs situés au début et à la fin d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="8094d-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="8094d-893">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="8094d-894">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="8094d-895">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="8094d-896">Supprime les espaces blancs de début et de fin pour chaque valeur contenue dans l’attribut proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="8094d-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="8094d-897">UCase</span><span class="sxs-lookup"><span data-stu-id="8094d-897">UCase</span></span>
<span data-ttu-id="8094d-898">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-898">**Description:**</span></span>  
<span data-ttu-id="8094d-899">La fonction UCase convertit tous les caractères d’une chaîne en majuscules.</span><span class="sxs-lookup"><span data-stu-id="8094d-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="8094d-900">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="8094d-901">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="8094d-902">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="8094d-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="8094d-903">Where</span><span class="sxs-lookup"><span data-stu-id="8094d-903">Where</span></span>

<span data-ttu-id="8094d-904">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-904">**Description:**</span></span>  
<span data-ttu-id="8094d-905">Retourne un sous-ensemble de valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) en fonction de la condition.</span><span class="sxs-lookup"><span data-stu-id="8094d-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="8094d-906">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="8094d-907">item : représente un élément de l’attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="8094d-908">attribute : l’attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="8094d-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="8094d-909">condition : toute expression pouvant avoir la valeur true ou false</span><span class="sxs-lookup"><span data-stu-id="8094d-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="8094d-910">expression : expression qui retourne une collection de valeurs</span><span class="sxs-lookup"><span data-stu-id="8094d-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="8094d-911">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="8094d-912">Retourne les valeurs de certificat de l’attribut à valeurs multiples userCertificate qui n’ont pas expiré.</span><span class="sxs-lookup"><span data-stu-id="8094d-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="8094d-913">With</span><span class="sxs-lookup"><span data-stu-id="8094d-913">With</span></span>
<span data-ttu-id="8094d-914">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-914">**Description:**</span></span>  
<span data-ttu-id="8094d-915">La fonction With permet de simplifier une expression complexe en utilisant une variable pour représenter une sous-expression qui apparaît une ou plusieurs fois dans l’expression complexe.</span><span class="sxs-lookup"><span data-stu-id="8094d-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="8094d-916">**Syntaxe**
`With(var variable, exp subExpression, exp complexExpression)` :</span><span class="sxs-lookup"><span data-stu-id="8094d-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="8094d-917">variable : représente la sous-expression.</span><span class="sxs-lookup"><span data-stu-id="8094d-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="8094d-918">subExpression : sous-expression représentée par une variable.</span><span class="sxs-lookup"><span data-stu-id="8094d-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="8094d-919">complexExpression : expression complexe.</span><span class="sxs-lookup"><span data-stu-id="8094d-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="8094d-920">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="8094d-921">Fonctionnellement équivalent à :</span><span class="sxs-lookup"><span data-stu-id="8094d-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="8094d-922">Qui retourne uniquement les valeurs de certificat non expirées de l’attribut userCertificate.</span><span class="sxs-lookup"><span data-stu-id="8094d-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="8094d-923">Word</span><span class="sxs-lookup"><span data-stu-id="8094d-923">Word</span></span>
<span data-ttu-id="8094d-924">**Description :**</span><span class="sxs-lookup"><span data-stu-id="8094d-924">**Description:**</span></span>  
<span data-ttu-id="8094d-925">La fonction Word retourne un mot contenu dans une chaîne, en fonction des paramètres qui décrivent les délimiteurs à utiliser et le nombre de mots à retourner.</span><span class="sxs-lookup"><span data-stu-id="8094d-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="8094d-926">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="8094d-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="8094d-927">string : chaîne à partir de laquelle le mot est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="8094d-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="8094d-928">WordNumber : nombre identifiant le nombre de mots à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="8094d-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="8094d-929">delimiters : chaîne représentant le ou les délimiteur(s) à utiliser pour identifier les mots</span><span class="sxs-lookup"><span data-stu-id="8094d-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="8094d-930">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="8094d-930">**Remarks:**</span></span>  
<span data-ttu-id="8094d-931">Chaque chaîne de caractères contenue dans la chaîne séparée par l’un des caractères figurant dans delimiters est identifiée en tant que mot :</span><span class="sxs-lookup"><span data-stu-id="8094d-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="8094d-932">Si number < 1, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="8094d-933">Si string a la valeur null, renvoie une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="8094d-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="8094d-934">Si la chaîne contient moins de mots ou ne contient pas les mots identifiés par les séparateurs, une chaîne vide est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8094d-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="8094d-935">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="8094d-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="8094d-936">Retourne « brown ».</span><span class="sxs-lookup"><span data-stu-id="8094d-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="8094d-937">Retourne « has ».</span><span class="sxs-lookup"><span data-stu-id="8094d-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8094d-938">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8094d-938">Additional Resources</span></span>
* [<span data-ttu-id="8094d-939">Comprendre les expressions d’approvisionnement déclaratif</span><span class="sxs-lookup"><span data-stu-id="8094d-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="8094d-940">Azure AD Connect Sync : personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="8094d-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="8094d-941">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8094d-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
