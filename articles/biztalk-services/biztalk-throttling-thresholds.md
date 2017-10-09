---
title: aaaLearn sur la limitation dans BizTalk Services | Documents Microsoft
description: "En savoir plus sur les seuils de limitation et les comportements qui s'ensuivent lors de l'exécution pour BizTalk Services. La limitation est basée sur l'utilisation de la mémoire et le nombre de messages. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>Limitation BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Les Services BizTalk Azure implémente la basée sur les deux conditions de limitation de service : numéro hello et l’utilisation de mémoire de traitement de messages simultanés. Cette rubrique répertorie les seuils de limitation de hello et décrit le comportement d’exécution hello lorsqu’une condition de limitation se produit.

## <a name="throttling-thresholds"></a>Seuils de limitation
Hello tableau ci-dessous répertorie hello limitation source et les seuils :

|  | Description | Seuil minimum | Seuil maximum |
| --- | --- | --- | --- |
| Mémoire |Pourcentage de la mémoire système totale disponible/PageFileBytes (octets de fichier de page). <p><p>PageFileBytes disponible totale est d’environ 2 fois hello RAM du système de hello. |60 % |70 % |
| Traitement de message |Nombre de messages traités simultanément |40 * nombre de cœurs |100 * nombre de cœurs |

Lorsqu’un seuil élevé est atteint, Azure BizTalk Services démarre toothrottle. La limitation s’arrête lorsque hello faible est atteint. Par exemple, votre service utilise 65 % de la mémoire système. Dans ce cas, le service de hello ne limite pas. Votre service monte à 70 % d'utilisation de mémoire système. Dans ce cas, service de hello limite et continue toothrottle jusqu'à ce que le service de hello utilise la mémoire de système de 60 % (seuil faible).

Azure BizTalk Services effectue le suivi hello (état normal et l’état d’accélérée) d’état de limitation et hello durée de limitation.

## <a name="runtime-behavior"></a>Comportement d'exécution
Quand Azure BizTalk Services entre dans un état de limitation, hello événements suivants se produisent :

* La limitation s'effectue par instance de rôle. Par exemple :<br/>
  L'instance RoleInstanceA est limitée. L'instance RoleInstanceB ne l'est pas. Dans ce cas, les messages dans RoleInstanceB sont traités normalement. Messages dans RoleInstanceA sont ignorés et échouent avec hello l’erreur suivante :<br/><br/>
  **Le serveur est occupé. Réessayez.**<br/><br/>
* Les sources d'extraction cessent d'interroger et de télécharger les messages. Par exemple : <br/>
  Un pipeline extrait les messages depuis une source FTP externe. instance de rôle Hello effectuant l’extraction de hello Obtient dans un état de limitation. Dans ce cas, le pipeline de hello arrête le téléchargement des messages supplémentaires jusqu'à ce que l’instance de rôle hello arrête la limitation.
* Une réponse est envoyée toohello client pour le client de hello peut renvoyer le message de type hello.
* Vous devez attendre jusqu'à ce que la limitation de hello est résolue. Plus précisément, vous devez attendre jusqu'à ce que hello faible est atteint.

## <a name="important-notes"></a>Remarques importantes
* Il n'est pas possible de désactiver la limitation.
* Il n'est pas possible de modifier les seuils de limitation.
* La limitation est déployée sur l'ensemble du système.
* Hello, serveur de base de données SQL Azure a également la limitation intégrés.

## <a name="additional-azure-biztalk-services-topics"></a>Autres rubriques Azure BizTalk Services
* [Lors de l’installation Bonjour Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Didacticiels : Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Voir aussi
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Tableau comparatif des états d'approvisionnement BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Sauvegarde et restauration de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Nom et clé de l'émetteur dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

