---
title: aaaMFA Server avec AD FS dans Windows Server | Documents Microsoft
description: "Cet article décrit comment tooget main d’Azure multi-Factor Authentication et AD FS dans Windows Server 2012 R2 et 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Configurer le serveur Azure multi-Factor Authentication toowork avec AD FS dans Windows Server
Si vous utilisez les Services de fédération Active Directory (AD FS) et que vous souhaitez toosecure les ressources cloud ou localement, vous pouvez configurer le serveur Azure multi-Factor Authentication toowork avec AD FS. Cette configuration active la vérification en deux étapes pour les points de terminaison de valeur élevée.

Cet article traite de l’utilisation du serveur Azure Multi-Factor Authentication avec AD FS dans Windows Server 2012 R2 ou Windows Server 2016. Pour plus d’informations, consultez les instructions trop[sécuriser les ressources de cloud et locales à l’aide du serveur Azure multi-Factor Authentication avec AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Sécuriser Windows Server AD FS avec le serveur Azure Multi-Factor Authentication
Lorsque vous installez le serveur Azure multi-Factor Authentication, vous avez hello options suivantes :

* Installer le serveur Azure multi-Factor Authentication localement sur hello même serveur que les services AD FS
* Installer localement de carte de l’authentification multifacteur Azure hello sur hello serveur AD FS, puis installez le serveur multi-Factor Authentication sur un autre ordinateur

Avant de commencer, vous devez être conscient des hello informations suivantes :

* Vous n’êtes pas requis tooinstall serveur Azure multi-Factor Authentication sur votre serveur AD FS. Toutefois, vous devez installer l’adaptateur multi-Factor Authentication hello pour AD FS sur Windows Server 2016 qui est en cours d’exécution AD FS de Windows Server 2012 R2. S’il s’agit d’une version prise en charge et que vous installez hello adaptateur AD FS séparément sur votre serveur de fédération AD FS, vous pouvez installer le serveur de hello sur un autre ordinateur. Consultez hello suivant les procédures toolearn comment tooinstall hello carte séparément.
* Si votre organisation utilise un message texte ou les méthodes de vérification des applications mobiles, les chaînes de hello définis dans les paramètres de la société contiennent un espace réservé, <$*application_name*$>. Dans le serveur MFA v7.1, vous pouvez fournir un nom d’application qui remplace cet espace réservé. 7.0 ou antérieure, cet espace réservé est remplacé pas automatiquement lorsque vous utilisez l’adaptateur hello AD FS. Pour les versions antérieures, supprimez hello espace réservé sur les chaînes appropriées hello lorsque vous sécurisez AD FS.
* compte de Hello que vous utilisez toosign dans doit avoir des groupes de sécurité utilisateur droits toocreate dans votre service Active Directory.
* Assistant installation de l’adaptateur Hello l’authentification multifacteur AD FS crée un groupe de sécurité appelé PhoneFactor Admins dans votre instance d’Active Directory. Il ajoute ensuite le compte de service hello AD FS de votre groupe de toothis de service de fédération. Vérifier sur votre contrôleur de domaine que hello groupe PhoneFactor Admins est bien créé et que le compte de service hello AD FS est membre de ce groupe. Si nécessaire, ajoutez manuellement toohello de compte de service AD FS de hello groupe PhoneFactor Admins sur votre contrôleur de domaine.
* Pour plus d’informations sur l’installation hello SDK du Service Web avec le portail de l’utilisateur hello, en savoir plus sur [déploiement du portail de l’utilisateur hello pour le serveur Azure multi-Factor Authentication.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Installer le serveur Azure multi-Factor Authentication localement sur le serveur de hello AD FS
1. Téléchargez et installez le serveur Azure Multi-Factor Authentication sur votre serveur AD FS. Pour plus d’informations concernant l’installation, consultez l’article sur la [prise en main du serveur Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. Dans la console de gestion du serveur Azure multi-Factor Authentication hello, cliquez sur hello **AD FS** icône. Sélectionnez les options de hello **autoriser l’inscription utilisateur** et **permettent aux utilisateurs tooselect méthode**.
3. Sélectionnez les options supplémentaires que vous aimeriez toospecify pour votre organisation.
4. Cliquez sur **Installer adaptateur AD FS**.
   
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Si la fenêtre d’Active Directory hello est affichée, cela signifie que deux choses. Votre ordinateur est tooa joint à un domaine et configuration d’Active Directory hello pour sécuriser les communications entre l’adaptateur hello AD FS et le service d’authentification multifacteur hello est incomplète. Cliquez sur **suivant** tooautomatically terminer cette configuration, ou sélectionnez hello **ignorer la configuration automatique d’Active Directory et configurer les paramètres manuellement** case à cocher. Cliquez sur **Suivant**.
6. Si windows du groupe Local hello est affiché, cela signifie que deux choses. Votre ordinateur n’est pas tooa joint à un domaine, et la configuration du groupe local hello pour sécuriser les communications entre l’adaptateur hello AD FS et le service d’authentification multifacteur hello est incomplète. Cliquez sur **suivant** tooautomatically terminer cette configuration, ou sélectionnez hello **ignorer la configuration automatique du groupe Local et configurer les paramètres manuellement** case à cocher. Cliquez sur **Suivant**.
7. Dans l’Assistant installation de hello, cliquez sur **suivant**. Serveur Azure multi-Factor crée hello groupe PhoneFactor Admins et ajoute toohello de compte de service AD FS de hello groupe PhoneFactor Admins.
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. Sur hello **lancer le programme d’installation** , cliquez sur **suivant**.
9. Dans le programme d’installation de la carte hello l’authentification multifacteur AD FS, cliquez sur **suivant**.
10. Cliquez sur **fermer** lorsque hello installation terminée.
11. Lorsque l’adaptateur hello a été installé, vous devez l’inscrire avec AD FS. Ouvrez Windows PowerShell et exécutez hello de commande suivante :<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse votre adaptateur nouvellement inscrit, modifier la stratégie d’authentification globale hello dans AD FS. Dans la console de gestion hello AD FS, accédez toohello **des stratégies d’authentification** nœud. Bonjour **multi-Factor Authentication** , cliquez sur hello **modifier** lien suivant toohello **paramètres globaux** section. Bonjour **modifier la stratégie d’authentification globale** fenêtre, sélectionnez **multi-Factor Authentication** comme une méthode d’authentification supplémentaire, puis cliquez sur **OK**. adaptateur de Hello est enregistré en tant que WindowsAzureMultiFactorAuthentication. Redémarrer hello AD FS pour effet de tootake hello d’inscription.

<center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

À ce stade, serveur multi-Factor Authentication est configuré toobe un toouse de fournisseur d’authentification supplémentaires avec AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Installer une instance autonome de l’adaptateur hello AD FS à l’aide de hello SDK du Service Web
1. Installer hello SDK du Service Web sur serveur hello serveur multi-Factor Authentication est en cours d’exécution.
2. Suivant de hello copie les fichiers à partir de la hello \Program Files\Multi-facteur d’authentification Active toohello serveur sur lequel vous envisagez de l’adaptateur tooinstall hello AD FS :
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Exécutez le fichier d’installation MultiFactorAuthenticationAdfsAdapterSetup64.msi hello.
4. Dans le programme d’installation de la carte hello l’authentification multifacteur AD FS, cliquez sur **suivant** installation de hello toostart.
5. Cliquez sur **fermer** lorsque hello installation terminée.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Modifier le fichier MultiFactorAuthenticationAdfsAdapter.config de hello
Suivez ces fichiers de MultiFactorAuthenticationAdfsAdapter.config étapes tooedit hello :

1. Ensemble hello **UseWebServiceSdk** nœud trop**true**.  
2. La valeur hello pour **WebServiceSdkUrl** toohello des URL de hello Web Services SDK multi-Factor Authentication. Par exemple : *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, où *certificatename* est le nom hello de votre certificat.  
3. Modifiez le script de hello Register-multifactorauthenticationadfsadapter.ps1 en ajoutant *- ConfigurationFilePath &lt;chemin d’accès&gt;*  fin toohello Hello `Register-AdfsAuthenticationProvider` commande, où  *&lt;chemin d’accès&gt;*  est le fichier de MultiFactorAuthenticationAdfsAdapter.config toohello hello chemin d’accès complet.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Configurer hello SDK du Service Web avec un nom d’utilisateur et un mot de passe
Il existe deux options de configuration hello SDK du Service Web. Hello est tout d’abord avec un nom d’utilisateur et un mot de passe, hello est ensuite avec un certificat client. Suivez ces étapes pour la première option de hello, ou passez hello directement ensuite.  

1. La valeur hello pour **WebServiceSdkUsername** tooan compte qui est membre du groupe de sécurité PhoneFactor Admins de hello. Hello d’utilisation &lt;domaine&gt;&#92;&lt; nom d’utilisateur&gt; format.  
2. La valeur hello pour **WebServiceSdkPassword** toohello mot de passe approprié.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Configurer hello SDK du Service Web avec un certificat client
Si vous ne souhaitez pas toouse un nom d’utilisateur et un mot de passe, suivez ces hello de tooconfigure étapes SDK du Service Web avec un certificat client.

1. Obtenir un certificat client à partir d’une autorité de certification pour le serveur hello hello SDK du Service Web est en cours d’exécution. Découvrez comment trop[obtenir des certificats clients](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importation hello toohello ordinateur local certificat personnel magasin de certificats client sur le serveur hello hello SDK du Service Web est en cours d’exécution. Assurez-vous que le certificat public de ce hello l’autorité de certification est dans le magasin de certificats des certificats racines approuvés.  
3. Exporter les clés publiques et privées de hello hello client tooa .pfx du fichier de certificat.  
4. Exporter la clé publique de hello dans fichier .cer tooa au format Base64.  
5. Dans le Gestionnaire de serveur, vérifiez que cette fonctionnalité de l’authentification du mappage de certificat Client \Web Server\Security\IIS hello serveur Web (IIS) est installée. S’il n’est pas installé, sélectionnez **Ajout de rôles et fonctionnalités** tooadd cette fonctionnalité.  
6. Dans le Gestionnaire des services Internet, double-cliquez sur **l’éditeur de Configuration** dans le site Web hello qui contient le répertoire virtuel du SDK du Service Web hello. Il est important tooselect site Web de hello, pas les répertoire virtuel hello.  
7. Accédez toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** section.  
8. Définissez enabled trop**true**.  
9. Définissez oneToOneCertificateMappingsEnabled trop**true**.  
10. Cliquez sur hello **...**  bouton toooneToOneMappings suivant, puis cliquez sur hello **ajouter** lien.  
11. Ouvrez hello Base64 .cer fichier que précédemment exporté. Supprimez *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----*, ainsi que tous les sauts de ligne. Copiez la chaîne résultante de hello.  
12. Jeu de certificats toohello chaîne copié hello précédant l’étape.  
13. Définissez enabled trop**true**.  
14. Définir le nom d’utilisateur tooan compte qui est membre du groupe de sécurité PhoneFactor Admins de hello. Hello d’utilisation &lt;domaine&gt;&#92;&lt; nom d’utilisateur&gt; format.  
15. Mot de passe hello mot de passe toohello compte approprié et puis fermez l’éditeur de Configuration.  
16. Cliquez sur hello **appliquer** lien.  
17. Dans le répertoire virtuel SDK du Service Web de hello, double-cliquez sur **authentification**.  
18. Vérifiez que l’emprunt d’identité ASP.NET et l’authentification de base sont trop**activé**, et que tous les autres éléments sont trop**désactivé**.  
19. Dans le répertoire virtuel SDK du Service Web de hello, double-cliquez sur **paramètres SSL**.  
20. Définissez les certificats clients trop**accepter**, puis cliquez sur **appliquer**.  
21. Copier le fichier .pfx de hello vous exportées server toohello antérieures qui est en cours d’exécution hello adaptateur AD FS.  
22. Importez le magasin de certificats personnel hello .pfx fichier toohello ordinateur local.  
23. Avec le bouton droit et sélectionnez **gérer les clés privées**, puis accorder un accès en lecture toohello compte et vous avez utilisé toosign dans le service toohello AD FS.  
24. Ouvrez hello client certificat et copie hello l’empreinte numérique à partir de hello **détails** onglet.  
25. Dans le fichier MultiFactorAuthenticationAdfsAdapter.config de hello, définissez **WebServiceSdkCertificateThumbprint** toohello chaîne copiée à l’étape précédente de hello.  

Enfin, tooregister hello l’adaptateur, exécutez hello \Program Files\Multi-script Factor Authentication Server\Register-multifactorauthenticationadfsadapter.ps1 dans PowerShell. adaptateur de Hello est enregistré en tant que WindowsAzureMultiFactorAuthentication. Redémarrer hello AD FS pour effet de tootake hello d’inscription.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Sécurisation des ressources Azure AD à l’aide d’AD FS
toosecure vos ressources de cloud, configurez une règle de revendication afin que les Services de fédération Active Directory émet hello multipleauthn revendication lorsqu’un utilisateur effectue une vérification en deux étapes avec succès. Cette revendication est passée sur tooAzure AD. Suivez cette toowalk procédure étapes hello :

1. Ouvrez Gestion AD FS.
2. Sur hello gauche, sélectionnez **confiance**.
3. Cliquez avec le bouton droit sur **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication…**

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **passer ou filtrer une revendication entrante** dans hello de liste déroulante, puis cliquez sur **suivant**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nommez votre règle.
7. Sélectionnez **références des méthodes d’authentification** comme hello entrants le type de revendication.
8. Sélectionnez **Transférer toutes les valeurs de revendication**.
    ![Assistant Ajouter une règle de revendication de transformation](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Cliquez sur **Terminer**. Fermez la console de gestion ADFS hello AD.

## <a name="related-topics"></a>Rubriques connexes
Pour la résolution des problèmes, consultez hello [FAQ de l’authentification multifacteur Azure](multi-factor-authentication-faq.md)
