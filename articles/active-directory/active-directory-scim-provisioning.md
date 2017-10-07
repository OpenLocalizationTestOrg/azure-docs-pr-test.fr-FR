---
title: "aaaUsing système pour la gestion d’identité entre domaines déployez automatiquement des utilisateurs et des groupes à partir d’Azure Active Directory tooapplications | Documents Microsoft"
description: "Azure Active Directory peuvent automatiquement approvisionner les utilisateurs et groupes tooany application ou identité banque qui est fronted par un service web avec l’interface hello défini dans la spécification du protocole SCIM de hello"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>À l’aide du système pour configurer les utilisateurs tooautomatically de gestion des identités entre domaines et les groupes à partir d’Azure Active Directory tooapplications

## <a name="overview"></a>Vue d'ensemble
Azure Active Directory (Azure AD) peuvent automatiquement approvisionner les utilisateurs et groupes tooany application ou identité banque qui est fronted par un service web avec l’interface hello défini dans hello [système pour inter-domaines Identity Management (SCIM) 2.0 spécification du protocole](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory peut envoyer des demandes toocreate, modifier ou supprimer des utilisateurs et groupes toohello web service affecté. service web de Hello peut traduire ces demandes en opérations sur le magasin d’identités cible hello. 

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. 



![][0]
*Figure 1 : Configuration de magasin d’identités Azure Active Directory tooan via un service web*

Cette fonctionnalité peut être utilisée conjointement avec la fonctionnalité de « apportez votre propre application » hello dans Azure AD tooenable l’authentification unique et de configuration pour les applications qui fournissent ou sont fronted par un service web SCIM automatique de l’utilisateur.

Il existe deux cas d’utilisation de SCIM dans Azure Active Directory :

* **Approvisionnement tooapplications utilisateurs et groupes qui prennent en charge SCIM** Applications qui prennent en charge SCIM 2.0 et utilisent des jetons de porteur OAuth pour l’authentification fonctionne avec Azure AD sans configuration.
* **Créer votre propre solution d’approvisionnement pour les applications qui prennent en charge d’autres la configuration basée sur les API** pour les applications non-SCIM, vous pouvez créer un tootranslate de point de terminaison SCIM entre le point de terminaison Azure AD SCIM hello et toute application prend en charge API hello pour la configuration de l’utilisateur. toohelp vous développez un point de terminaison SCIM, nous fournissons des bibliothèques du Common Language Infrastructure (CLI), ainsi que des exemples de code qui montrent comment toodo fournissent un point de terminaison SCIM et traduire les messages de SCIM.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Configuration des utilisateurs et groupes tooapplications qui prennent en charge SCIM
Azure AD peut être tooapplications d’utilisateurs et groupes de disposition affectée tooautomatically configuré qui implémentent un [système pour la gestion d’identité entre domaines 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) service web et d’accepter des jetons de porteur OAuth pour l’authentification . Dans la spécification de hello SCIM 2.0, applications doivent respecter ces conditions :

* Prend en charge la création d’utilisateurs ou des groupes, conformément à la section 3.3 de hello protocole SCIM.  
* Prend en charge la modification des utilisateurs ou des groupes avec des demandes de correctif logiciel conformément à la section 3.5.2 Hello protocole SCIM.  
* Prend en charge la récupération d’une ressource connue en fonction de la section 3.4.1 Hello protocole SCIM.  
* Prend en charge l’interrogation des utilisateurs ou des groupes, conformément à la section 3.4.2 Hello protocole SCIM.  Par défaut, les utilisateurs sont interrogés par externalId et les groupes sont interrogés par displayName.  
* Prend en charge l’interrogation d’utilisateur, par ID, par le gestionnaire conformément à la section 3.4.2 Hello protocole SCIM.  
* Prend en charge l’interrogation des groupes par ID et par membre conformément à la section 3.4.2 Hello protocole SCIM.  
* Accepte les jetons de porteur OAuth pour l’autorisation conformément à la section 2.1 du protocole SCIM de hello.

Vérifiez avec votre fournisseur d’application ou dans la documentation du fournisseur de votre application la conformité à ces exigences.

### <a name="getting-started"></a>Prise en main
Les applications qui prennent en charge le profil SCIM hello décrite dans cet article peuvent être connecté tooAzure Active Directory à l’aide de la fonctionnalité de hello « bibliothèque non application » dans la galerie d’applications hello Azure AD. Une fois connecté, Azure AD s’exécute un processus de synchronisation toutes les 20 minutes où elle interroge le point de terminaison de l’application hello SCIM pour utilisateurs et groupes et crée ou modifie les selon toohello détails de l’affectation.

**tooconnect une application qui prend en charge SCIM :**

1. Connectez-vous trop[hello Azure portal](https://portal.azure.com). 
2. Parcourir trop ** Azure Active Directory > Applications d’entreprise, puis sélectionnez **nouvelle application > tous les > application Non-gallery**.
3. Entrez un nom pour votre application, puis cliquez sur **ajouter** icône toocreate un objet application.
    
  ![][1]
  *Figure 2 : galerie d’applications Azure AD*
    
4. Dans l’écran hello résultant, sélectionnez hello **Provisioning** onglet dans la colonne de gauche hello.
5. Bonjour **Mode d’approvisionnement** menu, sélectionnez **automatique**.
    
  ![][2]
  *Figure 3 : Configuration de l’approvisionnement Bonjour portail Azure*
    
6. Bonjour **URL de client** , entrez l’URL de hello du point de terminaison de l’application hello SCIM. Par exemple : https://api.contoso.com/scim/v2/
7. Si le point de terminaison hello SCIM requiert un jeton de support OAuth à partir d’un émetteur autre que Azure AD, puis hello de copie requis de jeton de support OAuth dans hello facultatif **Secret jeton** champ. Si ce champ est laissé vide, Azure AD inclut un jeton de porteur OAuth émis par Azure AD avec chaque requête. Les applications qui utilisent Azure AD comme fournisseur d’identité peuvent valider ce jeton émis par Azure AD.
8. Cliquez sur hello **tester la connexion** bouton toohave Azure Active Directory tentative tooconnect toohello SCIM point de terminaison. Si hello tentatives échouent, les informations d’erreur s’affiche.  
9. Si hello tentatives tooconnect toohello application réussisse, puis cliquez sur **enregistrer** toosave l’identification d’administrateur d’hello.
10. Bonjour **mappages** section, il existe deux ensembles sélectionnables des mappages d’attributs : un pour les objets utilisateur et un pour les objets de groupe. Sélectionnez chaque un tooreview hello des attributs qui sont synchronisés à partir de l’application de tooyour Azure Active Directory. Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello utilisateurs et groupes dans votre application pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

    >[!NOTE]
    >Vous pouvez éventuellement désactiver la synchronisation des objets de groupe en désactivant hello « groupes de » de mappage. 

11. Sous **paramètres**, hello **étendue** champ définit les utilisateurs et les groupes sont synchronisés. En sélectionnant « Synchronisation uniquement affecté aux utilisateurs et groupes » (recommandé) est synchronisés uniquement les utilisateurs et groupes affectés Bonjour **utilisateurs et groupes** onglet.
12. Une fois que votre configuration est terminée, modifiez hello **état d’approvisionnement** trop**sur**.
13. Cliquez sur **enregistrer** toostart hello service de configuration d’Azure AD. 
14. Si la synchronisation uniquement affecté aux utilisateurs et groupes (recommandés), être vraiment tooselect hello **utilisateurs et groupes** onglet, puis attribuez les utilisateurs de hello et/ou groupes que vous souhaitez toosync.

Une fois la synchronisation initiale hello a démarré, vous pouvez utiliser hello **journaux d’Audit** onglet progression toomonitor, qui affiche toutes les actions effectuées par hello mise en service du service sur votre application. Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Création de votre propre solution d’attribution pour n’importe quelle application
En créant un service Web SCIM doté d'une interface avec Azure Active Directory, vous pouvez activer l'authentification unique et l'attribution d'utilisateurs d'automatique pour pratiquement n'importe quelle application qui fournit une API d'attribution d'utilisateurs REST ou SOAP.

Fonctionnement :

1. Azure AD fournit une bibliothèque Common Language Infrastructure nommée [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Les développeurs et les intégrateurs système toocreate de cette bibliothèque et de déployer un site web SCIM point de terminaison capable de se connecter de magasin d’identités de l’application Azure AD tooany.
2. Les mappages sont implémentées dans hello web service toomap hello standardisé utilisateur toohello utilisateur schéma et de protocole requis par l’application hello.
3. URL de point de terminaison Hello est inscrit dans Azure AD en tant que partie d’une application personnalisée dans la galerie d’applications hello.
4. Utilisateurs et groupes bénéficient d’application toothis dans Azure AD. Lors de l’affectation, ils sont placés dans une application cible de file d’attente toobe synchronisé toohello. le processus de synchronisation gère la file d’attente hello Hello s’exécute toutes les 20 minutes.

### <a name="code-samples"></a>Exemples de code
toomake ce processus, un ensemble de [exemples de code](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) sont fournis que créer un point de terminaison du service web SCIM et montrent la configuration automatique. Exemple : un fournisseur qui gère un fichier avec des lignes de valeurs séparées par des virgules représentant des utilisateurs et des groupes.  Hello autres est d’un fournisseur qui fonctionne sur le service Amazon Web Services Gestion des identités et l’accès de hello.  

**Configuration requise**

* Visual Studio 2013 ou une version ultérieure
* [Kit de développement logiciel (SDK) Azure pour .NET](https://azure.microsoft.com/downloads/)
* Ordinateur Windows qui prend en charge hello ASP.NET framework 4.5 toobe sert hello de point de terminaison SCIM. Cet ordinateur doit être accessible à partir du cloud de hello
* [Dans un abonnement Azure avec une version d’évaluation ou sous licence d’Azure AD Premium](https://azure.microsoft.com/services/active-directory/)
* exemple d’Amazon AWS Hello requiert des bibliothèques à partir de hello [Toolkit AWS pour Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Pour plus d’informations, consultez hello Lisez-moi fichier inclus dans l’exemple hello.

### <a name="getting-started"></a>Mise en route
Hello tooimplement de façon simple un point de terminaison SCIM qui peut accepter la mise en service des demandes d’Azure AD est toobuild et déployer l’exemple de code hello qui génère le fichier de valeurs séparées par des virgules (CSV) tooa hello utilisateurs fournis.

**toocreate un point de terminaison SCIM exemple :**

1. Télécharger le package d’exemple de code hello à [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Décompressez le package de hello et placez-le sur votre ordinateur Windows à un emplacement tel que C:\AzureAD-BYOA-Provisioning-Samples\.
3. Dans ce dossier, lancez hello FileProvisioningAgent de solution dans Visual Studio.
4. Sélectionnez **Outils > Gestionnaire de Package de bibliothèque > Package Manager Console**et exécutez hello suivant les commandes pour les références de solution du projet tooresolve hello hello FileProvisioningAgent :
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Générez le projet de FileProvisioningAgent hello.
6. Lancer l’application d’invite de commandes hello dans Windows (en tant qu’administrateur) et utilisez hello **cd** commande toochange hello Active tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** dossier.
7. Exécutez hello commande suivante, en remplaçant < adresse ip > avec hello IP adresse ou nom de domaine de l’ordinateur de Windows hello :
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. Dans Windows sous **paramètres Windows > réseau et les paramètres Internet**, sélectionnez hello **pare-feu Windows > Paramètres avancés**et créer un **règle de trafic entrant** qui permet l’accès entrant tooport 9000.
9. Si la machine virtuelle Windows hello est derrière un routeur, hello routeur besoins toobe configuré tooperform traduction d’accès réseau entre le port 9000 qui est exposé toohello internet et le port 9000 sur l’ordinateur de Windows hello. Cela est nécessaire pour tooaccess en mesure de Azure AD toobe ce point de terminaison dans le cloud de hello.

**tooregister hello exemple SCIM point de terminaison dans Azure AD :**

1. Connectez-vous trop[hello Azure portal](https://portal.azure.com). 
2. Parcourir trop ** Azure Active Directory > Applications d’entreprise, puis sélectionnez **nouvelle application > tous les > application Non-gallery**.
3. Entrez un nom pour votre application, puis cliquez sur **ajouter** icône toocreate un objet application. objet d’application Hello créé est prévue toorepresent hello cible application serait approvisionner tooand mise en œuvre de point de terminaison unique hello d’authentification pour et pas seulement SCIM.
4. Dans l’écran hello résultant, sélectionnez hello **Provisioning** onglet dans la colonne de gauche hello.
5. Bonjour **Mode d’approvisionnement** menu, sélectionnez **automatique**.
    
  ![][2]
  *Figure 4 : Configuration de l’approvisionnement Bonjour portail Azure*
    
6. Bonjour **URL de client** , entrez l’URL de hello exposés à internet et de port de votre point de terminaison SCIM. Cela serait quelque chose comme http://testmachine.contoso.com:9000 ou http://<ip-address>:9000/, où < adresse ip > est hello internet exposées IP adresse.  
7. Si le point de terminaison hello SCIM requiert un jeton de support OAuth à partir d’un émetteur autre que Azure AD, puis hello de copie requis de jeton de support OAuth dans hello facultatif **Secret jeton** champ. Si ce champ est laissé vide, Azure AD inclura un jeton de porteur OAuth émis par Azure AD avec chaque requête. Les applications qui utilisent Azure AD comme fournisseur d’identité peuvent valider ce jeton émis par Azure AD.
8. Cliquez sur hello **tester la connexion** bouton toohave Azure Active Directory tentative tooconnect toohello SCIM point de terminaison. Si hello tentatives échouent, les informations d’erreur s’affiche.  
9. Si hello tentatives tooconnect toohello application réussisse, puis cliquez sur **enregistrer** toosave l’identification d’administrateur d’hello.
10. Bonjour **mappages** section, il existe deux ensembles sélectionnables des mappages d’attributs : un pour les objets utilisateur et un pour les objets de groupe. Sélectionnez chaque un tooreview hello des attributs qui sont synchronisés à partir de l’application de tooyour Azure Active Directory. Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello utilisateurs et groupes dans votre application pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.
11. Sous **paramètres**, hello **étendue** champ définit les utilisateurs et les groupes sont synchronisés. En sélectionnant « Synchronisation uniquement affecté aux utilisateurs et groupes » (recommandé) est synchronisés uniquement les utilisateurs et groupes affectés Bonjour **utilisateurs et groupes** onglet.
12. Une fois que votre configuration est terminée, modifiez hello **état d’approvisionnement** trop**sur**.
13. Cliquez sur **enregistrer** toostart hello service de configuration d’Azure AD. 
14. Si la synchronisation uniquement affecté aux utilisateurs et groupes (recommandés), être vraiment tooselect hello **utilisateurs et groupes** onglet, puis attribuez les utilisateurs de hello et/ou groupes que vous souhaitez toosync.

Une fois la synchronisation initiale hello a démarré, vous pouvez utiliser hello **journaux d’Audit** onglet progression toomonitor, qui affiche toutes les actions effectuées par hello mise en service du service sur votre application. Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

étape finale de Hello de vérification de l’exemple hello est tooopen hello fichier TargetFile.csv dans le dossier de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello sur votre ordinateur Windows. Une fois que hello processus de déploiement est exécuté, ce fichier montre les détails hello de tous les affecté et configuré les utilisateurs et groupes.

### <a name="development-libraries"></a>Bibliothèques de développement
toodevelop votre propre service web qui est conforme à la spécification SCIM toohello, tout d’abord vous familiariser avec hello suivant bibliothèques fournies par Microsoft toohelp accélérer le processus de développement hello : 

1. Les bibliothèques CLI (Common Language Infrastructure) sont proposées pour une utilisation avec les langages basés sur cette infrastructure, notamment C#. Une de ces bibliothèques, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), déclare une interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, illustrée hello suivant illustration : A développeur à l’aide des bibliothèques de hello implémente cette interface avec une classe qui peut être appelée de façon générique, en tant que fournisseur. les bibliothèques Hello activer hello développeur toodeploy un service web qui respecte la spécification de SCIM toohello. service web de Hello peut être soit hébergé dans Internet Information Services, ou n’importe quel assembly du Common Language Infrastructure exécutable. Demande est traduite en, ces méthodes appels toohello fournisseur seraient être programmées par toooperate de développeur hello sur le magasin d’identités.
  
  ![][3]
  
2. [Express gestionnaires d’itinéraire](http://expressjs.com/guide/routing.html) sont disponibles pour l’analyse des objets de requête node.js représentant des appels (tel que défini par la spécification de SCIM de hello), service web de node.js tooa.   

### <a name="building-a-custom-scim-endpoint"></a>Création d’un point de terminaison SCIM personnalisé
À l’aide des bibliothèques CLI hello, les développeurs qui utilisent ces bibliothèques peuvent héberger leurs services dans un assembly de Common Language Infrastructure exécutable, ou dans Internet Information Services. Voici un exemple de code pour l’hébergement d’un service dans un assembly exécutable, à l’adresse hello http://localhost : 9000 : 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Ce service doit avoir un HTTP adresse et serveur de certificat d’authentification de quels hello autorité de certification racine est hello suivantes : 

* CNNIC
* Comodo
* CyberTrust
* DigiCert
* GeoTrust
* GlobalSign
* Go Daddy
* VeriSign
* WoSign

Un certificat d’authentification serveur peut être le port lié tooa sur un hôte Windows à l’aide de l’utilitaire shell hello réseau : 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Ici, la valeur hello fournie pour l’argument de certhash hello est l’empreinte numérique hello du certificat de hello, tandis que la valeur hello fournie pour l’argument d’appid hello est un identificateur global unique arbitraire.  

service de hello toohost dans Internet Information Services, un développeur serait générer un assembly de bibliothèque de code CLA avec une classe nommée démarrage dans l’espace de noms hello par défaut de l’assembly hello.  Voici un exemple de classe de ce type : 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Gestion de l’authentification du point de terminaison
Les demandes d’Azure Active Directory incluent un jeton de support OAuth 2.0.   Toute demande hello réception de service doit authentifier émetteur hello comme étant Azure Active Directory pour le compte de locataire Azure Active Directory hello attendu, pour un accès toohello service web de Azure Active Directory Graph.  Jeton de hello, l’émetteur de hello est identifié par une revendication d’iss, comme « iss » : « https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/ ».  Dans cet exemple, l’adresse de base hello de valeur de revendication hello, https://sts.windows.net, identifie les Azure Active Directory comme hello émetteur, tandis que le segment de l’adresse relative, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello est un identificateur unique de hello Azure Active Locataire d’annuaire pour le compte qui hello jeton a été émis.  Si le jeton de hello a été émis pour accéder au service web de Azure Active Directory Graph hello, puis identificateur hello de ce service, 00000002-0000-0000-c000-type "000000000000", doit être dans la valeur hello aud du jeton hello de revendication.  

Les développeurs qui utilisent les bibliothèques CLA hello fournies par Microsoft pour la création d’un service SCIM peuvent authentifier les demandes d’Azure Active Directory à l’aide de paquet Microsoft.owin.Security.ActiveDirectory hello en procédant comme suit : 

1. Dans un fournisseur, implémenter la propriété Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de hello en le faisant retournent un toobe méthode appelée chaque fois que le service de hello est démarré : 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Ajoutez hello suivant code toothat méthode toohave tooany de toute demande de points de terminaison du service hello authentifié comme portant un jeton émis par Azure Active Directory pour le compte d’un client spécifié, pour l’accès toohello service web de Azure AD Graph : 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Schéma des utilisateurs et des groupes
Azure Active Directory peuvent configurer deux types de ressources tooSCIM web services.  Ces types de ressources sont des utilisateurs et des groupes.  

Ressources de l’utilisateur sont identifiés par l’identificateur de schéma hello, urn : ietf:params:scim:schemas:extension:enterprise:2.0:User, qui est inclus dans cette spécification de protocole : http://tools.ietf.org/html/draft-ietf-scim-core-schema.  mappage par défaut de Hello d’attributs hello d’utilisateurs dans les attributs de toohello Azure Active Directory des ressources de l’urn : ietf:params:scim:schemas:extension:enterprise:2.0:User est fourni dans le tableau 1, ci-dessous.  

Ressources du groupe sont identifiés par l’identificateur de schéma hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  Le tableau 2 ci-dessous montre hello par défaut mappés attributs hello des groupes dans Azure les attributs Active Directory toohello des ressources de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  

### <a name="table-1-default-user-attribute-mapping"></a>Tableau 1 : Mappage d’attributs utilisateur par défaut
| Utilisateur Azure Active Directory | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |active |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |title |
| mail |emails[type eq "work"].value |
| mailNickName |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>Tableau 2 : Mappage d’attribut par défaut
| Groupe Azure Active Directory | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickName |displayName |
| membres |membres |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>Approvisionnement et annulation d’approvisionnement utilisateur
Hello après l’illustration montre les messages hello qu’Azure Active Directory envoie tooa SCIM service toomanage hello du cycle de vie d’un utilisateur dans un autre magasin d’identités. diagramme de Hello montre également comment un service SCIM implémenté à l’aide des bibliothèques CLI hello fourni par Microsoft pour la génération de que ces services traduire par ces demandes toohello appelle des méthodes d’un fournisseur.  

![][4]
*Figure 5 : séquence d’approvisionnement et d’annulation de l’approvisionnement d’utilisateurs*

1. Les requêtes Active Directory Azure hello service pour un utilisateur avec une valeur d’attribut externalId correspondance la valeur de l’attribut mailNickname hello d’un utilisateur dans Azure AD. requête de Hello est exprimée comme une demande de protocole HTTP (Hypertext Transfer) telles que cet exemple, dans lequel jyoung est un exemple d’un mailNickname d’un utilisateur dans Azure Active Directory : 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de requête de fournisseur de service hello.  Voici la signature hello de cette méthode : 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Voici la définition hello d’interface de Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello : 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  Bonjour suivant l’exemple d’une requête pour un utilisateur avec une valeur donnée pour l’attribut d’externalId hello, les valeurs des arguments hello passés la méthode de requête toohello sont : 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Si hello réponse tooa toohello service web de requêtes pour un utilisateur avec une valeur d’attribut externalId qui correspond à la valeur de l’attribut mailNickname hello d’un utilisateur ne renvoie pas de tous les utilisateurs, Azure Active Directory demande ensuite cette disposition de service hello un utilisateur toohello correspondant un dans Azure Active Directory.  Voici un exemple de requête : 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  bibliothèques de Common Language Infrastructure Hello fournis par Microsoft pour l’implémentation de services SCIM traduit cette demande dans un toohello d’appel de méthode Create de fournisseur de service hello.  Hello méthode Create a cette signature : 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  Dans une demande tooprovision un utilisateur, valeur hello d’argument de ressource hello est une instance de hello Microsoft.SystemForCrossDomainIdentityManagement. Classe de Core2EnterpriseUser, définie dans la bibliothèque de Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.  Si l’utilisateur de hello tooprovision hello demande réussit, puis hello implémentation de méthode hello est attendu tooreturn une instance de hello Microsoft.SystemForCrossDomainIdentityManagement. Classe Core2EnterpriseUser, avec la valeur hello de propriété de l’identificateur hello définie toohello d’identificateur unique de l’utilisateur qui vient d’être configuré de hello.  

3. tooupdate un utilisateur connu tooexist dans un magasin d’identités fronted par un SCIM, continue d’Azure Active Directory en demandant l’état actuel de hello de cet utilisateur à partir du service de hello avec une demande, tels que : 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Dans un service est généré à l’aide des bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduit en un toohello d’appel de méthode de récupération du fournisseur de service hello.  Voici la signature hello de méthode de récupération hello : 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  Dans l’exemple hello d’un état demande tooretrieve hello en cours d’un utilisateur, les valeurs de hello des propriétés de hello d’objet hello fournie comme valeur de hello d’argument de paramètres hello sont les suivantes : 
  
  * Identificateur "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier : "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Si un attribut de référence est toobe mis à jour, puis Azure Active Directory requêtes hello service toodetermine ou non hello valeur actuelle de l’attribut de référence hello dans le magasin d’identités hello fronted par service de hello correspond déjà la valeur hello de l’attribut dans Azure Active Directory. Pour les utilisateurs, hello seul attribut de quels hello valeur actuelle est interrogée de cette façon est hello manager. Voici un exemple d’une demande de toodetermine si l’attribut de gestionnaire hello d’un objet utilisateur particulier a actuellement une certaine valeur : 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Hello la valeur de paramètre de requête hello attributs id, signifie que s’il existe un objet utilisateur est conforme aux expression hello fournie en tant que valeur hello hello filtre du paramètre de requête, puis service de hello est toorespond attendu avec un urn : ietf:params:scim:schemas : ressource de noyaux : 2.0:User ou urn : ietf:params:scim:schemas:extension:enterprise:2.0:User, incluant hello uniquement la valeur d’attribut d’id de cette ressource.  Hello valeur Hello **id** est inconnu toohello demandeur. Il est inclus dans la valeur hello hello filtre du paramètre de requête ; Hello lui demandant d’elle vise réellement toorequest une représentation minimale d’une ressource qui satisfont à expression de filtre hello comme une indication de ces ou non l’objet existe.   

  Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de requête de fournisseur de service hello. valeur de Hello de propriétés hello objet hello fournie comme valeur de hello d’argument de paramètres hello sont les suivantes : 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  Ici, valeur hello de l’index hello x peut être 0 et valeur hello de hello index y peut être de 1, ou valeur hello de x peut-être être de 1 et valeur hello y peut être 0, selon l’ordre de hello des expressions de hello hello filtre du paramètre de requête.   

5. Voici un exemple d’une demande à partir d’Azure Active Directory tooan SCIM service tooupdate un utilisateur : 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  bibliothèques de Microsoft Common Language Infrastructure Hello pour l’implémentation de services SCIM traduit les demande hello dans un toohello d’appel de méthode de mise à jour du fournisseur de service hello. Voici la signature hello Hello méthode de mise à jour : 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    Dans l’exemple hello d’une demande de tooupdate un utilisateur, objet hello fournie comme valeur de hello d’argument de correctif hello possède ces valeurs de propriété : 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. un utilisateur à partir d’un magasin d’identités de provisionnement toode fronted par un service SCIM, Azure AD envoie une demande de telles que : 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Si le service de hello a été généré à l’aide de bibliothèques du Common Language Infrastructure hello fournis par Microsoft pour l’implémentation de services SCIM, demande de hello est traduite dans un toohello d’appel de méthode de suppression du fournisseur de service hello.   Cette méthode a sa signature : 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  objet de Hello fournie comme valeur de hello d’argument de resourceIdentifier hello possède ces valeurs de propriété dans l’exemple hello d’une demande toode-disposition un utilisateur : 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Approvisionnement et annulation d’approvisionnement d’un groupe
Hello après l’illustration montre les messages hello que Azure AcD envoie tooa SCIM service toomanage hello du cycle de vie d’un groupe dans un autre magasin d’identités.  Ces messages diffèrent des messages hello se rapportant toousers de trois façons : 

* schéma de Hello d’une ressource de groupe est identifié en tant que http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Requêtes tooretrieve groupes stipulent cet attribut de membres hello est toobe exclu à partir de n’importe quelle ressource fournie dans la demande de toohello de réponse.  
* Toodetermine demandes indique si un attribut de référence a une certaine valeur sont des requêtes sur les attributs des membres hello.  

![][5]
*Figure 6 : séquence d’approvisionnement et d’annulation de l’approvisionnement d’un groupe*

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Automatiser la configuration d’utilisateur/Deprovisioning tooSaaS applications](active-directory-saas-app-provisioning.md)
* [Personnalisation des mappages d’attributs pour l’approvisionnement des utilisateurs](active-directory-saas-customizing-attribute-mappings.md)
* [Écriture d’expressions pour les mappages d’attributs](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Filtres d’étendue pour l’approvisionnement des utilisateurs](active-directory-saas-scoping-filters.md)
* [Notifications d’approvisionnement de comptes](active-directory-saas-account-provisioning-notifications.md)
* [Liste des didacticiels sur la façon de tooIntegrate applications SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
