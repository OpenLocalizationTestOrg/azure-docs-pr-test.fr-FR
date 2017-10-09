---
title: "aaaLearn sur la vérification en deux étapes dans l’authentification Multifacteur Azure | Documents Microsoft"
description: "Quelle est l’authentification multifacteur Azure, pourquoi utiliser l’authentification Multifacteur, plus d’informations sur le client de l’authentification multifacteur hello et les différentes méthodes de hello et les versions disponibles. "
keywords: "Introduction tooMFA, vue d’ensemble de l’authentification multifacteur, quelle est l’authentification multifacteur"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a>Présentation d'Azure Multi-Factor Authentication
Vérification en deux étapes est une méthode d’authentification qui nécessite plus d’une méthode de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions. Elle fonctionne avec deux ou plusieurs de hello les méthodes de vérification suivantes :

* Un élément que vous connaissez (généralement un mot de passe)
* Un élément que vous possédez (un appareil de confiance qui n'est pas facilement dupliqué, comme un téléphone)
* Un élément vous concernant particulièrement (biométrie)

<center>![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/pword.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificats](./media/multi-factor-authentication/phone.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce](./media/multi-factor-authentication/smart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Carte à puce virtuelle](./media/multi-factor-authentication/vsmart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nom d’utilisateur et mot de passe](./media/multi-factor-authentication/cert.png)</center>

Azure Multi-Factor Authentication (MFA) est la solution de vérification en deux étapes de Microsoft. Azure MFA permet toodata d’accès de sauvegarde et d’applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une authentification forte au moyen de diverses méthodes de vérification, notamment les appels téléphoniques, l’envoi de SMS ou la vérification sur l’application mobile.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a>Pourquoi utiliser Azure Multi-Factor Authentication ?
Aujourd’hui, plus que jamais, les personnes sont de plus en plus connectées. Avec les Smartphones, tablettes, ordinateurs portables et PC, personnes ont plusieurs options sur comment ils vont tooconnect et restent connectés à tout moment. Ils peuvent accéder à leurs comptes et leurs applications où qu’ils soient, cela signifie qu’ils peuvent être plus productifs et mieux servir leurs clients.

L’authentification multifacteur Azure est un toouse facile, évolutive, et une solution fiable qui fournit une deuxième méthode d’authentification pour vos utilisateurs sont toujours protégés.

| ![TooUse simple](./media/multi-factor-authentication/simple.png) | ![Évolutif](./media/multi-factor-authentication/scalable.png) | ![Toujours protégé](./media/multi-factor-authentication/protected.png) | ![Fiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| **Toouse simple** |**Évolutif** |**Toujours protégé** |**Fiable** |

* **TooUse facile** -Azure multi-Factor Authentication est simple tooset des et utilisation. Hello une protection supplémentaire qui est fourni avec l’authentification multifacteur Azure permet aux utilisateurs toomanage leurs propres appareils. De plus, dans de nombreux cas elle peut être configurée de manière très simple.
* **Évolutive** -Azure multi-Factor Authentication utilise l’alimentation hello du cloud de hello et s’intègre à votre site AD et les applications personnalisées. Cette protection est étendue même tooyour des scénarios critiques, de haut volume.
* **Toujours protégé** -Azure multi-Factor Authentication fournit une authentification forte à l’aide de normes du secteur hello la plus élevées.
* **Fiable** : nous garantissons une disponibilité à 99,9 % d'Azure Multi-Factor Authentication. Hello service est considérée comme non disponible lorsqu’il est impossible de demandes de vérification tooreceive ou processus pour la vérification en deux étapes hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur le [fonctionnement d’Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)

- En savoir plus sur hello différents [versions et les méthodes de consommation pour l’authentification multifacteur Azure](multi-factor-authentication-versions-plans.md)
