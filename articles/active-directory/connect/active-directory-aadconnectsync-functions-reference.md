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
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="78bef-103">Azure AD Connect Sync : Référence aux fonctions</span><span class="sxs-lookup"><span data-stu-id="78bef-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="78bef-104">Dans Azure AD Connect, les fonctions sont utilisée toomanipulate une valeur d’attribut lors de la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="78bef-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="78bef-105">Hello syntaxe des fonctions de hello est exprimée à l’aide de hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="78bef-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="78bef-106">Si une fonction est surchargée et accepte plusieurs syntaxes, toutes les syntaxes valides sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="78bef-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="78bef-107">les fonctions Hello sont fortement typées et elles vérifient que le type de hello passé dans le type de hello documentée de correspondances.</span><span class="sxs-lookup"><span data-stu-id="78bef-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="78bef-108">Si le type de hello ne correspond pas, une erreur est générée.</span><span class="sxs-lookup"><span data-stu-id="78bef-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="78bef-109">types de Hello sont exprimées par hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="78bef-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="78bef-110">**bin** : binaire</span><span class="sxs-lookup"><span data-stu-id="78bef-110">**bin** – Binary</span></span>
* <span data-ttu-id="78bef-111">**bool** : booléen</span><span class="sxs-lookup"><span data-stu-id="78bef-111">**bool** – Boolean</span></span>
* <span data-ttu-id="78bef-112">**dt** : date/heure UTC</span><span class="sxs-lookup"><span data-stu-id="78bef-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="78bef-113">**enum** : énumération des constantes connues</span><span class="sxs-lookup"><span data-stu-id="78bef-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="78bef-114">**EXP** – Expression, qui est attendu tooevaluate tooa booléen</span><span class="sxs-lookup"><span data-stu-id="78bef-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="78bef-115">**mvbin** : binaire à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="78bef-116">**mvstr** : chaîne à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="78bef-117">**mvref** : référence à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="78bef-118">**num** : numérique</span><span class="sxs-lookup"><span data-stu-id="78bef-118">**num** – Numeric</span></span>
* <span data-ttu-id="78bef-119">**ref** : référence</span><span class="sxs-lookup"><span data-stu-id="78bef-119">**ref** – Reference</span></span>
* <span data-ttu-id="78bef-120">**str** : chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-120">**str** – String</span></span>
* <span data-ttu-id="78bef-121">**var** : variante de (quasiment) tout autre type</span><span class="sxs-lookup"><span data-stu-id="78bef-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="78bef-122">**void** : ne retourne aucune valeur</span><span class="sxs-lookup"><span data-stu-id="78bef-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="78bef-123">Hello fonctions avec les types hello **mvbin**, **mvstr**, et **mvref** ne fonctionnent sur des attributs à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="78bef-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="78bef-124">Les fonctions avec **bin**, **str** et **ref** fonctionnent sur des attributs à valeur unique et à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="78bef-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="78bef-125">Référence des fonctions</span><span class="sxs-lookup"><span data-stu-id="78bef-125">Functions Reference</span></span>
| <span data-ttu-id="78bef-126">Liste des fonctions</span><span class="sxs-lookup"><span data-stu-id="78bef-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="78bef-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="78bef-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="78bef-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="78bef-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="78bef-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="78bef-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="78bef-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="78bef-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="78bef-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="78bef-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="78bef-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="78bef-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="78bef-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="78bef-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="78bef-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="78bef-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="78bef-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="78bef-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="78bef-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="78bef-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="78bef-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="78bef-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="78bef-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="78bef-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="78bef-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="78bef-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="78bef-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="78bef-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="78bef-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="78bef-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="78bef-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="78bef-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="78bef-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="78bef-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="78bef-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="78bef-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="78bef-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="78bef-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="78bef-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="78bef-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="78bef-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="78bef-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="78bef-148">CertVersion</span><span class="sxs-lookup"><span data-stu-id="78bef-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="78bef-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="78bef-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="78bef-150">**Conversion**</span><span class="sxs-lookup"><span data-stu-id="78bef-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="78bef-151">CBool</span><span class="sxs-lookup"><span data-stu-id="78bef-151">CBool</span></span>](#cbool) |[<span data-ttu-id="78bef-152">CDate</span><span class="sxs-lookup"><span data-stu-id="78bef-152">CDate</span></span>](#cdate) |[<span data-ttu-id="78bef-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="78bef-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="78bef-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="78bef-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="78bef-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="78bef-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="78bef-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="78bef-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="78bef-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="78bef-158">CNum</span><span class="sxs-lookup"><span data-stu-id="78bef-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="78bef-159">CRef</span><span class="sxs-lookup"><span data-stu-id="78bef-159">CRef</span></span>](#cref) |[<span data-ttu-id="78bef-160">CStr</span><span class="sxs-lookup"><span data-stu-id="78bef-160">CStr</span></span>](#cstr) |[<span data-ttu-id="78bef-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="78bef-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="78bef-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="78bef-163">**Date / Heure**</span><span class="sxs-lookup"><span data-stu-id="78bef-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="78bef-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="78bef-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="78bef-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="78bef-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="78bef-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="78bef-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="78bef-167">Now</span><span class="sxs-lookup"><span data-stu-id="78bef-167">Now</span></span>](#now) | |
| [<span data-ttu-id="78bef-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="78bef-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="78bef-169">**Directory**</span><span class="sxs-lookup"><span data-stu-id="78bef-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="78bef-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="78bef-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="78bef-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="78bef-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="78bef-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="78bef-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="78bef-173">**Evaluation**</span><span class="sxs-lookup"><span data-stu-id="78bef-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="78bef-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="78bef-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="78bef-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="78bef-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="78bef-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="78bef-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="78bef-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="78bef-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="78bef-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="78bef-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="78bef-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="78bef-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="78bef-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="78bef-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="78bef-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="78bef-182">IsString</span><span class="sxs-lookup"><span data-stu-id="78bef-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="78bef-183">**Mathématique**</span><span class="sxs-lookup"><span data-stu-id="78bef-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="78bef-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="78bef-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="78bef-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="78bef-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="78bef-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="78bef-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="78bef-187">**Multi-valued**</span><span class="sxs-lookup"><span data-stu-id="78bef-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="78bef-188">Contains</span><span class="sxs-lookup"><span data-stu-id="78bef-188">Contains</span></span>](#contains) |[<span data-ttu-id="78bef-189">Count</span><span class="sxs-lookup"><span data-stu-id="78bef-189">Count</span></span>](#count) |[<span data-ttu-id="78bef-190">Item</span><span class="sxs-lookup"><span data-stu-id="78bef-190">Item</span></span>](#item) |[<span data-ttu-id="78bef-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="78bef-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="78bef-192">Join</span><span class="sxs-lookup"><span data-stu-id="78bef-192">Join</span></span>](#join) |[<span data-ttu-id="78bef-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="78bef-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="78bef-194">Split</span><span class="sxs-lookup"><span data-stu-id="78bef-194">Split</span></span>](#split) | | |
| <span data-ttu-id="78bef-195">**Flux de programme**</span><span class="sxs-lookup"><span data-stu-id="78bef-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="78bef-196">Error</span><span class="sxs-lookup"><span data-stu-id="78bef-196">Error</span></span>](#error) |[<span data-ttu-id="78bef-197">IIF</span><span class="sxs-lookup"><span data-stu-id="78bef-197">IIF</span></span>](#iif) |[<span data-ttu-id="78bef-198">Sélection</span><span class="sxs-lookup"><span data-stu-id="78bef-198">Select</span></span>](#select) |[<span data-ttu-id="78bef-199">Switch</span><span class="sxs-lookup"><span data-stu-id="78bef-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="78bef-200">Where</span><span class="sxs-lookup"><span data-stu-id="78bef-200">Where</span></span>](#where) |[<span data-ttu-id="78bef-201">With</span><span class="sxs-lookup"><span data-stu-id="78bef-201">With</span></span>](#with) | | | |
| <span data-ttu-id="78bef-202">**Text**</span><span class="sxs-lookup"><span data-stu-id="78bef-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="78bef-203">GUID</span><span class="sxs-lookup"><span data-stu-id="78bef-203">GUID</span></span>](#guid) |[<span data-ttu-id="78bef-204">InStr</span><span class="sxs-lookup"><span data-stu-id="78bef-204">InStr</span></span>](#instr) |[<span data-ttu-id="78bef-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="78bef-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="78bef-206">LCase</span><span class="sxs-lookup"><span data-stu-id="78bef-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="78bef-207">Left</span><span class="sxs-lookup"><span data-stu-id="78bef-207">Left</span></span>](#left) |[<span data-ttu-id="78bef-208">Len</span><span class="sxs-lookup"><span data-stu-id="78bef-208">Len</span></span>](#len) |[<span data-ttu-id="78bef-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="78bef-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="78bef-210">Mid</span><span class="sxs-lookup"><span data-stu-id="78bef-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="78bef-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="78bef-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="78bef-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="78bef-212">PadRight</span></span>](#padright) |[<span data-ttu-id="78bef-213">PCase</span><span class="sxs-lookup"><span data-stu-id="78bef-213">PCase</span></span>](#pcase) |[<span data-ttu-id="78bef-214">Replace</span><span class="sxs-lookup"><span data-stu-id="78bef-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="78bef-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="78bef-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="78bef-216">Right</span><span class="sxs-lookup"><span data-stu-id="78bef-216">Right</span></span>](#right) |[<span data-ttu-id="78bef-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="78bef-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="78bef-218">Trim</span><span class="sxs-lookup"><span data-stu-id="78bef-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="78bef-219">UCase</span><span class="sxs-lookup"><span data-stu-id="78bef-219">UCase</span></span>](#ucase) |[<span data-ttu-id="78bef-220">Word</span><span class="sxs-lookup"><span data-stu-id="78bef-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="78bef-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="78bef-221">BitAnd</span></span>
<span data-ttu-id="78bef-222">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-222">**Description:**</span></span>  
<span data-ttu-id="78bef-223">Hello fonction BitAnd définit des bits spécifiés sur une valeur.</span><span class="sxs-lookup"><span data-stu-id="78bef-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="78bef-224">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="78bef-225">value1, value2 : valeurs numériques qui doivent être liées par AND.</span><span class="sxs-lookup"><span data-stu-id="78bef-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="78bef-226">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-226">**Remarks:**</span></span>  
<span data-ttu-id="78bef-227">Cette fonction convertit les deux paramètres toohello binaire et définit un bit :</span><span class="sxs-lookup"><span data-stu-id="78bef-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="78bef-228">0 - si une ou les deux bits correspondants dans hello *masque* et *indicateur* sont 0</span><span class="sxs-lookup"><span data-stu-id="78bef-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="78bef-229">1 - si les deux bits correspondants de hello sont 1.</span><span class="sxs-lookup"><span data-stu-id="78bef-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="78bef-230">En d’autres termes, elle retourne 0 dans tous les cas sauf si les bits correspondants de hello des deux paramètres sont 1.</span><span class="sxs-lookup"><span data-stu-id="78bef-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="78bef-231">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="78bef-232">Retourne 7, car hexadécimale « F » et « F7 » prendre la valeur de toothis.</span><span class="sxs-lookup"><span data-stu-id="78bef-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="78bef-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="78bef-233">BitOr</span></span>
<span data-ttu-id="78bef-234">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-234">**Description:**</span></span>  
<span data-ttu-id="78bef-235">Hello fonction BitOr définit des bits spécifiés sur une valeur.</span><span class="sxs-lookup"><span data-stu-id="78bef-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="78bef-236">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="78bef-237">value1, value2 : valeurs numériques qui doivent être liées par OR</span><span class="sxs-lookup"><span data-stu-id="78bef-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="78bef-238">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-238">**Remarks:**</span></span>  
<span data-ttu-id="78bef-239">Cette fonction convertit les deux paramètres toohello binaire et définit un bit de too1 si une ou les deux bits correspondants hello masque et l’indicateur sont 1 et too0 si les deux bits correspondants de hello sont 0.</span><span class="sxs-lookup"><span data-stu-id="78bef-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="78bef-240">En d’autres termes, elle retourne 1 dans tous les cas sauf si les bits correspondants de hello des deux paramètres égalent 0.</span><span class="sxs-lookup"><span data-stu-id="78bef-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="78bef-241">CBool</span><span class="sxs-lookup"><span data-stu-id="78bef-241">CBool</span></span>
<span data-ttu-id="78bef-242">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-242">**Description:**</span></span>  
<span data-ttu-id="78bef-243">Hello fonction CBool retourne qu'une valeur booléenne en fonction de l’expression de hello évaluée</span><span class="sxs-lookup"><span data-stu-id="78bef-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="78bef-244">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="78bef-245">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-245">**Remarks:**</span></span>  
<span data-ttu-id="78bef-246">Si l’expression de hello évalue tooa différent de zéro, CBool retourne True, sinon elle retourne False.</span><span class="sxs-lookup"><span data-stu-id="78bef-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="78bef-247">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="78bef-248">Retourne True si les deux attributs ont hello la même valeur.</span><span class="sxs-lookup"><span data-stu-id="78bef-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="78bef-249">CDate</span><span class="sxs-lookup"><span data-stu-id="78bef-249">CDate</span></span>
<span data-ttu-id="78bef-250">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-250">**Description:**</span></span>  
<span data-ttu-id="78bef-251">Hello fonction CDate retourne une valeur DateTime UTC à partir d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="78bef-252">DateTime n’est pas un type d’attribut natif dans Sync, mais il est utilisé par certaines fonctions.</span><span class="sxs-lookup"><span data-stu-id="78bef-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="78bef-253">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="78bef-254">Valeur : chaîne comportant une date, une heure, et éventuellement, un fuseau horaire</span><span class="sxs-lookup"><span data-stu-id="78bef-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="78bef-255">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-255">**Remarks:**</span></span>  
<span data-ttu-id="78bef-256">Hello retourné de chaîne est toujours en UTC.</span><span class="sxs-lookup"><span data-stu-id="78bef-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="78bef-257">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="78bef-258">Retourne une valeur DateTime basée sur l’heure de début de l’employé hello</span><span class="sxs-lookup"><span data-stu-id="78bef-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="78bef-259">Renvoie une valeur DateTime représentant « 2013-01-11 12:00 AM ».</span><span class="sxs-lookup"><span data-stu-id="78bef-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="78bef-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="78bef-260">CertExtensionOids</span></span>
<span data-ttu-id="78bef-261">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-261">**Description:**</span></span>  
<span data-ttu-id="78bef-262">Retourne hello Oid des valeurs de toutes les extensions critiques hello d’un objet de certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="78bef-263">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="78bef-264">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-265">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="78bef-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="78bef-266">CertFormat</span></span>
<span data-ttu-id="78bef-267">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-267">**Description:**</span></span>  
<span data-ttu-id="78bef-268">Retourne hello nom du format de hello de ce certificat X.509v3.</span><span class="sxs-lookup"><span data-stu-id="78bef-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="78bef-269">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="78bef-270">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-271">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="78bef-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="78bef-272">CertFriendlyName</span></span>
<span data-ttu-id="78bef-273">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-273">**Description:**</span></span>  
<span data-ttu-id="78bef-274">Retourne hello associé alias pour un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="78bef-275">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="78bef-276">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-277">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="78bef-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="78bef-278">CertHashString</span></span>
<span data-ttu-id="78bef-279">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-279">**Description:**</span></span>  
<span data-ttu-id="78bef-280">Retourne hello la valeur de hachage SHA1 pour le certificat X.509v3 de hello sous forme de chaîne hexadécimale.</span><span class="sxs-lookup"><span data-stu-id="78bef-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="78bef-281">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="78bef-282">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-283">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="78bef-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="78bef-284">CertIssuer</span></span>
<span data-ttu-id="78bef-285">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-285">**Description:**</span></span>  
<span data-ttu-id="78bef-286">Retourne hello nom de l’autorité de certification hello qui a émis le certificat x.509v.3 de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="78bef-287">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="78bef-288">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-289">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="78bef-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="78bef-290">CertIssuerDN</span></span>
<span data-ttu-id="78bef-291">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-291">**Description:**</span></span>  
<span data-ttu-id="78bef-292">Retourne hello nom unique de l’émetteur du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="78bef-293">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="78bef-294">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-295">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="78bef-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="78bef-296">CertIssuerOid</span></span>
<span data-ttu-id="78bef-297">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-297">**Description:**</span></span>  
<span data-ttu-id="78bef-298">Retourne hello Oid de l’émetteur du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="78bef-299">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="78bef-300">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-301">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="78bef-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="78bef-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="78bef-303">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-303">**Description:**</span></span>  
<span data-ttu-id="78bef-304">Retourne des informations d’algorithme de clé hello pour ce certificat x.509v.3 sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="78bef-305">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="78bef-306">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-307">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="78bef-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="78bef-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="78bef-309">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-309">**Description:**</span></span>  
<span data-ttu-id="78bef-310">Retourne les paramètres d’algorithme de clé hello du certificat x.509v.3 hello sous forme de chaîne hexadécimale.</span><span class="sxs-lookup"><span data-stu-id="78bef-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="78bef-311">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="78bef-312">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-313">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="78bef-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="78bef-314">CertNameInfo</span></span>
<span data-ttu-id="78bef-315">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-315">**Description:**</span></span>  
<span data-ttu-id="78bef-316">Retourne l’émetteur et l’objet de hello noms à partir d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="78bef-317">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="78bef-318">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-319">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="78bef-320">X509NameType : hello valeur X509NameType pour l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="78bef-321">includesIssuerName : nom de l’émetteur de hello tooinclude true ; Sinon, false.</span><span class="sxs-lookup"><span data-stu-id="78bef-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="78bef-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="78bef-322">CertNotAfter</span></span>
<span data-ttu-id="78bef-323">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-323">**Description:**</span></span>  
<span data-ttu-id="78bef-324">Retourne la date de hello en heure locale après laquelle un certificat n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="78bef-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="78bef-325">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="78bef-326">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-327">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="78bef-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="78bef-328">CertNotBefore</span></span>
<span data-ttu-id="78bef-329">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-329">**Description:**</span></span>  
<span data-ttu-id="78bef-330">Retourne la date de hello en heure locale à laquelle un certificat devient valide.</span><span class="sxs-lookup"><span data-stu-id="78bef-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="78bef-331">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="78bef-332">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-333">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="78bef-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="78bef-334">CertPublicKeyOid</span></span>
<span data-ttu-id="78bef-335">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-335">**Description:**</span></span>  
<span data-ttu-id="78bef-336">Retourne hello Oid de la clé publique hello du certificat x.509v.3 hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="78bef-337">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="78bef-338">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-339">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="78bef-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="78bef-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="78bef-341">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-341">**Description:**</span></span>  
<span data-ttu-id="78bef-342">Retourne hello Oid hello paramètres de clé publique pour le certificat X.509v3 de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="78bef-343">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="78bef-344">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-345">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="78bef-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="78bef-346">CertSerialNumber</span></span>
<span data-ttu-id="78bef-347">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-347">**Description:**</span></span>  
<span data-ttu-id="78bef-348">Retourne le numéro de série hello du certificat X.509v3 de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="78bef-349">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="78bef-350">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-351">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="78bef-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="78bef-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="78bef-353">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-353">**Description:**</span></span>  
<span data-ttu-id="78bef-354">Retourne hello Oid de l’algorithme de hello utilisé signature de hello toocreate d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="78bef-355">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="78bef-356">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-357">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="78bef-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="78bef-358">CertSubject</span></span>
<span data-ttu-id="78bef-359">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-359">**Description:**</span></span>  
<span data-ttu-id="78bef-360">Obtient hello nom unique du sujet d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="78bef-361">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="78bef-362">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-363">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="78bef-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="78bef-364">CertSubjectNameDN</span></span>
<span data-ttu-id="78bef-365">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-365">**Description:**</span></span>  
<span data-ttu-id="78bef-366">Retourne hello nom unique du sujet d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="78bef-367">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="78bef-368">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-369">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="78bef-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="78bef-370">CertSubjectNameOid</span></span>
<span data-ttu-id="78bef-371">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-371">**Description:**</span></span>  
<span data-ttu-id="78bef-372">Retourne hello Oid de nom de l’objet hello à partir d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="78bef-373">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="78bef-374">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-375">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="78bef-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="78bef-376">CertThumbprint</span></span>
<span data-ttu-id="78bef-377">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-377">**Description:**</span></span>  
<span data-ttu-id="78bef-378">Hello retourne l’empreinte numérique d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="78bef-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="78bef-379">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="78bef-380">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-381">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="78bef-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="78bef-382">CertVersion</span></span>
<span data-ttu-id="78bef-383">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-383">**Description:**</span></span>  
<span data-ttu-id="78bef-384">Retourne hello version du format d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="78bef-385">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="78bef-386">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-387">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="78bef-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-388">CGuid</span></span>
<span data-ttu-id="78bef-389">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-389">**Description:**</span></span>  
<span data-ttu-id="78bef-390">Hello fonction CGuid convertit la représentation sous forme de chaîne hello d’une représentation binaire de GUID tooits.</span><span class="sxs-lookup"><span data-stu-id="78bef-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="78bef-391">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="78bef-392">Une chaîne rédigée au format suivant : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="78bef-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="78bef-393">Contains</span><span class="sxs-lookup"><span data-stu-id="78bef-393">Contains</span></span>
<span data-ttu-id="78bef-394">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-394">**Description:**</span></span>  
<span data-ttu-id="78bef-395">fonction de Hello Contains recherche une chaîne à l’intérieur d’un attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="78bef-396">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-396">**Syntax:**</span></span>  
<span data-ttu-id="78bef-397">`num Contains (mvstring attribute, str search)` - sensible à la casse</span><span class="sxs-lookup"><span data-stu-id="78bef-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="78bef-398">`num Contains (mvref attribute, str search)` - sensible à la casse</span><span class="sxs-lookup"><span data-stu-id="78bef-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="78bef-399">attribut : hello attribut à valeurs multiples toosearch.</span><span class="sxs-lookup"><span data-stu-id="78bef-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="78bef-400">recherche : chaîne toofind dans l’attribut de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="78bef-401">Casetype : CaseInsensitive ou CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="78bef-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="78bef-402">Retourne les index dans l’attribut à valeurs multiples hello où la chaîne de hello a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="78bef-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="78bef-403">0 est retourné si la chaîne de hello est introuvable.</span><span class="sxs-lookup"><span data-stu-id="78bef-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="78bef-404">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-404">**Remarks:**</span></span>  
<span data-ttu-id="78bef-405">Pour les attributs de chaîne à valeurs multiples, hello recherche sous-chaînes dans les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="78bef-406">Pour les attributs de référence, hello chaîne recherchée doit correspondre exactement hello valeur toobe est considérée comme une correspondance.</span><span class="sxs-lookup"><span data-stu-id="78bef-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="78bef-407">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="78bef-408">Si l’attribut proxyAddresses de hello possède une adresse de messagerie principale (indiqué en majuscules « SMTP : »), puis revenez attribut proxyAddress de hello, sinon renvoie une erreur.</span><span class="sxs-lookup"><span data-stu-id="78bef-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="78bef-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="78bef-409">ConvertFromBase64</span></span>
<span data-ttu-id="78bef-410">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-410">**Description:**</span></span>  
<span data-ttu-id="78bef-411">Hello ConvertFromBase64 fonction convertit hello spécifié chaîne régulière du tooa valeur codée en base64.</span><span class="sxs-lookup"><span data-stu-id="78bef-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="78bef-412">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-412">**Syntax:**</span></span>  
<span data-ttu-id="78bef-413">`str ConvertFromBase64(str source)` - part du principe que l’encodage utilisé est Unicode</span><span class="sxs-lookup"><span data-stu-id="78bef-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="78bef-414">source : chaîne encodée Base64</span><span class="sxs-lookup"><span data-stu-id="78bef-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="78bef-415">En codage : Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="78bef-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="78bef-416">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="78bef-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="78bef-417">Les deux exemples renvoient «*Hello world!*»</span><span class="sxs-lookup"><span data-stu-id="78bef-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="78bef-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="78bef-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="78bef-419">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-419">**Description:**</span></span>  
<span data-ttu-id="78bef-420">Hello ConvertFromUTF8Hex fonction convertit hello spécifié la chaîne de tooa valeur encodée en UTF8 hexadécimal.</span><span class="sxs-lookup"><span data-stu-id="78bef-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="78bef-421">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="78bef-422">source : chaîne encodée sur 2 octets UTF8</span><span class="sxs-lookup"><span data-stu-id="78bef-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="78bef-423">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-423">**Remarks:**</span></span>  
<span data-ttu-id="78bef-424">Hello différence entre cette fonction et ConvertFromBase64([],UTF8) dans ce résultat hello est convivial pour l’attribut de nom unique hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="78bef-425">Ce format est utilisé par Azure Active Directory en tant que nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="78bef-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="78bef-426">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="78bef-427">Renvoie «*Hello world!*».</span><span class="sxs-lookup"><span data-stu-id="78bef-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="78bef-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="78bef-428">ConvertToBase64</span></span>
<span data-ttu-id="78bef-429">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-429">**Description:**</span></span>  
<span data-ttu-id="78bef-430">Hello fonction ConvertToBase64 convertit une chaîne de tooa la chaîne Unicode en base64.</span><span class="sxs-lookup"><span data-stu-id="78bef-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="78bef-431">Convertit la valeur hello d’un tableau d’entiers tooits équivalent représentation encodée en chiffres base 64.</span><span class="sxs-lookup"><span data-stu-id="78bef-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="78bef-432">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="78bef-433">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="78bef-434">Renvoie « SABlAGwAbABvACAAdwBvAHIAbABkACEA ».</span><span class="sxs-lookup"><span data-stu-id="78bef-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="78bef-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="78bef-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="78bef-436">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-436">**Description:**</span></span>  
<span data-ttu-id="78bef-437">Hello ConvertToUTF8Hex fonction convertit une chaîne de tooa les valeur encodée en UTF8 hexadécimal.</span><span class="sxs-lookup"><span data-stu-id="78bef-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="78bef-438">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="78bef-439">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-439">**Remarks:**</span></span>  
<span data-ttu-id="78bef-440">le format de sortie Hello de cette fonction est utilisé par Azure Active Directory en tant que format d’attribut DN.</span><span class="sxs-lookup"><span data-stu-id="78bef-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="78bef-441">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="78bef-442">Renvoie 48656C6C6F20776F726C6421.</span><span class="sxs-lookup"><span data-stu-id="78bef-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="78bef-443">Count</span><span class="sxs-lookup"><span data-stu-id="78bef-443">Count</span></span>
<span data-ttu-id="78bef-444">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-444">**Description:**</span></span>  
<span data-ttu-id="78bef-445">Hello fonction Count retourne le nombre de hello d’éléments dans un attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="78bef-446">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="78bef-447">CNum</span><span class="sxs-lookup"><span data-stu-id="78bef-447">CNum</span></span>
<span data-ttu-id="78bef-448">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-448">**Description:**</span></span>  
<span data-ttu-id="78bef-449">Hello fonction CNum prend une chaîne et retourne un type de données numérique.</span><span class="sxs-lookup"><span data-stu-id="78bef-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="78bef-450">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="78bef-451">CRef</span><span class="sxs-lookup"><span data-stu-id="78bef-451">CRef</span></span>
<span data-ttu-id="78bef-452">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-452">**Description:**</span></span>  
<span data-ttu-id="78bef-453">Convertit un attribut de chaîne de référence tooa</span><span class="sxs-lookup"><span data-stu-id="78bef-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="78bef-454">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="78bef-455">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="78bef-456">CStr</span><span class="sxs-lookup"><span data-stu-id="78bef-456">CStr</span></span>
<span data-ttu-id="78bef-457">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-457">**Description:**</span></span>  
<span data-ttu-id="78bef-458">Hello pour la fonction CStr convertit le type de données de chaîne de tooa.</span><span class="sxs-lookup"><span data-stu-id="78bef-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="78bef-459">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="78bef-460">valeur : peut être une valeur numérique, un attribut de référence ou une valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="78bef-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="78bef-461">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="78bef-462">Peut renvoyer « cn=Joe,dc=contoso,dc=com ».</span><span class="sxs-lookup"><span data-stu-id="78bef-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="78bef-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="78bef-463">DateAdd</span></span>
<span data-ttu-id="78bef-464">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-464">**Description:**</span></span>  
<span data-ttu-id="78bef-465">Retourne une valeur Date contenant une toowhich date qu'un intervalle de temps spécifié a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="78bef-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="78bef-466">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="78bef-467">intervalle : expression qui est l’intervalle de salutation pendant laquelle vous souhaitez que tooadd de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="78bef-468">chaîne de Hello doit avoir une des valeurs suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="78bef-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="78bef-469">yyyy Année</span><span class="sxs-lookup"><span data-stu-id="78bef-469">yyyy Year</span></span>
  * <span data-ttu-id="78bef-470">q Trimestre</span><span class="sxs-lookup"><span data-stu-id="78bef-470">q Quarter</span></span>
  * <span data-ttu-id="78bef-471">m Mois</span><span class="sxs-lookup"><span data-stu-id="78bef-471">m Month</span></span>
  * <span data-ttu-id="78bef-472">y Jour de l’année</span><span class="sxs-lookup"><span data-stu-id="78bef-472">y Day of year</span></span>
  * <span data-ttu-id="78bef-473">s Jour</span><span class="sxs-lookup"><span data-stu-id="78bef-473">d Day</span></span>
  * <span data-ttu-id="78bef-474">w Jour de la semaine</span><span class="sxs-lookup"><span data-stu-id="78bef-474">w Weekday</span></span>
  * <span data-ttu-id="78bef-475">ww Semaine</span><span class="sxs-lookup"><span data-stu-id="78bef-475">ww Week</span></span>
  * <span data-ttu-id="78bef-476">h Heure</span><span class="sxs-lookup"><span data-stu-id="78bef-476">h Hour</span></span>
  * <span data-ttu-id="78bef-477">n Minute</span><span class="sxs-lookup"><span data-stu-id="78bef-477">n Minute</span></span>
  * <span data-ttu-id="78bef-478">s Seconde</span><span class="sxs-lookup"><span data-stu-id="78bef-478">s Second</span></span>
* <span data-ttu-id="78bef-479">valeur : hello du nombre d’unités que tooadd.</span><span class="sxs-lookup"><span data-stu-id="78bef-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="78bef-480">Il peut être positif (dates tooget Bonjour futures) ou négatif (dates tooget Bonjour passées).</span><span class="sxs-lookup"><span data-stu-id="78bef-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="78bef-481">date : DateTime représentant date toowhich hello intervalle est ajouté.</span><span class="sxs-lookup"><span data-stu-id="78bef-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="78bef-482">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="78bef-483">Ajoute 3 mois et renvoie une valeur DateTime représentant « 2001-04-01 ».</span><span class="sxs-lookup"><span data-stu-id="78bef-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="78bef-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="78bef-484">DateFromNum</span></span>
<span data-ttu-id="78bef-485">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-485">**Description:**</span></span>  
<span data-ttu-id="78bef-486">Hello les fonction DateFromNum convertit une valeur dans tooa de format de date du AD type DateTime.</span><span class="sxs-lookup"><span data-stu-id="78bef-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="78bef-487">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="78bef-488">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="78bef-489">Renvoie une valeur DateTime représentant 2012-01-01 23:00:00.</span><span class="sxs-lookup"><span data-stu-id="78bef-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="78bef-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="78bef-490">DNComponent</span></span>
<span data-ttu-id="78bef-491">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-491">**Description:**</span></span>  
<span data-ttu-id="78bef-492">Hello les fonction DNComponent retourne la valeur hello un composant DN spécifié à partir de la gauche.</span><span class="sxs-lookup"><span data-stu-id="78bef-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="78bef-493">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="78bef-494">nom unique : hello référence attribut toointerpret</span><span class="sxs-lookup"><span data-stu-id="78bef-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="78bef-495">ComponentNumber : composant hello hello DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="78bef-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="78bef-496">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="78bef-497">Si dn est « cn=Joe,ou=… », la fonction renvoie Joe.</span><span class="sxs-lookup"><span data-stu-id="78bef-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="78bef-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="78bef-498">DNComponentRev</span></span>
<span data-ttu-id="78bef-499">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-499">**Description:**</span></span>  
<span data-ttu-id="78bef-500">Hello DNComponentRev fonction retourne la valeur hello d’un composant DN spécifié à partir de la droite (fin hello).</span><span class="sxs-lookup"><span data-stu-id="78bef-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="78bef-501">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="78bef-502">nom unique : hello référence attribut toointerpret</span><span class="sxs-lookup"><span data-stu-id="78bef-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="78bef-503">ComponentNumber - composant hello dans hello DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="78bef-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="78bef-504">Options : contrôleur de domaine – ignorer tous les composants avec « dc = »</span><span class="sxs-lookup"><span data-stu-id="78bef-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="78bef-505">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-505">**Example:**</span></span>  
<span data-ttu-id="78bef-506">Si le nom de domaine est « cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com », alors</span><span class="sxs-lookup"><span data-stu-id="78bef-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="78bef-507">Renvoient US.</span><span class="sxs-lookup"><span data-stu-id="78bef-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="78bef-508">Error</span><span class="sxs-lookup"><span data-stu-id="78bef-508">Error</span></span>
<span data-ttu-id="78bef-509">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-509">**Description:**</span></span>  
<span data-ttu-id="78bef-510">Hello fonction Error est utilisée tooreturn une erreur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="78bef-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="78bef-511">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="78bef-512">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="78bef-513">Si hello attribut accountName n’est pas présent, provoquent une erreur sur l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="78bef-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="78bef-514">EscapeDNComponent</span></span>
<span data-ttu-id="78bef-515">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-515">**Description:**</span></span>  
<span data-ttu-id="78bef-516">Hello fonction EscapeDNComponent prend un composant d’un nom unique et l’échappe afin qu’il peut être représentée dans l’annuaire LDAP.</span><span class="sxs-lookup"><span data-stu-id="78bef-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="78bef-517">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="78bef-518">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="78bef-519">Garantit que l’objet de hello peut être créé dans un annuaire LDAP même si l’attribut displayName de hello comporte des caractères qui doivent être échappés dans l’annuaire LDAP.</span><span class="sxs-lookup"><span data-stu-id="78bef-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="78bef-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="78bef-520">FormatDateTime</span></span>
<span data-ttu-id="78bef-521">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-521">**Description:**</span></span>  
<span data-ttu-id="78bef-522">fonction FormatDateTime de Hello est utilisé tooformat une chaîne de tooa date/heure au format spécifié.</span><span class="sxs-lookup"><span data-stu-id="78bef-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="78bef-523">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="78bef-524">valeur : une valeur au format de DateTime hello</span><span class="sxs-lookup"><span data-stu-id="78bef-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="78bef-525">format : une chaîne représentant le tooconvert de format hello pour.</span><span class="sxs-lookup"><span data-stu-id="78bef-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="78bef-526">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-526">**Remarks:**</span></span>  
<span data-ttu-id="78bef-527">Hello les valeurs possibles pour le format de hello se trouve ici : [Formats de Date/heure définis par l’utilisateur (fonction Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="78bef-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="78bef-528">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="78bef-529">Renvoie comme résultat « 2007-12-25 ».</span><span class="sxs-lookup"><span data-stu-id="78bef-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="78bef-530">Peut donner comme résultat « 20140905081453.0Z ».</span><span class="sxs-lookup"><span data-stu-id="78bef-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="78bef-531">GUID</span><span class="sxs-lookup"><span data-stu-id="78bef-531">GUID</span></span>
<span data-ttu-id="78bef-532">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-532">**Description:**</span></span>  
<span data-ttu-id="78bef-533">fonction de Hello GUID génère un nouveau GUID aléatoire.</span><span class="sxs-lookup"><span data-stu-id="78bef-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="78bef-534">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="78bef-535">IIF</span><span class="sxs-lookup"><span data-stu-id="78bef-535">IIF</span></span>
<span data-ttu-id="78bef-536">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-536">**Description:**</span></span>  
<span data-ttu-id="78bef-537">Hello fonction IIF renvoie l’un d’un ensemble de valeurs possibles selon une condition spécifiée.</span><span class="sxs-lookup"><span data-stu-id="78bef-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="78bef-538">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="78bef-539">condition : toute valeur ou expression qui peut être évaluée tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="78bef-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="78bef-540">valueIfTrue : si la condition de hello a la valeur tootrue, hello a retourné la valeur.</span><span class="sxs-lookup"><span data-stu-id="78bef-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="78bef-541">valueIfFalse : si la condition de hello a la valeur toofalse, hello a retourné la valeur.</span><span class="sxs-lookup"><span data-stu-id="78bef-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="78bef-542">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="78bef-543">Si l’utilisateur hello est intern, retourne l’alias hello d’un utilisateur avec « t- » ajouté toohello début, sinon retourne hello alias de l’utilisateur en l’état.</span><span class="sxs-lookup"><span data-stu-id="78bef-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="78bef-544">InStr</span><span class="sxs-lookup"><span data-stu-id="78bef-544">InStr</span></span>
<span data-ttu-id="78bef-545">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-545">**Description:**</span></span>  
<span data-ttu-id="78bef-546">Hello fonction InStr hello première occurrence d’une sous-chaîne dans une chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="78bef-547">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="78bef-548">contrôle de chaîne : toobe recherchée de chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="78bef-549">correspondance de chaîne : chaîne toobe trouvé</span><span class="sxs-lookup"><span data-stu-id="78bef-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="78bef-550">Démarrer : démarrage de position toofind hello sous-chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="78bef-551">compare : vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="78bef-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="78bef-552">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-552">**Remarks:**</span></span>  
<span data-ttu-id="78bef-553">Position de hello retourne où la sous-chaîne de hello a été trouvée ou 0 si introuvable.</span><span class="sxs-lookup"><span data-stu-id="78bef-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="78bef-554">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="78bef-555">Dans la liste too5</span><span class="sxs-lookup"><span data-stu-id="78bef-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="78bef-556">Prend la valeur too7</span><span class="sxs-lookup"><span data-stu-id="78bef-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="78bef-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="78bef-557">InStrRev</span></span>
<span data-ttu-id="78bef-558">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-558">**Description:**</span></span>  
<span data-ttu-id="78bef-559">Hello fonction InStrRev trouve hello dernière occurrence d’une sous-chaîne dans une chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="78bef-560">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="78bef-561">contrôle de chaîne : toobe recherchée de chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="78bef-562">correspondance de chaîne : chaîne toobe trouvé</span><span class="sxs-lookup"><span data-stu-id="78bef-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="78bef-563">Démarrer : démarrage de position toofind hello sous-chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="78bef-564">compare : vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="78bef-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="78bef-565">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-565">**Remarks:**</span></span>  
<span data-ttu-id="78bef-566">Position de hello retourne où la sous-chaîne de hello a été trouvée ou 0 si introuvable.</span><span class="sxs-lookup"><span data-stu-id="78bef-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="78bef-567">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="78bef-568">Renvoie 7.</span><span class="sxs-lookup"><span data-stu-id="78bef-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="78bef-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="78bef-569">IsBitSet</span></span>
<span data-ttu-id="78bef-570">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-570">**Description:**</span></span>  
<span data-ttu-id="78bef-571">fonction de Hello IsBitSet teste si un bit est défini ou non.</span><span class="sxs-lookup"><span data-stu-id="78bef-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="78bef-572">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="78bef-573">valeur : valeur numérique qui est évaluée. Flag : valeur numérique qui a hello bit toobe évaluée</span><span class="sxs-lookup"><span data-stu-id="78bef-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="78bef-574">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="78bef-575">Renvoie la valeur True, car le bit « 4 » est défini dans la valeur hexadécimale de hello « F »</span><span class="sxs-lookup"><span data-stu-id="78bef-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="78bef-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="78bef-576">IsDate</span></span>
<span data-ttu-id="78bef-577">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-577">**Description:**</span></span>  
<span data-ttu-id="78bef-578">Si l’expression de hello peut être évalue en un type DateTime, hello fonction IsDate prend la valeur tooTrue.</span><span class="sxs-lookup"><span data-stu-id="78bef-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="78bef-579">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="78bef-580">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-580">**Remarks:**</span></span>  
<span data-ttu-id="78bef-581">Utilisé toodetermine si CDate() peut aboutir.</span><span class="sxs-lookup"><span data-stu-id="78bef-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="78bef-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="78bef-582">IsCert</span></span>
<span data-ttu-id="78bef-583">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-583">**Description:**</span></span>  
<span data-ttu-id="78bef-584">Retourne la valeur true si les données brutes hello peuvent être sérialisées en objet de certificat .NET X509Certificate2.</span><span class="sxs-lookup"><span data-stu-id="78bef-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="78bef-585">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="78bef-586">certificateRawData : représentation en tableau d’octets d’un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="78bef-587">tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.</span><span class="sxs-lookup"><span data-stu-id="78bef-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="78bef-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="78bef-588">IsEmpty</span></span>
<span data-ttu-id="78bef-589">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-589">**Description:**</span></span>  
<span data-ttu-id="78bef-590">Si l’attribut de hello est présent dans hello CS ou MV mais prend la valeur tooan une chaîne vide, puis hello IsEmpty évalue tooTrue.</span><span class="sxs-lookup"><span data-stu-id="78bef-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="78bef-591">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="78bef-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-592">IsGuid</span></span>
<span data-ttu-id="78bef-593">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-593">**Description:**</span></span>  
<span data-ttu-id="78bef-594">Si la chaîne de hello a pu être converti tooa GUID, fonction IsGuid prend hello évaluée tootrue.</span><span class="sxs-lookup"><span data-stu-id="78bef-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="78bef-595">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="78bef-596">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-596">**Remarks:**</span></span>  
<span data-ttu-id="78bef-597">Un GUID est défini en tant que chaîne en fonction de l’un de ces modèles : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.</span><span class="sxs-lookup"><span data-stu-id="78bef-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="78bef-598">Utilisé toodetermine si la fonction CGuid() peut aboutir.</span><span class="sxs-lookup"><span data-stu-id="78bef-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="78bef-599">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="78bef-600">Si la valeur StrAttribute de hello a un format de GUID, renvoie une représentation binaire, sinon retourne une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="78bef-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="78bef-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="78bef-601">IsNull</span></span>
<span data-ttu-id="78bef-602">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-602">**Description:**</span></span>  
<span data-ttu-id="78bef-603">Si hello expression tooNull, IsNull (fonction) hello retourne true.</span><span class="sxs-lookup"><span data-stu-id="78bef-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="78bef-604">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="78bef-605">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-605">**Remarks:**</span></span>  
<span data-ttu-id="78bef-606">Pour un attribut, une valeur Null est exprimée par l’absence de hello d’attribut de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="78bef-607">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="78bef-608">Renvoie la valeur True si l’attribut de hello n’est pas présent dans hello CS ou MV.</span><span class="sxs-lookup"><span data-stu-id="78bef-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="78bef-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="78bef-609">IsNullOrEmpty</span></span>
<span data-ttu-id="78bef-610">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-610">**Description:**</span></span>  
<span data-ttu-id="78bef-611">Si l’expression de hello est une chaîne null ou vide, fonction de hello IsNullOrEmpty retourne true.</span><span class="sxs-lookup"><span data-stu-id="78bef-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="78bef-612">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="78bef-613">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-613">**Remarks:**</span></span>  
<span data-ttu-id="78bef-614">Pour un attribut, il évaluait tooTrue si l’attribut de hello est absent ou n’est présent, mais est une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="78bef-615">inverse Hello de cette fonction s’appelle IsPresent.</span><span class="sxs-lookup"><span data-stu-id="78bef-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="78bef-616">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="78bef-617">Renvoie la valeur True si l’attribut de hello n’est pas présent ou est une chaîne vide dans hello CS ou MV.</span><span class="sxs-lookup"><span data-stu-id="78bef-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="78bef-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="78bef-618">IsNumeric</span></span>
<span data-ttu-id="78bef-619">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-619">**Description:**</span></span>  
<span data-ttu-id="78bef-620">Hello fonction IsNumeric retourne une valeur booléenne indiquant si une expression peut être évaluée comme un type de nombre.</span><span class="sxs-lookup"><span data-stu-id="78bef-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="78bef-621">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="78bef-622">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-622">**Remarks:**</span></span>  
<span data-ttu-id="78bef-623">Utilisé toodetermine si CNum() peut être l’expression de hello tooparse réussie.</span><span class="sxs-lookup"><span data-stu-id="78bef-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="78bef-624">IsString</span><span class="sxs-lookup"><span data-stu-id="78bef-624">IsString</span></span>
<span data-ttu-id="78bef-625">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-625">**Description:**</span></span>  
<span data-ttu-id="78bef-626">Si l’expression de hello peut être évaluée tooa type chaîne, puis hello fonction IsString prend tooTrue.</span><span class="sxs-lookup"><span data-stu-id="78bef-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="78bef-627">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="78bef-628">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-628">**Remarks:**</span></span>  
<span data-ttu-id="78bef-629">Utilisé toodetermine si CStr() peut être l’expression de hello tooparse réussie.</span><span class="sxs-lookup"><span data-stu-id="78bef-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="78bef-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="78bef-630">IsPresent</span></span>
<span data-ttu-id="78bef-631">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-631">**Description:**</span></span>  
<span data-ttu-id="78bef-632">Si hello expression chaîne tooa qui n’est pas Null et n’est pas vide, puis hello IsPresent fonction retourne la valeur true.</span><span class="sxs-lookup"><span data-stu-id="78bef-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="78bef-633">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="78bef-634">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-634">**Remarks:**</span></span>  
<span data-ttu-id="78bef-635">inverse Hello de cette fonction s’appelle IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="78bef-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="78bef-636">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="78bef-637">Item</span><span class="sxs-lookup"><span data-stu-id="78bef-637">Item</span></span>
<span data-ttu-id="78bef-638">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-638">**Description:**</span></span>  
<span data-ttu-id="78bef-639">Hello fonction Item retourne un élément à partir d’un chaîne/attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="78bef-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="78bef-640">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="78bef-641">attribute : attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="78bef-642">index : élément de tooan d’index dans la chaîne à valeurs multiples hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="78bef-643">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-643">**Remarks:**</span></span>  
<span data-ttu-id="78bef-644">Hello fonction Item est utile avec hello fonction Contains comme fonction de ce dernier hello retourne tooan élément index du hello dans un attribut à valeurs multiples hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="78bef-645">Génère une erreur si l’index est hors limites.</span><span class="sxs-lookup"><span data-stu-id="78bef-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="78bef-646">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="78bef-647">Retourne hello adresse de messagerie principale.</span><span class="sxs-lookup"><span data-stu-id="78bef-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="78bef-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="78bef-648">ItemOrNull</span></span>
<span data-ttu-id="78bef-649">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-649">**Description:**</span></span>  
<span data-ttu-id="78bef-650">Hello fonction ItemOrNull retourne un élément à partir d’un chaîne/attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="78bef-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="78bef-651">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="78bef-652">attribute : attribut à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="78bef-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="78bef-653">index : élément de tooan d’index dans la chaîne à valeurs multiples hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="78bef-654">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-654">**Remarks:**</span></span>  
<span data-ttu-id="78bef-655">Hello fonction ItemOrNull est utile avec hello fonction Contains comme fonction de ce dernier hello retourne tooan élément index du hello dans un attribut à valeurs multiples hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="78bef-656">Renvoie une valeur Null si l’index est hors limites.</span><span class="sxs-lookup"><span data-stu-id="78bef-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="78bef-657">Join</span><span class="sxs-lookup"><span data-stu-id="78bef-657">Join</span></span>
<span data-ttu-id="78bef-658">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-658">**Description:**</span></span>  
<span data-ttu-id="78bef-659">fonction de jointure Hello prend une chaîne à valeurs multiples et retourne une chaîne à valeur unique avec séparateur spécifié inséré entre chaque élément.</span><span class="sxs-lookup"><span data-stu-id="78bef-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="78bef-660">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="78bef-661">attribut : attribut à valeurs multiples contenant des chaînes toobe joint.</span><span class="sxs-lookup"><span data-stu-id="78bef-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="78bef-662">délimiteur : toute chaîne tooseparate utilisé les sous-chaînes de hello Bonjour a retourné une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="78bef-663">Si omis, hello caractère espace (« ») est utilisé.</span><span class="sxs-lookup"><span data-stu-id="78bef-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="78bef-664">Si le délimiteur est une chaîne de longueur nulle (" ») ou rien du tout, tous les éléments de liste de hello sont concaténés sans délimiteurs.</span><span class="sxs-lookup"><span data-stu-id="78bef-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="78bef-665">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="78bef-665">**Remarks**</span></span>  
<span data-ttu-id="78bef-666">Il existe une parité entre hello jointure et des fonctions de fractionnement.</span><span class="sxs-lookup"><span data-stu-id="78bef-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="78bef-667">Hello fonction Join prend un tableau de chaînes et les joint à l’aide d’une chaîne de délimiteur, tooreturn une chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="78bef-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="78bef-668">Hello fonction Split prend une chaîne et la sépare au niveau du délimiteur hello, tooreturn un tableau de chaînes.</span><span class="sxs-lookup"><span data-stu-id="78bef-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="78bef-669">Toutefois, la principale différence est que Join peut concaténer des chaînes avec n’importe quelle chaîne de délimiteur, Split peut uniquement séparer des chaînes à l’aide d’un délimiteur de caractère unique.</span><span class="sxs-lookup"><span data-stu-id="78bef-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="78bef-670">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="78bef-671">Peut retourner : « SMTP:john.doe@contoso.com,smtp:jd@contoso.com »</span><span class="sxs-lookup"><span data-stu-id="78bef-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="78bef-672">LCase</span><span class="sxs-lookup"><span data-stu-id="78bef-672">LCase</span></span>
<span data-ttu-id="78bef-673">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-673">**Description:**</span></span>  
<span data-ttu-id="78bef-674">Hello fonction LCase convertit tous les caractères dans un cas de toolower de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="78bef-675">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="78bef-676">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="78bef-677">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="78bef-678">Left</span><span class="sxs-lookup"><span data-stu-id="78bef-678">Left</span></span>
<span data-ttu-id="78bef-679">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-679">**Description:**</span></span>  
<span data-ttu-id="78bef-680">fonction gauche Hello retourne un nombre spécifié de caractères à partir de la gauche hello d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="78bef-681">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="78bef-682">chaîne : hello caractères tooreturn de chaîne à partir de</span><span class="sxs-lookup"><span data-stu-id="78bef-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="78bef-683">NumChars : nombre identifiant le nombre hello de tooreturn de caractères à partir du début hello (gauche) de chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="78bef-684">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-684">**Remarks:**</span></span>  
<span data-ttu-id="78bef-685">Chaîne contenant les caractères numChars première hello dans la chaîne :</span><span class="sxs-lookup"><span data-stu-id="78bef-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="78bef-686">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="78bef-687">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78bef-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="78bef-688">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-688">If string is null, return empty string.</span></span>

<span data-ttu-id="78bef-689">Si la chaîne contient moins de caractères que le nombre de hello spécifié dans numChars, une chaîne de toostring identiques (c'est-à-dire, contenant tous les caractères dans le paramètre 1) est retournée.</span><span class="sxs-lookup"><span data-stu-id="78bef-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="78bef-690">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="78bef-691">Renvoie « Joh ».</span><span class="sxs-lookup"><span data-stu-id="78bef-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="78bef-692">Len</span><span class="sxs-lookup"><span data-stu-id="78bef-692">Len</span></span>
<span data-ttu-id="78bef-693">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-693">**Description:**</span></span>  
<span data-ttu-id="78bef-694">Hello fonction Len renvoie le nombre de caractères dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="78bef-695">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="78bef-696">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="78bef-697">Renvoie 8.</span><span class="sxs-lookup"><span data-stu-id="78bef-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="78bef-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="78bef-698">LTrim</span></span>
<span data-ttu-id="78bef-699">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-699">**Description:**</span></span>  
<span data-ttu-id="78bef-700">Hello fonction LTrim supprime les espaces de début d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="78bef-701">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="78bef-702">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="78bef-703">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="78bef-704">Mid</span><span class="sxs-lookup"><span data-stu-id="78bef-704">Mid</span></span>
<span data-ttu-id="78bef-705">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-705">**Description:**</span></span>  
<span data-ttu-id="78bef-706">Hello Mid, fonction retourne un nombre spécifié de caractères à partir d’une position spécifiée dans une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="78bef-707">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="78bef-708">chaîne : hello caractères tooreturn de chaîne à partir de</span><span class="sxs-lookup"><span data-stu-id="78bef-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="78bef-709">Démarrer : nombre identifiant hello en caractères tooreturn de chaîne à partir de la position de début</span><span class="sxs-lookup"><span data-stu-id="78bef-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="78bef-710">NumChars : nombre identifiant le nombre de hello de tooreturn de caractères à partir de la position dans la chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="78bef-711">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-711">**Remarks:**</span></span>  
<span data-ttu-id="78bef-712">Renvoie numChars caractères à partir de la position de départ dans la chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="78bef-713">Chaîne contenant numChars caractères à partir de la position de départ dans la chaîne :</span><span class="sxs-lookup"><span data-stu-id="78bef-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="78bef-714">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="78bef-715">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78bef-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="78bef-716">Si Démarrer > hello longueur de chaîne, retourne la chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78bef-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="78bef-717">Si start < = 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78bef-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="78bef-718">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-718">If string is null, return empty string.</span></span>

<span data-ttu-id="78bef-719">S’il ne reste pas numChars caractères dans la chaîne à partir de la position de départ, autant de caractères que possible sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="78bef-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="78bef-720">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="78bef-721">Renvoie « hn Do ».</span><span class="sxs-lookup"><span data-stu-id="78bef-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="78bef-722">Renvoie « Doe ».</span><span class="sxs-lookup"><span data-stu-id="78bef-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="78bef-723">Now</span><span class="sxs-lookup"><span data-stu-id="78bef-723">Now</span></span>
<span data-ttu-id="78bef-724">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-724">**Description:**</span></span>  
<span data-ttu-id="78bef-725">Hello maintenant fonction retourne une valeur DateTime spécifiant hello date et l’heure, en fonction de tooyour date l’ordinateur et heure système.</span><span class="sxs-lookup"><span data-stu-id="78bef-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="78bef-726">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="78bef-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="78bef-727">NumFromDate</span></span>
<span data-ttu-id="78bef-728">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-728">**Description:**</span></span>  
<span data-ttu-id="78bef-729">Hello fonction NumFromDate renvoie une date dans le format de date AD.</span><span class="sxs-lookup"><span data-stu-id="78bef-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="78bef-730">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="78bef-731">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="78bef-732">Renvoie 129699324000000000.</span><span class="sxs-lookup"><span data-stu-id="78bef-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="78bef-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="78bef-733">PadLeft</span></span>
<span data-ttu-id="78bef-734">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-734">**Description:**</span></span>  
<span data-ttu-id="78bef-735">Hello PadLeft fonction gauche remplit un tooa de chaîne spécifiée à l’aide d’un caractère de remplissage fourni de longueur.</span><span class="sxs-lookup"><span data-stu-id="78bef-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="78bef-736">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="78bef-737">chaîne : hello toopad de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-737">string: hello string toopad.</span></span>
* <span data-ttu-id="78bef-738">longueur : un nombre entier représentant hello souhaité de longueur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="78bef-739">padCharacter : chaîne composée d’un toouse caractère unique en tant que caractère de remplissage hello</span><span class="sxs-lookup"><span data-stu-id="78bef-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="78bef-740">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-740">**Remarks:**</span></span>

* <span data-ttu-id="78bef-741">Si la longueur de chaîne hello est inférieure à la longueur, padCharacter est ajouté à plusieurs reprises toohello début (gauche) de la chaîne jusqu'à ce qu’il a un toolength égale longueur.</span><span class="sxs-lookup"><span data-stu-id="78bef-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="78bef-742">PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.</span><span class="sxs-lookup"><span data-stu-id="78bef-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="78bef-743">Si la longueur de chaîne hello est égal tooor supérieure à la longueur, la chaîne est retournée sans modification.</span><span class="sxs-lookup"><span data-stu-id="78bef-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="78bef-744">Si la chaîne a une longueur supérieure à ou un toolength égal, un toostring identiques de chaîne est retournée.</span><span class="sxs-lookup"><span data-stu-id="78bef-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="78bef-745">Si la longueur de chaîne hello est inférieure à la longueur, une nouvelle chaîne Hello souhaité longueur est retournée contenant string remplie avec un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="78bef-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="78bef-746">Si la chaîne est null, la fonction hello retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="78bef-747">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="78bef-748">Renvoie « 000000User ».</span><span class="sxs-lookup"><span data-stu-id="78bef-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="78bef-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="78bef-749">PadRight</span></span>
<span data-ttu-id="78bef-750">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-750">**Description:**</span></span>  
<span data-ttu-id="78bef-751">Hello PadRight fonction droite remplit un tooa de chaîne spécifiée à l’aide d’un caractère de remplissage fourni de longueur.</span><span class="sxs-lookup"><span data-stu-id="78bef-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="78bef-752">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="78bef-753">chaîne : hello toopad de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-753">string: hello string toopad.</span></span>
* <span data-ttu-id="78bef-754">longueur : un nombre entier représentant hello souhaité de longueur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="78bef-755">padCharacter : chaîne composée d’un toouse caractère unique en tant que caractère de remplissage hello</span><span class="sxs-lookup"><span data-stu-id="78bef-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="78bef-756">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-756">**Remarks:**</span></span>

* <span data-ttu-id="78bef-757">Si la longueur de chaîne hello est inférieure à la longueur, padCharacter est ajouté à plusieurs reprises toohello fin (droite) de la chaîne jusqu'à ce qu’il a un toolength égale longueur.</span><span class="sxs-lookup"><span data-stu-id="78bef-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="78bef-758">PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.</span><span class="sxs-lookup"><span data-stu-id="78bef-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="78bef-759">Si la longueur de chaîne hello est égal tooor supérieure à la longueur, la chaîne est retournée sans modification.</span><span class="sxs-lookup"><span data-stu-id="78bef-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="78bef-760">Si la chaîne a une longueur supérieure à ou un toolength égal, un toostring identiques de chaîne est retournée.</span><span class="sxs-lookup"><span data-stu-id="78bef-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="78bef-761">Si la longueur de chaîne hello est inférieure à la longueur, une nouvelle chaîne Hello souhaité longueur est retournée contenant string remplie avec un padCharacter.</span><span class="sxs-lookup"><span data-stu-id="78bef-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="78bef-762">Si la chaîne est null, la fonction hello retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="78bef-763">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="78bef-764">Renvoie « User000000 ».</span><span class="sxs-lookup"><span data-stu-id="78bef-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="78bef-765">PCase</span><span class="sxs-lookup"><span data-stu-id="78bef-765">PCase</span></span>
<span data-ttu-id="78bef-766">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-766">**Description:**</span></span>  
<span data-ttu-id="78bef-767">Hello fonction PCase convertit hello premier caractère de chaque mot délimité par des espaces dans un cas de tooupper de chaîne, et tous les autres caractères sont converties en cas de toolower.</span><span class="sxs-lookup"><span data-stu-id="78bef-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="78bef-768">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="78bef-769">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-769">**Remarks:**</span></span>

* <span data-ttu-id="78bef-770">Cette fonction ne fournit pas actuellement une casse appropriée tooconvert un mot qui est entièrement en majuscule, par exemple un acronyme.</span><span class="sxs-lookup"><span data-stu-id="78bef-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="78bef-771">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="78bef-772">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="78bef-773">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="78bef-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="78bef-774">RandomNum</span></span>
<span data-ttu-id="78bef-775">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-775">**Description:**</span></span>  
<span data-ttu-id="78bef-776">Hello fonction RandomNum retourne un nombre aléatoire entre un intervalle spécifié.</span><span class="sxs-lookup"><span data-stu-id="78bef-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="78bef-777">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="78bef-778">Démarrer : une identification hello inférieure limite de hello valeur aléatoire toogenerate</span><span class="sxs-lookup"><span data-stu-id="78bef-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="78bef-779">fin : une identification hello supérieur limite de hello valeur aléatoire toogenerate</span><span class="sxs-lookup"><span data-stu-id="78bef-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="78bef-780">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="78bef-781">Peut renvoyer 734.</span><span class="sxs-lookup"><span data-stu-id="78bef-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="78bef-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="78bef-782">RemoveDuplicates</span></span>
<span data-ttu-id="78bef-783">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-783">**Description:**</span></span>  
<span data-ttu-id="78bef-784">Hello fonction RemoveDuplicates prend une chaîne à valeurs multiples et assurez-vous que chaque valeur est unique.</span><span class="sxs-lookup"><span data-stu-id="78bef-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="78bef-785">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="78bef-786">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="78bef-787">Renvoie un attribut proxyAddress expurgé duquel toutes les valeurs en double ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="78bef-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="78bef-788">Replace</span><span class="sxs-lookup"><span data-stu-id="78bef-788">Replace</span></span>
<span data-ttu-id="78bef-789">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-789">**Description:**</span></span>  
<span data-ttu-id="78bef-790">Hello fonction Replace remplace toutes les occurrences d’une chaîne tooanother de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="78bef-791">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="78bef-792">chaîne : les valeurs dans un tooreplace de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="78bef-793">Ancienne valeur : tooreplace et toosearch de chaîne hello pour.</span><span class="sxs-lookup"><span data-stu-id="78bef-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="78bef-794">NewValue : hello chaîne tooreplace à.</span><span class="sxs-lookup"><span data-stu-id="78bef-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="78bef-795">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-795">**Remarks:**</span></span>  
<span data-ttu-id="78bef-796">fonction Hello reconnaît hello suivant monikers spéciaux suivants :</span><span class="sxs-lookup"><span data-stu-id="78bef-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="78bef-797">\n – Nouvelle ligne</span><span class="sxs-lookup"><span data-stu-id="78bef-797">\n – New Line</span></span>
* <span data-ttu-id="78bef-798">\r – Retour chariot</span><span class="sxs-lookup"><span data-stu-id="78bef-798">\r – Carriage Return</span></span>
* <span data-ttu-id="78bef-799">\t – Tabulation</span><span class="sxs-lookup"><span data-stu-id="78bef-799">\t – Tab</span></span>

<span data-ttu-id="78bef-800">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="78bef-801">Remplace CRLF par une virgule et un espace et peut entraîner une trop « One Microsoft Way, Redmond, WA, États-Unis »</span><span class="sxs-lookup"><span data-stu-id="78bef-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="78bef-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="78bef-802">ReplaceChars</span></span>
<span data-ttu-id="78bef-803">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-803">**Description:**</span></span>  
<span data-ttu-id="78bef-804">Hello fonction ReplaceChars remplace toutes les occurrences des caractères trouvés dans hello chaîne ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="78bef-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="78bef-805">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="78bef-806">chaîne : un tooreplace de chaîne de caractères dans.</span><span class="sxs-lookup"><span data-stu-id="78bef-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="78bef-807">ReplacePattern : une chaîne qui contient un dictionnaire avec tooreplace de caractères.</span><span class="sxs-lookup"><span data-stu-id="78bef-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="78bef-808">Hello format est {source1} : {cible1}, {source2} : {cible2}, {sourceN}, {Ciblen} où source est hello caractère toofind et cible hello chaîne tooreplace avec.</span><span class="sxs-lookup"><span data-stu-id="78bef-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="78bef-809">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-809">**Remarks:**</span></span>

* <span data-ttu-id="78bef-810">fonction Hello prend chaque occurrence des sources définies et les remplace par les cibles hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="78bef-811">source de Hello doit être exactement un caractère (unicode).</span><span class="sxs-lookup"><span data-stu-id="78bef-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="78bef-812">source de Hello ne peut pas être vide ni dépasser un caractère (erreur d’analyse).</span><span class="sxs-lookup"><span data-stu-id="78bef-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="78bef-813">cible de Hello peut avoir plusieurs caractères, par exemple ö : oe, β : ss.</span><span class="sxs-lookup"><span data-stu-id="78bef-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="78bef-814">cible de Hello peut être vide, indiquant que les caractères hello doivent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="78bef-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="78bef-815">source de Hello respecte la casse et doit être une correspondance exacte.</span><span class="sxs-lookup"><span data-stu-id="78bef-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="78bef-816">Bonjour, (virgule) et : (deux-points) sont des caractères réservés et ne peut pas être remplacé à l’aide de cette fonction.</span><span class="sxs-lookup"><span data-stu-id="78bef-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="78bef-817">Les espaces et autres caractères blancs Bonjour chaîne ReplacePattern sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="78bef-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="78bef-818">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="78bef-819">Renvoie Raksmorgas.</span><span class="sxs-lookup"><span data-stu-id="78bef-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="78bef-820">Retourne « ONeil », graduation hello est défini toobe supprimé.</span><span class="sxs-lookup"><span data-stu-id="78bef-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="78bef-821">Right</span><span class="sxs-lookup"><span data-stu-id="78bef-821">Right</span></span>
<span data-ttu-id="78bef-822">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-822">**Description:**</span></span>  
<span data-ttu-id="78bef-823">fonction Hello retourne un nombre spécifié de caractères à partir de hello droite (fin) d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="78bef-824">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="78bef-825">chaîne : hello caractères tooreturn de chaîne à partir de</span><span class="sxs-lookup"><span data-stu-id="78bef-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="78bef-826">NumChars : nombre identifiant le nombre de hello de tooreturn caractères de fin hello (à droite) de chaîne</span><span class="sxs-lookup"><span data-stu-id="78bef-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="78bef-827">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-827">**Remarks:**</span></span>  
<span data-ttu-id="78bef-828">Les caractères NumChars sont retournées à partir de la dernière position de hello de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="78bef-829">Chaîne contenant les caractères numChars dernière hello dans la chaîne :</span><span class="sxs-lookup"><span data-stu-id="78bef-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="78bef-830">Si numChars = 0, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="78bef-831">Si numChars < 0, retourne une chaîne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78bef-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="78bef-832">Si la chaîne est null, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-832">If string is null, return empty string.</span></span>

<span data-ttu-id="78bef-833">Si la chaîne contient moins de caractères hello nombre spécifié dans NumChars, une toostring identiques de chaîne est retournée.</span><span class="sxs-lookup"><span data-stu-id="78bef-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="78bef-834">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="78bef-835">Renvoie « Doe ».</span><span class="sxs-lookup"><span data-stu-id="78bef-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="78bef-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="78bef-836">RTrim</span></span>
<span data-ttu-id="78bef-837">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-837">**Description:**</span></span>  
<span data-ttu-id="78bef-838">Hello RTrim (fonction) supprime les espaces de fin d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="78bef-839">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="78bef-840">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="78bef-841">Renvoie « Test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="78bef-842">Sélectionnez</span><span class="sxs-lookup"><span data-stu-id="78bef-842">Select</span></span>
<span data-ttu-id="78bef-843">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-843">**Description:**</span></span>  
<span data-ttu-id="78bef-844">Traite toutes les valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) selon la fonction spécifiée.</span><span class="sxs-lookup"><span data-stu-id="78bef-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="78bef-845">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="78bef-846">élément : représente un élément dans un attribut à valeurs multiples hello</span><span class="sxs-lookup"><span data-stu-id="78bef-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="78bef-847">attribut : attribut à valeurs multiples hello</span><span class="sxs-lookup"><span data-stu-id="78bef-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="78bef-848">expression : expression qui retourne une collection de valeurs</span><span class="sxs-lookup"><span data-stu-id="78bef-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="78bef-849">condition : n’importe quelle fonction qui peut traiter un élément dans l’attribut de hello</span><span class="sxs-lookup"><span data-stu-id="78bef-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="78bef-850">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="78bef-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="78bef-851">Retourner toutes les valeurs hello dans donnez d’attribut à valeurs multiples hello après la suppression des traits d’union (-).</span><span class="sxs-lookup"><span data-stu-id="78bef-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="78bef-852">Split</span><span class="sxs-lookup"><span data-stu-id="78bef-852">Split</span></span>
<span data-ttu-id="78bef-853">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-853">**Description:**</span></span>  
<span data-ttu-id="78bef-854">Hello fonction Split prend une chaîne séparée par un délimiteur et le rend une chaîne à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="78bef-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="78bef-855">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="78bef-856">valeur : hello chaîne avec un tooseparate de caractère délimiteur.</span><span class="sxs-lookup"><span data-stu-id="78bef-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="78bef-857">délimiteur : unique toobe de caractère utilisé comme séparateur de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="78bef-858">limit : nombre maximal de valeurs qu’il est possible de renvoyer.</span><span class="sxs-lookup"><span data-stu-id="78bef-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="78bef-859">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="78bef-860">Retourne une chaîne à valeurs multiples comprenant 2 éléments utiles pour l’attribut proxyAddress de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="78bef-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="78bef-861">StringFromGuid</span></span>
<span data-ttu-id="78bef-862">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-862">**Description:**</span></span>  
<span data-ttu-id="78bef-863">Hello fonction StringFromGuid prend un GUID binaire et il convertit la chaîne de tooa</span><span class="sxs-lookup"><span data-stu-id="78bef-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="78bef-864">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="78bef-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="78bef-865">StringFromSid</span></span>
<span data-ttu-id="78bef-866">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-866">**Description:**</span></span>  
<span data-ttu-id="78bef-867">Hello les fonction StringFromSid convertit un tableau d’octets contenant la chaîne tooa d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="78bef-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="78bef-868">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="78bef-869">Switch</span><span class="sxs-lookup"><span data-stu-id="78bef-869">Switch</span></span>
<span data-ttu-id="78bef-870">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-870">**Description:**</span></span>  
<span data-ttu-id="78bef-871">fonction Switch de Hello est tooreturn utilisé une valeur unique en fonction des conditions évaluées.</span><span class="sxs-lookup"><span data-stu-id="78bef-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="78bef-872">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="78bef-873">expr : expression de type Variant tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="78bef-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="78bef-874">valeur : valeur toobe retournée si l’expression correspondante hello est True.</span><span class="sxs-lookup"><span data-stu-id="78bef-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="78bef-875">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-875">**Remarks:**</span></span>  
<span data-ttu-id="78bef-876">Hello argument de la fonction Switch liste se compose de paires d’expressions et de valeurs.</span><span class="sxs-lookup"><span data-stu-id="78bef-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="78bef-877">expressions de Hello sont évaluées de gauche tooright et valeur hello associée hello première expression tooevaluate tooTrue est retournée.</span><span class="sxs-lookup"><span data-stu-id="78bef-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="78bef-878">Si les parties hello ne sont pas correctement appariées, une erreur d’exécution se produit.</span><span class="sxs-lookup"><span data-stu-id="78bef-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="78bef-879">Par exemple, si expr1 est True, Switch renvoie la valeur1.</span><span class="sxs-lookup"><span data-stu-id="78bef-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="78bef-880">Si expr-1 est False, mais expr-2 est True, Switch renvoie la valeur 2, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="78bef-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="78bef-881">Switch ne renvoie rien si :</span><span class="sxs-lookup"><span data-stu-id="78bef-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="78bef-882">Aucune des expressions de hello ont la valeur True.</span><span class="sxs-lookup"><span data-stu-id="78bef-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="78bef-883">première expression de True Hello possède une valeur correspondante qui a la valeur Null.</span><span class="sxs-lookup"><span data-stu-id="78bef-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="78bef-884">Switch évalue toutes les expressions, même si elle n’en renvoie qu’une.</span><span class="sxs-lookup"><span data-stu-id="78bef-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="78bef-885">Pour cette raison, il est conseillé de surveiller les éventuels effets secondaires.</span><span class="sxs-lookup"><span data-stu-id="78bef-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="78bef-886">Par exemple, si l’évaluation de hello d’une expression entraîne une division par zéro, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="78bef-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="78bef-887">Valeur peut être également la fonction d’erreur hello, qui retourne une chaîne personnalisée.</span><span class="sxs-lookup"><span data-stu-id="78bef-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="78bef-888">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="78bef-889">Renvoie la langue de hello parlée dans certaines grandes villes, sinon retourne une erreur.</span><span class="sxs-lookup"><span data-stu-id="78bef-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="78bef-890">Trim</span><span class="sxs-lookup"><span data-stu-id="78bef-890">Trim</span></span>
<span data-ttu-id="78bef-891">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-891">**Description:**</span></span>  
<span data-ttu-id="78bef-892">fonction Trim Hello supprime les espaces à gauche et blanc à partir d’une chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="78bef-893">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="78bef-894">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="78bef-895">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="78bef-896">Supprime les espaces à gauche et pour chaque valeur de l’attribut proxyAddress de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="78bef-897">UCase</span><span class="sxs-lookup"><span data-stu-id="78bef-897">UCase</span></span>
<span data-ttu-id="78bef-898">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-898">**Description:**</span></span>  
<span data-ttu-id="78bef-899">Hello fonction UCase convertit tous les caractères dans un cas de tooupper de chaîne.</span><span class="sxs-lookup"><span data-stu-id="78bef-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="78bef-900">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="78bef-901">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="78bef-902">Renvoie « test ».</span><span class="sxs-lookup"><span data-stu-id="78bef-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="78bef-903">Where</span><span class="sxs-lookup"><span data-stu-id="78bef-903">Where</span></span>

<span data-ttu-id="78bef-904">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-904">**Description:**</span></span>  
<span data-ttu-id="78bef-905">Retourne un sous-ensemble de valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) en fonction de la condition.</span><span class="sxs-lookup"><span data-stu-id="78bef-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="78bef-906">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="78bef-907">élément : représente un élément dans un attribut à valeurs multiples hello</span><span class="sxs-lookup"><span data-stu-id="78bef-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="78bef-908">attribut : attribut à valeurs multiples hello</span><span class="sxs-lookup"><span data-stu-id="78bef-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="78bef-909">condition : toute expression qui peut être évaluée tootrue ou false</span><span class="sxs-lookup"><span data-stu-id="78bef-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="78bef-910">expression : expression qui retourne une collection de valeurs</span><span class="sxs-lookup"><span data-stu-id="78bef-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="78bef-911">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="78bef-912">Retourner des valeurs de certificat hello dans userCertificate d’attribut à valeurs multiples hello qui ne sont pas expiré.</span><span class="sxs-lookup"><span data-stu-id="78bef-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="78bef-913">With</span><span class="sxs-lookup"><span data-stu-id="78bef-913">With</span></span>
<span data-ttu-id="78bef-914">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-914">**Description:**</span></span>  
<span data-ttu-id="78bef-915">Hello avec fonction fournit une toosimplify de façon à une expression complexe à l’aide d’une variable toorepresent une sous-expression qui apparaît une ou plusieurs fois dans une expression complexe de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="78bef-916">**Syntaxe**
`With(var variable, exp subExpression, exp complexExpression)` :</span><span class="sxs-lookup"><span data-stu-id="78bef-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="78bef-917">variable : représente hello sous-expression.</span><span class="sxs-lookup"><span data-stu-id="78bef-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="78bef-918">subExpression : sous-expression représentée par une variable.</span><span class="sxs-lookup"><span data-stu-id="78bef-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="78bef-919">complexExpression : expression complexe.</span><span class="sxs-lookup"><span data-stu-id="78bef-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="78bef-920">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="78bef-921">Fonctionnellement équivalent à :</span><span class="sxs-lookup"><span data-stu-id="78bef-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="78bef-922">Qui retourne uniquement les valeurs de certificat valide dans l’attribut userCertificate de hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="78bef-923">Word</span><span class="sxs-lookup"><span data-stu-id="78bef-923">Word</span></span>
<span data-ttu-id="78bef-924">**Description :**</span><span class="sxs-lookup"><span data-stu-id="78bef-924">**Description:**</span></span>  
<span data-ttu-id="78bef-925">Hello fonction Word renvoie un mot contenu dans la chaîne, en fonction des paramètres décrivant hello délimiteurs toouse et tooreturn nombre du mot hello.</span><span class="sxs-lookup"><span data-stu-id="78bef-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="78bef-926">**Syntaxe :**</span><span class="sxs-lookup"><span data-stu-id="78bef-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="78bef-927">chaîne : hello chaîne tooreturn un mot.</span><span class="sxs-lookup"><span data-stu-id="78bef-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="78bef-928">WordNumber : nombre identifiant le nombre de mots à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="78bef-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="78bef-929">délimiteurs : une chaîne représentant un ou plusieurs délimiteurs hello qui doivent être utilisés tooidentify mots</span><span class="sxs-lookup"><span data-stu-id="78bef-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="78bef-930">**Remarques :**</span><span class="sxs-lookup"><span data-stu-id="78bef-930">**Remarks:**</span></span>  
<span data-ttu-id="78bef-931">Chaque chaîne de caractères dans une chaîne séparée par hello un des caractères hello dans les délimiteurs sont identifiés en tant que mots :</span><span class="sxs-lookup"><span data-stu-id="78bef-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="78bef-932">Si number < 1, retourne une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="78bef-933">Si string a la valeur null, renvoie une chaîne vide.</span><span class="sxs-lookup"><span data-stu-id="78bef-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="78bef-934">Si la chaîne contient moins de mots ou ne contient pas les mots identifiés par les séparateurs, une chaîne vide est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="78bef-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="78bef-935">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="78bef-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="78bef-936">Retourne « brown ».</span><span class="sxs-lookup"><span data-stu-id="78bef-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="78bef-937">Retourne « has ».</span><span class="sxs-lookup"><span data-stu-id="78bef-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78bef-938">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="78bef-938">Additional Resources</span></span>
* [<span data-ttu-id="78bef-939">Comprendre les expressions d’approvisionnement déclaratif</span><span class="sxs-lookup"><span data-stu-id="78bef-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="78bef-940">Azure AD Connect Sync : personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="78bef-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="78bef-941">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78bef-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
