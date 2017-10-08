---
title: "expériences d’aaaConnect tooAzure de périphériques joints au domaine Active Directory pour Windows 10 | Documents Microsoft"
description: "Explique comment les administrateurs peuvent configurer réseau d’entreprise de stratégie de groupe tooenable périphériques toobe toohello de joints au domaine."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10
Jonction de domaine est organisations de manière standard hello connecté appareils pour le travail de hello cours des 15 dernières années et bien plus encore. Il a activé toosign d’utilisateurs dans les appareils tootheir à l’aide de leur travail de Windows Server Active Directory (Active Directory) ou comptes d’établissement scolaire et autorisées informatique toofully gérer ces appareils. Les organisations reposent généralement sur l’acquisition d’images de méthodes tooprovision périphériques toousers et généralement utiliser System Center Configuration Manager (SCCM) ou la stratégie de groupe toomanage les.


Jonction de domaine dans Windows 10 offre hello avantages suivants une fois que vous vous connectez les appareils tooAzure Active Directory (Azure AD) :

* Seul sign-on (SSO) tooAzure AD ressources depuis n’importe où
* Accès toohello enterprise du Windows Store à l’aide de travail ou d’établissement scolaire (aucun compte Microsoft requis)
* itinérance des paramètres utilisateur compatible pour l’entreprise sur tous les appareils avec un compte professionnel ou scolaire (aucun compte Microsoft requis) ;
* authentification forte et connexion pratique pour les comptes professionnels ou scolaires avec Windows Hello Entreprise et Windows Hello ;
* Capacité toorestrict accéder uniquement toodevices qui sont conformes aux paramètres de stratégie de groupe d’unité d’organisation

## <a name="prerequisites"></a>Composants requis
Jonction de domaine poursuit toobe utile. Toutefois, tooget les avantages de hello Azure AD de l’authentification unique, l’itinérance des paramètres à l’aide de travail ou établissement scolaire et accéder au magasin de tooWindows avec un travail ou d’établissement scolaire, vous devez hello suivant :

* Abonnement Azure AD
* Azure AD Connect tooextend hello local active tooAzure AD
* Stratégie qui a défini tooconnect tooAzure de périphériques joints au domaine Active Directory
* Version de Windows 10 (version 10551 ou ultérieure) pour les appareils

tooenable Windows Hello entreprise et Windows Hello, vous aurez également besoin des éléments suivants de hello :

- **Infrastructure de clé publique (PKI)** pour l’émission de certificats utilisateur.

- **Branche actuelle de System Center Configuration Manager** -vous devez tooinstall version 1606 ou supérieures.  
Pour plus d'informations, consultez les pages suivantes : 
    - [Documentation de System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog de l’équipe System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Les paramètres Windows Hello Entreprise dans System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

En tant qu’une demande de déploiement toohello autre infrastructure à clé publique, vous pouvez effectuer les suivant hello :

* Avoir quelques contrôleurs de domaine avec les services de domaine Active Directory Windows Server 2016.

tooenable l’accès conditionnel, vous pouvez créer des paramètres de stratégie de groupe qui autorisent l’accès des périphériques appartenant à un toodomain avec des déploiements supplémentaires. toomanage le contrôle d’accès basé sur la compatibilité du périphérique de hello, vous devrez suivant de hello :

* System Center Configuration Manager Current Branch (version 1606 ou ultérieure) pour les scénarios Windows Hello Entreprise

## <a name="deployment-instructions"></a>Instructions de déploiement

toodeploy, suivez les étapes de hello répertoriés dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Étape suivante
* [Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail](active-directory-azureadjoin-windows10-devices-overview.md)
* [Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [En savoir plus sur les scénarios d’utilisation pour Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configuration d’Azure AD Join](active-directory-azureadjoin-setup.md)

