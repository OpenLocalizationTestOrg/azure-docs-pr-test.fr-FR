---
title: "Architecture de sécurité d’aaaIoT | Documents Microsoft"
description: "Considérations et recommandations relatives à l’architecture de sécurité IoT"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>Architecture de sécurité de l’Internet des objets
Lorsque vous concevez un système, il est important toounderstand les menaces potentielles hello toothat système et ajouter les défenses en conséquence, comme système de hello est conçu et mise en œuvre. Il est particulièrement important toodesign hello produit à partir du début de hello avec la sécurité à l’esprit, car vous assurer que les solutions d’atténuation appropriées sont en place à partir du début de hello permet de comprendre comment un intrus peut être en mesure de toocompromise un système. 

## <a name="security-starts-with-a-threat-model"></a>La sécurité commence par un modèle de menace
Microsoft a utilisé durée pendant laquelle les modèles de menace pour ses produits et a effectué des processus disponibles publiquement de modélisation des menaces de la société hello. Hello expérience d’entreprise montre que la modélisation hello a des avantages inattendus au-delà de hello immédiate de comprendre quelles sont les menaces sont hello concernant la plupart des. Par exemple, il crée également d’accès pour un débat avec d’autres utilisateurs en dehors de l’équipe de développement hello, qui peut provoquer une toonew idées et des améliorations dans les produits hello.

objectif de Hello de modélisation des menaces est toounderstand comment un intrus peut être en mesure de toocompromise un système et puis assurez-vous que les solutions d’atténuation appropriées sont en place. Modélisation des menaces force les solutions d’atténuation hello conception équipe tooconsider comme système de hello est conçu et non après le déployée d’un système. Cela est extrêmement important, car rattrapage sécurité défenses tooa large éventail de périphériques dans le champ de hello est irréalisable, sujette aux erreurs et laisse les clients exposés.

De nombreuses équipes de développement faire un excellent travail capture hello fonctionnel pour le système de hello qui tirent profit des clients. Toutefois, l’identification des méthodes non évidente que quelqu'un peut utilisation malveillante de système de hello est plus complexe. La modélisation des menaces peut aider les équipes de développement à comprendre ce qu’une personne malveillante peut effectuer et pourquoi. Modélisation des menaces est un processus structuré qui crée une discussion sur la sécurité de hello décisions de conception dans le système de hello, ainsi que la conception toohello modifications effectuées tout au long des processus hello ayant un impact sur la sécurité. Alors qu’un modèle de menace est simplement un document, cette documentation représente également une façon idéale de continuité des activités tooensure des connaissances, la conservation des leçons apprises et aider à intégrer la nouvelle équipe rapidement. Enfin, un résultat de la modélisation des menaces est tooenable vous tooconsider autres aspects de la sécurité, telles que les engagements de sécurité vous souhaitez tooprovide tooyour clients. Ces engagements pris conjointement avec la modélisation des menaces documentent et orientent les tests de votre solution IoT.

### <a name="when-toothreat-model"></a>Lorsque le modèle de toothreat
[Modélisation des menaces](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) offres hello plus grande valeur si elle est incorporée dans la phase de conception hello. Lors de la conception, vous avez hello plus grande flexibilité toomake modifications tooeliminate menaces. Éliminer les menaces de par sa conception est résultat souhaité de hello. C’est en effet bien plus facile que d’ajouter des préventions, les tester et s’assurer qu’elles restent en cours. Par ailleurs, procéder à de telles éliminations n’est pas toujours possible. Il devient plus difficile tooeliminate menaces comme un produit devenait plus adultes et à son tour finalement nécessite davantage de travail et les compromis beaucoup plus difficiles à très tôt dans le développement de hello de modélisation des menaces.

### <a name="what-toothreat-model"></a>Quel modèle toothreat
Vous devez thread solution hello de modèle comme un entier et également le focus Bonjour suivant des zones :

* fonctionnalités de sécurité et confidentialité Hello
* fonctions Hello dont les échecs sont concernant la sécurité
* fonctions Hello qui touchent une limite d’approbation 

### <a name="who-threat-models"></a>Qui doit réaliser le modèle de menace
La modélisation des menaces est un processus comme un autre.  Il est un bonne idée tootreat hello menace document comme tout autre composant de solution de hello et le valider. De nombreuses équipes de développement faire un excellent travail capture hello fonctionnel pour le système de hello qui tirent profit des clients. Toutefois, l’identification des méthodes non évidente que quelqu'un peut utilisation malveillante de système de hello est plus complexe. La modélisation des menaces peut aider les équipes de développement à comprendre ce qu’une personne malveillante peut effectuer et pourquoi.

### <a name="how-toothreat-model"></a>Comment toothreat modèle
processus de modélisation des menaces Hello sont composé de quatre étapes ; étapes de Hello sont :

* Application hello modèle
* Énumérer les menaces
* Prévenir les menaces
* Valider les solutions d’atténuation hello

#### <a name="hello-process-steps"></a>étapes du processus Hello
Tookeep trois règles générales à l’esprit lors de la création d’un modèle de menaces :

1. Créez un diagramme de l’architecture de référence. 
2. Commencez par la logique de largeur. Obtenir une vue d’ensemble et comprendre le système de hello dans son ensemble, avant d’examiner en profondeur.  Cette permet de garantir que vous approfondie Bonjour droite place.
3. Lecteur de processus de hello, ne laissez pas les processus hello lecteur vous. Si vous détectez un problème dans la phase de modélisation de hello et que vous souhaitez tooexplore il accédez pour qu’il !  Ne vous sentez pas besoin de toofollow ces étapes aveuglément.  

#### <a name="threats"></a>Menaces
Hello quatre principaux éléments d’un modèle de menace sont :

* Processus (services web, services Win32, démons *nix, etc.) Notez que certaines entités complexes (comme les passerelles et capteurs sur site) peuvent être résumées sous la forme d’un processus lorsque l’exploration technique de ces zones n’est pas possible.
* Magasins de données (tout emplacement de stockage des données, par exemple un fichier de configuration ou une base de données)
* Flux de données (où elles se déplacent entre les autres éléments dans une application hello)
* Les entités externes (tout ce qui interagit avec le système de hello, mais n’est pas sous contrôle de code hello de l’application hello, exemples incluent les utilisateurs et satellite flux)

Tous les éléments dans le diagramme architectural de hello sont les menaces toovarious sujet ; Nous allons utiliser mnémonique STRIDE hello. Lecture [menace pour la modélisation, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow plus d’informations sur les éléments STRIDE hello.

Différents éléments du diagramme d’application hello sont les menaces STRIDE toocertain sujet :

* Les processus sont tooSTRIDE d’objet
* Flux de données sont tooTID d’objet
* Banques de données sont tooTID de l’objet et parfois R, si les magasins de données hello sont des fichiers journaux.
* Les entités externes sont tooSRD d’objet

## <a name="security-in-iot"></a>Sécurité des solutions IoT
Les appareils connectés spécial contenant un nombre important de potentiels surface interaction et les modèles d’interaction, de prendre en considération tooprovide une infrastructure pour sécuriser l’accès numérique toothose périphériques. le terme Hello « accès numérique » est utilisé toodistinguish ici à partir de toutes les opérations sont effectuées via une interaction directe des périphériques où la sécurité d’accès est fournie via le contrôle d’accès physique. Par exemple, placer les appareil hello dans une salle avec un verrou sur la porte de hello. Lors de l’accès physique ne peut pas être refusée à l’aide de logiciels et matériels, pouvez mesures tooprevent l’accès physique à partir du début toosystem interférence. 

Comme nous Explorer les modèles d’interaction hello, nous allons nous intéresser à « contrôle de l’appareil » et « données de périphérique » avec hello même niveau d’attention. « Contrôle de l’appareil » peut être classé en tant que toutes les informations fournies tooa périphérique par un tiers avec comme objectif hello modification ou influencent son comportement vers son état ou hello de son environnement. « Données de l’appareil » peuvent être classées en tant que toutes les informations qu’un appareil émet tooany autre partie sur son état et son hello observé l’état de son environnement.

Dans l’ordre toooptimize meilleures pratiques de sécurité, il est recommandé qu’une architecture IoT standard être divisé en plusieurs zones/de composant dans le cadre de l’exercice de modélisation des menaces hello. Ces zones sont décrites en détail dans cette section et incluent les éléments suivants :

* périphérique,
* passerelle de champ,
* passerelles cloud,
* prenant en charge les revendications.

Les zones sont large toosegment de façon une solution. souvent, chaque zone possède ses propres exigences de données et d’authentification et d’autorisation. Les zones peuvent être également utilisée tooisolation endommager et limiter l’impact de hello des zones de confiance faible sur les zones de confiance plus élevés.

Chaque zone est séparé par une limite d’approbation, qui est indiqué comme hello pointillés ligne rouge dans le diagramme hello ci-dessous. Il représente une transition de données / d’informations à partir d’une source tooanother. Au cours de cette transition, hello/de données peut être sujet tooSpoofing, falsification, répudiation, divulgation d’informations, déni de Service et élévation de privilèges (STRIDE).

![Zones de sécurité IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Hello composants mentionnés dans chaque limite sont également soumis tooSTRIDE, l’activation d’un 360 complète la vue de la solution de hello de modélisation des menaces. élaborent des sections Hello ci-dessous sur chacun des composants de hello et les problèmes de sécurité spécifiques et les solutions qui doivent être mises en place.

les sections Hello qui suivent traite des composants standard que se trouvés généralement dans ces zones.

### <a name="hello-device-zone"></a>Hello Zone d’appareil
environnement des appareils Hello est un espace physique immédiate hello autour de périphérique hello sur lesquels l’accès physique et/ou numérique pair à pair de « réseau local » aux toohello appareil n’est possible. Un « réseau local » est supposé toobe un réseau distinct et isolé – mais potentiellement liés Internet public de trop : hello, et inclut une technologie de radio sans fil à courte portée qui permet la communication pair à pair de périphériques. Il effectue *pas* inclure n’importe quel illusion hello tel un réseau local de création de la technologie de virtualisation de réseau et également pas les réseaux opérateur public qui nécessitent des toocommunicate deux périphériques sur espace d’un réseau public s’il s’agissait de relation de communication tooenter égal à égal.

### <a name="hello-field-gateway-zone"></a>Hello Zone de champ de passerelle
Une passerelle de champ est un périphérique/équipement ou un logiciel serveur à usage général qui agit en tant qu’activateur de communication, mais elle peut également servir de système de contrôle de périphérique et de concentrateur de traitement des données du périphérique. zone de passerelle du champ Hello inclut la passerelle de champ hello elle-même et tous les périphériques qui sont attachés tooit. Hello nom l’indique, les passerelles de champ agissent de traitement des données en dehors de dédié, sont généralement emplacement lié, est potentiellement intrusion toophysical de sujet et redondance sera limitée. Tous les toosay qui a une passerelle de champ est en général une chose une peut toucher et saboter tout en sachant que sa fonction est. 

Une passerelle de champ diffère d’un routeur de trafic simple dans la mesure où il a un rôle actif dans la gestion de l’accès et du flux d’informations, ce qui signifie qu’il s’agit d’un terminal de session ou de connexion réseau et d’entité adressable d’application. En revanche, un périphérique NAT ou un pare-feu n’est pas qualifié de passerelle de champ, car il ne s’agit pas de terminaux de connexion ou de session. Ils acheminent (ou bloquent) les connexions ou les sessions qui transitent par eux. passerelle de champ Hello a deux zones de surface distinctes. Un fait face périphériques hello qui sont attaché tooit représente hello au sein de la zone de hello et hello autres fait face à toutes les parties externes est bord hello de zone de hello.   

### <a name="hello-cloud-gateway-zone"></a>zone de passerelle de cloud Hello
Passerelle de cloud est un système qui permet la communication à distance à partir d’et passerelles toodevices ou un champ à partir de plusieurs sites sur espace d’un réseau public, généralement à un nuage contrôle et données analyse système, une fédération de ces systèmes. Dans certains cas, une passerelle de cloud peut faciliter immédiatement d’usage toospecial accèdent aux appareils à partir de terminaux tels que les tablettes ou téléphones. Dans le contexte hello présenté ici, « cloud » vise toorefer tooa dédié le traitement des données système qui n’est pas lié toohello même site comme hello attaché appareils ou des passerelles du champ. Également dans une Zone de Cloud, les mesures opérationnelles empêchent un accès physique ciblé et infrastructure de « cloud public » tooa nécessairement exposé ne sont pas.  

Une passerelle de cloud peut potentiellement être associée à une passerelle de cloud de réseau virtualisation superposition tooinsulate hello et tous ses périphériques connectés ou des passerelles du champ à partir de tout autre trafic réseau. la passerelle de cloud Hello lui-même est ni un système de contrôle d’appareil, ni un traitement ou support de stockage des données de l’appareil ; Ces fonctionnalités de l’interface avec la passerelle de cloud hello. zone de passerelle de cloud Hello inclut la passerelle de cloud hello elle-même, ainsi que toutes les passerelles de champ et périphériques directement ou indirectement joint tooit. bord Hello de zone de hello est une surface d’exposition distinct dans lequel toutes les parties externes communiquent par l’intermédiaire.

### <a name="hello-services-zone"></a>zone des services Hello
Pour ce contexte, un « service » est défini comme un composant ou un module logiciel qui interface avec des périphériques via une passerelle de champ ou cloud pour la collecte et l’analyse des données, ainsi que pour la commande et le contrôle.  Les services sont des médiateurs. Ils agissent sous leur identité vers les passerelles et autres sous-systèmes, stocker et analysent les données, autonome problème commandes toodevices basé sur les analyses de données ou les planifications et exposer des informations et les utilisateurs finaux de contrôle des fonctionnalités tooauthorized.

### <a name="information-devices-vs-special-purpose-devices"></a>Appareils d’information et périphériques à usage spécifique
Les PC, les téléphones et les tablettes sont des appareils d’information essentiellement interactifs. Les téléphones et les tablettes sont explicitement optimisés via l’optimisation de la durée de vie de la batterie. Ils préférence désactivent partiellement lors de le n'interaction pas immédiatement avec une personne, ou lorsque aucun services tels que la lecture de musique ou de guidage leur propriétaire tooa les emplacement particulier. Du point de vue des systèmes, ces appareils de technologie de l’information font principalement office de proxy pour les personnes. Ce sont des « actionneurs » qui suggèrent des actions et des « capteurs » qui collectent des saisies. 

Les appareils à usage spécial, à partir des lignes de production température simple capteurs toocomplex fabrique avec des milliers de composants à l’intérieur, sont différents. Ces appareils sont beaucoup plus limités dans le but et même si elles fournissent une interface utilisateur, ils sont en grande partie étendue toointerfacing avec ou être intégrés dans les éléments multimédias dans Bonjour physique. Ils mesurent et signalent des conditions d’environnement, activent des vannes, contrôlent des servomécanismes, déclenchent des alarmes, allument des lumières et effectuent bien d’autres tâches. Ils aident toodo pour lequel un appareil d’informations est soit trop générique, trop coûteuses, trop grande ou trop fragile. effet concret de Hello dicte immédiatement leurs techniques de conception en tant que bien hello disponible monétaire budget pour leur production et le fonctionnement de la durée de vie prévue. combinaison de Hello de ces deux facteurs clés contraint hello disponible opérationnel allocation de réserve d’énergie, l’encombrement physique et donc un stockage disponible, de calcul et de fonctionnalités de sécurité.  

Si un élément « va incorrect » avec des périphériques contrôlables automatisées ou à distance, par exemple, défauts ou toowillful de défauts de logique de contrôle non autorisé des intrusions et manipulation. un grand nombre de production Hello risque d’être détruit, bâtiments peuvent être vidés ou gravés vers le bas et personnes peuvent être la victime ou même de matrice. Bien sûr, il s’agit là d’une classe de dommages totalement différente de ceux rencontrés par une personne atteignant le plafond d’une carte de crédit volée. déplacer Hello barre de sécurité pour les appareils qui rendent les choses, et également pour les données de capteur que par la suite les résultats dans les commandes qui provoquent des choses toomove, doit être supérieure dans n’importe quel scénario bancaire ou de commerce électronique. 

### <a name="device-control-and-device-data-interactions"></a>Interactions du contrôle de périphérique et des données de périphérique
Les appareils connectés spécial contenant un nombre important de potentiels surface interaction et les modèles d’interaction, de prendre en considération tooprovide une infrastructure pour sécuriser l’accès numérique toothose périphériques. le terme Hello « accès numérique » est utilisé toodistinguish ici à partir de toutes les opérations sont effectuées via une interaction directe des périphériques où la sécurité d’accès est fournie via le contrôle d’accès physique. Par exemple, placer les appareil hello dans une salle avec un verrou sur la porte de hello. Lors de l’accès physique ne peut pas être refusée à l’aide de logiciels et matériels, pouvez mesures tooprevent l’accès physique à partir du début toosystem interférence. 

Comme nous Explorer les modèles d’interaction hello, nous allons nous intéresser à « contrôle de l’appareil » et « données de périphérique » avec hello même niveau d’attention lors de la modélisation des menaces. « Contrôle de l’appareil » peut être classé en tant que toutes les informations fournies tooa périphérique par un tiers avec comme objectif hello modification ou influencent son comportement vers son état ou hello de son environnement. « Données de l’appareil » peuvent être classées en tant que toutes les informations qu’un appareil émet tooany autre partie sur son état et son hello observé l’état de son environnement. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Architecture de référence Azure IoT hello de modélisation des menaces
Microsoft utilise framework hello présentée ci-dessus pour Azure IoT de modélisation des menaces toodo. Dans la section hello ci-dessous, nous utilisons donc exemple concret hello toodemonstrate d’Architecture de référence Azure IoT comment toothink sur pour IoT et comment tooaddress hello menaces de modélisation des menaces identifiée. Dans notre cas, nous avons identifié quatre domaines principaux :

* Périphériques et sources de données
* Transport de données
* Périphérique et traitement des événements
* Présentation

![Modélisation des menaces pour Azure IoT](media/iot-security-architecture/iot-security-architecture-fig2.png) 

diagramme de Hello ci-dessous fournit une vue simplifiée de l’Architecture de Microsoft IoT à l’aide d’un modèle de diagramme de flux de données qui est utilisé par hello outil de modélisation de menace de Microsoft :

![Modélisation des menaces pour Azure IoT à l’aide de l’outil MS de modélisation des menaces](media/iot-security-architecture/iot-security-architecture-fig3.png)

Il est important de toonote qui hello architecture sépare les fonctionnalités de périphérique et passerelle hello. Cela permet des passerelles sont plus sécurisées hello utilisateur tooleverage : ils sont capables de communiquer avec la passerelle de cloud hello à l’aide des protocoles sécurisés, qui nécessite une plus grande charge de traitement qu’un périphérique natif - par exemple un thermostat - Impossible fournir sur son propre. Dans la zone des services Azure hello, nous supposons que hello que passerelle de Cloud est représentée par hello Azure IoT Hub service.

### <a name="device-and-data-sourcesdata-transport"></a>Périphériques et sources de données/transport de données
Cette section explore l’architecture hello présentée ci-dessus via thématique hello de modélisation des menaces et donne une vue d’ensemble de la façon dont nous corrigeons certains des problèmes inhérents de hello. Nous nous concentrerons sur hello principaux éléments d’un modèle de menace :

* Processus (ceux qui relèvent de notre contrôle et éléments externes)
* Communication (également appelée flux de données)
* Stockage (également appelé magasins de données)

#### <a name="processes"></a>Processus
Dans chacune des catégories de hello décrites Bonjour Azure IoT architecture, nous essayons toomitigate un nombre de menaces différentes entre les données de différentes étapes hello existe dans : processus, de communication et de stockage. Nous donner une vue d’ensemble de hello ci-dessous ceux qui sont plus courantes pour la catégorie « processus » de hello, suivi d’une vue d’ensemble de la manière dont ces pourraient être mieux atténuées : 

**L’usurpation d’identité (S)**: un intrus peut extraire le matériel de clé de chiffrement à partir d’un appareil, soit au niveau du logiciel ou matériel de hello et par la suite accéder au système de hello avec un autre périphérique physique ou virtuel sous l’identité hello Hello du périphérique hello le matériel de clé a été extraite. Les télécommandes qui peuvent allumer toutes les TV et qui sont des outils de plaisanterie populaires en sont une bonne illustration.

**Déni de service (D)** : un appareil peut être dans l’incapacité de fonctionner ou de communiquer en raison d’interférences avec des fréquences radio ou d’une rupture de câbles. Par exemple, une caméra de surveillance dont l’alimentation ou la connexion réseau ont été intentionnellement mises hors-service ne signalera pas de données du tout.

**Falsification (T)**: une personne malveillante peut partiellement ou totalement remplacer le logiciel hello en cours d’exécution sur l’appareil de hello, autorisant potentiellement hello remplacé logiciel tooleverage hello authentique identité du périphérique de hello si hello matériel de clé ou hello chiffrement installations contenant les principaux documents ont été programme illicite de toohello disponibles. Par exemple, une personne malveillante peut tirer parti des extraits de toointercept matériel clé et supprimer les données d’appareil hello sur voie de communication hello et remplace par false qui est authentifié avec le matériel de clé hello volé.

**Divulgation d’informations (I)**: si hello appareil exécute logiciel manipulé, ces logiciels manipulé pourrait potentiellement avoir une fuite des parties toounauthorized de données. Par exemple, une personne malveillante peut tirer parti des extrait clé matérielle tooinject lui-même en chemin d’accès de communication hello entre l’appareil de hello et une passerelle de contrôleur ou un champ ou toosiphon passerelle informations de cloud computing.

**Élévation de privilèges (E)**: un périphérique qui exécute la fonction spécifique peut être forcé toodo autre chose. Par exemple, une vanne est programmée tooopen moitié peut être complètement exécute tooopen tous hello moyen.

| **Composant** | **Menace** | **Atténuation** | **Risque** | **Implémentation** |
| --- | --- | --- | --- | --- |
| Appareil |S |Assignation d’équipement de toohello d’identité et l’authentification des appareils de hello |Périphérique ou partie d’un appareil de hello à remplacer par un autre périphérique. Comment savoir qu'impliquent toohello bon appareil ? |L’authentification des appareils hello, à l’aide de la sécurité TLS (Transport Layer) ou IPSec. L’infrastructure doit prendre en charge l’utilisation d’une clé prépartagée (PSK) sur les périphériques qui ne peuvent pas gérer le chiffrement asymétrique complet. Exploitation d’Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Appliquer appareil de toohello mécanismes inviolable par exemple en le rendant très difficile tooimpossible tooextract clés et autre matériel de chiffrement à partir de l’appareil de hello. |risque de Hello est si quelqu'un falsification constitue l’appareil hello (interférence physique). Comment être sûr de la non-falsification du périphérique ? |atténuation de la plus efficace de Hello est une fonctionnalité de module de plateforme sécurisée qui permet de stocker des clés dans un circuit de processeur spécial ne peut pas être lu à partir de quels hello clés, mais est utilisable uniquement pour les opérations de chiffrement qui utilisent la clé de hello mais jamais divulguent clé de hello . Chiffrement de la mémoire du périphérique de hello. Gestion de clés pour les appareils hello. Signature du code hello. | |
| E |Ayant le contrôle d’accès de périphérique de hello. Schéma d’autorisation. |Si le périphérique de hello autorise pour des actions individuelles toobe effectuées en fonction des commandes à partir d’une source externe, ou même compromis capteurs, il permet l’attaque de hello tooperform opérations accessible autrement. |Ayant le schéma d’autorisation pour appareil de hello | |
| Passerelle de champ |S |L’authentification hello champ passerelle tooCloud passerelle (basé de certificats, PSK, la demande de remboursement,...) |Si quelqu’un peut usurper l’identité de la passerelle de champ, elle peut alors se présenter comme un périphérique. |TLS RSA/PSK, IPSe, [RFC 4279](https://tools.ietf.org/html/rfc4279). Tous hello même stockage de clés et les problèmes de l’attestation de périphériques en général, le meilleur des cas est utiliser TPM. Extension 6LowPAN pour IPSec toosupport réseaux de capteur sans fil (WSN). |
| TRID |Protéger hello champ passerelle contre les altérations (sécurisée TPM) ? |Usurpation qui amener la passerelle de cloud hello penser qu’il parle toofield passerelle peut entraîner la divulgation d’informations et falsification de données |Chiffrement de la mémoire, module de plateforme sécurisée, authentification. | |
| E |Mécanisme de contrôle d’accès pour la passerelle de champ | | | |

Voici quelques exemples de menaces existant dans cette catégorie :

L’usurpation d’identité : Une personne malveillante peut extraire de matériel de clé de chiffrement à partir d’un appareil, soit au niveau logiciel ou matériel de hello et par la suite l’accès système hello avec un autre périphérique physique ou virtuel sous l’identité de hello hello appareil hello de matériel de clé a été extraite.

**Déni de service**  : un appareil peut être dans l’incapacité de fonctionner ou de communiquer en raison d’interférences avec des fréquences radio ou d’une rupture de câbles. Par exemple, une caméra de surveillance dont l’alimentation ou la connexion réseau ont été intentionnellement mises hors-service ne signalera pas de données du tout.

**Falsification**: une personne malveillante peut partiellement ou totalement remplacer le logiciel hello en cours d’exécution sur l’appareil de hello, autorisant potentiellement hello remplacé logiciel tooleverage hello authentique identité du périphérique de hello si hello matériel de clé ou hello chiffrement installations contenant les principaux documents ont été programme illicite de toohello disponibles.

**Falsification** : une caméra de surveillance qui affiche une image (en spectre visible) d’un couloir vide peut être forcée à afficher une photo de ce couloir. Un capteur de détection de fumée ou d’incendie peut signaler la présence d’une personne utilisant un briquet. Dans les deux cas, l’appareil hello soit techniquement entièrement fiable vers le système de hello, mais il va signaler ces informations manipulées.

**Falsification**: une personne malveillante peut tirer parti des extraits de toointercept matériel clé et supprimer des données à partir de l’appareil hello sur voie de communication hello et remplacez-le par données false qui sont authentifiées avec le matériel de clé hello volé.

**Falsification**: une personne malveillante peut partiellement ou totalement remplacer le logiciel hello en cours d’exécution sur l’appareil de hello, autorisant potentiellement hello remplacé logiciel tooleverage hello authentique identité du périphérique de hello si hello matériel de clé ou hello chiffrement installations contenant les principaux documents ont été programme illicite de toohello disponibles.

**Divulgation d’informations**: si hello appareil exécute logiciel manipulé, ces logiciels manipulé pourrait potentiellement avoir une fuite des parties toounauthorized de données.

**Divulgation d’informations**: une personne malveillante peut tirer parti des extrait clé matérielle tooinject lui-même en chemin d’accès de communication hello entre l’appareil de hello et une passerelle de contrôleur ou le champ ou toosiphon passerelle informations de cloud computing.

**Déni de Service**: appareil de hello peut être désactivée ou activée dans un mode dans lequel la communication n’est pas possible (qui est intentionnel de nombreuses machines industrielles).

**Falsification**: appareil de hello peut être reconfiguré toooperate dans un état inconnu toohello contrôle système (en dehors des paramètres d’étalonnage connus) et donc fournir des données qui peuvent être mal interprétées

**Élévation de privilège**: un périphérique qui exécute la fonction spécifique peut être forcé toodo autre chose. Par exemple, une vanne est programmée tooopen moitié peut être complètement exécute tooopen tous hello moyen.

**Déni de Service**: appareil de hello peut être activé dans un état où la communication n’est pas possible.

**Falsification**: appareil de hello peut être reconfiguré toooperate dans un état inconnu toohello contrôle système (en dehors des paramètres d’étalonnage connus) et donc fournir des données qui peuvent être mal interprétées.

**L’usurpation d’identité/falsification/répudiation**: si non sécurisés (ce qui est rarement hello cas avec le contrôle à distance de consommateur) une personne malveillante peut manipuler état hello d’un appareil anonymement. Les télécommandes qui peuvent allumer toutes les TV et qui sont des outils de plaisanterie populaires en sont une bonne illustration.

#### <a name="communication"></a>Communication
Menaces pesant sur le chemin de communication entre des périphériques, des passerelles de périphérique et de champ, et des passerelles de périphérique et cloud. tableau Hello ci-dessous présente quelques conseils autour de sockets ouverts sur le périphérique de hello/VPN :

| **Composant** | **Menace** | **Atténuation** | **Risque** | **Implémentation** |
| --- | --- | --- | --- | --- |
| IoT Hub de périphérique |TID |(D) Trafic de hello tooencrypt TLS (PSK/RSA) |Écoute ou interférer communication hello entre l’appareil de hello et passerelle de hello |Sécurité au niveau du protocole hello. Avec les protocoles personnalisés, nous devons toofigure comment tooprotect les. Dans la plupart des cas, les communications hello ont lieu à partir de hello appareil toohello IoT Hub (appareil établit la connexion de hello). |
| Périphérique Périphérique |TID |(D) Trafic de hello tooencrypt TLS (PSK/RSA). |Lecture des données en transit entre les périphériques. Falsification des données de hello. Surcharge d’appareil hello avec nouvelles connexions |Sécurité au niveau du protocole hello (MQTT/AMQP/HTTP/CoAP. Avec les protocoles personnalisés, nous devons toofigure comment tooprotect les. limitation des risques Hello pour hello menace de déni de service est toopeer pour les appareils via une passerelle de cloud ou un champ et demandez-lui d’act uniquement en tant que clients vers le réseau de hello. Hello d’homologation peut entraîner une connexion directe entre homologues hello après avoir été demandée par la passerelle de hello |
| Périphérique d’entité externe |TID |Fort de jumelage du périphérique de toohello hello entité externe |Périphérique toohello de la connexion hello écoute clandestine. Communication hello interférence avec les appareils hello |En toute sécurité d’associer hello entité externe toohello périphérique NFC/Bluetooth LE. Contrôle hello opérationnel Panneau de configuration de l’appareil hello (physique) |
| Passerelle de champ Passerelle cloud |TID |Trafic de hello tooencrypt TLS (PSK/RSA). |Écoute ou interférer communication hello entre l’appareil de hello et passerelle de hello |Sécurité au niveau du protocole hello (MQTT/AMQP/HTTP/CoAP). Avec les protocoles personnalisés, nous devons toofigure comment tooprotect les. |
| Passerelle cloud de périphérique |TID |Trafic de hello tooencrypt TLS (PSK/RSA). |Écoute ou interférer communication hello entre l’appareil de hello et passerelle de hello |Sécurité au niveau du protocole hello (MQTT/AMQP/HTTP/CoAP). Avec les protocoles personnalisés, nous devons toofigure comment tooprotect les. |

Voici quelques exemples de menaces existant dans cette catégorie :

**Déni de Service**: contraintes périphériques sont généralement sous la menace de déni de service lorsqu’ils écoutent activement pour les connexions entrantes ou non sollicité sur un réseau, car une personne malveillante peut ouvrir plusieurs connexions en parallèle et pas les traiter ou de service les très lentement ou hello périphérique peut être submergé le trafic non sollicité. Dans les deux cas, appareil de hello peut effectivement être rendu inutilisable sur le réseau de hello.

**L’usurpation d’identité, la divulgation d’informations**: appareils limitées et spécial ont souvent des fonctionnalités de sécurité d’une seule pour l’ensemble comme mot de passe ou de la protection de code confidentiel ou qu’elles dépendent entièrement confiance réseau hello, ce qui signifie que leur accorde l’accès tooinformation quand un appareil est sur hello même réseau et que ce réseau est souvent uniquement protégé par une clé partagée. Cela signifie que lorsque hello partagé toodevice secrète ou réseau est indiqué, il est possible toocontrol hello périphérique ou observer les données émises à partir de l’appareil de hello.  

**L’usurpation d’identité**: un intrus peut intercepter ou partiellement remplacer hello diffusion et l’usurpation d’identité hello donneur d’ordre (l’homme hello milieu)

**Falsification**: un intrus peut intercepter ou partiellement remplacer hello diffusion et envoyer de fausses informations 

**Divulgation d’informations :** une personne malveillante peut espionner une diffusion et obtenir des informations sans autorisation **par déni de Service :** une personne malveillante peut bourrage hello diffusion signal et refuser la distribution d’informations

#### <a name="storage"></a>Storage
Passerelle de chaque appareil et le champ a une forme de stockage (temporaire pour les données hello files d’attente, stockage d’images de système d’exploitation (OS)).

| **Composant** | **Menace** | **Atténuation** | **Risque** | **Implémentation** |
| --- | --- | --- | --- | --- |
| Stockage du périphérique |TRID |Chiffrement de stockage, les journaux hello de signature |Lecture de données à partir du stockage de hello (données PII), de falsification des données de télémétrie. Falsification des données de contrôle de commande en file d’attente ou mises en cache. Falsification des packages de mises à jour de configuration ou le microprogramme lors de la mise en cache ou en file d’attente locale peut entraîner des composants tooOS et/ou le système ne soit compromis |Chiffrement, code d’authentification de message (MAC) ou signature numérique. Si possible, contrôle d’accès renforcé via des listes de contrôle d’accès aux ressources (ACL) ou des autorisations. |
| Image de système d’exploitation de périphérique |TRID | |Falsification des systèmes d’exploitation / remplacement de composants de hello du système d’exploitation |Partition du système d’exploitation en lecture seule, image du système d’exploitation signée, chiffrement. |
| Champ de stockage (files d’attente de données hello) de la passerelle |TRID |Chiffrement de stockage, les journaux hello de signature |La lecture des données à partir du stockage de hello (données PII), de falsification des données de télémétrie, falsifier en file d’attente ou mis en cache les données de contrôle de commande. Falsification des packages de mises à jour de configuration ou le microprogramme (destinés à des appareils ou une passerelle de champ) lors de la mise en cache ou en file d’attente locale peut entraîner des composants tooOS et/ou le système ne soit compromis |BitLocker |
| Image de système d’exploitation de passerelle de champ |TRID | |Falsification des systèmes d’exploitation / remplacement de composants de hello du système d’exploitation |Partition du système d’exploitation en lecture seule, image du système d’exploitation signée, chiffrement. |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Périphérique et traitement des événements/zone de passerelle cloud
Une passerelle de cloud est un système qui permet la communication à distance à partir d’et passerelles toodevices ou un champ à partir de plusieurs sites sur espace d’un réseau public, généralement à un nuage contrôle et données analyse système, une fédération de ces systèmes. Dans certains cas, une passerelle de cloud peut faciliter immédiatement d’usage toospecial accèdent aux appareils à partir de terminaux tels que les tablettes ou téléphones. Dans le contexte hello présenté ici, « cloud » vise toorefer tooa dédié le traitement des données système qui n’est pas lié toohello même site comme hello attaché appareils ou des passerelles du champ, et au cas où les mesures opérationnelles ciblé d’accès physique, mais n’est pas nécessairement infrastructure de « cloud public » tooa.  Une passerelle de cloud peut potentiellement être associée à une passerelle de cloud de réseau virtualisation superposition tooinsulate hello et tous ses périphériques connectés ou des passerelles du champ à partir de tout autre trafic réseau. la passerelle de cloud Hello lui-même est ni un système de contrôle d’appareil, ni un traitement ou support de stockage des données de l’appareil ; Ces fonctionnalités de l’interface avec la passerelle de cloud hello. zone de passerelle de cloud Hello inclut la passerelle de cloud hello elle-même, ainsi que toutes les passerelles de champ et périphériques directement ou indirectement joint tooit.

Passerelle de cloud est principalement personnalisé généré logiciel en cours d’exécution en tant que service avec la passerelle de champ toowhich des points de terminaison exposés et les appareils se connectent. Par conséquent, il convient de la concevoir dans une optique de sécurité. Suivez le processus [Security Development Lifecycle (SDL)](http://www.microsoft.com/sdl) pour concevoir et créer ce service. 

#### <a name="services-zone"></a>Zone des services
Un système de contrôle (ou un contrôleur) est une solution logicielle qui interagit avec un périphérique, ou un passerelle de champ ou une passerelle de cloud à des fins de hello de contrôle d’un ou plusieurs appareils, toocollect et/ou magasin et/ou d’analyse les données de l’appareil pour la présentation, ou à des fins de contrôle suivantes. Systèmes de contrôle sont des entités uniquement de hello dans la portée de hello de cette discussion qui peut immédiatement facilitent l’interaction avec des personnes. exception de Hello est intermédiaires surfaces de contrôle physiques sur les appareils, comme un commutateur qui permet à une personne l’appareil de hello tooturn désactiver ou modifier d’autres propriétés, et pour lequel il n’existe aucun équivalent fonctionnel qui sont accessibles numériquement. 

Surfaces de contrôle physiques intermédiaires sont ceux où toute sorte de régissant la logique contraint fonction hello de surface de contrôle hello physique où une fonction équivalente peut être initiée à distance ou d’entrée est en conflit avec une entrée à distance peut être évités : ce type passe des surfaces de contrôle sont conceptuellement attaché tooa système de contrôle local que tire parti hello même fonctionnalité sous-jacente de tout autre système de contrôle à distance qui hello appareil ne peut être attaché tooin parallèle. Informatique peut être lu à dans le nuage principales menaces toohello [Cloud Security Alliance (CSA)](https://cloudsecurityalliance.org/research/top-threats/) page.

## <a name="additional-resources"></a>Ressources supplémentaires
Consultez toohello suivant des articles pour plus d’informations :

* [Outil SDL de modélisation des menaces](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx)
* [Microsoft Azure IoT reference architecture (Architecture de référence Microsoft Azure IoT)](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>Voir aussi
toolearn savoir plus sur la sécurisation de votre solution IoT, consultez [sécuriser votre déploiement IoT][lnk-security-deployment].

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]
* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]

Vous pouvez lire sur la sécurité IoT Hub dans [tooIoT d’accès contrôle Hub] [ lnk-devguide-security] Bonjour guide du développeur IoT Hub.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md