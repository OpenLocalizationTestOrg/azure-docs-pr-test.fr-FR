---
title: "intégration d’aaaVPN avec l’authentification Multifacteur Azure à l’aide d’extension NPS | Documents Microsoft"
description: "Cet article décrit l’intégration de votre infrastructure VPN avec l’authentification Multifacteur Azure à l’aide d’extension du serveur NPS (Network Policy Server) hello pour Microsoft Azure."
services: active-directory
keywords: "Azure MFA, intégration VPN, Azure Active Directory, extension de serveur NPS"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>Intégrer votre infrastructure VPN avec Azure multi-Factor Authentication (MFA) à l’aide d’extension du serveur NPS (Network Policy Server) hello pour Azure

## <a name="overview"></a>Vue d'ensemble

Hello extension du Service NPS (Network Policy Server) pour Azure permet aux organisations d’authentification client toosafeguard Authentication Dial-In Service RADIUS (Remote User) à l’aide de nuage [Azure multi-Factor Authentication (MFA)](multi-factor-authentication-get-started-server-rdg.md), qui fournit la vérification en deux étapes.

Cet article fournit des instructions pour l’intégration de l’infrastructure de serveur NPS hello avec l’authentification Multifacteur Azure à l’aide d’extension NPS hello pour la vérification en deux étapes sécurisé tooenable Azure pour les utilisateurs qui tentent de réseau de tooyour tooconnect à l’aide d’un réseau privé virtuel. 

Hello stratégie réseau et les Services d’accès (NPS) donne aux organisations hello suivant capacités :

* Spécifier des emplacements centraux pour la gestion de hello et le contrôle de toospecify de demandes de réseau qui peut se connecter, les heures de la journée, les connexions sont autorisées, durée hello des connexions et niveau de hello de sécurité que les clients doivent utiliser tooconnect et ainsi de suite. Plutôt que de spécifier ces stratégies sur chaque serveur VPN ou de passerelle des services Bureau à distance (RD), ces stratégies peuvent être spécifiées une seule fois dans un emplacement central. Hello protocole RADIUS sert tooprovide hello centralisée de l’authentification, l’autorisation et gestion des comptes (AAA). 
* Établir et appliquer les stratégies de contrôle d’intégrité de client de Protection d’accès réseau (NAP) qui détermine si les appareils sont autorisées sans restriction ou à accès restreint toonetwork ressources.
* Fournir un moyen tooenforce authentification et l’autorisation pour les commutateurs Ethernet et des points d’accès sans fil compatibles too802.1x accès.    

Pour plus d’informations, consultez [Serveur NPS (Network Policy Server)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

tooenhance sécurité et fournir le niveau élevé de conformité, les entreprises peuvent intégrer NPS avec tooensure Azure MFA que les utilisateurs utilisent la vérification en deux étapes toobe en mesure de vous connecter toohello port virtuel sur le serveur VPN de hello. Pour toobe les utilisateurs autorisé à accéder, ils doivent fournir leur combinaison nom d’utilisateur/mot de passe avec les informations utilisateur de hello a dans leur contrôle. Ces informations doivent être approuvées et pas facilement dupliquées, comme un numéro de téléphone portable, numéro de téléphone fixe, une application sur un appareil mobile et autres.

Disponibilité toohello préalable de hello extension NPS pour Azure, les clients qui souhaitaient vérification en deux étapes tooimplement intégré NPS Azure MFA des environnements et avaient tooconfigure et mettre à jour un serveur distinct de l’authentification Multifacteur dans l’environnement local de hello en tant que documentées dans la passerelle Bureau à distance et le serveur Azure multi-Factor Authentication utilisant RADIUS.

disponibilité Hello d’extension NPS hello pour Azure offre désormais des organisations hello choix toodeploy une solution d’authentification Multifacteur local ou une nuage MFA solution toosecure RADIUS l’authentification du client.
 
## <a name="authentication-flow"></a>Flux d’authentification
Lorsqu’un utilisateur connecte à tooa le port virtuel sur un serveur VPN, ils doivent tout d’abord s’authentifier à l’aide d’une variété de protocoles, ce qui autorise l’utilisation de hello d’une combinaison de nom d’utilisateur/mot de passe et des méthodes d’authentification par certificat. 

Dans tooauthenticating d’ajout et vérification d’identité, les utilisateurs doivent disposer hello appropriés des autorisations d’accès à distance. Dans des implémentations simples, ces autorisations d’accès à distance qui autorisent l’accès sont définies directement sur les objets de l’utilisateur Active Directory hello. 

 ![Propriétés de l’utilisateur](./media/nps-extension-vpn/image1.png)

Pour des implémentations simples, chaque serveur VPN autorise ou refuse l’accès en fonction des stratégies définies sur chaque serveur VPN local.

Dans les implémentations de plus grandes et plus évolutives, hello attributions des stratégies ou refuser l’accès VPN sont centralisées sur les serveurs RADIUS. Dans ce cas, le serveur VPN de hello agit comme un serveur d’accès (client RADIUS) qui transfère les demandes de connexion et le serveur RADIUS de compte messages tooa. tooconnect toohello port virtuel sur le serveur VPN de hello, les utilisateurs doivent être authentifiés et répondent aux conditions hello définies de manière centralisée sur les serveurs RADIUS. 

Lorsque hello extension NPS pour Azure est intégré à hello NPS, les flux d’authentification réussie hello est la suivante :

1. serveur VPN de Hello reçoit une demande d’authentification d’un utilisateur VPN qui inclut hello nom d’utilisateur et mot de passe tooconnect tooa ressource, telle qu’une session Bureau à distance. 
2. Agissant comme un client RADIUS, serveur VPN convertit le message de demande d’accès RADIUS tooa hello demande et envoie hello message (mot de passe est chiffré) toohello RADIUS NPS (server) sur lequel est installé hello extension du serveur NPS. 
3. Hello nom d’utilisateur et mot de passe est vérifiée dans Active Directory. Si hello nom d’utilisateur / mot de passe est incorrect, hello serveur RADIUS envoie un message de refus d’accès. 
4. Si toutes les conditions, comme spécifié dans hello de demande de connexion de serveur NPS et stratégies de réseau sont remplies (par exemple, l’heure du jour ou de groupe de restrictions d’appartenance), hello extension NPS déclenche une demande d’authentification secondaire avec l’authentification Multifacteur Azure. 
5. L’authentification Multifacteur Azure communique avec Azure Active Directory, récupère les détails de l’utilisateur hello et effectue l’authentification secondaire hello à l’aide de la méthode hello configuré par l’utilisateur hello (message texte, application mobile et ainsi de suite). 
6. En cas de réussite de stimulation d’authentification Multifacteur de hello, Azure MFA communique extension NPS toohello hello résultat.
7. Une fois que la tentative de connexion hello est authentifié et autorisé, hello serveur NPS où hello extension est installé envoie un acceptation d’accès RADIUS message toohello serveur VPN (client RADIUS).
8. Hello est accordé l’accès toohello de port virtuel sur le serveur VPN et établit un tunnel VPN chiffré.

## <a name="prerequisites"></a>Composants requis
Cette section détaille hello requise avant d’intégrer l’authentification Multifacteur Azure hello passerelle Bureau à distance. Avant de commencer, vous devez avoir hello suivant des conditions préalables en place.

* Infrastructure VPN
* Rôle des services de stratégie et d’accès réseau (NPS)
* Licence Azure MFA
* Logiciel Windows Server
* Bibliothèques
* Azure AD synchronisé avec AD local 
* ID du GUID Azure Active Directory

### <a name="vpn-infrastructure"></a>Infrastructure VPN
Cet article suppose que vous disposez d’une infrastructure VPN de travail à l’aide de Microsoft Windows Server 2016 en place et que ce serveur VPN hello est actuellement pas configuré tooforward connexion demandes tooa serveur RADIUS. Vous allez configurer hello VPN infrastructure toouse un serveur RADIUS central dans ce guide.

Si vous n’avez pas d’une infrastructure de travail en place, vous pouvez rapidement créer cette infrastructure par les instructions suivantes hello fournie dans nombreux didacticiels le programme d’installation VPN que vous pouvez rechercher sur hello Microsoft et des sites tiers. 

### <a name="network-policy-and-access-services-nps-role"></a>Rôle des services de stratégie et d’accès réseau (NPS)

Hello service de rôle NPS fournit des fonctionnalités hello RADIUS serveur et client. Cet article suppose que vous avez installé le rôle de serveur NPS hello sur un serveur membre ou un contrôleur de domaine dans votre environnement. Configurez le RADIUS pour une configuration de VPN dans ce guide. Installer le rôle de serveur NPS hello sur un serveur _autres_ que votre serveur VPN.

Pour plus d’informations sur l’installation du rôle de serveur NPS hello service Windows Server 2012 ou version ultérieure, consultez [installer un serveur de stratégie de contrôle d’intégrité NAP](https://technet.microsoft.com/library/dd296890.aspx). La stratégie d’accès réseau (NAP) est déconseillée dans Windows Server 2016. Pour obtenir une description des meilleures pratiques pour NPS, y compris hello recommandation tooinstall NPS sur un contrôleur de domaine, consultez [meilleures pratiques pour NPS](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Licences

Une licence pour Azure MFA est obligatoire, disponible via un abonnement Azure AD Premium, Enterprise Mobility plus Security (EMS) ou MFA. Pour plus d’informations, consultez [comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). À des fins de test, vous pouvez utiliser un abonnement d’évaluation.

### <a name="software"></a>Logiciel

Hello, extension de serveur NPS requiert Windows Server 2008 R2 SP1 ou version ultérieure avec le service de rôle NPS hello installé. Toutes les étapes de hello dans ce guide a été effectuées à l’aide de Windows Server 2016.

### <a name="libraries"></a>Bibliothèques

Hello suivant deux bibliothèques est requise :

* [Visual C++ Redistributable Packages pour Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
* _Module Microsoft Azure Active Directory pour Windows PowerShell version 1.1.166.0_ ou version supérieure. Pour la version la plus récente hello et des instructions d’installation, consultez [Microsoft Azure Active Directory PowerShell Module Version historique de publication de](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Ces bibliothèques ne sont pas compressées avec hello NPS le programme d’installation des fichiers d’extension (version 0.9.1.2), en dépit de la documentation existante qui stipule le contraire. Au minimum, vous devez installer les Packages redistribuables hello Visual C++ pour Visual Studio 2013. Hello Microsoft Azure Module Active Directory pour Windows PowerShell est installé, si elle n’est pas déjà présent, via un script de configuration que vous exécutez en tant que partie du processus d’installation de hello. Il n’a aucun tooinstall besoin de ce module avance s’il n’est pas déjà installé.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory synchronisé avec Active Directory local 

toouse hello extension serveur NPS local utilisateurs doivent être synchronisés avec Azure Active Directory et activés pour l’authentification multifacteur. Ce guide part du principe que les utilisateurs locaux sont synchronisés avec Azure Active Directory en utilisant AD Connect. Vous trouverez ci-dessous des instructions pour fournir aux utilisateurs l’authentification multifacteur.
Pour obtenir plus d’informations sur Azure AD Connect, consultez [Intégrer vos répertoires locaux avec Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID du GUID Azure Active Directory 
tooinstall hello NPS, vous devez tooknow hello GUID de hello Azure Active Directory. Instructions pour la recherche hello GUID de hello Azure Active Directory sont fournies dans la section suivante de hello.

## <a name="configure-radius-for-vpn-connections"></a>Configurer RADIUS pour les connexions VPN

Si vous avez installé le rôle de serveur NPS hello sur un serveur membre, vous devez tooconfigure tooauthenticate et autorisez les clients VPN qui demandent des connexions VPN. 

Cette section part du principe que vous avez installé les rôles de serveur de stratégie réseau hello mais que vous n'avez pas configuré pour une utilisation dans votre infrastructure.

>[!NOTE]
>Si vous disposez déjà d’un serveur VPN de travail qui utilise un serveur RADIUS centralisé pour l’authentification, vous pouvez ignorer cette section.
>

### <a name="register-server-in-active-directory"></a>Enregistrer le serveur dans Active Directory
toofunction correctement dans ce scénario, le serveur NPS de hello doit toobe inscrit dans Active Directory.

1. Ouvrez le Gestionnaire de serveurs.
2. Dans Gestionnaire de serveurs, cliquez sur **Outils** puis cliquez sur **Serveur de stratégie réseau**. 
3. Dans la console du serveur NPS hello, cliquez sur **NPS (Local)**, puis cliquez sur **inscrire un serveur dans Active Directory**. Cliquez deux fois sur **OK**.

 ![Serveur de stratégie réseau](./media/nps-extension-vpn/image2.png)

4. Laissez la console de hello ouvert pour la procédure suivante de hello.

### <a name="use-wizard-tooconfigure-radius-server"></a>Utiliser un serveur RADIUS tooconfigure Assistant
Vous pouvez utiliser un standard (basée sur l’Assistant) ou un serveur RADIUS de configuration avancée option tooconfigure hello. Cette section suppose l’utilisation de hello hello basée sur l’Assistant standard option de configuration.

1. Dans la console du serveur NPS hello, cliquez sur **NPS (Local)**.
2. Sous Configuration standard, sélectionnez **Serveur RADIUS pour l’accès à distance ou les connexions VPN**, puis cliquez sur **Configurer une connexion VPN ou accès à distance**.

 ![Configurer VPN](./media/nps-extension-vpn/image3.png)

3. Dans hello page Sélectionnez les accès à distance ou le Type de connexions de réseau privé virtuel, sélectionnez **des connexions de réseau privé virtuel**, puis cliquez sur **suivant**.

 ![Réseau privé virtuel](./media/nps-extension-vpn/image4.png)

4. Page hello de spécifier l’accès à distance ou de serveur VPN, cliquez sur **ajouter**.
5. Bonjour **client RADIUS nouvelle** boîte de dialogue, fournissez un nom convivial, entrez le nom pouvant être résolu de hello ou adresse IP du serveur VPN de hello et entrez un mot de passe secret partagé. Créez un mot de passe secret partagé long et complexe. Enregistrer ce mot de passe, que vous en avez besoin pour les étapes de la section suivante de hello.

 ![Nouveau client RADIUS](./media/nps-extension-vpn/image5.png)

6. Cliquez sur **OK**, puis sur **Suivant**.
7. Sur hello **configurer des méthodes d’authentification** page, acceptez la sélection par défaut de hello (authentification cryptée Microsoft version 2 (MS-CHAPv2) ou choisissez une autre option, puis cliquez sur **suivant**.

  >[!NOTE]
  >Si vous configurez le protocole EAP (Extensible Authentication Protocol), vous devez utiliser MS CHAPv2 ou PEAP. Aucun autre EAP n’est pris en charge.
 
8. Sur la page spécifier des groupes d’utilisateurs de hello, cliquez sur **ajouter** et sélectionnez un groupe approprié, le cas échéant. Sinon, laissez la sélection hello tooall l’accès toogrant vide les utilisateurs.

 ![Spécifier des groupes d’utilisateurs](./media/nps-extension-vpn/image7.png)

9. Cliquez sur **Suivant**.
10. Sur la page de spécifier des filtres IP hello, cliquez sur **suivant**.
11. Sur la page spécifier les paramètres de chiffrement de hello, acceptez les paramètres par défaut de hello, puis cliquez sur **suivant**.

 ![Spécifier le chiffrement](./media/nps-extension-vpn/image8.png)

12. Sur hello spécifier un nom de domaine, hello nom vide, acceptez le paramètre par défaut de hello, puis cliquez sur **suivant**.

 ![Spécifier un nom de domaine](./media/nps-extension-vpn/image9.png)

13. Sur hello à la fin de la nouvelle connexion d’accès ou la page de clients RADIUS et les connexions de réseau privé virtuel, cliquez sur **Terminer**.

 ![Finaliser des connexions](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>Vérifier la configuration RADIUS
Cette section détaille la configuration hello que vous avez créé à l’aide d’Assistant de hello.

1. Sur le serveur NPS hello, dans la console NPS (Local) hello, développez les Clients RADIUS, puis sélectionnez **Clients RADIUS**.
2. Dans le volet d’informations hello, vous avez créé à l’aide d’Assistant un client RADIUS hello avec le bouton droit, puis cliquez sur **propriétés**. propriétés de Hello pour votre client RADIUS (serveur VPN de hello) doivent être toothose comme indiqué ci-dessous.

 ![Properties VPN](./media/nps-extension-vpn/image11.png)

3. Cliquez sur **Annuler**.
4. Sur le serveur NPS hello, dans la console NPS (Local) hello, développez **stratégies**, puis sélectionnez **stratégies de demande de connexion**. Vous devez voir la stratégie de connexions VPN hello qui ressemble à image hello ci-dessous.

 ![Demandes de connexion](./media/nps-extension-vpn/image12.png)

5. Sous stratégies, sélectionnez **Stratégies réseau**. Vous devez une stratégie de connexions de réseau privé virtuel (VPN, Virtual Private Network) qui ressemble à image hello ci-dessous.

 ![Propriétés du réseau](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>Configurer l’authentification de serveur VPN toouse RADIUS
Dans cette section, vous configurez l’authentification RADIUS toouse hello VPN server. Cette section part du principe que vous disposez d’une configuration de l’utilisation du serveur VPN mais que vous n’avez pas configuré l’authentification RADIUS toouse hello VPN server. Après avoir configuré le serveur VPN de hello, vous confirmez que votre configuration fonctionne comme prévu.

>[!NOTE]
>Si vous disposez déjà d’une configuration de serveur VPN de travail qui utilise l’authentification RADIUS, vous pouvez ignorer cette section.
>

### <a name="configure-authentication-provider"></a>Configurer le fournisseur d’authentification
1. Sur le serveur VPN de hello, ouvrez le Gestionnaire de serveur.
2. Dans le Gestionnaire de serveur, cliquez sur **Outils**, puis sur **Routage et accès à distance**.
3. Dans la console de routage et accès distant hello, cliquez sur  **\[nom du serveur\] (local)**, puis cliquez sur **propriétés**.

 ![Routage et d’accès à distance](./media/nps-extension-vpn/image14.png)
 
4. Bonjour **[propriétés nom du serveur} (local)** boîte de dialogue, cliquez sur hello **sécurité** onglet. 
5. Sur hello **sécurité** onglet, sous le fournisseur d’authentification, cliquez sur **l’authentification RADIUS**, puis **configurer**.

 ![Authentification RADIUS](./media/nps-extension-vpn/image15.png)
 
6. Dans la boîte de dialogue de l’authentification RADIUS hello, cliquez sur **ajouter**.
7. Dans hello ajouter un serveur RADIUS, dans nom du serveur, ajouter hello hello nom ou l’adresse IP du serveur RADIUS de hello que vous avez configuré dans la section précédente de hello.
8. Dans le secret partagé, cliquez sur **modification** et ajoutez hello partagée de mot de passe secret vous avez créé et enregistré précédemment.
9. Dans le délai d’attente (secondes), modifiez la valeur de tooa de valeur de hello entre **30** et **60**. Cela est nécessaire tooallow suffisamment de temps toocomplete hello second facteur d’authentification.
 
 ![Ajouter un serveur RADIUS](./media/nps-extension-vpn/image16.png)
 
10. Cliquez sur **OK** jusqu'à la fermeture de toutes les boîtes de dialogue.

### <a name="test-vpn-connectivity"></a>Connectivité VPN de test
Dans cette section, vous confirmez que le client VPN hello est authentifié et autorisé par le serveur RADIUS de hello lorsque vous essayez de port virtuel de tooconnect tooVPN. Cette section part du principe que vous utilisez Windows 10 comme un client VPN. 

>[!NOTE]
>Si vous avez déjà configuré un serveur VPN toohello de tooconnect de client VPN et que vous avez enregistré les paramètres de hello, vous pouvez ignorer tooconfiguring de hello étapes connexes et l’enregistrement d’un objet de connexion VPN.
>

1. Sur votre ordinateur client VPN, cliquez sur **Démarrer**, puis sur**Paramètres** (icône d’engrenage).
2. Dans Paramètres de la fenêtre, cliquez sur **Réseau et Internet**.
3. Cliquez sur **VPN**.
4. Cliquez sur **Ajouter une connexion VPN**.
5. Ajouter une connexion VPN, spécifiez Windows (intégrée) comme hello fournisseur VPN, puis terminée hello restant des champs, selon le cas et cliquez sur **enregistrer**. 

 ![Ajouter une connexion VPN](./media/nps-extension-vpn/image17.png)
 
6. Ouvrez hello **Centre réseau et partage** dans le panneau de configuration.
7. Cliquez sur **Modifier les paramètres de l’adaptateur**.

 ![Modifier les paramètres de l’adaptateur](./media/nps-extension-vpn/image18.png)

8. Avec le bouton droit de connexion de réseau VPN hello, puis cliquez sur Propriétés. 

 ![Propriétés du réseau VPN](./media/nps-extension-vpn/image19.png)

9. Dans la boîte de dialogue Propriétés hello VPN, cliquez sur hello **sécurité** onglet. 
10. Dans l’onglet sécurité de hello, assurez-vous que seul **Microsoft CHAP Version 2 (MS-CHAP v2)** est sélectionné, puis cliquez sur OK.

 ![Autoriser les protocoles](./media/nps-extension-vpn/image20.png)

11. Cliquez sur la connexion VPN de hello, puis cliquez sur **connexion**.
12. Dans la page Paramètres de hello, cliquez sur **connexion**.

Si la connexion s’affiche dans le journal de sécurité hello sur le serveur RADIUS de hello en tant que 6272 d’ID d’événement, comme illustré ci-dessous.

 ![Propriétés de l’événement](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Guide de résolution des problèmes
Supposons que votre configuration VPN fonctionnait avant que vous avez configuré hello VPN server toouse un serveur RADIUS centralisé pour l’authentification et l’autorisation. Dans ce cas, il est probable que le problème de hello peut être dû à une configuration incorrecte de hello serveur RADIUS ou hello utilisation d’un nom d’utilisateur non valide ou le mot de passe. Par exemple, si vous utilisez un autre suffixe UPN de hello dans nom d’utilisateur hello, tentative de connexion hello risque d’échouer (vous devez utiliser hello du même nom de compte pour de meilleurs résultats). 

tootroubleshoot ces problèmes, un toostart idéal est de journaux des événements de sécurité tooexamine hello sur hello serveur RADIUS. recherche de temps toosave pour les événements, vous pouvez utiliser hello en fonction du rôle serveur d’accès et de stratégie de réseau affichage personnalisé dans l’Observateur d’événements, comme indiqué ci-dessous. ID d’événement 6273 indique les événements où hello serveur NPS refusé accès tooa utilisateur. 

 ![Observateur d’événements](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Configurer l’authentification multifacteur
Cette section fournit des instructions pour activer les utilisateurs pour l’authentification multifacteur et de configurer des comptes pour la vérification en deux étapes. 

### <a name="enable-multi-factor-authentication"></a>Activer l’authentification multifacteur
Dans cette section, activez des comptes Azure AD pour l’authentification multifacteur. Hello d’utilisation **portail classique** tooenable des utilisateurs pour l’authentification Multifacteur. 

1. Ouvrez un navigateur et accédez trop[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Ouvrez une session en tant qu’administrateur de hello.
3. Dans le portail de hello, dans le volet de navigation gauche hello, cliquez sur **ACTIVE DIRECTORY**.

 ![Répertoire par défaut](./media/nps-extension-vpn/image23.png)

4. Dans la colonne de nom hello, cliquez sur **répertoire par défaut** (ou un autre annuaire, le cas échéant).
5. Dans la page de démarrage rapide de hello, cliquez sur **configurer**.

 ![Configuration par défaut](./media/nps-extension-vpn/image24.png)

6. Sur la page Configurer de hello, faites défiler la liste et, dans la section de l’authentification multifacteur hello, cliquez sur **gérer les paramètres de service**.

 ![Gérer les paramètres de l’authentification multifacteur](./media/nps-extension-vpn/image25.png)
 
7. Sur la page de l’authentification multifacteur hello, passez en revue les paramètres de service par défaut hello, puis cliquez sur **utilisateurs**. 

 ![Utilisateurs MFA](./media/nps-extension-vpn/image26.png)
 
8. Sur la page des utilisateurs hello, sélectionnez les utilisateurs de hello que vous souhaitez tooenable pour l’authentification Multifacteur, puis cliquez sur **activer**.

 ![Propriétés](./media/nps-extension-vpn/image27.png)
 
9. Lorsque vous y êtes invité, cliquez sur **Activer l’authentification multifacteur**.

 ![Activer la MFA](./media/nps-extension-vpn/image28.png)
 
10. Cliquez sur **Fermer**. 
11. Actualisez la page de hello. Hello, état de l’authentification Multifacteur est tooEnabled modifiée.

Pour plus d’informations sur la façon de tooenable les utilisateurs pour l’authentification multifacteur, consultez [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>Configurer des comptes pour la vérification en deux étapes
Une fois qu’un compte a été activé pour l’authentification Multifacteur, les utilisateurs ne sont pas en mesure de toosign dans tooresources régie par la stratégie d’authentification Multifacteur hello jusqu'à ce qu’ils ont correctement configuré un toouse appareil approuvé pour le second facteur d’authentification hello ayant utilisé vérification en deux étapes.

Dans cette section, configurez un périphérique approuvé pour une utilisation avec la vérification en deux étapes. Il existe plusieurs options pour vous tooconfigure ceux-ci, y compris hello suivantes :

* **Application mobile**. Vous installez hello Microsoft Authenticator application sur un appareil Windows Phone, Android ou iOS. Selon les stratégies de votre organisation, vous êtes application hello de toouse requis dans un des deux modes : recevoir des notifications de vérifications (une notification est envoyée tooyour appareil) ou utilisez le code de vérification (vous devez tooenter une vérification du code met à jour de toutes les 30 secondes). 
* **Appel ou SMS sur téléphone mobile**. Vous pouvez recevoir un appel téléphonique automatisé ou un message texte. Avec l’option d’appel téléphonique hello, vous répondez hello appel et appuyez sur tooauthenticate de signe # hello. Avec l’option de texte hello, vous pouvez répondre à un message texte toohello ou entrez le code de vérification hello dans l’interface de connexion hello.
* **Appel téléphonique au bureau**. Ce processus est hello même que celle décrite pour les appels téléphoniques automatisés ci-dessus.

Suivez ces instructions pour configurer une notification push appareil toouse hello application mobile tooreceive pour la vérification.

1. Ouverture de session trop[https://aka.ms/mfasetup](https://aka.ms/mfasetup) ou n’importe quel site, tel que [https://portal.azure.com](https://portal.azure.com), dans laquelle vous requises tooauthenticate à l’aide de vos informations d’identification de l’activation de l’authentification Multifacteur. 
2. Lors de la connexion avec votre nom d’utilisateur et le mot de passe, vous sont présentées avec un écran qui vous invite à entrer vous tooset compte hello pour la vérification de sécurité supplémentaire.

 ![Sécurité supplémentaire](./media/nps-extension-vpn/image29.png)

3. Cliquez sur **Configurer maintenant**.
4. Sur la page de vérification de sécurité supplémentaires de hello, sélectionnez un type de contact (téléphone d’authentification, téléphone ou application mobile). Puis sélectionnez un pays ou une région et une méthode. méthode Hello varie en fonction du type que vous sélectionnez. Par exemple, si vous choisissez application Mobile, vous pouvez sélectionner si tooreceive des notifications de vérification ou toouse un code de vérification. des étapes de Hello qui suivent supposent que vous choisissez **application Mobile** comme hello le type de contact.

 ![Authentification par téléphone](./media/nps-extension-vpn/image30.png)

5. Sélectionnez Application Mobile, cliquez sur **Recevoir des notifications pour la vérification**, puis sur **Configurer**. 

 ![Vérification par l’application mobile](./media/nps-extension-vpn/image31.png)
 
6. Si vous n’avez pas déjà fait, installez application mobile de hello authenticator sur votre appareil. 
7. Suivez les instructions de hello hello application mobile tooscan Bonjour présentées code-barres ou entrer manuellement les informations de hello, puis cliquez sur **fait**.

 ![Configurer l’application mobile](./media/nps-extension-vpn/image32.png)

8. Dans la page de vérification de sécurité supplémentaires de hello, cliquez sur **Contact me** et dispositif de tooyour toonotification envoyée de réponse.
9. Sur la page de vérification de sécurité supplémentaires de hello, entrez un numéro de contact au cas où vous perdez application mobile de toohello accès, puis cliquez sur **suivant**.

 ![Numéro de téléphone mobile](./media/nps-extension-vpn/image33.png)
 
10. Dans hello vérification de sécurité supplémentaire, cliquez sur **fait**.

Hello appareil est maintenant configuré tooprovide une deuxième méthode de vérification. Pour plus d’informations sur la configuration des comptes pour la vérification en deux étapes, consultez [Configurer mon compte pour la vérification en deux étapes](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Installer et configurer l’extension NPS

Cette section fournit des instructions pour la configuration de VPN toouse Azure MFA pour l’authentification du client avec hello serveur VPN.

Une fois que vous installez et configurez hello NPS extension, tout l’authentification du client RADIUS qui est traité par ce serveur est requis toouse Azure MFA. Si tous les utilisateurs de votre VPN sont inscrits dans l’authentification Multifacteur Azure, vous pouvez configurer un autre RADIUS server tooauthenticate les utilisateurs qui ne sont pas toouse configuré l’authentification Multifacteur. Ou vous pouvez créer une entrée de Registre qui permet aux utilisateurs récusé tooprovide un second facteur d’authentification, uniquement si elles sont inscrits dans l’authentification Multifacteur. 

Créer une nouvelle valeur de chaîne nommée _REQUIRE_USER_MATCH dans HKLM\SOFTWARE\Microsoft\AzureMfa_et hello valeur tooTRUE ou FALSE. 

 ![Exiger une correspondance d’utilisateur](./media/nps-extension-vpn/image34.png)
 
Si les valeur hello sont ensemble tooTRUE ou ne pas définie, toutes les demandes d’authentification sont une stimulation d’authentification Multifacteur sujet tooan. Si hello a la valeur tooFALSE, l’authentification Multifacteur défis sont émis uniquement toousers qui sont inscrits dans l’authentification Multifacteur. Utilisez uniquement hello paramètre FALSE dans le test ou dans les environnements de production pendant une période d’intégration.

### <a name="acquire-azure-active-directory-guid-id"></a>Acquérir l’ID du GUID Azure Active Directory

Dans le cadre de la configuration de hello Hello extension du serveur NPS, vous devez hello ID Azure Active Directory et les informations d’identification d’administrateur de toosupply pour votre locataire Azure AD. Hello étapes suivantes vous indiquent comment ID de tooget hello locataire.

1. Se connecter toohello portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com) en tant qu’administrateur global de hello Hello Azure locataire.
2. Bonjour barre de navigation gauche, cliquez sur hello **Azure Active Directory** icône.
3. Cliquez sur **Propriétés**.
4. toocopy votre dans le Presse-papiers de toohello ID de répertoire, sélectionnez hello **copie** icône.
 
 ![ID du répertoire](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Installation de l’extension de serveur NPS hello
Hello, extension de serveur NPS doit toobe installé sur un serveur qui a hello stratégie réseau et rôle de Services d’accès (NPS) est installé et qui fonctionne en tant que serveur RADIUS de hello dans votre conception. Extension NPS hello n’installez pas sur votre serveur de bureau à distance.

1. Télécharger l’extension de serveur NPS hello de [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Copiez le serveur NPS toohello hello le programme d’installation le fichier exécutable (NpsExtnForAzureMfaInstaller.exe).
3. Sur le serveur NPS de hello, double-cliquez sur **NpsExtnForAzureMfaInstaller.exe**. À l’invite, cliquez sur **Exécuter**.
4. Bonjour NPS Extension pour la boîte de dialogue de l’authentification Multifacteur Azure, consultez hello le contrat de licence, vérifiez **J’accepte les conditions générales du contrat de licence toohello**, puis cliquez sur **installer**.

 ![Extension NPS](./media/nps-extension-vpn/image36.png)
 
5. Bonjour NPS Extension pour la boîte de dialogue de l’authentification Multifacteur Azure, cliquez sur **fermer**.  

 ![Configuration réussie](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurer des certificats pour une utilisation avec l’extension de serveur NPS hello à l’aide d’un script PowerShell
tooensure des communications sécurisées et assurance, vous devez tooconfigure certificats pour une utilisation par extension NPS hello. composants du serveur NPS Hello incluent un script Windows PowerShell qui configure un certificat auto-signé à utiliser avec le serveur NPS. 

script de Hello exécute hello suivant des actions :

* crée un certificat auto-signé
* Associe la clé publique du certificat tooservice de principal sur Azure AD
* Magasins hello certificat dans le magasin de l’ordinateur local hello
* Attribution de l’accès toohello de clé privée du certificat toohello utilisateur réseau
* redémarre le service de serveur de stratégie réseau

Si vous souhaitez toouse vos propres certificats, vous avez besoin de votre principal de service de certificat toohello tooassociate hello public sur Azure AD et ainsi de suite.
script de hello toouse, fournissent les extension hello avec vos informations d’identification d’administration Active Directory de Azure et hello ID de locataire Azure Active Directory vous avez copiée précédemment. Exécuter les script hello sur chaque serveur NPS sur lequel vous installez l’extension de serveur NPS hello.

1. Ouvrez une invite administrative Windows PowerShell.
2. À l’invite de commandes PowerShell hello, tapez _cd « c:\Program Files\Microsoft\AzureMfa\Config »_, puis appuyez sur **entrée**.
3. Tapez _.\AzureMfsNpsExtnConfigSetup.ps1_, puis appuyez sur **ENTRÉE**. 
 * script de Hello vérifie toosee si le module Azure Active Directory PowerShell hello est installé. S’il n’est pas installé, script de hello installe le module de hello pour vous.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Une fois le script de hello vérifie l’installation de hello du module PowerShell de hello, il affiche la boîte de dialogue module Azure Active Directory PowerShell hello. Dans la boîte de dialogue hello, entrez vos informations d’identification d’administrateur d’Azure AD et un mot de passe, puis cliquez sur **connectez-vous**. 
 
 ![Connexion PowerShell](./media/nps-extension-vpn/image39.png)
 
5. Lorsque vous y êtes invité, collez l’ID de client hello copiés précédemment toohello Presse-papiers, puis appuyez sur **entrée**. 

 ![ID client](./media/nps-extension-vpn/image40.png)

6. script de Hello crée un certificat auto-signé et effectue d’autres modifications de configuration. sortie de Hello est comme image hello indiqué ci-dessous.

 ![Certificat auto-signé](./media/nps-extension-vpn/image41.png)

7. Redémarrez le serveur de hello.
 
### <a name="verify-configuration"></a>Vérifier la configuration
configuration de hello tooverify, vous devez tooestablish une connexion VPN avec le serveur VPN. Lors de l’entrée avec succès vos informations d’identification pour l’authentification principale, hello connexion VPN attend hello authentification secondaire toosucceed avant hello est établie, comme indiqué ci-dessous. 

 ![Vérifier la configuration](./media/nps-extension-vpn/image42.png)

Si vous authentifiez correctement avec la méthode de vérification secondaire hello que vous avez configuré précédemment dans l’authentification Multifacteur Azure, vous êtes connecté toohello ressource. Toutefois, si l’authentification secondaire hello n’a pas réussie, refusé accès tooresource. 

Dans l’exemple hello ci-dessous, hello authentificateur application sur un appareil Windows phone est l’authentification secondaire utilisé tooprovide hello.

 ![Vérifier le compte](./media/nps-extension-vpn/image43.png)

Une fois que vous avez correctement authentifié à l’aide de la méthode secondaire hello, vous disposez des accès toohello de port virtuel sur le serveur VPN de hello. Toutefois, étant requis toouse une méthode d’authentification secondaire à l’aide d’une application mobile sur un appareil de confiance, journal hello dans le processus est plus sécurisée qu’elle serait en utilisant uniquement un nom d’utilisateur / mot de passe.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Afficher les journaux de l’Observateur d’événements pour les événements de connexion réussie
tooview hello ouverture de session réussie des événements dans les journaux de l’Observateur d’événements Windows hello, vous pouvez émettre hello suivant du journal de sécurité Windows hello Windows PowerShell commande tooquery sur le serveur NPS de hello.

événements d’ouverture de session réussie tooquery dans les journaux Observateur d’événements de sécurité hello, utilisez hello suivant de commande,
* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 

 ![Observateur d’événements de sécurité](./media/nps-extension-vpn/image44.png)
 
Vous pouvez également afficher journal de sécurité hello ou hello stratégie réseau et accéder aux Services affichage personnalisé, comme indiqué ci-dessous :

 ![Accès à la stratégie réseau](./media/nps-extension-vpn/image45.png)

Sur serveur hello où vous avez installé les extensions du serveur NPS hello pour l’authentification Multifacteur Azure, vous trouverez des journaux de l’Observateur d’événements application extension toohello spécifique à **d’Application et de Services Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL

 ![Nombre d'événements](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Guide de résolution des problèmes
Si la configuration de hello ne fonctionne pas comme prévu, une tootroubleshoot de toostart parfait est tooverify qui hello utilisateur toouse configuré Azure MFA. Avoir les utilisateur hello vous connecter trop[https://portal.azure.com](https://portal.azure.com). S’ils sont invités à une vérification secondaire et peuvent correctement s’authentifier, vous pouvez éliminer une configuration incorrecte d’Azure MFA.

Si l’authentification Multifacteur Azure fonctionne pour les utilisateurs de hello, vous devez examiner les journaux d’événements appropriés hello. Il s’agit notamment des journaux des événements de sécurité, la passerelle opérationnelle et l’authentification Multifacteur Azure hello qui sont décrites dans la section précédente de hello. 

Voici un exemple de sortie du journal de sécurité montrant un échec d’événement de connexion (ID d’événement 6273) :

 ![Journal de sécurité](./media/nps-extension-vpn/image47.png)

Est un événement associé à partir des journaux de hello AzureMFA indiquée ci-dessous :

 ![Journaux Azure MFA](./media/nps-extension-vpn/image48.png)

tooperform avancée résoudre les options, consultez hello NPS de base de données journal des fichiers de format où hello service NPS est installé. Ces fichiers journaux sont créés dans le dossier _%SystemRoot%\System32\Logs_ comme fichiers texte délimité par des virgules. Pour obtenir une description de ces fichiers journaux, consultez [Interpréter des fichiers journaux au format base de données de serveur NPS](https://technet.microsoft.com/library/cc771748.aspx). 

les entrées de Hello dans ces fichiers journaux sont toointerpret difficile sans les importer dans une feuille de calcul ou une base de données. Vous pouvez trouver un nombre de tooassist en ligne des analyseurs de IAS dans interprétation hello des fichiers journaux. Voici sortie hello d’une telle téléchargeable [à contribution volontaire application](http://www.deepsoftware.com/iasviewer): 

 ![Application de logiciel à contribution volontaire](./media/nps-extension-vpn/image49.png)

Enfin, pour obtenir des options de résolution des problèmes supplémentaires, vous pouvez utiliser un analyseur de protocoles, tel que Wireshark ou [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). Hello l’image suivante à partir de Wireshark affiche les messages hello RADIUS entre le serveur VPN de hello et le serveur NPS de hello.

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

Pour plus d’informations, consultez [Intégrer votre infrastructure NPS existante à Azure Multi-Factor Authentication](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Étapes suivantes
[Comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)

[Passerelle des services Bureau à distance et serveur Multi-Factor Authentication avec RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Intégrer vos répertoires locaux à Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)

