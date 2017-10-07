---
title: "aaaKey notes de mise à jour de coffre .NET 2.x API | Documents Microsoft"
description: "Les développeurs .NET utilisera cette toocode API pour Azure Key Vault"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="4a31d-103">Azure Key Vault .NET 2.0 - Notes de publication et guide de migration</span><span class="sxs-lookup"><span data-stu-id="4a31d-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="4a31d-104">Hello des remarques et conseils suivants sont destinés aux développeurs qui travaillent avec Azure Key Vault .NET / bibliothèque de c#.</span><span class="sxs-lookup"><span data-stu-id="4a31d-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="4a31d-105">Dans la transition hello à partir d’une version toohello 2.0 hello 1.0, un nombre de mises à jour ont été apportée seront nécessiter du travail de migration dans votre code afin que vous toobenefit les améliorations fonctionnelles hello et ajouts de fonctionnalités telles que **le coffre de clés certificats** prend en charge.</span><span class="sxs-lookup"><span data-stu-id="4a31d-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="4a31d-106">Certificats Key Vault</span><span class="sxs-lookup"><span data-stu-id="4a31d-106">Key Vault certificates</span></span>

<span data-ttu-id="4a31d-107">Prise en charge des certificats de coffre de clés offre pour la gestion de votre x509 certificats et hello suit les comportements :</span><span class="sxs-lookup"><span data-stu-id="4a31d-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="4a31d-108">Permet un toocreate du propriétaire du certificat à un certificat via un processus de création du coffre de clés ou importation hello d’un certificat existant.</span><span class="sxs-lookup"><span data-stu-id="4a31d-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="4a31d-109">Cela concerne à la fois les certificats auto-signés et ceux générés par une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="4a31d-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="4a31d-110">Permet à un propriétaire de certificat du coffre de clés tooimplement le stockage sécurisé et gestion de X509 certificats sans interaction avec la clé privée.</span><span class="sxs-lookup"><span data-stu-id="4a31d-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="4a31d-111">Permet un toocreate du propriétaire du certificat à une stratégie qui dirige le coffre de clés toomanage hello cycle de vie d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="4a31d-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="4a31d-112">Permet les propriétaires de certificat tooprovide informations de contact pour la notification des événements de cycle de vie d’expiration et le renouvellement de certificat.</span><span class="sxs-lookup"><span data-stu-id="4a31d-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="4a31d-113">Prend en charge le renouvellement automatique avec des émetteurs sélectionnés : fournisseurs de certificats X509 de partenaire Key Vault/autorités de certification.</span><span class="sxs-lookup"><span data-stu-id="4a31d-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="4a31d-114">Remarque : fournisseurs/autorités Non associés sont également autorisées, mais le ne prendra pas en charge la fonctionnalité de renouvellement automatique hello.</span><span class="sxs-lookup"><span data-stu-id="4a31d-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="4a31d-115">Prise en charge de .NET</span><span class="sxs-lookup"><span data-stu-id="4a31d-115">.NET support</span></span>

* <span data-ttu-id="4a31d-116">**.NET 4.0** n’est pas pris en charge par version de hello 2.0 de hello Azure Key Vault .NET / bibliothèque c#</span><span class="sxs-lookup"><span data-stu-id="4a31d-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="4a31d-117">**.NET core** est pris en charge par la version 2.0 de hello Hello .NET d’Azure Key Vault / bibliothèque c#</span><span class="sxs-lookup"><span data-stu-id="4a31d-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="4a31d-118">Espaces de noms</span><span class="sxs-lookup"><span data-stu-id="4a31d-118">Namespaces</span></span>

* <span data-ttu-id="4a31d-119">Hello d’espace de noms pour **modèles** est remplacée par **Microsoft.Azure.KeyVault** trop**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="4a31d-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="4a31d-120">Hello **Microsoft.Azure.KeyVault.Internal** espace de noms est supprimé.</span><span class="sxs-lookup"><span data-stu-id="4a31d-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="4a31d-121">espace de noms Hello Azure SDK dépendances sont modifiés à partir de **Hyak.Common** et **Hyak.Common.Internals** trop**Microsoft.Rest** et  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="4a31d-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="4a31d-122">Modifications des types</span><span class="sxs-lookup"><span data-stu-id="4a31d-122">Type changes</span></span>

* <span data-ttu-id="4a31d-123">*Secret* modifié trop*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="4a31d-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="4a31d-124">*Dictionnaire* modifié trop*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="4a31d-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="4a31d-125">*Liste<T>, string []* modifié trop*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="4a31d-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="4a31d-126">*NextList* modifié trop *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="4a31d-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="4a31d-127">Types de retour</span><span class="sxs-lookup"><span data-stu-id="4a31d-127">Return types</span></span>

* <span data-ttu-id="4a31d-128">**KeyList** et **SecretList** renvoient *IPage<T>* au lieu de *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="4a31d-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="4a31d-129">Hello généré **BackupKeyAsync** retournera *BackupKeyResult* qui contient *valeur* (objet blob de sauvegarde).</span><span class="sxs-lookup"><span data-stu-id="4a31d-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="4a31d-130">Avant de hello méthode a été encapsulée et le retour seule valeur hello.</span><span class="sxs-lookup"><span data-stu-id="4a31d-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="4a31d-131">Exceptions</span><span class="sxs-lookup"><span data-stu-id="4a31d-131">Exceptions</span></span>

* <span data-ttu-id="4a31d-132">*KeyVaultClientException* est modifié trop*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="4a31d-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="4a31d-133">Erreur du service Hello est modifié de *exception. Erreur* trop*exception. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="4a31d-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="4a31d-134">Supprimer des informations supplémentaires à partir du message d’erreur hello pour **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="4a31d-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="4a31d-135">Constructeurs</span><span class="sxs-lookup"><span data-stu-id="4a31d-135">Constructors</span></span>

* <span data-ttu-id="4a31d-136">Au lieu d’accepter un *HttpClient* comme argument de constructeur, constructeur de hello accepte uniquement *HttpClientHandler* ou *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="4a31d-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="4a31d-137">Packages téléchargés</span><span class="sxs-lookup"><span data-stu-id="4a31d-137">Downloaded packages</span></span>

<span data-ttu-id="4a31d-138">Lorsqu’un client traite une dépendance sur suit hello de coffre de clés ont été téléchargés.</span><span class="sxs-lookup"><span data-stu-id="4a31d-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="4a31d-139">Liste des packages précédents</span><span class="sxs-lookup"><span data-stu-id="4a31d-139">Previous package list</span></span>

* <span data-ttu-id="4a31d-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="4a31d-148">Liste des packages actuels</span><span class="sxs-lookup"><span data-stu-id="4a31d-148">Current package list</span></span>

* <span data-ttu-id="4a31d-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="4a31d-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="4a31d-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="4a31d-152">Modifications de classe</span><span class="sxs-lookup"><span data-stu-id="4a31d-152">Class changes</span></span>

* <span data-ttu-id="4a31d-153">La classe **UnixEpoch** a été supprimée</span><span class="sxs-lookup"><span data-stu-id="4a31d-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="4a31d-154">**Base64UrlConverter** classe a été renommée trop**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="4a31d-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="4a31d-155">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="4a31d-155">Other changes</span></span>

* <span data-ttu-id="4a31d-156">Version toothis de hello API a été ajoutée à la prise en charge pour la configuration de hello de stratégie de nouvelle tentative d’opération KV sur les erreurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="4a31d-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="4a31d-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="4a31d-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="4a31d-158">Pour les opérations de hello retournent un *coffre*, type de retour de hello est une classe contenant une propriété de coffre.</span><span class="sxs-lookup"><span data-stu-id="4a31d-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="4a31d-159">Hello type de retour est désormais *coffre*.</span><span class="sxs-lookup"><span data-stu-id="4a31d-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="4a31d-160">*PermissionsToKeys* et *PermissionsToSecrets* sont à présent *Permissions.Keys* et *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="4a31d-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="4a31d-161">Certaines hello retourner les modifications de types s’appliquent toohello panneau ainsi.</span><span class="sxs-lookup"><span data-stu-id="4a31d-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="4a31d-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="4a31d-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="4a31d-163">package de Hello est alors divisé trop**Microsoft.Azure.KeyVault.Extensions** et **Microsoft.Azure.KeyVault.Cryptography** pour les opérations de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="4a31d-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

