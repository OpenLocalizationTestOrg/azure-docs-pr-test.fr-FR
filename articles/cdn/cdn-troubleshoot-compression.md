---
title: la compression de fichiers aaaTroubleshooting dans Azure CDN | Documents Microsoft
description: "Résolvez les problèmes de compression des fichiers CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Résolution des problèmes de compression des fichiers CDN
Cet article vous aide à résoudre les problèmes de [compression des fichiers CDN](cdn-improve-performance.md).

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) et cliquez sur **Get Support**.

## <a name="symptom"></a>Symptôme
La compression pour votre point de terminaison est activée, mais les fichiers sont renvoyés non compressés.

> [!TIP]
> toocheck si vos fichiers sont retournés compressés, vous devez toouse un outil comme [Fiddler](http://www.telerik.com/fiddler) ou de votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  En-têtes de réponse HTTP de hello vérification retournée avec votre mise en cache CDN contenus.  S’il existe un en-tête nommé `Content-Encoding` avec une valeur **gzip**, **bzip2**, ou **deflate**, votre contenu est compressé.
> 
> ![En-tête d’encodage de contenu](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Cause :
Il existe plusieurs causes possibles, y compris :

* Hello a demandé le contenu n’est pas éligible pour la compression.
* La compression n’est pas activée pour hello type de fichier demandé.
* requête HTTP de Hello n’incluait pas un en-tête de demande d’un type de compression valide.

## <a name="troubleshooting-steps"></a>Étapes de dépannage
> [!TIP]
> Comme avec le déploiement de nouveaux points de terminaison CDN les modifications de configuration prennent certaines toopropagate de temps via le réseau de hello.  En règle générale, les modifications sont appliquées dans les 90 minutes.  S’il s’agit hello première fois que vous avez configuré la compression pour votre point de terminaison CDN, vous devez envisager d’attente toobe 1 et 2 heures que la propagation des paramètres de compression de hello toohello POP. 
> 
> 

### <a name="verify-hello-request"></a>Vérifiez que la demande de hello
Tout d’abord, nous devons effectuer une vérification de validité rapide à la demande de hello.  Vous pouvez utiliser votre navigateur [outils de développement](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello des demandes en cours.

* Vérifiez la demande de hello est envoyé URL de point de terminaison tooyour, `<endpointname>.azureedge.net`et pas votre origine.
* Vérifiez que la demande hello contient un **Accept-Encoding** en-tête et hello valeur pour cet en-tête contient **gzip**, **deflate**, ou **bzip2** .

> [!NOTE]
> Les profils du **CDN Azure fourni par Akamai** prennent uniquement en charge l’encodage **gzip**.
> 
> 

![En-têtes de requête CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Vérifier les paramètres de compression (profil CDN Standard)
> [!NOTE]
> Cette étape s’applique uniquement si votre profil CDN est un profil du **CDN Azure Standard fourni par Verizon** ou du **CDN Azure Standard fourni par Akamai**. 
> 
> 

Accédez de point de terminaison tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur hello **configurer** bouton.

* Vérifiez que la compression est activée.
* Vérifiez le type MIME de hello pour hello contenu toobe compressé est inclus dans la liste hello des formats compressés.

![Paramètres de compression CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Vérifier les paramètres de compression (profil CDN Premium)
> [!NOTE]
> Cette étape s’applique uniquement si votre profil CDN est un profil du **CDN Azure Premium fourni par Verizon** .
> 
> 

Accédez de point de terminaison tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur hello **gérer** bouton.  portail supplémentaire du Hello s’ouvre.  Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.  Cliquez sur **Compression**. 

* Vérifiez que la compression est activée.
* Vérifiez que hello **Types de fichiers** liste contient une liste séparée par des virgules (sans espaces) des types MIME.
* Vérifiez le type MIME de hello pour hello contenu toobe compressé est inclus dans la liste hello des formats compressés.

![Paramètres de compression Premium CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Vérifiez le contenu de hello est mis en cache.
> [!NOTE]
> Cette étape vaut uniquement si votre profil CDN est un profil du **CDN Azure fourni par Verizon** (Standard ou Premium).
> 
> 

À l’aide des outils de développement de votre navigateur, vérifiez le fichier hello tooensure hello réponse en-têtes est mis en cache dans une région de hello où elle est demandée.

* Vérifiez hello **Server** en-tête de réponse.  l’en-tête Hello doit avoir le format de hello **plateforme (ID de serveur/POP)**, comme dans hello l’exemple suivant.
* Vérifiez hello **X-Cache** en-tête de réponse.  Hello en-tête doit indiquer **atteint**.  

![En-têtes de réponse CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Vérifiez le fichier de hello répond aux exigences de taille hello
> [!NOTE]
> Cette étape vaut uniquement si votre profil CDN est un profil du **CDN Azure fourni par Verizon** (Standard ou Premium).
> 
> 

toobe éligible pour la compression, un fichier doit satisfaire hello suivant les exigences de taille :

* Plus de 128 octets.
* Moins de 1 Mo.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Vérifiez la demande hello sur le serveur d’origine hello pour un **Via** en-tête
Hello **Via** en-tête HTTP indique au serveur web toohello qui hello demande est passé par un serveur proxy.  Par défaut des serveurs web Microsoft IIS ne pas compresser les réponses lors de la demande de hello contient un **Via** en-tête.  toooverride ce comportement, hello suivants :

* **IIS 6**: [HcNoCompressionForProxies de définir = « FALSE » dans les propriétés de la métabase IIS hello](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 et**: [définissez à la fois **noCompressionForHttp10** et **noCompressionForProxies** tooFalse de configuration du serveur hello](http://www.iis.net/configreference/system.webserver/httpcompression)

