---
title: "aaaHow toobuild une application qui peut se connecter n’importe quel utilisateur Azure AD | Documents Microsoft"
description: "Procédure étape par étape pour créer une application capable de connecter un utilisateur à partir de n’importe quel client Azure Active Directory, également appelée application mutualisée."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Comment toosign dans n’importe quel utilisateur Azure Active Directory (AD) à l’aide hello modèle d’application de l’architecture mutualisée
Si vous proposez un logiciel comme un réduire d’application de Service organisations, vous pouvez configurer votre application tooaccept connexions à partir de n’importe quel client Azure AD.  Dans Azure AD, ce processus s’appelle créer une application mutualisée.  Les utilisateurs de n’importe quel client Azure AD seront en mesure de toosign dans l’application tooyour après consentez toouse leur compte avec votre application.  

Si vous avez une application existante qui possède son propre système de compte, ou prend en charge d’autres types de connexion auprès d’autres fournisseurs cloud, l’ajout de la connexion Azure AD à partir de n’importe quel client est simple. Inscrivez simplement votre application, ajoutez le code de connexion via OAuth2, OpenID Connect ou SAML, et placez un bouton « Se connecter avec Microsoft » dans votre application. Cliquez sur hello suivant toolearn bouton plus sur la personnalisation de votre application.

[![Bouton d’inscription][Connexion à AAD]][AAD-App-Branding]

Cet article suppose que vous êtes déjà familiarisé avec la création d’une application à client unique pour Azure AD.  Si vous n’êtes pas le cas, head sauvegarde toohello [page d’accueil du guide de développement] [ AAD-Dev-Guide] et essayez l’une de nos Démarrages rapides !

Il existe quatre étapes simples tooconvert votre application dans une application de plusieurs locataire Azure AD :

1. Mettre à jour votre application d’enregistrement toobe architecture mutualisée
2. Mettre à jour votre /common de code toosend demandes toohello point de terminaison 
3. Mettre à jour votre code toohandle plusieurs valeurs de l’émetteur
4. Comprendre le consentement de l’utilisateur et de l’administrateur et application des modifications de code appropriées

Examinons chaque étape en détail. Vous pouvez également accéder directement trop[cette liste d’exemples d’architecture mutualisées][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Architecture mutualisée de mise à jour d’enregistrement toobe
Par défaut, les inscriptions web app/API dans Azure AD sont de type client unique.  Rendez votre inscription mutualisée en recherche basculer hello » multiples avec clients » sur la page des propriétés de l’enregistrement de l’application Bonjour hello [portail Azure] [ AZURE-portal] et en lui affectant trop « Oui ».

Notez également, avant d’effectuer une application mutualisée, Azure AD nécessite hello URI ID d’application de toobe d’application hello globalement unique. Hello URI ID d’application est une des manières de hello qu'une application est identifiée dans les messages de protocole.  Pour une application à locataire unique, il est suffisant pour toobe d’URI ID d’application hello unique au sein de ce client.  Pour une application mutualisée, il doit être globalement unique pour Azure Active Directory puisse trouver l’application hello sur tous les locataires.  L’unicité globale est appliquée en demandant hello URI ID d’application toohave un nom d’hôte qui correspond à un domaine vérifié du locataire Azure AD de hello.  Par exemple, si le nom hello de votre client a été contoso.onmicrosoft.com puis valide URI ID d’application serait `https://contoso.onmicrosoft.com/myapp`.  Si votre client possède le domaine vérifié `contoso.com`, un URI ID d’application valide serait alors `https://contoso.com/myapp`.  Définition d’une application en tant qu’architecture mutualisée échouera si hello URI ID d’application ne suit pas ce modèle.

Les inscriptions clientes natives sont mutualisées par défaut.  Vous n’avez pas besoin tootake tout toomake action native client application d’enregistrement mutualisée.

## <a name="update-your-code-toosend-requests-toocommon"></a>Mettre à jour votre code toosend demandes trop commun
Dans une application à locataire unique, les demandes de connexion sont envoyés connexion point de terminaison du client toohello. Par exemple, pour contoso.onmicrosoft.com point de terminaison hello serait :

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Les demandes envoyées de point de terminaison du locataire tooa peut se connecter les utilisateurs (ou invités) dans ce tooapplications locataire dans ce locataire.  Avec une application mutualisée, application hello ne sait pas au préalable quel utilisateur de hello client provient, afin que vous ne pouvez pas envoyer des demandes point de terminaison du client tooa.  Au lieu de cela, les demandes sont envoyées tooan de point de terminaison qui sur AD Azure tous les locataires :

    https://login.microsoftonline.com/common

Lorsque Azure AD reçoit une demande sur hello/point de terminaison commun, il connecte les utilisateur hello et comme une conséquence détecte utilisateur hello client provient.  Hello/point de terminaison commun fonctionne avec tous les protocoles d’authentification hello pris en charge par Azure AD : OpenID Connect, OAuth 2.0, SAML 2.0 et WS-Federation.

application Hello réponse de connexion toohello puis contient un jeton représentant hello utilisateur.  valeur d’émetteur Hello dans le jeton de hello indique une application quel utilisateur de hello du client à partir de.  Lorsqu’une réponse est reçue hello/point de terminaison commun, valeur d’émetteur hello dans le jeton de hello correspondront locataire toohello de l’utilisateur.  Il est important de toonote hello/point de terminaison commun n’est pas un client et n’est pas un émetteur, elle est simplement un multiplexeur.  Lorsque vous utilisez /common, hello logique dans les jetons de toovalidate de votre application doit toobe mis à jour tootake cela en compte. 

Comme mentionnées précédemment, mutualisées applications doivent également fournir une expérience utilisateur cohérente pour les utilisateurs, suivant hello application Azure AD instructions de personnalisation. Cliquez sur hello suivant toolearn bouton plus sur la personnalisation de votre application.

[![Bouton d’inscription][Connexion à AAD]][AAD-App-Branding]

Examinons une utilisation hello de hello /common point de terminaison et l’implémentation de votre code plus en détail.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Mettre à jour votre code toohandle plusieurs valeurs de l’émetteur
Les applications web et les API reçoivent et valident les jetons d’Azure AD.  

> [!NOTE]
> Alors que les applications clientes natives demander et recevoir des jetons d’Azure AD, ils le font dans ce toosend les tooAPIs, où ils sont validés.  Les applications natives ne valident pas les jetons et doivent les traiter comme des valeurs opaques.
> 
> 

Examinons la manière dont une application valide les jetons qu’elle reçoit d’Azure AD.  Une application à client unique sélectionne généralement une valeur de point de terminaison de type :

    https://login.microsoftonline.com/contoso.onmicrosoft.com

et l’utiliser tooconstruct une URL de métadonnées (dans ce cas, OpenID Connect) telles que :

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload deux informations essentielles qui sont des jetons de toovalidate utilisé : client de hello de la signature du clés et la valeur de l’émetteur.  Chaque locataire Azure AD a une valeur d’émetteur unique sous forme de hello :

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

où la valeur GUID de hello est version rename-safe de hello d’ID du hello client de hello.  Si vous cliquez sur hello précédant le lien de métadonnées pour `contoso.onmicrosoft.com`, vous pouvez voir cette valeur de l’émetteur dans le document de hello.

Lorsqu’une application à locataire unique valide un jeton, il vérifie la signature hello du jeton hello contre hello clés à partir du document de métadonnées hello de signature. Ainsi, il toomake valeur d’émetteur hello que hello correspondances jeton Bonjour un qui a été trouvé dans le document de métadonnées hello.

Depuis hello/common point de terminaison ne correspond pas tooa client et n’est pas un émetteur, lorsque vous examinez la valeur d’émetteur hello dans les métadonnées de hello pour/communes qu’il a une URL basée sur un modèle au lieu d’une valeur réelle :

    https://sts.windows.net/{tenantid}/

Par conséquent, une application mutualisée ne peut pas valider les jetons simplement en mettant en correspondance la valeur d’émetteur hello dans les métadonnées de hello avec hello `issuer` valeur de jeton de hello.  Une application mutualisée a besoin d’une logique toodecide les valeurs de l’émetteur sont valides et qui sont pas, selon les locataire hello partie ID de valeur d’émetteur hello.  

Par exemple, si une application mutualisée autorise uniquement les connexion des clients spécifiques qui se sont inscrites pour leur service, puis il doit vérifier valeur d’émetteur hello ou hello `tid` toomake de jeton hello que ce client se trouve dans leur liste de valeur de revendication abonnés.  Si une application mutualisée traite avec des personnes uniquement et ne rend pas toutes les décisions d’accès basées sur les clients, il peut ignorer hello émetteur valeur complètement.

Dans les exemples d’architecture mutualisée hello Bonjour [connexes contenu](#related-content) section à fin hello de cet article, la validation de l’émetteur est désactivé tooenable tout toosign de locataire Azure AD dans.

Maintenant examinons confort hello pour les utilisateurs qui se connectent à des applications de toomulti-client.

## <a name="understanding-user-and-admin-consent"></a>Comprendre le consentement de l’utilisateur et de l’administrateur
Pour un utilisateur toosign dans l’application tooan dans Azure AD, application hello doit être représentée dans le locataire de l’utilisateur hello.  Ainsi, organisation de hello toodo choses comme appliquer des stratégies lorsque des utilisateurs à partir de leurs clients se connectent toohello application.  Pour une application à locataire unique, cet enregistrement est simple ; Il a hello qui se produit lorsque vous enregistrez l’application hello Bonjour [portail Azure][AZURE-portal].

Pour une application mutualisée, l’inscription initiale de hello pour une application hello vit dans le locataire d’Azure AD hello utilisé par le développeur de hello.  Quand un utilisateur à partir d’un autre client s’inscrit dans l’application toohello pour hello première fois, Azure AD vous demande les autorisations de toohello tooconsent demandées par l’application hello.  Si ils donnent leur consentement, une représentation de l’application hello appelé un *principal du service* est créé dans hello du client de l’utilisateur et de connexion peut continuer. Une délégation est également créée dans le répertoire hello qui enregistre hello consentement toohello application utilisateur. Consultez [les objets de Principal du Service et Application] [ AAD-App-SP-Objects] pour plus d’informations sur l’application hello des objets d’Application et de principal du service, et comment elles rapportent tooeach autres.

![Consentement toosingle de couche application][Consent-Single-Tier] 

Cette expérience de consentement est affectée par les autorisations de hello demandées par l’application hello.  Azure AD prend en charge deux types d’autorisations, application seule et application déléguée :

* Une autorisation déléguée accorde une tooact de capacité application hello comme un utilisateur connecté pour un sous-ensemble de l’utilisateur de hello hello choses.  Par exemple, vous pouvez accorder une application Bonjour autorisation déléguée tooread Bonjour signé dans un calendrier de l’utilisateur.
* Une application uniquement l’autorisation directement identité toohello de l’application hello.  Par exemple, vous pouvez accorder une liste des tooread hello application hello application seule autorisation des utilisateurs dans un client, quelle que soit l’application de toohello qui est connecté.

Certaines autorisations peuvent être consenti tooby un utilisateur standard, tandis que d’autres nécessitent le consentement de l’administrateur d’un client. 

### <a name="admin-consent"></a>Consentement de l’administrateur
Les autorisations application seule nécessitent toujours le consentement de l’administrateur d’un client.  Si votre application demande une autorisation d’application uniquement, et un utilisateur tente de toosign dans toohello application, un message d’erreur s’affichera indiquant que les utilisateurs hello n’est pas en mesure de tooconsent.

Certaines autorisations déléguées nécessitent également le consentement de l’administrateur d’un client.  Par exemple, hello capacité toowrite arrière tooAzure AD en tant qu’utilisateur connecté de hello requiert le consentement de l’administrateur d’un client.  Comme les autorisations d’application uniquement, si un utilisateur ordinaire tente toosign dans application tooan qui demande une autorisation déléguée qui requiert le consentement de l’administrateur, votre application reçoit une erreur.  Si une autorisation nécessite ou non consentement de l’administrateur est déterminé par le développeur hello qui a publié les ressources hello et se trouve dans la documentation de hello pour la ressource de hello.  Liens tootopics décrivant les autorisations disponibles hello pour hello API Azure AD Graph et l’API Graph sont Bonjour [connexes contenu](#related-content) section de cet article.

Si votre application utilise des autorisations qui nécessitent le consentement de l’administrateur, vous devez toohave un mouvement tel qu’un bouton ou un lien sur lequel hello admin action peut être lancée hello.  demande de Hello votre application envoie pour cette action est une demande d’autorisation OAuth2/OpenID Connect habituelle, mais qui inclut également hello `prompt=admin_consent` paramètre de chaîne de requête.  Une fois hello administrateur a donné son consentement et principal du service hello est créé dans le locataire de hello, demandes de connexion ultérieures n’avez pas besoin de hello `prompt=admin_consent` paramètre. Étant donné que l’administrateur de hello a décidé hello demandé que les autorisations sont acceptables, aucun autre utilisateur de client de hello ne sera invité à donner son consentement à partir de là.

Hello `prompt=admin_consent` paramètre peut également être utilisé par les applications qui demandent des autorisations qui ne nécessitent pas de consentement de l’administrateur. Cette opération est effectuée lorsque hello application requiert une expérience où hello tenant admin « inscrit » une fois et aucun autre sont invités à donner son consentement à partir de ce point sur.

Si une application requiert le consentement de l’administrateur, et un administrateur se connecte en mais hello `prompt=admin_consent` paramètre n’est pas envoyé, hello admin sera consentement correctement toohello application **uniquement pour leur compte d’utilisateur**.  Les utilisateurs standard ne seront toujours pas en mesure de toosign dans et application toohello de consentement.  Cela est utile si vous souhaitez toogive hello client administrateur hello capacité tooexplore votre application avant d’autoriser l’accès aux autres utilisateurs.

Un administrateur peut interdire hello pour les utilisateurs normaux tooconsent tooapplications.  Si cette fonctionnalité est désactivée, consentement de l’administrateur est toujours requis pour hello application toobe est défini dans le locataire de hello.  Si vous souhaitez tootest votre application avec le consentement d’utilisateur normal désactivée, vous trouverez hello commutateur de la configuration de client de hello Azure AD section de configuration de hello [portail Azure][AZURE-portal].

> [!NOTE]
> Certaines applications cherchent à une expérience où utilisateurs normaux sont en mesure de tooconsent initialement et versions ultérieure application hello peut impliquer administrateur de hello et demander des autorisations qui nécessitent le consentement de l’administrateur.  Il est sans toodo de façon ceci avec un enregistrement unique d’application dans Azure AD aujourd'hui.  point de terminaison v2 Hello à venir Azure AD permettra applications autorisations toorequest lors de l’exécution, au lieu d’au moment de l’inscription, qui activera ce scénario.  Pour plus d’informations, consultez hello [Guide du développeur v2 modèle d’application Azure AD][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Consentement et applications multiniveau
Votre application peut comporter plusieurs niveaux, chacun représenté par sa propre inscription dans Azure AD.  Par exemple, une application native qui appelle une API web ou une application web qui appelle une autre API web.  Dans ces deux cas, client hello (application native ou web) demande de ressource de hello autorisations toocall (API web).  Pour hello client toobe consenti correctement dans un affichage du locataire, toutes les ressources toowhich, il demande des autorisations doit déjà exister dans du hello locataire.  Si cette condition n’est pas remplie, Azure AD renvoie une erreur qui hello ressource doit être ajoutée en premier.

**Plusieurs niveaux dans un seul client**

Cela peut poser problème si votre application logique implique deux ou plusieurs inscriptions d’application, par exemple un client et une ressource distincts.  Comment obtenir les ressources hello dans locataire hello premier ?  Azure AD aborde ce cas en activant client et la ressource toobe consenti en une seule étape. utilisateur de Hello voit hello la somme totale des autorisations hello demandé par le client de hello et ressources sur la page de consentement hello.  tooenable ce comportement, inscription d’application de la ressource hello doit inclure l’ID d’application du client hello comme un `knownClientApplications` dans son manifeste d’application.  Par exemple :

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Cette propriété peut être mis à jour via la ressource de hello [manifeste de l’application][AAD-App-Manifest]. Cela est illustré dans un client natif à plusieurs niveaux appelant exemple web API Bonjour [connexes contenu](#related-content) section à fin hello de cet article. Hello diagramme suivant fournit une vue d’ensemble de consentement pour une application à plusieurs niveaux enregistrée dans un client unique :

![Consentement toomulti couche client connus application][Consent-Multi-Tier-Known-Client] 

**Plusieurs niveaux dans plusieurs clients**

Un cas similaire se produit si différents niveaux de hello d’une application sont inscrits dans les différents clients.  Par exemple, considérez cas hello de la création d’une application cliente native qui appelle hello Office 365 Exchange Online API.  toodevelop hello natif application et versions ultérieur pour toorun d’application native hello dans un affichage du locataire, le principal du service Exchange Online hello doit être présent.  Dans ce cas, hello développeur et le client doivent acheter Exchange Online pour toobe principal du service hello créé dans leurs clients.  

Dans les cas de hello d’une API générée par une organisation autre que Microsoft, développeur de hello Hello API doit tooprovide un moyen pour leur application de hello tooconsent clients dans les clients de leurs clients. Hello recommandé est de conception pour Bonjour 3e partie développeur toobuild Bonjour API tel qu’il peut également fonctionner comme tooimplement d’un client web d’inscription :

1. Suivez hello hello de tooensure antérieur sections API implémente les spécifications de hello application mutualisée/code d’enregistrement
2. En outre tooexposing hello API étendues et des rôles, vérifiez l’inscription de hello comprend hello « se connecter et lire le profil de l’utilisateur « autorisation Azure AD (fournie par défaut)
3. Implémenter une page de connexion-dans/connexion-haut dans le client web hello suivant hello [consentement de l’administrateur](#admin-consent) guide traite de la version antérieure 
4. Une fois que l’utilisateur de hello donne son consentement toohello application, hello liens de service principal et l’autorisation de délégation sont créés dans leur locataire, et application native hello peut obtenir des jetons pour hello API

Hello suivant schéma fournit une vue d’ensemble de consentement pour une application à plusieurs niveaux inscrite dans différents locataires :

![Application multipartie toomulti-niveau de consentement][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Révocation d’un consentement
Les utilisateurs et les administrateurs peuvent révoquer application tooyour de consentement à tout moment :

* Les utilisateurs revoke accès tooindividual applications en les supprimant de leur [Applications du volet d’accès] [ AAD-Access-Panel] liste.
* Administrateurs de révoquer l’accès tooapplications en les supprimant de Azure AD à l’aide de la section de gestion hello Azure AD de hello [portail Azure][AZURE-portal].

Si un administrateur a consenti application tooan pour tous les utilisateurs dans un locataire, les utilisateurs ne peut pas révoquer l’accès individuellement.  Seul l’administrateur de hello peut révoquer l’accès et uniquement pour hello toute application.

### <a name="consent-and-protocol-support"></a>Consentement et prise en charge des protocoles
Consentement est pris en charge dans Azure AD via hello OAuth, OpenID Connect, WS-Federation et SAML protocoles.  Hello protocoles SAML et WS-Federation ne gèrent pas hello `prompt=admin_consent` paramètre, donc le consentement de l’administrateur est uniquement possible via OAuth et OpenID Connect.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Applications mutualisées et mise en cache des jetons d’accès
Applications mutualisées peuvent également obtenir toocall de jetons d’accès API qui est protégés par Azure AD.  Une erreur courante lors de l’utilisation de hello Active Directory Authentication Library (ADAL) avec une application mutualisée, est tooinitially demande un jeton pour un utilisateur à l’aide de /common, recevoir une réponse, puis demander un jeton suivant pour le même utilisateur également à l’aide de /common.  Étant donné que la réponse hello d’Azure AD provient d’un client, pas/commun, la bibliothèque ADAL met en cache le jeton hello comme étant à partir du client de hello. Hello ultérieur appeler tooget trop commun un jeton d’accès pour entrée de cache hello utilisateur échecs hello et hello utilisateur est invité à toosign dans à nouveau.  Assurez-vous que des appels à un utilisateur déjà connecté deviennent tooavoid manquant du cache hello, point de terminaison du client toohello.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toobuild une application qui peut se connecter un utilisateur à partir de n’importe quel client Azure Active Directory. Après avoir activé l’authentification unique entre votre application et d’Azure Active Directory, vous pouvez également mettre à jour votre tooaccess application API exposées par les ressources de Microsoft, tels qu’Office 365. Par conséquent, vous pouvez offrir une expérience personnalisée dans votre application, par exemple affichant des informations contextuelles toohello utilisateurs, telles que leur photo de profil ou de leur prochain rendez-vous de calendrier. toolearn en savoir plus sur l’API de fabrication appelle tooAzure Active Directory et services Office 365 comme Exchange, SharePoint, OneDrive, OneNote, Planner, Excel et plus d’informations, visitez : [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Contenu connexe
* [Exemples d’applications mutualisées][AAD-Samples-MT]
* [Directives de personnalisation des applications][AAD-App-Branding]
* [Guide du développeur Azure AD][AAD-Dev-Guide]
* [Objets principal du service et application][AAD-App-SP-Objects]
* [Intégration d’applications dans Azure Active Directory][AAD-Integrating-Apps]
* [Vue d’ensemble de l’infrastructure de consentement de hello][AAD-Consent-Overview]
* [Étendues des autorisations de l’API Graph Microsoft][MSFT-Graph-permision-scopes]
* [Étendues des autorisations de l’API Graph Azure AD][AAD-Graph-Perm-Scopes]

Utilisez hello suivant tooprovide des commentaires de la section commentaires et nous aider à affiner et mettre en forme notre contenu.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














