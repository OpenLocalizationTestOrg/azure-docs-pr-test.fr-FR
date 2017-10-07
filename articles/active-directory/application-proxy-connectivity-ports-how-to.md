---
title: "ports de pare-feu aaaHow tooopen hello requises pour une application de Proxy d’Application | Documents Microsoft"
description: "Découvrez quels tooopen ports pour hello AD Azure Proxy d’Application toowork correctement"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Comment tooopen hello ports de pare-feu requises pour une application de Proxy d’Application

toosee une liste complète des ports de hello requis et de la fonction hello de chaque port, voir la section de configuration requise de hello Hello [documentation de Proxy d’Application](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Le proxy d’application utilise uniquement des ports de sortie.

Vous pouvez également vérifier si vous avez tous hello requis ports ouverts en ouvrant le hello [connecteur Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) à partir de votre réseau local. Un nombre plus élevé de coches vertes signifie une résilience accrue. 

## <a name="app-proxy-regions"></a>Régions du proxy d’application

Nous travaillons sur une méthode toolet connait de ces régions doit toobe verte pour vous. Pour l’instant, assurez-vous que toutes le sont. La région États-Unis du Centre est également requise, quelle que soit la région où vous vous trouvez.

toomake vraiment hello outil donne hello de bons résultats, veillez à :

-   Outil hello ouvert sur un navigateur à partir du serveur hello où vous avez installé le connecteur de hello.

-   Assurez-vous que les serveurs proxy ou pare-feu tooyour applicable connecteur sont également appliquées toothis page. Cela est possible dans Internet Explorer en accédant trop**paramètres**  - &gt; **Options Internet**  - &gt; **connexions**  - &gt; **Paramètres Lan**. Dans cette page, vous consultez le champ hello « Utiliser un Proxy Server pour votre réseau local ». Activez cette case et placez l’adresse du proxy hello dans le champ « Address » de hello.

## <a name="next-steps"></a>Étapes suivantes
[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
