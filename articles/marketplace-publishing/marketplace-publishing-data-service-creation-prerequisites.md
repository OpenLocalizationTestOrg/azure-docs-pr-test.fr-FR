---
title: "aaaTechnical les composants requis pour la création d’un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comprendre les exigences de hello pour la création d’un toodeploy du Service de données et de vendre sur hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Conditions préalables techniques pour la création d’un Service de données proposent pour hello Azure Marketplace
> [!IMPORTANT]
> **À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.** Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners). Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Processus hello soigneusement avant le début de lire et comprendre où et pourquoi chaque étape est effectuée. Autant que possible, vous devez préparer les informations de votre société et d’autres données, téléchargez les outils nécessaires, ou créer des composants techniques avant de commencer le processus de création offre hello.

Vous devez avoir hello prêts avant de commencer le processus de hello des éléments suivants :

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Prendre une décision sur quelle technologie sera toopublish utilisé votre offre de Service de données
Un éditeur peut choisir entre plusieurs technologies lors de la publication du service de données dans Azure Marketplace. Hello principales technologies prises en charge décrites ci-dessous. Peu importe quelle technologie est utilisée toopublish hello Service de données, l’utilisateur final hello consomme des données de hello via hello **flux OData** exposées par le Service Azure Marketplace. Vous trouverez des informations détaillées sur le service OData à l’adresse [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>Base de données SQL Azure
Il incombe à l’éditeur de préparer le jeu de données dans SQL Azure. Vous devez toosubscribe tooAzure, configurer la taille appropriée de la base de données et télécharger vos données dans la base de données SQL Azure. Serveur de publication est également responsable tookeep ses données actualisées. Plus d’informations sur l’abonnement tooAzure Services que vous trouverez sur [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Lors du déplacement des données de salutation dans SQL Azure, hello Azure Marketplace peut exposer des tables et des vues. Hello Publisher peut spécifier les tables/vues et les colonnes sont l’utilisateur final toohello exposé. Fournisseur de contenu hello supplémentaire peut également spécifier les colonnes qui peuvent être interrogées par l’utilisateur final hello et celles qui est retournés uniquement dans la charge utile de hello. Ainsi, un niveau élevé de flexibilité sur les données dans la base de données hello doivent être exposées. Les colonnes qui peuvent être interrogées doivent toobe soutenu par un ou plusieurs index de base de données.

## <a name="rest-based-web-service"></a>Service web REST
Protocole pris en charge : **HTTPS uniquement**

Services basée sur REST existants peuvent être exposés via hello Azure Marketplace. Étant donné que hello jeu de données est toujours l’utilisateur final toohello exposé comme forme de flux OData, hello service Azure Marketplace doit toomap en mesure de toobe hello service tooa service OData basé. toodo donc tous les paramètres en tant que paramètres HTTP tooexpose pas besoin de points de terminaison hello basée sur REST.

charge utile de Hello doit toobe dans un formulaire qui peut être mappé dans une réponse ATOM. Par conséquent, réponse hello à partir des services de hello doit toobe au format XML et ne peut contenir un élément extensible qui contient des valeurs de charge utile hello (par exemple, le jeu d’enregistrements). Hello service Azure Marketplace mappera hello extensible nœud toohello entrée dans les valeurs de charge utile ATOM et hello dans les nœuds de propriété dans le nœud d’entrée hello.

Les informations d’autorisation (par exemple, API clés, l’authentification par jeton, etc.) doivent toobe fournie comme paramètre HTTP ou dans l’en-tête HTTP de hello (paire clé / valeur) : l’authentification de base est également pris en charge. Une clé valide doit toobe fournie et toutes les demandes via Azure Marketplace sont apportées via cette clé. Utilisateur d’analyse et de facturation s’effectue à la couche d’Azure Marketplace hello.

Erreurs retournées par le service de hello doivent toobe mappé à des codes d’état HTTP. En cas de service de hello retourne un fichier XML qui contient l’erreur de hello ces allez toobe mappé par les codes d’état tooHTTP service hello Azure Marketplace.

## <a name="soap-based-web-services"></a>Services web SOAP
Protocole : **HTTPS uniquement**

configuration requise de Hello est même hello comme dans la section de service basée sur REST hello. Hello seule différence est que les paramètres peuvent également être fournis dans un corps XML qui est en cours envoyés au service de l’éditeur toohello avec chaque demande effectuée via Azure Marketplace. Cela signifie qu’utilisateur hello de paramètres HTTP fournit à hello frontaux sont traduits dans les éléments XML d’un document XML qui est en cours de publication avec le service web de hello demande toohello du fournisseur de contenu.

## <a name="odata-based-web-services"></a>Services web OData
Protocole : **HTTPS uniquement**

Données peuvent être exposées comme un tooAzure du service OData Marketplace. système de Hello est continu toopass service hello via et remplace racine hello du service de hello racine du service Azure Marketplace hello – tooensure tous les appels Parcourir Azure Marketplace.

Les services OData seulement n’avez pas besoin toogo par rapport à une base de données back-end hello. OData prend en charge tout type de stockage ou business du service de hello logique toodrive.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous passé en revue les conditions préalables hello et effectué les tâches nécessaires hello, vous pouvez déplacer vers l’avant avec hello création de votre offre de Service de données en tant que hello détaillée dans [Guide de publication de Service de données](marketplace-publishing-data-service-creation.md).

Ou, si vous souhaitez que hello tooreview globale de processus et les articles respectifs hello pour chacun des hello phases de publication, consultez l’article de hello [mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
