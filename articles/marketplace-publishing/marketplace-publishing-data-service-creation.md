---
title: "aaaGuide toocreating un Service de données pour hello Marketplace | Documents Microsoft"
description: "Comment toocreate, certifier et déployer un Service de données pour obtenir des instructions détaillées d’achat sur hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Guide de publication du Service de données pour hello Azure Marketplace
> [!IMPORTANT]
> **À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.** Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners). Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Après avoir effectué l’étape hello 1, [la création du compte et l’inscription](marketplace-publishing-accounts-creation-registration.md), nous vous découvrirez hello [général non technique](marketplace-publishing-pre-requisites.md) et [spécifications techniques](marketplace-publishing-data-service-creation-prerequisites.md) d’un Service de données offrent sur Azure Marketplace. Maintenant nous vous guidera à travers les étapes de hello pour la création d’une offre de Service de données sur hello [portail de publication] [ link-pubportal] pour hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Connexion toohello portail de publication.
Accédez trop[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Pour la première heure connexion tooPublishing Portal, utilisez hello même compte avec lequel vendeur de votre société de profil a été inscrite dans le centre de développement.**  (Vous pouvez ultérieurement ajouter tous les employés de votre société comme un co-admin Bonjour portail de publication).

Cliquez sur hello **publier des Services de données** en mosaïque si c’est la première connexion de hello dans le portail de publication hello.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Choisissez **Data Services** dans le menu de navigation hello hello côté gauche.
  ![dessin](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Créez un service de données.
Renseignez les titre hello pour votre nouvelle offre de Service de données et cliquez sur « + » sur hello droite.

  ![dessin](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Révision hello sous-menu sous hello créée récemment Service de données dans le menu de navigation hello.
Cliquez sur hello **procédure pas à pas** onglet et examinez toutes les étapes nécessaires requises toopublish correctement hello Service de données sur hello Azure Marketplace.

> [!TIP]
> Vous pouvez toujours cliquer sur les liens hello dans la page de « Procédure pas à pas » hello ou utiliser les onglets dans l’offre de Service de données hello sous-menu sur le côté gauche de hello.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Créez un plan.
### <a name="offers-plans-transactions"></a>Offres, plans, transactions.
Chaque offre peut avoir plusieurs plans, mais doit en avoir au moins un (1). Lorsque les utilisateurs finaux s’abonner tooyour offre qu’ils s’abonner pour l’une de Plan l’offre de hello. Chaque plan définit la façon dont les utilisateurs finaux seront être toouse en mesure de votre service.

Actuellement Azure Marketplace prennent en charge le modèle d’un niveau de Transaction d’abonnement mensuel basé uniquement pour les Services de données, autrement dit, les utilisateurs finaux payer des frais mensuels selon le prix toohello de plan spécifique de hello ils abonnés tooand sera en mesure de tooconsume chaque nombre de mois de transaction définie par le plan de hello.

Chaque Transaction généralement définie comme le nombre d’enregistrements renvoyés par votre Service de données basé sur la requête hello envoyé toohello Service. valeur par défaut Hello est 100. Nombre de transactions retournés tooeach requête sera nombre d’enregistrements divisé par 100 et arrondi au nombre entier le plus proche de toohello.

C’est le Service Azure Marketplace couche responsabilité toomonitor (compteur) nombre de transactions consommée par chaque requête.

> [!IMPORTANT]
> Les utilisateurs finaux qui atteint la limite de transaction hello mois hello seront bloqués de continuer le service de hello toouse jusqu'à la fin de leur cycle d’abonnement mensuel.
> 
> Hello plan ou un des plans de hello permettre (mais ne doit pas) inclut un nombre illimité de transactions.
> 
> 

### <a name="create-a-plan"></a>Créez un plan.
1. Cliquez sur **« + »** toohello suivant « ajouter un nouveau plan ».
2. Choisissez une des options de hello : **illimité** ou **limité** l’utilisation de ce plan.  Si nombre hello du plan de hello transaction fournis Limited autorisera tooconsume dans un mois.
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Portail de publication également suggère « Identificateur de Plan », qui sera utilisé toocommunicate toohello les utilisateurs finaux hello nom du plan hello dans l’interface utilisateur de hello et utilisée également par hello tooidentify de marché Service hello Plan. Vous pouvez modifier hello « Identificateur de Plan » si vous le souhaitez.
   
   > [!NOTE]
   > Hello « Identificateur de Plan » doit être unique dans l’étendue de hello de chaque offre. Comme de nombreux autres identificateurs utilisés dans hello planifier de portail de publication identificateur sera verrouillé une fois hello premier tooproduction de publication et que vous ne sera pas en mesure de toochange cet identificateur.
   > 
   > 
3. Cliquez sur tooaccept de votre choix.
4. Vous êtes ensuite invité à répondre à quelques questions supplémentaires concernant votre plan nouvellement créé.
   
    ![dessin](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Question | Signification |
| --- | --- |
| **Ce plan est gratuit et disponible dans le monde entier** |Vous pouvez créer un plan entièrement gratuit. Si son hello envisagez uniquement pour cette offre, cela signifie que vous publiez « Offre gratuite » Bonjour Marketplace. S’il s’agit uniquement pour des (peu) Plan, hello vous donne une option toooffer les utilisateurs finaux toolearn plus d’informations sur votre service avec un petit nombre de transactions par mois.  Si les réponses hello sont « Oui », vous n’êtes invitée aucun autre question. |

> [!NOTE]
> Les utilisateurs finaux peuvent toujours mettre à niveau toohello payé plans.
> 
> 

| Question | Signification |
| --- | --- |
| **Existe-t-il un essai gratuit ?** |Vous pouvez choisir entre « Aucune évaluation » tout ou donner un toouse option votre Plan pour « Mois ». Éditeurs, tels que toouse cette tooprovide les utilisateurs finaux hello possibilité toounderstand hello avantages liés aux options de hello offrent gratuitement pendant un mois. |

> [!IMPORTANT]
> Les utilisateurs finaux seront en mesure de toopurchase une évaluation gratuite si elles ont établi paiement carte de crédit, par exemple, accord entreprise.
> 
> Après un mois de la version d’évaluation gratuite de hello, Azure Marketplace démarrera charge clients prix hello date hello d’abonnement de hello, sauf si le client de hello initiée par l’annulation d’abonnement hello. Aucune notification spéciale ne sera fournie aux utilisateurs finaux toohello.
> 
> 

| Question | Signification |
| --- | --- |
| **Ce plan requiert un toopurchase de code de promotion ?** |Serveurs de publication ont une tootheir d’accès toolimit option Plans de Service en fournissant un code spécial, appelé « A du Promocode » toospecific clients. Uniquement les utilisateurs finaux qui disposera de cet Promocode seront en mesure de toosubscribe toohello Plan. Si vous choisissez « Non », vous acceptez que tout le monde à partir de la région de hello où hello offrent est disponible (voir [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) pour plus de détails) seront en mesure de toosubscribe toothis plan. Vous n’aurez à répondre à aucune autre question. |
| **Également masquer ce plan pour toute personne ne disposant pas d’un code promotionnel valide ?** |Si hello répondre toohello précédent à la question est « Oui » hello serveur de publication a un toocompletely option apparaissant dans hello l’interface utilisateur de hello Marketplace pour supprimer ce plan. Cela signifie que, les clients verront pas ce plan dans la page de détails de l’offre de hello. Les utilisateurs finaux afin de recevront un toopurchase du promocode, seront tooit toosubscribe en mesure d’à l’aide du promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Créez votre contenu marketing pour Marketplace.
Pour la façon dont les informations de tooprovide requises dans **Marketing, tarification, prise en charge et des catégories** onglets, visitez [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) qui est commun tooall artefacts publiées Bonjour Azure Marketplace.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Connectez votre tooyour offre de Service (en fonction de SQL Azure ou repose sur le Service Web).
Cliquez sur hello **Data Services** sous-menu.

Sur la moitié supérieure de hello de page de hello vous serez invité à indiquer l’offre de hello tooprovide **Namespace**.  

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.png)

Hello ci-dessous question définit comment hello Publisher va tooexpose nouvellement créé offre tooAzure Marketplace. (Pour plus d’informations, consultez hello [Guide requis technique des Services données](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Hello de publication de base de données basée service**

Cliquez sur **Base de données**. Hello suivant page s’affiche :

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate un mappage de CSDL pour hello Dataset basé sur hello de base de données SQL Azure :

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.4.png)

Puis pour chaque table

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.6.png)

Dans le cas d’un service web

  ![dessin](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Lecture [mappage existant web tooOData service via CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) pour obtenir des instructions détaillées et des exemples de création d’un Service Web de CSDL.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez créé votre offre de Service de données, assurez-vous d’effectuer les instructions hello Bonjour [Guide de contenu Marketing Marketplace](marketplace-publishing-push-to-staging.md) avant de vous déplacez vers le bas trop[votre Service de données de test dans la mise en lots](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Voir aussi
* [Mise en route : Comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)
* Si vous êtes intéressé par le fonctionnement hello le processus de mappage global OData et leur objectif, lisez cet article [mappage du Service de données OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview définitions, des structures et des instructions.
* Si vous êtes intéressé par apprentissage et comprendre les nœuds spécifiques hello et leurs paramètres, lisez cet article [nœuds de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) pour les définitions et des explications, des exemples et contexte de cas d’utilisation.
* Si vous souhaitez parcourir les exemples, consultez cet article [exemples de mappage de données Service OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee exemple de code et comprendre la syntaxe du code et du contexte.

[link-pubportal]:https://publish.windowsazure.com
