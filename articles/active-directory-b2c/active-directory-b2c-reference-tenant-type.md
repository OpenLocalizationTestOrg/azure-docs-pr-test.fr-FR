---
title: "Azure Active Directory B2C : Disponibilité régionale et résidence des données | Microsoft Docs"
description: "Une rubrique sur les types de clients d’Azure Active Directory B2C hello"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C : Disponibilité régionale et résidence des données
Disponibilité de la région et la délégation de données sont deux concepts très différents qui s’appliquent différemment tooAzure AD B2C reste hello de Azure. Cet article expliquent hello les différences entre ces deux concepts et comparer la façon dont elles s’appliquent tooAzure et Azure Active Directory B2C.

## <a name="summary"></a>Résumé
Azure AD B2C est **généralement disponible dans le monde** avec l’option hello pour **délégation de données dans un État-Unis ou Europe**.

## <a name="concepts"></a>Concepts
* **Disponibilité de la région** fait référence toowhere un service est disponible pour utilisation.
* **Délégation de données** fait référence utilisateur toowhere les données sont stockées.

## <a name="region-availability"></a>Disponibilité des régions
Azure AD B2C est disponible dans le monde entier via hello cloud public Azure. 

Cela diffère de modèle de hello la plupart des autres suivent des services Azure risquent de disponibilité avec la délégation de données. Vous pouvez voir des exemples dans les deux Azure [produits disponibles par région](https://azure.microsoft.com/regions/services/) page et hello [calculatrice de prix Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Résidence des données
Azure Active Directory B2C conserve les données des utilisateurs aux États-Unis ou en Europe.

La résidence des données est déterminée selon le pays/la région sélectionné lors de la [création d’un client Azure Active Directory B2C](active-directory-b2c-get-started.md).

![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Données se trouvent aux États-Unis hello pour hello suivant pays/régions :

> États-Unis, Canada, Costa Rica, République dominicaine, Salvador, Guatemala, Mexique, Panama, Porto Rico et Trinité-et-Tobago

Données se trouvent en Europe pour hello suivant pays/régions :

> Algérie, Autriche, Azerbaïdjan, Bahreïn, Biélorussie, Belgique, Bulgarie, Croatie, Chypre, République tchèque, Danemark, Égypte, Estonie, Finlande, France, Allemagne, Grèce, Hongrie, Islande, Irlande, Israël, Italie, Jordanie, Kazakhstan, Kenya, Koweït, Lettonie, Liban, Liechtenstein, Lituanie, Luxembourg, Macédoine, Malte, Monténégro, Maroc, Pays-Bas, Nigeria, Norvège , Oman, Pakistan, Pologne, Portugal, Qatar, Roumanie, Russie, Arabie saoudite, Serbie, Slovaquie, Slovénie, Afrique du Sud, Espagne, Suède, Suisse, Tunisie, Turquie, Ukraine, Émirats Arabes Unis et Royaume-Uni.

Hello autres pays/régions sont dans le processus de hello de toohello liste ajoutée.  Pour l’instant, vous pouvez toujours utiliser Azure AD B2C en choisissant une des pays/régions de hello ci-dessus.

> Afghanistan, Argentine, Australie, Brésil, Chili, Colombie, Équateur, RAS de Hong Kong, Inde, Indonésie, Irak, Japon, Corée, Malaisie, Nouvelle-Zélande, Paraguay, Pérou, Philippines, Singapour, Sri Lanka, Taïwan, Thaïlande, Uruguay et Venezuela.

## <a name="preview-tenant"></a>Client de la version préliminaire
Si vous avez créé un client B2C pendant la période d’évaluation d’Azure AD B2C, il est probable que votre **type de client** indique **Client de la version préliminaire**. Si c’est le cas de hello, vous devez utiliser votre client uniquement pour le développement et à des fins de tests et pas pour les applications de production.

> [!IMPORTANT]
> Il n’existe aucun chemin d’accès de la migration à partir d’un client de B2C B2C locataire tooa production à l’échelle d’aperçu. Notez que des problèmes connus lorsque vous supprimez un client Aperçu B2C et recréer un B2C de production à l’échelle de locataire avec hello le même nom de domaine. Vous avez toocreate un locataire B2C de production à l’échelle avec un nom de domaine différent.


![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
