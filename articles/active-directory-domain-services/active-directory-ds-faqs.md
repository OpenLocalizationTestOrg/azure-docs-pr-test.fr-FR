---
title: aaaFAQs - Azure Active Directory Domain Services | Documents Microsoft
description: Forum aux questions sur les services de domaine Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Services de domaine Azure Active Directory : Forum aux questions (FAQ)
Cette page répond aux questions fréquemment posées sur hello Azure des Services de domaine Active Directory. N'hésitez pas à la consulter pour vous tenir au courant des mises à jour.

### <a name="troubleshooting-guide"></a>Guide de résolution des problèmes
Consultez tooour [guide de dépannage](active-directory-ds-troubleshooting.md) pour les problèmes de toocommon solutions rencontrés lorsque configuration ou de l’administration des Services de domaine Active Directory de Azure.

### <a name="configuration"></a>Configuration
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Puis-je créer plusieurs domaines pour un seul annuaire Azure AD ?
Non. Vous ne pouvez créer qu’un seul domaine pris en charge par les services de domaine Azure AD par annuaire Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Puis-je activer les services de domaine Azure AD dans un réseau virtuel Azure Resource Manager ?
Non. Les services de domaine Azure AD peuvent uniquement être activés dans un réseau virtuel Azure classique. Vous pouvez connecter hello classique de réseau virtuel tooa Gestionnaire de ressources du réseau virtuel votre domaine géré dans un réseau virtuel du Gestionnaire de ressources à l’aide de toouse d’homologation du réseau virtuel.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Puis-je activer les services de domaine Azure AD dans un annuaire Azure AD fédéré ? Utiliser les utilisateurs de tooauthenticate AD FS pour l’accès tooOffice 365. Puis-je activer les services de domaine Azure AD pour cet annuaire ?
Non. Les Services de domaine Active Directory Azure a besoin d’accéder à toohello les hachages de mot de passe de comptes d’utilisateur, les utilisateurs tooauthenticate via NTLM ou Kerberos. Dans un répertoire fédéré, les hachages de mot de passe ne sont pas stockées dans l’annuaire Azure AD de hello. Par conséquent, les services de domaine Azure AD ne fonctionnent pas avec ces annuaires Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Puis-je rendre les services de domaine Azure AD disponibles dans plusieurs réseaux virtuels au sein de mon abonnement ?
service Hello lui-même ne met pas directement en charge ce scénario. Les services de domaine Azure AD sont disponibles dans un seul réseau virtuel à la fois. Toutefois, vous pouvez configurer la connectivité entre plusieurs réseaux virtuels tooexpose les Services de domaine Active Directory de Azure tooother réseaux virtuels. Cet article décrit comment vous pouvez [connecter des réseaux virtuels dans Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Puis-je activer les services de domaine Azure AD à l’aide de PowerShell ?
Le déploiement à l’aide de PowerShell ou automatisé des services de domaine Azure AD n’est pas disponible actuellement.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Les Services de domaine Active Directory de Azure n’est disponible dans le nouveau portail de Azure hello ?
Non. Les Services de domaine Active Directory Azure peuvent être configurés uniquement dans hello [portail Azure classic](https://manage.windowsazure.com). Nous pensons que la prise en charge de tooextend de hello [portail Azure](https://portal.azure.com) Bonjour futures.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Puis-je ajouter domaine géré contrôleurs tooan des Services de domaine Active Directory de Azure ?
Non. domaine Hello fourni par les Services de domaine Active Directory de Azure est un domaine géré. Vous n’avez pas besoin de tooprovision, configurer ou gérer les contrôleurs de domaine pour ce domaine - gestion de ces activités sont fournies en tant que service par Microsoft. Par conséquent, vous ne pouvez pas ajouter autres contrôleurs de domaine (en lecture-écriture ou en lecture seule) pour le domaine géré de hello.

### <a name="administration-and-operations"></a>Administration et opérations
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Puis-je connecter le contrôleur de domaine toohello pour mon domaine géré à l’aide du Bureau à distance ?
Non. Vous n’avez pas les autorisations tooconnect toodomain contrôleurs hello gérés via le Bureau à distance. Les membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent administrer hello de domaine gérés à l’aide des outils d’administration Active Directory tels que hello centre d’Administration d’Active Directory (ADAC) ou Active Directory PowerShell. Ces outils sont installés à l’aide de hello 'Server Outils d’Administration distant' fonctionnalité sur un serveur Windows joints à un domaine géré de toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>J’ai activé les services de domaine Azure AD. Le compte d’utilisateur utilisent la fonctionnalité toodomain joindre le domaine toothis machines ?
Membres du groupe d’administration hello 'Administrateurs du contrôleur de domaine AAD' peuvent machines de jonction de domaine. En outre, les membres de ce groupe disposent toomachines accès Bureau à distance qui ont été toohello joint à un domaine.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Ai-je besoin de privilèges d’administrateur de domaine pour le domaine géré de hello fournie par les Services de domaine Active Directory de Azure ?
Non. Vous ne sont pas des privilèges d’administrateur sur le domaine géré de hello. Des privilèges « administrateur de domaine » et « administrateur de l’entreprise » ne sont pas disponibles pour vous toouse dans le domaine de hello. Administrateur de domaine existant ou de groupes d’administrateurs entreprise au sein de votre annuaire Azure AD sont également pas accordés des privilèges d’administrateur sur le domaine de hello/entreprise du domaine.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Puis-je modifier les appartenances aux groupes à l’aide de LDAP ou d’autres outils d’administration AD sur des domaines gérés ?
Non. Vous ne pouvez pas modifier les appartenances aux groupes dans des domaines pris en charge par les services de domaine Azure AD. Hello que va de même pour les attributs de l’utilisateur. Vous pouvez toutefois modifier les appartenances aux groupes ou les attributs d’utilisateur dans Azure AD ou sur votre domaine local. Ces modifications sont automatiquement synchronisée tooAzure AD les Services de domaine.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Combien de temps faut-il pour modifications I rendre visibles les toomy Azure AD directory toobe dans mon domaine géré ?
Modifications apportées à votre annuaire Azure AD à l’aide de hello interface utilisateur Azure AD ou PowerShell appartiennent à un domaine géré de tooyour synchronisés. Ce processus de synchronisation s’exécute en arrière-plan de hello. Après que la synchronisation initiale de hello à usage unique de votre annuaire est terminée, elle généralement prend environ 20 minutes sur les modifications effectuées dans Azure AD toobe répercutées dans votre domaine géré.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Puis-je étendre schéma hello de domaine géré de hello fourni par les Services de domaine Active Directory de Azure ?
Non. schéma de Hello est géré par Microsoft pour le domaine géré de hello. Les extensions de schéma ne sont pas prises en charge par les services de domaine Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Puis-je modifier ou ajouter des enregistrements DNS dans mon domaine géré ?
Oui. Les membres du groupe de hello « administrateurs de contrôleur de domaine AAD » ont des privilèges administrateur DNS, toomodify enregistrements DNS dans le domaine géré de hello. Ils peuvent utiliser la console du Gestionnaire DNS hello sur un ordinateur en cours d’exécution Windows Server toohello joint à un domaine géré, toomanage DNS. toouse hello console du Gestionnaire DNS, installation 'Outils du serveur DNS', qui fait partie de la fonctionnalité facultative de hello « Outils d’Administration de serveur distant » sur le serveur de hello. Vous trouverez plus d’informations sur les [utilitaires pour l’administration, la surveillance et la résolution des problèmes DNS](https://technet.microsoft.com/library/cc753579.aspx) sur TechNet.

### <a name="billing-and-availability"></a>Facturation et disponibilité
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Les services de domaine Azure AD sont-ils payants ?
Oui. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Existe-t-il une version d’évaluation gratuite pour le service de hello ?
Ce service est inclus dans la version d’évaluation gratuite de hello pour Azure. Vous pouvez vous inscrire pour bénéficier d’un [essai gratuit d’un mois d’Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Puis-je obtenir les services de domaine Azure AD dans le cadre d’Enterprise Mobility Suite (EMS) ? Ai-je besoin de Services de domaine Azure AD Premium toouse Azure AD ?
Non. Les services de domaine Azure AD constituent un service Azure avec paiement à l’utilisation et ne font pas partie d’EMS. Azure Active Directory Domain Services peut être utilisé avec toutes les éditions d’Azure AD (Gratuit, De base et Premium). La facturation se fait à l’utilisation, sur une base horaire.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Les régions Azure est le service de hello disponible dans ?
Consultez toohello [Services Azure par région](https://azure.microsoft.com/regions/#services/) toosee page une liste de hello régions Azure où les Services de domaine Active Directory de Azure est disponible.
