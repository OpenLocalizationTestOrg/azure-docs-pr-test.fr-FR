---
title: "le cloud de votre infrastructure d’identité locale Bonjour aaaMonitor."
description: "Il s’agit hello Azure AD Connect Health page qui décrit ce qu’il est et pourquoi l’utiliser."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Surveiller votre identité infrastructure et la synchronisation services locaux dans le cloud de hello
Azure Active Directory (Azure AD) Connect Health vous permet de surveiller et obtenir votre identité locale hello infrastructure et les services de synchronisation. Il vous permet de toomaintain un tooOffice connexion fiable 365 et Microsoft Online Services en fournissant des fonctionnalités de surveillance pour les composants de votre clé d’identité tels que les serveurs de Services de fédération Active Directory (AD FS), les serveurs Azure AD Connect (également appelées en tant que moteur de synchronisation), les contrôleurs de domaine Active Directory, etc.. En rendant hello principaux points de données sur ces composants facilement accessible afin que vous pouvez obtenir l’utilisation et d’autres important insights toomake de prendre des décisions informées.

informations de Hello sont présentées en hello [portail Azure AD Connect Health](https://aka.ms/aadconnecthealth). Dans le portail Azure AD Connect Health hello, vous pouvez afficher les alertes, l’analyse des performances, analytique de l’utilisation et d’autres informations. Azure AD Connect Health permet à lentille unique de hello d’intégrité de composants de votre clé d’identité dans un seul emplacement.

![Présentation d’Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Comme les fonctions hello dans Azure AD Connect Health augmentent, portail de hello fournit un tableau de bord unique à travers objectif hello d’identité. Vous obtenez un environnement plus robust, intégré et sain pour votre tooincrease les utilisateurs de leurs réalisation des tâches tooget possibilité.

## <a name="why-use-azure-ad-connect-health"></a>Pourquoi utiliser Azure AD Connect Health ?
Lorsque vous intégrez vos annuaires locaux à Azure AD, vos utilisateurs sont plus productifs, car il existe une identité commune tooaccess à la fois de cloud computing et ressources locales. Toutefois, cette intégration crée défi hello de garantir que cet environnement est intègre, afin que les utilisateurs peuvent accéder de manière fiable les ressources à la fois localement et dans hello cloud à partir de n’importe quel appareil. Azure AD Connect Health vous permet de surveiller et obtenir votre infrastructure d’identité locale qui est utilisé tooaccess Office 365 ou autres applications Azure AD. Son installation est aussi simple que celle d’un agent sur chacun de vos serveurs d’identité local.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Utilisation d’Azure AD Connect Health pour AD FS](active-directory-aadconnect-health-adfs.md)
Azure AD Connect Health pour AD FS prend en charge AD FS 2.0 dans Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2. Prend également en charge le serveur proxy de surveillance hello AD FS ou prend en charge les serveurs proxy d’applications web qui fournissent l’authentification pour l’accès extranet. Avec une installation simple et à faible coût de l’Agent d’intégrité de hello, Azure AD Connect Health pour AD FS fournit hello suivant l’ensemble de fonctionnalités clés :

* Analyse des alertes tooknow lorsque AD FS et serveurs de proxy ADFS ne sont pas sains
* Notifications par courrier électronique pour les alertes critiques
* Tendances des données de performance, utiles pour la planification des capacités d’AD FS
* Analytique d’utilisation pour les connexions AD FS avec les tableaux croisés dynamiques (applications, les utilisateurs, l’emplacement réseau etc.), qui sont utile toounderstand comment AD FS est mise en route utilisé
* Rapports AD FS comme le Top 50 des utilisateurs avec des tentatives ayant échoué en raison de noms d’utilisateur/mots de passe incorrects et leur dernière adresse IP

Hello vidéo suivante fournit une vue d’ensemble d’Azure AD Connect Health pour AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health pour la synchronisation](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health pour la synchronisation surveille et fournit des informations sur les synchronisations hello qui se produisent entre votre Active Directory local et le Azure AD. Azure AD Connect Health pour la synchronisation fournit hello suivant l’ensemble de fonctionnalités clés :

* Surveillance avec tooknow des alertes lorsqu’un serveur Azure AD Connect, également appelé hello moteur de synchronisation n’est pas intègre
* Notifications par courrier électronique pour les alertes critiques
* Analyse opérationnelle de synchronisation, notamment les graphiques de latence pour les opérations de synchronisation et les tendances dans différentes opérations, en particulier les ajouts, les mises à jour, les suppressions
* Aperçu rapide d’informations sur les propriétés de la synchronisation et le dernier succès exporter tooAzure AD
* Rapports sur les erreurs de synchronisation de niveau objet \(ne nécessite pas Azure AD Premium\)

Hello vidéo suivante fournit une vue d’ensemble d’Azure AD Connect Health pour la synchronisation.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Utilisation d’Azure AD Connect Health pour AD DS](active-directory-aadconnect-health-adds.md)
Azure AD Connect Health pour Active Directory Domain Service (AD DS) permet de surveiller les contrôleurs de domaine installés sur Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016. Hello installation de l’Agent de contrôle d’intégrité permet de vous toomonitor votre local environnement AD DS à partir du cloud de hello. Azure AD Connect Health pour AD DS fournit hello suivant l’ensemble de fonctionnalités clés :

* Analyse toodetect des alertes lorsque des contrôleurs de domaine ne sont pas intègres et notifications pour les alertes critiques par courrier électronique
* tableau de bord de contrôleurs de domaine Hello, qui fournit un aperçu rapide de contrôle d’intégrité hello et l’état de fonctionnement de vos contrôleurs de domaine
* tableau de bord Hello état de réplication qui a les dernières informations de réplication hello et lie tootroubleshooting guides lorsque des erreurs sont détectées.
* Rapide accès à distance tooperformance des graphiques de données de compteurs de performances courants qui sont nécessaires pour la résolution des problèmes et à des fins d’analyse

Hello vidéo suivante fournit une vue d’ensemble d’Azure AD Connect Health pour AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Démarrer avec Azure AD Connect Health
tooget en route avec Azure AD Connect Health, hello utilisation comme suit :

1. Accédez à [Obtenir Azure AD Premium](../active-directory-get-started-premium.md) ou [Démarrer une version d’évaluation](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Téléchargez et installez les agents Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) sur vos serveurs d’identité.
3. Tableau de bord de vue hello Azure AD Connect Health à [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> N’oubliez pas qu’avant de voir les données dans votre tableau de bord Azure AD Connect Health, vous devez tooinstall hello Agents d’intégrité de Connect de Azure AD sur vos serveurs cibles.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Téléchargement et installation de l’agent Azure AD Connect Health
* Assurez-vous que vous [satisfaire aux exigences de hello](active-directory-aadconnect-health-agent-install.md#requirements) pour Azure AD Connect Health.
* Prise en main d’Azure AD Connect Health pour AD FS
    * [Téléchargez l’agent Azure AD Connect Health pour AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Consultez les instructions d’installation hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Prise en main d’Azure AD Connect Health pour la synchronisation
    * [Téléchargez et installez la version la plus récente d’Azure AD Connect hello](http://go.microsoft.com/fwlink/?linkid=615771). Hello Agent d’intégrité pour la synchronisation sera installé dans le cadre de l’installation de se connecter hello Azure AD (version 1.0.9125.0 ou une version ultérieure).
* Prise en main d’Azure AD Connect Health pour AD DS
    * [Téléchargez l’agent Azure AD Connect Health pour AD DS](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Consultez les instructions d’installation hello](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portail Azure AD Connect Health
portail d’Azure AD Connect Health Hello affiche des vues d’analytique de l’utilisation, analyse des performances et alertes. URL Hello https://aka.ms/aadconnecthealth est toohello le panneau principal d’Azure AD Connect Health. Considérez les panneaux comme des fenêtres. Sur le panneau principal de hello, vous voyez **Quick Start**, les services dans Azure AD Connect Health et les options de configuration supplémentaires. Consultez hello suivant capture d’écran et brève explication qui suivent la capture d’écran de hello. Après avoir déployé les agents hello, service de contrôle d’intégrité hello identifie automatiquement les services de hello surveillance d’Azure AD Connect Health.

> [!NOTE]
> Pour plus d’informations, consultez hello [FAQ de connexion AD Azure](active-directory-aadconnect-health-faq.md) ou hello [page Azure Active Directory tarification](https://aka.ms/aadpricing).
    
![portail Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Démarrage rapide**: lorsque vous sélectionnez cette option, hello **Quick Start** panneau s’ouvre. Vous pouvez télécharger hello Agent Azure AD Connect Health en sélectionnant **obtenir des outils**. Vous pouvez également accéder à la documentation et fournir des commentaires.
* **Active Directory Federation Services**: cette option affiche tous les services AD FS de hello que Azure AD Connect Health analyse. Lorsque vous sélectionnez une instance, panneau hello qui s’ouvre affiche des informations sur cette instance de service. Il comporte une vue d’ensemble, les propriétés, les alertes, les données de surveillance et une analyse de l’utilisation. En savoir plus sur les fonctionnalités hello [à l’aide de Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (synchronisation)** : cette option affiche les serveurs Azure AD Connect actuellement surveillés par Azure AD Connect Health. Lorsque vous sélectionnez entrée de hello, panneau hello qui s’ouvre affiche des informations sur vos serveurs Azure AD Connect. En savoir plus sur les fonctionnalités hello [à l’aide de Azure AD Connect Health pour la synchronisation](active-directory-aadconnect-health-sync.md).
* **Les Services de domaine Active Directory**: cette option affiche toutes les forêts hello AD DS que Azure AD Connect Health analyse. Lorsque vous sélectionnez une forêt, panneau hello qui s’ouvre affiche des informations sur cette forêt. Ces informations incluent une vue d’ensemble des informations essentielles, tableau de bord de contrôleurs de domaine hello, tableau de bord hello état de réplication, des alertes et surveillance. En savoir plus sur les fonctionnalités hello [à l’aide de Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md).
* **Configurer**: cette section inclut options tooturn hello après dans ou hors tension :

  - La mise à jour automatique tooautomatically update hello Azure AD Connect Health agent toohello version la plus récente : vous serez toohello mises à jour automatiquement les dernières versions de hello Agent Azure AD Connect Health lorsqu’elles deviennent disponibles. Cette option est activée par défaut.
  - Autoriser les données de contrôle d’intégrité du répertoire Microsoft access tooyour Azure AD uniquement à des fins de dépannage : Si cette option est activée, Microsoft peut voir hello les mêmes données que vous voyez. L’accès à ces informations simplifient la résolution des problèmes. Elle est désactivée par défaut.

## <a name="related-links"></a>Liens connexes
* [Installation de l’agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
