---
title: "domaine personnalisé du contenu tooa Azure CDN aaaMap | Documents Microsoft"
description: "Découvrez comment toomap Azure CDN contenu tooa des domaines personnalisés."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Mapper un domaine personnalisé de tooa contenu CDN Azure
Vous pouvez mapper un point de terminaison CDN de tooa domaine personnalisé dans l’ordre toouse votre propre nom de domaine dans l’URL toocached de contenu au lieu d’utiliser un sous-domaine de azureedge.net.

Il existe deux façons toomap votre point de terminaison CDN tooa domaine personnalisé :

1. [Créer un enregistrement CNAME avec votre bureau d’enregistrement de domaine et mapper votre domaine et sous-domaine toohello CDN point de terminaison personnalisé](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Un enregistrement CNAME est une fonctionnalité DNS qui mappe un domaine source, tel que `www.contosocdn.com` ou `cdn.contoso.com`, domaine de destination tooa. Dans ce cas, le domaine de la source hello est votre domaine personnalisé et votre sous-domaine (un sous-domaine, comme **www** ou **cdn** est toujours requis). domaine de destination Hello est votre point de terminaison CDN.  
   
    processus Hello de mappage de votre point de terminaison CDN tooyour domaine personnalisé peut, cependant, provoquer dans une courte période de temps d’arrêt pour le domaine de hello pendant l’inscription de domaine de hello Bonjour portail Azure.
2. [Ajouter une étape d’inscription intermédiaire avec **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Si votre domaine personnalisé d’est actuellement prise en charge une application avec un contrat de niveau de service (SLA) qui nécessite la présence d’aucun temps d’interruption, vous pouvez ensuite utiliser hello Azure **cdnverify** sous-domaine tooprovide une inscription intermédiaire étape afin que les utilisateurs seront en mesure de tooaccess votre domaine pendant que hello DNS mappage a lieu.  

Après avoir enregistré votre domaine personnalisé à l’aide de hello au-dessus de procédures, vous devez trop[vérifier ce sous-domaine personnalisé hello référence votre point de terminaison CDN](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Vous devez créer un enregistrement CNAME avec votre toomap de bureau d’enregistrement de domaine de votre point de terminaison CDN toohello domaine. Les enregistrements CNAME mappent des sous-domaines spécifiques, tels que `www.contoso.com` ou `cdn.contoso.com`. Il n’est pas possible de toomap un domaine racine de tooa enregistrement CNAME, tel que `contoso.com`.
> 
> Un sous-domaine ne peut être associé qu'à un point de terminaison CDN. Hello enregistrement CNAME que vous créez achemine tout le trafic adressé toohello sous-domaine toohello spécifié de point de terminaison.  Par exemple, si vous associez `www.contoso.com` à votre point de terminaison CDN, vous ne pouvez pas l’associer à d’autres points de terminaison Azure, comme un point de terminaison de compte de stockage ou un point de terminaison de service cloud. Toutefois, vous pouvez utiliser différents sous-domaines de hello même domaine pour les points de terminaison de service différent. Vous pouvez également mapper différents sous-domaines toohello même point de terminaison CDN.
> 
> Pour **Azure CDN de Verizon** les points de terminaison (Standard ou Premium), notez qu’elle occupe trop**90 minutes** des noeuds tooCDN toopropagate des modifications de domaine personnalisé.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Inscrire un domaine personnalisé pour un point de terminaison CDN Azure
1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).
2. Cliquez sur **Parcourir**, puis **CDN profils**, puis hello profil CDN avec point de terminaison hello vous souhaitez que le domaine personnalisé de toomap tooa.  
3. Bonjour **profil CDN** panneau, cliquez sur le point de terminaison CDN hello avec lequel vous souhaitez que le sous-domaine de hello tooassociate.
4. Haut hello du Panneau de point de terminaison hello, cliquez sur hello **ajouter un domaine personnalisé** bouton.  Bonjour **ajouter un domaine personnalisé** panneau, vous verrez les nom d’hôte de point de terminaison hello, dérivée de point de terminaison CDN, toouse dans la création d’un enregistrement CNAME. format Hello d’adresse de nom d’hôte hello apparaît sous la forme  **&lt;EndpointName >. azureedge.net**.  Vous pouvez copier cette toouse de nom d’hôte pour la création d’enregistrement CNAME de hello.  
5. Parcourir le site web de tooyour de domaines et recherchez la section hello pour la création d’enregistrements DNS. Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.
6. Rechercher la section de hello pour la gestion des enregistrements CNAME. Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello CNAME, Alias ou sous-domaines.
7. Créez un enregistrement CNAME qui mappe votre sous-domaine choisi (par exemple, **www** ou **cdn**) toohello nom d’hôte fourni dans hello **ajouter un domaine personnalisé** panneau. 
8. Retourner toohello **ajouter un domaine personnalisé** panneau, puis entrez votre domaine personnalisé, y compris les sous-domaine hello, dans la boîte de dialogue hello. Par exemple, entrez le nom de domaine hello au format de hello `www.contoso.com` ou `cdn.contoso.com`.   
   
   Azure vérifiera que l’enregistrement CNAME de hello existe pour le nom de domaine hello que vous avez entré. Si hello CNAME est correct, votre domaine personnalisé est validé.  Pour **Azure CDN de Verizon** les points de terminaison (Standard ou Premium), cela peut prendre jusqu'à minutes too90 pour le domaine personnalisé paramètres toopropagate tooall CDN noeuds, toutefois.  
   
   Notez que, dans certains cas, il peut prendre le temps pour les serveurs de tooname toopropagate enregistrement hello CNAME sur hello Internet. Si votre domaine n’est pas validé immédiatement, et si vous pensez hello enregistrement CNAME est correct, puis attendez quelques minutes, puis réessayez.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Inscrire un domaine personnalisé pour un point de terminaison CDN Azure à l’aide du sous-domaine cdnverify intermédiaire de hello
1. Ouvrez une session sur hello [Azure Portal](https://portal.azure.com/).
2. Cliquez sur **Parcourir**, puis **CDN profils**, puis hello profil CDN avec point de terminaison hello vous souhaitez que le domaine personnalisé de toomap tooa.  
3. Bonjour **profil CDN** panneau, cliquez sur le point de terminaison CDN hello avec lequel vous souhaitez que le sous-domaine de hello tooassociate.
4. Haut hello du Panneau de point de terminaison hello, cliquez sur hello **ajouter un domaine personnalisé** bouton.  Bonjour **ajouter un domaine personnalisé** panneau, vous verrez les nom d’hôte de point de terminaison hello, dérivée de point de terminaison CDN, toouse dans la création d’un enregistrement CNAME. format Hello d’adresse de nom d’hôte hello apparaît sous la forme  **&lt;EndpointName >. azureedge.net**.  Vous pouvez copier cette toouse de nom d’hôte pour la création d’enregistrement CNAME de hello.
5. Parcourir le site web de tooyour de domaines et recherchez la section hello pour la création d’enregistrements DNS. Vous pourrez trouver ces informations dans une section telle que **Domain Name**, **DNS** ou **Name Server Management**.
6. Rechercher la section de hello pour la gestion des enregistrements CNAME. Vous pouvez posséder de page de paramètres avancés de tooan toogo et recherchez les mots hello **CNAME**, **Alias**, ou **sous-domaines**.
7. Créez un enregistrement CNAME et fournir un alias de sous-domaine qui inclut hello **cdnverify** sous-domaine. Par exemple, sous-domaine hello que vous spécifiez sera au format de hello **cdnverify.www** ou **cdnverify.cdn**. Puis indiquez le nom d’hôte hello, qui est votre point de terminaison CDN, au format de hello **cdnverify.&lt; EndpointName >. azureedge.net**. Votre mappage DNS doit ressembler à ceci :`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Retourner toohello **ajouter un domaine personnalisé** panneau, puis entrez votre domaine personnalisé, y compris les sous-domaine hello, dans la boîte de dialogue hello. Par exemple, entrez le nom de domaine hello au format de hello `www.contoso.com` ou `cdn.contoso.com`. Notez que dans cette étape, vous ne devez pas sous-domaine de hello toopreface avec **cdnverify**.  
   
    Azure vérifiera que l’enregistrement CNAME de hello existe pour le nom de domaine hello cdnverify que vous avez entré.
9. À ce stade, votre domaine personnalisé a été vérifié par Azure, mais le domaine tooyour du trafic n’est pas encore en cours routé tooyour point de terminaison CDN. Après avoir attendu suffisamment longue toopropagate de paramètres de domaine personnalisé hello tooallow toohello CDN bord nœuds (90 minutes **Azure CDN de Verizon**, 1 à 2 minutes pour **CDN Azure à partir d’Akamai**), retourner tooyour DNS site web de bureau d’enregistrement et de créer un autre enregistrement CNAME qui mappe votre point de terminaison CDN tooyour sous-domaine. Par exemple, spécifiez le sous-domaine hello en tant que **www** ou **cdn**, et hello nom d’hôte en tant que  **&lt;EndpointName >. azureedge.net**. Cette étape, hello l’inscription de votre domaine personnalisé est terminée.
10. Enfin, vous pouvez supprimer l’enregistrement CNAME de hello vous avez créé à l’aide de **cdnverify**, tel qu’il était nécessaire uniquement comme une étape intermédiaire.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Vérifiez ce sous-domaine personnalisé hello fait référence à votre point de terminaison CDN
* Une fois que vous avez terminé l’inscription de hello de votre domaine personnalisé, vous pouvez accéder au contenu est mis en cache au point de terminaison CDN à l’aide du domaine personnalisé de hello.
  Tout d’abord, assurez-vous que vous disposez d’un contenu public qui est mis en cache au point de terminaison hello. Par exemple, si votre point de terminaison CDN est associé à un compte de stockage, hello CDN met en cache le contenu dans des conteneurs blob publics. domaine personnalisé de hello tootest, assurez-vous que votre conteneur est tooallow un accès public et qu’il contient au moins un objet blob.
* Dans votre navigateur, accédez à adresse toohello du blob hello hello de domaine personnalisé. Par exemple, si votre domaine personnalisé est `cdn.contoso.com`, objet blob mis en cache de hello URL tooa sera similaire toohello suivant l’URL : http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Voir aussi
[Comment tooEnable hello réseau CDN (Content Delivery) pour Azure](cdn-create-new-endpoint.md)  

