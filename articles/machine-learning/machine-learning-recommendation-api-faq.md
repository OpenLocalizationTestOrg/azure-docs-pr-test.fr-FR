---
title: aaaSet haut et utilisez hello Machine Learning recommandations API | Documents Microsoft
description: "API Microsoft RECOMMANDATIONS créée avec le FAQ sur Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Forum aux questions relatif à la configuration et à l’utilisation de l’API de Machine Learning Recommendations
**Qu’est-ce que RECOMMENDATIONS ?**

> [!NOTE]
> Vous devez commencer à l’aide de hello Service cognitifs de recommandations API au lieu de cette version. Hello Service cognitifs recommandations remplacera ce service et toutes les hello nouvelles fonctionnalités seront développées il. Il propose de nouvelles fonctionnalités telles que la prise en charge du traitement par lot, un meilleur Explorateur d’API, une surface d’API plus propre, une expérience d’inscription/de facturation plus cohérente, etc.
> En savoir plus sur [migration toohello nouveau Service cognitifs](http://aka.ms/recomigrate)
> 
> 

Pour les organisations et les entreprises qui s’appuient sur les recommandations toocross vente incitative et de clients de services tootheir, recommandations dans Azure Machine Learning fournit un moteur de recommandations de libre-service. C’est une implémentation du filtrage collaboratif qui utilise la factorisation de matrice comme algorithme de base. Les développeurs d’applications peuvent accéder à RECOMMENDATIONS à l’aide d’API REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Que puis-je faire avec RECOMMENDATIONS ?**

RECOMMENDATIONS utilise comme données d'entrée un élément ou un ensemble d'éléments et renvoie une liste de recommandations pertinentes. Par exemple : un client d’un détaillant en ligne clique sur un produit. site de vente en ligne Hello envoie ce produit en tant que tooRECOMMENDATIONS d’entrée, obtient une liste de produits en retour et décide de ces produits s’affichera toohello client. Vous pouvez souhaitez toouse recommandations toooptimize votre Boutique en ligne ou même tooinform votre intérieur ventes centre d’appel ou de département.

**Existe-t-il des restrictions d’utilisation ?**

Recommandations a hello les limites d’utilisation suivantes :

* Nombre maximal de modèles par abonnement : 10
* Nombre maximal d'éléments qu'un catalogue peut contenir : 100 000
* nombre maximal de Hello de points d’utilisation qui sont conservés est ~ 5 000 000. Hello plus ancien est supprimé si nouveaux sera téléchargé ou signalé.
* La taille maximale des données pouvant être envoyées dans un message électronique (par exemple, importation des données de catalogue ou des données d’utilisation) est de 200 Mo
* Le nombre de transactions par seconde (TPS) pour une build de modèle Recommendations inactive est d’environ 2 TPS. Construction d’un modèle recommandations actif peut contenir jusqu'à too20 TPS.

## <a name="purchase-and-billing"></a>Achat et facturation
**Combien coûte des recommandations pendant la période de lancement hello ?**

Recommendations est un service par abonnement. La facturation est effectuée en fonction du volume de transactions par mois. Vous pouvez vérifier hello [offrent page](https://datamarket.azure.com/dataset/amla/recommendations) dans Microsoft Azure Marketplace pour les informations de tarification.

**Des coûts liés au suivi et au stockage de l’activité des utilisateurs de Recommendations me seront-ils facturés ?**

Pas au moment de hello.

**Existe-t-il une version d’évaluation gratuite de Recommendations ?**

Puisqu’il est gratuit qui est restreinte too10, 000 transactions par mois.

**Quand serai-je facturé pour l’utilisation de Recommendations ?**

Un abonnement payant est un abonnement pour lequel il existe des frais mensuels. Lorsque vous achetez un abonnement payant, vous êtes immédiatement facturé pour hello premier utilisation mois de. Vous payez un montant hello associé offre hello sur la page d’abonnement hello (plus taxes applicables). Cette facture mensuelle est établie chaque mois sur hello même calendar date sous forme de votre achat initial jusqu'à l’annulation d’abonnement de hello. 

**Comment mettre à niveau le service de niveau supérieur tooa ?**

Vous pouvez acheter ou mettre à jour votre abonnement à partir de hello [offrent page](https://datamarket.azure.com/dataset/amla/recommendations) page sur Microsoft Azure Marketplace.

Lorsque vous mettez à niveau un abonnement :

* Les transactions qui demeurent sur votre ancien abonnement ne sont pas ajoutées tooyour nouvel abonnement. 
* Vous payez le prix plein pour un nouvel abonnement hello, même si vous disposez des transactions inutilisées sur votre ancien abonnement.

Processus tooupgrade un abonnement :

* Nevigate toohello [offrent page](https://datamarket.azure.com/dataset/amla/recommendations).
* Connectez-vous toohello Marketplace si vous n’êtes pas déjà connecté.
* Dans le volet droit de hello, tous les plans de hello disponibles sont répertoriés. Cliquez sur bouton radio hello hello plan de tooupgrade à.
* Si vous souhaitez tooupgrade, cliquez sur **OK**. Si vous ne souhaitez pas tooupgrade, cliquez sur **Annuler**.

**Important** boîte de dialogue hello lire attentivement avant de mettre à niveau, car il existe des implications en matière de facturation et d’utilisation.

**Lorsque mes tooRecommendations abonnement se termine ?**

Votre abonnement prendra fin lorsque vous l’annulerez. Si vous souhaitez que toocancel vos abonnements, consultez hello suivant les instructions.

**Comment annuler mon abonnement à Recommendations ?**

toocancel votre abonnement, hello utilisation suivant les étapes. Si votre abonnement actuel est un abonnement payant, votre abonnement reste en vigueur jusqu'à fin hello Hello en cours de période de facturation. Si vous avez besoin de hello toobe annulation effective immédiatement, contactez-nous à l’adresse [Support technique de Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Remarque** aucun remboursement n’est donnée si vous annulez avant la fin hello d’une période de facturation ou pour les transactions inutilisées dans une période de facturation.

* Accédez toohello [offrent page](https://datamarket.azure.com/dataset/amla/recommendations).
* Connectez-vous toohello Marketplace si vous n’êtes pas déjà connecté.
* Cliquez sur **Annuler** toohello à droite de l’état et le nom du dataset hello. Vous pouvez utiliser cet abonnement jusqu'à hello Hello actuel de votre limite de transaction ou de la période de facturation fin (selon celle qui se produit en premier).

Si vous souhaitez que toocancel votre abonnement immédiatement par conséquent, vous pouvez acheter un abonnement, fichier un ticket à [Support technique de Microsoft](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Prise en main de Recommendations
**Recommendations est-il adapté à ma situation ?** 

Recommandations dans l’apprentissage est pour les entreprises qui s’appuient sur les recommandations toocross vente incitative produits ou services tootheir clients et. Si vous disposez d’un site Web à destination de vos clients, d’une équipe commerciale, d’une équipe commerciale interne ou d’un centre d’appels et si vous proposez un catalogue qui contient quelques dizaines de produits ou services, l’utilisation de Recommendations pourrait être un avantage pour vos résultats financiers. 

Expérimentation des recommandations est conçue toobe relativement simple. version basées sur des API actuelle de Hello nécessite des compétences de programmation de base. Si vous avez besoin d’aide, contactez le fournisseur hello développé votre site Web. Si vous avez un service informatique interne ou un développeur interne, ils doivent être en mesure de tooget des toowork de recommandations pour vous. 

**Quelles sont les conditions requises de hello pour des recommandations ?**

Recommandations nécessite que vous disposez d’un journal de choix de l’utilisateur en matière de tooyour catalogue. Si vous ne possédez pas ce type de journal mais que vous disposez d’un site web à destination des clients, Recommendations peut collecter l’activité des utilisateurs pour vous. 

Recommendations nécessite également un catalogue de vos produits ou services. Si vous n’avez pas catalogue de hello, recommandations peuvent utiliser les données d’utilisation client réel hello et distiller un catalogue. Un catalogue implicite n’inclut pas les éléments qui n’ont pas été signalés comme faisant partie des transactions utilisateur.

**Comment définir des recommandations pour hello première ?**

Après avoir [abonnement](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, vous devez utiliser la documentation de l’API de hello Bonjour [recommandations de formation Azure Machine - Guide de démarrage rapide](machine-learning-recommendation-api-quick-start-guide.md) tooset configuration du service hello.

**Où puis-je trouver la documentation de l’API ?** 

documentation de l’API de Hello est [Azure Machine Learning recommandations-Guide de démarrage rapide](machine-learning-recommendation-api-quick-start-guide.md).

**Que faire options j’ai tooRecommendations de tooupload catalogue et l’utilisation de données ?**

Vous avez deux options pour le téléchargement de vos données de catalogue et d’utilisation : vous pouvez exporter les données de hello à partir de votre système CRM ou d’autres journaux et téléchargez-le tooRecommendations, ou vous pouvez ajouter le site Web de tooyour de balises qui effectuera le suivi des activités des utilisateurs. Si vous utilisez la méthode de ce dernier hello, données de hello doivent être stockées dans Azure.

## <a name="maintenance-and-support"></a>Maintenance et assistance
**Quelle est la taille maximale de mon jeu de données ?**

Chaque jeu de données peut contenir too100, 000 éléments de catalogue et Mo too2048 des données d’utilisation.
En outre, un abonnement peut contenir des jeux de données too10 (modèles).

**Où puis-je obtenir une aide technique pour Recommendations ?**

Le support technique est disponible sur hello [Microsoft Azure prend en charge](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Où puis-je trouver des conditions d’utilisation de hello ?**

[Conditions de service de l’API de Microsoft Azure Machine Learning Recommendations.](https://datamarket.azure.com/dataset/amla/recommendations#terms)

