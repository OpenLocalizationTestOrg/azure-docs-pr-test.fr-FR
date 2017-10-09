---
title: "concepts de vue d’ensemble et la clé de la gestion des API aaaAzure | Documents Microsoft"
description: Learn about APIs, products, roles, groups, and other API Management key concepts.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>Présentation de Gestion des API
Gestion des API permet aux organisations de publier des API tooexternal, les partenaires et les développeurs internes toounlock hello potentiel leurs données et services. Les entreprises partout sont recherche tooextend leurs opérations comme plateforme numérique, création de nouveaux canaux, recherche de nouveaux clients et en avec existants. Gestion des API fournit hello principales compétences tooensure un programme API réussi via l’intérêt du développeur, perspectives professionnelles, analytique, la sécurité et protection.

Regardez hello suivant vidéo pour une vue d’ensemble de la gestion des API Azure et apprenez comment toouse gestion des API tooadd nombreuses fonctionnalités tooyour API, y compris le contrôle d’accès, du taux de limitation, la surveillance, la journalisation des événements et réponse mise en cache, avec un minimum de travail.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse gestion des API, les administrateurs créent des API. Chaque API se compose d’une ou plusieurs opérations, et chaque API peut être ajouté tooone ou plusieurs produits. toouse une API, les développeurs s’abonnent tooa produit qui contient cette API, et ils peuvent alors appeler opération hello d’API, des stratégies d’utilisation sujet tooany qui peut être en vigueur.

Cette rubrique offre une présentation des principaux concepts associés à Gestion des API.

> [!NOTE]
> Pour plus d’informations, consultez hello [gestion des API en nuage : maîtriser hello Power d’API](http://j.mp/ms-apim-whitepaper) livre blanc PDF. Ce livre blanc d’introduction à la gestion des API, publié par CITO Research, présente les opérations suivantes : 
> 
> * Configuration requise des API et défis communs
> * Découplage des API et présentation des façades
> * Motivation des développeurs et exécution rapide
> * Sécurisation de l'accès
> * Analyse et mesures
> * Prise de contrôle et aperçu d’une plate-forme de gestion des API
> * Utilisation du cloud par rapport aux solutions locales
> * Gestion des API Azure
> 
> 

## <a name="apis"></a>API et opérations
API sont foundation hello d’une instance de service de gestion des API. Chaque API représente un ensemble d’opérations des toodevelopers disponibles. Chaque API contenait un service principal de toohello référence qui implémente l’API de hello et ses opérations d’opérations toohello implémentées par le service principal de hello de mappage. Les opérations dans Gestion des API sont hautement configurables. Elles contrôlent le mappage d'URL, les paramètres de requête et de chemin d'accès, le contenu de la demande et de la réponse, et la mise en cache de la réponse de l'opération. Limite de taux, les quotas et les stratégies de restriction IP peuvent également être implémentées au niveau de l’opération individuelle ou de hello API.

Pour plus d’informations, consultez [comment toocreate API] [ How toocreate APIs] et [comment tooadd opérations tooan API][How tooadd operations tooan API].

## <a name="products"></a> Produits
Les produits sont comment API sont toodevelopers chaque bande. Les produits dans Gestion des API possèdent une ou plusieurs API et sont configurés avec un titre, une description et des conditions d'utilisation. Les produits peuvent être **ouverts** ou **protégés**. Produits protégés doivent être souscrit toobefore ils peuvent être utilisés pendant l’ouverture produits peuvent être utilisés sans abonnement. Lorsqu'un produit est prêt à l'emploi pour les développeurs, il peut être publié. Une fois qu’elle est publiée, elle peut être affichée (et Bonjour cas des produits protégés abonnée à) par les développeurs. Approbation de l’abonnement est configurée au niveau du produit hello et peut exiger l’approbation administrateur ou être approuvée automatiquement.

Les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits. Produits accorder toogroups de visibilité, et les développeurs peuvent afficher et s’abonner toohello les produits qui sont des groupes toohello visible dans laquelle ils appartiennent. 

Pour plus d’informations, consultez [comment toocreate et publier un produit] [ How toocreate and publish a product] et hello suite vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"></a> Groupes
Les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits. Gestion des API a hello suivant groupes système immuables.

* **Administrateurs** : les administrateurs d’abonnements Azure sont membres de ce groupe. Administrateurs de gérer des instances de service de gestion des API, création hello API, opérations et produits qui sont utilisés par les développeurs.
* **Développeurs** : les utilisateurs authentifiés du portail des développeurs appartiennent à ce groupe. Les développeurs sont des clients hello générer des applications à l’aide de votre API. Les développeurs sont accordées portail des développeurs accès toohello et générer des applications qui appellent des opérations d’une API hello.
* **Invités** -non authentifié utilisateurs du portail développeur, tels que les clients potentiels en visitant le portail des développeurs hello d’une baisse d’instance gestion des API dans ce groupe. Ils peuvent bénéficier de certain accès en lecture seule, par exemple, hello capacité tooview API mais pas de les appellent.

Dans les groupes de système toothese plus, les administrateurs peuvent créer des groupes personnalisés ou [tirer parti des groupes externes dans les clients Azure Active Directory associés](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Groupes personnalisés et externes peuvent être utilisés avec des groupes de systèmes en offrant aux développeurs une visibilité et accéder aux produits de tooAPI. Par exemple, vous pouvez créer un groupe personnalisé pour les développeurs affiliés à spécifiques à une organisation partenaire et les autoriser à accéder toohello API à partir d’un produit contenant uniquement des API pertinentes. Un utilisateur peut être membre de plusieurs groupes.

Pour plus d’informations, consultez [comment toocreate et l’utilisation de groupes][How toocreate and use groups].

## <a name="developers"></a> Développeurs
Les développeurs représentent les comptes d’utilisateur hello dans une instance de service de gestion des API. Les développeurs peuvent être créés ou invité toojoin par les administrateurs, ou ils peuvent inscrire hello [portail des développeurs][Developer portal]. Chaque développeur est un membre d’un ou plusieurs groupes et peut être s’abonner toohello produits qui accordent des groupes de toothose de visibilité.

Lorsque les développeurs s’abonnent tooa produit qu’ils bénéficient de clé primaire et secondaire de hello pour le produit de hello. Cette clé est utilisée lors d’appels dans les API du produit hello.

Pour plus d’informations, consultez [comment les développeurs toocreate ou invitation] [ How toocreate or invite developers] et [comment les groupes avec les développeurs tooassociate][How tooassociate groups with developers].

## <a name="policies"></a> Stratégies
Les stratégies sont une fonctionnalité puissante de gestion des API qui permettent d’éditeur de hello toochange hello du comportement de hello API via la configuration. Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API. Les instructions populaires incluent une conversion de format à partir de XML tooJSON et appel de limitation du débit montant de hello toorestrict d’appels entrants à partir d’un développeur, et de nombreuses autres stratégies sont disponibles.

Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello. Certaines stratégies telles que hello [flux de contrôle](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) et [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) stratégies basées sur des expressions de stratégie. Pour plus d’informations, consultez [stratégies avancées](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx), et en les hello espion suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Pour obtenir la liste complète des stratégies Gestion des API, consultez la page [Référence de stratégie][Policy reference]. Pour plus d’informations sur l’utilisation et la configuration des stratégies, consultez la page [Stratégies Gestion des API][API Management policies]. Pour consulter un didacticiel sur la création d’un produit avec des stratégies de limite de débit et de quota, référez-vous à la page [Création et configuration de paramètres de produit avancés][How create and configure advanced product settings]. Pour une démonstration, consultez hello suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"></a> Portail des développeurs
portail des développeurs Hello est où les développeurs peuvent obtenir des informations sur votre API, d’une vue et d’appeler des opérations et s’abonner tooproducts. Clients potentiels peuvent visiter le portail des développeurs hello, afficher des API et des opérations et de l’inscription. URL de Hello pour votre portail des développeurs se trouve sur le tableau de bord hello Bonjour portail classique Azure pour votre instance de service de gestion des API.

Vous pouvez personnaliser hello apparence de votre portail des développeurs par l’ajout de contenu personnalisé, la personnalisation des styles et l’ajout de votre marque.

## <a name="api-management-and-hello-api-economy"></a>Gestion des API et hello économie d’API
toolearn plus sur la gestion des API, hello espion suivant présentation conférence hello Microsoft Ignite 2015.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




