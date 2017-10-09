---
title: "mises à jour du système d’aaaApply dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** appliquer les mises à jour du système ** et ** redémarrer après l’application de mises à jour du système **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Appliquer les mises à jour système dans Azure Security Center
Azure Security Center recherche quotidiennement les mises à jour manquantes du système d’exploitation sur les machines virtuelles Windows et Linux. Security Center récupère une liste des mises à jour de sécurité et critiques disponibles dans Windows Update ou WSUS (Windows Server Update Services), selon le service configuré sur les machines virtuelles Windows.  Centre de sécurité vérifie également pour les dernières mises à jour de hello dans les systèmes Linux. S’il manque une mise à jour système sur votre machine virtuelle, Security Center vous recommande de l’appliquer.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **appliquer les mises à jour système**.

   ![Appliquer des mises à jour système][1]
2. Hello **appliquer les mises à jour système** panneau s’ouvre en affichant une liste de mises à jour système manquantes de machines virtuelles. Sélectionnez une machine virtuelle.

   ![Sélectionner une machine virtuelle][2]
3. Un panneau s’ouvre et affiche une liste des mises à jour manquantes sur cette machine. Sélectionnez une mise à jour système. Dans cet exemple, sélectionnons KB3156016.

   ![Mises à jour de sécurité manquantes][3]

4. Suivez les étapes de hello Bonjour **mise à jour de sécurité** panneau tooapply hello mise à jour manquante.

   ![Mise à jour de sécurité][4]

## <a name="reboot-after-system-updates"></a>Redémarrer après l’application des mises à jour système
1. Retourner toohello **recommandations** panneau. Une fois que vous avez appliqué les mises à jour système, une nouvelle entrée est générée, appelée **Redémarrer après l’application des mises à jour système**. Cette entrée permet de savoir que vous avez besoin de processus de hello toocomplete tooreboot hello machine virtuelle de l’application de mises à jour du système.

   ![Redémarrer après l’application des mises à jour système][5]
2. Sélectionnez **Redémarrer après l’application des mises à jour système**. Cette opération ouvre **un redémarrage est en attente toocomplete les mises à jour système** panneau affiche la liste des ordinateurs virtuels que vous avez besoin de toorestart toocomplete hello applique le processus de mises à jour du système.

   ![Redémarrage en attente][6]

Redémarrez hello machine virtuelle à partir de processus de hello toocomplete Azure.

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
