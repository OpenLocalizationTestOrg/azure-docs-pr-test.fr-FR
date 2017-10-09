---
title: "aaaHandling les alertes de sécurité dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous aide aux incidents de sécurité toouse Azure Security Center fonctionnalités toohandle."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Gestion des incidents de sécurité dans Azure Security Center
Triage et examen des alertes de sécurité peuvent être fastidieuse pour les analystes en sécurité même hello expérimentés, et pour la plupart se tooeven difficile de savoir où toobegin. À l’aide de [analytique](security-center-detection-capabilities.md) tooconnect les informations de hello entre distinctes [alertes de sécurité](security-center-managing-and-responding-alerts.md), centre de sécurité peut vous fournir une vue unique d’une campagne d’attaque et que tous les Hello connexes alertes – vous pouvez comprendre rapidement les intrus de hello actions a duré et quelles ressources ont été affectés.

Ce document explique comment toouse sécurité fonctionnalité disponible dans le centre de sécurité tooassist vous avertir des incidents de sécurité.

## <a name="what-is-a-security-incident"></a>Qu’est-ce qu’un incident de sécurité ?
Dans le Centre de sécurité, un incident de sécurité est un regroupement de toutes les alertes d’une ressource correspondant à des modèles de [chaîne de destruction](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Incidents apparaissent dans hello [alertes de sécurité](security-center-managing-and-responding-alerts.md) vignette et lame. Un Incident indiquent liste hello d’alertes associées, ce qui permet de vous tooobtain plus d’informations sur chaque occurrence.

## <a name="managing-security-incidents"></a>Gestion des incidents de sécurité
Vous pouvez examiner les incidents de sécurité actuel en examinant hello sécurité alertes vignette. Accès hello portail Azure et suivez les étapes de hello ci-dessous toosee plus de détails sur chaque incident de sécurité :

1. Tableau de bord du centre de sécurité hello, vous verrez hello **alertes de sécurité** vignette.

    ![Vignette Alertes de sécurité dans le Centre de sécurité](./media/security-center-incident/security-center-incident-fig1.png)

2. Cliquez sur cette tooexpand vignette il et si un incident de sécurité est détectée, elle s’affiche sous le graphique d’alertes de sécurité hello comme indiqué ci-dessous :

    ![Incident de sécurité](./media/security-center-incident/security-center-incident-fig2.png)

3. Remarquez que description de l’incident hello sécurité comporte une icône différente par rapport à tooother alertes. Cliquez sur cette tooview plus d’informations sur cet incident.

    ![Incident de sécurité](./media/security-center-incident/security-center-incident-fig3.png)

4. Sur hello **incident** panneau s’affiche en plus des détails sur cet incident de sécurité, notamment sa description complet, sa gravité (qui dans ce cas est élevée), son état actuel (dans ce cas, il est toujours *active*, ce qui implique l’utilisateur de hello n’a pas mis un tooit action - cela, avec le bouton droit sur l’incident hello Bonjour **alertes de sécurité** panneau), hello effectuées sur la ressource (dans ce cas *VM1*), hello des étapes de mise à jour d’incident de hello et dans le volet du bas hello vous avez des alertes hello qui ont été inclus dans cet incident. Si vous souhaitez tooobtain plus d’informations sur chaque alerte, cliquez sur elle et un autre panneau s’ouvre, comme indiqué ci-dessous :

    ![Incident de sécurité](./media/security-center-incident/security-center-incident-fig4.png)

Hello plus d’informations sur ce panneau varie en fonction toohello alerte. Lecture [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) pour plus d’informations sur la façon de toomanage ces alertes. Voici quelques considérations importantes concernant cette fonctionnalité :

* Un nouveau filtre vous permet de toocustomize que votre tooIncident vue uniquement, les alertes uniquement, ou les deux.
* Hello même alerte peut exister en tant que partie d’un Incident (le cas échéant), ainsi que les toobe visible sous la forme d’une alerte autonome.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment toouse hello fonctionnalité incident de sécurité dans le centre de sécurité. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [La gestion et de répondre toosecurity des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)
* [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md)
* [Guide des opérations et de planification du Centre de sécurité Azure](security-center-planning-and-operations-guide.md)
* [La gestion et de répondre toosecurity des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)
* [Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/): trouvez des billets de blog sur la sécurité et la conformité Azure.
