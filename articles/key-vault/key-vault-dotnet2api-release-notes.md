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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>Azure Key Vault .NET 2.0 - Notes de publication et guide de migration
Hello des remarques et conseils suivants sont destinés aux développeurs qui travaillent avec Azure Key Vault .NET / bibliothèque de c#. Dans la transition hello à partir d’une version toohello 2.0 hello 1.0, un nombre de mises à jour ont été apportée seront nécessiter du travail de migration dans votre code afin que vous toobenefit les améliorations fonctionnelles hello et ajouts de fonctionnalités telles que **le coffre de clés certificats** prend en charge.

## <a name="key-vault-certificates"></a>Certificats Key Vault

Prise en charge des certificats de coffre de clés offre pour la gestion de votre x509 certificats et hello suit les comportements :  

* Permet un toocreate du propriétaire du certificat à un certificat via un processus de création du coffre de clés ou importation hello d’un certificat existant. Cela concerne à la fois les certificats auto-signés et ceux générés par une autorité de certification.
* Permet à un propriétaire de certificat du coffre de clés tooimplement le stockage sécurisé et gestion de X509 certificats sans interaction avec la clé privée.  
* Permet un toocreate du propriétaire du certificat à une stratégie qui dirige le coffre de clés toomanage hello cycle de vie d’un certificat.  
* Permet les propriétaires de certificat tooprovide informations de contact pour la notification des événements de cycle de vie d’expiration et le renouvellement de certificat.  
* Prend en charge le renouvellement automatique avec des émetteurs sélectionnés : fournisseurs de certificats X509 de partenaire Key Vault/autorités de certification.
  
  * Remarque : fournisseurs/autorités Non associés sont également autorisées, mais le ne prendra pas en charge la fonctionnalité de renouvellement automatique hello.

## <a name="net-support"></a>Prise en charge de .NET

* **.NET 4.0** n’est pas pris en charge par version de hello 2.0 de hello Azure Key Vault .NET / bibliothèque c#
* **.NET core** est pris en charge par la version 2.0 de hello Hello .NET d’Azure Key Vault / bibliothèque c#

## <a name="namespaces"></a>Espaces de noms

* Hello d’espace de noms pour **modèles** est remplacée par **Microsoft.Azure.KeyVault** trop**Microsoft.Azure.KeyVault.Models**.
* Hello **Microsoft.Azure.KeyVault.Internal** espace de noms est supprimé.
* espace de noms Hello Azure SDK dépendances sont modifiés à partir de **Hyak.Common** et **Hyak.Common.Internals** trop**Microsoft.Rest** et  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Modifications des types

* *Secret* modifié trop*SecretBundle*
* *Dictionnaire* modifié trop*IDictionary*
* *Liste<T>, string []* modifié trop*IList<T>*
* *NextList* modifié trop *NextPageLink*

## <a name="return-types"></a>Types de retour

* **KeyList** et **SecretList** renvoient *IPage<T>* au lieu de *ListKeysResponseMessage*
* Hello généré **BackupKeyAsync** retournera *BackupKeyResult* qui contient *valeur* (objet blob de sauvegarde). Avant de hello méthode a été encapsulée et le retour seule valeur hello.

## <a name="exceptions"></a>Exceptions

* *KeyVaultClientException* est modifié trop*KeyVaultErrorException*
* Erreur du service Hello est modifié de *exception. Erreur* trop*exception. Body.Error.Message*.
* Supprimer des informations supplémentaires à partir du message d’erreur hello pour **[JsonExtensionData]**.

## <a name="constructors"></a>Constructeurs

* Au lieu d’accepter un *HttpClient* comme argument de constructeur, constructeur de hello accepte uniquement *HttpClientHandler* ou *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Packages téléchargés

Lorsqu’un client traite une dépendance sur suit hello de coffre de clés ont été téléchargés.

### <a name="previous-package-list"></a>Liste des packages précédents

* package id="Hyak.Common" version="1.0.2" targetFramework="net45"
* package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"
* package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"
* package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"
* package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"
* package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>Liste des packages actuels

* package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"
* package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>Modifications de classe

* La classe **UnixEpoch** a été supprimée
* **Base64UrlConverter** classe a été renommée trop**Base64UrlJsonConverter**

## <a name="other-changes"></a>Autres modifications

* Version toothis de hello API a été ajoutée à la prise en charge pour la configuration de hello de stratégie de nouvelle tentative d’opération KV sur les erreurs temporaires.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Pour les opérations de hello retournent un *coffre*, type de retour de hello est une classe contenant une propriété de coffre. Hello type de retour est désormais *coffre*.
* *PermissionsToKeys* et *PermissionsToSecrets* sont à présent *Permissions.Keys* et *Permissions.Secrets*
* Certaines hello retourner les modifications de types s’appliquent toohello panneau ainsi.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* package de Hello est alors divisé trop**Microsoft.Azure.KeyVault.Extensions** et **Microsoft.Azure.KeyVault.Cryptography** pour les opérations de chiffrement hello.

