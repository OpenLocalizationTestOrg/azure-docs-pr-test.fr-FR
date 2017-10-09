---
title: "aaaAzure analyse la vue d’ensemble et de gestion de la sécurité | Documents Microsoft"
description: " Azure fournit tooaid de mécanismes de sécurité dans la gestion de hello et la surveillance des services cloud Azure et les ordinateurs virtuels.  Cet article fournit une vue d’ensemble de ces fonctionnalités et services clés de sécurité. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Présentation de la gestion et surveillance de la sécurité Azure
Azure fournit tooaid de mécanismes de sécurité dans la gestion de hello et la surveillance des services cloud Azure et les ordinateurs virtuels. Cet article fournit une vue d’ensemble de ces fonctionnalités et services clés de sécurité. Des liens sont fournis tooarticles qui fournissent des détails de chaque afin d’en savoir plus.

Hello la sécurité de vos services de cloud de Microsoft est un partenariat et un partage des responsabilités entre vous et Microsoft. Responsabilité partagée signifie que Microsoft est chargé de hello Microsoft Azure et de la sécurité physique de ses centres de données (à l’aide des protections de sécurité telles que les portes d’entrée de badge verrouillé, clôtures et gardes). En outre, Azure fournit des niveaux élevés de sécurité de cloud en couche logicielle hello qui répond à la sécurité de hello, de confidentialité et de conformité de ses clients exigeants.

Vous êtes propriétaire de vos données et les identités, les responsabilités hello pour la protection, sécurité hello de vos ressources locales et sécurité hello des composants de cloud que vous contrôlez. Microsoft fournit avec toohelp de contrôles et des fonctions de sécurité que vous protégez vos données et applications. Le degré de responsable de la sécurité est basée sur le type hello du service cloud.

Hello suivant le graphique résume le solde hello de responsabilité pour le client Microsoft et hello.

![Responsabilité partagée][1]

Pour aller plus loin sur la gestion de la sécurité, consultez [Gestion de la sécurité dans Azure](azure-security-management.md).

Voici hello principales fonctionnalités toobe abordée dans cet article :

* Contrôle d’accès en fonction du rôle
* Logiciel anti-programme malveillant
* Azure Multi-Factor Authentication
* ExpressRoute
* Passerelles de réseau virtuel
* Privileged Identity Management
* Identity Protection
* Centre de sécurité

## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle
Le contrôle d’accès en fonction du rôle (RBAC) Azure offre une gestion précise de l’accès pour les ressources Azure. À l’aide de RBAC, vous pouvez quantité d’allocation de personnes uniquement hello d’accès dont ils ont besoin tooperform leur travail.  RBAC peut également vous aider à vous assurer que lorsque les utilisateurs quittent l’organisation de hello ils perdent tooresources d’accès dans le cloud de hello.

En savoir plus :

* [Blog de l’équipe Active Directory sur le RBAC](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Logiciel anti-programme malveillant
Avec Azure, vous pouvez utiliser le logiciel anti-programme malveillant à partir des fournisseurs de sécurité majeures telles que Microsoft, Symantec, Trend Micro, McAfee et Kaspersky toohelp protéger vos machines virtuelles à partir de fichiers malveillants, de logiciels de publicité et d’autres menaces.

Microsoft Antimalware offre que Hello de capacité tooinstall un agent de logiciel anti-programme malveillant pour des ordinateurs virtuels et les rôles PaaS. En fonction de System Center Endpoint Protection, cette fonctionnalité met local ayant fait leurs preuves cloud de toohello de technologie de sécurité.

Nous vous proposons d’intégration en profondeur pour de tendance [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ et [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ produits Bonjour plateforme Azure. DeepSecurity est une solution Antivirus et SecureCloud une solution de chiffrement. DeepSecurity est déployé sur des machines virtuelles à l’aide d’un modèle d’extension. À l’aide d’interface utilisateur du portail hello et PowerShell, vous pouvez choisir toouse DeepSecurity à l’intérieur de nouveaux ordinateurs virtuels qui sont en cours lancés ou des machines virtuelles existantes qui sont déjà déployées.

Symantec Endpoint Protection (SEP) est également pris en charge sur Azure. Grâce à l’intégration de portail, les clients peuvent indiquer qu’ils ont l’intention toouse SEP dans une machine virtuelle. SEP peut être installé sur un tout nouveau VM via hello portail Azure, ou peut être installé sur un ordinateur virtuel existant, à l’aide de PowerShell.

En savoir plus :

* [Déploiement de solutions anti-programmes malveillants sur des machines virtuelles Azure (en anglais)](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Microsoft Antimalware pour Azure Cloud Services et les machines virtuelles](azure-security-antimalware.md)
* [Comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur une machine virtuelle Windows](../virtual-machines/windows/classic/install-trend.md)
* [Comment tooinstall et configurer Symantec Endpoint Protection sur une machine virtuelle Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Nouvelles options anti-programmes malveillants pour protéger les machines virtuelles – McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Azure Multi-Factor Authentication
Azure multi-Factor authentication (MFA) est une méthode d’authentification qui nécessite l’utilisation de hello de plusieurs méthodes de vérification et ajoute une seconde couche critique de sécurité toouser connexions et transactions. L’authentification Multifacteur permet toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Elle fournit une authentification forte par le biais de diverses options de vérification : appel téléphonique, SMS, notification par application mobile ou code de vérification et jetons OATH tiers.

En savoir plus :

* [Authentification multifacteur](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Présentation d'Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication : fonctionnement](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute vous permet d’étendre vos réseaux locaux dans hello cloud de Microsoft sur une connexion privée dédiée facilitée par un fournisseur de connectivité. Grâce à ExpressRoute, vous pouvez établir des services de cloud computing tooMicrosoft de connexions, tels que Microsoft Azure, Office 365, CRM Online. La connectivité peut provenir d'un réseau universel (IP VPN), d’un réseau Ethernet point à point ou d’une interconnexion virtuelle via un fournisseur de connectivité dans un centre de colocalisation. Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ainsi, toooffer de connexions ExpressRoute plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello.

En savoir plus :

* [Présentation technique d’ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Passerelles de réseau virtuel
Les passerelles VPN, également appelés des passerelles de réseau virtuel Azure, sont utilisées toosend le trafic de réseau entre les réseaux virtuels et les emplacements sur site. Ils sont également le trafic de toosend utilisé entre plusieurs réseaux virtuels dans Azure (au réseau).  Les passerelles VPN garantissent la sécurisation de la connectivité entre les locaux entre Azure et votre infrastructure.

En savoir plus :

* [À propos des passerelles VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Vue d’ensemble de la sécurité du réseau Azure](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Parfois, les utilisateurs doivent toocarry opérations nécessitant des privilèges de ressources Azure ou d’autres applications SaaS. Cela signifie souvent que les organisations ont toogive les privilèges permanentes d’accès dans Azure Active Directory (Azure AD). C’est un risque de sécurité croissant pour les ressources hébergées dans le cloud, car les entreprises ne peuvent pas suffisamment surveiller ce que ces utilisateurs font avec leur accès privilégié.
En outre, si un compte d’utilisateur disposant d’un accès privilégié est compromis, cette seule faille peut affecter votre sécurité globale sur le cloud. Azure AD Privileged Identity Management permet tooresolve ce risque en réduisant le temps d’exposition hello de privilèges et en augmentant la visibilité de l’utilisation.  

Privileged Identity Management introduit le concept de hello d’un administrateur temporaire pour un rôle ou un « juste à temps » des accès d’administrateur, ce qui sont un utilisateur qui a besoin d’un processus d’activation pour ce rôle de toocomplete. modifications du processus d’activation Hello hello affectation hello tooa du rôle d’utilisateur dans Azure AD à partir de tooactive inactif, pour une période de temps, telles que les huit heures.

En savoir plus :

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Prise en main d’Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Identity Protection
Protection d’identité Azure Active Directory (AD) fournit une vue consolidée des activités suspectes connectez-vous et toohelp de vulnérabilités potentielles protéger votre entreprise. Identity Protection détecte les activités de connexion suspectes pour les utilisateurs et les identités privilégiées (administrateurs) en fonction de signaux tels que les attaques par force brute, les fuites d’informations d’identification et les connexions provenant d’emplacements inconnus et d’appareils infectés.

En fournissant des notifications et la mise à jour recommandée, Identity Protection aide les risques de toomitigate en temps réel. Il calcule la gravité de risque d’utilisateur, et vous pouvez configurer des stratégies basées sur les risques tooautomatically aide protéger l’accès application contre les menaces futures.

En savoir plus :

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Centre de sécurité
Azure Security Center vous aide à empêcher, détecter et répondre toothreats et fournit le qu'augmentation de la visibilité et contrôler, sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Centre de sécurité vous permet d’optimiser et de surveiller la sécurité de hello de vos ressources Azure par :

* L’activation de stratégies toodefine pour vos ressources d’abonnement Azure selon tooyour sécurité de l’entreprise a besoin et hello type d’applications ou de la sensibilité des données hello dans chaque abonnement.
* Analyse de l’état de hello de vos machines virtuelles Azure, le réseau et les applications.
* En fournissant une liste de priorité des alertes de sécurité, notamment les alertes de partenaires intégrées étudier des solutions, ainsi que des informations hello tooquickly et des recommandations sur la façon de tooremediate une attaque.

En savoir plus :

* [Introduction tooAzure centre de sécurité](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
