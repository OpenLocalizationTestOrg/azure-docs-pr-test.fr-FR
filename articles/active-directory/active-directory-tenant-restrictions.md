---
title: "aaaManage accès toocloud applications en limitant les locataires - Azure | Documents Microsoft"
description: "Comment toouse toomanage de locataire Restrictions que les utilisateurs peuvent accéder aux applications en fonction de son locataire Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Utiliser les applications cloud tooSaaS locataire Restrictions toomanage accès

Grandes organisations qui utilisent la sécurité que les services de toocloud toomove tels qu’Office 365, mais tooknow besoin que leurs utilisateurs seulement peuvent accéder à des ressources approuvées. En règle générale, sociétés limiter les noms de domaine ou des adresses IP lorsqu’ils souhaitent toomanage accès. Cette approche échoue dans un monde où les applications SaaS sont hébergées dans un cloud public et s’exécutent sur des noms de domaine partagés comme outlook.office.com et login.microsoftonline.com. Ces adresses de blocage empêcherait les utilisateurs d’accéder à Outlook sur le web de hello entièrement, au lieu de simplement les restriction des ressources et des identités de tooapproved.

Demande d’accès de Azure Active Directory solution toothis est une fonctionnalité appelée Restrictions du locataire. Client Restrictions permet aux organisations toocontrol accès tooSaaS applications, basées sur l’utilisation d’applications hello Azure AD client hello pour l’authentification unique sur le cloud. Par exemple, vous souhaiterez les applications Office 365 tooallow accès tooyour organisation, tout en empêchant les instances de l’accès tooother organisation de ces mêmes applications.  

Restrictions donne aux organisations hello capacité toospecify hello liste de clients que les utilisateurs sont autorisés à tooaccess du client. Azure AD puis accorde uniquement l’accès toothese autorisé locataires.

Cet article se concentre sur les Restrictions de locataire pour Office 365, mais la fonctionnalité de hello doit fonctionner avec n’importe quelle application SaaS cloud qui utilise les protocoles d’authentification moderne avec Azure AD pour l’authentification unique. Si vous utilisez SaaS applications avec un Azure AD différent du locataire du locataire hello utilisé par Office 365, rendre Vérifiez que tous les clients sont autorisés. Pour plus d’informations sur les applications SaaS cloud, consultez hello [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Fonctionnement

Hello global solution comprend hello suivant des composants : 

1. **Azure AD** : si hello `Restrict-Access-To-Tenants: <permitted tenant list>` est présent, Azure AD uniquement les problèmes des jetons de sécurité pour hello autorisés aux clients. 

2. **Infrastructure de serveur proxy local** – un périphérique proxy capable d’inspection SSL, en-tête de hello tooinsert configuré contenant la liste des hello autorisées locataires dans le trafic destiné à Azure AD. 

3. **Le logiciel client** – toosupport locataire Restrictions, le logiciel client doit demander des jetons directement à partir d’Azure AD, afin que le trafic peut être intercepté par l’infrastructure du proxy hello. Actuellement, les Restrictions du client sont prises en charge par les applications Office 365 basées sur un navigateur et par les clients Office en cas d’utilisation de l’authentification moderne (comme OAuth 2.0). 

4. **L’authentification moderne** : services de cloud computing doivent utiliser l’authentification moderne toouse Restrictions du client et bloquer l’accès à tooall les clients non autorisée. Les services Office 365 cloud doivent être des protocoles d’authentification moderne toouse configuré par défaut. Pour hello dernières informations sur la prise en charge Office 365 pour l’authentification moderne, consultez [l’authentification moderne de mise à jour Office 365](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Hello suivant le diagramme illustre le flux de trafic de haut niveau hello. Inspection SSL est requis uniquement sur le trafic tooAzure AD, toohello pas les services de cloud Office 365. Cette distinction est importante, car le volume de trafic hello pour l’authentification tooAzure AD est généralement beaucoup plus faible que les applications de tooSaaS de volume de trafic comme Exchange Online et SharePoint Online.

![Flux de trafic des Restrictions du client - Schéma](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Configurer les Restrictions du client

Il existe deux étapes tooget a démarré avec des Restrictions de locataire. première étape de Hello est toomake sûr que vos clients peuvent se connecter à des adresses droit toohello. Hello est ensuite tooconfigure à votre infrastructure du proxy.

### <a name="urls-and-ip-addresses"></a>URL et adresses IP

toouse Restrictions du locataire, vos clients doivent être toohello en mesure de tooconnect suivant tooauthenticate d’URL Azure AD : login.microsoftonline.com, login.microsoft.com et login.windows.net. En outre, tooaccess Office 365, vos clients doivent également être en mesure de tooconnect toohello/URL de noms de domaine complets et adresses IP définies dans [plages d’adresses IP et des URL d’Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Configuration du proxy et conditions requises

Hello configuration suivante est requis tooenable locataire Restrictions via votre infrastructure de serveur proxy. Ce guide est générique, vous devez faire référence documentation du fournisseur tooyour proxy pour les étapes d’implémentation spécifique.

#### <a name="prerequisites"></a>Composants requis

- proxy de Hello doit être en mesure de tooperform SSL l’interception, insertion d’en-tête HTTP et les destinations de filtre à l’aide de noms de domaine complets/URL. 

- Les clients doivent approuver la chaîne de certificats hello présentée par proxy hello pour les communications SSL. Par exemple, si des certificats à partir d’une infrastructure PKI interne sont utilisés, hello interne émettrice certificat certificat d’autorité racine doit être approuvé.

- Cette fonctionnalité est incluse dans les abonnements Office 365, mais si vous souhaitez que les applications SaaS toouse locataire Restrictions toocontrol accès tooother licences Azure AD Premium 1 sont requis.

#### <a name="configuration"></a>Configuration

Pour chaque toologin.microsoftonline.com de demande entrant, login.microsoft.com et login.windows.net, insérez deux en-têtes HTTP : *restreindre l’accès aux locataires* et *limiter le contexte d’accès*.

en-têtes de Hello doivent inclure hello suivant d’éléments : 
- Pour *restreindre l’accès aux locataires*, une valeur de \<autorisés liste du locataire\>, qui est une liste séparée par des virgules de clients, vous souhaitez tooallow utilisateurs tooaccess. N’importe quel domaine qui est inscrit auprès d’un client peut être le locataire de hello tooidentify utilisé dans cette liste. Par exemple, toopermit accéder aux clients de Contoso et Fabrikam tooboth, hello présente de paire nom/valeur comme :`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Pour *limiter le contexte d’accès*, une valeur d’un ID de répertoire unique, déclaration locataire est paramètre hello client Restrictions. Par exemple, toodeclare Contoso en tant que client hello définies hello stratégie Restrictions du client, une paire nom/valeur hello ressemble à :`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Vous pouvez trouver votre ID de répertoire Bonjour [portail Azure](https://portal.azure.com). Connectez-vous en tant qu’administrateur, sélectionnez **Azure Active Directory**, puis sélectionnez **Propriétés**.

tooprevent les utilisateurs d’insérer leur propre en-tête HTTP avec les clients non approuvés, hello nécessaire proxy en-tête de restreindre l’accès aux locataires hello tooreplace si elle est déjà présent dans la demande entrante de hello. 

Les clients doivent être forcé toouse hello proxy pour toutes les demandes toologin.microsoftonline.com, login.microsoft.com et login.windows.net. Par exemple, si les fichiers de certificat PAC sont utilisées toodirect clients toouse hello proxy, les utilisateurs finaux ne doit pas être en mesure de tooedit ou désactiver les fichiers hello PAC.

## <a name="hello-user-experience"></a>expérience utilisateur Hello

Cette section montre expérience hello pour les utilisateurs et administrateurs.

### <a name="end-user-experience"></a>Expérience de l’utilisateur final

Un exemple d’utilisateur se trouve sur le réseau de Contoso hello, mais la tentative de tooaccess hello Fabrikam instance d’une partagé SaaS application comme Outlook en ligne. Si un client non autorisée pour cette instance n’est Contoso, l’utilisateur hello voit hello suivant page :

![Page Accès refusé pour les utilisateurs dans des clients non autorisés](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Expérience administrateur

Lors de la configuration de Restrictions du client est effectuée sur l’infrastructure du proxy de l’entreprise hello, administrateurs peuvent accéder aux rapports de Restrictions du locataire hello Bonjour portail Azure directement. des rapports tooview hello, atteindre la page de présentation de Azure Active Directory toohello, puis regardez sous « Autres fonctionnalités ».

admin Hello pour le client de hello spécifié en tant que client de hello contexte d’accès restreint peuvent utiliser cette toosee rapport toutes les connexions bloqué en raison d’hello stratégie de Restrictions du locataire, notamment son identité hello utilisée et l’ID de répertoire cible de hello.

![Utiliser des tentatives de connexion Azure tooview portail restreint hello](./media/active-directory-tenant-restrictions/portal-report.png)

Comme d’autres rapports Bonjour portail Azure, vous pouvez utiliser des filtres toospecify hello étendue de votre rapport. Vous pouvez filtrer par utilisateur, application, client ou intervalle de temps spécifique.

## <a name="office-365-support"></a>Prise en charge d’Office 365

Les applications Office 365 doivent respecter la prise en charge de deux critères toofully les Restrictions client :

1. client Hello utilisé prend en charge l’authentification moderne
2. L’authentification moderne est activée en tant que protocole d’authentification par défaut hello pour le service cloud hello.

Consultez trop[l’authentification moderne de mise à jour Office 365](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) pour les informations les plus récentes hello sur lequel Office clients prennent actuellement en charge l’authentification moderne. Cette page inclut également tooinstructions des liens pour l’activation de l’authentification moderne sur spécifique Exchange Online et Skype entreprise Online aux clients. L’authentification moderne est déjà activée par défaut dans SharePoint Online.

Restrictions du client est actuellement pris en charge par les applications Office 365 basée sur navigateur (hello SharePoint du portail Office, Yammer, sites, Outlook sur hello Web, etc..). Pour les clients lourds (Outlook, Skype Entreprise, Word, Excel, PowerPoint, etc.) Les Restrictions du client peuvent uniquement être appliquées si l’authentification moderne est utilisée.  

Outlook et Skype pour les clients d’entreprise qui prennent en charge l’authentification moderne sont toujours en mesure de toouse des protocoles hérités par rapport aux locataires où l’authentification moderne n’est pas activée, contournant les Restrictions du locataire. Pour Outlook sur Windows, les clients peuvent choisir restrictions tooimplement empêcher les utilisateurs finaux d’ajouter des profils de tootheir de comptes de messagerie de non approuvé. Par exemple, consultez hello [empêcher l’ajout de comptes d’Exchange par défaut](http://gpsearch.azurewebsites.net/default.aspx?ref=1) paramètre de stratégie de groupe. Pour Outlook sur les plateformes non Windows et pour Skype Entreprise sur toutes les plateformes, la prise en charge complète des Restrictions du client n’est actuellement pas disponible.

## <a name="testing"></a>Test

Si vous souhaitez tootry les restrictions applicables du client avant l’implémentation pour toute l’organisation, il existe deux options : une approche basée sur l’hôte à l’aide d’un outil comme Fiddler ou un déploiement par étapes des paramètres de proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler pour une approche basée sur hôte

Fiddler est un proxy qui peut être utilisé toocapture et modifier le trafic HTTP/HTTPS, notamment insérer des en-têtes HTTP de débogage gratuitement sur Internet. tooconfigure Fiddler tootest Restrictions du locataire, effectuez hello comme suit :

1.  [Téléchargez et installez Fiddler](http://www.telerik.com/fiddler).
2.  Configurer le trafic HTTPS Fiddler toodecrypt, par [documentation d’aide de Fiddler](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configurer hello tooinsert de Fiddler *restreindre l’accès aux locataires* et *limiter le contexte d’accès* en-têtes à l’aide de règles personnalisées :
  1. Dans l’outil de débogueur Web Fiddler hello, sélectionnez hello **règles** menu et sélectionnez **personnaliser les règles...** fichier de CustomRules tooopen hello.
  2. Ajouter hello lignes au début de hello Hello suivantes *OnBeforeRequest* (fonction). Remplacez le \<domaine du client\> par un domaine enregistré auprès de votre client, par exemple, contoso.onmicrosoft.com. Remplacez \<l’ID de répertoire\> par l’identificateur GUID Azure AD de votre client.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Si vous devez tooallow plusieurs clients, utilisez un nom de client de virgules tooseparate hello. Par exemple :

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Enregistrez et fermez le fichier de CustomRules hello.

Après avoir configuré Fiddler, vous pouvez capturer le trafic en va de toohello **fichier** menu et en sélectionnant **capturer le trafic**.

### <a name="staged-rollout-of-proxy-settings"></a>Déploiement par étapes des paramètres du proxy

En fonction des capacités de hello de votre infrastructure de serveur proxy, vous pouvez être mise en œuvre de hello toostage en mesure d’utilisateurs tooyour de paramètres. Voici deux options principales à prendre en compte :

1.  Utilisez PAC fichiers toopoint utilisateurs tooa test proxy infrastructure de test, alors que les utilisateurs normaux continuent d’infrastructure du proxy toouse hello production.
2.  Certains serveurs proxy peuvent prendre en charge des configurations différentes à l’aide de groupes.

Pour plus d’informations, consultez la documentation de serveur de proxy tooyour.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur [l’authentification moderne Office 365 mise à jour](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Hello de révision [plages d’adresses IP et des URL d’Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
