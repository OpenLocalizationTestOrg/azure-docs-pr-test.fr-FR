---
title: portail aaaUser pour le serveur Azure MFA | Documents Microsoft
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget démarrer avec Azure MFA et le portail de l’utilisateur hello."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portail de l’utilisateur pour hello serveur Azure multi-Factor Authentication

portail de l’utilisateur Hello est un site web IIS qui permet aux utilisateurs tooenroll dans Azure multi-Factor Authentication (MFA) et de gérer leurs comptes. Un utilisateur peut modifier son numéro de téléphone, modifier leur code PIN ou choisissez toobypass vérification en deux étapes lors de leur ouverture de session suivante.

Les utilisateurs connectez-vous au portail de l’utilisateur toohello avec leur nom d’utilisateur normal et le mot de passe, puis effectuent un appel de vérification en deux étapes ou répondent toocomplete des questions de sécurité leur authentification. Si l’inscription de l’utilisateur est autorisée, les utilisateurs configurer leur numéro de téléphone et hello du code confidentiel moment de sa première que connexion dans le portail de l’utilisateur toohello.

Portail de l’utilisateur les administrateurs peut-être configurer et accordé l’autorisation tooadd nouveaux utilisateurs et mise à jour des utilisateurs existants.

Selon votre environnement, vous souhaiterez peut-être portail de l’utilisateur toodeploy hello sur hello même serveur comme serveur Azure multi-Factor Authentication ou sur un autre serveur connecté à internet.

![Portail de l’utilisateur MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portail de l’utilisateur Hello est uniquement disponible avec le serveur multi-Factor Authentication. Si vous utilisez l’authentification multifacteur dans le cloud de hello, consultez votre toohello utilisateurs [votre compte pour la vérification en deux étapes de configuration](./end-user/multi-factor-authentication-end-user-first-time.md) ou [gérer vos paramètres de vérification en deux étapes](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Installer le service web de hello SDK

Dans les deux cas, si hello le SDK Service Web Azure multi-Factor Authentication est **pas** déjà installé sur le serveur Azure multi-Factor Authentication (MFA) de hello, hello terminé les étapes qui suivent.

1. Ouvrez la console du serveur multi-Factor hello.
2. Accédez toohello **SDK du Service Web** et sélectionnez **installer le SDK du Service Web**.
3. Installation hello complète à l’aide des valeurs par défaut hello, sauf si vous avez besoin de toochange pour une raison quelconque.
4. Lier à un site toohello de certificat SSL dans IIS.

Si vous avez des questions sur la configuration d’un certificat SSL sur un serveur IIS, voir l’article hello [comment tooSet configuration de SSL sur IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hello SDK du Service Web doit être sécurisé avec un certificat SSL. Un certificat auto-signé peut être ajouté à cet effet. Importer le certificat de hello dans le magasin de « Trusted Root Certification Authorities » hello hello Local du compte d’ordinateur sur le serveur web du portail utilisateur hello afin qu’il approuve ce certificat lors de l’ouverture de connexion SSL de hello.

![Kit de développement logiciel (SDK) du Service Web d’installation du serveur MFA](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Déployer le portail de l’utilisateur hello sur hello même serveur que hello serveur Azure multi-Factor Authentication

Hello conditions préalables suivantes sont requises tooinstall portail de l’utilisateur hello sur hello **même serveur** comme hello du serveur Azure multi-Factor Authentication :

* IIS, avec ASP.net et IIS 6 avec compatibilité de la métabase (pour IIS 7 ou version ultérieure)
* Un compte avec des droits d’administrateur sur l’ordinateur de hello et domaine le cas échéant. compte de Hello a besoin de groupes de sécurité Active Directory autorisations toocreate.
* Portail de l’utilisateur hello sécurisé avec un certificat SSL.
* Hello SDK du Service Azure multi-Factor d’authentification Web sécurisé avec un certificat SSL.

toodeploy hello ces étapes à suivre de portail, utilisateur :

1. Ouvrez la console du serveur Azure multi-Factor Authentication hello, cliquez sur hello **portail de l’utilisateur** icône Bonjour gauche menu, puis cliquez sur **installer le portail utilisateur**.
2. Installation hello complète à l’aide des valeurs par défaut hello, sauf si vous avez besoin de toochange pour une raison quelconque.
3. Lier un site toohello de certificat SSL dans IIS

   > [!NOTE]
   > Le certificat SSL est généralement un certificat SSL signé publiquement.

4. Ouvrez un navigateur web à partir de n’importe quel ordinateur et accédez URL toohello où le portail de l’utilisateur hello a été installé (exemple : https://mfa.contoso.com/MultiFactorAuth). Assurez-vous qu'aucun avertissement ou erreur de certificat ne soit affiché.

![Installation du portail de l’utilisateur du serveur MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Si vous avez des questions sur la configuration d’un certificat SSL sur un serveur IIS, voir l’article hello [comment tooSet configuration de SSL sur IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Déployer le portail de l’utilisateur sur un serveur distinct hello

Si le serveur de hello où le serveur Azure multi-Factor Authentication est en cours d’exécution n’est pas connecté à internet, vous devez installer le portail de l’utilisateur hello sur un **serveur distinct, sur internet**.

Si votre organisation utilise hello application Authenticator de Microsoft comme l’une des méthodes de vérification hello et souhaitez le portail de l’utilisateur toodeploy hello sur son propre serveur, effectuez hello suivant les exigences :

* Utilisez la version 6.0 ou ultérieure du serveur Azure multi-Factor Authentication de hello.
* Installer le portail de l’utilisateur hello sur un serveur de web orienté internet exécutant Microsoft internet Information Services (IIS) 6.x ou version ultérieure.
* Lorsque vous utilisez IIS 6.x, assurez-vous d’ASP.NET v2.0.50727 est installé, inscrit et définir trop**autorisées**.
* Lorsque vous utilisez IIS 7.x ou une version ultérieure, IIS, y compris l’authentification de base, ASP.NET et IIS 6 avec compatibilité de la métabase.
* Portail de l’utilisateur hello sécurisé avec un certificat SSL.
* Hello SDK du Service Azure multi-Factor d’authentification Web sécurisé avec un certificat SSL.
* Vérifiez que ce portail hello de l’utilisateur peut se connecter à toohello le SDK Service Web Azure multi-Factor Authentication via le protocole SSL.
* Assurez-vous que portail de l’utilisateur hello peut authentifier toohello le SDK Service Web Azure multi-Factor Authentication avec des informations d’identification de hello d’un compte de service dans le groupe de sécurité « Administrateurs PhoneFactor » hello. Ce compte de service et ce groupe doivent exister dans Active Directory si hello serveur Azure multi-Factor Authentication s’exécute sur un serveur appartenant à un domaine. Ce compte de service et ce groupe existent localement sur hello serveur Azure multi-Factor Authentication s’il n’est pas tooa joint à un domaine.

Portail de l’utilisateur hello lors de l’installation sur un serveur autre que hello serveur Azure multi-Factor nécessite hello comme suit :

1. **Sur le serveur MFA de hello**, parcourir le chemin d’installation de toohello (exemple : C:\Program Files\Multi-Factor Authentication Server) et copier le fichier hello **MultiFactorAuthenticationUserPortalSetup64** tooa emplacement serveur d’Internet accessible toohello où vous souhaitez l’installer.
2. **Serveur de web exposés à internet hello**, exécutez le fichier d’installation de hello MultiFactorAuthenticationUserPortalSetup64 en tant qu’administrateur, modifiez hello Site si vous le souhaitez et modifier le nom court du tooa répertoire virtuel hello si vous souhaitez.
3. Lier à un site toohello de certificat SSL dans IIS.

   > [!NOTE]
   > Le certificat SSL est généralement un certificat SSL signé publiquement.

4. Parcourir trop**C:\inetpub\wwwroot\MultiFactorAuth**
5. Modifier le fichier Web.Config de hello dans le bloc-notes

    * Trouver la clé de hello **« USE_WEB_SERVICE_SDK »** et modifiez **valeur = « false »** trop**valeur = « true »**
    * Trouver la clé de hello **« WEB_SERVICE_SDK_AUTHENTICATION_USERNAME »** et modifiez **valeur = « «** trop**valeur = « Domaine\utilisateur »** où domaine\nom d’utilisateur est un compte de Service qui fait partie de Groupe de « PhoneFactor Admins ».
    * Trouver la clé de hello **« WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD »** et modifiez **valeur = « «** trop**valeur = « Password »** où le mot de passe est un mot de passe hello pour hello Service Compte entré dans la ligne précédente de hello.
    * Rechercher la valeur de hello **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** et modifier ce toohello de URL d’espace réservé URL du Service Web SDK nous installés à l’étape 2.
    * Enregistrez le fichier Web.Config de hello et fermez le bloc-notes.

6. Ouvrez un navigateur web à partir de n’importe quel ordinateur et accédez URL toohello où le portail de l’utilisateur hello a été installé (exemple : https://mfa.contoso.com/MultiFactorAuth). Assurez-vous qu'aucun avertissement ou erreur de certificat ne soit affiché.

Si vous avez des questions sur la configuration d’un certificat SSL sur un serveur IIS, voir l’article hello [comment tooSet configuration de SSL sur IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurer les paramètres du portail utilisateur Bonjour serveur Azure multi-Factor Authentication

Maintenant que portail de l’utilisateur hello est installé, vous devez tooconfigure hello serveur Azure multi-Factor Authentication toowork avec le portail de hello.

1. Dans la console du serveur Azure multi-Factor Authentication hello, cliquez sur hello **portail de l’utilisateur** icône. Sur l’onglet Paramètres de hello, entrez le portail de l’utilisateur toohello hello URL Bonjour **URL du portail utilisateur** zone de texte. Si la fonctionnalité de courrier électronique a été activée, cette URL est incluse dans les messages électroniques hello envoyés toousers lorsqu’ils sont importés dans hello serveur Azure multi-Factor Authentication.
2. Choisissez les paramètres de hello que vous souhaitez toouse Bonjour portail de l’utilisateur. Par exemple, si les utilisateurs sont autorisés à toochoose leurs méthodes d’authentification, assurez-vous que **permettent aux utilisateurs tooselect méthode** est activée, ainsi que les méthodes hello ils peuvent choisir de.
3. Définir qui doivent être des administrateurs sur hello **administrateurs** onglet. Vous pouvez créer des autorisations administratives précises à l’aide des cases à cocher hello et les menus déroulants dans les boîtes d’ajouter/modifier hello.

Configuration facultative :
- **Les Questions de sécurité** -définir approuvé les questions de sécurité pour votre langage de l’environnement et hello qu’ils s’affichent dans.
- **Sessions précédentes** : configurez l’intégration du portail utilisateur avec un site Web basé sur le formulaire à l’aide de MFA.
- **Adresses IP approuvées** -autoriser les utilisateurs tooskip l’authentification Multifacteur lors de l’authentification à partir d’une liste de confiance des adresses IP ou des plages.

![Configuration du portail de l’utilisateur du serveur MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Serveur de l’authentification multifacteur Azure fournit plusieurs options pour le portail de l’utilisateur hello. Hello tableau suivant fournit une liste de ces options et une explication de leur utilisation.

| Paramètres du portail de l'utilisateur | Description |
|:--- |:--- |
| URL du portail de l'utilisateur | Entrez les URL de hello de hébergeant le portail de hello. |
| Authentification principale | Spécifiez type hello de toouse d’authentification lors de la connexion toohello portal. Authentification Windows, Radius ou LDAP. |
| Autoriser toolog utilisateurs dans | Autoriser les utilisateurs tooenter un nom d’utilisateur et un mot de passe sur hello-page de connexion pour le portail de l’utilisateur hello. Si cette option n’est pas sélectionnée, les zones de hello apparaissent en grisé. |
| Autoriser l'inscription utilisateur | Autoriser un tooenroll utilisateur dans l’authentification multifacteur en les mettant écran installation tooa qui les invite à entrer des informations supplémentaires telles que le numéro de téléphone. Invite pour téléphone de secours permet aux utilisateurs toospecify un numéro de téléphone secondaire. Invite pour le tiers jeton OATH permet d’utilisateurs toospecify jeton OATH tiers. |
| Autoriser les utilisateurs tooinitiate contournement à usage unique | Autoriser les utilisateurs tooinitiate un contournement à usage unique. Si un utilisateur configure cette option, elle prendra hello d’effet prochaine hello utilisateur se connecte. Choisir le contournement secondes fournit hello utilisateur une zone afin qu’ils peuvent modifier hello comme valeur par défaut 300 secondes. Dans le cas contraire, contournement à usage unique de hello est uniquement valable pour 300 secondes. |
| Autoriser les utilisateurs tooselect (méthode) | Autoriser les utilisateurs toospecify leur méthode de contact principale. Cela peut être un appel téléphonique, un message texte, une application mobile ou un jeton OATH. |
| Autoriser les utilisateurs tooselect language | Autoriser les utilisateurs de langue hello toochange utilisée pour hello un appel téléphonique, message texte, application mobile ou jeton OATH. |
| Autoriser l’application mobile de tooactivate utilisateurs | Autoriser les utilisateurs toogenerate un processus d’activation code toocomplete hello application mobile d’activation qui est utilisé avec le serveur de hello.  Vous pouvez également définir le nombre de hello d’appareils qu’ils peuvent activer application hello sur, entre 1 et 10. |
| Utiliser les questions de sécurité de secours | Autorise les questions de sécurité en cas d’échec de la vérification en deux étapes. Vous pouvez spécifier le nombre de hello de questions de sécurité qui doit être répondu correctement. |
| Autoriser le jeton OATH d’utilisateurs tooassociate tiers | Autoriser les utilisateurs toospecify jeton OATH tiers. |
| Utiliser le jeton OATH de secours | Autoriser pour l’utilisation de hello d’un jeton OATH au cas où vérification en deux étapes ne réussit pas. Vous pouvez également spécifier le délai d’expiration de session hello en minutes. |
| Activation de la journalisation | Activer la journalisation sur le portail de l’utilisateur hello. Hello des fichiers journaux sont trouvent dans : C:\Program Files\Multi-Factor Authentication Server\Logs. |

Ces paramètres deviennent utilisateur toohello visible dans le portail de hello une fois qu’ils sont activés et qu’ils sont signés dans le portail de l’utilisateur toohello.

![Paramètres du portail de l'utilisateur](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Inscription utilisateur libre-service

Si vous souhaitez que votre toosign d’utilisateurs et inscrivez, vous devez sélectionner hello **autoriser toolog utilisateurs dans** et **autoriser l’inscription utilisateur** options sous l’onglet Paramètres de hello. N’oubliez pas que les paramètres de hello que vous sélectionnez affectent expérience d’authentification de l’utilisateur du hello.

Par exemple, lorsqu’un utilisateur se connecte dans le portail de l’utilisateur pour hello toohello première fois, ils sont ensuite dirigés page du programme d’installation de Azure multi-Factor d’authentification utilisateur toohello. Selon la façon dont vous avez configuré l’authentification multifacteur Azure, hello. l’utilisateur peut être en mesure de tooselect leur méthode d’authentification.

S’ils sélectionner la méthode de vérification hello appel vocal ou ont été préconfiguré toouse cette méthode, page de hello invite hello utilisateur tooenter leur numéro de téléphone principal et l’extension, le cas échéant. Ils peuvent également être autorisé à tooenter un numéro de téléphone de secours.

![Inscrire des numéros de téléphone principal et de sauvegarde](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Si l’utilisateur de hello est requis toouse un code confidentiel pour s’authentifier, hello page vous invite à les toocreate un code confidentiel. Après avoir entré ses numéros de téléphone et un code confidentiel (le cas échéant), utilisateur de hello clique hello **tooAuthenticate appeler maintenant** bouton. L’authentification multifacteur Azure effectue le numéro de téléphone principal d’un appel téléphonique vérification toohello l’utilisateur. utilisateur de Hello doit répondre à un appel téléphonique hello et entrer son code confidentiel (le cas échéant) et appuyez sur # toomove sur toohello d’étape suivante du processus d’auto-inscription hello.

Si l’utilisateur de hello sélectionne la méthode de vérification de Message texte hello ou a été préconfigurée toouse cette méthode, page de hello invite utilisateur hello pour leur numéro de téléphone mobile. Si l’utilisateur de hello est requis toouse un code confidentiel pour s’authentifier, hello page également vous invite à les tooenter un code confidentiel.  Après avoir entré son numéro de téléphone et un code confidentiel (le cas échéant), utilisateur de hello clique hello **tooAuthenticate texte me maintenant** bouton. Azure multi-Factor Authentication effectue un téléphone mobile SMS vérification toohello d’un utilisateur. utilisateur de Hello reçoit hello SMS avec un unique-time-code secret (OTP), puis message toohello de réponses avec ce code ainsi que leur code confidentiel (le cas échéant).

![SMS du portail de l'utilisateur](./media/multi-factor-authentication-get-started-portal/text.png)

Si l’utilisateur de hello sélectionne la méthode de vérification de l’application Mobile hello, page de hello invite application hello utilisateur tooinstall hello Microsoft Authenticator sur leur appareil et générer un code d’activation. Après avoir installé l’application hello, utilisateur de hello clique sur bouton Générer le Code d’Activation de hello.

> [!NOTE]
> application de Microsoft Authenticator toouse hello, utilisateur de hello doit activer les notifications push pour leur appareil.

page de Hello affiche un code d’activation et une URL avec une image de code-barres. Si l’utilisateur de hello est requis toouse un code confidentiel pour s’authentifier, hello page en outre vous invite à les tooenter un code confidentiel. utilisateur de Hello passe code d’activation de hello et l’URL dans l’application de Microsoft Authenticator hello ou utilise l’image de code-barres du scanneur tooscan hello hello code-barres et clique sur le bouton Activer de hello.

Après l’activation de hello est terminée, les utilisateurs hello clique sur hello **m’authentifier maintenant** bouton. Azure multi-Factor Authentication effectue l’application mobile de l’utilisateur toohello vérification. utilisateur de Hello doit entrer son code confidentiel (le cas échéant) et appuyez sur bouton authentifier de hello dans leur toomove application mobile toohello d’étape suivante du processus d’auto-inscription hello.

Si les administrateurs de hello ont configuré des réponses et questions de sécurité toocollect hello serveur Azure multi-Factor Authentication, hello utilisateur est ensuite dirigé page de Questions de sécurité toohello. utilisateur de Hello doit sélectionner quatre questions de sécurité et fournir des réponses aux questions de tootheir sélectionné.

![Questions de sécurité du portail de l'utilisateur](./media/multi-factor-authentication-get-started-portal/secq.png)

l’inscription automatique Hello utilisateur est maintenant terminée et hello utilisateur s’est connecté dans le portail de l’utilisateur toohello. Utilisateurs peuvent se connecter au portail de l’utilisateur toohello à tout moment dans toochange de futures hello leurs numéros de téléphone, les codes confidentiels, les méthodes d’authentification et les questions de sécurité si la modification de leurs méthodes est autorisée par les administrateurs.

## <a name="next-steps"></a>Étapes suivantes

- [Déployer hello Service Web d’application Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md)
