---
title: AAA(deprecated) FAQ - publier et utiliser les applications de Machine Learning dans Azure Marketplace | Documents Microsoft
description: "(déconseillée) Forum aux questions sur les applications de Machine Learning publication Bonjour Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(déconseillée) Publication et à l’aide d’applications de Machine Learning Bonjour Azure Marketplace : Forum aux questions

> [!NOTE]
> DataMarket et Data Services vont être mis hors service et les abonnements existants seront annulés à compter du 31/03/2017. Par conséquent, cet article deviendra obsolète. 
> 
> En guise d’alternative, vous pouvez publier votre toohello d’expériences d’apprentissage [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/) pour avantage hello de communauté de science des données hello. Pour plus d’informations, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Questions relatives à la consommation à partir de Marketplace
**1. Je reçois hello message d’erreur suivant après avoir entré pour le service web de hello entrée :**

**demande de Hello a généré une erreur de principal ou le délai d’attente principale. équipe de Hello enquête sur les problème de hello. Nous sommes désolés pour ce désagrément de hello. (500)**

Vos paramètres d’entrée ne soit pas conforme toohello le format requis pour le service web spécifique de hello. Reportez-vous toohello correspondante documentation lien toofind hello format correct pour les paramètres d’entrée et les limitations de hello de ce service web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Si le lien hello API pour le service web hello que je vois sur hello « Explorer ce jeu de données » la page et le coller dans une autre fenêtre de navigateur, les informations d’identification dois-je puis-je utiliser les résultats de hello tooaccess et comment copier les voir ?**

Vous devez utiliser votre compte Marketplace en tant que nom d’utilisateur hello et clé de compte principal hello en tant que mot de passe hello. Vous trouverez la clé de compte principal Hello sur hello **Explorer ce jeu de données** page sous description hello du service web de hello (cliquez sur hello **afficher** bouton). résultat de Hello peut s’afficher dans le navigateur de hello ou il peut être disponible trop téléchargement, selon le navigateur que vous utilisez.

**3. Je reçois hello message d’erreur suivant après la saisie d’entrée de hello pour le service web de hello sur la page de « Explorer ce jeu de données » hello :** 

**Une erreur inattendue s’est produite pendant le traitement de votre demande. Réessayez.**

Un ou plusieurs paramètres d’entrée de votre service web peuvent dépasse limite hello lors de l’utilisation du service web de hello sur marketplace de hello **Explorer ce jeu de données** page. services de Hello peuvent être appelées avec une longueur d’entrée le plus à l’aide de méthodes HTTP POST. Pour obtenir des exemples, consultez [exemples de solutions à l’aide de R sur l’apprentissage automatique et publié tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Pas pourquoi n’importe quel élément hello « Explorateur d’API » onglet int hello magasin Bonjour portail classique Azure ?** 

Il s’agit d’un problème connu avec hello Azure Marketplace de portail classique. équipe de Hello fonctionne tooresolve ce problème. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Questions relatives à la publication à partir d’Azure Machine Learning sur Marketplace
**1. Pourquoi mes transactions de logos ou d’images ne s’actualisent-elles pas pour mon service web ?** 

Logos et images sont mises en cache dans le portail de publication hello et peut prendre jusqu'à jours too10 pour un nouveau logo hello ou tooupdate d’image sur le portail hello.

**2. Pourquoi est-onglet de « Détail » hello de mon service web sur le Marketplace affichant un message d’erreur ?**

Il existe un problème connu de Marketplace lors de la connexion tooAzure Machine Learning pour plus d’informations de service. équipe de Hello fonctionne tooresolve ce problème.

**3. Pourquoi hello, exemple de code R dans les services web Azure Machine Learning hello ne fonctionne pas pour la consommation de services web hello dans Marketplace ?**

systèmes d’authentification Hello sont différents lors de la connexion des services web de Machine Learning tooAzure directement comparé les services web tooconnecting toothese via hello Marketplace. services Hello dans Marketplace sont des services OData, et elles peuvent être appelées avec des méthodes GET ou POST. 

**4. Pourquoi les liens de support hello de mon service web n'offre pas la mise à jour correctement pour certains de Mes offres ?**

Hello, prise en charge des liens sont globaux par le serveur de publication, et non par offre. 

**5. Comment puis-je publier un service web avec le mode de saisie de lot sur Marketplace ?**

mode d’entrée du lot Hello n’est actuellement pas pris en charge dans les services web Marketplace.

**6. Qui faut-il contacter tooget aide si vous avez des questions concernant devient un serveur de publication de données, ou si vous rencontrez des problèmes lors de la publication ?**

Contactez hello Azure Marketplace à < mailto:datamarketbd@microsoft.com > pour plus d’informations.

