---
title: "aaaAnalyze les statistiques d’utilisation avec Azure CDN avancées HTTP rapports | Documents Microsoft"
description: "Découvrez comment toocreate avancée rapports HTTP dans le CDN Microsoft Azure. Ces rapports fournissent des informations détaillées sur l’activité CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Analyser les statistiques d’utilisation avec les rapports HTTP avancés dans Microsoft Azure CDN
## <a name="overview"></a>Vue d'ensemble
Ce document présente les rapports HTTP avancés disponibles dans Microsoft Azure CDN. Ces rapports fournissent des informations détaillées sur l’activité CDN.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Accès aux rapports HTTP avancés
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **rapports avancés de HTTP** menu volant.  Cliquez sur **HTTP Large Platform**.
   
    ![Portail de gestion CDN - Menu Rapports avancés](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Les options de rapport sont affichées.

## <a name="geography-reports-map-based"></a>Rapports géographiques (à partir d’une carte)
Il existe cinq rapports qui tirent parti d’un tooindicate carte des régions hello à partir de laquelle votre contenu est demandé. Il s’agit des rapports World Map, United States Map, Canada Map, Europe Map et Asia Pacific Map.

Chaque rapport cartographique évalue les entités géographiques (par exemple, pays, États et provinces) en fonction du pourcentage de toohello d’accès provient de cette région. En outre, une carte est fourni toohelp visualiser les emplacements hello à partir de laquelle votre contenu est demandé. Il est en mesure de toodo par un codage en couleurs de chaque région selon la quantité de toohello de la demande rencontré dans cette région. Les régions ombrées plus claires indiquent une demande de contenu plus faible, tandis que les régions plus foncées illustrent des niveaux plus soutenus.

Informations détaillées sur le trafic et la bande passante pour chaque région sont fournies directement sous le mappage de hello. Cela vous permet de tooview hello nombre de correspondances, pourcentage hello d’accès, le montant total de hello de données transférées (en Go) et pourcentage hello des données transférées pour chaque région. Vous pouvez afficher la description de chacune de ces mesures. Enfin, lorsque vous pointez sur une région (par exemple, pays, l’état ou province), nom de hello et pourcentage hello d’accès qui s’est produite dans la région de hello seront affichera en tant qu’une info-bulle.

Une brève description est fournie ci-dessous pour chaque type de rapport géographique dérivé d’une carte.

| Nom du rapport | Description |
| --- | --- |
| World Map |Ce rapport permet à la demande dans le monde tooview hello pour votre contenu CDN. Chaque pays sont colorées sur hello world carte tooindicate hello pourcentage d’accès provient de cette région. |
| United States Map |Ce rapport vous permet à la demande de hello tooview pour votre contenu CDN hello États-Unis. Chaque état est coloré sur ce pourcentage de hello tooindicate mappage d’accès provient de cette région. |
| Canada Map |Ce rapport permet à la demande de hello tooview pour votre contenu CDN au Canada. Chaque région est colorée sur ce pourcentage de hello tooindicate mappage d’accès provient de cette région. |
| Europe Map |Ce rapport permet à la demande de hello tooview pour votre contenu CDN en Europe. Chaque pays est coloré sur ce pourcentage de hello tooindicate mappage d’accès provient de cette région. |
| Asia Pacific Map |Ce rapport permet à la demande de hello tooview pour votre contenu CDN en Asie. Chaque pays est coloré sur ce pourcentage de hello tooindicate mappage d’accès provient de cette région. |

## <a name="geography-reports-bar-charts"></a>Rapports géographiques (graphiques à barres)
Il existe deux rapports supplémentaires qui fournissent des informations statistiques en fonction de toogeography, qui sont les villes de haut et haut pays. Ces rapports classent les villes et pays, respectivement, selon le nombre de toohello d’accès provenant de ces régions. Lors de la génération de ce type de rapport, un graphique à barres indique 10 villes hello ou pays qui a demandé le contenu sur une plateforme spécifique. Ce graphique à barres vous permet de tooquickly évaluer les régions hello qui génèrent hello plus grand nombre de demandes pour votre contenu.

Hello le côté gauche du graphique de hello (axe y) indique le nombre d’accès s’est produite dans la région spécifiée du hello. Directement sous le graphique hello (axe x), vous trouverez une étiquette pour chacune des régions de 10 premières hello.

### <a name="using-hello-bar-charts"></a>À l’aide de graphiques à barres hello
* Si vous pointez sur une barre, nom de hello et le nombre total de hello d’accès qui se sont produites dans la région de hello seront affichera en tant qu’une info-bulle.
* info-bulle Hello pour hello rapport de villes du haut identifie une ville par son nom, le département/province et l’abréviation du pays.
* Si la ville de hello ou une région (par exemple, département/province) à partir de laquelle une demande n’a pas pu être déterminée, puis il indique qu’elles sont inconnues. Si le pays de hello est inconnu, deux points d’interrogation (c'est-à-dire ??) ; s’affichera.
* Un rapport peut inclure des métriques pour « Europe » ou hello « Région Asie/Pacifique. » Ces éléments ne sont pas censés tooprovide des informations statistiques sur toutes les adresses IP de ces régions. Au lieu de cela, elles s’appliquent uniquement toorequests qui proviennent d’adresses IP qui sont répartis dans Europe ou en Asie/Pacifique, au lieu de ville spécifique de tooa ou pays.

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez nombre total de hello d’accès, le pourcentage de hello de succès, quantité hello de données transférées (en Go), et le pourcentage hello de données transférées pour hello 250 régions supérieure. Vous pouvez afficher la description de chacune de ces mesures.

Une brève description est fournie pour les deux types de rapports ci-dessous.

| Nom du rapport | Description |
| --- | --- |
| Top Cities |Ce rapport indique les villes selon le nombre de toohello d’accès provenant de cette région. |
| Top Countries |Ce rapport indique les pays selon le nombre de toohello d’accès provenant de cette région. |

## <a name="daily-summary"></a>Daily Summary
Hello rapport de résumé quotidien vous permet de tooview hello nombre d’accès et les données transférées sur une plateforme particulière sur une base quotidienne. Ces informations peuvent être utilisées tooquickly discerner les modèles d’activités CDN. Par exemple, ce rapport peut vous aider à détecter les jours où a été recensé un trafic supérieur ou inférieur au niveau attendu.

Lors de la génération de ce type de rapport, un graphique à barres fournit une indication visuelle en tant que montant toohello de demande spécifique à la plateforme expérimentée quotidiennement sur hello période couverte par le rapport de hello. Pour ce faire, il sera affichant une barre pour chaque jour dans les rapports hello. Par exemple, la sélection hello période appelée « Dernière semaine » génère un graphique à barres avec sept barres. Chaque barre indique le nombre total de hello d’accès en raison d’un jour.

Hello côté gauche du graphique de hello (axe y) indique le nombre d’accès s’est produite sur hello spécifié date. Directement sous le graphique hello (axe x), vous trouverez une étiquette qui indique la date de hello (Format : AAAA-MM-JJ) pour chaque jour inclus dans le rapport de hello.

> [!TIP]
> Si vous pointez sur une barre, nombre total de hello d’accès qui se sont produites à cette date s’affichera en tant qu’une info-bulle.
> 
> 

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez nombre total de hello d’accès et la quantité de hello de données transférées (en Go) pour chaque jour couverte par les rapports hello.

## <a name="by-hour"></a>By Hour
Hello les rapports par heure vous permet de tooview hello nombre d’accès et les données transférées sur une plateforme spécifique, toutes les heures. Ces informations peuvent être utilisées tooquickly discerner les modèles d’activités CDN. Par exemple, ce rapport peut vous aider à détecter hello périodes journée hello qui rencontrent une valeur supérieure ou inférieure à trafic attendu.

Lors de la génération de ce type de rapport, un graphique à barres fournit une indication visuelle en tant que montant toohello de demande spécifique à la plateforme en raison d’heures sur hello période couverte par le rapport de hello. Pour ce faire, il sera affichant une barre pour chaque heure couverte par les rapports hello. Par exemple, si vous sélectionnez une période de 24 heures, vous obtiendrez un graphique contenant vingt-quatre barres. Chaque barre indique le nombre total de hello d’accès lors de l’heure.

Hello le côté gauche du graphique de hello (axe y) indique le nombre d’accès s’est produite sur l’heure hello. Directement sous le graphique hello (axe x), vous trouverez une étiquette qui indique la date et d’heure hello (Format : AAAA-MM-JJ HH) pour chaque heure inclus dans le rapport de hello. Le temps est déclaré à l’aide du format 24 heures, et il est spécifié à l’aide de la zone de temps UTC/GMT hello.

> [!TIP]
> Si vous pointez sur une barre, nombre total de hello d’accès qui s’est produite pendant cette heure s’affichera en tant qu’une info-bulle.
> 
> 

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez nombre total de hello d’accès et la quantité de hello de données transférées (en Go) pour chaque heure couverte par les rapports hello.

## <a name="by-file"></a>By File
Hello par fichier de rapport permet de vous tooview hello du trafic à la demande et hello engagée sur une plateforme spécifique pour hello plus demandé actifs. Lors de la génération de ce type de rapport, un graphique à barres sera généré sur actifs plus demandés 10 premières hello sur hello période spécifiée.

> [!NOTE]
> Pour des raisons de hello de ce rapport, des URL CNAME edge sont tootheir converti équivalent CDN URL. Cela permet qu'une concordance exacte pour le nombre total de hello d’accès associé à un élément multimédia, quelle que soit la hello CDN ou bord URL CNAME utilisée toorequest.
> 
> 

partie gauche du graphique de hello (axe y) Hello indique le nombre de hello de requêtes pour chaque élément multimédia sur hello période spécifiée. Directement sous le graphique hello (axe x), vous trouverez une étiquette qui indique le nom de fichier hello pour chacun des actifs demandés 10 premières hello.

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez hello informations pour chacun des actifs demandés 250 supérieur hello suivantes : chemin d’accès relatif, le nombre total de hello de présences dans le pourcentage hello d’accès, de quantité hello de données transférées (en Go) et le pourcentage de hello de données transférées.

## <a name="by-file-detail"></a>By File Detail
Hello rapport par fichier détaillé vous permet de quantité de hello tooview du trafic à la demande et hello effectuée sur une plateforme spécifique pour un composant spécifique. Tout en haut de ce rapport est hello fichier détails pour option hello. Cette option fournit une liste de vos ressources plus demandés sur la plateforme sélectionnée de hello. Dans l’ordre toogenerate un rapport en détail du fichier, vous devez asset souhaité de hello tooselect de hello détails de fichier pour l’option. Après quoi, un graphique à barres indique la quantité hello de demande quotidienne qu’il a générées sur hello période spécifiée.

partie gauche du graphique de hello (axe y) Hello indique le nombre total de hello de demandes qu’un élément multimédia en raison d’un jour donné. Directement sous le graphique hello (axe x), vous trouverez une étiquette qui indique la date de hello (Format : AAAA-MM-JJ) pour la demande CDN pour hello actif a été signalée.

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez nombre total de hello d’accès et la quantité de hello de données transférées (en Go) pour chaque jour couverte par les rapports hello.

## <a name="by-file-type"></a>By File Type
Hello les rapports par Type de fichier permet de vous tooview hello quantité de trafic à la demande et hello induite par type de fichier. Lors de la génération de ce type de rapport, un graphique en anneau indique pourcentage hello d’accès généré par les types de fichier 10 premières hello.

> [!TIP]
> Si vous pointez sur un secteur dans un graphique en anneau de hello, type de média Internet de hello du que type de fichier s’affichera sous la forme d’une info-bulle.
> 
> 

les données de Hello qui a été utilisé toogenerate graphique hello peuvent être affichées en dessous. Vous y trouverez les/Internet de l’extension de nom de fichier hello type de média, nombre total de hello d’accès, pourcentage hello de succès, quantité hello de données transférées (en Go) et pourcentage de données transférées pour chacun des hello hello premiers 250 types de fichiers.

## <a name="by-directory"></a>By Directory
Hello active par rapport permet montant de hello tooview du trafic à la demande et hello effectuée sur une plateforme spécifique pour le contenu d’un répertoire spécifique. Lors de la génération de ce type de rapport, un graphique à barres indique le nombre total de hello d’accès généré par le contenu dans les répertoires de 10 premières hello.

### <a name="using-hello-bar-chart"></a>À l’aide du graphique à barres hello
* Placez le curseur sur une barre de répertoire de toohello de chemin d’accès relatif hello tooview correspondant.
* Le contenu stocké dans un sous-dossier d’un répertoire n’est pas pris en compte dans le calcul de la demande par répertoire. Ce calcul s’appuie uniquement sur le nombre de hello de requêtes générées pour le contenu stocké dans le répertoire réels de hello.
* Pour des raisons de hello de ce rapport, des URL CNAME edge sont tootheir converti équivalent CDN URL. Cela permet qu'un décompte précis pour toutes les statistiques associé avec un élément multimédia, quelle que soit la hello CDN ou bord URL CNAME utilisée toorequest.

Hello côté gauche du graphique de hello (axe y) indique hello le nombre total de demandes de contenu hello stockées dans vos 10 répertoires supérieure. Chaque barre sur le graphique de hello représente un répertoire. Hello d’utiliser un codage en couleurs toomatch schéma une barre tooa directory répertoriés dans la section de répertoires complètes de 250 haut hello.

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez hello informations pour chacun des répertoires de haut 250 hello suivantes : chemin d’accès relatif, le nombre total de hello de présences dans le pourcentage hello d’accès, de quantité hello de données transférées (en Go) et le pourcentage de hello de données transférées.

## <a name="by-browser"></a>By Browser
Hello les rapports par le navigateur vous permet de tooview les navigateurs ont été utilisé toorequest de contenu. Lors de la génération de ce type de rapport, un graphique à secteurs indique le pourcentage hello de demandes traitées par les principaux navigateurs de 10 hello.

### <a name="using-hello-pie-chart"></a>À l’aide du graphique à secteurs de hello
* Pointez sur un secteur dans hello graphique à secteurs tooview les nom d’un navigateur et la version.
* Pour des raisons de hello de ce rapport, chaque combinaison unique/version du navigateur est considéré comme un navigateur différent.
* tranche Hello appelé « Autre » indique le pourcentage hello de demandes traitées par tous les autres navigateurs et des versions.

les données de Hello qui a été utilisé toogenerate hello secteurs peuvent être affichées en dessous. Vous y trouverez hello navigateur type/numéro de version nombre total de hello d’accès et le pourcentage de hello d’accès pour chacun des principaux navigateurs de 250 hello.

## <a name="by-referrer"></a>By Referrer
Hello les rapports par point d’accès vous permet de tooview hello Meilleures références toocontent sur la plateforme sélectionnée de hello. Un point d’accès indique le nom d’hôte hello à partir de laquelle une demande a été générée. Lors de la génération de ce type de rapport, un graphique à barres indique quantité hello de la demande (c'est-à-dire, accès) générés par les points d’accès hello top 10.

partie gauche du graphique de hello (axe y) Hello indique le nombre total de hello de demandes qu’en raison d’un élément multimédia pour chaque point d’accès. Chaque barre sur le graphique de hello représente un point d’accès. Hello d’utiliser un codage en couleurs toomatch schéma une barre tooa référent répertoriés dans la section du haut 250 référent hello.

les données de Hello qui a été utilisé toogenerate graphique à barres hello peuvent être affichées en dessous. Vous y trouverez hello URL, le nombre total de hello d’accès et le pourcentage de hello d’accès généré à partir de chacune des principales références de 250 hello.

## <a name="by-download"></a>By Download
Hello par télécharger un rapport vous permet de tooanalyze les modèles de téléchargement pour votre contenu plus demandé. haut Hello du rapport de hello contient un graphique à barres que téléchargements compare tentée avec des téléchargements terminés pour hello top 10 actifs demandés. Chaque barre est coloré en fonction de toowhether, d' qu'il s’agit un tentative de téléchargement (bleu) ou un téléchargement terminé (vert).

> [!NOTE]
> Pour des raisons de hello de ce rapport, des URL CNAME edge sont tootheir converti équivalent CDN URL. Cela permet qu'un décompte précis pour toutes les statistiques associé avec un élément multimédia, quelle que soit la hello CDN ou bord URL CNAME utilisée toorequest.
> 
> 

Hello le côté gauche du graphique de hello (axe y) indique hello des noms de fichiers de ressources demandé 10 premières hello. Directement sous le graphique hello (axe x), vous trouverez des étiquettes qui indiquent le nombre total de hello de téléchargements de tentative/terminé.

Directement sous le graphique à barres hello, hello informations suivantes est répertorié pour actifs demandés 250 supérieur hello : chemin d’accès relatif (nom de fichier compris), le nombre de hello de fois où il a été téléchargée toocompletion, hello nombre de fois qu’il a été demandé et hello pourcentage de demandes ayant abouti à un téléchargement complet.

> [!TIP]
> Notre CDN n’est pas informé par un client HTTP (par exemple, un navigateur) lorsqu’une ressource a été entièrement téléchargée. Par conséquent, nous avons toocalculate si une ressource a été complètement téléchargée conséquente toostatus codes et les demandes de plage d’octets. Hello première chose que nous allons lorsque ce calcul est si hello demande entraîne un code d’état OK 200. Dans ce cas, puis nous examinons tooensure des demandes de plages d’octets qu’ils couvrent actif complet de hello. Enfin, nous comparez hello taille toohello de données transférées de ressource demandée de hello. Si hello données transférées est égal tooor supérieure à la taille du fichier hello et demandes de plages d’octets hello sont appropriées pour cet élément multimédia, puis hello positionnement est compté comme un téléchargement complet.
> 
> En raison de la nature d’interprétation toohello de ce rapport, vous devez conserver Bonjour l’esprit les points qui peuvent changer la cohérence de hello et la précision de ce rapport suivants.
> 
> * Les modèles de trafic ne peuvent pas être prédits avec précision lorsque les agents utilisateurs se comportent différemment. Cela peut porter le taux de téléchargement terminé au-delà de 100 %.
> * Les ressources qui utilisent un téléchargement progressif HTTP ne peuvent pas être représentés avec précision dans ce rapport. Il s’agit d’échéance toousers recherche toodifferent positions dans une vidéo.
> 
> 

## <a name="by-404-errors"></a>By 404 Errors
Hello par 404 ce rapport vous permet de type hello de tooidentify de contenu génère hello plus nombre de codes d’état 404 introuvable. haut Hello du rapport de hello contient un graphique à barres pour les ressources de 10 premiers hello pour lequel un code d’état 404 introuvable a été retournée. Ce graphique à barres compare le nombre total de hello de requêtes avec les requêtes qui génèrent un code d’état introuvable 404 pour ces ressources. Chaque barre est codée par couleur. Une barre jaune sert tooindicate qui hello demande a généré un code d’état 404 introuvable. Une barre rouge est utilisée tooindicate hello nombre de demandes pour un composant de hello.

> [!NOTE]
> Pour des raisons de hello de ce rapport, notez hello qui suit :
> 
> * Un accès représente une demande de ressource, quel que soit le code d’état.
> * URL du CNAME Edge sont tootheir converti équivalent CDN URL. Cela permet qu'un décompte précis pour toutes les statistiques associé avec un élément multimédia, quelle que soit la hello CDN ou bord URL CNAME utilisée toorequest.
> 
> 

partie gauche du graphique de hello (axe y) Hello indique le nom de fichier hello pour chacun des hello top 10 actifs demandés qui a généré un code d’état 404 introuvable. Directement sous le graphique hello (axe x), vous trouverez des étiquettes qui indiquent le nombre total de hello de requêtes et de nombre de hello de requêtes qui génèrent un code d’état 404 introuvable.

Directement sous le graphique à barres hello, hello informations suivantes est répertorié pour actifs demandés 250 supérieur hello : chemin d’accès relatif (nom de fichier compris), nombre de hello de demandes qui ont provoqué un 404 introuvable code d’état, nombre total de hello de fois que hello asset était demande de hello pourcentage de requêtes qui génèrent un code d’état 404 introuvable.

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
* [Statistiques en temps dans Microsoft Azure CDN](cdn-real-time-stats.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
* [Analyser les performances de serveurs Edge](cdn-edge-performance.md)

