---
title: "prise en charge d’aaaHTTP/2 dans Azure CDN | Documents Microsoft"
description: En savoir plus sur la prise en charge de HTTP/2 et de CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Prise en charge de HTTP/2 dans Azure CDN

HTTP/2 est un tooHTTP/1.1\ révision majeure. Il fournit plus rapide d’expérience utilisateur améliorée, temps de réponse réduit et performances de site web, tout en conservant les méthodes HTTP familières hello, les codes d’état et sémantique. Bien que HTTP/2 est conçue toowork HTTP et HTTPS, de nombreux navigateurs web de client prennent uniquement en charge HTTP/2 sur TLS.

###<a name="http2-benefits"></a>Avantages de HTTP/2

avantages de Hello de HTTP/2 :

*   **Multiplexage et accès concurrentiel**

    Avec HTTP 1.1, effectuer plusieurs demandes de ressources nécessite plusieurs connexions TCP, et chaque connexion représente une surcharge qui a un impact sur les performances. HTTP/2 permet à plusieurs ressources toobe demandé sur une connexion TCP unique.

*   **Compression des en-têtes**

    Par la compression des en-têtes hello HTTP pour les ressources traitées, l’heure sur le câble de hello est sensiblement réduit.

*   **Dépendances de flux**

    Dépendances de flux de données permettent de client de hello tooindicate toohello server, qui ont la priorité des ressources.


##<a name="http2-browser-support"></a>Prise en charge de HTTP/2 par les navigateurs

Tous les navigateurs principaux hello ont implémenté la prise en charge HTTP/2 dans leur version actuelle. Non pris en charge des navigateurs seront automatiquement secours tooHTTP/1.1.

|Browser|Version minimale|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Activation de la prise en charge de HTTP/2 dans Azure CDN

La prise en charge HTTP/2 est actuellement active pour les profils **Azure CDN d’Akamai** et **Azure CDN de Verizon**. Aucune action supplémentaire n’est nécessaire de la part des clients.

##<a name="next-steps"></a>Étapes suivantes

avantages de hello toosee de HTTP/2 en action, consultez [cette démonstration d’Akamai](https://http2.akamai.com/demo).

toolearn plus de HTTP/2, visitez hello suivant des ressources :

*   [Page d’accueil de la spécification HTTP/2](https://http2.github.io/)
*   [Forum Aux Questions officiel de HTTP/2](https://http2.github.io/faq/)
*   [Informations sur HTTP/2 d’Akamai](https://http2.akamai.com/)

toolearn savoir plus sur les fonctionnalités disponibles du CDN Azure, consultez hello [vue d’ensemble du CDN Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).
