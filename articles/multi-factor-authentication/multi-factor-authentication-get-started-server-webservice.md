---
title: "aaaAzure Service Web d’application Mobile MFA Server | Documents Microsoft"
description: "Hello Microsoft Authenticator application offre la possibilité d’authentification hors-bande supplémentaires.  Il permet de hello toousers de notifications push MFA server toouse."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Activation de l'authentification par application mobile avec le serveur Azure Multi-Factor Authentication

application de Microsoft Authenticator Hello offre une option de vérification out-of-band supplémentaire. Au lieu de passer un appel téléphonique automatisé ou un utilisateur SMS toohello lors de la connexion, l’authentification multifacteur Azure exécute un push d’une application de Microsoft Authenticator toohello notification sur tablette ou smartphone de l’utilisateur hello. Hello utilisateur appuie simplement sur **Vérifiez** (ou entre un code PIN et appuie sur « Authentifier ») dans hello application toocomplete leurs connectez-vous.

Il est préférable d’utiliser une application mobile pour la vérification en deux étapes si la réception par téléphone n’est pas fiable. Si vous utilisez application hello comme un générateur de jetons OATH, il ne nécessite pas une connexion réseau ou internet.

Selon votre environnement, vous souhaiterez toodeploy hello mobile web du service d’applications sur hello même serveur comme serveur Azure multi-Factor Authentication ou sur un autre serveur connecté à internet.

## <a name="requirements"></a>Configuration requise

application de Microsoft Authenticator toouse hello, hello Voici requis afin que hello application puisse communiquer avec le Service Web d’application Mobile :

* Azure Multi-Factor Authentication Server 6.0 ou version ultérieure
* Installez le service Web de l’application mobile sur un serveur Web sur Internet exécutant Microsoft® [Internet Information Services (IIS) 7.x ou version ultérieure](http://www.iis.net/)
* ASP.NET v4.0.30319 est installé, inscrit et définir tooAllowed
* Les services de rôle requis incluent ASP.NET et une compatibilité avec la métabase IIS 6.
* Le service Web de l’application mobile est accessible via une URL publique
* Le service Web de l’application mobile est sécurisé avec un certificat SSL.
* Installer le SDK Service Web Azure multi-Factor Authentication de hello dans IIS 7.x ou une version ultérieure sur hello **même serveur que hello serveur Azure multi-Factor Authentication**
* Hello le SDK Service Web Azure multi-Factor Authentication est sécurisée avec un certificat SSL.
* Service Web d’application mobile peut se connecter à toohello le SDK Service Web Azure multi-Factor Authentication via SSL
* Service Web d’application mobile peut s’authentifier toohello Web Services SDK Azure MFA à l’aide des informations d’identification hello d’un compte de service qui est membre du groupe de sécurité « Administrateurs PhoneFactor » hello. Ce compte de service et ce groupe existent dans Active Directory si hello serveur Azure multi-Factor Authentication se trouve sur un serveur appartenant à un domaine. Ce compte de service et ce groupe existent localement sur hello serveur Azure multi-Factor Authentication s’il n’est pas tooa joint à un domaine.

## <a name="install-hello-mobile-app-web-service"></a>Installer hello application mobile web service

Avant d’installer le service web d’application mobile hello, soyez conscient des hello les détails suivants :

* Il vous faut un compte de service faisant partie du groupe « PhoneFactor Admins ». Ce compte peut être identique à un hello utilisé pour l’installation du portail de l’utilisateur hello de hello.
* Il est utile tooopen un navigateur web sur le serveur de web hello Internet et accédez URL toohello Hello SDK Service Web qui a été entrée dans le fichier web.config de hello. Si le navigateur de hello accéder avec succès à un service web de toohello, il vous invite à entrer des informations d’identification. Entrez le nom d’utilisateur hello et un mot de passe qui ont été entrés dans le fichier web.config de hello exactement comme il apparaît dans le fichier de hello. Assurez-vous qu'aucun avertissement ou erreur de certificat ne soit affiché.
* Si un pare-feu ou un proxy inverse est placé devant le serveur web de Service Web d’application Mobile hello et effectue un déchargement SSL, vous pouvez modifier fichier web.config de Service Web d’application Mobile hello afin que hello Service Web d’application Mobile puisse utiliser http au lieu de https. SSL est toujours requis depuis l’application Mobile toohello pare-feu/proxy inverse de hello. Ajouter hello suivant clé toohello \<appSettings\> section :

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Installer le service web de hello SDK

Dans les deux cas, si hello le SDK Service Web Azure multi-Factor Authentication est **pas** déjà installé sur le serveur Azure multi-Factor Authentication (MFA) de hello, hello terminé les étapes qui suivent.

1. Ouvrez la console du serveur multi-Factor hello.
2. Accédez toohello **SDK du Service Web** et sélectionnez **installer le SDK du Service Web**.
3. Installation hello complète à l’aide des valeurs par défaut hello, sauf si vous avez besoin de toochange pour une raison quelconque.
4. Lier à un site toohello de certificat SSL dans IIS.

Si vous avez des questions sur la configuration d’un certificat SSL sur un serveur IIS, voir l’article hello [comment tooSet configuration de SSL sur IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hello SDK du Service Web doit être sécurisé avec un certificat SSL. Un certificat auto-signé peut être ajouté à cet effet. Importer le certificat de hello dans le magasin de « Trusted Root Certification Authorities » hello hello Local du compte d’ordinateur sur le serveur web du portail utilisateur hello afin qu’il approuve ce certificat lors de l’ouverture de connexion SSL de hello.

![Kit de développement logiciel (SDK) du Service Web d’installation du serveur MFA](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Installer le service de hello

1. **Sur le serveur MFA de hello**, parcourir le chemin d’installation de toohello.
2. Accédez toohello dossier où hello serveur Azure MFA est par défaut de hello installée est **C:\Program Files\Azure multi-Factor Authentication**.
3. Recherchez le fichier d’installation hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Si le serveur hello est **pas** connecté à Internet, copie hello installation fichier toohello sur Internet le serveur.
4. Si hello serveur MFA est **pas** côté internet commutateur toohello **serveur Internet**.
5. Exécutez hello **MultiFactorAuthenticationMobileAppWebServiceSetup64** installer un fichier en tant qu’administrateur, de modifier hello Site si vous le souhaitez et de modifier le nom court du tooa répertoire virtuel hello si vous souhaitez.
6. Après l’installation en terminant hello, parcourir trop**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (ou le répertoire approprié basé sur le nom du répertoire virtuel hello) et de modifier le fichier Web.Config de hello.

   * Trouver la clé de hello **« WEB_SERVICE_SDK_AUTHENTICATION_USERNAME »** et modifiez **valeur = « «** trop**valeur = « Domaine\utilisateur »** où domaine\nom d’utilisateur est un compte de Service qui fait partie de Groupe de « PhoneFactor Admins ».
   * Trouver la clé de hello **« WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD »** et modifiez **valeur = « «** trop**valeur = « Password »** où le mot de passe est un mot de passe hello pour hello Service Compte entré dans la ligne précédente de hello.
   * Recherche hello **paramètre pfMobile App Web Service_pfwssdk_PfWsSdk** définir et modifier la valeur hello à partir de **http://localhost:4898/PfWsSdk.asmx** toohello URL du SDK du Service Web (exemple : https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Enregistrez le fichier Web.Config de hello et fermez le bloc-notes.

   > [!NOTE]
   > SSL est utilisé pour cette connexion, vous devez référencer hello Web Services SDK par **le nom de domaine complet (FQDN)** et **pas l’adresse IP**. Hello certificat SSL aurait été émis pour le nom de domaine complet de hello et hello URL utilisée doit correspondre au nom hello sur le certificat de hello.

7. Si le site Web hello que Service Web d’application Mobile a été installé sous n’a pas déjà été lié avec un certificat signé publiquement, installer le certificat de hello sur le serveur de hello, ouvrez le Gestionnaire des services Internet et lier le site Web de hello certificat toohello.
8. Ouvrez un navigateur web à partir de n’importe quel ordinateur et accédez URL toohello où le Service Web d’application Mobile a été installé (exemple : https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Assurez-vous qu'aucun avertissement ou erreur de certificat ne soit affiché.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurer les paramètres des applications mobiles hello dans hello serveur Azure multi-Factor Authentication

Maintenant que hello application mobile web service est installé, vous devez tooconfigure hello serveur Azure multi-Factor Authentication toowork avec le portail de hello.

1. Dans la console du serveur multi-Factor hello, cliquez sur l’icône portail utilisateur hello. Vérification de leurs méthodes d’authentification, si les utilisateurs sont autorisés à toocontrol **l’application Mobile** sur l’onglet Paramètres de hello, sous **permettent aux utilisateurs tooselect méthode**. Sans cette fonctionnalité est activée, les utilisateurs finaux sont toocontact obligatoire l’activation de toocomplete du support technique pour hello l’application Mobile.
2. Vérifiez hello **autoriser les utilisateurs tooactivate l’application Mobile** boîte.
3. Vérifiez hello **autoriser l’inscription utilisateur** boîte.
4. Cliquez sur hello **l’application Mobile** icône.
5. Entrez les URL de hello qui est utilisée avec le répertoire virtuel hello qui a été créé lors de l’installation MultiFactorAuthenticationMobileAppWebServiceSetup64 (exemple : https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) dans le champ de hello  **URL du Service Web de l’application mobile :**.
6. Remplir hello **nom de compte** champ hello entreprise ou organisation toodisplay de nom de l’application mobile hello pour ce compte.
   ![Configuration du serveur MFA et paramètres de l’application mobile](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Étapes suivantes

- [Scénarios avancés avec Azure Multi-Factor Authentication et des VPN tiers](multi-factor-authentication-advanced-vpn-configurations.md).