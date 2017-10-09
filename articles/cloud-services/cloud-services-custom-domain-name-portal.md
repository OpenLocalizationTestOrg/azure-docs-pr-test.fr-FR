---
title: "aaaConfigure un nom de domaine personnalisé dans les Services de cloud computing | Documents Microsoft"
description: "Découvrez comment tooexpose votre toohello de données d’application ou Azure internet sur un domaine personnalisé en configurant les paramètres DNS.  Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configuration d’un nom de domaine personnalisé pour un service cloud Azure
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-custom-domain-name-portal.md)
> * [portail Azure Classic](cloud-services-custom-domain-name.md)
> 
> 

Lorsque vous créez un Service Cloud, Azure affecte sous-domaine tooa de **cloudapp.net**. Par exemple, si votre Service Cloud est nommé « contoso », vos utilisateurs seront être en mesure de tooaccess votre application sur une URL telle que http://contoso.cloudapp.net. Azure attribue également une adresse IP virtuelle.

Toutefois, vous pouvez également exposer votre application sur votre propre nom de domaine, par exemple, **contoso.com**. Cet article explique comment tooreserve ou configurer un nom de domaine personnalisé pour les rôles web de Service Cloud.

Vous avez compris ce que sont les enregistrements CNAME et A ? [Saut au-delà de hello explication](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> les procédures de Hello dans cette tâche s’appliquent à des Services de cloud computing tooAzure. Pour App Services, consultez [cette page](../app-service-web/web-sites-custom-domain-name.md). Pour les comptes de stockage, consultez [cette page](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Familiarisez-vous rapidement--utilisez hello Azure nouveau [guidée procédure pas à pas](http://support.microsoft.com/kb/2990804)!  Grâce à elle, l'association d'un nom de domaine personnalisé ET la sécurisation de la communication (SSL) avec les services cloud Azure ou les sites Web Azure deviennent un jeu d'enfants.
> 
> 

## <a name="understand-cname-and-a-records"></a>Présentation des enregistrements CNAME et A
CNAME (ou les enregistrements d’alias) et un enregistrement à la fois vous permettre de tooassociate un nom de domaine à un serveur spécifique (ou de service dans ce cas,) toutefois ils fonctionnent différemment. Il existe également certaines considérations spécifiques lors de l’utilisation d’un enregistrement avec les services de cloud computing de Azure dont vous devez tenir compte avant de décider quels toouse.

### <a name="cname-or-alias-record"></a>Enregistrement CNAME ou d'alias
Un enregistrement CNAME associe un *spécifique* domaine, tel que **contoso.com** ou **www.contoso.com**, nom de domaine canonique tooa. Dans ce cas, le nom de domaine canonique hello est hello **[myapp] .cloudapp .net** nom de domaine de votre Azure hébergé l’application. Une fois créé, hello CNAME crée un alias pour hello **[myapp] .cloudapp .net**. Hello entrée CNAME peut résoudre l’adresse IP de toohello de votre **[myapp] .cloudapp .net** service automatiquement, donc si l’adresse IP de hello du service de cloud hello change, vous n’avez pas n’importe quelle action aux tootake.

> [!NOTE]
> Des bureaux d’enregistrement de domaine vous permettre uniquement de sous-domaines de toomap lors de l’utilisation d’un enregistrement CNAME, tels que www.contoso.com et non les noms de racine, par exemple, contoso.com. Pour plus d’informations sur les enregistrements CNAME, consultez la documentation hello fournie par votre bureau d’enregistrement, [hello Wikipédia sur l’enregistrement CNAME](http://en.wikipedia.org/wiki/CNAME_record), ou hello [IETF de noms de domaine - implémentation et spécification](http://tools.ietf.org/html/rfc1035) document.
> 
> 

### <a name="a-record"></a>Enregistrement A
Un *A* enregistrement mappe à un domaine, tel que **contoso.com** ou **www.contoso.com**, *ou un domaine générique* comme  **\*. contoso.com**, adresse IP de tooan. Dans le cas de hello d’un Service Cloud Azure, hello adresse IP virtuelle du service de hello. Par conséquent, hello le principal avantage d’un enregistrement sur un enregistrement CNAME est que vous pouvez avoir une entrée qui utilise un caractère générique, tel que \* **. contoso.com**, qui serait gérer les demandes de plusieurs sous-domaines comme  **Mail.contoso.com**, **login.contoso.com**, ou **www.contso.com**.

> [!NOTE]
> Dans la mesure où un enregistrement est mappé tooa adresse IP, il ne peut pas résoudre automatiquement les modifications toohello IP adresse de votre Service Cloud. adresse IP de Hello utilisé par votre Service Cloud est allouée hello première fois que vous déployez tooan d’emplacement vide (production ou intermédiaire.) Si vous supprimez le déploiement hello pour l’emplacement de hello, adresse IP de hello est publiée par Azure et une nouvelle adresse IP peut être attribué à n’importe quel emplacement toohello de futurs déploiements.
> 
> Pour des raisons pratiques, adresse IP de hello d’un emplacement de déploiement donné (production ou intermédiaire) est conservée lorsque vous échangez entre la mise en lots et les déploiements de production ou d’effectuer une mise à niveau sur place d’un déploiement existant. Pour plus d’informations sur la réalisation de ces actions, consultez [toomanage de services cloud](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Ajout d’un enregistrement CNAME pour votre domaine personnalisé
toocreate un enregistrement CNAME, vous devez ajouter une nouvelle entrée dans la table de hello DNS pour votre domaine personnalisé à l’aide des outils hello fournies par votre bureau d’enregistrement. Chaque bureau d’enregistrement a une méthode similaire, mais légèrement différente de la spécification d’un enregistrement CNAME, mais sont des concepts de hello hello même.

1. Utilisez une de ces hello toofind de méthodes **. cloudapp.net** nom de domaine affecté tooyour le service cloud.
   
   * Connexion toohello [portail Azure], sélectionnez votre service cloud, regardez hello **Essentials** section et recherchez hello **URL du Site** entrée.
     
       ![section d’aperçu rapide montrant l’URL du site hello][csurl]
     
       **OR**
   * Installer et configurer [Azure Powershell](/powershell/azure/overview), puis utilisez hello en commande suivant :
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Enregistrez le nom de domaine hello utilisé dans les URL de hello retourné par l’autre méthode, car vous en aurez besoin lors de la création d’un enregistrement CNAME.
2. Ouvrez une session sur le site Web de tooyour DNS du bureau d’enregistrement et atteindre la page toohello de gestion DNS. Recherchez des liens ou les zones du site de hello étiquetés comme étant **nom de domaine**, **DNS**, ou **gestion des noms de serveur**.
3. Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements CNAME. Vous avez peut-être enregistrement de hello tooselect type à partir d’une liste déroulante, ou accédez tooan paramètres page Avancé. Vous devez rechercher les mots hello **CNAME**, **Alias**, ou **sous-domaines**.
4. Vous devez également fournir hello domaine ou un sous-domaine alias pour hello CNAME, tel que **www** si vous souhaitez un alias pour que toocreate **www.customdomain.com**. Si vous voulez toocreate un alias pour le domaine racine de hello, il peut être répertorié comme hello '**@**' symbole dans les outils de votre bureau d’enregistrement DNS.
5. Vous devez ensuite fournir un nom d’hôte canonique, qui correspond au domaine **cloudapp.net** de votre application dans le cas présent.

Par exemple, hello suivant l’enregistrement CNAME transmet tout le trafic à partir de **www.contoso.com** trop**contoso.cloudapp.net**, le nom de domaine personnalisé hello de votre application déployée :

| Alias/Nom d'hôte/Sous-domaine | Domaine canonique |
| --- | --- |
| www |contoso.cloudapp.net |

> [!NOTE]
> Un visiteur de **www.contoso.com** ne verrez jamais d’hôte de true hello (contoso.cloudapp.net), hello processus de transfert est invisible toothe utilisateur.
> 
> Hello exemple ci-dessus s’applique uniquement tootraffic à hello **www** sous-domaine. Puisqu'il n'est pas possible d'utiliser des caractères génériques pour les enregistrements CNAME, vous devez créer un enregistrement CNAME pour chaque domaine/sous-domaine. Si vous voulez le trafic de toodirect à partir de sous-domaines, tel que *. contoso.com, tooyour cloudapp.net adresse, vous pouvez configurer un **redirection d’URL** ou **vers l’URL avant** entrée dans vos paramètres DNS, ou créez un enregistrement A.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Ajouter un enregistrement A pour votre domaine personnalisé
toocreate un un enregistrement, vous devez tout d’abord rechercher les hello adresse IP virtuelle de votre service cloud. Puis, ajoutez une nouvelle entrée dans la table DNS hello pour votre domaine personnalisé à l’aide des outils hello fournies par votre bureau d’enregistrement. Chaque bureau d’enregistrement a une méthode similaire, mais légèrement différente de la spécification d’un enregistrement A, mais sont des concepts de hello hello même.

1. Utilisez une des hello suit méthodes tooget hello IP adresse de votre service cloud.
   
   * Connexion toohello [portail Azure], sélectionnez votre service cloud, regardez hello **Essentials** section et recherchez hello **des adresses IP publiques** entrée.
     
       ![section d’aperçu rapide montrant les adresses IP virtuelles hello][vip]
     
       **OR**
   * Installer et configurer [Azure Powershell](/powershell/azure/overview), puis utilisez hello en commande suivant :
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Enregistrer l’adresse IP de hello, car vous en aurez besoin lors de la création d’un enregistrement A.
2. Ouvrez une session sur le site Web de tooyour DNS du bureau d’enregistrement et atteindre la page toohello de gestion DNS. Recherchez des liens ou les zones du site de hello étiquetés comme étant **nom de domaine**, **DNS**, ou **gestion des noms de serveur**.
3. Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements A. Vous avez peut-être enregistrement de hello tooselect type à partir d’une liste déroulante, ou accédez tooan paramètres page Avancé.
4. Sélectionnez ou entrez le domaine de hello ou un sous-domaine qui utilise cet enregistrement A. Par exemple, sélectionnez **www** si vous souhaitez un alias pour que toocreate **www.customdomain.com**. Si vous voulez toocreate une entrée de caractère générique pour tous les sous-domaines, entrez « ***'. Cela permet de couvrir tous les sous-domaines tels que **mail.domainepersonnalisé.com**, **login.domainepersonnalisé.com** et **www.domainepersonnalisé.com**.
   
    Si vous voulez toocreate un un enregistrement pour le domaine racine de hello, il peut être répertorié comme hello '**@**' symbole dans les outils de votre bureau d’enregistrement DNS.
5. Entrez les adresse hello de votre service cloud dans hello fourni le champ. Cela associe entrée de domaine hello utilisée dans l’enregistrement A de hello avec l’adresse IP de hello de déploiement de votre service cloud.

Par exemple, hello suivant un enregistrement transmet tout le trafic à partir de **contoso.com** trop**137.135.70.239**, hello d’adresse IP de votre application déployée :

| Nom d'hôte/Sous domaine | Adresse IP |
| --- | --- |
| @ |137.135.70.239 |

Cet exemple illustre la création d’un enregistrement A pour le domaine racine de hello. Si vous le souhaitez toocreate un toocover d’entrée générique tous les sous-domaines, vous devez entrer « ***' en tant que sous-domaine de hello.

> [!WARNING]
> Les adresses IP dans Azure sont dynamiques par défaut. Vous aurez probablement besoin de toouse un [adresses IP réservées](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure votre adresse IP ne change pas.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Comment les Services de cloud computing tooManage](cloud-services-how-to-manage.md)
* [Comment tooa de contenu CDN tooMap un domaine personnalisé](../cdn/cdn-map-content-to-custom-domain.md)
* [Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portail Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
