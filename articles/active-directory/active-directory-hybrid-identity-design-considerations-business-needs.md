---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les besoins de l’identité | Documents Microsoft"
description: "Identifier les besoins hello entreprise vous amènent toodefine les exigences de hello pour la conception d’identité hello hybride."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Déterminer les besoins d’identité pour votre solution d’identités hybrides
Hello de première étape de la conception d’une solution d’identité hybride consiste toodetermine des exigences de hello pour l’organisation de l’entreprise hello qui va exploiter cette solution.  Identité hybride démarre en tant qu’un rôle de prise en charge (il prend en charge toutes les autres solutions de cloud grâce à l’authentification) et est mis sur les fonctionnalités nouvelles et intéressantes tooprovide nouvelles charges de travail pour les utilisateurs de déverrouiller.  Ces charges de travail ou les services que vous souhaitez tooadopt pour vos utilisateurs détermine hello besoins en termes de conception d’identité hello hybride.  Le besoin de ces services et les charges de travail identité hybride de tooleverage à la fois localement et dans le cloud de hello.  

Vous devez toogo sur ces aspects clés de hello entreprise toounderstand qu’il est désormais une exigence et plans de société hello pour hello futures. Si vous n’avez pas visibilité hello de stratégie à long terme hello de conception d’identité hybride, sans doute que votre solution ne sera pas évolutive hello des besoins grandissants et.   T diagramme ci-dessous montre un exemple d’un hybride identité hello d’architecture et de charges de travail qui sont en cours de déverrouillage pour les utilisateurs. Il s’agit simplement d’un exemple de toutes les possibilités de nouveau hello qui peuvent être déverrouillés et remis avec une stratégie d’identité hybride solide. 

Certains composants qui font partie de l’architecture d’identité hybride hello![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Déterminer les besoins métier
Chaque entreprise a des exigences différentes, même si ces sociétés font partie de hello même secteur, les besoins réels hello peuvent varier. Vous pouvez toujours tirer parti des meilleures pratiques du secteur de hello, mais il est finalement besoins hello entreprise vous amènent toodefine les exigences de hello pour la conception d’identité hello hybride. 

Assurez-vous de questions suivantes de hello tooanswer tooidentify votre entreprise a besoin :

* Votre entreprise cherche toocut coûts opérationnels informatiques ?
* Votre entreprise recherche les ressources de cloud toosecure (applications SaaS, infrastructure) ?
* Est votre entreprise recherche toomodernize votre service informatique ?
  * Sont vos utilisateurs plus mobiles et exigeantes informatique toocreate exceptions dans votre réseau de périmètre tooallow autre type de trafic tooaccess les différentes ressources ?
  * Votre entreprise a-t-elle des applications héritées qui nécessaires toobe publié les utilisateurs modernes toothese mais ne sont pas facile toorewrite ?
  * Votre entreprise devez tooaccomplish toutes ces tâches et le placer sous contrôle de hello même temps ?
* Est votre entreprise recherche les identités des utilisateurs toosecure et réduire les risques en rassemblant de nouveaux outils qui tirent parti d’expertise hello de Azure sécurité expertise localement Microsoft ?
* Est votre entreprise lors de la tentative tooget rid de hello redoutée comptes « externes » en local et de les déplacer cloud toohello où ils ne sont plus une menace dormante à l’intérieur de votre environnement local ?

## <a name="analyze-on-premises-identity-infrastructure"></a>Analyser votre infrastructure d’identité locale
Maintenant que vous avez une idée concernant vos besoins d’entreprise, vous devez tooevaluate votre infrastructure d’identité locale. Cette évaluation est importante pour la définition hello spécifications techniques toointegrate votre système de gestion toohello cloud identité identité solution actuel. Vérifiez que hello tooanswer suivant questions :

* Quelle solution d’authentification et d’autorisation votre entreprise utilise-t-elle en local ? 
* Votre entreprise dispose-t-elle actuellement de services de synchronisation en local ?
* Votre entreprise utilise-t-elle des fournisseurs d’identité tiers ?

Vous devez également toobe prenant en charge des services de cloud computing hello peut-être votre entreprise. Effectuer une intégration évaluation toounderstand hello actuel avec ce modèle, les modèles IaaS ou PaaS dans votre environnement est très important. Vérifiez que hello tooanswer suivante des questions au cours de cette évaluation :

* Votre entreprise dispose-t-elle d’une intégration avec un fournisseur de services cloud ?
* Le cas échéant, quels sont les services utilisés ?
* Cette intégration est-elle actuellement en production ou s’agit-il d’un pilote ?

> [!NOTE]
> Si vous ne dispose d’un mappage précis de toutes vos applications et services de cloud computing, vous pouvez utiliser l’outil de Cloud App Discovery hello. Cet outil peut fournir à votre service informatique une visibilité sur toutes les applications cloud d’entreprise et clientes de votre organisation. Qui rend plus facile que jamais toodiscover shadow IT dans votre organisation, notamment des détails sur les modèles d’utilisation et de tous les utilisateurs l’accès à vos applications cloud. tooget démarré consultez [de Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Évaluer les exigences d’intégration des identités
Ensuite, vous devez les exigences d’intégration tooevaluate hello identité. Cette évaluation est important toodefine hello prescriptions comment doit authentifier les utilisateurs, aspect de présence de l’organisation hello dans le cloud de hello, comment les organisation hello permettra d’autorisation et l’expérience utilisateur quels hello est continu toobe. Vérifiez que hello tooanswer suivant questions :

* Votre organisation va-t-elle utiliser la fédération, l’authentification standard, ou les deux ?
* La fédération est-elle obligatoire ?  En raison de suivant de hello :
  * Authentification unique Kerberos
  * Votre entreprise possède des applications locales (générées en interne ou tierces) qui utilisent SAML ou des fonctionnalités de fédération similaires.
  * MFA via des cartes à puce RSA SecurID, etc.
  * Règles d’accès client permettant de traiter des questions hello ci-dessous :
    1. Puis-je bloquer tous les accès externe tooOffice 365 basées sur l’adresse IP de hello du client de hello ?
    2. Puis-je bloquer tous les accès externe tooOffice 365, à l’exception d’Exchange ActiveSync ?
    3. Puis-je bloquer tous les accès externe tooOffice 365, à l’exception des applications basée sur navigateur (OWA, simulé)
    4. Puis-je bloquer tous les accès externe tooOffice 365 pour les membres des groupes AD désignés
* Préoccupations relatives à la sécurité et à l’audit
* Investissement existant déjà dans l’authentification fédérée
* Le nom que notre organisation va utiliser pour le domaine dans le cloud de hello ?
* Organisation de hello dispose d’un domaine personnalisé ?
  1. Ce domaine est-il public et facilement vérifiable via DNS ?
  2. Si elle n’est pas le cas, puis vous avez un domaine public qui peut être utilisé tooregister un UPN de remplacement dans Active Directory ?
* Sont des identificateurs d’utilisateurs hello cohérent pour la représentation sous forme de cloud ? 
* Organisation de hello dispose d’applications qui nécessitent une intégration avec les services cloud ?
* Organisation de hello dispose de plusieurs domaines et tous les utilise l’authentification standard ou fédérée ?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Évaluer des applications exécutées dans votre environnement
Maintenant que vous avez une idée sur votre site et infrastructure de cloud computing, vous devez les applications de hello tooevaluate qui s’exécutent dans ces environnements. Cette évaluation est importante toodefine hello spécifications techniques toointegrate ces système de gestion des applications toohello cloud identité. Vérifiez que hello tooanswer suivant questions :

* Où nos applications vont-elles résider ?
* Les utilisateurs vont-ils accéder aux applications locales ?  Dans le cloud de hello ? Ou les deux ?
* Existe-t-il des plans tootake hello existante des charges de travail et les déplacer toohello cloud ?
* Existe-t-il des plans toodevelop nouvelles applications qui résident localement ou dans hello cloud qui utilisera l’authentification cloud ?

## <a name="evaluate-user-requirements"></a>Évaluer les exigences des utilisateurs
Vous devez également les besoins des utilisateurs tooevaluate hello. Cette évaluation est étapes hello toodefine important qui seront nécessaires pour l’intégration et aider les utilisateurs que leur transition toohello cloud. Vérifiez que hello tooanswer suivant questions :

* Les utilisateurs vont-ils accéder aux applications en local ?
* Les utilisateurs accèdent aux applications dans le cloud de hello ?
* Comment les utilisateurs généralement connexion tootheir environnement local ?
* Comment les utilisateurs connectez-vous toohello sera cloud ?

> [!NOTE]
> Notez que tootake de chacune des réponses et comprendre hello sous-tend hello. [Déterminer les besoins de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) passe en revue les options hello disponibles et pour et le contre de chaque option.  En répondant à chacune de ces questions, vous sélectionnerez l’option correspondant le mieux à vos besoins métier.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les exigences de synchronisation de répertoire](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

