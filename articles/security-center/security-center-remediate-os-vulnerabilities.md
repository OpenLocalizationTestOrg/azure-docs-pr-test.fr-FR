---
title: "des vulnérabilités d’aaaRemediate du système d’exploitation dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** corriger le système d’exploitation des vulnérabilités **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Corriger les vulnérabilités du système d’exploitation dans Azure Security Center
Centre de sécurité Azure analyse tous les jours de votre système d’exploitation de l’ordinateur virtuel (VM) (système d’exploitation) pour les configurations qui pourrait rendre hello VM plus vulnérables tooattack et recommande la configuration change tooaddress ces vulnérabilités. Centre de sécurité vous recommande de résoudre les vulnérabilités lors de la configuration du système d’exploitation de votre machine virtuelle ne correspond pas à des règles de configuration recommandée de hello.

> [!NOTE]
> Pour plus d’informations sur les configurations spécifiques hello en cours d’analyse, consultez hello [liste des règles de configuration recommandée](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Ce document n'est pas un guide pas à pas.
>
>

1. Bonjour **recommandations** panneau, sélectionnez **les vulnérabilités du système d’exploitation corriger**.
   ![Remediate OS vulnerabilities][1]

    Hello **les vulnérabilités du système d’exploitation corriger** panneau s’ouvre et répertorie vos machines virtuelles avec des configurations de système d’exploitation qui ne correspondent pas hello les règles de configuration recommandée.  Pour chaque machine virtuelle, panneau de hello identifie :

   * **Échec de règles** --nombre hello de règles hello configuration de système d’exploitation de l’ordinateur virtuel a échoué.
   * **DERNIÈRE analyse** --hello date et heure que le centre de sécurité analysés dernière configuration de système d’exploitation de la machine virtuelle hello.
   * **ÉTAT** --hello l’état actuel de la vulnérabilité de hello :

     * Ouvrez : hello vulnérabilité n'a pas été traitée encore
     * En cours d’exécution : Une vulnérabilité de hello est actuellement appliquée, aucune action n’est requise par vous
     * Résolu : une vulnérabilité de hello a déjà été traitée (lorsque hello a été résolu, entrée de hello est grisée)
   * **GRAVITÉ** --toutes les vulnérabilités sont définies à gravité tooa basse, ce qui signifie une vulnérabilité doit être traitée, mais ne nécessite pas une attention immédiate.

2. Sélectionnez une machine virtuelle. Un panneau pour cette machine virtuelle s’ouvre et affiche les règles hello qui ont échoué.
   ![Règles de configuration ayant échoué][2]

3. Sélectionnez une règle. Dans cet exemple, nous allons sélectionner **Le mot de passe doit respecter des exigences de complexité**. Un panneau s’ouvre décrivant impact de règle et hello hello a échoué. Passez en revue les détails de hello et prendre en compte la façon dont les configurations de système d’exploitation sont appliquées.
  ![Description de la règle d’échec hello][3]

  Centre de sécurité utilise des identificateurs uniques de tooassign énumération CCE (Common Configuration) pour les règles de configuration. Hello informations suivantes est fournie sur ce panneau :

  - NOM : nom de règle
  - GRAVITÉ : valeur de gravité CCE (critique, important ou avertissement)
  - CCIED--Identificateur unique de CCE pour la règle de hello
  - DESCRIPTION : description de la règle
  - VULNÉRABILITÉ : explication de la vulnérabilité ou du risque si la règle n’est pas appliquée
  - IMPACT : impact sur l’activité lorsque la règle est appliquée
  - VALEUR attendue : Valeur de prévu lorsque le centre de sécurité analyse la configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello
  - OPÉRATION de règle : Des règles utilisées par le centre de sécurité lors de l’analyse de configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello
  - VALEUR réelle : La valeur retournée après l’analyse de configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello
  - RÉSULTAT DE L’ÉVALUATION : résultat de l’analyse : réussite ou échec

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello centre de sécurité « vulnérabilités de correction du système d’exploitation » de recommandation. Vous pouvez consulter le jeu de hello des règles de configuration [ici](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Centre de sécurité utilise des identificateurs uniques de tooassign CCE (Common Configuration Enumeration) pour les règles de configuration. Visitez hello [CCE](https://nvd.nist.gov/cce/index.cfm) site pour plus d’informations.

toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des ressources :

* [Plateformes prises en charge dans Azure Security Center](security-center-os-coverage.md) : répertorie les machines virtuelles Windows et Linux prises en charge.
* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) -en savoir comment les stratégies de sécurité tooconfigure pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) -en savoir comment toomonitor hello d’intégrité de vos ressources Azure.
* [Gestion et répond toosecurity alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) -en savoir comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) -en savoir comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) -Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
