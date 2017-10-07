---
title: "aaaAzure RemoteApp - test de votre utilisation de la bande passante réseau avec quelques scénarios courants | Documents Microsoft"
description: "Découvrez les scénarios d’utilisation courants qui peuvent vous aider à déterminer vos besoins en bande passante réseau pour Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp : test de l’utilisation de votre bande passante réseau avec quelques scénarios courants
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Comme expliqué dans [l’utilisation de la bande passante du réseau estimation Azure RemoteApp](remoteapp-bandwidth.md), hello meilleures toofigure de façon quel impact hello d’Azure RemoteApp tooyour réseau est toorun certains tests d’utilisation. Exécuter ces tests pour un jeu de temps période et mesures hello la bande passante nécessaire pour chaque scénario. Si vous avez la possibilité de hello, vous pouvez également mesurer hello réseau paquets réseau et perte instabilité toounderstand hello modèles de réseau qui seront créées dans votre environnement spécifique.

Lors de l’évaluation de l’utilisation de la bande passante hello, n’oubliez pas que l’utilisation varie entre différents utilisateurs au sein de votre société. Par exemple, les lecteurs et rédacteurs de texte consomment généralement moins de bande passante que les utilisateurs qui utilisent la vidéo. Pour de meilleurs résultats, analysez vos besoins de l’utilisateur et créer un mélange de hello les scénarios suivants qui correspond le mieux aux utilisateurs de hello dans votre entreprise. N’oubliez pas trop[facteurs hello révision ayant un impact sur l’utilisation de la bande passante et l’utilisateur expérience](remoteapp-bandwidthexperience.md) -qui vous aidera à identifier les tests idéale hello.

Tout d’abord en savoir plus sur les tests hello, choisir votre combinaison, puis les exécuter. Vous pouvez utiliser la table hello ci-dessous toohelp suivre les performances.

> [!NOTE]
> Si vous ne pouvez pas faire vos propres tests de réseau, ou vous n’avez pas hello temps toodo donc, consultez notre [estimations de la bande passante réseau de base/recommandations](remoteapp-bandwidthguidelines.md). Néanmoins, comme votre consommation peut varier, *exécutez* vos propres tests si vous en avez la possibilité.
> 
> 

## <a name="hello-usage-tests"></a>tests de l’utilisation de Hello
Chaque test est exécuté pour une période différente et teste différentes fonctions/fonctionnalités qui consomment de la bande passante réseau. N’oubliez pas de combinaison de hello toochoose de test qui correspond le mieux à vos utilisateurs de la société.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>Présentation PowerPoint complexe avec animations, exécutée pendant une durée allant de 900 et 1 000 secondes
Un utilisateur présente entre 45 et 50 diapositives haute fidélité en utilisant Microsoft Office PowerPoint en mode plein écran. les diapositives Hello doivent contenir des images, les transitions (avec animations) et les arrière-plans avec un dégradé de couleur typiques de votre entreprise. utilisateur de Hello doit consacrer au moins 20 secondes sur chaque diapositive.

Ce scénario crée le trafic de rafale, lorsqu’une diapositive passe toohello de diapositive suivante dans la présentation de hello.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Présentation PowerPoint simple exécutée pendant environ 620 secondes
Un utilisateur présente un simple fichier PowerPoint incluant environ 30 diapositives en utilisant Microsoft Office PowerPoint en mode plein écran. les diapositives Hello sont beaucoup plus de texte que dans le scénario exécutif/complexe PowerPoint de hello et plus simple arrière-plans et les images (diagrammes noirs). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer exécuté pendant environ 250 secondes
Un utilisateur parcourt le web de hello à l’aide d’Internet Explorer. l’utilisateur Hello accède et fait défiler une combinaison de texte, des images et des schémas. Hello des pages web stockées sur le lecteur de disque local hello du serveur hôte de Session Bureau à distance (hôte de Session Bureau à distance) de hello en tant qu’un. Fichier MHT. Hello utilisateur fait défiler une à l’aide de PG. préc, PG. suiv, haut et bas clés, des intervalles différents pour chaque type de clé/du défilement :

    - Bas - 250 touches toutes les 500 ms
    - Page haut - 36 touches toutes les 1 000 ms
    - Bas - 75 touches toutes les 100 ms
    - Page bas - 20 touches toutes les 500 ms
    - Haut - 120 touches toutes les 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>Simple document PDF exécuté pendant environ 610 secondes
Un utilisateur lit un document PDF dans lequel il effectue des recherches de différentes manières à l’aide d’Adobe Acrobat Reader. document de Hello doit être composé de tables, des graphiques simples et plusieurs polices de texte. document de Hello est long à 35-40 pages. utilisateur de Hello fait défiler vers l’arrière à deux des vitesses différentes et transfère à quatre formats différents de zoom (ajuster toopage, toowidth adaptée, 100 % et l’autre de votre choix). Hello Zoom garantit que le texte hello (police) effectue le rendu de différentes tailles. Le défilement est à l’aide de hello PG. préc, PG. suiv, haut et bas clés, des intervalles différents pour chaque défilement.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>Document PDF (mixte) exécuté pendant environ 320 secondes
Un utilisateur lit un document PDF dans lequel il effectue des recherches de différentes manières à l’aide d’Adobe Acrobat Reader. document de Hello se compose des images de haute qualité (y compris des photographies), des tables, des graphiques simples et plusieurs polices de texte. utilisateur de Hello fait défiler vers l’arrière à deux des vitesses différentes et transfère à quatre formats différents de zoom (ajuster toopage, toowidth adaptée, 100 % et l’autre de votre choix). Hello Zoom garantit que le texte hello (police) effectue le rendu de différentes tailles. Le défilement est à l’aide de hello PG. préc, PG. suiv, haut et bas clés, des intervalles différents pour chaque défilement.

### <a name="flash-video-playback---run-for-180-seconds"></a>Lecture d’une vidéo au format Flash pendant environ 180 secondes
Un utilisateur consulte une vidéo au format Adobe Flash incorporée dans une page web. page web de Hello est stocké dans hello disque dur du serveur hôte de Session Bureau à distance de hello. Hello vidéo est lu dans Internet Explorer par un plug-in de lecteur incorporé.

Ce scénario présente des utilisateurs qui consultent le contenu multimédia de pages web. La plupart des données de salutation doit bo via VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Saisie à distance sur Word pendant environ 1 800 secondes
Un utilisateur tape un document au moyen d’une session Bureau à distance. Séquences de touches sont envoyées à partir du côté client de hello hello RDP session tooa du document dans Microsoft Word en cours d’exécution dans la session à distance de hello. Hello taux est un caractère de toutes les 250 ms (nombre total de 7050 caractères). 

Il s’agit d’un des scénarios les plus courants de hello pour un travailleur du savoir. Ce scénario teste la réactivité hello d’un utilisateur en tapant un processeur de travail modernes. Ce scénario est tooeven sensibles petites modifications dans l’utilisation de la bande passante.

## <a name="tracking-hello-test-results"></a>Suivi des résultats des tests hello
Vous pouvez utiliser hello suivant des scénarios de hello tooevaluate table dans votre environnement. Vous trouverez ci-dessous les données de salutation sont fins d’illustration uniquement - il peut être considérablement différent de ce que vous observez. 

Par souci de simplicité, nous supposons que tous les scénarios sont testés à l’aide de la résolution d’écran hello même 1920 x 1080 pixels, et les transports TCP sur un réseau avec une latence (différé de) sous réseau et 200 ms instabilité dans hello ms de 120 marque de 1 %.

Sur la table de hello :

* **Moyenne expérience** contient la bande passante réseau hello où la productivité des utilisateurs est peu affectée, mais n’exclut pas les problèmes de vidéo ou audio occasionnelles. système de Hello est en mesure de toorecover rapidement en tirant parti de la logique dynamique de hello. Hello réseau de bande passante estimations tentative tooguarantee hello qualité de l’expérience utilisateur hello.
  * **Problèmes notables (point d’arrêt)** contient la bande passante réseau hello où les utilisateurs peuvent remarquer des problèmes significatifs dans leur expérience, et leur productivité est affectée pour des périodes de temps mesurable. À ce stade, les algorithmes de RDP hello éprouvent et ne peut pas garantir la qualité de l’utilisateur hello d’expérience en raison de la bande passante réseau insuffisantes.
  * **Recommandé** contient la bande passante du réseau hello recommandée pour une bonne ou excellente expérience. Il s’agit généralement d’une étape supérieure à la valeur hello hello correspondant **moyenne expérience** colonne.
  * **Notes** inclut les observations et commentaires.

| Test | Expérience moyenne | Problèmes notables (point d’arrêt) | Bande passante réseau recommandée | Notes |
| --- | --- | --- | --- | --- |
| PowerPoint complexe avec animations |10 Mo/s |1 Mo/s |> 10 Mo/s, de préférence 100 Mo/s |À une vitesse de 1 Mo/s, de nombreuses animations sont perdues |
| Simple PowerPoint |5 Mo/s |256 Ko/s |10 Mo/s |À 256 Ko/s diapositives de hello chargement avec retard |
| Internet Explorer |10 Mo/s |1 Mo/s |> 10 Mo/s, de préférence 100 Mo/s |À une vitesse de 1 Mo/s, les vidéos web sont floues et hachées et le défilement rapide rencontre des problèmes |
| PowerPoint simple |1 Mo/s |256 Ko/s |5 Mo/s |À 256 Ko/s, il prend un certain temps page hello de tooload |
| PDF mixte |1 Mo/s |256 Ko/s |5 Mo/s |À 256 Ko/s de la page hello prend une quantité considérable de tooload de temps |
| Lecture de vidéo au format Flash |10 Mo/s |1 Mo/s |> 10 Mo/s, de préférence 100 Mo/s |1 Mo/s hello vidéo est grenue et certaines images sont supprimées. |
| Saisie à distance sur Word |256 Ko/s |128 Ko/s |1 Mo/s |À 256 Ko/s utilisateur peut remarquer des temps de hello entre les séquences de touches |

la bande passante du réseau tooevaluate hello par utilisateur, créez un mélange de hello au-dessus de scénarios et proportion correspondante de hello de bande passante réseau requis. Sélectionnez un numéro le plus élevé de hello nécessaire pour vos scénarios. Étant donné que les utilisateurs utilisent presque jamais le seul système de hello, envisagez une réserve pour les utilisateurs qui travaillent simultanément sur hello même réseau.

## <a name="learn-more"></a>En savoir plus
* [Estimation de l’utilisation de la bande passante réseau Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp : quelle est la corrélation entre la bande passante réseau et la qualité de l’expérience d’utilisation ?](remoteapp-bandwidthexperience.md)
* [Bande passante réseau Azure RemoteApp : instructions générales (si vous ne pouvez pas tester votre propre bande passante)](remoteapp-bandwidthguidelines.md)

