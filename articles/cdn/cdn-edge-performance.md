---
title: "performances du nœud de bord aaaAnalyze dans Azure CDN | Documents Microsoft"
description: "Analyser les performances du nœud de périmètre dans Microsoft Azure CDN. Bord performances Analytique fournit des informations précises le trafic et la bande passante utilisé pour hello CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Analyser les performances du nœud de périmètre dans Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Vue d'ensemble
Analytique des performances de bord fournit des informations granulaires le trafic et la bande passante utilisé pour hello CDN. Ces informations peuvent ensuite être utilisés toogenerate tendances des statistiques, qui vous permettront d’insight toogain sur la façon dont vos éléments multimédias sont mis en cache et remis tooyour clients. À son tour, cela permet de tooform une stratégie sur la remise de hello toooptimize de votre contenu et de toodetermine les problèmes doit-elle être traités hello de tirer parti de toobetter CDN. Par conséquent, non seulement vous sera tooimprove en mesure de performances de livraison de données, mais, vous devez également être en mesure de tooreduce vos coûts CDN.

> [!NOTE]
> Tous les rapports utilisent la notation UTC/GMT lorsque vous spécifiez une date ou une heure.
> 
> 

## <a name="reports-and-log-collection"></a>Rapports et collecte de journaux
Données d’activité CDN doivent être collectées par module de bord performances Analytique hello avant qu’il peut générer des rapports sur ce dernier. Ce processus de collecte se produit une fois par jour et recouvre activité hello qui ont eu lieu au cours de hello jour précédent. Cela signifie que les statistiques d’un rapport représentent un échantillon des statistiques de hello jour au moment du hello il a été traitée et ne sont pas nécessairement contenir hello jeu de données complet pour hello jour actuel. Hello principale fonction de ces rapports est tooassess performances. Ils ne doivent pas être utilisés à des fins de facturation ou pour générer des statistiques numériques exactes.

> [!NOTE]
> les données brutes Hello à partir de laquelle les rapports bord performances analytiques sont générés sont disponibles pendant au moins 90 jours.
> 
> 

## <a name="dashboard"></a>tableau de bord
tableau de bord de bord performances Analytique Hello effectue le suivi du trafic CDN actuel et historique via un graphique et des statistiques. Utilisez ce tableau de bord toodetect récente et à long terme des tendances sur les performances de hello du trafic CDN pour votre compte.

Ce tableau de bord se décompose comme suit :

* Un graphique interactif qui permet une visualisation hello des mesures clés et les tendances.
* Une chronologie donnant une idée des schémas à long terme pour les mesures et tendances clés.
* Des mesures clés et des informations statistiques sur la façon dont notre réseau CDN améliore le trafic du site mesuré en termes de performances globales, d’utilisation et d’efficacité.

### <a name="accessing-hello-edge-performance-dashboard"></a>L’accès au tableau de bord performances de bord hello
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **bord performances Analytique** menu volant.  Cliquez sur **Tableau de bord**.
   
    tableau de bord analytique Hello bord nœud s’affiche.

### <a name="chart"></a>Graphique
tableau de bord Hello contient un graphique qui effectue le suivi de la métrique sur hello période sélectionnée dans la chronologie hello qui apparaît juste en dessous.  Une chronologie graphiques des toohello deux dernières années d’activité CDN s’affiche directement sous le graphique de hello.

#### <a name="using-hello-chart"></a>À l’aide du graphique de hello
* Par défaut, les taux de rendement du cache hello pour hello 30 derniers jours est tracer.
* Ce graphique est généré à partir des données recueillies chaque jour.
* Vous pointez sur une journée sur le graphique de ligne hello indique une valeur de date et hello de métrique de hello à cette date.
* Cliquez sur Mettre en surbrillance les week-ends tootoggle une superposition des barres verticales gris claires qui représentent les week-ends sur le graphique de hello. Ce type de superposition est utile pour identifier les modèles de trafic pendant les week-ends.
* Cliquez sur tootoggle vue une année il y a un segment de recouvrement de hello précédent l’activité de l’année précédente sur hello même période sur le graphique de hello. Ce type de comparaison permet de connaître les modèles d’utilisation à long terme du CDN. coin supérieur droit de Hello du graphique de hello contient une légende qui indique le code de couleur hello pour chaque graphique linéaire.

#### <a name="updating-hello-chart"></a>Mise à jour hello graphique
* Plage de temps : Effectuez hello suivantes :
  * Sélectionnez la région souhaités hello dans la chronologie de hello. graphique de Hello mettra à jour avec les données correspondant toohello période sélectionnée.
  * Double-cliquez sur hello graphique toodisplay toutes les données historiques disponibles des tooa au maximum de deux ans.
* Métrique : Cliquez sur l’icône de graphique hello apparaît suivant toohello souhaité métrique. graphique de Hello et hello chronologie sont actualisées avec les données de mesure de hello correspondant.

### <a name="key-metrics-and-statistics"></a>Statistiques et mesures clés
#### <a name="efficiency-metrics"></a>Mesures de l’efficacité
Hello ces métriques vise toosee si vous pouvez améliorer l’efficacité du cache. Hello principaux avantages est dérivés de l’efficacité du cache sont :

* Charge réduite sur le serveur d’origine hello qui peut-être entraîner :
  * une amélioration des performances du serveur web ;
  * une réduction des coûts d’exploitation.
* Amélioration de l’accélération de livraison de données depuis plus de requêtes seront pris en charge directement à partir de hello CDN.

| Champ | Description |
| --- | --- |
| Cache Efficiency |Indique le pourcentage de hello de transfert de données qui a été traitée à partir du cache. Cette métrique mesures quand une version mise en cache de hello demandé a été pris en charge le contenu directement à partir de hello CDN (serveurs edge) toorequesters (par exemple, le navigateur web) |
| Hit Rate |Indique le pourcentage de hello de demandes qui ont été pris en charge à partir du cache. Cette métrique mesures quand une version mise en cache de hello demandé a été pris en charge le contenu directement à partir de hello CDN (serveurs edge) toorequesters (par exemple, le navigateur web). |
| % of Remote Bytes - No Cache Config |Indique le pourcentage de hello du trafic qui a été traitée à partir de l’origine serveurs toohello CDN (serveurs edge) qui n’est pas mis en cache en raison de la fonctionnalité de contournement du Cache hello (moteur de règles HTTP). |
| % of Remote Bytes - Expired Cache |Indique le pourcentage de hello du trafic qui a été traitée à partir de l’origine serveurs toohello CDN (serveurs edge) à la suite de revalidation contenue obsolète. |

#### <a name="usage-metrics"></a>Mesures d’utilisation
Hello sert de ces métriques tooprovide idée hello suit les mesures de réduction des coûts :

* En réduisant les coûts d’exploitation via hello CDN.
* Réduction des dépenses CDN grâce à l’efficacité du cache et à la compression.

> [!NOTE]
> Les numéros de volume de trafic représentent le trafic qui a été utilisé dans les calculs de rapports et les pourcentages et peut afficher uniquement une partie du trafic total de hello pour les clients de gros volumes.
> 
> 

| Champ | Description |
| --- | --- |
| Ave Bytes Out |Indique le nombre moyen de hello d’octets transférés pour chaque demande pris en charge du demandeur de toohello hello CDN (serveurs edge) (par exemple, le navigateur web). |
| No Cache Config Byte Rate |Indique le pourcentage de hello du trafic provenant de hello CDN (serveurs edge) toohello demandeur (par exemple, le navigateur web) qui n’est pas mis en cache en raison de la fonctionnalité de contournement du Cache toohello. |
| Compressed Byte Rate |Indique le pourcentage de hello du trafic envoyé à partir de hello CDN (serveurs edge) toorequesters (par exemple, le navigateur web) dans un format compressé. |
| Bytes Out |Indique la quantité de hello de données, en octets, qui ont été remis du demandeur de toohello hello CDN (serveurs edge) (par exemple, le navigateur web). |
| Bytes In |Indique la quantité hello de données, en octets, envoyés par les demandeurs (par exemple, le navigateur web) toohello CDN (serveurs edge). |
| Bytes Remote |Indique la quantité hello de données, en octets, envoyés à partir de la clientèle et du CDN toohello serveurs origine CDN (serveurs edge). |

#### <a name="performance-metrics"></a>Mesures de performances
Hello ces métriques vise tootrack les performances globales du CDN pour votre trafic.

| Champ | Description |
| --- | --- |
| Transfer Rate |Indique le taux moyen de hello à laquelle le contenu a été transféré du demandeur de tooa hello CDN. |
| Duration |Indique la durée moyenne de hello, en millisecondes, nécessaire toodeliver un demandeur de tooa actif (par exemple, le navigateur web). |
| Compressed Request Rate |Indique le pourcentage de hello d’accès qui ont été remis du demandeur de toohello hello CDN (serveurs edge) (par exemple, le navigateur web) dans un format compressé. |
| 4xx Error Rate |Indique le pourcentage de hello d’accès qui a généré un code d’état 4xx. |
| 5xx Error Rate |Indique le pourcentage de hello d’accès qui a généré un code d’état 5xx. |
| Correspondances |Indique le nombre de hello de demandes pour le contenu CDN. |

#### <a name="secure-traffic-metrics"></a>Mesures de trafic sécurisé
Hello vise de ces métriques de performances du CDN tootrack pour le trafic HTTPS.

| Champ | Description |
| --- | --- |
| Secure Cache Efficiency |Indique le pourcentage de hello de transférer les requêtes HTTPS qui ont été pris en charge à partir du cache de données. Cette mesure mesure une version mise en cache de hello demande le contenu a été traitée directement à partir de hello CDN (serveurs edge) toorequesters (par exemple, le navigateur web) via le protocole HTTPS. |
| Secure Transfer Rate |Indique le taux moyen de hello à laquelle le contenu a été transféré depuis hello CDN (serveurs edge) toorequesters (par exemple, les serveurs web) via le protocole HTTPS. |
| Average Secure Duration |Indique la durée moyenne de hello, en millisecondes, nécessaire toodeliver un demandeur de tooa actif (par exemple, le navigateur web) via le protocole HTTPS. |
| Secure Hits |Indique le nombre hello de demandes HTTPS pour le contenu CDN. |
| Secure Bytes Out |Indique la quantité hello du trafic HTTPS, en octets, qui ont été remis du demandeur de toohello hello CDN (serveurs edge) (par exemple, le navigateur web). |

## <a name="reports"></a>Rapports
Chaque rapport de ce module contient un graphique et des statistiques sur l’utilisation de la bande passante et du trafic pour différents types de mesures (par exemple, codes d’état HTTP, codes d’état du cache, URL de demande, etc..). Ces informations peuvent être utilisé toodelve profond dans la façon dont le contenu est prise en charge tooyour clients et les performances de livraison du comportement tooimprove données toofine ajuster CDN.

### <a name="accessing-hello-edge-performance-reports"></a>L’accès aux rapports de performances hello edge
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **bord performances Analytique** menu volant.  Cliquez sur **HTTP Large Object**.
   
    écran de rapports analytique Hello bord nœud s’affiche.

| Rapport | Description |
| --- | --- |
| Daily Summary |Vous permet des tendances de trafic quotidien tooview sur une période de temps. Chaque barre sur ce graphique représente une date particulière. taille Hello de barre de hello indique le nombre total de hello d’accès qui se sont produites à cette date. |
| Hourly Summary |Vous permet des tendances du trafic de toutes les heures tooview sur une période de temps. Chaque barre de ce graphique représente une heure donnée à une date particulière. taille Hello de barre de hello indique le nombre total de hello d’accès qui s’est produite pendant cette heure. |
| Protocoles |Affiche la répartition hello du trafic entre hello HTTP et les protocoles HTTPS. Un graphique en anneau indique le pourcentage de hello d’accès qui s’est produite pour chaque type de protocole. |
| HTTP Methods |Vous permet de tooget un sens rapide des méthodes HTTP sont en cours toorequest utilisé vos données. En général, les méthodes de demande HTTP hello les plus courantes sont GET, HEAD et POST. Un graphique en anneau indique le pourcentage de hello d’accès qui s’est produite pour chaque type de méthode de requête HTTP. |
| URLs |Contient un graphique qui affiche l’URL demandée 10 premières hello. Une barre s’affiche pour chaque URL. Hello hauteur hello indique le nombre d’accès URL spécifique a générés au fil de l’intervalle de temps hello couvertes par les rapports hello. Statistiques pour les 100 premiers de hello demandé Qu'url sont affichent directement sous ce graphique. |
| CNAMEs |Contient un graphique qui affiche hello top 10 enregistrements CNAME utilisé toorequest actifs sur un intervalle de temps hello d’un rapport. Statistiques pour les 100 premiers de hello demandé que CNAME s’affichent directement sous ce graphique. |
| Origins |Contient un graphique qui affiche hello 10 premiers CDN ou client serveurs d’origine à partir de laquelle les ressources ont été demandées sur une période spécifiée. Statistiques pour les 100 premiers de hello demandé CDN ou client serveurs d’origine sont affichent directement sous ce graphique. Serveurs d’origine client sont identifiées par nom hello défini dans hello option de nom de répertoire. |
| Geo POPs |Affiche la quantité de trafic acheminé via un point de présence (POP) particulier. abréviation à trois lettres Hello représente un POP dans notre réseau CDN. |
| Clients |Contient un graphique qui affiche hello top 10 clients nécessitant des ressources sur une période spécifiée. Pour des raisons de hello de ce rapport, toutes les demandes provenant de hello même adresse IP sont considérés comme toobe de hello même client. Statistiques pour les clients de 100 premières hello s’affichent directement sous ce graphique. Ce rapport est utile pour déterminer les modèles d’activité de téléchargement pour vos principaux clients. |
| États du cache |Donne une description détaillée de comportement du cache, ce qui peut révéler des approches pour améliorer hello expérience utilisateur globale. Étant donné que les performances les meilleures hello proviennent de présences dans le cache, vous pouvez optimiser les vitesses de remise de données par la réduction des absences dans le cache et de présences dans le cache a expiré. |
| NONE Details |Contient un graphique qui affiche les 10 URL supérieur hello pour les ressources pour lequel actualisation de contenu du cache n’est pas activée sur une période spécifiée. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| CONFIG_NOCACHE Details |Contient un graphique qui affiche les URL des 10 premiers hello pour les ressources qui ne sont pas mises en cache en raison de la configuration du CDN du client toohello. Ces types de ressources ont été pris en charge par serveur d’origine hello. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| UNCACHEABLE Details |Contient un graphique qui affiche les 10 URL supérieur hello pour les ressources qui n’a pas mis en cache en raison de données d’en-tête toorequest. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| TCP_HIT Details |Contient un graphique qui affiche les 10 URL supérieur hello pour les ressources qui sont traitées immédiatement à partir du cache. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| TCP_MISS Details |Contient un graphique qui affiche les 10 URL supérieur hello pour les ressources qui ont un état de cache de TCP_MISS. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| TCP_EXPIRED_HIT Details |Contient un graphique qui affiche hello top 10 des URL pour obsolètes actifs qui ont été traitées directement à partir de hello POP. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| TCP_EXPIRED_MISS Details |Contient un graphique qui affiche les 10 URL supérieur hello pour les ressources obsolètes pour lequel une nouvelle version avait toobe récupérée à partir du serveur d’origine hello. Statistiques pour les URL de 100 premières hello pour ces types de ressources s’affichent directement sous ce graphique. |
| TCP_CLIENT_REFRESH_MISS Details |Contient un graphique à barres qui affiche hello top 10 URL actifs ont été récupérés à partir d’un serveur d’origine en raison de la demande de cache non tooa à partir du client de hello. Statistiques pour les URL de 100 premières hello pour ces types de requêtes s’affichent directement sous ce graphique. |
| Client Request Types |Indique le type de hello de demandes qui ont été apportées par les clients HTTP (par exemple, les navigateurs). Ce rapport inclut un graphique en anneau qui fournit un sens en tant que toohow demandes sont gérées. Les informations de la bande passante et le trafic pour chaque type de demande s’affiche sous le graphique de hello. |
| User Agent |Contient un graphique à barres affichant hello top 10 utilisateur agents toorequest votre contenu via notre CDN. En règle générale, un agent utilisateur est un navigateur web, un lecteur multimédia ou un navigateur de téléphone mobile. Statistiques pour les agents de 100 utilisateurs hello supérieur s’affichent directement sous ce graphique. |
| Referrers |Contient un graphique à barres affichant hello Meilleures références 10 toocontent est accédé via notre CDN. En règle générale, un point d’accès est hello des URL de page web de hello ou une ressource qui établit un lien tooyour contenu. Informations détaillées sont fournies sous le graphique de hello pour les références de 100 premières hello. |
| Compression Types |Contient un graphique en anneau qui répartit les ressources demandées selon qu’elles ont été ou non compressées par nos serveurs Edge. pourcentage de Hello de biens compressés est divisée en type hello de compression utilisé. Informations détaillées sont fournies sous le graphique de hello pour chaque type de compression et l’état. |
| File Types |Contient un graphique à barres qui affiche hello top 10 types de fichiers qui ont été demandés via notre CDN pour votre compte. Pour des raisons de hello de ce rapport, un type de fichier est défini par l’extension de nom de fichier de l’élément multimédia hello et le type de support Internet (par exemple, .html \[texte/html\], .htm \[texte/html\], .aspx \[texte/html\], etc..). Informations détaillées sont fournies sous le graphique de hello pour les types de fichier 100 premières hello. |
| Unique Files |Contient un graphique qui trace le nombre total de hello de ressources uniques qui ont été demandées à un jour donné sur une période spécifiée. |
| Token Auth Summary |Contient un graphique à secteurs décrivant brièvement si les ressources demandées étaient ou non protégées par une authentification par jeton. Actifs protégés sont affichés dans le graphique de hello en fonction des résultats toohello de leur authentification tentée. |
| Token Auth Deny Details |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui ont été refusées en raison de l’authentification basée sur les tooToken. |
| HTTP Response Codes |Fournit une répartition des codes d’état hello HTTP (par exemple, 200 OK, 403 interdit, 404 introuvable, etc.) qui ont été remis tooyour HTTP clients par nos serveurs edge. Vous permet d’un graphique à secteurs tooquickly évaluer la façon dont vos éléments multimédias ont été pris en charge. Les données de statistiques détaillées sont fournies pour chaque code de réponse ci-dessous graphique de hello. |
| 404 Errors |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui génèrent un code de réponse 404 introuvable. |
| 403 Errors |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui génèrent un code de réponse 403 Interdit. Un code de réponse 403 Forbidden est renvoyé lorsqu’une demande est refusée par un serveur d’origine client ou un serveur Edge dans notre point de présence. |
| 4xx Errors |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui génèrent un code de réponse dans la plage de 400 hello. Les codes de réponse « 403 Not Found » et « 404 Forbidden » sont exclus de ce rapport. En règle générale, un code de réponse 4xx est renvoyé lorsqu’une demande est refusée en raison d’une erreur client. |
| 504 Errors |Contient un graphique à barres qui vous permet de tooview hello supérieur 10 requêtes qui génèrent un code de réponse de délai d’attente de la passerelle 504. Un code de réponse de délai d’attente de la passerelle 504 se produit lorsqu’un délai d’attente se produit lorsqu’un proxy HTTP essaye toocommunicate avec un autre serveur. Dans les cas de hello de notre CDN, un code de réponse de délai d’attente de la passerelle 504 se produit généralement lorsqu’un serveur edge est tooestablish impossible la communication avec un serveur d’origine client. |
| 502 Errors |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui génèrent un code de réponse 502 Passerelle incorrecte. Un code de réponse « 502 Bad Gateway » est renvoyé en cas d'échec du protocole HTTP entre un serveur et un proxy HTTP. Dans les cas de hello de notre CDN, un code de réponse 502 Passerelle incorrecte se produit généralement lorsqu’un serveur d’origine client renvoie une réponse non valide tooan bord serveur. Une réponse est considérée comme non valide si elle ne peut pas être analysée ou si elle est incomplète. |
| 5xx Errors |Contient un graphique à barres qui vous permet de tooview hello top 10 requêtes qui génèrent un code de réponse dans la plage de 500 hello.  Les codes de réponse « 502 Bad Gateway » et « 504 Gateway Timeout » sont exclus de ce rapport. |

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
* [Statistiques en temps dans Microsoft Azure CDN](cdn-real-time-stats.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
* [Rapports HTTP avancés](cdn-advanced-http-reports.md)

