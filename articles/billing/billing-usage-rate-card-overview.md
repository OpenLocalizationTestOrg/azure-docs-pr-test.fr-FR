---
title: "API de facturation d’aaaAzure | Documents Microsoft"
description: "En savoir plus sur l’utilisation de facturation d’Azure et RateCard APIs, qui sont utilisés tooprovide connaître la consommation des ressources Azure et les tendances."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/18/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: b3214996cc3279f76fdc7f0dbd2059c3ae7bb15c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-billing-apis-tooprogrammatically-get-insight-into-your-azure-usage"></a>Utilisez API de facturation Azure tooprogrammatically obtenir un aperçu de votre utilisation d’Azure
Utilisez les données d’utilisation et de la ressource toopull API de facturation d’Azure à vos outils d’analyse de données par défaut. Hello l’utilisation des ressources Azure et RateCard APIs peuvent vous aider à prévoir avec précision et de gérer les coûts. Hello API sont implémentés en tant qu’un fournisseur de ressources et la partie de la famille hello d’API exposées par hello Azure Resource Manager.  

## <a name="azure-invoice-download-api-preview"></a>API Azure Invoice Download (version préliminaire)
Une fois hello [participer a été terminée](billing-manage-access.md#opt-in), les factures de téléchargement à l’aide de la version d’évaluation de hello [facture API](/rest/api/billing). fonctionnalités de Hello :

* **Role-based Access Control de Azure** -configurer l’accès à des stratégies sur hello [portail Azure](https://portal.azure.com) ou via [applets de commande Azure PowerShell](/powershell/azure/overview) toospecify les utilisateurs ou les applications peut accéder données d’utilisation de l’abonnement toohello. Les appelants doivent utiliser les jetons Azure Active Directory standard pour l’authentification. Ajoutez hello appelant tooeither hello du lecteur de facturation, lecteur, le propriétaire ou contributeur rôle tooget accès toohello données d’utilisation pour un abonnement Azure spécifique.
* **Filtrage de dates** -hello d’utilisation `$filter` tooget paramètre date de fin de la période de facture de toutes les factures hello dans l’ordre chronologique inverse par hello. 

> [!NOTE]
> Cette fonctionnalité est dans la première version de la version préliminaire et sujet incompatibles toobackward modifications peut-être être. Elle n’est actuellement pas disponible pour certaines offres d’abonnement (EA, CSP, AIO non pris en charge) et Azure Allemagne.

## <a name="azure-resource-usage-api-preview"></a>API Azure Resource Usage (version préliminaire)
Hello d’utiliser Azure [API de l’utilisation des ressources](https://msdn.microsoft.com/library/azure/mt219003) tooget vos données de consommation Azure estimée. Hello API inclut :

* **Role-based Access Control de Azure** -configurer l’accès à des stratégies sur hello [portail Azure](https://portal.azure.com) ou via [applets de commande Azure PowerShell](/powershell/azure/overview) toospecify les utilisateurs ou les applications peut accéder données d’utilisation de l’abonnement toohello. Les appelants doivent utiliser les jetons Azure Active Directory standard pour l’authentification. Ajoutez hello appelant tooeither hello du lecteur de facturation, lecteur, le propriétaire ou contributeur rôle tooget accès toohello données d’utilisation pour un abonnement Azure spécifique.
* **Agrégations horaires ou quotidiennes** : les appelants peuvent indiquer s’ils souhaitent visualiser leurs données d’utilisation Azure par intervalles de temps horaires ou quotidiens. valeur par défaut Hello est quotidienne.
* **Métadonnées de l’instance (y compris les balises de ressources)** – obtenir des détails au niveau de l’instance comme hello uri de ressource complet (/subscriptions/ {id d’abonnement} /...), hello des informations sur les groupes de ressources et les balises de ressources. Ces métadonnées vous permet de façon déterministe et allouer par programmation de l’utilisation par des balises hello, pour les cas d’usage, comme la charge entre.
* **Métadonnées des ressources** -détails de la ressource comme nom de compteur hello, catégorie de compteur, sous-catégorie de jauge, unité et région donner à l’appelant de hello une meilleure compréhension de ce qui a été consommé. Nous travaillons également la terminologie de métadonnées tooalign ressource hello portail Azure, Azure utilisation CSV, EA CSV, de facturation et autres expériences publics, toolet vous corréler les données des expériences.
* **Utilisation pour tous les types d’offre** : les données d’utilisation sont accessibles pour tous les types d’offre, tels que Paiement à l’utilisation, MSDN, Engagement monétaire, Crédit monétaire et Contrat Entreprise (EA).

## <a name="azure-resource-ratecard-api-preview"></a>API Azure Resource RateCard (version préliminaire)
Hello d’utilisation [API RateCard de ressources Azure](https://msdn.microsoft.com/library/azure/mt219005) liste de hello tooget de ressources Azure disponibles et des informations de tarification estimées pour chacun. Hello API inclut :

* **Role-based Access Control de Azure** -configurer vos stratégies d’accès sur hello [portail Azure](https://portal.azure.com) ou [applets de commande Azure PowerShell](/powershell/azure/overview) toospecify les utilisateurs ou les applications peut accéder toohello RateCard données. Les appelants doivent utiliser les jetons Azure Active Directory standard pour l’authentification. Ajoutez hello appelant tooeither hello du lecteur, le propriétaire ou contributeur rôle tooget accès toohello données d’utilisation pour un abonnement Azure spécifique.
* **Prise en charge des offres Paiement à l’utilisation, MSDN, Engagement monétaire et Crédit monétaire (offre EA non prise en charge)** : cette API fournit des informations de tarif au niveau des offres Azure.  appelant Hello de cette API doit passer taux et les détails de la ressource tooget informations offre hello. Nous sommes taux d’EA tooprovide actuellement impossible, car les offres EA personnalisé taux par l’inscription. 

## <a name="scenarios"></a>Scénarios
Voici quelques scénarios hello sont rendues possibles avec une combinaison de hello de hello d’utilisation et hello RateCard APIs :

* **Azure dépenses au cours des mois de hello** -combinaison de hello d’utilisation de hello d’utilisation et RateCard APIs tooget mieux appréhender votre cloud dépenses au cours des mois de hello. Vous pouvez analyser toutes les heures hello et des estimations de compartiments quotidiennes de l’utilisation et la facturation.
* **Configurer des alertes** : hello d’utilisation et hello RateCard APIs tooget estimée de la consommation de cloud et les frais, configurer des alertes basée monétaire ou ressource.
* **Prédire la facture** – Get votre consommation estimée cloud dépenses et appliquer d’apprentissage algorithmes toopredict quel facture hello serait à fin hello Hello cycle de facturation.
* **Avant la consommation de l’analyse du coût** – utilisez hello RateCard API toopredict est la quantité de votre facture serait pour votre utilisation attendue lorsque vous déplacez votre tooAzure les charges de travail. Si vous avez des charges de travail existantes dans d’autres clouds ou les clouds privés, vous pouvez également mapper votre utilisation avec tooget de taux Azure hello passent d’une meilleure estimation de Azure. Cela donne estimation vous hello toopivot de capacité sur l’offre et compare et contraste entre les types d’autre offre hello au-delà de paiement à l’utilisation, telles qu’engagement et crédit. Hello API vous donne également hello capacité toosee coût différences par région et vous permet de toodo un toohelp d’analyse de simulation coût décisions de déploiement.
* **Analyse de scénarios** -
  
  * Vous pouvez déterminer s’il est plus économique toorun les charges de travail dans une autre région ou dans une autre configuration de ressource Azure de hello. Ressource Azure, les coûts peuvent différer selon hello région Azure que vous utilisez.
  * Vous pouvez également déterminer si un autre type d’offre Azure propose un meilleur tarif pour une ressource Azure.
  
## <a name="partner-solutions"></a>Solutions de partenaires
[L’utilisation de Microsoft Azure et RateCard API activer Cloudyn tooProvide ITFM pour les clients](billing-usage-rate-card-partner-solution-cloudyn.md) décrit l’expérience d’intégration hello offerte par les partenaires de l’API de facturation Azure [Cloudyn](https://www.cloudyn.com/microsoft-azure/). Cet article parle leurs expériences et inclut une vidéo qui montre comment vous pouvez utiliser Cloudyn et hello insights de tooget API de facturation d’Azure à partir des données de consommation de Azure.

[Cloud Cruiser et intégration de l’API de facturation Microsoft Azure](billing-usage-rate-card-partner-solution-cloudcruiser.md) décrit comment [rapide du Cloud Cruiser pour Azure Pack](http://www.cloudcruiser.com/partners/microsoft/) fonctionne directement depuis le portail Windows Azure Pack (WAP) de hello. Vous pouvez gérer en toute transparence de ces deux aspects de hello opérationnels et financiers de hello cloud Microsoft Azure privé ou publique à partir d’une seule interface utilisateur.   

## <a name="next-steps"></a>Étapes suivantes
* Passez en revue les exemples de code hello sur GitHub :
  * [Exemple de code de l’API Invoice](https://go.microsoft.com/fwlink/?linkid=845124)

  * [Exemple de code de l’API Usage](https://github.com/Azure-Samples/billing-dotnet-usage-api)

  * [Exemple de code de l’API RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)

* toolearn en savoir plus sur hello Azure Resource Manager, consultez [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md). 

* Pour plus d’informations sur suite hello d’outils toohelp nécessaire, vous obtenez une présentation du cloud dépenses, consultez l’article de Gartner hello [Guide de marché pour les outils de l’informatique financières Management (ITFM)](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).

