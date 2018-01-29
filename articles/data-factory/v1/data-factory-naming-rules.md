---
title: "Règles d’affectation des noms des entités Azure Data Factory | Microsoft Docs"
description: "Décrit les règles d'affectation de noms pour les entités Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: a6bb9cc567ac9c9658c18bc20e11a6349ec7b930
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - Règles d’affectation des noms
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). Si vous utilisez la version 2 du service Data Factory, qui est en préversion, consultez [Azure Data Factory - Règles d’affectation des noms](../naming-rules.md).

Le tableau suivant fournit des règles d'affectation de noms pour les artefacts Data Factory.

| NOM | Unicité du nom | Contrôles de validation |
|:--- |:--- |:--- |
| Data Factory |Unique sur Microsoft Azure. Les noms ne respectent pas la casse, c’est-à-dire que `MyDF` et `mydf` font référence à la même fabrique de données. |<ul><li>Chaque fabrique de données est liée à un seul abonnement Azure.</li><li>Les noms d’objet doivent commencer par une lettre ou un chiffre, et peuvent comporter uniquement des lettres, des chiffres et des tirets (-).</li><li>Chaque tiret (-) doit être immédiatement précédé et suivi par une lettre ou un chiffre. Les tirets consécutifs ne sont pas autorisés dans les noms de conteneurs.</li><li>Le nom doit contenir entre 3 et 63 caractères.</li></ul> |
| Services/tableaux/pipelines liés |Unique dans une fabrique de données. Les noms sont sensibles à la casse. |<ul><li>Un tableau peut contenir un maximum de 260 caractères.</li><li>Les noms d’objet doivent commencer par une lettre, un chiffre ou un trait de soulignement (_).</li><li>Les caractères suivants ne sont pas autorisés : « . », « + », « ? », « / », « < », « > », « * », « % », « & », « : », « \\ »</li></ul> |
| Groupe de ressources |Unique sur Microsoft Azure. Les noms sont sensibles à la casse. |<ul><li>Nombre maximal de caractères : 1 000.</li><li>Un nom peut contenir des lettres, des chiffres et les caractères suivants : « - », « _ », « , » et « . ».</li></ul> |

