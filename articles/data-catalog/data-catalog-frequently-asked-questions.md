---
title: aaaAzure Data Catalog, Forum aux questions | Documents Microsoft
description: "Forum Aux Questions sur Azure Data Catalog, y compris sur les fonctionnalités de détection de source de données, d’annotation et de gestion."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Forum Aux Questions Azure Data Catalog
Cet article fournit elles sonttrop des réponses demandé toohello Azure Data Catalog service liées à des questions.

## <a name="what-is-azure-data-catalog"></a>Qu’est-ce qu’Azure Data Catalog ?
Data Catalog est un service entièrement géré, hébergé par Microsoft Azure, qui sert de système d’inscription et de détection des sources de données d’entreprise. Avec le catalogue de données, tous les utilisateurs, les chercheurs de toodata analystes et développeurs peuvent inscrire, découvrir, comprendre et consommer des sources de données.

## <a name="what-customer-challenges-does-it-solve"></a>Quels sont les défis clients que ce service permet de résoudre ?
Adresses des données de catalogue hello défis de découverte de la source de données et de « données sombres » afin que les utilisateurs peuvent découvrir et comprendre les sources de données d’entreprise.

## <a name="what-are-its-target-audiences"></a>Quel est le public cible ?
Data Catalog est conçu pour les utilisateurs, techniciens ou non, notamment :

* Les développeurs de données et les professionnels BI et analytique : personnes chargées de production analytique et données de contenu pour les autres tooconsume.
* Gestionnaires de données : personnes qui ont des connaissances hello sur hello données, ce que cela signifie et comment il est prévu toobe utilisé.
* Les consommateurs de données : personnes qui doivent toobe les tooeasily en mesure de découvrir, comprendre et connecter les données toohello nécessaires toodo leur travail, à l’aide de l’outil hello de leur choix.
* Centrale informatique : personnes qui ont besoin de toomake des centaines de sources de données pouvant être découvert par les utilisateurs professionnels, et qui ont besoin de supervision de toomaintain sur l’utilisation de données et par qui.

## <a name="what-is-its-availability-by-region"></a>Quelle est la disponibilité du service par région ?
Les services de catalogue de données sont actuellement disponibles dans hello suivant des centres de données :

* Ouest des États-Unis
* Est des États-Unis
* Europe de l'Ouest
* Europe du Nord
* Est de l’Australie
* Asie du Sud-Est

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Quelles sont ses limites de nombre hello de ressources de données ?
Bonjour données catalogue gratuit est too5 limitée, les ressources de données inscrits 000.

Hello prend en charge l’Édition Standard de catalogue de données des too100, 000 inscrit des ressources de données.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Quels sont les types de sources et de ressources de données pris en charge ?
Pour obtenir la liste des sources de données actuellement prises en charge, reportez-vous au [DSR Data Catalog](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>Comment demander la prise en charge d’une autre source de données ?
toosubmit demandes de fonctionnalités et vos commentaires, accédez toohello [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Comment démarrer avec Data Catalog ?
Hello la meilleure façon tooget démarré est en accédant trop[prise en main de catalogue de données](data-catalog-get-started.md). Cet article est une vue d’ensemble de bout en bout des capacités hello dans le service hello.

## <a name="how-do-i-register-my-data"></a>Comment inscrire mes données ?
tooregister vos données dans le catalogue de données :
1. Dans le portail Azure Data Catalog hello, Bonjour **publier** zone, l’outil d’inscription de début hello Azure Data Catalog. 
2. Bonjour catalogue de données de publication d’application, connectez-vous à hello même informations d’identification que vous utilisez tooaccess hello portail Data Catalog.
3. Sélectionnez la source de données hello et les actifs spécifiques hello que vous souhaitez tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>Quelles propriétés sont extraites pour les ressources de données qui sont inscrites ?
propriétés spécifiques de Hello diffèrent de la source de données source toodata mais, en général, hello service de publication de catalogue de données extrait hello informations suivantes :

* Nom de la ressource
* Type de ressource
* Description de la ressource
* Noms de l’attribut/de la colonne
* Types de données de l'attribut/de la colonne
* Description de l’attribut/de la colonne

> [!IMPORTANT]
> L’inscription des ressources de données avec les données de catalogue ne pas déplacer ou copier vos données dans le cloud toohello. L’enregistrement de ressources à partir d’une source de données, copies hello tooAzure des métadonnées des éléments multimédias, mais les données de hello restent dans l’emplacement de source de données existant hello. règle de toothis Hello exception est si vous choisissez d’enregistrements d’aperçu tooupload ou un profil de données lorsque vous inscrivez les biens hello. Lorsque vous incluez un aperçu, too20 enregistrements sont copiés à partir de chaque élément multimédia et stockées sous la forme d’un instantané dans le catalogue de données. Lorsque vous incluez un profil des données, les informations d’agrégation sont calculées et incluses dans les métadonnées de hello sont stockée dans le catalogue de hello. Informations d’agrégation peut inclure taille hello des tables, hello pourcentage de valeurs null par colonne, ou hello minimal, des valeurs maximales et moyennes pour les colonnes. 
>
>

> [!NOTE]
> Pour les sources de données telles que SQL Server Analysis Services qui ont une première classe **Description** propriété hello catalogue de données de publication d’application extrait cette valeur de propriété. Pour les bases de données relationnelles SQL Server qui n’ont pas une première classe **Description** propriété hello application de publication de catalogue de données extrait les valeur hello hello **ms_description** propriété étendue pour les objets et les colonnes. Pour plus d’informations, consultez la page [Utilisation de propriétés étendues sur les objets de base de données](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Combien doit prendre pour tooappear de ressources qui vient d’être référencées dans le catalogue de hello ?
Après avoir inscrit des ressources avec le catalogue de données, il peut être une période de 5 secondes too10 avant qu’ils apparaissent dans le portail du catalogue de données hello.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Comment annoter et enrichir les métadonnées hello pour mon actifs de données enregistrées ?
Hello métadonnées tooprovide façon la plus simple pour les ressources référencées est actif de hello tooselect dans le portail du catalogue de données hello et puis entrez les valeurs hello dans le volet de propriétés hello ou schéma pour l’objet sélectionné de hello.

Vous pouvez également fournir des métadonnées, telles que les balises et les experts pendant le processus d’inscription de hello. les valeurs Hello que vous fournissez dans hello service de publication de catalogue de données s’appliquent actifs tooall en cours d’inscription à ce moment-là. tooview hello objets récemment enregistrés dans le portail hello pour l’annotation supplémentaire, sélectionnez hello **vue portail** bouton sur l’écran final de hello Hello application de publication de catalogue de données.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Comment supprimer mes objets de données inscrits ?
Vous pouvez supprimer un objet à partir du catalogue de données en sélectionnant les objet hello dans le portail de hello puis en cliquant hello **supprimer** bouton. Objet de hello suppression supprime ses métadonnées de catalogue de données, mais n’affecte pas la source de données sous-jacente hello.

## <a name="what-is-an-expert"></a>Qu’est-ce qu’un expert ?
Un expert est une personne qui a un point de vue éclairé sur un objet de données. Un objet peut avoir plusieurs experts. Un expert, toobe hello « propriétaire » n’a pas besoin d’un objet, mais est simplement une personne qui sait comment les données de salutation peuvent et doit être utilisé.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Comment partager des informations avec l’équipe de catalogue de données hello si vous rencontrez des problèmes ?
problèmes de tooreport, partager des informations et poser des questions, accédez toohello [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Hello catalogue fonctionne avec une autre source de données qui m’intéresse ?
Nous travaillons activement sur l’ajout de plusieurs tooData de sources de données catalogue. Si vous souhaitez toosee une source de données pris en charge, il suggère (ou vocale votre prise en charge si elle a déjà été suggéré) en accédant de toohello [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>Comment est Azure Data Catalog liées toohello Data Catalog dans Power BI pour Office 365 ?
Vous pouvez considérer Azure Data Catalog d’évolution de hello catalogue de données dans Power BI. À compter du ressort 2017, Azure Data Catalog est utilisé tooenable hello de partage et de découverte des requêtes dans Excel 2016 et Power Query pour Excel. Fonctions de catalogue de données dans Excel sont toousers disponibles avec les licences Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>Que faire autorisations ai-je besoin actifs tooregister avec le catalogue de données ?
outil de toorun hello catalogue de données d’inscription, vous devez disposer des autorisations sur la source de données hello qui vous permet de métadonnées de hello tooread à partir de la source de hello. tooalso incluent une version d’évaluation, vous devez disposer des autorisations qui vous tooread dans les données hello à partir des objets hello en cours d’inscription.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>Data Catalog sera-t-il également disponible pour un déploiement local ?
Catalogue de données est un service cloud qui peut fonctionner avec le cloud et locales toodeliver de sources de données, une solution de détection de source de données hybride. Il n’existe actuellement aucun plan pour une version de hello service de catalogue de données qui s’exécute localement.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>Puis-je extraire plus ou les métadonnées à partir de sources de données hello qu'inscrire ?
Nous travaillons activement tooexpand les fonctionnalités de hello du catalogue de données. Si vous souhaitez toohave extraites à partir de la source de données hello lors de l’enregistrement des métadonnées supplémentaires, suggérer qu’il (ou vote pour celle-ci, si elle a déjà été suggéré) hello [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Bonjour future, nous permettra tiers tooadd nouveaux types de source données via une API d’extensibilité.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Comment restreindre visibilité hello inscrit de ressources de données, afin que seules certaines personnes peut les découvrir ?
Sélectionnez les ressources de données hello Bonjour catalogue de données, puis cliquez sur hello **Take Ownership** bouton. Les propriétaires de ressources de données dans le catalogue de données peuvent modifier la visibilité de hello paramètres tooeither autoriser hello de toodiscover tous les utilisateurs appartenant actifs ou restreindre les utilisateurs toospecific de visibilité.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Comment modifier l’enregistrement de hello pour une ressource de données afin que les modifications de source de données hello sont répercutées dans le catalogue de hello ?
métadonnées de hello tooupdate pour les ressources de données qui sont déjà enregistrés dans le catalogue de hello, réinscrivez simplement source de données hello qui contient les ressources hello. Les modifications apportées à la source de données hello, telles que les colonnes soient ajoutés ou supprimés à partir des tables ou vues, sont mises à jour dans le catalogue de hello, mais toutes les annotations fournies par les utilisateurs sont conservées.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>Il n’y a pas de réponse à ma question ici. Où puis-je en trouver une ?
Accédez toohello [forum Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Les questions qui y sont posées se retrouveront ici.
