---
title: toomicroservices aaaIntroduction sur Azure | Documents Microsoft
description: "Vue d’ensemble de pourquoi il est important pour le développement d’applications modernes de création d’applications de cloud avec une approche microservices et comment Azure Service Fabric fournit une plateforme tooachieve cela."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Pourquoi un microservices approche toobuilding applications ?
Pour les développeurs de logiciels que nous sommes, il n’y a rien de nouveau dans notre conception de l’affacturage d’une application en composants. Il s’agit de paradigme de centrale hello orientation objet abstractions de logiciels et composants réutilisables. Aujourd'hui, cette factorisation a tendance à écran de hello tootake des classes et des interfaces entre les couches de technologie et les bibliothèques partagées. En règle générale, une approche hiérarchisée est adoptée avec un magasin principal, une logique métier de couche intermédiaire et une interface utilisateur frontale. Ce que *a* hello évolution de ces dernières années est que, en tant que développeurs, avons distributed applications pour le cloud de hello et contrôlée par l’entreprise hello.

évolution des besoins professionnels Hello sont :

* Un service qui est généré et opère au niveau de clients tooreach de mise à l’échelle dans des régions géographiques nouveau (par exemple).
* Remise plus rapide de fonctionnalités et fonctions toobe toorespond en mesure de toocustomer demandes dans une solution agile.
* Coûts de tooreduce d’utilisation améliorée des ressources.

Ces besoins de l’entreprise affectent *la manière* dont nous créons des applications.

Pour plus d’informations sur l’approche de hello de toomicroservices Azure, consultez [Microservices : une révolution application alimentée par le cloud de hello](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Approches de conception monolithique et de microservices
Toutes les applications évoluent au fil du temps. Applications réussies évoluent en étant toopeople utile. Les applications ratées n’évoluent pas et sont, en fin de compte, déconseillées. question de Hello devient : quantité savoir sur vos besoins aujourd'hui, et elles resteront en hello futures ? Par exemple, supposons que vous créez une application de création de rapports pour un service. Vous êtes certain que l’application hello reste étendue hello de votre entreprise et que les rapports de hello sont courtes. Votre choix de l’approche est différente, par exemple, la création d’un service qui fournit des tootens de contenu vidéo de millions de clients. 

Mise en route de la porte de hello quelque chose comme preuve de concept est parfois un facteur déterminant hello, alors que vous savez qu’application hello peut être modifiée ultérieurement. Il n’est pas très pertinent de lancer une ingénierie complexe pour quelque chose qui ne sera jamais utilisé. Il s’agit de compromis d’ingénierie habituel hello. Sur hello autre part, lorsque les sociétés parler de construction pour hello cloud, les attentes hello est de croissance et de l’utilisation. problème de Hello est que la croissance et mise à l’échelle sont imprévisibles. Nous aimerions tooprototype en mesure de toobe rapidement tout en également sachant qu’il s’agit d’un toodeal de chemin d’accès avec succès futurs. Cette approche de démarrage lean hello est : build, de mesures, en savoir plus et effectuer une itération.

Au cours de l’ère du client-serveur hello, nous révélé toofocus sur la création d’applications à plusieurs niveaux à l’aide des technologies spécifiques dans chaque couche. terme de Hello *monolithique* application a vu le jour de ces approches. les interfaces Hello révélé toobe entre les couches de hello et une conception plus étroitement couplée a été utilisée entre les composants de chaque couche. Les développeurs concevaient et factorisaient des classes compilées dans des bibliothèques et liaient celles-ci dans quelques fichiers exécutables et DLL. 

Voici les avantages toosuch une approche de conception monolithique. Il est souvent toodesign plus simple, et il a des appels plus rapides entre les composants, étant donné que ces appels sont souvent sur la communication entre processus (IPC). En outre, tout le monde teste un produit unique, ce qui tend à toobe plusieurs personnes-gourmandes en ressources. inconvénient de Hello est qu’il existe un couplage étroit entre les couches à plusieurs niveaux, et vous ne pouvez pas mettre à l’échelle des composants individuels. Si vous devez tooperform correctifs ou mises à niveau, vous avez toowait pour d’autres toofinish leur test. Il est plus difficile toobe agile.

Microservices adresse ces inconvénients et plus adaptés à hello précédant les besoins de l’entreprise, mais ils possèdent également des avantages et inconvénients. les avantages de Hello des microservices sont que chacun d’eux généralement encapsule les fonctionnalités d’entreprise plus simple, qui vous mettre à l’échelle vers le haut ou vers le bas, test, déployez et gérez de manière indépendante. Un avantage important d’une approche de microservice est que les équipes sont dues à plusieurs scénarios d’entreprise à la technologie qui hello hiérarchisé approche encourage. Dans la pratique, de plus petites équipes développent un microservice en s’appuyant sur un scénario client et utilisent les technologies de leur choix. 

En d’autres termes, organisation de hello n’a pas besoin d’applications de microservice toomaintain toostandardize technique. Équipes individuelles propres services faire ce que qui leur convient en fonction de l’expérience de l’équipe ou problème de hello toosolve plus approprié. Dans la pratique, il est préférable de disposer d’un ensemble de technologies recommandées, par exemple d’un magasin NoSQL particulier ou d’une infrastructure d’application web.

inconvénient Hello de microservices est fourni dans la gestion de nombre hello augmenté des entités distinctes et de gérer le contrôle de version et des déploiements plus complexes. Le trafic réseau entre hello microservices augmente, ainsi que les latences réseau correspondante hello. Disposer d’un grand nombre de services granulaires et bavards est la recette idéale pour des performances cauchemardesques. Sans outils toohelp afficher ces dépendances, il est difficile trop « voir » le système dans son ensemble hello. 

Normes qu’approche de microservice hello fonctionne acceptant du comportement toocommunicate et en cours à tolérance de panne de choses de hello uniquement à partir d’un service, plutôt que les contrats rigides. Il est important toodefine ces contrats au préalable Bonjour de conception, car les services de mise à jour indépendamment les uns des autres. Une autre description a été formulée pour la conception avec une approche de microservices : « la SOA affinée ».

***Dans le bloc-notes, hello approche de conception microservices est sur une fédération découplée de services pour la communication avec les modifications indépendantes apportées tooeach et respect des normes.***

Que plusieurs applications de cloud sont produites, les personnes découvrez que cette décomposition de hello globale application dans les services indépendants, axée sur le scénario est une approche mieux à long terme.

## <a name="comparison-between-application-development-approaches"></a>Comparaison entre les approches de développement des applications
![Développement d’applications pour la plateforme Service Fabric][Image1]

1) Une application monolithique contient des fonctionnalités propres à un domaine. Elle est normalement divisée en couches fonctionnelles telles que web, métier et données.

2) Vous mettez à l’échelle une application monolithique en la clonant sur plusieurs serveurs/machines virtuelles/conteneurs.

3) Une application de microservices sépare les fonctionnalités en services plus petits distincts.

4) Hello échelles d’approche microservices arrière en déployant chaque service indépendamment, créer des instances de ces services sur plusieurs ordinateurs virtuels ou de serveurs/conteneurs.

Conception d’un microservice approche n’est pas une panacée pour tous les projets, mais elle n’est alignée plus étroitement avec des objectifs commerciaux hello décrits précédemment. En commençant par une approche monolithique peut être acceptable si vous savez que vous devez le code de hello hello opportunité toorework ultérieurement dans une conception microservices. En général, vous commencez par une application monolithique et lentement décomposez-la en étapes, en commençant par les zones fonctionnelles hello nécessitant toobe plus évolutif ou agile.

toosummarize, hello microservice consiste toocompose votre application de nombreux services petits. services de Hello s’exécutent dans des conteneurs qui sont déployés sur un cluster d’ordinateurs. Plus petites équipes développement un service qui met l’accent sur un scénario et indépendamment de test, version, déploiement et mettre à l’échelle de chaque service afin que l’ensemble de l’application hello peut évoluer.

## <a name="what-is-a-microservice"></a>Que sont les microservices ?
Il existe plusieurs définitions du terme « microservice ». Si vous recherchez hello Internet, vous trouverez de nombreuses ressources utiles qui fournissent leurs propres points de vue et les définitions. Toutefois, la plupart des hello suivant les caractéristiques des microservices est largement convenue :

* Ils encapsulent un scénario client ou d’entreprise. Qu’est le problème hello à résoudre ?
* Ils sont développés par une petite équipe d’ingénierie.
* Ils peuvent être écrits dans tout langage de programmation et utiliser toute infrastructure.
* Ils se composent d’un code et éventuellement d’un état, gérés indépendamment en termes de contrôle des versions, de déploiement et de mise à l’échelle.
* Ils interagissent avec les autres microservices sur des interfaces et protocoles bien définis.
* Ont des noms uniques (URL) utilisées tooresolve leur emplacement.
* Restent cohérents et disponibles en présence de hello d’échecs.

Vous pouvez résumer ces caractéristiques par :

***Les applications de microservice sont composées de services d’envergure modeste, évolutifs, dont les versions sont gérées indépendamment et qui communiquent entre eux via des protocoles standard avec des interfaces bien définies.***

Nous avons abordé les deux premiers points de hello Bonjour précédant la section et maintenant nous développer et à clarifier hello d’autres.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Ils peuvent être écrits dans tout langage de programmation et utiliser toute infrastructure
En tant que développeurs, nous devons être libre toochoose une langue ou un framework que nous souhaitons, en fonction de nos besoins hello du service de hello ou de compétences. Dans certains services, vous pourrez valeur des gains de performance hello de C++ au-dessus de tous les autres. Dans d’autres services, facilité de hello de développement de code managé en c# ou Java peut être plus importante. Dans certains cas, vous devrez peut-être toouse une bibliothèque de partenaire, technologie de stockage de données, ou les moyens d’exposition hello tooclients de service.

Une fois que vous avez choisi une technologie, vous accédez toohello opérationnel ou la gestion du cycle de vie et la mise à l’échelle du service de hello.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Permet de toobe de code et l’état indépendamment avec version, déployé et à l’échelle
Toutefois vous choisissez toowrite votre microservices, code de hello et éventuellement hello état doit indépendamment déployer, mettre à niveau et mettre à l’échelle. Il s’agit réellement d'entre hello plus difficile toosolve de problèmes, car elle provient bas tooyour les choix des technologies. Mise à l’échelle, il est difficile de comprendre comment toopartition (ou partition) à la fois hello code et l’état. Lorsque du code de hello et état utilisent des technologies distinctes, qui est commune aujourd'hui, les scripts de déploiement hello pour votre microservice doivent toobe toocope en mesure de mise à l’échelle les deux. Il s’agit également sur la souplesse et une flexibilité, donc vous pouvez mettre à niveau certaines hello microservices sans avoir tooupgrade tous à la fois.

Retournant toohello monolithiques et microservice approche pour un instant, hello diagramme suivant illustre les différences de hello dans l’état de toostoring approche hello.

#### <a name="state-storage-between-application-styles"></a>Stockage de l’état entre les styles d’application
![Stockage de l’état de la plateforme Service Fabric][Image2]

***approche monolithique Hello hello gauche possède une seule base de données et les niveaux des technologies spécifiques.***

***approche de microservices Hello sur hello droite a un graphique de microservices interconnectés où l’état est généralement consacré toohello microservice et différentes technologies sont utilisées.***

Dans une approche monolithique, application hello utilise généralement une base de données. Hello avantage qu’il s’agit d’un emplacement unique, ce qui la rend facile toodeploy. Chaque composant peut avoir une seule table toostore son état. Les équipes doivent toostrictly état distinct, qui est un défi. Inévitablement des temptations tooadd une nouvelle table de clients existants colonne tooan, faire une jointure entre les tables et créer des dépendances au niveau de la couche de stockage hello. Une fois cela effectué, vous ne pouvez pas mettre à l’échelle les composants individuels. 

Dans l’approche de microservices hello, chaque service gère et stocke son propre état. Chaque service est responsable de la mise à l’échelle des demandes de hello toomeet ensemble code et état du service de hello. Un inconvénient est que lorsqu’il existe un toocreate besoin de vues ou des requêtes, des données de votre application, vous devez tooquery dans les magasins état disparates. En règle générale, vous pouvez résoudre ce problème en disposant d’un microservice séparé qui génère une vue sur une collection de microservices. Si vous devez tooperform plusieurs requêtes impromptus sur les données de salutation, chaque microservice doit-elle envisager d’écrire son service d’entrepôt de données tooa de données pour l’analytique en mode hors connexion.

Contrôle de version est la version spécifique toohello déployé d’un microservice ainsi que plusieurs versions différentes, déployer et exécuter côte à côte. Le contrôle de version répond à des scénarios de hello où une version plus récente d’un microservice échoue au cours de la mise à niveau et doit tooan arrière de tooroll version antérieure. Hello autre scénario de contrôle de version effectue A/B-style de test, où les différents utilisateurs rencontrent différentes versions de service de hello. Par exemple, il est commun tooupgrade un microservice pour un ensemble spécifique de nouvelles fonctionnalités de clients tootest avant de le déployer plus largement. Après un cycle de vie de la gestion de microservices, cela maintenant nous amène toocommunication entre eux.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Ils interagissent avec les autres microservices sur des interfaces et protocoles bien définis
Cette rubrique doit peu d’attention ici, car une documentation complète sur l’architecture orientée services qui a été publié sur hello 10 dernières années décrit les modèles de communication. En règle générale, communication avec le service utilise une approche REST avec les protocoles HTTP et TCP et XML ou JSON en tant que format de sérialisation hello. Il s’agit du point de vue de l’interface, adopter l’approche de conception web hello. Toutefois, rien ne vous empêche d’utiliser des protocoles binaires ou vos propres formats de données. Attendez-vous à des personnes toohave fois plus difficile à l’aide de votre microservices s’ils sont ouvertement disponibles.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Un nom unique (URL) a utilisé tooresolve son emplacement
N’oubliez pas la façon dont nous utiliserons indiquant que hello microservice consiste comme hello web ? Comme hello web, votre microservice doit toobe adressable partout où il est en cours d’exécution. Si vous pensez à des machines et à celles qui exécutent un microservice spécifique, les choses tournent mal rapidement. 

Bonjour même façon que DNS résout un ordinateur particulier du tooa URL spécifique, votre microservice doit toohave un nom unique afin que son emplacement actuel est détectable. Microservices nécessitent un nom adressable qui les rendre indépendante de l’infrastructure hello qui s’exécutent sur. Cela implique qu’il existe une interaction entre la façon dont votre service est déployé et comment il est découvert, car il doit y toobe un Registre de service. De même, lorsqu’un ordinateur tombe en panne, service de Registre hello doit indiquent où le service de hello est en cours d’exécution. 

Cela nous amène la rubrique suivante de toohello : résilience et la cohérence.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Reste cohérent et disponible en présence de hello d’échecs
Traitement des erreurs inattendues est un des hello plus difficile toosolve de problèmes, en particulier dans un système distribué. Une grande partie du code hello que nous écrire en tant que développeurs est la gestion des exceptions, et il s’agit également répartition hello la plupart du temps passé dans le test. problème de Hello est plus complexe que l’écriture de code toohandle échecs. Que se passe-t-il en cas d’échec de l’ordinateur hello où hello microservice est en cours d’exécution ? Non seulement vous devez toodetect cet échec microservice (un problème sur son propre), mais vous devez également quelque chose toorestart votre microservice. 

Un microservice doit toofailures résilient de toobe et redémarrez souvent sur un autre ordinateur pour des raisons de disponibilité. Cela est également fourni état toohello qui a été enregistré pour le compte hello microservice, où hello microservice peut récupérer cet état à partir de, et si hello microservice est en mesure de toorestart avec succès. En d’autres termes, il doit y résilience toobe dans le calcul de hello (redémarrages du processus de hello), ainsi que la résilience d’état de hello ou de données (aucune donnée de hello et de perte de données ne reste cohérente).

problèmes de Hello de résilience sont aggravés durant les autres scénarios, tels que lorsque les échecs de se produire pendant une mise à niveau de l’application. Hello microservice, utilisation de système de déploiement hello, n’a pas besoin toorecover. Il doit également toothen décider s’il peut continuer la version plus récente de toomove toohello vers l’avant ou à la place restaurer tooa précédente version toomaintain un état cohérent. Questions telles que si suffisamment d’ordinateurs est disponible tookeep progresser et comment toorecover les versions précédentes de hello microservice doivent toobe considéré comme. Cela nécessite hello microservice tooemit d’intégrité informations toobe en mesure de toomake ces décisions.

### <a name="reports-health-and-diagnostics"></a>Rapports d’intégrité et diagnostics
Cela peut paraître évident, et c’est souvent négligé, mais un microservice doit générer des rapports sur son intégrité et ses diagnostics. Dans le cas contraire, les connaissances d’un point de vue opérationnel sont limitées. Mise en corrélation des événements de diagnostic sur un ensemble de services indépendants et traitement des décalages d’horloge machine toomake les sens de l’ordre des événements hello sont complexe. Bonjour formats de la même manière que vous interagissez avec un microservice dans convenu de protocoles et des données, il ressort nécessité d’une standardisation dans comment stockent des toolog intégrité et les événements de diagnostic qui finissent dans un événement pour l’interrogation et affichage. Dans une approche de microservices, il est essentiel que les différentes équipes soient d’accord sur un format de journalisation unique. Il doit y toobe une approche cohérente tooviewing des événements de diagnostic dans l’application hello dans son ensemble.

L’intégrité diffère des diagnostics. Contrôle d’intégrité est sur microservice hello ses actions appropriées du tootake état en cours de création de rapports. Un bon exemple fonctionne avec un déploiement et mise à niveau de disponibilité toomaintain mécanismes. Bien qu’un service peut être actuellement défectueux en raison de l’arrêt de processus tooa ou redémarrage de l’ordinateur, hello service peut encore être opérationnelle. Vous devez absolument Hello est toomake cette pire en effectuant une mise à niveau. meilleure Hello est toodo une enquête en premier ou attendez hello microservice toorecover. Les événements d’intégrité d’un microservice nous aident à prendre des décisions avisées et nous aident effectivement à créer des services de réparation spontanée.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric en tant que plateforme de microservices
Azure Service Fabric apparus à partir d’une transition par Microsoft à partir de proposant des produits de zone, qui ont été généralement monolithiques dans le style, toodelivering services. expérience de Hello de génération et d’exploitation de services de grande taille, telles que la base de données SQL Azure et base de données Azure Cosmos, en forme de l’infrastructure de Service. plateforme de Hello a évolué au fil du temps comme services plus adopté. Surtout, Service Fabric avait toorun non seulement dans Azure, mais également dans les déploiements de Windows Server autonome.

***objectif Hello de Service Fabric est toosolve hello des problèmes de création et l’exécution d’un service et utiliser des ressources d’infrastructure efficacement, afin que les équipes de résoudre les problèmes d’entreprise à l’aide d’une approche de microservices.***

Service Fabric fournit trois toohelp de grands domaines vous générez des applications qui utilisent une approche de microservices :

* Une plateforme qui fournit le système toodeploy de services, mise à niveau, détecter, redémarrez les services ayant échouées, détection de services, router des messages, gérer l’état et surveiller l’intégrité. Ces services système permettent en effet bon nombre des caractéristiques hello de microservices décrit précédemment.
* Applications toodeploy de capacité soit en cours d’exécution dans des conteneurs ou en tant que processus. Service Fabric est un conteneur et orchestrateur de processus.
* API de programmation productifs, toohelp vous générez des applications en tant que microservices : [ASP.NET Core, Reliable Actors et des Services fiables](service-fabric-choose-framework.md). Vous pouvez choisir n’importe quel toobuild code votre microservice. Mais ces API rendre hello plus simple, et ils s’intégrer à la plate-forme hello à un niveau inférieur. Ainsi, par exemple, vous pouvez obtenir des informations d’intégrité et des diagnostics, ou vous pouvez tirer parti de la haute disponibilité intégrée.

***Service Fabric est indifférent à la façon dont vous créez votre service. Vous pouvez utiliser la technologie de votre choix. Toutefois, il fournit des API de programmation intégrés qui le rendent plus facile toobuild microservices.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migration tooService d’applications existant Fabric
Un tooService approche clé Fabric est tooreuse code existant, qui peut ensuite être modernisé avec microservices de nouveau. Il existe cinq étapes tooapplication modernisation, et vous pouvez démarrer et arrêter à une des étapes de hello. Ces composants sont les suivants :

1) Prenez une application monolithique classique
2) De courbes d’élévation et MAJ - utiliser des conteneurs ou code d’invité exécutables toohost existant dans l’infrastructure de Service.
3) Modernisation - Ajout de nouveaux microservices en plus du code en conteneur existant. 
4) Innovation - pénétrer hello monolithique microservices exclusivement en fonction des besoins.
5) Transformé en microservices - transformation hello monolithiques applications existantes ou la création de nouvelles applications greenfield.

![TooMicroservices de migration][Image3]

Il est important tooemphasis là encore, vous pouvez **démarrer et arrêter à un de ces étapes**, vous n’êtes pas contraint toomoved toohello prochaine étape. Passons maintenant aux exemples de chacune de ces étapes.

**Déplacer** - grand nombre d’entreprises est délibéré et décalage applications monolithiques existantes dans les conteneurs toofor deux raisons ;

- Réduction des coûts en raison de tooconsolidation et de la suppression des applications existantes sur le matériel ou en cours d’exécution à une densité plus élevée. 
- Un contrat de déploiement cohérent entre le développement et les opérations.

Réduction des coûts est faciles à comprendre et au sein de Microsoft grand nombre d’applications existantes est placées dans des conteneurs simplement toomillions de dollars. Un déploiement cohérent est tooevaluate plus difficile, mais tout aussi importantes. Il indique que les développeurs peuvent toujours être toochoose libre hello technologie qui convient le mieux les, toutefois, les opérations hello uniquement acceptera une toodeploy de façon unique et gérer ces applications. Cela diminue opérations hello de ne pas avoir de toodeal complexité hello de nombreuses technologies différentes, ou forcer les développeurs tooonly choisir certains d'entre eux. En principe, chaque application est placée dans des images de déploiement autonomes.

De nombreuses organisations ne vont pas plus loin. Ils disposent déjà des avantages hello de conteneurs et Service Fabric fournit l’expérience de gestion complète hello de déploiement, les mises à niveau, le contrôle de version, annulations, etc. de contrôle d’intégrité.

**Modernisation** -hello est de nouveaux services en même temps que le code en conteneur existant. Si vous vous apprêtez toowrite nouveau code, il est meilleure toodecide tootake petites étapes vers le bas le chemin d’accès de hello microservices. Cela peut consister dans l’ajout d’un nouveau point de terminaison d’API REST ou d’une nouvelle logique métier. De cette manière, vous démarrez sur le trajet hello de microservices de nouvelle génération et des pratiques de développement et de les déployer.

**Innovation** -n’oubliez pas ces d’origine évolution des besoins professionnels au début de hello de cet article, qui engendrent une approche de microservices hello ? Hello de cette étape est la décision, ceux-ci sont se produise à toomy l’application en cours et dans ce cas, je dois toostart fractionnement monolithique de hello ou innovation. Le présent exemple consiste en une base de données devenant un goulot d’étranglement de traitement depuis son utilisation comme file d’attente de workflow. En tant que nombre hello du flux de travail hello l’augmentation des demandes de travail toobe besoins distribué pour la mise à l’échelle. Afin d’obtenir cette portion de l’application hello qui n’est pas mise à l’échelle ou vous tooupdate plus fréquemment, cela les fractionnement en un microservice et innovation. 

**Transformation en microservices** : il s’agit de l’étape lors de laquelle l’application est entièrement composée (ou décomposée) en microservices. tooreach ici, vous avez effectué le parcours de microservices hello. Vous pouvez démarrer ici, mais toodo cela sans un toohelp de plateforme microservices vous est un investissement important. 

### <a name="are-microservices-right-for-my-application"></a>Les microservices conviennent-ils à mon application ?
Peut-être. Ce que nous avons rencontré était que comme plus en plus d’équipes dans Microsoft a commencé à toobuild pour cloud hello pour des raisons professionnelles, bon nombre d'entre elles réalisé avantages hello d’une approche microservice. Bing, par exemple, développe des microservices dans le domaine de la recherche depuis des années. Pour les autres équipes, l’approche de microservices hello était nouvelle. Les équipes trouvé qu’il existait toosolve des problèmes en dehors de leurs domaines de noyaux de force. C’est pourquoi le Service Fabric acquise traction en tant que technologie hello de choix pour la création de services.

Hello Service Fabric vise complexités de hello tooreduce de création d’applications avec une approche microservice, afin que vous n’avez pas toogo via en tant que nombre coûteux redesigns. Commencez petit, à l’échelle lorsque nécessaire, déconseiller des services, ajouter de nouveaux et faire évoluer avec le client, l’utilisation est approche de hello. Nous savons également qu’il n’y a de nombreux autres problèmes encore toobe résolu microservices toomake plus abordable pour la plupart des développeurs. Conteneurs et le modèle de programmation intervenant hello sont des exemples de petites étapes dans cette direction, et garantir que plusieurs innovations vont apparaître toomake cela plus facile.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Étapes suivantes
* [Présentation de la terminologie Service Fabric](service-fabric-technical-overview.md)
* [Microservices : Revolution une application par le cloud de hello](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
