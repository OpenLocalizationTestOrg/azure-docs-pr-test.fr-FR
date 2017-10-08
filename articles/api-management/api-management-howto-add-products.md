---
title: aaaHow toocreate et publier un produit de gestion des API Azure
description: "Découvrez comment toocreate et publier des produits dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Comment toocreate et publier un produit de gestion des API Azure
Dans Gestion des API Azure, un produit contient une ou plusieurs API ainsi que les conditions hello et de quota d’utilisation d’utilisation. Une fois qu’un produit est publié, les développeurs peuvent s’abonner toohello produit et commencer l’API du produit toouse hello. rubrique de Hello fournit un guide toocreating un produit, l’ajout d’une API et sa publication pour les développeurs.

## <a name="create-product"></a>Création d’un produit
Les opérations sont ajoutées et configurés tooan API dans le portail de publication hello. tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Cliquez sur **produits** dans menu hello Bonjour toodisplay gauche Bonjour **produits** page, puis cliquez sur **ajouter un produit**.

![Produits][api-management-products]

![New product][api-management-add-new-product]

Entrez un nom descriptif pour le produit de hello Bonjour **nom** champ et une description du produit de hello en hello **Description** champ.

Les produits de Gestion des API peuvent être **Ouverts** ou **Protégés**. Produits protégés doivent être souscrit toobefore ils peuvent être utilisés pendant l’ouverture produits peuvent être utilisés sans abonnement. Vérifiez **abonnement** toocreate un produit protégé qui nécessite un abonnement. Il s’agit de paramètre par défaut de hello.

Vérifiez **exiger l’approbation de l’abonnement** si vous souhaitez un tooreview administrateur et l’accepter ou rejeter abonnement tente toothis produit. Si hello est désactivée, les tentatives d’abonnement sera approuvée automatiquement. Pour plus d’informations sur les abonnements, consultez [afficher le produit abonnés tooa][View subscribers tooa product].

tooallow développeur comptes toosubscribe produit de toohello plusieurs fois, vérifiez hello **autoriser plusieurs abonnements** case à cocher. Si cette case n’est pas activée, chaque compte de développeur peut s’abonner à un produit toohello seule fois uniquement.

![Abonnements multiples illimités][api-management-unlimited-multiple-subscriptions]

nombre de hello toolimit de plusieurs abonnements simultanés, vérifiez hello **limiter le nombre d’abonnements simultanés à** case à cocher et entrez la limite d’abonnement hello. Dans l’exemple suivant de hello, abonnements simultanés sont toofour limitée par le compte de développeur.

![Quatre abonnements multiples][api-management-four-multiple-subscriptions]

Une fois que toutes les nouvelles options de produit sont configurées, cliquez sur **enregistrer** produit toocreate hello.

![Produits][api-management-products-page]

> Par défaut les nouveaux produits non publiés et sont visible toohello uniquement **administrateurs** groupe.
> 
> 

tooconfigure un produit, cliquez sur le nom du produit hello Bonjour **produits** onglet.

## <a name="add-apis"></a>Produit de tooa ajouter des API
Hello **produits** page contient quatre des liens pour la configuration : **Résumé**, **paramètres**, **visibilité**, et  **Les abonnés**. Hello **Résumé** onglet est où vous pouvez ajouter les API et publier ou annuler la publication d’un produit.

![Résumé][api-management-new-product-summary]

Avant de publier votre produit vous devez tooadd une ou plusieurs API. toodo, cliquez sur **tooproduct d’ajouter les API**.

![Add APIs][api-management-add-apis-to-product]

Sélectionnez hello souhaité API et cliquez sur **enregistrer**.

## <a name="add-description"></a>Produit de tooa ajouter des informations descriptives
Hello **paramètres** onglet vous permet de tooprovide des informations détaillées sur le produit hello comme son objectif, hello donne accès à des API et autres informations utiles. contenu de Hello est destiné aux développeurs de hello en appelant l’API de hello et peuvent être écrits en texte brut ou un balisage HTML.

![Product settings][api-management-product-settings]

Vérifiez **abonnement** toocreate un produit protégé qui nécessite une toobe d’abonnement utilisé, ou désactivez hello case à cocher toocreate un produit en cours qui peut être appelé sans un abonnement.

Sélectionnez **exiger l’approbation de l’abonnement** si vous souhaitez toomanually approuver toutes les demandes d’abonnement de produit. Par défaut, tous les abonnements sont acceptés automatiquement.

tooallow développeur comptes toosubscribe produit de toohello plusieurs fois, vérifiez hello **autoriser plusieurs abonnements** case à cocher et si vous le souhaitez spécifier une limite. Si cette case n’est pas activée, chaque compte de développeur peut s’abonner à un produit toohello seule fois uniquement.

Si vous le souhaitez renseignez hello **conditions d’utilisation** champ décrivant les conditions d’utilisation de hello pour le produit hello que les abonnés doivent accepter dans le produit de commande toouse hello.

## <a name="publish-product"></a>Publication d’un produit
Avant de hello API dans un produit peut être appelée, produit de hello doit être publié. Sur hello **Résumé** pour le produit de hello, cliquez sur **publier**, puis cliquez sur **Oui, publiez-le** tooconfirm. toomake privé produit précédemment publiée, cliquez sur **annuler la publication**.

![Publish product][api-management-publish-product]

## <a name="make-visible"></a>Rendre un toodevelopers visible du produit
Hello **visibilité** onglet vous permet de toochoose les rôles sont le produit de hello en mesure de toosee sur le portail des développeurs hello et s’abonner toohello produit.

![Product visibility][api-management-product-visiblity]

visibilité tooenable ou désactivation d’un produit pour les développeurs de hello dans un groupe, ou désactivez la case à cocher en regard du groupe de hello hello, puis cliquez sur **enregistrer**.

> Pour plus d’informations, consultez [mode développeur de toomanage groupes toocreate et l’utilisation de comptes dans Gestion des API Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Afficher le produit tooa abonnés
Hello **abonnés** onglet répertorie les développeurs hello qui se sont abonnés toohello produit. Hello détails et les paramètres pour chaque développeur peuvent être affichés en cliquant sur le nom du développeur hello. Dans cet exemple sans les développeurs ont encore abonnés toohello produit.

![Développeurs][api-management-developer-list]

## <a name="next-steps"></a>Étapes suivantes
Une fois hello souhaité API ont été ajoutées et hello produit publié, les développeurs peuvent s’abonner toohello produit et commencer toocall hello API. Pour suivre le didacticiel présentant comment configurer ces éléments, ainsi que certains paramètres de produit avancés, consultez la page [Création et configuration de paramètres de produit avancés dans Gestion des API Azure][How create and configure advanced product settings in Azure API Management].

Pour plus d’informations sur l’utilisation des produits, consultez hello suivant vidéo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
