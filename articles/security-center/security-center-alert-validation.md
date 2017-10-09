---
title: "aaaAlerts Validation dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous permet d’alertes de sécurité toovalidate hello dans Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a>Validation des alertes dans Azure Security Center
Ce document vous permet d’apprendre comment tooverify si votre système est configuré correctement pour les alertes du centre de sécurité Azure.

## <a name="what-are-security-alerts"></a>Que sont les alertes de sécurité ?
Centre de sécurité automatiquement collecte, analyse et intègre des données de journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire connectés, comme les solutions de protection de pare-feu et de point de terminaison, toodetect et toothreats vous alerte. Lecture [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) pour plus d’informations sur les alertes de sécurité et en lecture [présentation des alertes de sécurité dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn plus hello différents types d’alertes.

## <a name="alert-validation"></a>Validation de l’alerte
Une fois que l’agent de centre de sécurité est installé sur votre ordinateur, suivez les étapes de hello ci-dessous à partir de l’ordinateur de hello ressource de hello attaqué toobe d’alerte de hello :

1. Copiez le bureau de l’ordinateur d’un exécutable (par exemple calc.exe) toohello ou autre répertoire de commodité.
2. Renommez ce fichier trop**ASC_AlertTest_662jfi039N.exe**.
3. Ouvrez l’invite de commandes hello et exécutez ce fichier avec un argument (simplement un nom d’argument FAUX), telle que : *ASC_AlertTest_662jfi039N.exe - foo*
4. Patientez 5 minutes too10 et ouvrez les alertes du centre de sécurité. Il vous devez rechercher une alerte toofollowing similaire une :

    ![Validation de l’alerte](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

Lorsque vous parcourez cette alerte, vérifiez que champ hello Arguments l’audit activé apparaît comme true. S’il affiche la valeur false, vous devez les arguments de ligne de commande tooenable l’audit. Vous pouvez activer cette option à l’aide de hello de ligne de commande suivante :

*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*


## <a name="see-also"></a>Voir aussi
Cet article introduit le processus de validation toohello alertes. Maintenant que vous êtes familiarisé avec cette validation, essayez hello suivant des articles :

* [Gestion et répond toosecurity les alertes dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Découvrez comment toomanage des alertes et des incidents de toosecurity répondre dans le centre de sécurité.
* [Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md). Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Présentation des alertes de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). En savoir plus sur hello différents types d’alertes de sécurité.
* [Guide de résolution des problèmes d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Découvrez comment tootroubleshoot commun problèmes dans le centre de sécurité. 
* [FAQ du Centre de sécurité Azure](security-center-faq.md). Trouver des questions fréquemment posées sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/). accédez à des billets de blog sur la sécurité et la conformité Azure.

