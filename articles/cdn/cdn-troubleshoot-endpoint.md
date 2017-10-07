---
title: "points de terminaison CDN Azure aaaTroubleshooting renvoi d’état 404 | Documents Microsoft"
description: "Dépannez les codes de réponse 404 avec les points de terminaison de CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Dépannage des points de terminaison de CDN renvoyant des états 404
Cet article vous aide à résoudre les problèmes liés aux [points de terminaison de CDN](cdn-create-new-endpoint.md) renvoyant des erreurs 404.

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Get Support**.

## <a name="symptom"></a>Symptôme
Vous avez créé un profil CDN et un point de terminaison, mais votre contenu ne semble pas toobe disponible sur hello CDN.  Utilisateurs qui tentent de tooaccess votre contenu via hello URL du CDN recevoir les codes d’état HTTP 404. 

## <a name="cause"></a>Cause :
Il existe plusieurs causes possibles, y compris :

* origine du fichier Hello n’est pas visible toohello CDN
* point de terminaison Hello est mal configuré, à l’origine de hello CDN toolook dans un emplacement erroné hello
* hôte de Hello rejette les en-tête de l’hôte à partir de hello CDN hello
* point de terminaison Hello n’a encore été toopropagate temps tout au long de hello CDN

## <a name="troubleshooting-steps"></a>Étapes de dépannage
> [!IMPORTANT]
> Après avoir créé un point de terminaison CDN, elle pas seront immédiatement disponible pour l’utilisation, comme le temps requis pour toopropagate d’inscription hello via hello CDN.  Pour les profils du <b>CDN Azure fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.  Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.  Si vous effectuez les étapes hello dans ce document et que vous vous continuez à obtenir des 404 réponses, attendez quelques heures toocheck avant d’ouvrir un ticket de support.
> 
> 

### <a name="check-hello-origin-file"></a>Vérifiez le fichier d’origine hello
Tout d’abord, nous devons vérifier hello ce fichier hello nous souhaitons mis en cache est disponible sur notre origine et est accessible publiquement.  Hello toodo moyen le plus rapide qui est tooopen un navigateur dans une session en privé ou Incognito, puis accédez directement toohello fichier.  Simplement taper ou coller l’URL de hello dans la zone d’adresse hello et de voir si qui résulte dans le fichier hello souhaitées.  Pour cet exemple, je vais toouse un fichier dans un compte de stockage Azure, accessible à `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Comme vous pouvez le voir, il réussit les tests hello.

![C’est terminé !](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Alors que cela est plus rapide de hello et tooverify de façon plus simple de votre fichier est disponible publiquement, certaines configurations de réseau de votre organisation pourrait donner vous hello illusion que ce fichier est publiquement disponible lorsqu’il est en fait, uniquement visible toousers de votre réseau) même si elle est hébergée dans Azure).  Si vous avez un navigateur externe à partir de laquelle vous pouvez tester, par exemple un périphérique mobile qui n’est pas connecté de réseau de l’organisation tooyour ou une machine virtuelle dans Azure, qui serait préférable.
> 
> 

### <a name="check-hello-origin-settings"></a>Vérifiez les paramètres d’origine hello
Maintenant que nous avons vérifié le fichier de hello est publiquement disponible sur internet de hello, nous devons vérifier les paramètres d’origine.  Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN tooyour et cliquez sur le point de terminaison hello vous effectuez un dépannage.  Hello résultant **point de terminaison** panneau, cliquez sur hello origine.  

![Panneau Point de terminaison avec origine mise en surbrillance](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Hello **origine** panneau s’affiche. 

![Panneau Origine](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Type et nom d’hôte de l’origine
Vérifiez que hello **type d’origine** est correct et vérifiez hello **nom d’hôte d’origine**.  Dans mon exemple, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, partie du nom d’hôte hello Hello URL est `cdndocdemo.blob.core.windows.net`.  Comme vous pouvez le voir dans la capture d’écran de hello, c’est exact.  Pour le stockage Azure, application Web et les origines de Service Cloud, hello **nom d’hôte d’origine** champ est une liste déroulante, nous n’avez pas besoin tooworry sur est correctement orthographié.  Toutefois, si vous utilisez une origine personnalisée, il est *absolument essentiel* d’orthographier correctement votre nom d’hôte.

#### <a name="http-and-https-ports"></a>Ports HTTP et HTTPS
Bonjour autres toocheck chose ici est votre **HTTP** et **ports HTTPS**.  Dans la plupart des cas, les ports 80 et 443 sont corrects, et aucune modification n’est nécessaire.  Toutefois, si le serveur d’origine hello est à l’écoute sur un port différent, que devez toobe représentée ici.  Si vous n’êtes pas sûr, il suffit de considérer URL hello pour votre fichier d’origine.  Hello HTTP et les spécifications du protocole HTTPS spécifient les ports 80 et 443 comme valeurs par défaut hello. Dans mon URL, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, un port n’est pas spécifié, donc hello comme valeur par défaut 443 est supposé et mes paramètres sont corrects.  

Toutefois, par exemple hello URL pour votre fichier d’origine que vous avez testé précédemment est `http://www.contoso.com:8080/file.txt`.  Hello de note `:8080` à fin hello du segment de nom d’hôte hello.  Qui indique le port de hello navigateur toouse `8080` tooconnect toohello serveur web `www.contoso.com`, et vous devrez donc tooenter 8080 Bonjour **port HTTP** champ.  Il est important toonote que ces paramètres de port affectent uniquement le point de terminaison hello port utilise les informations de tooretrieve à partir de l’origine de hello.

> [!NOTE]
> **CDN Azure à partir d’Akamai** points de terminaison n’autorisent pas de plage de ports TCP complète hello pour les origines.  Pour obtenir la liste des ports d’origine non autorisés, consultez l’article [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Ports d’origine autorisés du CDN Azure fourni par Akamai).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Vérifiez les paramètres de point de terminaison hello
Retour sur hello **point de terminaison** panneau, cliquez sur hello **configurer** bouton.

![Panneau Point de terminaison avec bouton Configurer mis en surbrillance](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Hello du point de terminaison **configurer** panneau s’affiche.

![Panneau Configurer](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocoles
Pour **protocoles**, vérifiez que le protocole hello utilisé par les clients de hello est sélectionné.  Hello même protocole utilisé par le client de hello sera hello une utilisé origine tooaccess hello est ports d’origine hello toohave important correctement configurés dans la section précédente de hello.  point de terminaison Hello n’écoute que sur hello par défaut ports HTTP et HTTPS (80 et 443), indépendamment des ports d’origine hello.

Revenons exemple hypothétique de tooour avec `http://www.contoso.com:8080/file.txt`.  Vous savez que Contoso a spécifié `8080` comme port HTTP. Cependant, supposons qu’il a aussi spécifié `44300` comme port HTTPS.  S’il avait créé un point de terminaison nommé `contoso`, le nom d’hôte du point de terminaison de son CDN serait `contoso.azureedge.net`.  Une demande de `http://contoso.azureedge.net/file.txt` est une demande HTTP, point de terminaison hello utiliserait HTTP sur le port 8080 tooretrieve à partir de l’origine de hello.  Une demande sécurisée via HTTPS, `https://contoso.azureedge.net/file.txt`, provoquerait hello toouse de point de terminaison HTTPS sur le port 44300 lorsque élaborer hello fichier à partir de l’origine de hello.

#### <a name="origin-host-header"></a>En-tête de l’hôte d’origine
Hello **en-tête hôte d’origine** est la valeur d’en-tête hôte hello envoyé origine toohello avec chaque demande.  Dans la plupart des cas, cela doit être hello même comme hello **nom d’hôte d’origine** nous avons vérifié précédemment.  Une valeur incorrecte dans ce champ ne provoque généralement 404 États, mais qu’il est probable toocause autres États 4xx, selon l’origine hello attend.

#### <a name="origin-path"></a>Chemin d’accès d’origine
Enfin, nous devons vérifier le champ **Chemin d’accès d’origine**,  qui est vide par défaut.  Vous devez uniquement utiliser ce champ si vous souhaitez que toonarrow hello étendue des ressources d’origine hébergé hello souhaité toomake disponible sur hello CDN.  

Par exemple, dans mon point de terminaison, j’aimerais toutes les ressources sur mon toobe de compte de stockage disponible, donc je laissé **chemin d’origine** vide.  Cela signifie qu’une demande trop`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` entraîne une connexion à partir de mon point de terminaison trop`cdndocdemo.core.windows.net` que les demandes `/publicblob/lorem.txt`.  De même, une demande de `https://cdndocdemo.azureedge.net/donotcache/status.png` entraîne la demande de point de terminaison hello `/donotcache/status.png` à partir de l’origine de hello.

Mais que se passe-t-il si je ne veux pas toouse hello CDN pour chaque chemin d’accès sur mon origine ?  Supposons que je souhaitais seulement tooexpose hello `publicblob` chemin d’accès.  Si vous entrez */publicblob* dans mon **chemin d’origine** champ, ce qui entraîne la tooinsert de point de terminaison hello */publicblob* avant chaque demande effectuée toohello origine.  Cela signifie que cette demande hello pour `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` prendra désormais réellement partie de demande hello de hello URL, `/publicblob/lorem.txt`et ajoutez `/publicblob` toohello début. Il en résulte dans une demande de `/publicblob/publicblob/lorem.txt` à partir de l’origine de hello.  Si le fichier tooan ne résout pas ce chemin d’accès, origine de hello retourne un état 404.  Hello lorem.txt tooretrieve URL correcte dans cet exemple serait réellement `https://cdndocdemo.azureedge.net/lorem.txt`.  Notez que nous n’inclure hello */publicblob* chemin d’accès, car la partie de demande hello de hello URL est `/lorem.txt` et le point de terminaison hello ajoute `/publicblob`, se traduisant par `/publicblob/lorem.txt` demande de hello transmises toohello origine .

