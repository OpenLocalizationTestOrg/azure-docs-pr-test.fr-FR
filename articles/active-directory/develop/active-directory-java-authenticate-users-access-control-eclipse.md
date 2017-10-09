---
title: "aaaHow toouse le contrôle d’accès (Java) | Documents Microsoft"
description: "Découvrez comment toodevelop et l’utilisation de contrôle d’accès avec Java dans Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 247dfd59-0221-4193-97ec-4f3ebe01d3c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: cbbce3b1a05eabf3b86a8cb91db1bde92dbb8960
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthenticate-web-users-with-azure-access-control-service-using-eclipse"></a>Comment tooAuthenticate utilisateurs Web auprès d’Azure Access Control Service à l’aide de Eclipse
Ce guide vous explique comment toouse hello Azure Access Control Service (ACS) au sein de la boîte à outils Azure pour Eclipse de hello. Pour plus d’informations sur ACS, consultez hello [étapes](#next_steps) section.

> [!NOTE]
> Hello filtre d’Azure Access Control Services est une version préliminaire CTP. En tant que logiciel préliminaire, il n'est pas officiellement pris en charge par Microsoft.
> 
> 

## <a name="what-is-acs"></a>Qu'est-ce qu'ACS ?
La plupart des développeurs ne sont pas des experts en matière d'identité et ne souhaitent généralement pas passer du temps à développer des mécanismes d'authentification et d'autorisation pour leurs applications et services. ACS est un service Azure qui fournit un moyen facile d’authentifier les utilisateurs qui ont besoin de tooaccess vos applications web et services sans avoir la logique d’authentification complexe toofactor dans votre code.

Hello suivant les fonctionnalités est disponible dans des services ACS :

* Intégration avec Windows Identity Foundation (WIF).
* Prise en charge des fournisseurs d'identité Web reconnus, notamment Windows Live ID, Google, Yahoo! et Facebook.
* Prise en charge d'Active Directory Federation Services (AD FS) 2.0.
* Un protocole Open Data Protocol (OData)-service de gestion qui fournit l’accès par programme des paramètres de tooACS.
* Portail de gestion qui permet un accès administratif toohello les paramètres des services ACS.

Pour plus d'informations sur ACS, consultez la page [Access Control Service 2.0][Access Control Service 2.0].

## <a name="concepts"></a>Concepts
Azure ACS repose sur les entités de hello d’identité basée sur les revendications, une approche cohérente toocreating des mécanismes d’authentification pour les applications qui s’exécutent localement ou dans le cloud de hello. Identité basée sur les revendications fournit une méthode courante pour les applications et services tooacquire les informations d’identité dont ils ont besoin sur les utilisateurs au sein de leur organisation, dans d’autres organisations et sur hello Internet.

tâches hello toocomplete de ce guide, vous devez comprendre hello suivant concepts :

**Client** -dans le contexte de hello de cette façon-tooguide, il s’agit d’un navigateur qui tente d’une application web de toogain access tooyour.

**Application de partie de confiance (RP) de tiers** -application d’une partie de confiance est un site Web ou un service qui sous-traite l’autorité d’authentification externe tooone. Dans le jargon d’identité, nous dire que ce hello RP fait confiance à cette autorité. Ce guide explique comment tooconfigure votre tootrust d’application des services ACS.

**Jeton** : un jeton est un ensemble de données de sécurité généralement émis après identification d'un utilisateur. Il contienne un ensemble de *revendications*, attributs de hello authentifié l’utilisateur. Une demande peut représenter le nom d'un utilisateur, son âge, l'identifiant pour un rôle qui lui est attribué, etc. Un jeton est généralement numériquement signé, ce qui signifie qu’il peut toujours être Corée tooits arrière émetteur et son contenu ne peut pas être falsifié. Une application utilisateur de partie de confiance du tooa gains d’accès à l’aide d’un jeton valide émis par une autorité qui reconnaît les applications de partie de confiance hello.

**Fournisseur d'identité** : un fournisseur d'identité est une autorité qui authentifie des identités d'utilisateur et émet des jetons de sécurité. travail réel de Hello d’émission de jetons est implémentée si un service spécial appelé Service de jeton de sécurité (STS). Les fournisseurs d'identité les plus connus sont Windows Live ID, Facebook, les référentiels d'utilisateurs professionnels (tels qu'Active Directory), etc.
Lorsque des services ACS est configuré tootrust une adresse IP, système de hello accepter et valider les jetons émis par cette IP. ACS peut faire confiance à plusieurs adresses IP à la fois, ce qui signifie que lorsque votre application fait confiance à des services ACS, vous pouvez proposer instantanément votre hello de tooall application les clients authentifiés de hello toutes les adresses IP que des services ACS fait confiance à votre place.

**Fournisseur de fédération** : les fournisseurs d'identité connaissent directement les utilisateurs et les authentifient grâce à leurs informations d'identification. Ils émettent des demandes en fonction des informations utilisateur connues. Un fournisseur de fédération est un autre type d’autorité : au lieu d'authentifier directement les utilisateurs, il agit comme intermédiaire entre l'application par partie de confiance et un ou plusieurs fournisseurs d'identité. Les fournisseurs d'identité comme les fournisseurs de fédération émettent des jetons de sécurité, ils utilisent donc tous les deux le service STS. ACS est un fournisseur de fédération.

**Moteur de règles ACS** -logique hello tootransform utilisé les jetons entrants à partir de la confiance des adresses IP tootokens destinée toobe consommée par hello RP est codifiée sous forme d’un simple des règles de transformation des revendications. ACS comprend un moteur de règles qui est chargé d'appliquer la logique de transformation que vous avez indiquée pour votre partie de confiance.

**Espace de noms ACS** : l'espace de noms constitue la partition la plus élevée d'ACS que vous utilisez pour organiser vos paramètres. Un espace de noms conserve une liste d’adresses IP que vous faites confiance, les applications de partie de confiance hello souhaité tooserve, règles hello que vous attendez hello règle moteur tooprocess les jetons entrants et ainsi de suite. Un espace de noms expose plusieurs points de terminaison qui seront utilisé par l’application hello et la tooperform tooget ACS développeur sa fonction.

Hello figure ci-dessous illustre le fonctionnement de l’authentification ACS avec une application web :

![Diagramme de flux ACS][acs_flow]

1. client Hello (dans ce cas, un navigateur) demande une page de hello RP.
2. Étant donné que la demande de hello n’est pas encore authentifié, hello RP redirige les autorité toohello hello utilisateur qu’il approuve, c'est-à-dire des services ACS. Hello ACS présente hello utilisateur choix hello d’adresses IP qui ont été spécifiées pour cette partie de confiance. utilisateur de Hello sélectionne hello les IP appropriée.
3. Hello client parcourt la page d’authentification d’IP toohello et invite hello utilisateur toolog sur.
4. Après l’authentification de client de hello (par exemple, identité hello entrées des informations d’identification), hello IP émet un jeton de sécurité.
5. Après avoir émis un jeton de sécurité, hello IP redirige hello client tooACS et client de hello envoie le jeton de sécurité hello émis par hello IP tooACS.
6. ACS valide le jeton de sécurité hello émis par adresse IP hello, entrées hello identité de ce jeton de revendications dans le moteur de règles hello ACS, calcule les revendications d’identité de sortie hello et émet un nouveau jeton de sécurité qui contient ces revendications de sortie.
7. ACS redirige hello client toohello RP. client de Hello envoie un nouveau jeton de sécurité hello émis par ACS toohello RP. Hello RP valide signature hello sur hello jeton de sécurité émis par ACS valide ce jeton de revendications hello et retourne la page hello qui a été demandée.

## <a name="prerequisites"></a>Composants requis
tâches de hello toocomplete dans ce guide, vous devez suivant de hello :

* Kit de développement logiciel (SDK) Java version 1.6 ou ultérieure
* IDE (environnement de développement intégré) Eclipse pour développeurs Java EE, Indigo ou ultérieur, Vous pouvez le télécharger à l’adresse suivante : <http://www.eclipse.org/downloads/>. 
* Une distribution d'un serveur Web ou d'un serveur d'applications basé sur Java, tel que Apache Tomcat, GlassFish, JBoss Application Server ou Jetty.
* Un abonnement Azure, qui peut être obtenu à l’adresse <http://www.microsoft.com/windowsazure/offers/>.
* Hello boîte à outils Azure pour Eclipse, avril 2014 de version ou une version ultérieure. Pour plus d’informations, consultez [installation hello boîte à outils Azure pour Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690946.aspx).
* Un toouse de certificat X.509 avec votre application. Vous avez besoin du certificat public (.cer) et de celui au format Personal Information Exchange (.PFX) (les instructions de création de ce certificat sont indiquées plus loin dans ce didacticiel).
* Vous êtes familiarisé avec hello Azure compute émulateur et le déploiement techniques décrits dans la page [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx).

## <a name="create-an-acs-namespace"></a>Création d'un espace de noms ACS
toobegin à l’aide du Service de contrôle d’accès (ACS) dans Azure, vous devez créer un espace de noms ACS. espace de noms Hello fournit une étendue unique pour l’adressage des ressources des services ACS à partir de votre application.

1. Ouvrez une session sur hello [portail de gestion Azure][Azure Management Portal].
2. Cliquez sur **Active Directory**. 
3. toocreate un nouvel espace de noms Access Control, cliquez sur **nouveau**, cliquez sur **des Services d’application**, cliquez sur **le contrôle d’accès**, puis cliquez sur **création rapide** . 
4. Entrez un nom pour l’espace de noms hello. Azure vérifie que le nom hello est unique.
5. Sélectionnez la région hello dans le hello espace de noms est utilisé. Pour de meilleures performances de hello, utilisez la région hello dans lequel vous déployez votre application.
6. Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse pour l’espace de noms hello ACS.
7. Cliquez sur **Créer**.

Azure crée et Active l’espace de noms hello. Attendez que l’état du nouvel espace de noms hello hello est **Active** avant de continuer. 

## <a name="add-identity-providers"></a>Ajout de fournisseurs d'identité
Dans cette tâche, vous ajoutez toouse d’adresses IP avec votre application de partie de confiance pour l’authentification. À des fins de démonstration, cette tâche montre comment tooadd Windows Live comme une adresse IP, mais vous pouvez utiliser des hello que des adresses IP répertoriée dans hello portail de gestion des services ACS.

1. Bonjour [portail de gestion Azure][Azure Management Portal], cliquez sur **Active Directory**, sélectionnez un espace de noms de contrôle d’accès, puis cliquez sur **gérer**. Hello portail de gestion des services ACS s’ouvre.
2. Dans le volet de navigation gauche hello Hello portail de gestion ACS, cliquez sur **fournisseurs d’identité**.
3. Windows Live ID est activé par défaut. Il n'est pas possible de le supprimer. Dans le cadre de ce didacticiel, seul Windows Live ID est utilisé. Toutefois, cet écran est où vous pouvez ajouter les autres adresses IP, en cliquant sur hello **ajouter** bouton.

Windows Live ID est maintenant activé comme fournisseur d'identité pour votre espace de noms ACS. Ensuite, vous spécifiez votre application web de Java (toobe créé ultérieurement) comme une partie de confiance.

## <a name="add-a-relying-party-application"></a>Ajout d'une application par partie de confiance
Dans cette tâche, vous configurez des services ACS toorecognize votre application web Java en tant qu’une application de partie de confiance valide.

1. Dans le portail de gestion des services ACS de hello, cliquez sur **applications de partie de confiance**.
2. Sur hello **Applications de partie de confiance** , cliquez sur **ajouter**.
3. Sur hello **ajouter une Application par partie de confiance** page, procédez comme hello suivant :
   
   1. Dans **nom**, nom du type hello Hello RP. Pour suivre l'exemple de ce didacticiel, entrez **Azure Web App**.
   2. Dans **Mode**, sélectionnez **Enter settings manually**.
   3. Dans **domaine**, type hello URI toowhich hello jeton de sécurité émis par ACS s’applique. Pour suivre notre exemple, entrez **http://localhost:8080/**.
      ![Domaine de partie de confiance à utiliser dans l'émulateur de calcul][relying_party_realm_emulator]
   4. Dans **URL de renvoi,** type hello URL toowhich ACS retourne le jeton de sécurité hello. Dans le cas présent, entrez **http://localhost:8080/MyACSHelloWorld/index.jsp**
      ![URL de retour vers partie de confiance pour utilisation dans l'émulateur de calcul][relying_party_return_url_emulator]
   5. Accepte les valeurs par défaut de hello reste hello de champs de hello.
4. Cliquez sur **Enregistrer**.

Vous avez correctement configuré votre application web Java lorsqu’il est exécuté dans l’émulateur de calcul Azure hello (à http://localhost : 8080 /) toobe une partie de confiance dans votre espace de noms ACS. Créez ensuite des règles de hello ACS utilise des revendications de tooprocess pour hello RP.

## <a name="create-rules"></a>Création de règles
Dans cette tâche, vous définissez des règles hello qui définissent la façon dont les revendications sont transmises à partir d’adresses IP tooyour RP. Fins hello de ce guide, nous allons simplement configurer types de revendications d’entrée ACS toocopy hello et les valeurs directement dans le jeton de sortie hello, sans filtrage ou en les modifiant.

1. Dans la page principale du portail de gestion ACS hello, cliquez sur **groupes de règles**.
2. Sur hello **groupes de règles** , cliquez sur **groupe de règles par défaut pour l’application Web Azure**.
3. Sur hello **modifier un groupe de règles** , cliquez sur **générer**.
4. Sur hello **générer des règles : groupe de règles par défaut pour l’application Web Azure** page, vérifiez que Windows Live ID est cochée, puis sur **générer**.    
5. Sur hello **modifier un groupe de règles** , cliquez sur **enregistrer**.

## <a name="upload-a-certificate-tooyour-acs-namespace"></a>Télécharger un espace de noms certificat tooyour ACS
Dans cette tâche, vous allez télécharger un. Certificat PFX qui sera utilisé toosign les demandes de jeton créés par votre espace de noms ACS.

1. Dans la page principale du portail de gestion ACS hello, cliquez sur **certificats et clés**.
2. Sur hello **certificats et clés** , cliquez sur **ajouter** ci-dessus **signature de jetons**.
3. Sur hello **ajouter un jeton de signature de certificat ou clé** page :
   1. Bonjour **utilisé pour** , cliquez sur **Application de partie de confiance** et sélectionnez **Azure Web App** (ce que vous avez précédemment en tant que nom hello de votre application de confiance).
   2. Bonjour **Type** section, sélectionnez **certificat X.509**.
   3. Bonjour **certificat** section, cliquez sur le bouton Parcourir de hello et accédez toohello fichier de certificat X.509 que vous souhaitez toouse. Il s'agit d'un fichier .PFX. Sélectionnez le fichier de hello, cliquez sur **ouvrir**, puis entrez le mot de passe du certificat hello Bonjour **mot de passe** zone de texte. Dans le cadre d'un test, vous pouvez utiliser un certificat auto-signé. toocreate un certificat auto-signé, utilisez hello **nouveau** bouton Bonjour **bibliothèque du filtre ACS** boîte de dialogue (décrite plus loin), ou utilisez hello **encutil.exe** utilitaire hello [site Web de projet] [ project website] Hello Azure Starter Kit pour Java.
   4. Vérifiez que **Make Primary** est sélectionné. Votre **ajouter un jeton de signature de certificat ou clé** page doit être similaire toohello suivant.
       ![Ajouter un certificat de signature de jeton][add_token_signing_cert]
   5. Cliquez sur **enregistrer** toosave vos paramètres et les fermer hello **ajouter un jeton de signature de certificat ou clé** page.

Ensuite, passez en revue les informations hello hello intégration d’Application page et copie Bonjour URI que vous devez tooconfigure votre toouse d’application Java web des services ACS.

## <a name="review-hello-application-integration-page"></a>Page d’intégration d’Application vérifier hello
Vous pouvez trouver toutes les informations de hello et tooconfigure nécessaire du code hello votre toowork de l’application (application de partie de confiance de hello) de web Java avec ACS sur la page d’intégration d’Application hello Hello portail de gestion des services ACS. Ces informations sont nécessaires pour la configuration de votre application Web Java et l'authentification fédérée.

1. Dans le portail de gestion des services ACS de hello, cliquez sur **intégration d’Application**.  
2. Bonjour **intégration d’Application** , cliquez sur **Pages de connexion**.
3. Bonjour **intégration de Page de connexion** , cliquez sur **application Web Azure**.

Bonjour **intégration de Page de connexion : application Web Azure** URL de la page, hello répertorié dans **Option 1 : page de connexion hébergée par ACS lien tooan** sera utilisé dans votre application web Java. Lorsque vous ajoutez hello filtre Azure Access Control service bibliothèque tooyour application Java, vous devez cette valeur.

## <a name="create-a-java-web-application"></a>Création d'une application web Java
1. Dans Eclipse, au menu de hello, cliquez sur **fichier**, cliquez sur **nouveau**, puis cliquez sur **projet Web dynamique**. (Si vous ne voyez pas **projet Web dynamique** répertorié comme un projet disponible après avoir cliqué sur **fichier**, **nouveau**, puis hello suivant : cliquez sur **fichier**, cliquez sur **nouveau**, cliquez sur **projet**, développez **Web**, cliquez sur **projet Web dynamique**, puis cliquez sur  **Ensuite**.) Pour des raisons de ce didacticiel, nommez le projet de hello **MyACSHelloWorld**. (Assurez-vous vous utilisez ce nom, les étapes suivantes de ce didacticiel attendent votre toobe de fichier WAR nommé MyACSHelloWorld). Votre écran apparaîtra similaire toohello suivantes :
   
    ![Créer un projet Hello World pour l'exemple ACS][create_acs_hello_world]
   
    Cliquez sur **Terminer**.
2. Dans la vue de l'Explorateur de projets Eclipse, développez **MyACSHelloWorld**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.
3. Bonjour **nouveau fichier JSP** boîte de dialogue, le nom de fichier hello **index.jsp**. Conservez le dossier parent hello MyACSHelloWorld/WebContent, comme indiqué dans les éléments suivants de hello :
   
    ![Ajouter un fichier JSP pour l'exemple ACS][add_jsp_file_acs]
   
    Cliquez sur **Suivant**.
4. Bonjour **sélectionner un modèle JSP** boîte de dialogue, sélectionnez **nouveau fichier JSP (html)** et cliquez sur **Terminer**.
5. Lorsque le fichier de hello index.jsp s’ouvre dans Eclipse, ajoutez dans le texte toodisplay **ACS Bonjour !** dans hello existant `<body>` élément. Votre mise à jour `<body>` le contenu doit apparaître comme suit de hello :
   
        <body>
          <b><% out.println("Hello ACS World!"); %></b>
        </body>
   
    Enregistrez index.jsp.

## <a name="add-hello-acs-filter-library-tooyour-application"></a>Ajouter hello application tooyour de bibliothèque filtre ACS
1. Dans l'Explorateur de projets Eclipse, cliquez avec le bouton droit sur **MyACSHelloWorld**, cliquez sur **Build Path**, puis sur **Configure Build Path**.
2. Bonjour **chemin d’accès de Build Java** boîte de dialogue, cliquez sur hello **bibliothèques** onglet.
3. Cliquez sur **Add Library**.
4. Cliquez sur **Azure Access Control Services Filter (by MS Open Tech)**, puis sur **Suivant**. Hello **filtre Azure Access Control service** boîte de dialogue s’affiche.  (hello **emplacement** champ peut avoir un chemin d’accès différent, selon où vous avez installé Eclipse, et le numéro de version hello peut être différent, en fonction des mises à jour logicielles.)
   
    ![Ajouter la bibliothèque de filtres ACS][add_acs_filter_lib]
5. À l’aide d’un navigateur ouvert toohello **intégration de Page de connexion** page Hello portail de gestion, de copier l’URL hello répertorié dans hello **Option 1 : page de connexion hébergée par ACS lien tooan** champ et le coller dans hello **Point de terminaison de l’authentification ACS** champ de boîte de dialogue hello Eclipse.
6. À l’aide d’un navigateur ouvert toohello **modifier l’Application par partie de confiance** page Hello portail de gestion, de copier l’URL hello répertorié dans hello **domaine** champ et le coller dans hello **domaine de partie de confiance**  champ de boîte de dialogue hello Eclipse.
7. Au sein de hello **sécurité** section hello Eclipse boîte de dialogue, si vous voulez toouse un certificat existant, cliquez sur **Parcourir**, accédez toohello certificat que vous souhaitez toouse, sélectionnez, puis cliquez sur  **Ouvrez**. Ou, si vous voulez toocreate un nouveau certificat, cliquez sur **nouveau** toodisplay hello **nouveau certificat** boîte de dialogue, puis spécifiez le mot de passe hello, nom de fichier .cer de hello et nom du fichier .pfx hello hello nouveau certificat.
8. Vérifiez **certificat de hello incorporé dans le fichier WAR hello**. Incorporation de certificat hello de cette manière inclut dans votre déploiement sans avoir toomanually l’ajouter en tant que composant. (Si vous devez plutôt enregistrer votre certificat en externe à partir de votre fichier WAR, vous pouvez ajouter le certificat de hello comme un composant de rôle et désactivez **certificat de hello incorporé dans le fichier WAR hello**.)
9. [Facultatif] Laissez la case à cocher **Require HTTPS connections** activée. Si vous définissez cette option, vous devez tooaccess votre application en utilisant le protocole HTTPS hello. Si vous ne souhaitez pas toorequire les connexions HTTPS, désactivez cette option.
10. Pour un déploiement toohello calcul émulateur, votre **Azure ACS filtre** paramètres ressemblera similaire toohello suivant.
    
    ![Émulateur de calcul Azure paramètres du filtre ACS pour un déploiement de toohello][add_acs_filter_lib_emulator]
11. Cliquez sur **Terminer**.
12. Cliquez sur **Yes** dans la boîte de dialogue indiquant qu'un fichier web.xml va être créé.
13. Cliquez sur **OK** tooclose hello **chemin d’accès de Build Java** boîte de dialogue.

## <a name="deploy-toohello-compute-emulator"></a>Déployer l’émulateur de calcul toohello
1. Dans l'Explorateur de projets Eclipse, cliquez avec le bouton droit sur **MyACSHelloWorld**, cliquez sur **Azure**, puis sur **Package for Azure**.
2. Dans **Project name**, entrez **MyAzureACSProject**, puis cliquez sur **Suivant**.
3. Sélectionnez un JDK et un serveur d'applications. (Ces étapes sont décrites en détail dans hello [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) didacticiel).
4. Cliquez sur **Terminer**.
5. Cliquez sur hello **exécuter dans l’émulateur Azure** bouton.
6. Après le démarrage de votre application web Java dans l’émulateur de calcul hello, fermez toutes les instances de votre navigateur (de sorte que toutes les sessions de navigateur actuelle n’interfèrent pas avec votre test de connexion des services ACS).
7. Exécutez votre application en ouvrant <http://localhost:8080/MyACSHelloWorld/> dans votre navigateur (ou <https://localhost:8080/MyACSHelloWorld/> si vous avez activé la case à cocher **Require HTTPS connections**). Vous devez fournir un identifiant Windows Live ID, puis vous devez être dirigé toohello les URL de renvoi spécifiée pour votre application de partie de confiance.
8. Lorsque vous avez terminé de consulter votre application, cliquez sur hello **réinitialiser l’émulateur Azure** bouton.

## <a name="deploy-tooazure"></a>Déployer tooAzure
toodeploy tooAzure, vous devez toochange hello partie de confiance domaine et renvoi URL de confiance pour votre espace de noms ACS.

1. Au sein de hello portail de gestion Azure Bonjour **modifier l’Application par partie de confiance** , modifiez **domaine** URL de hello toobe de votre site déployé. Remplacez **exemple** portant le nom DNS de hello vous avez spécifié pour votre déploiement.
   
    ![Domaine de partie de confiance à utiliser en production][relying_party_realm_production]
2. Modifier **URL de renvoi** URL de hello toobe de votre application. Remplacez **exemple** portant le nom DNS de hello vous avez spécifié pour votre déploiement.
   
    ![URL de renvoi de partie de confiance à utiliser en production][relying_party_return_url_production]
3. Cliquez sur **enregistrer** toosave change de votre URL mise à jour les tiers domaine et de renvoi.
4. Conserver hello **intégration de Page de connexion** page ouverte dans votre navigateur, vous devez vous toocopy à partir de celui-ci dans quelques instants.
5. Dans l'Explorateur de projets Eclipse, cliquez avec le bouton droit sur **MyACSHelloWorld**, cliquez sur **Build Path**, puis sur **Configure Build Path**.
6. Cliquez sur hello **bibliothèques** , cliquez sur **filtre Azure Access Control service**, puis cliquez sur **modifier**.
7. À l’aide d’un navigateur ouvert toohello **intégration de Page de connexion** page Hello portail de gestion, de copier l’URL hello répertorié dans hello **Option 1 : page de connexion hébergée par ACS lien tooan** champ et le coller dans hello **Point de terminaison de l’authentification ACS** champ de boîte de dialogue hello Eclipse.
8. À l’aide d’un navigateur ouvert toohello **modifier l’Application par partie de confiance** page Hello portail de gestion, de copier l’URL hello répertorié dans hello **domaine** champ et le coller dans hello **domaine de partie de confiance**  champ de boîte de dialogue hello Eclipse.
9. Au sein de hello **sécurité** section hello Eclipse boîte de dialogue, si vous voulez toouse un certificat existant, cliquez sur **Parcourir**, accédez toohello certificat que vous souhaitez toouse, sélectionnez, puis cliquez sur  **Ouvrez**. Ou, si vous voulez toocreate un nouveau certificat, cliquez sur **nouveau** toodisplay hello **nouveau certificat** boîte de dialogue, puis spécifiez le mot de passe hello, nom de fichier .cer de hello et nom du fichier .pfx hello hello nouveau certificat.
10. Conserver **certificat de hello incorporé dans le fichier WAR hello** activée, en supposant que le certificat de hello tooembed dans le fichier WAR hello.
11. [Facultatif] Laissez la case à cocher **Require HTTPS connections** activée. Si vous définissez cette option, vous devez tooaccess votre application en utilisant le protocole HTTPS hello. Si vous ne souhaitez pas toorequire les connexions HTTPS, désactivez cette option.
12. Pour un déploiement tooAzure, vos paramètres de filtre d’Azure ACS recherche similaire toohello suivant.
    
    ![Paramètres de filtre ACS Azure pour un déploiement de production][add_acs_filter_lib_production]
13. Cliquez sur **Terminer** tooclose hello **modifier la bibliothèque** boîte de dialogue.
14. Cliquez sur **OK** tooclose hello **propriétés MyACSHelloWorld** boîte de dialogue.
15. Dans Eclipse, cliquez sur hello **publier tooAzure Cloud** bouton. Répondre aux invites toohello, similaires comme étant effectués dans hello **toodeploy tooAzure de votre application** section Hello [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) rubrique. 

Une fois que votre application web a été déployée, fermez toutes les sessions de navigateur ouvert, exécuter votre application web, et vous devez fournir toosign avec informations d’identification de l’identifiant Windows Live ID, suivi d’envoi toohello retourne l’URL de votre application de confiance.

Lorsque vous avez terminé à l’aide de votre application ACS Hello World, n’oubliez pas les déploiement de hello toodelete (vous pouvez apprendre comment toodelete un déploiement Bonjour [création d’une Application Hello World pour Azure dans Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944.aspx) rubrique).

## <a name="next_steps"></a>Étapes suivantes
Pour un examen de hello SAML Security Assertion Markup Language () retournée par une application de tooyour ACS, consultez [comment tooview SAML retourné par hello Azure Access Control Service][How tooview SAML returned by hello Azure Access Control Service]. toofurther Explorer tooexperiment avec des scénarios plus sophistiqués et les fonctionnalités d’ACS, consultez [Access Control Service 2.0][Access Control Service 2.0].

En outre, cette hello exemple **certificat de hello incorporé dans le fichier WAR hello** option. Cette option permet de certificat de hello toodeploy simple. Si vous préférez tookeep votre certificat de signature distinct à partir de votre fichier WAR, vous pouvez utiliser hello suivant technique :

1. Au sein de hello **sécurité** section Hello **filtre Azure Access Control service** boîte de dialogue, tapez **${env. JAVA_HOME}/myCert.cer** et désactivez **certificat de hello incorporé dans le fichier WAR hello**. Modifiez mycert.cer si le nom de fichier du certificat est différent. Cliquez sur **Terminer** boîte de dialogue tooclose hello.
2. Certificat hello de copie en tant que composant dans votre déploiement : dans l’Explorateur de projets d’Eclipse, développez **MyAzureACSProject**, avec le bouton droit **WorkerRole1**, cliquez sur **propriétés** , développez **rôle Azure**, puis cliquez sur **composants**.
3. Cliquez sur **Add**.
4. Au sein de hello **ajouter un composant** boîte de dialogue :
   
   1. Bonjour **importation** section :
      1. Hello d’utilisation **fichier** bouton toonavigate toohello certificat toouse. 
      2. Sous **Method**, sélectionnez **copy**.
   2. Pour **en tant que nom**, cliquez sur la zone de texte hello et acceptez le nom par défaut de hello.
   3. Bonjour **déployer** section :
      1. Sous **Method**, sélectionnez **copy**.
      2. Pour **toodirectory**, type **JAVA_HOME %**.
   4. Votre **ajouter un composant** boîte de dialogue doit se présenter comme toohello suivant.
      
       ![Ajouter un composant de certificat][add_cert_component]
   5. Cliquez sur **OK**.

Votre certificat doit maintenant être inclus dans votre déploiement. Notez qu’incorporer le certificat de hello dans le fichier WAR hello ou en ajouter en tant que d’un déploiement tooyour de composant, vous devez tooupload hello certificat tooyour espace de noms comme décrit dans hello [télécharger un espace de noms tooyour ACS certificat] [ Upload a certificate tooyour ACS namespace] section.

[What is ACS?]: #what-is
[Concepts]: #concepts
[Prerequisites]: #pre
[Create a Java web application]: #create-java-app
[Create an ACS Namespace]: #create-namespace
[Add Identity Providers]: #add-IP
[Add a Relying Party Application]: #add-RP
[Create Rules]: #create-rules
[Upload a certificate tooyour ACS namespace]: #upload-certificate
[Review hello Application Integration Page]: #review-app-int
[Configure Trust between ACS and Your ASP.NET Web Application]: #config-trust
[Add hello ACS Filter library tooyour application]: #add_acs_filter_library
[Deploy toohello compute emulator]: #deploy_compute_emulator
[Deploy tooAzure]: #deploy_azure
[Next steps]: #next_steps
[project website]: http://wastarterkit4java.codeplex.com/releases/view/61026
[How tooview SAML returned by hello Azure Access Control Service]: active-directory-java-view-saml-returned-by-access-control.md
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[Windows Identity Foundation]: http://www.microsoft.com/download/en/details.aspx?id=17331
[Windows Identity Foundation SDK]: http://www.microsoft.com/download/en/details.aspx?id=4451
[Azure Management Portal]: https://manage.windowsazure.com
[acs_flow]: ./media/active-directory-java-authenticate-users-access-control-eclipse/ACSFlow.png

<!-- Eclipse-specific -->
[add_acs_filter_lib]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibrary.png
[add_acs_filter_lib_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryEmulator.png
[add_acs_filter_lib_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddACSFilterLibraryProduction.png

[relying_party_realm_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmEmulator.png
[relying_party_return_url_emulator]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLEmulator.png
[relying_party_realm_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyRealmProduction.png
[relying_party_return_url_production]: ./media/active-directory-java-authenticate-users-access-control-eclipse/RelyingPartyReturnURLProduction.png
[add_cert_component]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddCertificateComponent.png
[add_jsp_file_acs]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddJSPFileACS.png
[create_acs_hello_world]: ./media/active-directory-java-authenticate-users-access-control-eclipse/CreateACSHelloWorld.png
[add_token_signing_cert]: ./media/active-directory-java-authenticate-users-access-control-eclipse/AddTokenSigningCertificate.png

