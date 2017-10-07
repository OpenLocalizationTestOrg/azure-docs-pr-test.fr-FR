---
title: aaaConfigure Azure MFA | Documents Microsoft
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit le toodo ensuite avec l’authentification Multifacteur.  Cela inclut les rapports, l’alerte de fraude, le contournement à usage unique, les messages vocaux personnalisés, la mise en cache, les adresses IP approuvées et les mots de passe d’application."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 75af734e-4b12-40de-aba4-b68d91064ae8
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: kgremban
ms.openlocfilehash: db7d87d95b73fed78d3ce599fd03da9692851663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-settings"></a>Configurer les paramètres d’Azure Multi-Factor Authentication
Cet article vous aide à gérer Azure Multi-Factor Authentication, maintenant que vous êtes opérationnel.  Elle couvre les différentes rubriques qui vous aident à hello tooget meilleur parti de l’authentification multifacteur Azure.  Ces fonctionnalités ne sont pas disponibles dans toutes les versions d’Azure Multi-Factor Authentication.

| Fonctionnalité | Description | 
|:--- |:--- |
| [Alerte de fraude](#fraud-alert) |Alerte de fraude peut être configuré et afin que vos utilisateurs peuvent signaler les tentatives frauduleuses tooaccess leurs ressources. |
| [Contournement à usage unique](#one-time-bypass) |Un contournement à usage unique permet un tooauthenticate utilisateur une seule fois par « contournement » de l’authentification multifacteur. |
| [Messages vocaux personnalisés](#custom-voice-messages) |Autoriser les messages vocaux personnalisés vous toouse vos propres enregistrements ou greetings avec l’authentification multifacteur. |
| [Mise en cache](#caching-in-azure-multi-factor-authentication) |La mise en cache vous permet de tooset une période spécifique afin que les tentatives d’authentification suivantes réussissent automatiquement. |
| [Adresses IP approuvées](#trusted-ips) |Administrateurs d’un locataire géré ou fédéré peuvent utiliser vérification en deux étapes de toobypass des adresses IP approuvées pour les utilisateurs qui se connectent à partir de l’intranet local de l’entreprise hello. |
| [Mots de passe d'application](#app-passwords) |Un mot de passe permet à une application qui n’est pas l’authentification multifacteur toobypass prenant en charge l’authentification Multifacteur et continue à travailler. |
| [Mémoriser Multi-Factor Authentication pour les appareils et les navigateurs mémorisés](#remember-multi-factor-authentication-for-devices-that-users-trust) |Permet aux appareils de tooremember pour un nombre défini de jours après qu’un utilisateur a connecté avec succès à l’aide de l’authentification Multifacteur. |
| [Méthodes de vérification sélectionnables](#selectable-verification-methods) |Vous permet de méthodes d’authentification hello toochoose qui sont disponibles pour les utilisateurs toouse. |

## <a name="access-hello-azure-mfa-management-portal"></a>Hello d’accès portail de gestion de l’authentification Multifacteur Azure

les fonctions Hello abordées dans cet article sont configurées dans hello portail de gestion Azure multi-Factor Authentication. Il existe deux façons tooaccess hello portail de gestion de l’authentification Multifacteur via hello portail Azure classic. Hello est tout d’abord par la gestion d’un fournisseur d’authentification multifacteur. Hello est ensuite via les paramètres de service d’authentification Multifacteur hello. 

### <a name="use-an-authentication-provider"></a>Utiliser un fournisseur d’authentification

Si vous utilisez un fournisseur d’authentification multifacteur pour basée sur la consommation de l’authentification Multifacteur, utilisez ce portail de gestion de méthode tooaccess hello.

tooaccess hello du portail de gestion de l’authentification Multifacteur via un fournisseur de d’authentification multifacteur Azure, la connexion en hello portail classique Azure en tant qu’administrateur et option de hello Sélectionnez Active Directory. Cliquez sur hello **fournisseurs d’authentification multifacteur** onglet, puis le répertoire et cliquez sur hello **gérer** bouton bas hello.

### <a name="use-hello-mfa-service-settings-page"></a>Utilisez la page des paramètres de Service d’authentification Multifacteur hello 

Si vous avez hello suivant des licences, vous pouvez utiliser la page des paramètres de Service d’authentification Multifacteur hello :
- Azure MFA
- Azure AD Premium 
- Enterprise Mobility + Security

tooaccess hello du portail de gestion de l’authentification Multifacteur via la page Paramètres de Service d’authentification Multifacteur, l’authentification à hello portail classique Azure en tant qu’administrateur de hello et sélectionnez l’option d’Active Directory hello. Cliquez sur votre annuaire, puis sur hello **configurer** onglet. Sous la section de l’authentification multifacteur hello, sélectionnez **gérer les paramètres de service**. Bas hello de page de paramètres de Service d’authentification Multifacteur hello, cliquez sur hello **Go toohello portal** lien.


## <a name="fraud-alert"></a>Alerte de fraude
Alerte de fraude peut être configuré et afin que vos utilisateurs peuvent signaler les tentatives frauduleuses tooaccess leurs ressources.  Les utilisateurs peuvent signaler une fraude avec l’application mobile hello ou via son téléphone.

### <a name="set-up-fraud-alert"></a>Configurer l’alerte de fraude
1. Accédez toohello portail de gestion de l’authentification Multifacteur par les instructions hello haut hello de cette page.
2. Bonjour portail de gestion Azure multi-Factor Authentication, cliquez sur **paramètres** sous hello section de configuration.
3. Sous la section alerte de fraude de page de paramètres hello de hello, vérifiez hello **permettent aux utilisateurs des alertes de fraude toosubmit** case à cocher.
4. Sélectionnez **enregistrer** tooapply vos modifications. 

### <a name="configuration-options"></a>Options de configuration

- **Bloquer l’utilisateur en cas de signalement de fraude** - Si un utilisateur signale une fraude, son compte est bloqué.
- **Code fraude au cours de message d’accueil Initial de tooReport** -les utilisateurs appuient généralement sur vérification en deux étapes de tooconfirm #. S’ils veulent tooreport fraude, ils saisir un code avant d’appuyer sur #. Ce code est **0** par défaut, mais vous pouvez le personnaliser.

> [!NOTE]
> Les utilisateurs toopress # 0 toosubmit une alerte de fraude, demandez à accueil vocaux de valeur par défaut de Microsoft. Si vous voulez toouse un code différent de 0, vous devez enregistrer et charger vos propres messages sonores personnalisés avec les instructions appropriées.

![Options d’alerte fraude - Capture d’écran](./media/multi-factor-authentication-whats-next/fraud.png)

### <a name="how-users-report-fraud"></a>Procédure de signalement d’une fraude par les utilisateurs 
Une alerte de fraude peut être déclarée de deux façons.  Soit via l’application mobile hello ou par téléphone de hello.  

#### <a name="report-fraud-with-hello-mobile-app"></a>Signaler une fraude avec l’application mobile hello
1. Quand une vérification est envoyée tooyour téléphone, sélectionnez-le tooopen hello Microsoft Authenticator application.
2. Sélectionnez **Deny** lors de la notification de hello. 
3. Cliquez sur **Signaler une fraude**.
4. Hello fermer l’application.

#### <a name="report-fraud-with-a-phone"></a>Signaler une fraude à l’aide d’un téléphone
1. Lorsqu’un appel de vérification arrive tooyour téléphone, répondez-y.  
2. tooreport fraude, entrez le code de fraude hello (valeur par défaut est 0) et puis hello signe #. Vous êtes alors averti qu’une alerte de fraude a été soumise.
3. Fin de l’appel hello.

### <a name="view-fraud-reports"></a>Afficher les rapports de fraude
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Sur la gauche de hello, sélectionnez Active Directory.
3. En haut de hello, sélectionnez **fournisseurs d’authentification multifacteur** tooshow une liste de vos fournisseurs d’authentification multifacteur.
4. Sélectionnez votre fournisseur d’authentification multifacteur, cliquez sur **gérer** bas hello de page de hello. Hello portail de gestion Azure multi-Factor Authentication s’ouvre.
5. Dans hello multi-Factor Authentication portail de gestion Azure sous Afficher un rapport, cliquez sur **alerte fraude**.
6. Spécifiez la plage de dates de hello que vous le souhaitez tooview dans les rapports hello. Vous pouvez également spécifier des noms d’utilisateur, numéros de téléphone et l’état de l’utilisateur hello.
7. Cliquez sur **exécuter** tooshow un rapport des alertes de fraude. Cliquez sur **exporter tooCSV** si vous souhaitez tooexport hello rapport.

## <a name="one-time-bypass"></a>Contournement à usage unique
Un contournement à usage unique permet un tooauthenticate utilisateur une seule fois sans effectuer de vérification en deux étapes. Hello contournement est temporaire et expire après un nombre de secondes spécifié. Dans les situations où téléphone ou l’application mobile de hello ne reçoit une notification ou un appel téléphonique, vous pouvez activer un contournement à usage unique pour les utilisateur hello peuvent accéder aux ressources de hello souhaité.

### <a name="create-a-one-time-bypass"></a>Créer un contournement à usage unique
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Accédez toohello portail de gestion de l’authentification Multifacteur par les instructions hello haut hello de cette page.
3. Si vous voyez le nom hello de votre fournisseur d’authentification Multifacteur Azure sur hello gauche avec un  **+**  tooit suivant, cliquez sur hello  **+** . Différents groupes de réplication du serveur MFA et le groupe de hello Azure par défaut sont affichés. Sélectionnez le groupe approprié de hello.
4. Sous Administration des utilisateurs, sélectionnez **Contournement à usage unique**.
5. Dans la page de contournement à usage unique hello, cliquez sur **nouveau contournement à usage unique**.

  ![Cloud](./media/multi-factor-authentication-whats-next/create1.png)

6. Entrez nom d’utilisateur hello, durée hello du contournement de hello et raison hello hello contournement. Cliquez sur **Contournement**.
7. Hello délai entre en vigueur immédiatement, c’est le cas utilisateur hello toosign besoins dans avant de contournement à usage unique de hello arrive à expiration. 

### <a name="view-hello-one-time-bypass-report"></a>Rapport de contournement hello vue à usage unique
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Sur la gauche de hello, sélectionnez Active Directory.
3. En haut de hello, sélectionnez **fournisseurs d’authentification multifacteur** tooshow une liste de vos fournisseurs d’authentification multifacteur.
4. Sélectionnez votre fournisseur d’authentification multifacteur, cliquez sur **gérer** bas hello de page de hello. Hello portail de gestion Azure multi-Factor Authentication s’ouvre.
5. Dans le portail de gestion de Azure multi-Factor Authentication de hello sur hello gauche, sous Afficher un rapport, cliquez sur **contournement à usage unique**.
6. Spécifiez la plage de dates de hello que vous le souhaitez tooview dans les rapports hello. Vous pouvez également spécifier des noms d’utilisateur, numéros de téléphone et l’état de l’utilisateur hello.
7. Cliquez sur **exécuter** tooshow un rapport des contournements. Cliquez sur **exporter tooCSV** si vous souhaitez tooexport hello rapport.

## <a name="custom-voice-messages"></a>Messages vocaux personnalisés
Autoriser les messages vocaux personnalisés vous toouse vos propres enregistrements ou les salutations pour vérification en deux étapes. Vous pouvez utiliser des messages vocaux personnalisés dans les enregistrements de Microsoft addition tooor tooreplace hello.

Avant de commencer, tenez compte des points suivants :

* formats de fichier Hello pris en charge sont .wav et .mp3.
* limite de taille de fichier Hello est de 5 Mo.
* Les messages d’authentification doivent durer moins de 20 secondes. Les messages de plus de 20 secondes ne donner à des utilisateurs de hello suffisamment toorespond de temps avant de hello vérification délai écoulé.

### <a name="set-up-a-custom-message"></a>Configurer un message personnalisé

Il existe deux parties toocreating votre message personnalisé. Tout d’abord, vous téléchargez le message de type hello, puis vous l’activez pour vos utilisateurs.

tooupload votre message personnalisé :

1. Créer un message vocal personnalisé à l’aide d’un des formats de fichier hello pris en charge.
2. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
3. Accédez toohello portail de gestion de l’authentification Multifacteur par les instructions hello haut hello de cette page.
4. Bonjour portail de gestion Azure multi-Factor Authentication, cliquez sur **Messages vocaux** sous hello section de configuration.
5. Sur hello configurer : page de Messages de la voix, cliquez sur **nouveau Message vocal**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom1.png)
6. Sur hello configurer : page nouveaux Messages vocaux, cliquez sur **gérer les fichiers audio**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom2.png)
7. Sur hello configurer : fichiers audio, cliquez sur **télécharger le fichier audio**.
   ![Cloud](./media/multi-factor-authentication-whats-next/custom3.png)
8. Sur hello configurer : télécharger un fichier audio, cliquez sur **Parcourir** et accédez tooyour vocal, cliquez sur **ouvrir**.
9. Ajoutez une description et cliquez sur **Télécharger**.
10. Une fois que le message d’appel vocal est chargé, un message confirme que vous avez téléchargé hello.

tooturn sur le message de type hello pour vos utilisateurs :

1. Sur hello gauche, cliquez sur **Messages vocaux**.
2. Sous hello section Messages vocaux, cliquez sur **nouveau Message vocal**.
3. Dans la liste déroulante langue de hello, sélectionnez une langue.
4. Si ce message est pour une application spécifique, spécifier dans la boîte de l’Application hello.
5. À partir de la liste déroulante Type de Message de hello, sélectionnez toobe de type de message hello remplacé par votre nouveau message personnalisé.
6. À partir de hello son fichier de liste déroulante, sélectionnez fichier audio hello que vous avez téléchargé dans la première partie de hello.
7. Cliquez sur **Créer**. Un message confirme que vous avez créé un message vocal.
    ![Cloud](./media/multi-factor-authentication-whats-next/custom5.png)</center>

## <a name="caching-in-azure-multi-factor-authentication"></a>Mise en cache dans Azure Multi-Factor Authentication
La mise en cache vous permet de tooset une période spécifique pour que les tentatives d’authentification suivantes dans le délai imparti aboutissent automatiquement. Mise en cache est utilisée lorsque les systèmes locaux tels que VPN envoyer de demandes de vérification lors de la première demande de hello est toujours en cours. Autorisant hello les demandes suivantes toosucceed automatiquement une fois hello réussit la première vérification de hello en cours. 

La mise en cache n’est pas prévue toobe utilisé pour les connexions tooAzure AD.

### <a name="set-up-caching"></a>Configurer la mise en cache 
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Accédez toohello portail de gestion de l’authentification Multifacteur par les instructions hello haut hello de cette page.
3. Bonjour portail de gestion Azure multi-Factor Authentication, cliquez sur **mise en cache** sous hello section de configuration.
4. Cliquez sur **nouveau Cache** sur la page de mise en cache de configurer hello.
5. Sélectionnez le type de Cache hello et les secondes du cache hello. Cliquez sur **Créer**.

<center>![Cloud](./media/multi-factor-authentication-whats-next/cache.png)</center>

## <a name="trusted-ips"></a>Adresses IP approuvées
Adresses IP approuvées sont une fonctionnalité de l’authentification Multifacteur Azure que les administrateurs d’un locataire géré ou fédéré peuvent utiliser la vérification en deux étapes de toobypass. Qui est utilisé pour les utilisateurs qui sont connectent à partir de l’intranet local de l’entreprise hello. Cette fonctionnalité est disponible avec la version complète de hello d’Azure multi-Factor Authentication, pas hello version gratuite pour les administrateurs. Pour plus d’informations sur la façon dont tooget hello version complète de l’authentification multifacteur Azure, consultez [Azure multi-Factor Authentication](multi-factor-authentication.md).

| Type de client Azure AD | Options d’Adresses IP approuvées disponibles |
|:--- |:--- |
| Adresses IP gérées |<li>Plages d’adresses IP spécifiques – les administrateurs peuvent spécifier une plage d’adresses IP qui peuvent contourner la vérification en deux étapes pour les utilisateurs qui se connectent à partir de l’intranet de l’entreprise hello.</li> |
| Adresses IP fédérées |<li>Tous les utilisateurs fédérés : tous les utilisateurs fédérés qui sont connectent dans à partir d’à l’intérieur de hello organisation contournent vérification en deux étapes à l’aide d’une revendication émise par AD FS.</li><br><li>Plages d’adresses IP spécifiques – les administrateurs peuvent spécifier une plage d’adresses IP qui peuvent contourner la vérification en deux étapes pour les utilisateurs qui se connectent à partir de l’intranet de l’entreprise hello. |

Ce contournement ne fonctionne qu’à partir de l'intranet d'une entreprise. 

**Expérience de l’utilisateur final au sein du réseau d’entreprise :**

Lorsque la fonction Adresses IP approuvées est désactivée, la vérification en deux étapes est requise pour les flux de navigateur et les mots de passe d’application sont requis pour les applications client riches plus anciennes. 

Quand la fonction Adresses IP approuvées est activée, la vérification en deux étapes n’est *pas* nécessaire pour les flux de navigateur. Mots de passe d’application sont *pas* requis pour les applications clientes riches plus anciens, autant que hello utilisateur n’a pas déjà créé un mot de passe. Une fois qu’un mot de passe est en cours d’utilisation, il reste requis. 

**Expérience de l’utilisateur final en dehors du réseau d’entreprise :**

Que la fonction Adresses IP approuvées soit activée ou non, la vérification en deux étapes est requise pour les flux de navigateur et les mots de passe d’application sont requis pour les applications client riches plus anciennes. 

### <a name="tooenable-trusted-ips"></a>tooenable d’adresses IP de confiance
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Parcourir la page des paramètres de Service d’authentification Multifacteur toohello par des instructions au début de hello hello de cet article.
3. Sur la page Paramètres du Service hello, sous adresses IP approuvées, vous avez deux options :
   
   * **Pour les demandes des utilisateurs fédérés provenant de mon intranet** : case à cocher hello. Tous les utilisateurs fédérés qui sont connectent à partir de la vérification en deux étapes hello réseau d’entreprise consistant à ignorer sont à l’aide d’une revendication émise par AD FS.
   * **Pour les demandes à partir d’une plage spécifique d’adresses IP publiques** – Entrez les adresses IP de hello dans la zone de texte hello fournie à l’aide de la notation CIDR. Par exemple : xxx.xxx.xxx.0/24 pour les adresses IP de hello plage xxx.xxx.xxx.1 – xxx.xxx.xxx.254, ou xxx.xxx.xxx.xxx/32 pour une adresse IP unique. Vous pouvez entrer des plages d’adresses IP too50. Les utilisateurs qui se connectent à partir de ces adresses IP contournent la vérification en deux étapes.
4. Cliquez sur **Enregistrer**.
5. Une fois les mises à jour hello ont été appliquées, cliquez sur **fermer**.

![Adresses IP approuvées](./media/multi-factor-authentication-whats-next/trustedips3.png)

## <a name="app-passwords"></a>Mots de passe d'application
Certaines applications, telles qu’Office 2010 ou version antérieure et qu’Apple Mail, ne prennent pas en charge la vérification en deux étapes. Ils ne sont pas tooaccept configuré une vérification du second. toouse ces applications, vous devez toouse « application des mots de passe » à la place de votre mot de passe traditionnel. mot de passe Hello permet hello application toobypass vérification en deux étapes et continuer à travailler.

> [!NOTE]
> Authentification moderne pour hello des Clients Office 2013
> 
> Clients Office 2013 (y compris Outlook) et nouveaux protocoles d’authentification moderne de prise en charge et peut être activé toowork avec la vérification en deux étapes. Une fois activés, les mots de passe d’application ne sont pas requis pour ces clients.  Pour plus d’informations, consultez [Version préliminaire publique de l’authentification moderne Office 2013 annoncée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

### <a name="important-things-tooknow-about-app-passwords"></a>Tooknow points importants sur les mots de passe d’application
Voici une liste des points importants à retenir sur les mots de passe d’application.

* Mots de passe d’application doivent être entrés dans la zone d’entrée de hello une fois par application. Les utilisateurs n’ont tookeep trace et les entrer chaque fois.
* mot de passe Hello est généré automatiquement et n’est pas fourni par l’utilisateur de hello. mot de passe généré automatiquement Hello est plus difficile pour une personne malveillante tooguess et est plus sécurisée.
* Un utilisateur peut posséder jusqu’à 40 mots de passe. 
* Applications qui mettent en cache les mots de passe et l’utilisation dans les scénarios sur site peuvent se mettent à échouer, car le mot de passe hello n’est pas connu en dehors de l’id d’organisation hello. Par exemple, des messages électroniques Exchange sur site, mais les messages hello archivé se trouvent dans le cloud de hello. Hello même mot de passe ne fonctionne pas.
* Au démarrage de l’authentification multifacteur, vous pouvez utiliser votre mot de passe avec certains clients autres que des navigateurs. Vous ne pouvez pas utiliser les mots de passe d’application pour les tâches d’administration. Assurez-vous de créer un compte de service avec un script PowerShell de toorun mot de passe fort et n’activez pas ce compte pour la vérification en deux étapes.

> [!WARNING]
> Les mots de passe d’application ne fonctionnent pas dans les environnements hybrides où les clients communiquent avec les points de terminaison locaux et les points de terminaison à découverte automatique cloud. Mots de passe de domaine sont requis tooauthenticate localement et mots de passe d’application sont requis tooauthenticate avec le cloud de hello.

### <a name="naming-guidance-for-app-passwords"></a>Recommandations en matière d'affectation de noms pour les mots de passe d'application
Noms de mot de passe d’application doivent refléter le périphérique hello sur lesquels ils sont utilisés. Par exemple, si vous disposez d’un ordinateur portable qui contient des applications autres que des navigateurs, créez un mot de passe d’application unique intitulé Ordinateur portable et servez-vous en. Ensuite, créez un autre mot de passe nommé bureau pour hello mêmes applications sur votre ordinateur de bureau. 

Microsoft recommande de créer un mot de passe par appareil, et non un mot de passe d’application par application.

### <a name="federated-sso-app-passwords"></a>Mots de passe d'application fédérés (SSO)
Azure AD prend en charge la fédération (authentification unique) avec les services de domaine Windows Server Active Directory (AD DS) locaux. Si votre organisation est fédérée avec Azure AD et que vous vous apprêtez toobe à l’aide de l’authentification multifacteur Azure, hello plus d’informations sur les mots de passe app sont importants pour vous. Cette section concerne uniquement les clients toofederated (SSO).

* Les mots de passe d’application sont vérifiés par Azure AD et contournent ainsi la fédération. La fédération n’est utilisée activement que lorsque vous configurez les mots de passe d’application.
* Pour les utilisateurs fédérés (SSO), jamais aller toohello fournisseur d’identité (IdP) à la différence des flux passif de hello. les mots de passe Hello sont stockés dans l’id d’organisation hello. Si l’utilisateur de hello quitte la société de hello, ces informations a les id de tooorganizational tooflow à l’aide de la synchronisation d’annuaire en temps réel. La désactivation/suppression de compte peut prendre jusqu'à toothree heures toosync, retardant la désactivation/suppression de mot de passe dans Azure AD.
* Les paramètres de contrôle d'accès client locaux ne sont pas honorés par Mot de passe d’application
* Aucune authentification locale de journalisation/fonctionnalité d’audit n’est disponible pour les mots de passe d’application.
* Certaines conceptions architecturales avancées peuvent exiger une combinaison de noms d’utilisateur, de mots de passe et de mots de passe d’application quand la vérification en deux étapes est utilisée avec les clients. Cependant, cela dépend de là où ils s’authentifient. Pour les clients qui s'authentifient auprès d'une infrastructure locale, vous utiliseriez le nom d'utilisateur et le mot de passe d’une organisation. Pour les clients qui s’authentifient auprès d’Azure AD, vous devez utiliser le mot de passe hello.

  Supposons, par exemple, que vous disposez d'une architecture qui se compose des instances suivantes :

  * Vous fédérez votre instance locale d'Active Directory avec Azure AD
  * Vous utilisez Exchange Online
  * Vous utilisez Lync qui est spécifiquement local
  * Vous utilisez Azure Multi-Factor Authentication

  ![Vérification](./media/multi-factor-authentication-whats-next/federated.png)

  Dans ces instances, vous devez suivre ces étapes :

  * Lors de la signature-dans tooLync, utilisez le nom d’utilisateur et mot de passe de votre organisation.
  * Lors de la tentative de carnet d’adresses tooaccess hello via un client Outlook qui se connecte tooExchange en ligne, utilisez un mot de passe.

### <a name="allow-app-password-creation"></a>Autoriser la création de mots de passe d’application
Par défaut, les utilisateurs ne peuvent pas créer des mots de passe d’application, mais vous pouvez activer la fonctionnalité de hello vous-même. tooallow utilisateurs hello des mots de passe d’application toocreate possibilité, utilisez les hello procédure :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Parcourir la page des paramètres de Service d’authentification Multifacteur toohello par des instructions au début de hello hello de cet article.
3. Sélectionnez le bouton radio de hello suivant trop**autoriser les utilisateurs toocreate application des mots de passe toosign dans les applications non-Web**.

![Création de mots de passe d'application](./media/multi-factor-authentication-whats-next/trustedips3.png)

### <a name="create-app-passwords"></a>Créer des mots de passe d’application
Les utilisateurs peuvent créer des mots de passe d'application lors de leur inscription initiale. Ils ont la possibilité à fin hello du processus d’inscription hello qui leur permet de mots de passe d’application toocreate.

Les utilisateurs peuvent aussi créer des mots de passe d’application après l’inscription. Ils peuvent créer des mots de passe d’application hello en modifiant leurs paramètres Bonjour portail Office 365 Azure pour le portail ou hello. Pour plus d’informations et pour connaître les étapes détaillées pour vos utilisateurs, consultez [Que sont les mots de passe d’application dans Azure Multi-Factor Authentication ?](./end-user/multi-factor-authentication-end-user-app-passwords.md).

## <a name="remember-multi-factor-authentication-for-devices-that-users-trust"></a>Mémoriser Multi-Factor Authentication pour les appareils utilisateur de confiance
La mémorisation Multi-Factor Authentication pour les appareils et les navigateurs de confiance est une fonctionnalité disponible gratuitement pour tous les utilisateurs MFA. L’authentification multifacteur permet utilisateurs tooby passe l’authentification Multifacteur pour un nombre défini de jours après l’ouverture de session. Cette fonctionnalité améliore la facilité d’utilisation en réduisant le nombre de hello de fois où un utilisateur peut effectuer la vérification en deux étapes sur hello même appareil.

Toutefois, si un appareil ou un compte est compromis, la mémorisation MFA des appareils de confiance est susceptible d’affecter la sécurité. Si un compte d’entreprise est compromis ou un périphérique de confiance est perdu ou volé, vous devez trop[restaurer l’authentification multifacteur sur tous les appareils](multi-factor-authentication-manage-users-and-devices.md#restore-mfa-on-all-remembered-devices-for-a-user). Cette action révoque l’état de hello approuvé à partir de tous les périphériques et utilisateur de hello est vérification en deux étapes tooperform requis. Vous pouvez également demander à votre toorestore utilisateurs l’authentification Multifacteur sur leurs propres appareils avec des instructions de hello dans [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md#require-two-step-verification-again-on-a-device-youve-marked-as-trusted)

### <a name="how-it-works"></a>Fonctionnement

Mémoriser l’authentification multifacteur fonctionne en définissant un cookie persistant sur le navigateur de hello lorsqu’un utilisateur archive hello « ne plus me demander pour **X** jours « zone à la connexion. Hello utilisateur ne sera pas invité pour l’authentification Multifacteur à nouveau à partir de ce navigateur avant l’expiration du cookie de hello. Si l’utilisateur de hello ouvre un autre navigateur sur hello même appareil ou efface les cookies, qu’ils soient de nouveau invité à tooverify. 

Hello « ne plus me demander pour **X** jours « case à cocher n’est pas affiché dans les applications non-Web, ils prennent en charge l’authentification moderne ou non. Ces applications utilisent des jetons d’actualisation qui fournissent de nouveaux jetons d’accès toutes les heures. Lorsqu’un jeton d’actualisation est validé, Azure AD vérifie la vérification de hello dernière heure en deux étapes a été effectuée dans le nombre de hello configuré de jours. 

En conclusion, sans oublier l’authentification Multifacteur sur les appareils de confiance réduit hello nombre d’authentifications sur les applications web (qui normalement, demandez à chaque fois). Mais il augmente également le nombre de hello d’authentifications pour les clients de l’authentification moderne (qui normalement de demander à tous les 90 jours).

> [!NOTE]
>Cette fonctionnalité n’est pas compatible avec la fonctionnalité de « Maintenir la connexion » hello d’AD FS lorsque les utilisateurs effectuent la vérification en deux étapes pour AD FS via hello serveur Azure MFA ou une solution d’authentification Multifacteur tierces. Vos utilisateurs, sélectionnez « Maintenir la connexion » sur AD FS et également marquer leur appareil, un niveau de confiance pour l’authentification Multifacteur, ils ne sont pas en mesure de tooverify après expiration de hello nombre « N’oubliez pas l’authentification Multifacteur » de jours. Azure AD demande une vérification en deux étapes frais, mais AD FS retourne un jeton avec la revendication de l’authentification Multifacteur hello d’origine et la date au lieu d’effectuer la vérification en deux étapes. Ce processus déclenche une boucle de vérification entre Azure AD et AD FS. 

### <a name="enable-remember-multi-factor-authentication"></a>Activer Mémoriser Multi-Factor Authentication
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Parcourir la page des paramètres de Service d’authentification Multifacteur toohello par des instructions au début de hello hello de cet article.
3. Sur la page Paramètres du Service de hello, sous Gérer les paramètres de périphérique utilisateur, vérifiez hello **autoriser les utilisateurs tooremember l’authentification multifacteur sur leurs appareils de confiance** boîte.
   ![Mémoriser des appareils](./media/multi-factor-authentication-whats-next/remember.png)
4. Définir hello nombre de jours que vous souhaitez le vérification en deux étapes toobypass tooallow hello approuvé périphériques. valeur par défaut Hello est de 14 jours.
5. Cliquez sur **Enregistrer**.
6. Cliquez sur **Fermer**.

### <a name="mark-a-device-as-trusted"></a>Marquer un appareil en tant qu’appareil de confiance

Une fois cette fonctionnalité activée, les utilisateurs peuvent marquer un appareil comme approuvé lorsqu’ils se connectent en cochant **Ne plus demander**.

![Ne plus demander - Capture d’écran](./media/multi-factor-authentication-whats-next/trusted.png)

## <a name="selectable-verification-methods"></a>Méthodes de vérification sélectionnables
Vous pouvez choisir les méthodes de vérification mises à la disposition de vos utilisateurs. Hello tableau suivant fournit une brève vue d’ensemble de chaque méthode.

Lorsque vos utilisateurs inscrivent leurs comptes pour l’authentification Multifacteur, ils choisir leur méthode de vérification préférée options hello que vous avez activée. conseils de Hello pour leurs processus d’inscription sont couvert dans [configurer mon compte pour la vérification en deux étapes](multi-factor-authentication-end-user-first-time.md)

| Méthode | Description |
|:--- |:--- |
| Appel toophone |Passe un appel vocal automatisé. Hello utilisateur réponses hello appel et appuie sur # dans hello phone pavé tooauthenticate. Ce numéro de téléphone n’est pas synchronisé tooon local Active Directory. |
| Toophone de message texte |Envoie un message texte contenant un code de vérification. l’utilisateur Hello est toohello texte de la réponse tooeither demandée, le message avec le code de vérification hello ou code de vérification tooenter hello dans l’interface de connexion hello. |
| Notification via une application mobile |Envoie un téléphone de tooyour de notification push ou d’un appareil inscrit. vues de notification de hello Hello utilisateur et sélectionne **Vérifiez** toocomplete vérification. <br>application de Microsoft Authenticator Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| Code de vérification de l’application mobile |application de Microsoft Authenticator Hello génère un nouveau code de vérification OATH toutes les 30 secondes. utilisateur de Hello entre ce code de vérification dans l’interface de connexion hello.<br>application de Microsoft Authenticator Hello est disponible pour [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), et [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |

### <a name="how-tooenabledisable-authentication-methods"></a>Comment tooenable ou désactiver les méthodes d’authentification
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Parcourir la page des paramètres de Service d’authentification Multifacteur toohello par des instructions au début de hello hello de cet article.
3. Sur la page Paramètres du Service hello, sous options de vérification, sélectionnez/désélectionnez les options de hello toouse de votre choix.
   ![Options de vérification](./media/multi-factor-authentication-whats-next/authmethods.png)
4. Cliquez sur **Save**.
5. Cliquez sur **Fermer**.
