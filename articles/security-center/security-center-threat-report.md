---
title: "aaaAzure rapport de centre de sécurité threat intelligence | Documents Microsoft"
description: "Ce document vous aide à rapports Intelligent menace de centre de sécurité toouse Azure pendant un toofind enquête plus d’informations sur une alerte de sécurité."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Rapport d’informations sur les menaces d’Azure Security Center
Ce document explique comment trouver des informations supplémentaires sur une menace ayant généré une alerte de sécurité dans les rapports d’informations sur les menaces d’Azure Security Center.

## <a name="what-is-a-threat-intelligence-report"></a>Qu’est-ce qu’un rapport d’informations sur les menaces ?
Détection des menaces de sécurité Center fonctionne en analysant les informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté. Il analyse cette information, corrélation souvent des informations provenant de plusieurs sources, les menaces tooidentify. Ce processus fait partie du centre de sécurité de hello [des fonctionnalités de détection](security-center-detection-capabilities.md).

Lorsqu’Azure Security Center identifie une menace, il déclenche une [alerte de sécurité](security-center-managing-and-responding-alerts.md), qui contient des informations détaillées sur un événement particulier, y compris des suggestions de correction. les équipes de réponse aux incidents tooassist examiner et corriger les menaces, centre de sécurité inclut un rapport de menace qui contient des informations sur les menaces hello qui a été détecté, y compris des informations telles que le :

* Identité ou associations des attaquants (si cette information est disponible)
* Objectifs des attaquants
* Campagnes d’attaque actuelles et historiques (si cette information est disponible)
* Tactiques, outils et procédures des attaquants
* Indicateurs de compromission (IoC) associés, tels que les URL et les hachages de fichier
* Victimology, qui est de l’industrie de hello et géographique prévalence tooassist vous pour déterminer si vos ressources Azure sont exposés
* Informations d’atténuation et de correction

> [!NOTE]
> Hello d’informations dans un rapport particulier varie ; niveau de Hello de détail est basé sur les activités et la récurrence hello les programmes malveillants.
>
>

Centre de sécurité comporte trois types de rapports de menace, lequel peuvent varier en fonction toohello attaque. rapports Hello disponibles sont :

* **Rapport sur le groupe d’activités** : fournit des informations détaillées sur les attaquants, leurs objectifs et leurs tactiques.
* **Rapport sur la campagne** : se concentre sur les détails des campagnes d’attaque spécifiques.
* **Rapport Résumé de la menace**: couvre tous les éléments hello dans les rapports de deux précédente hello.

Ce type d’information est très utile pendant hello [réponse aux incidents](security-center-incident-response.md) traiter, où il existe une source de hello toounderstand enquête en cours d’attaque de hello, les motivations de l’attaquant hello et ce que toodo toomitigate cela problème de déplacement vers l’avant.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Comment tooaccess hello rapport menace ?
Vous pouvez consulter vos alertes en cours en examinant hello **alertes de sécurité** vignette. Ouvrez hello portail Azure, puis suivez les étapes de hello ci-dessous toosee plus de détails sur chaque alerte :

1. Tableau de bord du centre de sécurité hello, vous verrez hello **alertes de sécurité** vignette.
2. Cliquez sur Bonjour vignette tooopen Bonjour **alertes de sécurité** panneau qui contient plus de détails sur les alertes hello et cliquez sur dans l’alerte de sécurité hello que vous souhaitez tooobtain plus d’informations sur les.

    ![Alertes de sécurité](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. Dans ce cas hello **suspectes processus exécuté** panneau affiche les détails de hello sur alerte hello comme indiqué dans la figure hello ci-dessous :

    ![Détails des alertes de sécurité](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. Hello d’informations disponibles pour chaque alerte de sécurité varie en fonction de type toohello d’alerte. Bonjour **rapports** champ que vous avez un lien toohello threat intelligence du rapport. Lorsque vous cliquez dessus, une autre fenêtre de navigateur s’affiche. Elle contient le fichier PDF.

   ![Sélection du stockage](./media/security-center-threat-report/security-center-threat-report-fig3.png)

À ce stade, vous pouvez télécharger hello PDF pour ce rapport et la lecture d’informations sur la sécurité de hello problème qui a été détecté et prendre des mesures en fonction des informations hello fournies.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris en quoi les rapports d’informations sur les menaces d’Azure Security Center peuvent vous être utiles lors de l’examen des alertes de sécurité. toolearn en savoir plus sur Azure Security Center, voir hello :

* [FAQ du Centre de sécurité Azure](security-center-faq.md). Trouver des questions fréquemment posées sur l’utilisation du service de hello.
* [Utilisation d’Azure Security Center pour la réponse aux incidents](security-center-incident-response.md)
* [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md)
* [Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md). Découvrez comment tooplan et comprendre les considérations de conception hello tooadopt Azure Security Center.
* [Gestion et répond toosecurity les alertes dans Azure Security Center](security-center-managing-and-responding-alerts.md). Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Gestion des incidents de sécurité dans Azure Security Center](security-center-incident.md)
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/). accédez à des billets de blog sur la sécurité et la conformité Azure.
