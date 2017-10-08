---
title: "l’installation d’aaaProblem hello Agent connecteur Proxy d’Application | Documents Microsoft"
description: "Comment tootroubleshoot les problèmes qui vous pouvez face lors de l’installation hello Agent connecteur Proxy d’Application"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problème d’installation hello Agent connecteur Proxy d’Application

Microsoft AAD Application Proxy Connector est un composant de domaine interne qui utilise la connectivité de connexions sortantes tooestablish hello du domaine interne de hello cloud point de terminaison disponible toohello.

## <a name="general-problem-areas-with-connector-installation"></a>Problèmes généraux avec l’installation du connecteur

En cas d’échec de l’installation de hello d’un connecteur, cause première hello fait généralement partie de hello suivant de zones :

1.  **Connectivité** – toocomplete une installation réussie, hello tooregister de besoins nouveau connecteur et établir les propriétés d’approbation futures. Pour cela, en vous connectant toohello service de cloud de Proxy d’Application AAD.

2.  **Établissement d’approbation** – nouveau connecteur de hello crée un certificat auto-signé et inscrit toohello cloud service.

3.  **L’authentification de l’administration de hello** – pendant l’installation, utilisateur de hello doit fournir des informations d’identification administrateur installation du connecteur toocomplete hello.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Vérifiez que le service de Proxy d’Application Cloud toohello de connectivité et de la page de Microsoft Login

**Objectif :** Vérifiez que l’ordinateur connecteur hello peut se connecter de point de terminaison toohello AAD Application Proxy d’inscription ainsi que la page de connexion de Microsoft.

1.  Ouvrir un toohello de navigateur et allez suivant la page web : <https://aadap-portcheck.connectorporttest.msappproxy.net> et vérifiez que tooCentral de connectivité hello des États-Unis et l’utilisation de centres de données est des États-Unis avec les ports 9090 et 9091.

2.  Si un de ces ports ne réussit pas (ne dispose pas une coche verte), vérifiez que hello pare-feu ou proxy du serveur principal a \*. msappproxy.net avec ports 9090 et 9091 définies correctement.

3.  Ouvrez un navigateur (onglet séparé) et accédez toohello suivant la page web : <https://login.microsoftonline.com>, assurez-vous que vous pouvez vous connecter toothat page.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Vérification de la prise en charge du certificat de confiance du proxy d’application par la machine et les composants principaux

**Objectif :** Vérifiez qu’ordinateur de connecteur hello, de pare-feu et de proxy de serveur principal peuvent prendre en charge de certificat hello créé par le connecteur hello pour approbation ultérieure.

>[!NOTE]
>connecteur de Hello tente toocreate un certificat SHA512 est pris en charge par TLS 1.2. Si l’ordinateur de hello ou de proxy et de pare-feu de serveur principal hello ne prend pas en charge TLS 1.2, hello installation d’échouer.
>
>

**problème de hello tooresolve :**

1.  Vérifiez l’ordinateur de hello prend en charge TLS 1.2 – les versions de toutes les fenêtres après 2012 R2 doivent prendre en charge TLS 1.2. Si votre ordinateur de connecteur à partir d’une version de 2012 R2 ou les avant, assurez-vous que hello Kbits/s suivants sont installés sur l’ordinateur de hello : <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Contactez votre administrateur réseau et demander tooverify que hello principal proxy et pare-feu ne bloquent pas SHA512 pour le trafic sortant.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Vérifiez qu’admin est utilisé tooinstall hello connecteur

**Objectif :** Vérifiez que cet utilisateur hello qui tente de connecteur de hello tooinstall est un administrateur disposant des informations d’identification correctes. Actuellement, les utilisateurs hello doivent être un administrateur global pour hello installation toosucceed.

**informations d’identification de tooverify hello sont correctes :**

Vous connecter trop<https://login.microsoftonline.com> et utilisation hello les mêmes informations d’identification. Vérifiez que hello connexion est établie. Vous pouvez vérifier le rôle d’utilisateur hello en accédant trop**Azure Active Directory**  - &gt; **utilisateurs et groupes**  - &gt; **tous les utilisateurs**. 

Sélectionnez votre compte d’utilisateur, puis « rôle active » dans le menu résultant de hello. Vérifiez que ce rôle sélectionné hello est « Administrateur général ». Si vous êtes tooaccess impossible des hello pages le long de ces étapes, vous n’êtes pas un administrateur global.

## <a name="next-steps"></a>Étapes suivantes
[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
