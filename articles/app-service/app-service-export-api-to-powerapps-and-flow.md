---
title: "aaaExporting un tooPowerApps de l’API de hébergés par Azure et le Microsoft Flow | Documents Microsoft"
description: "Vue d’ensemble de la façon dont tooexpose une API hébergés dans le Service d’applications tooPowerApps et Microsoft Flow"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Exportation d’un tooPowerApps de l’API de hébergés par Azure et de Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Création de connecteurs personnalisés pour PowerApps et Microsoft Flow

[PowerApps](https://powerapps.com) est un service pour la création et l’utilisation d’applications métier personnalisées connectent tooyour données et de travailler sur plusieurs plateformes. [Microsoft Flow](https://flow.microsoft.com) , il est facile tooautomate de flux de travail et des processus d’entreprise entre vos applications favorites et les services. PowerApps et Microsoft Flow sont fournis avec un large éventail de sources de toodata de liens intégrés tels que Office 365, Dynamics 365, Salesforce et bien plus encore. Toutefois, les utilisateurs doivent également des sources de données en mesure de tooleverage toobe et les API en cours de génération par l’entreprise.

De même, les développeurs qui veulent tooexpose leurs API plus largement dans hello organisation souhaiterez toomake leurs tooPowerApps disponible d’API et les utilisateurs de Microsoft Flow. Cette rubrique va vous montrer comment tooexpose une API générée à l’aide de tooPowerApps Azure App Service ou des fonctions d’Azure et Microsoft Flow. [Azure App Service](https://azure.microsoft.com/services/app-service/) est une offre platform-as-a-service qui permet aux développeurs tooquickly et facilement web d’entreprise de génération, mobile et les applications API. [Les fonctions Azure](https://azure.microsoft.com/services/functions/) est une solution basée sur les événements de calcul sans serveur qui vous permet de code auteur tooquickly pouvant réagir tooother des parties de votre système et de la mise à l’échelle en fonction de la demande.

toolearn savoir plus sur ces services, consultez :
- [PowerApps Guided Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) (Formation guidée sur PowerApps) 
- [Formation guidée sur Microsoft Flow](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Présentation d’App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Vue d’ensemble d’Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Partage d’une définition d’API

API est souvent décrits à l’aide un [OpenAPI document](https://www.openapis.org/) (parfois appelée tooas un document « Swagger »). Contient tous les hello plus d’informations sur les opérations sont disponibles et la structuration des données de salutation. PowerApps et Microsoft Flow peuvent créer des connecteurs personnalisés pour tout document Open API 2.0. Une fois un connecteur personnalisé est créé, il peut être utilisé dans hello exactement comme un des hello liens intégrés et peut rapidement être intégré dans une application.

Azure App Service et Azure Functions [prennent en charge](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) la création, l’hébergement et la gestion d’un document Open API. Dans l’ordre toocreate un connecteur personnalisé pour un site web, mobile, API ou d’application de la fonction, PowerApps et flux doivent toobe reçoit une copie de la définition de hello.

> [!NOTE]
> Car une copie de la définition de l’API de hello est utilisée, PowerApps et Microsoft Flow immédiatement ne saura pas sur les mises à jour ou une application de toohello de modifications avec rupture. Si une nouvelle version de l’API de hello est rendue disponible, ces étapes doivent être répétés pour la nouvelle version de hello. 

tooprovide PowerApps et Microsoft Flow avec la définition de l’API hello hébergé pour votre application, procédez comme suit :

1. Ouvrez hello [portail Azure](https://portal.azure.com) et accédez tooyour application du Service d’applications ou des fonctions d’Azure.

    Si vous utilisez le Service d’applications Azure, sélectionnez **définition d’API** à partir de la liste des paramètres hello. 
    
    Si vous utilisez Azure Functions, sélectionnez votre application de fonction, choisissez **Fonctionnalités de la plateforme**, puis **Définition de l’API**. Vous pouvez également choisir de tooopen hello **définition d’API (version préliminaire)** onglet à la place.

2. Si une définition de l’API a été fournie, vous verrez un **exporter tooPowerApps + Microsoft Flow** bouton. Cliquez sur ce processus d’exportation bouton toobegin hello.

3. Sélectionnez hello **mode d’exportation**. Ce paramètre détermine les étapes hello vous devez toofollow toocreate un connecteur. App Service offre deux options pour fournir votre définition d’API à PowerApps et Microsoft Flow :

    **Express** vous permet de créer hello personnalisé connecteur dans hello portail Azure. Il requiert que hello que vous utilisez actuellement connecté l’utilisateur a connecteurs de toocreate d’autorisation dans l’environnement cible de hello. Il s’agit de hello approche recommandée si cette condition peut être remplie. Si vous utilisez ce mode, suivez hello [Express exportation](#express) instructions ci-dessous.

    **Manuel** vous permet d’exporter une copie de la définition d’API hello qui peut être importée à l’aide de hello PowerApps ou Microsoft Flow portails. Il s’agit de hello approche recommandée si hello utilisateur Azure et hello utilisateur avec des connecteurs de toocreate d’autorisation sont différentes personnes ou si le connecteur de hello doit toobe créé dans une autre locataire. Si vous utilisez ce mode, suivez hello [importation et exportation manuelle](#manual) instructions ci-dessous.

<a name="express"></a>
## <a name="express-export"></a>Mode d’exportation express

Dans cette section, vous allez créer un nouveau connecteur personnalisé à partir de hello portail Azure. Vous devez être connecté en hello client toowhich vous souhaitez tooexport, et vous devez avoir toocreate d’autorisation à un connecteur personnalisé dans l’environnement cible de hello.

1. Sélectionnez l’environnement hello dans lequel vous souhaitez que le connecteur de hello toocreate. Puis, indiquez un nom pour votre connecteur personnalisé.

2. Si votre définition de l’API comprend des définitions de sécurité, elles seront exigées à l’étape n° 2. Si nécessaire, sécuriser hello détails de la configuration des utilisateurs de toogrant d’accès nécessaire tooyour API. Pour en savoir plus, consultez la section [Authentification](#auth) plus bas. 

3. Cliquez sur **OK** toocreate votre lien personnalisé.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Mode d’exportation et d’importation manuel

Dans l’ordre toocreate un connecteur personnalisé pour un site web, mobile, API ou d’application de la fonction, les deux étapes seront nécessaires :

1. [La récupération de la définition de l’API hello à partir du Service d’applications ou des fonctions d’Azure](#export)
2. [L’importation de la définition de l’API hello dans PowerApps et Microsoft Flow](#import)

Il est possible que ces deux étapes devez toobe effectué par différentes personnes au sein d’une organisation, comme un utilisateur donné ne peut pas avoir tooperform d’autorisation les deux actions. Dans ce cas, un développeur qui a des collaborateurs accès toohello application du Service d’applications ou les fonctions Azure devez définition de hello API tooobtain (un seul fichier JSON) ou un tooit de lien. Ils devront à tooprovide puis lequel définition tooa PowerApps ou Microsoft Flow le propriétaire. Peut utiliser ce lien personnalisé de hello métadonnées toocreate hello.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>La récupération de la définition de l’API hello à partir du Service d’applications ou des fonctions d’Azure

Dans cette section, vous allez exporter la définition de l’API hello votre API de Service d’application, toobe utilisé ultérieurement dans le portail de PowerApps ou Microsoft Flow hello.

1. Vous pouvez choisir tooeither **télécharger hello API définition** ou **obtenir un lien**. Selon que vous choisissez, le résultat de hello sera fournie dans la section suivante de hello. Sélectionnez une de ces options et suivez les instructions de hello.
 
2. Si votre définition de l’API comprend des définitions de sécurité, elles seront exigées à l’étape n° 2. Lors de l’importation, PowerApps et Microsoft Flow détecteront ces définitions et demanderont les informations de sécurité. Rassemblez hello informations d’identification associées tooeach définition pour une utilisation dans la section suivante de hello. Pour en savoir plus, consultez la section [Authentification](#auth) plus bas. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>L’importation de la définition de l’API hello dans PowerApps et Microsoft Flow

Dans cette section, vous allez créer un connecteur personnalisé dans PowerApps et Microsoft Flow à l’aide de la définition de hello API obtenue précédemment. Connecteurs personnalisés sont partagés entre hello deux services, il suffit de définition de hello tooimport qu’une seule fois. Pour plus d’informations sur les connecteurs personnalisés, consultez [enregistrer et utiliser des connecteurs personnalisés dans PowerApps] et [enregistrer et utiliser des connecteurs personnalisés dans Microsoft Flow].

1. Ouvrez hello [portail web de Powerapps](https://web.powerapps.com) ou hello [portail web de Microsoft Flow](https://flow.microsoft.com/)et vous connecter. 

2. Cliquez sur hello **paramètres** bouton (icône d’engrenage hello) hello en haut à droite de la page de hello et sélectionnez **les connecteurs personnalisé**. 

3. Cliquez sur **Créer un connecteur personnalisé**.

4. Sur hello **général** onglet, fournissez un nom pour votre API et puis télécharger la définition de OpenAPI hello ou collez dans l’URL de métadonnées hello. Cliquez sur **Continuer**.

4. Sur hello **sécurité** sous l’onglet si vous n’êtes plus d’informations d’authentification demandées tooprovide, entrez les valeurs hello obtenus dans la section précédente de hello. Dans le cas contraire, passez toohello prochaine étape.

5. Sur hello **définitions** onglet, toutes les opérations de hello définies dans votre fichier OpenAPI sont remplis automatiquement. Si toutes vos opérations requises sont définies, vous pouvez accéder toohello prochaine étape. Si ce n’est pas le cas, vous pouvez ajouter et modifier les opérations ici.

6. Cliquez sur **Créer un connecteur**. Si vous souhaitez que les appels d’API tootest, accédez à toohello prochaine étape.

7. Sur hello **Test** , créer une connexion, sélectionnez une opération tootest et entrez les données requises par l’opération de hello.

8. Cliquez sur **Test de fonctionnement**.


<a name="auth"></a>
## <a name="authentication"></a>Authentification

PowerApps et Microsoft Flow prend en charge une collection de fournisseurs d’identité qui peut être toolog utilisé dans les utilisateurs de votre lien personnalisé. Si votre API nécessite une authentification, assurez-vous qu’elle est capturée en tant que _définition de sécurité_ dans votre document Open API. Pendant l’exportation, vous aurez besoin des valeurs de configuration tooprovide permettent à une action d’ouverture de session Microsoft Flow tooperform PowerApps.

Cette section traite des types d’authentification hello qui sont pris en charge par le flux de hello express : clé API, Azure Active Directory et générique OAuth 2.0. Pour obtenir une liste complète des fournisseurs et des informations d’identification hello chacune nécessite, consultez [enregistrer et utiliser des connecteurs personnalisés dans PowerApps] et [enregistrer et utiliser des connecteurs personnalisés dans Microsoft Flow].

### <a name="api-key"></a>Clé API
Lorsque cette méthode de sécurité est utilisée, hello de votre connecteur pourront clé de hello tooprovide demandées lorsqu’ils créent une connexion. Vous pouvez fournir une toohelp de nom de la clé d’API que leur savoir quelle clé est nécessaire. Pour les fonctions d’Azure, il s’agit généralement une des clés d’hôte hello, couvrant plusieurs fonctions au sein de l’application de fonction hello.

### <a name="azure-active-directory"></a>Azure Active Directory
Lorsque vous configurez un connecteur personnalisé qui requiert une connexion d’AAD, deux inscriptions d’application AAD sont nécessaires : une API de serveur principal toomodel hello et d’un connecteur de hello toomodel dans PowerApps et le flux.

Votre API doit être configuré toowork avec la première inscription à hello et ce sera déjà être prises en charge si vous avez utilisé hello [d’authentification/autorisation du Service application](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) fonctionnalité.

Vous devez toomanually créer l’enregistrement du deuxième hello pour le connecteur de hello, à l’aide des étapes hello traitées dans [Ajout d’une application AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Hello l’inscription doit toohave déléguée accès tooyour API et une URL de réponse de `https://msmanaged-na.consent.azure-apim.net/redirect`. Consultez [cet exemple](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) pour plus de détails, en remplaçant votre API pour hello Azure Resource Manager.

Hello, les valeurs de configuration suivantes est requise :
- **ID client** -hello ID client de votre inscription auprès d’AAD du connecteur
- **Clé secrète client** -question secrète du client hello de votre inscription auprès d’AAD du connecteur
- **URL de connexion** hello - URL de base pour AAD. Dans Azure public, il s’agit généralement de `https://login.windows.net`.
- **ID de locataire** -hello ID de hello client toobe est utilisé pour la connexion de hello. Doit être « commune » ou hello ID du client hello dans le hello connecteur est en cours de création.
- **URL de ressource** -hello URL de ressource de l’enregistrement AAD API principal

> [!IMPORTANT]
> Si une autre personne sera importer la définition de hello API dans PowerApps et Microsoft Flow dans le cadre du flux de hello manuelle, vous devez tooprovide avec hello client et ID de clé secrète du client **de l’inscription du connecteur de hello**, ainsi que en tant qu’URL de ressource hello de votre API. Assurez-vous que ces informations secrètes sont gérées de façon sécurisée. **Ne partagez pas les informations d’identification de sécurité hello Hello API elle-même.**

### <a name="generic-oauth-20"></a>Generic OAuth 2.0
prise en charge OAuth 2.0 générique Hello vous permet de toointegrate avec n’importe quel fournisseur OAuth 2.0. Ainsi, vous toobring dans n’importe quel fournisseur personnalisé qui n’est pas pris en charge en mode natif.

Hello, les valeurs de configuration suivantes est requise :
- **ID client** -hello ID de client OAuth 2.0
- **Clé secrète client** -question secrète du client hello OAuth 2.0
- **URL d’autorisation** -hello URL d’autorisation OAuth 2.0
- **URL de jeton** -hello URL de jeton OAuth 2.0
- **Actualiser les URL** -hello URL d’actualisation OAuth 2.0



[enregistrer et utiliser des connecteurs personnalisés dans PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[enregistrer et utiliser des connecteurs personnalisés dans Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
