---
title: "fonctionnalités aaaSecurity qui peuvent être utilisées avec le stockage Azure | Documents Microsoft"
description: " Cet article fournit une vue d’ensemble de fonctionnalités de sécurité Azure hello principales qui peut être utilisé avec le stockage Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Vue d’ensemble des fonctionnalités de sécurité d’Azure Storage
Stockage Azure est la solution de stockage cloud hello pour les applications modernes qui s’appuient sur la durabilité, disponibilité et évolutivité toomeet hello aux besoins de leurs clients. Azure Storage fournit un ensemble complet de fonctionnalités de sécurité :

* compte de stockage Hello peut être sécurisé à l’aide du contrôle d’accès en fonction du rôle et Azure Active Directory.
* Les données peuvent être sécurisées en transit entre une application et Azure au moyen du chiffrement côté client, de HTTPS ou de SMB 3.0.
* Donnée peut être définie toobe automatiquement chiffré lors de l’écriture tooAzure stockage à l’aide du chiffrement de Service de stockage.
* Les disques du système d’exploitation et les données utilisées par les ordinateurs virtuels peuvent être définies toobe chiffré à l’aide du chiffrement de disque Azure.
* Accès délégué toohello les objets de données dans le stockage Azure peuvent être accordées à l’aide de Signatures d’accès partagé.
* méthode d’authentification Hello utilisé par un utilisateur lors de l’accès au stockage peut être suivi à l’aide d’analytique de stockage.

Pour obtenir une présentation plus détaillée à la sécurité dans le stockage Azure, consultez hello [guide de sécurité de stockage Azure](../storage/common/storage-security-guide.md). Ce guide fournit une présentation approfondie dans les fonctionnalités de sécurité hello du stockage Azure telles que des clés de compte de stockage, de chiffrement des données en transit et au repos et analytique de stockage.

Cet article fournit une vue d’ensemble des fonctionnalités de sécurité Azure pouvant être utilisées avec le Stockage Azure. Des liens sont fournis tooarticles qui fournissent des détails de chaque fonctionnalité afin d’en savoir plus.

Voici hello principales fonctionnalités toobe abordée dans cet article :

* Contrôle d’accès en fonction du rôle
* Accès délégué toostorage objets
* Chiffrement en transit
* Chiffrement au repos et chiffrement Service Storage
* Azure Disk Encryption
* Azure Key Vault

## <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle
Vous pouvez sécuriser un compte de stockage en utilisant le contrôle d’accès en fonction du rôle (RBAC). Restreindre l’accès basé sur hello [devez tooknow](https://en.wikipedia.org/wiki/Need_to_know) et [moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principes de sécurité est impérative pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données. Ces droits d’accès sont accordées en attribuant hello toogroups du rôle RBAC approprié et les applications à une certaine étendue. Vous pouvez utiliser [rôles RBAC intégrés](../active-directory/role-based-access-built-in-roles.md), telles que contributeur du compte de stockage, tooassign privilèges toousers.

En savoir plus :

* [Contrôle d’accès en fonction du rôle Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Accès délégué toostorage objets
Une signature d’accès partagé (SAS) fournit tooresources accès délégué dans votre compte de stockage. Hello SAS signifie que vous pouvez accorder à qu'un client limitée tooobjects autorisations dans votre compte de stockage pour une période de temps et avec un jeu d’autorisations spécifié. Vous pouvez accorder ces autorisations limitées sans avoir tooshare vos clés d’accès de compte. Hello SAS est un URI qui englobe dans ses paramètres de requête, toutes les informations de hello nécessaires pour la ressource de stockage tooa un accès authentifié. ressources de stockage tooaccess par hello SAS, hello client a seulement besoin tooprovide hello SAS toohello approprié constructeur ou une méthode.

En savoir plus :

* [Modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Créer et utiliser une signature d’accès partagé avec Blob Storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Chiffrement en transit
Le chiffrement en transit est un mécanisme de protection des données transmises sur des réseaux. Azure Storage vous permet de sécuriser les données à l’aide de diverses fonctionnalités :

* Le [chiffrement au niveau du transport](../storage/common/storage-security-guide.md#encryption-in-transit) (HTTPS, par exemple) lorsque vous transférez des données vers ou à partir d’Azure Storage.
* Le [chiffrement câblé](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), par exemple le chiffrement SMB 3.0 pour les partages de fichiers Azure.
* [Le chiffrement côté client](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), les données de salutation tooencrypt avant leur transfert dans les données de stockage et toodecrypt salutation après leur transfert hors stockage.

En savoir plus sur le chiffrement côté client :

* [Client-Side Encryption for Microsoft Azure Storage (Chiffrement côté client pour Microsoft Azure Storage)](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud security controls series: Encrypting Data in Transit (Série consacrée aux contrôles de sécurité dans le cloud : chiffrement des données en transit)](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Chiffrement au repos
Pour de nombreuses organisations, le [chiffrement des données au repos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) est une étape obligatoire du processus de gestion de la confidentialité, de la conformité et de la souveraineté des données. Trois fonctionnalités Azure fournissent un chiffrement des données « au repos ».

* [Chiffrement du Service Storage](../storage/common/storage-security-guide.md#encryption-at-rest) vous permet de toorequest que service de stockage hello chiffrer automatiquement des données lors de l’écriture de tooAzure stockage.
* [Le chiffrement côté client](../storage/common/storage-security-guide.md#client-side-encryption) fournit également la fonctionnalité hello du chiffrement au repos.
* [Le chiffrement des disques Azure](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) vous permet des disques tooencrypt hello du système d’exploitation et des disques de données utilisées par une machine virtuelle IaaS.

En savoir plus sur Storage Service Encryption :

* Le [chiffrement du service de stockage Azure](https://azure.microsoft.com/services/storage/) est disponible pour le [Stockage Blob Azure](https://azure.microsoft.com/services/storage/blobs/). Pour plus d’informations sur les autres types de stockage Azure, consultez [File](https://azure.microsoft.com/services/storage/files/), [Disk (Premium Storage)](https://azure.microsoft.com/services/storage/premium-storage/), [Table](https://azure.microsoft.com/services/storage/tables/) et [Queue](https://azure.microsoft.com/services/storage/queues/).
* [Azure Storage Service Encryption pour les données au repos](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Encryption
Azure Disk Encryption pour les machines virtuelles vous permet de répondre aux exigences de conformité et de sécurité des organisations en chiffrant vos disques de machine virtuelle (y compris les disques d’amorçage et disques de données) avec des clés et stratégies que vous pouvez contrôler dans [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Azure Disk Encryption pour les machines virtuelles est compatible avec les systèmes d’exploitation Linux et Windows. Il utilise également le coffre de clés toohelp vous protégez, gérez et auditer l’utilisation de vos clés de chiffrement de disque. Toutes les données hello dans vos disques de machine virtuelle sont chiffrées au repos à l’aide de la technologie de chiffrement standard dans vos comptes de stockage Azure. Hello des solutions de chiffrement de disque pour Windows est basée sur [le chiffrement de lecteur BitLocker Microsoft](https://technet.microsoft.com/library/cc732774.aspx), et hello solution Linux est basée sur [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

En savoir plus :

* [Azure Disk Encryption pour des machines virtuelles IaaS Windows et Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>coffre de clés Azure
Le chiffrement des disques Azure utilise [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp vous contrôler et gérer des clés de chiffrement de disque et des clés secrètes dans votre abonnement de coffre de clés, tout en garantissant que toutes les données de disques de machine virtuelle hello sont chiffrées au repos dans votre Azure Stockage. Vous devez utiliser des clés de tooaudit de coffre de clés et l’utilisation de la stratégie.

En savoir plus :

* [Qu’est-ce qu’Azure Key Vault ?](../key-vault/key-vault-whatis.md)
* [Prise en main du coffre de clés Azure](../key-vault/key-vault-get-started.md)
