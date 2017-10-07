---
title: "aaaAzure Forum aux questions de l’authentification multifacteur | Documents Microsoft"
description: "Forum aux questions et réponses associées tooAzure multi-Factor Authentication. Multi-Factor Authentication est une méthode permettant de vérifier l’identité d’un utilisateur qui requiert d’autres méthodes que le nom d’utilisateur et le mot de passe. Il fournit une couche supplémentaire de sécurité toouser connectez-vous et transactions."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Questions fréquentes relatives à Azure Multi-Factor Authentication
Ce forum aux questions répond aux questions courantes sur Azure multi-Factor Authentication et à l’aide du service d’authentification multifacteur hello. Il est divisé en questions sur le service de hello en général, les modèles, des expériences utilisateur, de facturation et de dépannage.

## <a name="general"></a>Généralités
**Q : Comment les données utilisateur sont-elles gérées par le serveur Azure Multi-Factor Authentication ?**

Avec le serveur de l’authentification multifacteur, les données utilisateur sont stockées sur les serveurs locaux hello. Aucune donnée utilisateur persistante n’est stockée dans le cloud de hello. Lorsque l’utilisateur de hello effectue la vérification en deux étapes, serveur multi-Factor Authentication envoie des données toohello service de cloud d’Azure multi-Factor Authentication pour l’authentification. Communication entre serveur multi-Factor Authentication et hello service de cloud de l’authentification multifacteur utilise Secure Sockets Layer (SSL) ou la sécurité TLS (Transport Layer) sur le port 443 sortant.

Lorsque les demandes d’authentification sont envoyées toohello le service cloud, les données sont collectées pour l’authentification et l’utilisation des rapports. Les champs de données inclus dans les journaux de vérification en deux étapes sont les suivants :

* **ID unique** (soit le nom d’utilisateur soit l’ID de serveur Multi-Factor Authentication local)
* **Prénom et nom** (facultatif)
* **Adresse de messagerie** (facultatif)
* **Numéro de téléphone** (en cas d’utilisation de l’authentification par appel vocal ou SMS)
* **Jeton de l’appareil** (en cas d’utilisation de l’authentification par application mobile)
* **Mode d'authentification**
* **Résultat de l'authentification**
* **Nom du serveur Multi-Factor Authentication**
* **Adresse IP du serveur Multi-Factor Authentication**
* **Adresse IP du client** (si disponible)

les champs facultatifs Hello peuvent être configurés dans le serveur multi-Factor Authentication.

résultat (succès ou refus) de la vérification de Hello et hello raison si elle a été refusée, est stockée avec les données d’authentification hello. Celles-ci sont disponibles dans les rapports d’utilisation et d’authentification.

## <a name="billing"></a>Facturation
La plupart des questions sur la facturation peuvent répondre en vous reportant tooeither hello [page de tarification de l’authentification multifacteur](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) ou documentation hello sur [comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**Q : est-il mon organisation facturée pour l’envoi des appels hello et les messages de texte qui sont utilisés pour l’authentification ?**

Non, vous n’êtes pas facturé pour les appels téléphoniques ou messages texte envoyés toousers via l’authentification multifacteur Azure. Si vous utilisez un fournisseur d’authentification Multifacteur par authentification, vous êtes facturé pour chaque authentification mais pas pour la méthode hello utilisée.

Vos utilisateurs peuvent facturés pour les appels hello ou des messages qu’ils reçoivent, service de téléphone personnel tootheir correspondants.

**Q : modèle de facturation par utilisateur hello facture-t-il me utilisateurs toutes activées ou hello seulement ceux qui a effectué la vérification en deux étapes ?**

Facturation est basée sur le nombre de hello d’utilisateurs configurés toouse l’authentification multifacteur, indépendamment de si elles effectuée le vérification en deux étapes ce mois.

**Q : Comment fonctionne la facturation Multi-Factor Authentication ?**

Lorsque vous créez un fournisseur MFA par utilisateur ou par authentification, l’abonnement Azure de votre organisation est facturé chaque mois en fonction de l’utilisation. Ce modèle de facturation est similaire toohow Azure facture pour l’utilisation d’ordinateurs virtuels et des sites Web.

Lorsque vous achetez un abonnement Azure multi-Factor Authentication, votre organisation paie uniquement des frais de licence annuelle hello pour chaque utilisateur. Les licences MFA et Office 365, Azure AD Premium ou les offres groupées Enterprise Mobility + Security sont facturés de cette manière. 

En savoir plus sur les options disponibles [comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**Q : Existe-t-il une version gratuite d’Azure Multi-Factor Authentication ?**

Dans certains cas, oui.

L’authentification multifacteur pour les administrateurs Azure offre un sous-ensemble des fonctionnalités de l’authentification Multifacteur Azure sans frais pour l’accès tooMicrosoft des services en ligne, y compris les portails d’administrateur Azure et Office 365 hello. Cette offre s’applique uniquement à des administrateurs de tooglobal dans des instances Azure Active Directory n’ayant pas de version de hello complète de l’authentification Multifacteur Azure via une licence de l’authentification Multifacteur, un groupe ou un fournisseur basée sur la consommation d’autonome. Si vos administrateurs utilisent la version gratuite de hello et que vous achetez une version complète de l’authentification Multifacteur Azure, tous les administrateurs globaux sont élevé toohello payé version automatiquement.

L’authentification multifacteur pour les utilisateurs Office 365 offre un sous-ensemble des fonctionnalités de l’authentification Multifacteur Azure sans frais pour l’accès tooOffice 365 services, y compris Exchange Online et SharePoint Online. Cette offre s’applique toousers qui disposent d’une licence Office 365 affectée, lors de la version de hello complète de l’authentification Multifacteur Azure via une licence de l’authentification Multifacteur, un groupe ou un fournisseur basée sur la consommation d’autonome dépourvu d’instance correspondante de hello d’Azure Active Directory.

**Q : Mon organisation peut-elle passer de la facturation de la consommation par utilisateur à la facturation par authentification, et inversement, à tout instant ?**

Si votre organisation acquiert MFA en tant que service autonome avec une facturation à la consommation, vous choisissez un modèle de facturation lorsque vous créez un fournisseur MFA. Vous ne pouvez pas modifier le modèle de facturation hello après avoir créé un fournisseur d’authentification Multifacteur. Toutefois, vous pouvez supprimer le fournisseur d’authentification Multifacteur hello et ensuite créer une avec un autre modèle de facturation.

Lorsqu’un fournisseur d’authentification Multifacteur est créé, il peut être lié tooan Azure Active Directory (également appelé « locataire Azure AD »). Si hello fournisseur actuel de l’authentification Multifacteur est lié tooan Azure AD client, vous pouvez en toute sécurité supprimer le fournisseur d’authentification Multifacteur hello et créez-en un qui est lié toohello AD Azure même client. Si vous avez acheté suffisamment l’authentification Multifacteur, du Azure AD Premium, ou de l’entrepôt Enterprise Mobility + Security (EMS) licences toocover tous les utilisateurs qui sont activés pour l’authentification Multifacteur, vous pouvez également supprimer fournisseur d’authentification Multifacteur hello complètement.

Si votre fournisseur d’authentification Multifacteur est *pas* tooan lié Azure AD client, ou vous liez locataire tooa AD Azure autre fournisseur MFA hello, de paramètres utilisateur et les options de configuration ne sont pas transférées. En outre, les serveurs de l’authentification Multifacteur Azure existants doive toobe réactivé à l’aide des informations d’identification d’activation générées par le biais hello nouveau fournisseur d’authentification Multifacteur. Réactivation hello serveurs MFA toolink les toohello nouveau fournisseur d’authentification Multifacteur n’affecte pas l’appel téléphonique et l’authentification des messages texte, mais les applications mobiles notifications cessera de fonctionner pour tous les utilisateurs jusqu'à ce qu’ils réactiver l’application mobile hello.

Pour plus d’informations sur les fournisseurs MFA, consultez [Prise en main du fournisseur Azure Multi-Factor Auth](multi-factor-authentication-get-started-auth-provider.md).

**Q : Mon organisation peut-elle passer du modèle de facturation à la consommation aux abonnements (modèle basé sur licence) à tout instant ?**

Dans certains cas, oui.

Vous pouvez ajouter des licences MFA, si votre répertoire comporte un fournisseur Azure Multi-Factor Authentication *par utilisateur*. Les utilisateurs dont les licences ne sont pas comptés dans la facturation par utilisateur basée sur la consommation hello. Les utilisateurs sans licences peuvent toujours être activées pour l’authentification Multifacteur via le fournisseur d’authentification Multifacteur hello. Si vous achetez et affectez des licences pour tous vos utilisateurs configuré toouse multi-Factor Authentication, vous pouvez supprimer le fournisseur de l’authentification multifacteur Azure hello. Vous pouvez toujours créer un autre fournisseur d’authentification Multifacteur par utilisateur si vous avez plus d’utilisateurs que les licences Bonjour futures.

Si votre annuaire comporte un *par authentification* fournisseur Azure multi-Factor Authentication, vous êtes toujours facturé pour chaque authentification, tant que fournisseur d’authentification Multifacteur hello est lié tooyour abonnement. Vous pouvez affecter l’authentification Multifacteur licences toousers, mais vous serez toujours facturé pour chaque demande de vérification en deux étapes, si elle provient d’une personne avec une licence de l’authentification Multifacteur ou non.

**Q : mon organisation ont toouse et synchroniser les identités toouse Azure multi-Factor Authentication ?**

Azure Active Directory est facultatif et n’est pas requis en cas d’utilisation des modèles de facturation basés sur la consommation par l’organisation. Si votre fournisseur d’authentification Multifacteur n’est pas lié tooan locataire Azure AD, vous pouvez uniquement déployer le serveur Azure multi-Factor Authentication ou hello SDK Azure multi-Factor Authentication localement.

Azure Active Directory est requis pour le modèle de licence hello, car les licences sont ajoutées locataire d’Azure AD toohello lorsque vous achetez et affectez toousers dans le répertoire de hello.

## <a name="manage-and-support-user-accounts"></a>Gérer et prendre en charge les comptes d’utilisateurs

**Q : que dois-je savoir mon toodo utilisateurs si elles n’acceptent pas une réponse sur leur téléphone ou que vous ne disposez pas leur téléphone avec eux ?**

Espérons que tous vos utilisateurs ont configuré plus d’une méthode de vérification. Indiquez-lui tootry vous reconnecter, mais sélectionnez une autre méthode de vérification sur la page de connexion hello.

Vous pouvez faire pointer votre toohello utilisateurs [guide de dépannage de l’utilisateur final](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**Q : que dois-je faire si un de mes utilisateurs ne peuvent pas obtenir tootheir compte ?**

Vous pouvez réinitialiser le compte d’utilisateur hello en les rendant toogo via le processus d’inscription de hello à nouveau. En savoir plus sur [la gestion des paramètres utilisateur et appareil avec Azure multi-Factor Authentication dans le cloud de hello](multi-factor-authentication-manage-users-and-devices.md).

**Q : Que dois-je faire si un de mes utilisateurs perd un téléphone utilisant des mots de passe d’applications ?**

tooprevent accès non autorisé, supprimez les mots de passe de tous les utilisateurs hello application. Une fois que l’utilisateur de hello a un appareil de rechange, ils peuvent recréer des mots de passe hello. En savoir plus sur [la gestion des paramètres utilisateur et appareil avec Azure multi-Factor Authentication dans le cloud de hello](multi-factor-authentication-manage-users-and-devices.md).

**Q : que se passe-t-il si un utilisateur ne peut pas se connecter dans les applications non-Web toonon ?**

Si votre organisation utilise toujours des clients hérités et vous [autorisé utilisation hello de mots de passe d’application](multi-factor-authentication-whats-next.md#app-passwords), puis les clients hérités toothese avec leur nom d’utilisateur et un mot de passe ne peut pas se connecter vos utilisateurs. Au lieu de cela, ils ont besoin trop[configurer des mots de passe d’application](./end-user/multi-factor-authentication-end-user-app-passwords.md). Vos utilisateurs doivent effacer (supprimer) leurs informations de connexion, redémarrez l’application hello, puis connectez-vous avec leur nom d’utilisateur et *mot de passe* au lieu de leur mot de passe standard.

Si votre organisation ne dispose pas des clients hérités, vous ne devez pas autoriser vos utilisateurs toocreate mots de passe d’application.

> [!NOTE]
> Authentification moderne pour les clients Office 2013
>
> Les mots de passe d’application sont nécessaires uniquement pour les applications ne prenant pas en charge l’authentification moderne. Clients Office 2013 prend en charge les protocoles d’authentification moderne, mais doivent toobe configuré. Les nouveaux clients Office prennent automatiquement en charge les protocoles d’authentification moderne. Pour plus d’informations, consultez hello [annonce de version préliminaire publique de l’authentification moderne Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**Q : Mes utilisateurs disent que parfois, ils ne reçoivent un message texte hello, ou ils répondent SMS bidirectionnel tootwo mais hello vérification expire.**

Livraison de messages texte et de réception de réponses dans SMS bidirectionnel n’est pas garanti, car il existe des facteurs incontrôlables susceptibles d’affecter la fiabilité de hello du service de hello. Ces facteurs incluent la puissance du signal hello, opérateur de téléphonie mobile hello et pays de destination hello.

Si vos utilisateurs ont souvent des problèmes liés à recevoir des messages texte de manière fiable, indiquez-lui toouse hello mobile application ou un appel téléphonique (méthode) à la place. application mobile Hello peut recevoir des notifications à la fois sur un réseau cellulaire et connexions Wi-Fi. En outre, application mobile hello peut générer des codes de vérification même lorsque l’appareil de hello n’a pas de signal. application de Microsoft Authenticator Hello est disponible pour [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), et [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Si vous devez utiliser des messages texte, nous vous recommandons d’utiliser des SMS unidirectionnels plutôt que bidirectionnels dans la mesure du possible. SMS à sens unique est plus fiable et il empêche les utilisateurs de subir des frais de SMS à partir de la réponse SMS tooa qui a été envoyé à partir d’un autre pays.

**Q : puis-je modifier durée hello que mes utilisateurs ont le code de vérification tooenter hello à partir d’un message texte avant l’expiration de système de hello ?**

Oui, dans certains cas. 

Pour les SMS à sens unique avec le serveur Azure MFA 7.0 ou version ultérieure, vous pouvez configurer délai d’attente hello paramètre en définissant une clé de Registre. Une fois hello service cloud MFA envoie un message de texte hello, code de vérification hello (ou code secret à usage unique) est retourné toohello serveur MFA. Hello serveur MFA stocke les code hello en mémoire pendant 300 secondes par défaut. Si l’utilisateur de hello n’entre pas code hello avant hello 300 secondes, leur authentification est refusée. Utilisez ces paramètre de procédure toochange hello par défaut délai :

1. Accédez à tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Créer une clé de Registre DWORD appelée **pfsvc_pendingSmsTimeoutSeconds** et définir des temps de hello en secondes que vous souhaitez les secrets à usage unique du toostore serveur Azure MFA hello.

>[!TIP] 
>Si vous avez plusieurs serveurs de l’authentification Multifacteur, uniquement les hello qui a traité la demande d’authentification d’origine hello sait code de vérification hello qui a été envoyé toohello utilisateur. Lorsque l’utilisateur de hello entre un code hello, hello toovalidate de demande d’authentification toohello il doit être envoyé même serveur. Si la validation du code hello est envoyée tooa un autre serveur, l’authentification de hello est refusée. 

Pour SMS bidirectionnel avec le serveur Azure MFA, vous pouvez configurer le paramètre de délai d’attente hello Bonjour portail de gestion de l’authentification Multifacteur. Si les utilisateurs ne répondent toohello SMS dans le délai d’attente défini hello, leur authentification est refusée. 

Impossible de configurer pour SMS à sens unique avec Azure MFA dans le cloud hello (y compris hello extension de serveur de stratégie réseau hello ou de l’adaptateur AD FS), paramètre de délai d’attente hello. Azure AD stocke le code de vérification hello de 180 secondes. 

**Q : Puis-je utiliser des jetons matériels avec le serveur Azure Multi-Factor Authentication ?**

Si vous utilisez le serveur Azure Multi-Factor Authentication, vous pouvez importer des jetons de mots de passe à usage unique et durée définie (TOTP) d’authentification ouverte tierce (OATH), puis les utiliser pour la vérification en deux étapes.

Vous pouvez utiliser des jetons ActiveIdentity qui sont des jetons OATH TOTP si vous placez une clé secrète hello dans un fichier CSV et que vous importez tooAzure serveur multi-Factor Authentication. Vous pouvez utiliser des jetons OATH avec Active Directory Federation Services (ADFS), l’authentification basée sur les formulaires d’Internet Information Server (IIS) et Authentication Dial-In Service RADIUS (Remote User) tant que système hello du client peut accepter l’entrée d’utilisateur de hello.

Vous pouvez importer des jetons OATH TOTP tiers avec hello suivant formats :  

- Conteneur portable de clé symétrique (PSKC)  
- CSV si hello contient un numéro de série, une clé secrète au format Base 32 et un intervalle de temps  

**Q : puis-je utiliser des Services Terminal Server de toosecure serveur Azure multi-Factor Authentication ?**

Oui, mais si vous utilisez Windows Server 2012 R2 ou une version ultérieure, vous pouvez le faire uniquement avec la Passerelle des services Bureau à distance (passerelle RD).

Modifications de sécurité dans Windows Server 2012 R2 modifié comment le serveur Azure multi-Factor Authentication se connecte de package de sécurité toohello autorité de sécurité locale (LSA) dans Windows Server 2012 et les versions antérieures. Pour les versions de Terminal Services sous Windows 2012 ou une version antérieure, vous pouvez [sécuriser une application avec l’authentification Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Si vous utilisez Windows Server 2012 R2, vous devez utiliser une passerelle RD.

**Q : J’ai configuré ID de l’appelant dans le serveur MFA, mais mes utilisateurs continuent de recevoir des appels Multi-Factor Authentication d’un appelant anonyme.**

Lorsque les appels de multi-Factor Authentication sont placés par réseau téléphonique public de hello, parfois, elles sont routées via un opérateur qui ne prend pas en charge les ID d’appelant. Pour cette raison, ID de l’appelant n’est pas garanti, même si hello système de multi-Factor Authentication envoie toujours.

**Q : Pourquoi mes utilisateurs soient invités à tooregister leurs informations de sécurité ?**
Il existe plusieurs raisons que les utilisateurs peuvent être demandées par invite tooregister leurs informations de sécurité :

- utilisateur de Hello a été activé pour l’authentification Multifacteur par leur administrateur dans Azure AD, mais n’a pas encore inscrits pour leur compte des informations de sécurité.
- utilisateur de Hello a été activée pour le mot de passe libre-service, réinitialiser dans Azure AD. informations de sécurité Hello va les aider à réinitialiser leur mot de passe Bonjour futures si jamais oubli.
- utilisateur de Hello a accédé à une application qui a un toorequire de stratégie d’accès conditionnel MFA et n’a pas enregistré précédemment pour l’authentification Multifacteur.
- Hello utilisateurs qui inscrivent un appareil avec Azure AD (y compris Azure AD Join) et votre organisation exige l’authentification Multifacteur pour l’inscription de périphérique, mais les utilisateurs hello n’ont pas été enregistrés pour l’authentification Multifacteur.
- utilisateur de Hello génère Windows Hello for Business dans Windows 10 (qui nécessite l’authentification Multifacteur) et n’a pas encore enregistré précédemment pour l’authentification Multifacteur.
- organisation de Hello a créé et activé une stratégie d’inscription de l’authentification Multifacteur qui a été appliqué toohello utilisateur.
- utilisateur de Hello précédemment inscrit pour l’authentification Multifacteur, mais avez choisi une méthode de vérification, un administrateur a désactivé depuis. Hello doivent donc passer par l’inscription de l’authentification Multifacteur à nouveau tooselect une nouvelle méthode de vérification par défaut.


## <a name="errors"></a>Errors
**Q : Que doit faire un utilisateur s’il voit un message d’erreur « La demande d’authentification ne concerne pas un compte activé » lorsqu’il utilise les notifications d’applications mobiles ?**

Indiquez-lui toofollow tooremove de cette procédure leur compte à partir de l’application mobile de hello, puis l’ajouter à nouveau :

1. Accédez trop[votre profil portail Azure](https://account.activedirectory.windowsazure.com/profile/) et connectez-vous avec votre compte professionnel.
2. Sélectionnez **Vérification de sécurité supplémentaire**.
3. Supprimer le compte hello à partir de l’application mobile hello.
4. Cliquez sur **configurer**, puis suivez hello instructions tooreconfigure hello application mobile.

**Q : que doivent faire les utilisateurs s’ils reçoivent un message d’erreur 0x800434D4L lors de la signature dans l’application de navigateur non tooa ?**

Erreur de Hello 0x800434D4L se produit lorsque vous essayez de toosign dans une application non-Web de tooa, installée sur un ordinateur local, ce qui ne fonctionne pas avec les comptes qui requièrent la vérification en deux étapes.

Une solution de contournement de cette erreur est toohave distincts des comptes d’utilisateurs pour liées et non administratives. Une version ultérieure, vous pouvez lier des boîtes aux lettres entre votre compte d’administrateur et un compte non administrateur afin que vous pouvez vous connecter tooOutlook à l’aide de votre compte non-administrateur. Pour plus d’informations sur cette solution, découvrez comment trop[donner un hello administrateur capacité tooopen et vue hello contenu d’un utilisateur](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Étapes suivantes
Si votre question n’est pas une réponse ici, veuillez laisser dans des commentaires hello bas hello de page de hello. Sinon, voici quelques options supplémentaires pour obtenir de l’aide :

* Hello de recherche [Base de connaissances Microsoft](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) pour les problèmes techniques toocommon de solutions.
* Rechercher et parcourir des questions techniques et les réponses à partir de la Communauté de hello ou demandez à votre propre question Bonjour [les forums Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Si vous êtes un client hérité de PhoneFactor et que vous avez des questions ou besoin d’aide pour réinitialiser un mot de passe, utilisez hello [mot de passe réinitialisé](mailto:phonefactorsupport@microsoft.com) lien tooopen un cas de prise en charge.
* Contactez un professionnel du support via le [Support du serveur Azure Multi-Factor Authentication (PhoneFactor)](https://support.microsoft.com/oas/default.aspx?prid=14947). Lorsque vous nous contactez, veillez à inclure autant d’informations que possible concernant votre problème. Vous pouvez fournir des informations incluent page hello où vous l’avez vu erreur de hello, code d’erreur spécifique hello, ID de session spécifique hello et hello des ID d’utilisateur hello qui a vu l’erreur de hello.
