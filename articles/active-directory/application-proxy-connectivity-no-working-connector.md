---
title: "groupe de connecteurs aaaNo travail trouvé pour une application de Proxy d’Application | Documents Microsoft"
description: "Résoudre les problèmes que vous pouvez rencontrer quand il n’existe aucun travail connecteur dans un groupe de connecteurs pour votre application avec hello Proxy d’Application Azure AD"
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
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Aucun groupe de connecteurs en fonctionnement n’est disponible pour une application de proxy d’application

Cet article vous vous tooresolve hello problèmes rencontrés quand il n’est pas un connecteur détecté pour une application de Proxy d’Application intégré à Azure Active Directory.

## <a name="overview-of-steps"></a>Vue d’ensemble des étapes
S’il n’existe aucun travail connecteur dans un groupe de connecteurs pour votre application, il existe quelques problème de hello tooresolve façons :

-   Si vous n’avez aucun connecteur de groupe de hello, vous pouvez :

    -   Télécharger un nouveau connecteur sur serveur local à droite de hello et lui attribuer le groupe de toothis

    -   Déplacez un connecteur actif dans hello

-   Si vous n’avez aucun connecteur active dans le groupe de hello, vous pouvez :

    -   Identifier la raison hello que votre connecteur est inactif et résoudre

    -   Déplacez un connecteur actif dans hello

tooknow suivantes, laquelle est problème de hello, ouvrir le menu de « Proxy d’Application » hello dans votre Application et examinez le message d’avertissement hello groupe de connecteurs. Il spécifier soit hello a besoin au moins un connecteur (vous avez aucun groupe de hello) ou qu’il ne dispose d’aucun connecteur active (même si vous avez probablement connecteurs inactifs).

   ![Sélection du groupe de connecteurs dans le portail Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Pour plus d’informations sur chacune de ces options, consultez la section correspondante de hello ci-dessous. Chacun de ces part du principe que vous démarrez à partir de la page de gestion du connecteur hello. Si vous examinez le message d’erreur hello ci-dessus, vous pouvez accéder toothis page en cliquant sur le message d’avertissement hello. Sinon, ce sont accessibles en accédant trop**Azure Active Directory**, en cliquant sur **des Applications d’entreprise**, puis **le Proxy d’Application.**

   ![Gestion du groupe de connecteurs dans le portail Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Télécharger un nouveau connecteur

toodownload un nouveau connecteur, utiliser le bouton de « Télécharger le connecteur » hello en hello haut hello.

besoins de connecteur hello Remarque toobe installé sur un ordinateur avec l’application de ligne de vue directe toohello principale et est généralement placé sur hello même serveur que l’application hello. Après avoir téléchargé, hello connecteur doit apparaître dans ce menu. Cliquez sur le connecteur de hello et utilisez hello « Groupe de connecteurs » liste déroulante toomake qu’il appartient toohello des groupes appropriés. Enregistrez les modifications hello.

   ![Téléchargez le connecteur de hello de hello portail Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Déplacer un connecteur

Si vous avez un connecteur actif qui doit appartenir toohello groupe et qui possède l’application de ligne de vue toohello cible principale, vous pouvez déplacer hello connecteur dans le groupe de hello attribué. toodo, cliquez sur hello connecteur. Dans le champ de « Groupe de connecteurs » hello, utilisez groupe approprié du hello hello tooselect de liste déroulante, cliquez sur Enregistrer.

## <a name="resolve-an-inactive-connector"></a>Résoudre le problème d’un connecteur inactif

Si hello uniquement connecteurs dans le groupe de hello sont inactives, ils sont susceptibles de sur un ordinateur qui n’effectue pas aient tous les ports nécessaires hello est débloqué.

consultez les ports hello document de résolution des problèmes pour plus d’informations sur l’examen de ce problème.

## <a name="next-steps"></a>Étapes suivantes
[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)


