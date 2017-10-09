---
title: "aaaAzure Mobile Engagement Guide de démarrage avec les meilleures pratiques"
description: "Guide de prise en main d’Azure Mobile Engagement et meilleures pratiques pour l’intégration"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Azure Mobile Engagement - Guide de prise en main et meilleures pratiques
## <a name="overview"></a>Vue d'ensemble
**écran mobile Hello est un espace très encombré :** dans 2013, une étude trouvé hello du périphérique mobile moyenne a 27 applications installées. Les utilisateurs passaient généralement 30 heures par mois sur leurs applications. La majeure partie de ce temps était consacrée aux réseaux sociaux et aux jeux (environ 20 heures). En 2014, hello Android marché avait applications environ 1,5 millions de toochoose les utilisateurs à partir de. store d’Apple Hello contenus environ 1.2 millions d’applications. L’utilisation des applications mobiles continue à augmenter alors que les développeurs se font concurrence sur ce marché en pleine expansion. 

moyenne Bonjour s’installer et désinstaller des applications avec haute fréquence en fonction de la modification des intérêts et des expériences dans l’application. En cas de réussite de commande toodetermine hello d’une application, il devient tooknow vital plus que simplement le nombre d’utilisateurs installe votre application. Il est important tooknow utile est de votre application et si cette tendance d’utilisation peut changer. Hello suivant questions est important :

* Les utilisateurs commencent toofind votre application sans intérêt ou obsolète ? 
* Combien d’utilisateurs ont complètement arrêté d’utiliser votre application ? 
* La tendance est-elle à la hausse ou à la baisse pour les achats in-app ?
* Les utilisateurs échouent toocomplete des flux de travail en raison de problèmes avec l’application hello ou manque d’intérêt ? 
* Pourriez vous conservez votre application utiles et pertinentes en envoyant la base des frais tooyour contenu utilisateur ? 
* Ce nouveau contenu serait hello même pour tous les utilisateurs ou se concentrent sur les segments d’utilisateurs basés sur le comportement de votre application ? 

Toothese similaire de réponses tooquestions peut vous aider à étendre la durée de vie hello et chiffre d’affaires à partir de votre application. Elles peuvent également vous aider à définir et à fidéliser votre base d’utilisateurs. 

Des média applications ont tendance à toohave certaines de rétention la plus élevée de hello entre utilisateurs. Une des raisons sont qu’ils fournissent constamment actualisées toousers de contenu. Adoption anticipée de notifications push utile dirigées segment d’un utilisateur tooa a tendance à toohave un fort impact sur la rétention de l’application. 

programme d’Azure Mobile Engagement Hello est conçue toohelp étendre la durée de vie hello et la rétention de votre application en fournissant une méthode toogather et d’analyser des informations détaillées sur l’utilisation de hello de votre application. Il vous permettra de classifier votre base d’utilisateurs en fonction de toobehavior et créer des campagnes ayant le focus pour la remise des notifications push et les messages dans l’application des segments d’utilisateurs tooidentified. Les indicateurs de performance clés (KPI) mesurent le degré d’activité de vos utilisateurs pour différents aspects de votre application. Azure Mobile Engagement fournit des méthodes de hello vous devez toodetermine ces indicateurs de performance clés. Il vous aide à accroître hello retour sur investissement (ROI) en fournissant l’infrastructure de hello, vous devez tooincrease engagement avec votre application mobile. 

Bonjour tooget de commande meilleur parti de Azure Mobile Engagement, vous devez toostart avec un plan d’engagement bien conçue. Votre plan vous aidera à identifier des données granulaires hello vous devez toosegment en mesure de toobe votre utilisateur base. Il peut être basé sur le comportement et les expériences au sein de l’application. Afin que votre plan de toobe réussie, il est une meilleure tooclearly de pratique définir hello indicateur de performance clé mesurera objectifs hello de votre application. Avec des indicateurs de gain de performances définis, vous pouvez facilement incorporer la logique nécessaire de hello dans vos toocollect fine-grained données d’application qui vous utilisez tooanalyze et évaluer vos indicateurs de performance clés. Cette rubrique est un guide des meilleures pratiques pour la définition des indicateurs de performance clés hello que vous utiliserez avec votre plan de projet. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Étape 1 : Définir votre modèle de résultat de hello toofit indicateurs de performance clés
Définir correctement les indicateurs de performance clés peut être une tâche difficile de toocomplete. Les applications conçues pour différents secteurs présentent des caractéristiques et des objectifs spécifiques, Cela peut généralement tooconfuse votre approche. toohelp éviter ce problème, les objectifs et les indicateurs de performance clés doivent être classées en trois catégories principales : **Business**, **Engagement**, et **technique**. C’est ce que nous appelons hello **modèle de solution**.

Un bon plan aura généralement les objectifs avec les indicateurs de performance clés hello qui mesurent les réussites hello dans chacune des hello suivant des catégories du modèle de résultat hello.

#### <a name="business-kpis"></a>KPI commerciaux
Indicateurs de performance clés entreprise doivent être hello plus simple partie toobuild. Vous les avez probablement déjà définis sous une certaine forme lors de la planification de votre application mobile. Ces KPI permettent généralement de mesurer les revenus et le retour sur investissement de votre application. Hello liste suivante fournit quelques exemples d’indicateurs de performance clés métier qui peut vous aider lors de la définition de vos indicateurs de performances :

* KPI commerciaux - Médias
  * Nombre de publicités cliquées
  * Nombre de pages consultées par utilisateur
  * Nombre d’abonnements en cours
* KPI commerciaux - Jeux
  * Nombre d’achats in-app
  * Revenu moyen par utilisateur
  * Temps passé par session
  * Nombre de jours joués et actuels dans le niveau du jeu
* KPI commerciaux - E-commerce
  * Nombre de jours d’utilisation de l’application
  * Revenu moyen par utilisateur
  * Montant moyen dans le panier lors du paiement
  * Catégorie de produit présentant le plus d’affichages et d’achats
* KPI commerciaux - Banques et assurances
  * Nombre de comptes
  * Fonctionnalités activées
  * Pages d’offre consultées
  * Alertes cliquées ou activées       

#### <a name="engagement-kpis"></a>KPI d’engagement
Un indicateur de performance clé Engagement est un engagement de hello performances indicateur toomeasure de vos utilisateurs. Les tendances dans cette zone de déterminer la rétention hello de votre application. Voici quelques exemples d’indicateurs de performance pour ce type de KPI :

* Utilisateurs actifs de hello ces 7 derniers jours
* Nombre d’utilisateur inactif pourquoi ces 7 derniers jours
* Nombre d’utilisateurs qui n’ont pas utilisé application hello des 30 derniers jours  

Certains facteurs externes évidents peuvent influencer les indicateurs de cette catégorie. Par exemple, vous pouvez envisager un toobe d’appareil mobile à un utilisateur à tout moment. Cela n’est pas nécessairement vrai. Une application de jeu peut avoir tendance d’utilisation plus élevé toohave autour des jours fériés lorsque passionné peut lire plus lors de l’école et travail.   

Bien définie dans cette catégorie peut vous aider à mesurer la relation hello entre votre application et vos clients.

#### <a name="technical-kpis"></a>KPI techniques
Les indicateurs de performance de cette catégorie vous aident à déterminer si votre application se comporte correctement, ne répond plus ou se bloque. Ces indicateurs peuvent mesurer la santé de votre application hello et déterminer les problèmes d’utilisation qui peuvent empêcher les utilisateurs d’utiliser l’application hello. Les informations collectées pour cette catégorie peut également contenir des informations de performances pouvant être pertinentes toomarketing équipes. les données de salutation peut également s’avérer utiles pour résoudre les problèmes à informatique et la prise en charge les équipes toohelp identifier des bogues. 

Voici quelques exemples de KPI techniques :

* Nombre d’exceptions non gérées ou gérées et informations les concernant 
* Date et heure du dernier incident
* Dernier bouton cliqué ou dernière page consultée
* Utilisation de la mémoire de l’application hello
* Fréquence d’images de l’application
* Version du système d’exploitation qui hello application est en cours d’exécution
* Version de l’application

Définir ces indicateurs de performance clés toohelp mesurer les performances d’application et identifier les bogues potentiels. Cette indicateurs doivent aider à réduire le temps de hello que vous devez toodeliver un correctif pour vos clients. Ils pourraient également vous aider à définir un segment d’utilisateurs ayant rencontré un problème particulier. Vous pouvez utiliser qu’utilisateur segmentation toocreate campagnes toodeliver des notifications concernant les correctifs disponibles et potentielle promotions toohelp récupérer la satisfaction des clients. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Exercice pratique nº 1 : créer votre tableau de bord de KPI
Lorsque vous définissez votre stratégie marketing, vos KPI doivent représenter chacun de vos principaux objectifs. Ils doivent être des points de données clairement définis qui permettent de toomonitor informations vitales toocollect votre application et hello le comportement de l’utilisateur final hello.

Créer un tableau de bord d’indicateur de performance clé qui contient hello sous informations

1. Quelles sont les hello indicateurs de performance clés pour l’application hello ?
2. Pointant de quelles données utiliser toorepresent chaque indicateur de performance clé ?
3. Où ces données se trouvent-elles pour mon application (écran, paramètres, système, etc.) ?
4. Puis-je exécuter une séquence d’engagement pour ce KPI ?

Vous pouvez utiliser hello **Générateur d’indicateur de performance clé** feuille de calcul dans notre [support manuel modèle] [ Media Playbook link] pour obtenir des exemples et des conseils.

## <a name="step-2-your-engagement-program"></a>Étape 2 : votre programme d’engagement
Un programme d’engagement mobile de qualité doit être considéré comme un composant clé de votre application. Cela doit absolument inclure un programme bienvenu performant qui s’exécute pour un utilisateur pendant hello premiers jours d’utilisation de l’application. Cela a tendance toohave un effet très positif sur l’engagement et la rétention de votre application. Des études ont montré que majorité hello d’arrêter les utilisateurs à l’aide d’une salutation application premiers jours après l’installation. Vous souhaitez toostrive toomeet ou dépassez intérêt de commande client expectation tôt pendant que l’utilisateur de hello se concentre sur votre application. Veillez à que vous présentez des avantages de votre application et de valeur de clé hello tooyour clients. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Notifications Push sont des engagements hello meilleure approche tooearly avec les utilisateurs d’appareils mobiles. Cependant, vous devez faire très attention lorsque vous segmentez les utilisateurs pour les notifications Push. En effet, dès qu’un utilisateur a le sentiment de recevoir du courrier indésirable ou des notifications inintéressantes, cela peut avoir des conséquences graves. En quelques clics, un utilisateur peut supprimer votre application tooreturn jamais. utilisateur de Hello devrait maintenant recevoir hautement personnalisée de valeur dans l’application au lieu de spam générique.

Une fois que les utilisateurs sont activement, votre programme engagement peut aider lecteur d’autres aspects de l’application hello.

Par exemple, vous pourriez configurer une campagne qui demande votre toorate utilisateurs actifs votre application. Étant donné que ce segment de l’utilisateur est hello plus actifs et hello la plus grande expérience avec votre application, vous attendez les toogive hello évaluation plus précise. Une fois que vous avez une classification des applications haute, il peut aider à augmenter le téléchargement d’organiques hello de votre application et réduire vos coûts d’acquisition de nouveau client.

#### <a name="engagement-sequence"></a>Séquence d’engagement
Un programme d’engagement global inclut différentes séquences d’engagement. Chaque séquence vise tooreach plusieurs objectifs.

###### <a name="life-push-sequence"></a>Séquence de transmission Push liée au cycle de vie
objectifs Hello pour une séquence de push de durée de vie sont différentes selon hello du cycle de vie de l’engagement de l’utilisateur hello avec application hello. Un utilisateur donné peut être nouveau, inactif ou très actif. À différents stades du cycle de vie de l’engagement, les utilisateurs peuvent bénéficier de votre nouvelle contenu sous forme de hello de toodocumentation conseils ou des liens. 

Par exemple un nouvel utilisateur peut doivent aider à la mise en route tooan orienté application ou bénéficier d’une nouvelle toohello de similaire incentive utilisateur, suivant hello première fois, qu'ils lancent l’application hello...

*« Toohave heureux que vous décidiez ! N’oubliez pas de toologin tooget le 1er du mois gratuit ! »*

###### <a name="behavioral-push-sequence"></a>Séquence de transmission Push comportementale
séquence de push comportementales Hello vise tooincrease sont basées sur le comportement de l’utilisateur collecté pour l’application hello.  

Par exemple, un utilisateur très actif d’une application de football fantastique peut bénéficier à partir de l’engagement par hello suivant de notifications push...

*« John, vous êtes un vrai fan de football américain ! Ouvrez une session dans la section de NFL tooour et gagnez accès gratuit toohello SuperBowl. »*

###### <a name="alerting-push-sequence"></a>Séquence de transmission Push d’alerte
Les utilisateurs apprécient de recevoir des actualités intéressantes axées sur leurs intérêts. Une séquence de transmission Push d’alerte améliore l’engagement en envoyant des alertes en fonction des intérêts qu’un utilisateur a clairement montrés. Cela peut être explicite lorsqu’un utilisateur sélectionne ses propres intérêts dans l’application hello. Il peut aussi être déterminé implicitement basé sur les données collectées au cours de l’interaction utilisateur avec l’application hello.

Par exemple, utilisateur hello d’une application de Commerce électronique peut acheter régulièrement une marque spécifique de café dont vous avez capturé avec une indicateur de performance clé d’entreprise. Hello alerte suivante permet d’améliorer l’engagement de cet utilisateur avec application hello.

*« Bonjour Wes, de votre marque favorite de café sera sur vente 25 % sur hello première semaine de septembre 2015. Nous vous remercions de vous en tant que client et souhaitiez toomake que vous étiez prenant en charge. »*

###### <a name="rentention-push-sequence"></a>Séquence de transmission Push de rétention
Cette séquence objectifs tooretain utilisateurs un toohelp de campagnes de notification push répétitives lecteur habitude régulière d’engagement avec application hello. Cela peut aider à augmenter la rétention de l’application si l’utilisateur de hello tire les interactions hello. 

Par exemple, hello d’une application associée sports peut s’afficher hello suivant une fois par semaine basée sur les équipes Favoris de l’utilisateur hello de notifications push :

*« Pour une chance toowin 200 points, go vote si hello New York Yankees gagne leur jeu cette semaine par rapport à Toronto bleu Jays ! ».*

#### <a name="hello-3w-approach"></a>approche de 3 w Hello
Maîtrise des séquences de push différents hello vous permettra de vous engager avec des utilisateurs finaux. Toutefois, vous devez toujours une approche de 3 w toouse hello pour personnaliser vos notifications. Hello 3 s approche doit répondre à qui, quand et que se passe-t-il pour chaque notification. Si vous répondez clairement à ces trois questions, vos notifications devraient être correctement ciblées pour l’engagement.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Qui : hello segment utilisateur qui reçoit les messages
En exécutant un push notifications tooyour les utilisateurs doit être considérée comme un canal de communication très sensibles. Assurez-vous que les notifications hello que viser un segment d’un utilisateur toosend tooa sont intérêts toohello également incluses dans l’étendue de ce segment de l’utilisateur. Une notification correctement routée est très probable toohave un effet négatif sur un utilisateur. Ils peuvent le jugent courrier indésirable des application tooyour en cours de désinstallation. 

Lorsque vous définissez les segments d’utilisateurs qui recevront des notifications, faites appel à un mélange de critères techniques et comportementaux spécifiques. Un exemple simple définition d’un segment de l’utilisateur peut être toohello similaire après l’instruction :

« Tous les utilisateurs qui a lancé hello une application mobile pour hello la première fois il y a 3 jours et visités page de connexion hello deux fois sans réellement terminer une connexion ».

Cette instruction permet d’identifier les données hello vous devriez toocollect toosupport un scénario spécifique.

###### <a name="what-hello-message-that-you-will-send"></a>Ce que : message de type hello à envoyer
**Ton**

Dans le cadre de vos engagements, utilisez un ton adapté aux utilisateurs du segment. Cela est certainement un tooconnect efficace avec vos utilisateurs finaux et promouvoir l’intérêt d’un utilisateur dans votre application. 

**Redirection**

Une notification push peut servir d’ouvrir plus d’application hello. Si hello message de notification fournit un contexte de diffusion news ou une promotion du produit, ce lien ciblé de notification peut directement toohello droite le contenu au sein de l’application hello. toosupport, vous devez créer une URL application de schéma toolet hello gèrent la redirection des hello. Lorsque vous travaillez sur vos séquences d’engagement, il s’agit d’une étape importante à laquelle il faut impérativement penser.

La redirection peut également être gérée pour d’autres systèmes. Par exemple, avec une URL d’Action, il est possible tooredirect les utilisateurs finaux réduire autres systèmes notamment hello suivantes :

* Un site web
* Une boîte aux lettres avec la messagerie déjà configurée
* Une boîte de réception de SMS
* Un service d’accès à distance
* Directement toohello Boutique d’applications pour l’application hello d’évaluation. 

Cela offre de nombreuses possibilités les utilisateurs finaux tooengage et créer des règles automatiques tooimprove performances.

**Format/contenu**

Différents types et formats de notification Push :

1. **Annonces** : vous permet de toosend publicité messages toousers à des moments différents (hors de l’application, dans l’application ou à tout moment).
2. **Interroge** : vous permettait de toogather des informations aux utilisateurs finaux en posant des questions. Ces réponses sont ensuite disponibles lors de la création des critères aux utilisateurs finaux tootarget.
3. **Push de données** : vous permet de toosend un binaire ou base64 données fichier tooupdate application hello. les informations de Hello contenues dans un push de données sont envoyées expérience des utilisateurs tooyour application toopersonalize hello dans votre application. Votre application a besoin de données de hello toosupport toobe conçu dans un push de données.
4. **Vignettes (Windows Phone uniquement)** : activé vous toouse hello services de notifications Push Microsoft (MPNS) toosend Notification Push Native contenant des données XML (pris en charge depuis la version 0.9.0 SDK. charge utile finale de Hello pour les vignettes ne peut pas dépasser 32 Ko.). message de type Hello apparaît directement sur la vignette de votre mère.
5. **Vue web** : fenêtre contextuelle comprenant du contenu web. Cette fenêtre contextuelle s’affiche lorsque l’utilisateur final hello a cliqué sur la notification d’émission hello. Un affichage web vous permet de toohave plus d’interaction avec l’utilisateur final hello.

> [!NOTE]
> Assurez-vous que contenu hello que vous envoyez en tant que des notifications push est compatible avec la plateforme de hello respectifs (iOS, Android, Windows) des recommandations pour le développement d’applications et d’envoyer des notifications push.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Quand : hello minutage de votre campagne
Lorsque est hello meilleur temps tooactivate une campagne de déclencher des notifications push ? Doit-elle être manuelle ou automatique ? Doit-elle être récurrente ? Détermination moment hello ou la fréquence est tooengage essentielles des utilisateurs avec des résultats optimaux hello. Pour chaque séquence de l’engagement et le scénario, vous devez spécifier quand sera hello meilleur temps toosend des notifications push. Voici quelques exemples possibles :

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

Si vous envoyez de nombreuses notifications tous les jours, vous devez prendre sérieusement en considération le fait que vos utilisateurs peuvent percevoir vos communications comme du courrier indésirable. 

Azure Mobile Engagement fournit deux méthodes toohelp éviter vos communications en cours perçues comme courrier indésirable. Tout d’abord, utilisez tooensure de segmentation de granularité fine vous faire hello de cible pas aux mêmes utilisateurs. En outre, Azure Mobile Engagement propose une fonctionnalité de « quotas ». Cette fonctionnalité permet de limiter les notifications envoyées pour une campagne. Par exemple, définir un too5 de quota par défaut par semaine garantit qu’un utilisateur inclus comme partie d’un segment d’un utilisateur hello campagne reçoit des notifications pas plus de 5 de cette semaine.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Exercice pratique nº 2 : créer votre programme d’engagement
Prenez le temps de synthèse de vos objectifs et définition des campagnes de hello que tooplay à l’aide de séquences spécifiques. Assurez-vous que vous appliquez des notifications de hello 3 s approche toohello dans vos campagnes marketing. 

Hello d’utilisation **Engagement programme** feuille de calcul hello [support manuel modèle] [ Media Playbook link] pour obtenir des exemples et des conseils.

## <a name="step-3-app-integration"></a>Étape 3 : intégration à l’application
#### <a name="create-a-tag-plan"></a>Création d’un plan de balises
toointegrate Azure Mobile Engagement dans votre application, vous devez toocreate un plan de la balise. plan de balise Hello est la clé de voûte de hello du projet de hello. Il définit la relation hello entre des spécifications marketing, les flux de travail hello de l’application hello et des données de balise réel hello collectées dans hello application toomeasure indicateurs de performance clés. Il indique quel analytique vous pourrez toosee dans le portail de hello. Il vous permet également de définir les segments d’utilisateurs et envoyer tooengage de notifications push ayant le focus à vos utilisateurs finaux. Une fois que vous avez plan de balise hello, ajout de toointegrate de code hello dans votre application est simple à l’aide de hello Kit de développement logiciel Azure Mobile Engagement.

Un plan de balises ne doit pas baliser tous les éléments d’une application. Il doit uniquement inclure les données de balise faisant partie de votre stratégie d’engagement mobile. Celles-ci seront probablement différentes d’une application à une autre. Hello [support manuel modèle] [ Media Playbook link] fournie par Azure Mobile Engagement permet, vous générez un plan de la balise avec une méthode donnée. Hello d’utilisation **balise Plan** planifier de votre numéro de feuille de calcul comme un toobuilding guide.

Lorsque vous définissez une section de la balise dans la feuille de calcul hello, être très spécifiques. Cela est très important tooavoid confusion. Détaillez chaque scénario attendu pour lequel chaque balise sera envoyée. Inclure le nom hello d’activité hello où chaque balise est incorporé. Cela doit tous être inclus dans hello **Informative** dans le cadre de la feuille de calcul hello. feuille de calcul Hello balise plan doit être de référence principales hello pour la vérification du test. 

Bonjour **toocollect de données** section, votre équipe de développement doit rechercher les types hello, les noms, les valeurs et les paires d’extra-info clé/valeur obligatoire pour chaque balise qui seront incorporé dans l’application hello.

Nous recommandons de consulter le plan de balise hello avec toutes les équipes sont associées au projet de hello. Apportez les corrections nécessaires et vérifiez que tout est clair pour les équipes de développement et marketing.

Hello **cahier des charges** feuille de calcul peut être guide toohelp utilisé toutes les personnes impliquées dans le projet de hello.

#### <a name="data-types"></a>Types de données
Il s’agit des types de données courants pris en charge par Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Appareils et utilisateurs
Azure Mobile Engagement identifie les utilisateurs en générant un identificateur unique pour chaque appareil. Cet identificateur est appelé identificateur de l’appareil hello (ou ID deviceid). Il est généré de manière à ce que toutes les applications en cours d’exécution sur ce partage de périphériques même hello même identificateur de l’appareil.

###### <a name="sessions-and-activities"></a>Sessions et activités
Une session est une instance de l’application hello en cours d’exécution par un utilisateur. session de Hello s’étend du temps hello utilisateur de hello démarre l’application hello, jusqu'à ce qu’il s’arrête.

Une activité est un regroupement logique d’un jeu lors d’une session d’application hello peut effectuer des tâches. Il s’agit généralement d’un écran en particulier dans une application hello, mais il peut être que tout élément défini par la logique de l’application hello hello. Balisez au minimum chaque écran ou activité pour votre application. Ainsi, vous toounderstand hello-chemin d’accès utilisateur.

###### <a name="events"></a>Événements
Les événements sont utilisés tooreport l’interaction utilisateur avec l’application hello. Il peut s’agir d’actions instantanées, telles que le partage de contenu ou le lancement d’une vidéo. Marquage des événements pour fournir des collections de données qui montrent comment les utilisateurs interagissent avec l’application hello. 

###### <a name="jobs"></a>Tâches
Les travaux sont utilisés tooreport les actions qui ont une durée. Voici quelques exemples :

* Exécution d’appels d’API
* Durée d’affichage des publicités
* Durée des tâches d’arrière-plan 
* Durée du processus d’achat
* Affichage d’une vidéo

###### <a name="errors"></a>Errors
Les erreurs sont tooreport utilisé les problèmes détectés par l’application hello. par exemple les actions utilisateur incorrectes ou les échecs d’appel d’API.

###### <a name="application-information"></a>Informations de l'application
Informations sur l’application (App-Info) sont utilisées tootag données liées tooa l’expérience utilisateur dans une application. Il est généré par l’intervention d’un utilisateur avec l’application hello. 

Pour une clé donnée app-info, Azure Mobile Engagement uniquement effectue le suivi de valeur la plus récente hello (aucun historique). App-info révèle état hello de votre application ou vos utilisateurs finaux. Par exemple hello ouverture de session de l’état ou groupe de produits favoris de l’utilisateur.

###### <a name="crash-data"></a>Données d’incident
Incidents automatiquement collectées par les défaillances d’application de rapports de kit de développement logiciel de Mobile Engagement hello ne pas gérées par l’application hello. par exemple une exception non gérée qui survient.

###### <a name="extra-data"></a>Données supplémentaires
Les événements, les erreurs, les activités et les tâches peuvent être optimisés à l’aide de paramètres. Il s’agit d’un développeur peut fournir en tant que données spécifiques à partir de l’application hello-des informations supplémentaires. C’est important pour définir une segmentation affinée. 

Par exemple, valeur hello d’une balise « article » vous permettra aux utilisateurs finaux toosegment selon qui afficher cet objet. Cependant, cela peut ne pas suffire. Il peut être plus intéressant d’inclure également dans cette même balise « article » des informations supplémentaires telles que « catégorie_information » au sein d’une activité. Cela serait utile toodetermine hello dynamiquement des catégories favorites pour l’utilisateur de hello. 

Les informations supplémentaires sont signalées sous forme de paire clé/valeur. Dans l’exemple hello pour cette application de support, hello extra-info pour « news_category » serait la valeur hello pour cette catégorie. par exemple « sport », « économie » ou « politique ».

#### <a name="tag-and-sdk-integration"></a>Intégration des balises et du Kit de développement logiciel (SDK)
Pour obtenir des instructions étape par étape pour l’intégration hello Kit de développement logiciel Azure Mobile Engagement dans votre application, suivez hello [intégration du Kit de développement logiciel Engagement](mobile-engagement-windows-store-integrate-engagement.md) documentation sur le site Web Azure. Choisissez votre plateforme cible à partir des liens de hello haut hello de cette page.

Nous vous recommandons de créer des projets pour deux applications s’appuyant sur Azure Mobile Engagement : Une pour le développement et test intermédiaire et hello autre pour la mise en lots de production. Votre équipe informatique peut ensuite promouvoir à partir de test mise en lots tooproduction lorsque le test d’acceptation utilisateur hello a réussi.

#### <a name="user-acceptance-testing-uat"></a>Test d’acceptation des utilisateurs (UAT)
Le test d’acceptation des utilisateurs (UAT) consiste à s’assurer que tout fonctionne comme prévu. Les workflows peuvent être menés à bien et rassembler toutes les données requises en fonction de votre plan de balises :

* Marquage des informations doit être en place selon des concepts AZME toodocumented
* Toutes les informations dont vous avez besoin sont collectées (y compris les valeurs d’informations supplémentaires et d’informations de l’application)
* Nomenclature correspond à tooyout conséquente, envisagez de balise
* Aucun doublon de balise n’est envoyé

Testez tous les types hello du comportement de notification que vous avez incorporé dans votre application

* Annonces, sondages, Push de données dans l’application et en dehors
* Vues de texte/web
* Mise à jour de badge, catégories

#### <a name="setup"></a>Paramétrage
La configuration d’Azure Mobile Engagement est très simple. Toute la documentation hello liées à l’interface utilisateur toohello est disponible sur le site Web Azure Mobile Engagement de hello, [comment toonavigate hello interface utilisateur](mobile-engagement-user-interface-home.md).

Il est recommandé de commencer par la configuration des rôles de droite hello et les appartenances aux rôles pour les utilisateurs de hello de votre projet. Cela vous permet de gérer la plate-forme de toohello d’accès appropriée pour tous les utilisateurs. Vos rôles peuvent inclure :

* Administrateurs
* Développeurs
* Utilisateurs 

Par la suite :

* Inscrire votre tootest deviceID sur votre propre appareil.
* Aller toohello les paramètres de votre compte et de graphiques de toohave hello fuseau horaire et l’heure de remise de notification définie pour votre fuseau horaire.
* Accédez toohello les paramètres de votre application et inscrire hello « App-info », vous avez besoin de l’utilisateur final tootarget à portée de main.

Pour plus d’informations sur comment toorun push votre première campagne de notification, consultez [comment tooget démarré à l’aide et la gestion exécute un push de tooreach des utilisateurs finaux de tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Conclusion
Les programmes d’engagement sont itératifs et vous devez en permanence améliorer le vôtre en déterminant ce qui fonctionne le mieux pour votre application à l’aide de tests. 

Au départ, lors du développement d’expérience avec engagement stratégies n’essaient pas toobuild une stratégie mission globale. Adopter une approche étape par étape identifier vos indicateurs de performance clés et comment tooleverage les. La stratégie d’engagement sera différente pour chaque application.

Une fois que vous avez développé de l’expérience vous pouvez considérer hello tooyour engagement programmes suivants :

* Suivi : vous attirez des utilisateurs et définissez probablement des sources de collecte de données. Azure mobile Engagement peut être des sources de toodata-collection liée. Il vous permet de toomonitor les performances de chaque source. Ces informations est toomaximize intéressante de vos investissements d’acquisition. 
* Test A/B : il s’agit d’une composante essentielle du programme d’engagement. Chaque application présente des caractéristiques spécifiques. Avec le test A/B, vous pouvez améliorer votre programme d’engagement.
* Emplacement géographique : il s’agit d’un atout considérable pour les marques. Fonctionnalité de toothis Merci, vous pouvez accéder au lieu de droite hello et l’heure. Nous vous recommandons de vérification que vous avez collecté suffisamment données de comportement de l’utilisateur final avant de démarrer toouse emplacement géographique.
* Push de données : le Push de données est une transmission Push invisible. Il vous permet de personnaliser votre application en fonction du comportement des utilisateurs finaux. Par exemple, si un segment de l’utilisateur consulte souvent des produits de haute technologie, propriétaire de l’application hello peut envoyer un push de données qui permettent de personnaliser sa page d’accueil avec le contenu de la haute technologie.

## <a name="next-steps"></a>Étapes suivantes
* [Créer un compte Azure Mobile Engagement](mobile-engagement-create.md).
* Visitez [définir votre stratégie Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn plus d’informations sur la définition de votre stratégie Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
