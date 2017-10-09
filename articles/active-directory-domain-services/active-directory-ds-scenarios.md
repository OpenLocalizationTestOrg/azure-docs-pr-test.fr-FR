---
title: "Services de domaine Azure Active Directory : scénarios de déploiement | Microsoft Docs"
description: "Scénarios de déploiement pour les Services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Scénarios de déploiement et cas d'usage
Dans cette section, nous examinons quelques scénarios et cas pratiques qui tirent parti des services de domaine Azure Active Directory (AD).

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Administration sécurisée et simple des machines virtuelles Azure
Vous pouvez utiliser Azure Active Directory Domain Services toomanage vos machines virtuelles Azure de manière simplifiée. Machines virtuelles peut être toohello joint à un domaine géré, vous permettant ainsi de toouse toolog dans les informations d’identification Active Directory d’entreprise. Cette approche contribue à éviter les soucis de gestion des informations d’identification telles que la maintenance des comptes d’administrateur locaux sur chacune de vos machines virtuelles Azure.

Serveurs virtuels qui appartiennent à un domaine géré de toohello jointes peuvent également être gérés et sécurisés à l’aide de la stratégie de groupe. Vous pouvez appliquer des lignes de base de sécurité requis tooyour Azure virtual machines et les verrouiller conformément aux instructions de sécurité de l’entreprise. Par exemple, vous pouvez utiliser groupe Stratégie gestion fonctionnalités toorestrict hello les types d’applications qui peuvent s’exécuter sur ces ordinateurs virtuels.

![Administration simple des machines virtuelles Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Comme les serveurs et une autre infrastructure atteint la fin de vie, Contoso est le déplacement de nombreuses applications actuellement hébergées sur le cloud de toohello local. La norme informatique actuelle exige que les serveurs hébergeant les applications d’entreprise soient joints à un domaine et gérés au moyen d’une stratégie de groupe. Contoso administrateur préfère toodomain joindre l’ordinateur virtuel déployé dans Azure, administration toomake plus facile. Par conséquent, les administrateurs et les utilisateurs peuvent se connecter à l’aide de leurs informations d’identification d’entreprise. À hello même temps, les ordinateurs peuvent être toocomply configuré avec des lignes de base de sécurité requis à l’aide de la stratégie de groupe. Contoso préférez pas toohave toodeploy, surveiller et gérer des contrôleurs de domaine dans Azure toosecure machines virtuelles. Les services de domaine Azure AD sont idéaux pour ce cas d’utilisation.

**Notes de déploiement**

Tenez compte des hello les points importants pour ce scénario de déploiement suivants :

* Les domaines gérés fournis par les services de domaine Azure AD offrent par défaut une structure d’unité d’organisation plate. Toutes les machines jointes au domaine résident dans une unité d’organisation plate. Vous pouvez toutefois choisir toocreate des unités d’organisation personnalisées.
* Des Services de domaine Active Directory Azure prend en charge la stratégie de groupe simple sous forme de hello d’un objet GPO intégré chaque pour hello utilisateurs et ordinateurs conteneurs. Vous pouvez créer des objets stratégie de groupe personnalisé et cibler les unités d’organisation toocustom.
* Les Services de domaine Active Directory Azure prend en charge le schéma d’objet ordinateur hello base AD. Vous ne pouvez pas étendre le schéma de l’objet d’ordinateur hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Courbes d’élévation et MAJ une application sur site qui utilise tooAzure de l’authentification de liaison LDAP Services d’Infrastructure
![Liaison LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso dispose d’une application sur site qui a été achetée auprès d’un ISV il y a de nombreuses années. application Hello est actuellement en mode maintenance par hello ISV et application de toohello modifications demandeur prohibitif pour Contoso. Cette application a un serveur basé sur le web frontal qui collecte les informations d’identification de l’utilisateur à l’aide d’un formulaire web et puis authentifie les utilisateurs en effectuant un toohello de liaison LDAP Active Directory d’entreprise. Contoso aimeriez toomigrate cette tooAzure d’application des Services d’Infrastructure. Il est souhaitable que l’application hello fonctionne en l’état, sans la moindre modification. En outre, les utilisateurs doivent être en mesure de tooauthenticate à l’aide de leurs informations d’identification d’entreprise existantes et sans avoir différemment des choses de toodo tooretrain les utilisateurs. En d’autres termes, les utilisateurs finaux doivent être oublies d’où l’application hello est en cours d’exécution et la migration hello doit être transparent toothem.

**Notes de déploiement**

Tenez compte des hello les points importants pour ce scénario de déploiement suivants :

* Assurez-vous qu’application hello n’a pas besoin toomodify/écriture toohello active. Domaines de toomanaged d’un accès en écriture LDAP fournies par les Services de domaine Active Directory de Azure n’est pas pris en charge.
* Vous ne pouvez pas modifier les mots de passe directement sur le domaine géré de hello. Les utilisateurs finaux peuvent modifier leur mot de passe soit à l’aide du mécanisme de changement de mot de passe libre-service d’Azure AD ou sur un répertoire local de hello. Ces modifications sont automatiquement synchronisées et disponibles dans le domaine géré de hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Courbes d’élévation et MAJ tooaccess hello directory tooAzure Services d’Infrastructure de lire une application sur site qui utilise le protocole LDAP
Contoso possède une application métier locale, développée il y a presque dix ans. Cette application est active prenant en charge et a été conçue toowork avec Windows Server Active Directory. application Hello utilise les informations/attributs LDAP (Lightweight Directory Access Protocol) tooread sur les utilisateurs à partir d’Active Directory. application Hello ne pas modifier les attributs ou d’écriture dans le cas contraire toohello active. Contoso aimeriez toomigrate cette tooAzure d’application des Services d’Infrastructure et mettre hors service matériel sur site de hello vieillissement actuellement hébergeant cette application. application Hello ne peut pas être réécrit toouse Active API modernes tels que hello basé sur REST des API Azure AD Graph. Par conséquent, une option de courbes d’élévation et MAJ est souhaitée selon laquelle l’application hello peut être migré toorun dans le cloud hello, sans modifier le code ou de réécriture d’application hello.

**Notes de déploiement**

Tenez compte des hello les points importants pour ce scénario de déploiement suivants :

* Assurez-vous qu’application hello n’a pas besoin toomodify/écriture toohello active. Domaines de toomanaged d’un accès en écriture LDAP fournies par les Services de domaine Active Directory de Azure n’est pas pris en charge.
* Assurez-vous qu’application hello n’a pas besoin un schéma Active Directory étendue personnalisée. Les extensions de schéma ne sont pas prises en charge par les services de domaine Azure AD.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Migrer un local service ou démon application tooAzure Services d’Infrastructure
Certaines applications sont constituées de plusieurs couches, où l’un des niveaux de hello doit couche de tooperform appels authentifiés tooa principale comme une couche de base de données. Les comptes de service Active Directory sont couramment utilisés pour ces cas d’utilisation. Vous pouvez de courbes d’élévation et MAJ ces applications tooAzure Services d’Infrastructure et l’utilisation des Services de domaine Active Directory Azure pour les besoins d’identité hello de ces applications. Vous pouvez choisir toouse hello même compte de service qui est synchronisée à partir de votre tooAzure de répertoire Active Directory local. Ou bien, vous pouvez tout d’abord créer une unité d’organisation personnalisée et ensuite créer un compte de service distinct dans cette unité d’organisation, toodeploy de telles applications.

![Compte de service à l’aide de l’authentification intégrée de Windows](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso est équipé d’une application de coffre de logiciel personnalisée qui inclut un site web frontal, un serveur SQL et un serveur FTP principal. Intégrée de Windows pour l’authentification des comptes de service est le serveur de toohello FTP utilisé tooauthenticate hello web frontal. le frontal web Hello toorun est configuré comme un compte de service. Hello serveur principal est configuré l’accès du compte de service hello tooauthorize pour hello serveur web frontal. Contoso ne préfère pas toohave toodeploy un ordinateur virtuel de contrôleur de domaine dans hello cloud toomove cette tooAzure d’application des Services d’Infrastructure. Contoso administrateur peut déployer des serveurs hello hello serveur web frontal, de SQL server et de machines virtuelles de hello FTP server tooAzure d’hébergement. Ces ordinateurs sont joint tooan les Services de domaine Active Directory Azure gérée de domaine. Ensuite, ils peuvent utiliser hello même compte de service dans leur annuaire local pour l’authentification de l’application hello. Ce compte de service est le domaine géré de Services de domaine Active Directory de Azure toohello synchronisé et est disponible pour utilisation.

**Notes de déploiement**

Tenez compte des hello les points importants pour ce scénario de déploiement suivants :

* Assurez-vous qu’application hello utilise le nom d’utilisateur/mot de passe pour l’authentification. L’authentification basée sur un certificat/carte à puce n’est pas prise en charge par les services de domaine Azure AD.
* Vous ne pouvez pas modifier les mots de passe directement sur le domaine géré de hello. Les utilisateurs finaux peuvent modifier leur mot de passe soit à l’aide du mécanisme de changement de mot de passe libre-service d’Azure AD ou sur un répertoire local de hello. Ces modifications sont automatiquement synchronisées et disponibles dans le domaine géré de hello.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Déploiements des services Bureau à distance Windows Server dans Azure
Vous pouvez utiliser les Services de domaine Active Directory de Azure tooprovide gérés AD tooyour serveurs Bureau à distance déployés dans Azure des services de domaine.

Pour plus d’informations sur ce scénario de déploiement, consultez Comment trop[intégrer les Services de domaine Active Directory de Azure à votre déploiement des services Bureau à distance](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
