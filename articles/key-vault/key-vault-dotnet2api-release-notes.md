---
title: "Notes de publication de l’API Key Vault .NET 2.x | Microsoft Docs"
description: "Les développeurs .NET utiliseront cette API pour coder pour Azure Key Vault"
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
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="b515b-103">Azure Key Vault .NET 2.0 - Notes de publication et guide de migration</span><span class="sxs-lookup"><span data-stu-id="b515b-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="b515b-104">Les notes et conseils suivants sont destinés aux développeurs utilisant Azure Key Vault .NET/bibliothèque C#.</span><span class="sxs-lookup"><span data-stu-id="b515b-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="b515b-105">Lors du passage de la version 1.0 à la version 2.0, un certain nombre de mises à jour effectuées nécessiteront un travail de migration dans votre code pour que vous puissiez bénéficier des améliorations fonctionnelles et des ajouts de fonctionnalités telles que la prise en charge des **certificats Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="b515b-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="b515b-106">Certificats Key Vault</span><span class="sxs-lookup"><span data-stu-id="b515b-106">Key Vault certificates</span></span>

<span data-ttu-id="b515b-107">La prise en charge des certificats Key Vault permet de gérer vos certificats x509 et les comportements suivants :</span><span class="sxs-lookup"><span data-stu-id="b515b-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="b515b-108">Permet à un propriétaire de certificat de créer un certificat via un processus de création de Key Vault ou l’importation d’un certificat existant.</span><span class="sxs-lookup"><span data-stu-id="b515b-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="b515b-109">Cela concerne à la fois les certificats auto-signés et ceux générés par une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="b515b-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="b515b-110">Permet à un propriétaire de certificat Key Vault d’implémenter le stockage sécurisé et la gestion des certificats X509 sans interaction avec des éléments de clé privée.</span><span class="sxs-lookup"><span data-stu-id="b515b-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="b515b-111">Permet à un propriétaire de certificat de créer une stratégie qui ordonne à Key Vault de gérer le cycle de vie d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="b515b-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="b515b-112">Permet aux propriétaires de certificat de fournir des informations de contact pour les notifications concernant des événements d’expiration du cycle de vie et le renouvellement de certificat.</span><span class="sxs-lookup"><span data-stu-id="b515b-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="b515b-113">Prend en charge le renouvellement automatique avec des émetteurs sélectionnés : fournisseurs de certificats X509 de partenaire Key Vault/autorités de certification.</span><span class="sxs-lookup"><span data-stu-id="b515b-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="b515b-114">REMARQUE : les fournisseurs/autorités non partenaires sont également autorisés, mais ils ne prendront pas en charge la fonctionnalité de renouvellement automatique.</span><span class="sxs-lookup"><span data-stu-id="b515b-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="b515b-115">Prise en charge de .NET</span><span class="sxs-lookup"><span data-stu-id="b515b-115">.NET support</span></span>

* <span data-ttu-id="b515b-116">**.NET 4.0** n’est pas pris en charge par la version 2.0 d’Azure Key Vault .NET/bibliothèque C#</span><span class="sxs-lookup"><span data-stu-id="b515b-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="b515b-117">**.NET Core** n’est pas pris en charge par la version 2.0 d’Azure Key Vault .NET/bibliothèque C#</span><span class="sxs-lookup"><span data-stu-id="b515b-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="b515b-118">Espaces de noms</span><span class="sxs-lookup"><span data-stu-id="b515b-118">Namespaces</span></span>

* <span data-ttu-id="b515b-119">L’espace de noms des **modèles** **Microsoft.Azure.KeyVault** est remplacé par **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="b515b-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="b515b-120">L’espace de noms **Microsoft.Azure.KeyVault.Internal** est supprimé.</span><span class="sxs-lookup"><span data-stu-id="b515b-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="b515b-121">L’espace de noms des dépendances du Kit de développement logiciel (SDK) Azure **Hyak.Common** et **Hyak.Common.Internals** est remplacé par **Microsoft.Rest** et **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="b515b-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="b515b-122">Modifications des types</span><span class="sxs-lookup"><span data-stu-id="b515b-122">Type changes</span></span>

* <span data-ttu-id="b515b-123">*Secret* est remplacé par *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="b515b-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="b515b-124">*Dictionary* est remplacé par *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="b515b-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="b515b-125">*List<T>, chaîne []* est remplacé par *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="b515b-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="b515b-126">*NextList* est remplacé par *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="b515b-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="b515b-127">Types de retour</span><span class="sxs-lookup"><span data-stu-id="b515b-127">Return types</span></span>

* <span data-ttu-id="b515b-128">**KeyList** et **SecretList** renvoient *IPage<T>* au lieu de *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="b515b-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="b515b-129">Le résultat généré **BackupKeyAsync** renvoie *BackupKeyResult* qui contient *Valeur* (objet blob de sauvegarde).</span><span class="sxs-lookup"><span data-stu-id="b515b-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="b515b-130">Auparavant, la méthode était encapsulée et ne renvoyait que la valeur.</span><span class="sxs-lookup"><span data-stu-id="b515b-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="b515b-131">Exceptions</span><span class="sxs-lookup"><span data-stu-id="b515b-131">Exceptions</span></span>

* <span data-ttu-id="b515b-132">*KeyVaultClientException* est remplacé par *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="b515b-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="b515b-133">L’erreur de service *exception.Error* est remplacée par *exception.Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="b515b-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="b515b-134">Les informations supplémentaires du message d’erreur pour **[JsonExtensionData]** ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="b515b-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="b515b-135">Constructeurs</span><span class="sxs-lookup"><span data-stu-id="b515b-135">Constructors</span></span>

* <span data-ttu-id="b515b-136">Au lieu d’accepter un *HttpClient* comme un argument de constructeur, le constructeur accepte seulement *HttpClientHandler* ou *DelegatingHandler[]*.</span><span class="sxs-lookup"><span data-stu-id="b515b-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="b515b-137">Packages téléchargés</span><span class="sxs-lookup"><span data-stu-id="b515b-137">Downloaded packages</span></span>

<span data-ttu-id="b515b-138">Lorsqu’un client traite une dépendance sur Key Vault, les éléments suivants sont téléchargés</span><span class="sxs-lookup"><span data-stu-id="b515b-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="b515b-139">Liste des packages précédents</span><span class="sxs-lookup"><span data-stu-id="b515b-139">Previous package list</span></span>

* <span data-ttu-id="b515b-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="b515b-148">Liste des packages actuels</span><span class="sxs-lookup"><span data-stu-id="b515b-148">Current package list</span></span>

* <span data-ttu-id="b515b-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="b515b-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="b515b-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="b515b-152">Modifications de classe</span><span class="sxs-lookup"><span data-stu-id="b515b-152">Class changes</span></span>

* <span data-ttu-id="b515b-153">La classe **UnixEpoch** a été supprimée</span><span class="sxs-lookup"><span data-stu-id="b515b-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="b515b-154">La classe **Base64UrlConverter** a été renommée **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="b515b-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="b515b-155">Autres modifications</span><span class="sxs-lookup"><span data-stu-id="b515b-155">Other changes</span></span>

* <span data-ttu-id="b515b-156">La prise en charge de la configuration de la stratégie de nouvelle tentative d’opération KV sur les défaillances passagères a été ajoutée à cette version de l’API.</span><span class="sxs-lookup"><span data-stu-id="b515b-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="b515b-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="b515b-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="b515b-158">Pour les opérations qui renvoyaient *vault*, le type de retour était une classe contenant une propriété Vault.</span><span class="sxs-lookup"><span data-stu-id="b515b-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="b515b-159">Le type de retour est maintenant *Vault*.</span><span class="sxs-lookup"><span data-stu-id="b515b-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="b515b-160">*PermissionsToKeys* et *PermissionsToSecrets* sont à présent *Permissions.Keys* et *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="b515b-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="b515b-161">Certaines modifications des types de retour s’appliquent également à control-plane.</span><span class="sxs-lookup"><span data-stu-id="b515b-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="b515b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="b515b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="b515b-163">Le package est interrompu jusqu’à **Microsoft.Azure.KeyVault.Extensions** et **Microsoft.Azure.KeyVault.Cryptography** pour les opérations de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="b515b-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

