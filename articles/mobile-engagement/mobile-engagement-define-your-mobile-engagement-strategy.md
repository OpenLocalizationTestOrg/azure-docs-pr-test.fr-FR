---
title: "aaaDefine votre stratégie Mobile Engagement | Documents Microsoft"
description: "Découvrez comment tooonboard et optimiser votre Engagement Mobile avec analytique et des notifications push."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7533e318-81b9-4360-aace-b7be8225985b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: afe32cb71019092eb28f2a8557404d60ad48ada4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-your-mobile-engagement-strategy"></a>Définir votre stratégie Mobile Engagement
*Vous avez écrit votre application pour une raison : toohave vos utilisateurs utilisent !*

Nous pensons que vous certainement placer une bonne traitent d’effort en essayant de toomake il une application que les utilisateurs apprécieront. Vous investi probablement une quantité importante d’utilisateurs de tooacquire budget marketing. Mais après pointe agréable de hello initial d’utilisateurs, vous pouvez voir les lentement arrêter à l’aide de votre application. *Ceci est le Azure Mobile Engagement !* : contourner les toostick et vous tooincrementally améliorer votre application via le test et en savoir plus.

Nos rétention de tooimproving approche et l’utilisation est basée sur recourant à des utilisateurs d’application par le biais des notifications push et les messages dans l’application, mais de manière très spéciale, des messages et de communication adaptée toothem, chaque comportement tootheir en fonction de votre application. Notre objectif est toolet que vous communiquez avec public adapté de hello au moment hello et emplacement hello.

Mais pour ce faire, vous aurez toostart avec *présentation de vos utilisateurs*, puis créez des groupes selon qu’ils a ou leurs caractéristiques (nous l’appelons segments), puis segment tooeach de communications pertinentes.

## <a name="mobile-engagement-serves-your-objectives"></a>Mobile Engagement répond à vos objectifs
*Nous avons cité la fidélisation et l’utilisation, mais dans quel but ?*

Pour créer votre stratégie Mobile Engagement, vous devez d’abord tenir compte des objectifs et des indicateurs de performance clés (KPI) de votre application.

Commencez par définir des objectifs de hello et indicateurs de performance clés qui aident à toodefine à votre engagement en cas d’usage avec prisme de droite hello.

Les cas d’usage sont une liste simple de campagnes que vous souhaitez toocommunicate toomake avec vos utilisateurs, allant d’accueil simple hello, toohello très avancée notification utilitaire déclenchée par votre système informatique. Un cas d’usage bien construit doit inclure au moins trois des hello *what-qui-lorsque*:

1. Une désignation très courte (par exemple, une « Campagne de bienvenue »)
2. **Ce que**: un exemple de message (par exemple, « toohave heureux que vous décidiez ! N’oubliez pas de toologin tooget le 1er du mois gratuit ! »). Ce message par aucun moyen final, que vous serez en mesure de toochange il quand que vous le souhaitez, mais elle permet généralement toostart penser qui nous souhaitez toosay.
3. **Qui**: segment hello qui recevra ce message (par exemple, « tous les utilisateurs qui a lancé tout d’abord des application hello pour hello fois il y a 3 jours, visités page de connexion hello mais n'êtes pas connecté à »).
   * Oui, vous pouvez le faire facilement avec Azure Mobile Engagement :)
   * Là encore, cela n’a pas toobe final que vous pouvez définir vos segments à tout moment, mais il est important toodefine tôt dans votre tooensure de critères de segmentation vous collectez des données de droite hello.
4. **Lorsque**: minutage hello de votre campagne. Il peut s'agir d'une date donnée ou du moment qui suit une action spécifique, basé sur un déclencheur. Mobile Engagement offre une importante durée possibilités toorightly votre communication.

Une fois que les cas d’usage et de segment sont définies, il donne une indication toodefine les données de salutation qui doivent être collectées au sein d’une application. C’est rôle hello d’un *« plan de la balise »*. Un plan de la balise permet tooensure qui collecte des données hello est spécifié toohello développeurs. Par conséquent, les développeurs sont en mesure de tooembed Mobile Engagement par hello à droite de la configuration vous toowork vos campagnes avec des données de droite hello. Il sera également très important toorun tests tooensure hello intégration est correcte et qu’il collecte ce dont vous avez besoin.

Basé sur l’intégration de hello, une fois que les applications sont publiées, vous avez un sont être en mesure de toosee votre analytique en temps réel, segmenter votre audience et puis démarrez toosend Active ciblé tooengage de notification push avec les utilisateurs finaux dans ou en dehors de l’application hello.

### <a name="use-cases-tooget-started"></a>Tooget de cas d’usage démarré
1. Bienvenue dans la stratégie : créer des campagnes de notification push plusieurs selon le comportement de l’utilisateur final hello au lancement hello d’application hello dans l’ordre de retenir toore à D + 2/5/10/15 après hello première session et l’augmentation première exécution rétention.
2. Promouvoir un nouveau contenu (fonctionnalité, l’article/vidéo ou produit) basé sur comportement hello hello par l’utilisateur toosend hello informations seuls tooend-les utilisateurs qui sont plus susceptibles de tooengage.
3. Taux d’application hello : cible inférieure à 1 pour cent de votre base de l’utilisateur qui est probablement étoiles d’application 5 hello toorate sur le magasin de hello.
4. Privilégier les abonnements : promouvoir contenu précieuses tooend-les utilisateurs que vous n’ont pas lu les encore tooincrease abonnement.
5. Didacticiel : n'imposez plus de didacticiel à tous les utilisateurs. Pourquoi ne pas générer super didacticiels dans l’application, puis le déclencheur les messages dans l’application uniquement si l’utilisateur de hello semble toonot utilisation hello app ou a des difficultés à utiliser une fonctionnalité ?

## <a name="why-do-you-need-analytics-tooengage"></a>Pourquoi devez-vous analytique tooengage ?
Comme vous le réalisez peut-être à ce stade, la diffusion de notifications push ne suffit pas. concept de base Hello de Mobile Engagement toohelp marketing et les développeurs prendre contact avec l’utilisateur final de la droite hello moment hello Bonjour droite placer. tooknow ces trois concepts essentiels, il est analytique toogather essentielles à partir de votre application, puis l’utiliser toosegment votre audience. Le bénéfice est encore plus grand quand des segments de comportements viennent compléter les données d'une autre base de données ou CRM, ou d'un canal croisé. Mobile Engagement permet la récupération des données à partir de n’importe quel endroit et l’utilise audience de droite tootarget hello.

toobe hello plus contextuel possible lorsque vous utilisez votre public, il est crucial toohave hello savoir du comportement des utilisateurs finaux hello, tooknow leur état dans en temps réel. Collecte de données permet de toofocus marketing réellement sur les cas d’usage tooplay d’accompagnement et leurs objectifs de stratégie mobile engagement. Pour atteindre les objectifs de hello définies précédemment est également hello motif recommandé hello en fait pas toogather n’est pas défini et tous les éléments dans analytique de hello, mais uniquement celles qui vous permettent de toofocus sur ce que vous souhaitez toolearn et votre cas d’utilisation. Il s’agit de toostart bon moyen de hello, essayez, test Découvrez la solution de hello toouse et l’adresse actives de notifications push et augmenter la rétention hello d’une application de toobring à un niveau de l’histoire de réussite.

> [!NOTE]
> N’oubliez pas : Trop de données supprime les données hello !
> 
> 

### <a name="use-cases-and-best-practices"></a>Cas d’utilisation et meilleures pratiques
Bonjour sections suivantes, nous allons brièvement certaines clés en cas d’utilisation qui nous sommes arrivés liste notre tooget de clients que vous avez démarré.

#### <a name="media"></a>Médias
Collecter de type hello du contenu qui est consommé par l’utilisateur final hello et puis audience hello basé sur ce comportement tootarget des types de contenu public tooan uniquement qui sera probablement tooconsume de segment. De cette façon, vous évitez d'envoyer des courriers indésirables à toute une base d'utilisateurs et vous assurez une meilleure fidélisation.

#### <a name="m-commerce"></a>M-commerce
Collecter les plus visités dans toopromote du public hello application et la cible de catégories de produits hello une remise ou nouveau produit dans cette catégorie qui hello par l’utilisateur sera probablement toopurchase. Objectif de chiffre d’affaires tooboost. À nouveau l’objectif de hello n’est pas toospam !

#### <a name="gaming"></a>Jeux
Collecter le niveau hello de jeu pour un utilisateur final et hello le temps passé dans une audience de hello tootarget période donnée qui peut être bloquée et serait probablement toojump tooa ensuite niveau avec une offre de bonus.

Communiquer sur des événements spécifiques avec des utilisateurs un incentive toothose pas jouer pour certains tooencourage tootry de temps les tooreturn.

#### <a name="retail"></a>Vente au détail
Collecter les produits hello ou marques une audience doit être le plus probable tooconsume basé sur le comportement ou les Favoris et lecteur hello audience tooyour magasin tooincrease bon chiffre d’affaires.

#### <a name="banking"></a>Opérations bancaires
Collecter des données à partir des utilisateurs finaux qui a créé un compte à hello premier lancement d’application hello. Objectif toodeploy une stratégie de bienvenue avec une notification push ciblé et augmenter le nombre hello d’abonnements de compte.

### <a name="how-toocreate-a-great-tag-plan"></a>Comment toocreate une balise excellente plan ?
Un plan de balise doit correspondre à une description du chemin d’accès utilisateur de hello ou un type de flux de travail de l’application hello, en fournissant tous les hello balises nécessaires (données) qui doivent être collecté toohave suffisamment de comportement de l’utilisateur toounderstand analytique et correctement de base d’utilisateurs hello segment. Il ne s'agit pas d'un processus technique. Par conséquent, les spécialistes du marketing est toospecify en mesure de hello données toocollect en fonction de leur stratégie Mobile Engagement.

Hello minimale est tootag au moins tous les écrans de hello (appelé *activités* dans Mobile Engagement) d’une application. Cela permet de déterminer le chemin d’accès utilisateur de hello.

Une activité peut contenir des *événements* qui collectent des informations d’action, par exemple, un clic sur un bouton. Cela permet la collection hello d’interactions au sein de l’application hello. Par conséquent, les spécialistes du marketing est en mesure de tooknow les utilisateurs qui écran sont sur le site et ce qu’ils font.

`Jobs` sont des actions avec une durée. Il s’agit très utile pour les toounderstand sont la durée nécessaire pour un toocreate utilisateur de compte ou toologin pour l’instance. Cela peut également être utile pour les développeurs toomonitor de la durée pendant laquelle il faut toocall un service web.

`Errors`peut également être analysé tooknow si les utilisateurs rencontrent des problèmes dans votre application. Par exemple, s’ils rencontrent souvent des problèmes de connexion.

Tous de ce type de données peuvent être augmentés avec des paramètres (*supplémentaire-informations* dans Mobile Engagement) qui vous toogather dynamique des données à partir de l’application hello. Il s’agit de segmentation de granularité fine tooallow important. Par exemple, les spécialistes du marketing peut segmenter un utilisateur en fonction de type hello du contenu, ils ont utilisé une. type Hello de contenu sera informations dynamiques de hello d’une activité ou un événement.

*Informations de l’application* sont des données qui vous permet de tooconfirm hello d’état de l’application hello ou d’utilisateur de hello en temps réel. Également, cela permet de toocategorize une base de l’audience et cibler rapidement. Par exemple, il peut utiliser statut Vrai/faux si hello utilisateur se connecte ou non, ou la date d’expiration de son abonnement.

#### <a name="example-of-tags"></a>Exemple de balises
*Cas d’utilisation : Segment audience comportement tootarget hello droit par l’utilisateur avec le contenu de la notification push droite hello*

1. Envoyer toopromote de notification push à une catégorie de produit : collecter l’audience de toosegment de données de comportement basé sur la catégorie hello du produit qu’ils ont visités x heures dans une période donnée ou un élément spécifique qu’ils ont ajoutés dans un panier d’achat. données Hello collectées vous toosegment et envoyer une audience de droite toohello de notification push.
2. Application de hello taux : collecter des données en fonction du contenu hello partagé par une audience hello sur un réseau social. Vise le public de hello toosegment en déterminant hello *ambassadeurs* de votre application. À l’aide d’une push notification dans l’application, les ambassadeurs hello sont audience de meilleures hello de votre toorate de tooask application votre application 5 étoiles dans le magasin de hello.
   
   ![][1]

*Cas d’utilisation : données déclaratives*

1. Les nouvelles alertes de segment : collecter l’audience de toosegment déclarative des données en fonction de leurs préférences. Ainsi, vous pouvez envoyer une notification push sur un sujet particulier qui intéresse vraiment une audience spécifique.
2. Segmentez l'audience en fonction de l'état de connexion. Collecter les données tooknow si un utilisateur est connecté ou qu’il a créé un compte. Permet aux utilisateurs finaux de la cible qui n’ont pas encore connecté dans et envoie un tooconvert de l’utilisateur final de tooencourage de notification push.
   ![][2]

### <a name="next-steps"></a>Étapes suivantes
* Visitez [Concepts d’Engagement Mobile] toolearn plus d’informations sur les concepts de base de Mobile Engagement.
* Visitez [créer une application d’Engagement Mobile](mobile-engagement-create.md) toocreate une nouvelle Collection d’application Mobile Engagement dans Azure et démarrer la gestion de vos applications avec le portail Mobile Engagement de hello.
* Visitez [meilleures pratiques](mobile-engagement-getting-started-best-practices.md) toogo dans les détails.
* Visitez [scénario d’application de jeu](mobile-engagement-gaming-scenario.md) toolearn sur l’implémentation de Mobile Engagement avec un exemple d’application de jeu. 
* Visitez [scénario d’une application multimédia](mobile-engagement-media-scenario.md) toolearn sur l’implémentation de Mobile Engagement avec un exemple d’application de support. 
* Visitez [didacticiels] toolearn plus sur l’implémentation de hello.

<!-- Images. -->
[1]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case1.png
[2]: ./media/mobile-engagement-define-your-mobile-engagement-strategy/use-case2.png

<!-- URLs. -->
[Concepts d’Engagement Mobile]: http://azure.microsoft.com/documentation/articles/mobile-engagement-concepts/
[didacticiels]: http://azure.microsoft.com/documentation/articles/mobile-engagement-ios-get-started/

