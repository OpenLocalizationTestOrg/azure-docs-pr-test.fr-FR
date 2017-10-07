---
title: aaaCreate un service Azure Search dans le portail de hello | Documents Microsoft
description: Configurer un service Azure Search dans le portail de hello.
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Créer un service Azure Search dans le portail de hello

Cet article explique comment toocreate ou configurer un indexeur Azure Search service dans le portail de hello. Pour obtenir des instructions relatives à PowerShell, consultez [Gérer Recherche Azure avec PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>S’abonner (payant ou gratuit)

[Ouvrir un compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) et utiliser tootry crédits gratuits à payer des services Azure. Une fois que les crédits sont épuisés, conserver hello compte et continuer toouse Azure les services gratuits, comme les sites Web. Votre carte de crédit n’est jamais facturé, sauf si vous modifiez vos paramètres et demandez toobe facturé explicitement.

Vous pouvez également [activer les avantages d’abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Un abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants. 

## <a name="find-azure-search"></a>Localiser Recherche Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur hello plus signe (« + ») dans hello angle supérieur gauche.
3. Sélectionnez **Web + Mobile** > **Recherche Azure**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Service de nom hello et le point de terminaison URL

Un nom de service fait partie du point de terminaison d’URL hello par rapport à laquelle les appels d’API sont émis. Tapez le nom de votre service Bonjour **URL** champ. 

Configuration requise du nom du service :
   * entre 2 et 60 caractères ;
   * lettres minuscules, chiffres ou tirets (« - ») ;
   * aucun tiret («- ») comme hello les 2 premiers caractères ou le dernier caractère unique
   * pas de tirets consécutifs (« -- »).

## <a name="select-a-subscription"></a>Sélectionner un abonnement
Si vous avez plusieurs abonnements, choisissez celui qui a également des services de stockage de données ou de fichiers. Azure Search peut détecter automatiquement le stockage Table Azure et Blob, de la base de données SQL et Azure Cosmos DB pour l’indexation *indexeurs*, mais uniquement pour les services Bonjour même abonnement.

## <a name="select-a-resource-group"></a>Sélectionner un groupe de ressources
Un groupe de ressources correspond à une collection de services et de ressources Azure utilisés ensemble. Par exemple, si vous utilisez Azure Search tooindex une base de données SQL, les deux services doivent faire partie de hello même groupe de ressources.

> [!TIP]
> La suppression d’un groupe de ressources supprime également les services hello qu’il contient. Pour les projets de prototype utilisant plusieurs services, tous les placer dans hello même groupe de ressources facilite le nettoyage après la projet de hello. 

## <a name="select-a-hosting-location"></a>Sélectionner un emplacement d’hébergement 
Comme un service Azure, Azure Search peut être hébergé dans le monde hello des centres de données. Veuillez noter que les [prix peuvent varier](https://azure.microsoft.com/pricing/details/search/) selon la zone géographique.

## <a name="select-a-pricing-tier-sku"></a>Sélectionner un niveau de tarification (SKU)
[Azure Search est actuellement disponible à différents niveaux tarifaires](https://azure.microsoft.com/pricing/details/search/): Gratuit, De base ou Standard. Chaque niveau a ses propres [capacité et limites](search-limits-quotas-capacity.md). Pour obtenir de l’aide, voir [Choisir un niveau tarifaire ou une référence (SKU)](search-sku-tier.md) .

Dans cette procédure pas à pas, nous avons choisi le niveau Standard de hello pour notre service.

## <a name="create-your-service"></a>Créer votre service

N’oubliez pas toopin votre tableau de bord toohello service pour faciliter l’accès à chaque fois que vous vous connectez.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Mettre à l’échelle le service
Il peut prendre quelques minutes toocreate un service (15 minutes ou plus selon le niveau de hello). Après la configuration de votre service, vous pouvez mettre à l’échelle toomeet vos besoins. Étant donné que vous avez choisi de niveau Standard de hello pour votre service Azure Search, vous pouvez faire évoluer votre service en deux dimensions : les réplicas et les partitions. Vous aviez choisi le niveau de base hello, vous pouvez uniquement ajouter des réplicas. Si vous avez configuré le service gratuit de hello, l’échelle n’est pas disponible.

***Partitions*** autoriser votre service toostore et la recherche dans plusieurs documents.

***Réplicas*** autoriser votre toohandle service une charge supérieure des requêtes de recherche.

> [!Important]
> Un service doit avoir [2 réplicas pour SLA en lecture seule et 3 réplicas pour SLA en lecture/écriture](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Accédez à panneau de service de recherche tooyour Bonjour portail Azure.
2. Dans le volet de navigation de gauche hello, sélectionnez **paramètres** > **échelle**.
3. Utilisez hello votre tooadd réplicas ou les Partitions.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Chaque couche dispose de différents [limites](search-limits-quotas-capacity.md) sur le nombre total de hello d’unités de recherche autorisée dans un seul service (réplicas * Partitions = nombre Total d’unités recherche).

## <a name="when-tooadd-a-second-service"></a>Lorsque tooadd un deuxième service

Une grande majorité des clients utiliser qu’un seul service mis en service à un niveau qui fournit hello [avec le bouton droit équilibre des ressources](search-sku-tier.md). Un service peut héberger plusieurs index, objet toohello [limites maximales du niveau hello vous sélectionnez](search-capacity-planning.md), avec chaque index isolé d’une autre. Dans Azure Search, les demandes peuvent uniquement être dirigé tooone index, en réduisant le risque de hello accidentelle ou intentionnelle de récupération des données à partir d’autres index hello même service.

Bien que la plupart des clients utilisent qu’un seul service, une redondance de service peut être nécessaire si les spécifications opérationnelles de hello suivants :

+ Récupération d’urgence (panne du centre de données). Azure Search ne fournit pas un basculement instantané en cas de hello d’une panne. Pour obtenir de l’aide et des recommandations, consultez la page [Administration des services](search-manage.md).
+ Votre examen de la modélisation d’une architecture mutualisée a déterminé que des services supplémentaires est une conception optimale hello. Pour plus d’informations, consultez la page [Conception pour une architecture mutualisée](search-modeling-multitenant-saas-applications.md).
+ Pour les applications globalement déployées, vous pouvez avoir besoin d’une instance d’Azure Search de latence de toominimize plusieurs régions de trafic international de votre application.

> [!NOTE]
> Dans la Recherche Azure, vous ne pouvez pas séparer les charges de travail d’indexation et de requête ; par conséquent, il n’est jamais question de créer plusieurs services pour des charges de travail séparées. Un index est toujours interrogé sur service de hello dans lequel il a été créé (vous ne peut pas créer un index dans un seul service et copiez-le tooanother).
>

Il n’est pas nécessaire de disposer d’un second service pour la haute disponibilité. Haute disponibilité pour les requêtes est obtenue lorsque vous utilisez 2 ou plusieurs réplicas dans hello même service. Les mises à jour des réplicas sont séquentielles, ce qui signifie qu’au moins l’un d’eux est opérationnel lors du déploiement d’une mise à jour de service. Pour plus d’informations sur la disponibilité, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Étapes suivantes
Après le déploiement d’un service Azure Search, vous êtes prêt trop[définir un index](search-what-is-an-index.md) afin de pouvoir télécharger et rechercher vos données.

service de hello tooaccess à partir de code ou un script, indiquez les URL de hello (*-nom du service*. search.windows.net) et une clé. Les clés d’administration accordent un accès total ; les clés de requête accordent un accès en lecture seule. Consultez [comment effectuer une recherche toouse Azure dans .NET](search-howto-dotnet-sdk.md) tooget a démarré.

Consultez [Créer et interroger votre premier index](search-get-started-portal.md) pour obtenir un didacticiel rapide sur le portail.

