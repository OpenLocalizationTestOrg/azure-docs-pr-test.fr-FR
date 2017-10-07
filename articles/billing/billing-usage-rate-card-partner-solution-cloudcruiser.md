---
title: "aaaCloud Cruiser et intégration de l’API de facturation Microsoft Azure | Documents Microsoft"
description: "Fournit une perspective unique du partenaire de la facturation Microsoft Azure Cloud Cruiser, sur leurs expériences intégration hello API de facturation Azure dans leurs produits.  Ces informations sont particulièrement utiles pour les clients Azure et Cloud Cruiser qui souhaitent utiliser ou essayer Cloud Cruiser pour Microsoft Azure Pack."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: b65128cf-5d4d-4cbd-b81e-d3dceab44271
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;sirishap;bryanla
ms.openlocfilehash: 74cc19bdeed26c6684210736caa0cb365e8f8821
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-cruiser-and-microsoft-azure-billing-api-integration"></a>Intégration des API Microsoft Azure Billing par Cloud Cruiser
Cet article décrit comment les informations de hello recueillies à partir de hello que nouvelles Microsoft Azure facturation API sont utilisables dans le Cloud Cruiser pour les flux de travail coûtent simulation et l’analyse.

## <a name="azure-ratecard-api"></a>API Azure RateCard
Hello RateCard API fournit des informations de taux de Azure. Une fois l’authentification avec les informations d’identification appropriées hello, vous pouvez interroger hello API toocollect métadonnées sur les services de hello disponibles sur Azure, ainsi que des tarifs de hello associés à votre ID d’offre.

Hello Voici un exemple de réponse à partir de l’API hello montrant les prix hello pour hello A0 (Windows) instance :

    {
        "MeterId": "0e59ad56-03e5-4c3d-90d4-6670874d7e29",
        "MeterName": "Compute Hours",
        "MeterCategory": "Virtual Machines",
        "MeterSubCategory": "A0 VM (Windows)",
        "Unit": "Hours",
        "MeterRates":
        {
            "0": 0.029
        },
        "EffectiveDate": "2014-08-01T00:00:00Z",
        "IncludedQuantity": 0.0,
        "MeterStatus": "Active"
    },

### <a name="cloud-cruisers-interface-tooazure-ratecard-api"></a>Cloud tooAzure d’Interface de Cruiser RateCard API
Cloud Cruiser peut tirer parti des informations RateCard API hello de différentes façons. Pour cet article, nous allons montrer comment il peut être utilisé toomake IaaS la charge de travail coût simulation et l’analyse.

toodemonstrate ce cas d’usage, imaginez une charge de travail de plusieurs instances en cours d’exécution sur Microsoft Azure Pack (WAP). objectif de Hello est toosimulate cette même charge de travail sur Azure et estimer les coûts de hello de faire de ce type de migration. Dans commande toocreate cette simulation, il existe deux principales tâches toobe effectuées :

1. **Importation et processus hello service informations collectées à partir de hello RateCard API.** Cette tâche est également effectuée sur des classeurs hello, où extrait hello hello RateCard API est transformé et publié tooa nouveau plan de taux. Ce nouveau plan de taux sera utilisé sur hello simulations tooestimate hello prix Azure.
2. **Normalisation des services WAP et des services Azure pour IaaS.** Par défaut, les services WAP reposent sur des ressources individuelles (UC, taille de la mémoire, taille de disque, etc.), alors que les services Azure sont basés sur la taille d’instance (A0, A1, A2, etc.). Cette première tâche peuvent être effectuées par le moteur ETL du Cloud Cruiser, appelée classeurs, où ces ressources sont disponibles sur les tailles d’instance, les services d’instance tooAzure analogue.

### <a name="import-data-from-hello-ratecard-api"></a>Importer des données à partir de hello RateCard API
Cloud Cruiser classeurs fournissent un moyen automatisé toocollect et processus des informations à partir de hello RateCard API.  Les classeurs ETL (extraction, transformation et chargement) vous permettent de collection de hello tooconfigure, transformation et la publication de données dans la base de données du Cloud Cruiser hello.

Chaque classeur peut avoir un ou plusieurs regroupements, ce qui vous toocorrelate des informations à partir de sources différentes toocomplement ou enrichir les données d’utilisation de hello. Hello suivant deux captures d’écran afficher comment toocreate un nouveau *collection* dans un classeur existant et l’importation des informations dans hello *collection* de hello RateCard API :

![Figure 1 : création d’une collection][1]

![Figure 2 : importer des données à partir de la nouvelle collection de hello][2]

Après avoir importé les données de salutation dans le classeur de hello, il est possible de toocreate plusieurs étapes et processus de transformation toomodify et modèle de données hello. Pour cet exemple, étant donné que nous intéresse uniquement infrastructure-as-a-Service (IaaS), nous pouvons utiliser des lignes inutiles hello transformation étapes tooremove, ou les enregistrements, liées tooservices autre que IaaS.

Hello capture d’écran suivante illustre les étapes de transformation hello tooprocess hello recueillies à partir de l’API de RateCard :

![Figure 3 : Transformation étapes tooprocess collectées données à partir de l’API de RateCard][3]

### <a name="defining-new-services-and-rate-plans"></a>Définition de nouveaux services et formules tarifaires
Il existe des services de toodefine de différentes manières sur Cloud Cruiser. Une des options de hello est tooimport les services de hello hello données d’utilisation. Cette méthode est généralement utilisée lorsque vous travaillez avec des clouds publics, où les services de hello sont déjà définies par le fournisseur de hello.

Un taux de Plan est un ensemble de taux de change ou les prix qui peuvent être appliqués toodifferent services, selon les dates de validité, ou un groupe de clients, entre autres options. Plans de taux peuvent également servir de simulation de toocreate Cloud Cruiser ou scénarios « What-if », toounderstand répercussions par des modifications dans les services du coût total de hello de charge de travail.

Dans cet exemple, nous allons utiliser les informations du service à partir de nouveaux services hello RateCard API toodefine hello dans Cloud Cruiser. Bonjour même façon, nous pouvons utiliser taux hello associés toohello toocreate un nouveau Plan de taux sur Cloud Cruiser des services.

À fin hello du processus de transformation hello, il est toocreate possible une nouvelle étape et publier des données de hello d’hello RateCard API en tant que les taux et les nouveaux services.

![Figure 4 : publication des données de hello de hello RateCard API en tant que de nouveaux Services et tarifs][4]

### <a name="verify-azure-services-and-rates"></a>Vérifier les services et tarifs Azure
Après la publication de services de hello et de tarifs, vous pouvez vérifier la liste hello des services de Cloud Cruiser importés *Services* onglet :

![Figure 5 : vérification hello nouveaux Services][5]

Sur hello *taux Plans* onglet, vous pouvez vérifier de nouveau plan de taux hello appelé « AzureSimulation » avec des taux de hello importée à partir de hello RateCard API.

![Figure 6 : vérification hello nouveau Plan de vitesse et de tarifs associés][6]

### <a name="normalize-wap-and-azure-services"></a>Normaliser les services WAP et Azure
Par défaut, WAP fournit des informations d’utilisation en rapport avec hello du calcul, de mémoire et de ressources réseau. Dans le Cloud Cruiser, vous pouvez définir vos services basées directement sur l’allocation de hello ou limitées l’utilisation de ces ressources. Par exemple, vous pouvez définir un taux de base pour toutes les heures d’utilisation du processeur ou frais hello en Go de mémoire allouée tooan instance.

Pour cet exemple, les coûts de toocompare commande entre WAP et Azure, nous devons tooaggregate hello l’utilisation des ressources sur le proxy d’application Web en lots, qui peut ensuite être mappé tooAzure services. Cette transformation peut être facilement implémentée dans les classeurs hello :

![Figure 7 : transformer les services de toonormalize WAP][7]

dernière étape de Hello au classeur de hello donnée toopublish hello dans la base de données du Cloud Cruiser hello. Au cours de cette étape, les données d’utilisation de hello sont désormais fournies dans les services (qui mappent toohello Services Azure) et lié les frais de hello toocreate toodefault taux.

Après la fin de classeur hello, vous pouvez automatiser le traitement de hello des données de hello, par l’ajout d’une tâche dans le Planificateur de hello et en spécifiant la fréquence de hello et l’heure pour hello classeur toorun.

![Figure 8 : planification du classeur][8]

### <a name="create-reports-for-workload-cost-simulation-analysis"></a>Créer des rapports concernant la simulation et l’analyse des coûts de la charge de travail
Une fois que l’utilisation de hello est collectée et frais sont chargés dans la base de données du Cloud Cruiser hello, nous pouvons exploiter hello Cloud Cruiser Insights module toocreate hello la charge de travail coût simulation qui nous attachons.

Commande toodemonstrate ce scénario, nous avons créé hello suivant du rapport :

![Comparaison des coûts][9]

graphique du haut Hello présente une comparaison de coût par les services, en comparant les prix hello de charge de travail hello en cours d’exécution pour chaque service spécifique entre WAP (bleu foncé) et Azure (bleu clair).

graphique du bas Hello affiche hello mêmes données répartis par service. Cela indique hello coûts pour chaque département de toorun leur charge de travail WAP et sur Azure, ainsi que de hello différence dans la barre d’économies hello (vert).

## <a name="azure-usage-api"></a>API Azure Usage
### <a name="introduction"></a>Introduction
Microsoft a récemment introduit hello API de l’utilisation d’Azure, permettant aux abonnés par extraction de données tooprogrammatically dans l’utilisation des données toogain connaître leur consommation. Il s’agit d’une excellente nouvelle pour les clients de Cloud Cruiser qui peuvent tirer parti de hello plus riche jeu de données disponible via cette API.

Cloud Cruiser peut tirer parti de l’intégration hello avec hello API d’utilisation de plusieurs façons. granularité de Hello (informations d’utilisation de toutes les heures) et les informations de métadonnées de ressources disponibles via hello que fournit des API hello dataset nécessaires toosupport flexibles Showback ou rétrofacturation modèles. 

Dans ce didacticiel, nous présente un exemple de comment Cloud Cruiser peut bénéficier des informations sur l’utilisation des API de hello. Plus spécifiquement, nous créer un groupe de ressources sur Azure, associer des balises de structure de compte hello, puis décrivent hello des processus d’extraction et de traitement des informations de balise hello dans Cloud Cruiser.

objectif final de Hello est toobe toocreate en mesure de rapports comme hello suivant un et être en mesure de tooanalyze de coût et consommation basée sur la structure de compte hello remplie par des balises de hello.

![Figure 10 : rapport avec répartitions à l’aide de balises][10]

### <a name="microsoft-azure-tags"></a>Balises Microsoft Azure
données Hello disponibles via hello API de l’utilisation d’Azure incluent non seulement les informations sur la consommation, mais également les métadonnées des ressources, y compris les balises associées. Balises fournissent un moyen simple de tooorganize vos ressources, mais dans toobe d’ordre efficace, vous devez tooensure qui :

* Les balises sont appliquées correctement toohello ressources au moment de l’approvisionnement
* Balises sont utilisées correctement sur la structure de compte hello Showback/rétrofacturation processus tootie hello utilisation toohello organisation.

Ces deux spécifications peuvent être difficiles, en particulier lorsqu’un processus manuel sur la fourniture de hello ou le côté de la charge. Erreur de saisie, incorrects ou manquants même balises sont plaintes des clients lorsqu’à l’aide de balises et ces erreurs peut effectuer une durée de vie sur hello côté très difficile de chargement.

Avec hello nouvelle API de l’utilisation d’Azure Cloud Cruiser peut extraire des informations de marquage de ressource et via un outil ETL perfectionné appelé classeurs, corriger ces erreurs de balisage courants. Par la transformation à l’aide d’expressions régulières et la corrélation des données, Cloud Cruiser peut identifier les ressources correctement avec balises et appliquer des balises correct de hello, garantissant hello correct association entre les ressources hello et consommateur de hello.

Sur le côté de la charge de hello, Cloud Cruiser automatise hello Showback/rétrofacturation processus et peut tirer parti des hello balise informations tootie hello utilisation toohello consommateur approprié (service, Division, projet, etc.). Cette automatisation représente une amélioration majeure et  garantit un processus de facturation cohérent et vérifiable.

### <a name="creating-a-resource-group-with-tags-on-microsoft-azure"></a>Création d'un groupe de ressources avec des balises dans Microsoft Azure
Hello première étape de ce didacticiel est toocreate un groupe de ressources Bonjour portail Azure, puis créer des balises tooassociate toohello ressources. Pour cet exemple, nous allons créer hello les étiquettes suivantes : département, environnement, propriétaire, projet.

capture d’écran Hello ci-dessous montre un exemple de que groupe de ressources avec hello associées des balises.

![Figure 11 : groupe de ressources avec des balises associées dans le portail Azure][11]

étape suivante de Hello est toopull hello plus d’informations à partir de hello API d’utilisation dans le Cloud Cruiser. Hello API d’utilisation fournit actuellement des réponses au format JSON. Voici un exemple de données hello récupérées :

    {
      "id": "/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXX/providers/Microsoft.Commerce/UsageAggregates/Daily_BRSDT_20150623_0000",
      "name": "Daily_BRSDT_20150623_0000",
      "type": "Microsoft.Commerce/UsageAggregate",
      "properties":
      {
        "subscriptionId": "bb678b04-0e48-4b44-XXXX-XXXXXXXXX",
        "usageStartTime": "2015-06-22T00:00:00+00:00",
        "usageEndTime": "2015-06-23T00:00:00+00:00",
        "meterName": "Compute Hours",
        "meterRegion": "",
        "meterCategory": "Virtual Machines",
        "meterSubCategory": "Standard_D1 VM (Non-Windows)",
        "unit": "Hours",
        "instanceData": "{\"Microsoft.Resources\":{\"resourceUri\":\"/subscriptions/bb678b04-0e48-4b44-XXXX-XXXXXXXX/resourceGroups/DEMOUSAGEAPI/providers/Microsoft.Compute/virtualMachines/MyDockerVM\",\"location\":\"eastus\",\"tags\":{\"Department\":\"Sales\",\"Project\":\"Demo Usage API\",\"Environment\":\"Test\",\"Owner\":\"RSE\"},\"additionalInfo\":{\"ImageType\":\"Canonical\",\"ServiceType\":\"Standard_D1\"}}}",
        "meterId": "e60caf26-9ba0-413d-a422-6141f58081d6",
        "infoFields": {},
        "quantity": 8

      },
    },


### <a name="import-data-from-hello-usage-api-into-cloud-cruiser"></a>Importer des données à partir de hello API d’utilisation dans le Cloud Cruiser
Cloud Cruiser classeurs fournissent un moyen automatisé toocollect et processus des informations à partir de hello API d’utilisation. Un classeur de (extraction, transformation et chargement) ETL vous permet de collection de hello tooconfigure, transformation et la publication de données dans la base de données du Cloud Cruiser hello.

Chaque classeur peut comporter une ou plusieurs collections. Cela vous permet de toocorrelate des informations à partir de sources différentes toocomplement ou augmentation hello les données d’utilisation. Pour cet exemple, nous allons créer une nouvelle feuille dans le classeur de modèle Azure hello (*UsageAPI)* et définir un nouveau *collection* tooimport des informations à partir de hello API d’utilisation.

![Figure 3 : données de l’utilisation des API importées dans une feuille de UsageAPI hello][12]

Notez que ce classeur a déjà des autres feuilles tooimport des services à partir de Azure (*ImportServices*) et traiter les informations sur la consommation de hello de hello API de facturation (*PublishData*).

Ensuite, nous allons utiliser hello de hello API d’utilisation toopopulate *UsageAPI* feuille et des informations de hello mettre en corrélation avec les données de consommation de hello de hello API de facturation sur hello *PublishData* feuille.

### <a name="processing-hello-tag-information-from-hello-usage-api"></a>Traitement des informations de balise hello de hello API d’utilisation
Après avoir importé les données de salutation dans le classeur de hello, nous allons créer des étapes de transformation Bonjour *UsageAPI* feuille dans l’ordre tooprocess hello plus d’informations à partir de l’API de hello. Première étape consiste à toouse un Bonjour de tooextract processeur « Fractionner JSON » des balises à partir d’un champ unique, puis créer des champs pour chacune d'entre elles (service, projet, propriétaire et environnement).

![Figure 4 : créer des champs pour les informations de balise hello][13]

Hello d’avis « Mise en réseau » service manque des informations de balise hello (jaune), mais nous pouvons vérifier qu’il fait partie de hello même groupe de ressources en examinant hello *ResourceGroupName* champ. Étant donné que nous avons balises hello pour hello autres ressources à partir de ce groupe de ressources, nous pouvons utiliser cette hello de tooapply informations ressource toothis de balises plus loin dans le processus de hello manquante.

étape suivante Hello est toocreate une recherche table association hello plus d’informations à partir de hello balises toohello *ResourceGroupName*. Cette table de choix sera utilisée sur hello suivant étape tooenrich hello la consommation de données avec les informations de balise.

### <a name="adding-hello-tag-information-toohello-consumption-data"></a>Ajout de données de consommation hello balise informations toohello
Maintenant nous pouvons accéder toohello *PublishData* feuille, les processus qui hello de hello API de facturation, les informations de consommation et ajouter des champs hello extraites à partir de balises de hello. Ce processus est exécuté en examinant la table de recherche hello créée à l’étape précédente hello, à l’aide de hello *ResourceGroupName* en tant que clé hello pour les recherches de hello.

![Figure 5 : remplissage de la structure de compte hello avec les informations de hello de recherches de hello][14]

Notez que les champs de la structure hello compte approprié pour le service de « Mise en réseau » hello ont été appliquées, résolution des problème de hello avec hello balises manquantes. Nous avons aussi remplis champs de structure de compte hello pour les ressources autre que notre groupe de ressources cible avec « Autre », dans l’ordre toodifferentiate sur hello des rapports.

Nous devons maintenant simplement tooadd une étape toopublish hello l’utilisation des données. Au cours de cette étape, taux de hello appropriés pour chaque service défini sur notre Plan de taux sera appliqué toohello informations d’utilisation, avec les frais résultant hello chargées dans la base de données hello.

partie de meilleures Hello est que vous n’avez toogo ce processus une seule fois. Lorsque le classeur de hello est terminée, vous devez simplement tooadd il toohello planificateur et elle seront exécutera toutes les heures ou tous les jours à hello de heure planifiée. Il est simplement la création de rapports ou personnalisation existantes, dans l’ordre tooanalyze hello données tooget des informations significatives à partir de votre utilisation du cloud.

### <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des instructions détaillées sur la création de Cloud Cruiser classeurs et rapports, veuillez vous reporter tooCloud Cruiser en ligne de [documentation](http://docs.cloudcruiser.com/) (connexion valide requis).  Pour obtenir plus d’informations sur Cloud Cruiser, contactez [info@cloudcruiser.com](mailto:info@cloudcruiser.com).
* Consultez [obtenir votre consommation de ressources Microsoft Azure](billing-usage-rate-card-overview.md) pour une vue d’ensemble de l’utilisation des ressources Azure de hello et RateCard APIs.
* Extraire hello [référence d’API REST de facturation Azure](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) pour plus d’informations sur les deux API qui font partie de jeu hello des API fournies par hello Azure Resource Manager.
* Si vous souhaitez que toodive directement dans l’exemple de code hello, découvrez nos exemples de Code API de facturation Microsoft Azure sur [exemples de Code Azure](https://azure.microsoft.com/documentation/samples/?term=billing).

### <a name="learn-more"></a>En savoir plus
* Consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) toolearn article plus hello Azure Resource Manager.

<!--Image references-->

[1]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Create-New-Workbook-Collection.png "Figure 1 : création d’une collection"
[2]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Import-Data-From-RateCard.png "Figure 2 : importer des données à partir de la nouvelle collection de hello"
[3]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transformation-Steps-Process-RateCard-Data.png "Figure 3 : Transformation étapes tooprocess collectées données à partir de l’API de RateCard"
[4]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Publish-RateCard-Data-New-Services-Rates.png "Figure 4 : publication des données de hello de hello RateCard API en tant que de nouveaux Services et tarifs"
[5]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing1.png "Figure 5 : vérification hello nouveaux Services"
[6]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Verify-Azure-Services-And-Pricing2.png "Figure 6 : vérification hello nouveau Plan de vitesse et de tarifs associés"
[7]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Transforming-WAP-Normalize-Services.png "Figure 7 : transformer les services de toonormalize WAP"
[8]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workbook-Scheduling.png "Figure 8 : planification du classeur"
[9]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/Workload-Cost-Simulation-Report.png "Figure 9 : exemple de rapport pour le scénario de comparaison de coût de la charge de travail hello"
[10]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/1_ReportWithTags.png "Figure 10 : rapport avec répartitions à l’aide de balises"
[11]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/2_ResourceGroupsWithTags.png "Figure 11 : groupe de ressources avec des balises associées dans le portail Azure"
[12]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/3_ImportIntoUsageAPISheet.png "Figure 12 : données de l’utilisation des API importées dans une feuille de UsageAPI hello"
[13]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/4_NewTagField.png "Figure 13 - créer de nouveaux champs pour les informations de balise hello"
[14]: ./media/billing-usage-rate-card-partner-solution-cloudcruiser/5_PopulateAccountStructure.png "Figure 14 : remplissage de la structure de compte hello avec les informations de hello de recherches de hello"
