---
title: "Configuration d’un nom de domaine personnalisé dans Cloud Services | Microsoft Docs"
description: "Découvrez comment exposer votre application ou vos données Azure sur un domaine personnalisé en configurant les paramètres DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b61f6aad7cf974ce25baf944e342284b02ea0048
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configuration d’un nom de domaine personnalisé pour un service cloud Azure
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-custom-domain-name-portal.md)
> * [Portail Azure Classic](cloud-services-custom-domain-name.md)
> 
> 

Lorsque vous créez une service cloud, Azure l'attribue à un sous-domaine de cloudapp.net. Par exemple, si votre service cloud s’intitule « contoso », vos utilisateurs peuvent accéder à votre application par le biais d’une URL telle que http://contoso.cloudapp.net. Azure attribue également une adresse IP virtuelle.

Toutefois, vous pouvez également exposer votre application sur votre propre nom de domaine, par exemple, contoso.com. Cet article explique comment réserver ou configurer un domaine personnalisé avec des rôles Web de service cloud.

Vous avez compris ce que sont les enregistrements CNAME et A ? [Passez l’explication](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Passez à la vitesse supérieure ! Utilisation de la [procédure pas à pas](http://support.microsoft.com/kb/2990804)Azure. Grâce à elle, l'association d'un nom de domaine personnalisé et la sécurisation de la communication (SSL) avec les services cloud Azure ou les sites Web Azure deviennent un jeu d'enfants.
> 
> 

<p/>

> [!NOTE]
> Les procédures décrites dans cette tâche s’appliquent aux services cloud Azure. Pour App Services, consultez [cette page](../app-service/app-service-web-tutorial-custom-domain.md). Pour les comptes de stockage, consultez [cette page](../storage/blobs/storage-custom-domain-name.md).
> 
> 

## <a name="understand-cname-and-a-records"></a>Présentation des enregistrements CNAME et A
Bien que fonctionnant différemment, les enregistrements CNAME (ou enregistrements d’alias) et A permettent d’associer un nom de domaine avec un serveur spécifique (ou un service dans ce cas). Avant de faire votre choix, certains aspects spécifiques sont également à prendre en considération lors de l’utilisation d’enregistrements A avec les services cloud Azure.

### <a name="cname-or-alias-record"></a>Enregistrement CNAME ou d'alias
Un enregistrement CNAME associe un domaine *spécifique*, tel que **contoso.com** ou **www.contoso.com**, à un nom de domaine canonique. Dans ce cas, le nom de domaine canonique est le nom de domaine **[myapp].cloudapp.net** de votre application hébergée Azure. Une fois créé, l’enregistrement CNAME émet un alias pour **[myapp].cloudapp.net**. L’entrée CNAME devient automatiquement l’adresse IP de votre service **[myapp].cloudapp.net**. Ainsi, même si l’adresse IP du service cloud change, vous n’avez aucune action à effectuer.

> [!NOTE]
> Certains bureaux d’enregistrement de domaines autorisent le mappage de sous-domaines uniquement lorsqu’un enregistrement CNAME est utilisé (par exemple, www.contoso.com) et non un nom racine (tel que contoso.com). Pour plus d'informations sur les enregistrements CNAME, consultez la documentation fournie par votre bureau d'enregistrement, la [page Wikipédia sur l'enregistrement CNAME](http://en.wikipedia.org/wiki/CNAME_record) ou le document [Noms de domaine IETF - Implémentation et spécification](http://tools.ietf.org/html/rfc1035).
> 
> 

### <a name="a-record"></a>Enregistrement A
Un enregistrement A mappe un domaine, tel que **contoso.com** ou **www.contoso.com**, *ou un nom de domaine générique* comme **\*.contoso.com**, sur une adresse IP. Dans le cas d’un service cloud Azure, il s’agit de l’adresse IP virtuelle du service. Le principal avantage d’un enregistrement A par rapport à un enregistrement CNAME est que vous pouvez disposer d’une entrée utilisant un caractère générique (par exemple, \***.contoso.com**), ce qui permet de gérer les demandes pour plusieurs sous-domaines, tels que **mail.contoso.com**, **login.contoso.com** ou **www.contso.com**.

> [!NOTE]
> L’enregistrement A étant associé à une adresse IP statique, les changements d’adresse IP de votre service cloud ne sont donc pas pris en compte automatiquement. L’adresse IP utilisée par votre service cloud est allouée la première fois que vous effectuez un déploiement vers un emplacement vide (de production ou intermédiaire). Si vous supprimez le déploiement de l’emplacement, l’adresse IP est publiée par Azure et tout déploiement futur dans l’emplacement peut recevoir une nouvelle adresse IP.
> 
> De façon assez pratique, l’adresse IP d’un emplacement de déploiement donné (de production ou intermédiaire) est conservée lors du basculement entre les déploiements intermédiaires et de production ou lors de l’exécution de la mise à niveau sur place d’un déploiement existant. Pour plus d’informations sur ces actions, consultez la rubrique [Gestion des services cloud](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Ajout d’un enregistrement CNAME pour votre domaine personnalisé
Pour créer un enregistrement CNAME, vous devez ajouter une nouvelle entrée dans la table DNS de votre domaine personnalisé en utilisant les outils fournis par votre bureau d’enregistrement. Chaque bureau d’enregistrement possède sa propre méthode de spécification des enregistrements CNAME, même si le fonctionnement général reste souvent similaire.

1. Employez une des méthodes suivantes pour connaître le nom de domaine **.cloudapp.net** attribué à votre service cloud.
   
   * Connectez-vous au [portail Azure Classic], sélectionnez votre service cloud, sélectionnez **Tableau de bord**, puis cherchez l’entrée **URL du site** dans la section **aperçu rapide**.
     
       ![section aperçu rapide indiquant l’URL du site][csurl]
     
       **OR**  
   * Installez et configurez [Azure Powershell](/powershell/azure/overview), puis utilisez la commande suivante :
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Enregistrez le nom de domaine utilisé dans l’URL renvoyée par l’une des méthodes, car vous en aurez besoin lors de la création d’un enregistrement CNAME.
2. Connectez-vous au site web du bureau d’enregistrement de votre DNS et accédez à la page de gestion DNS. Recherchez la mention **Nom de domaine**, **DNS** ou **Gestion du nom de serveur**.
3. Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements CNAME. Il se peut que vous deviez sélectionner le type d’enregistrement dans une liste déroulante ou accéder à une page de paramètres avancés. La section recherchée doit normalement comporter les mots **CNAME**, **Alias** ou **Sous-domaines**.
4. Vous devez également fournir l’alias de domaine ou de sous-domaine pour l’enregistrement CNAME, tel que **www** si vous voulez créer un alias pour **www.domainepersonnalisé.com**. Si vous voulez créer un alias pour le domaine racine, l’entrée correspondante devrait être répertoriée avec le symbole «**@**» dans les outils DNS de votre bureau d’enregistrement.
5. Vous devez ensuite fournir un nom d’hôte canonique, qui correspond au domaine **cloudapp.net** de votre application dans le cas présent.

Par exemple, l’enregistrement CNAME suivant renvoie tout le trafic de **www.contoso.com** vers **contoso.cloudapp.net**, le nom de domaine personnalisé de votre application déployée :

| Alias/Nom d'hôte/Sous-domaine | Domaine canonique |
| --- | --- |
| www |contoso.cloudapp.net |

Un utilisateur consultant le site **www.contoso.com** ne verra jamais l’adresse de l’hôte réel (contoso.cloudapp.net). Le processus de transfert est donc invisible pour l’utilisateur final.

> [!NOTE]
> L'exemple ci-dessus s'applique uniquement au trafic du sous-domaine **www**. Puisqu'il n'est pas possible d'utiliser des caractères génériques pour les enregistrements CNAME, vous devez créer un enregistrement CNAME pour chaque domaine/sous-domaine. Pour rediriger le trafic de sous-domaines tels que \*.contoso.com vers votre adresse cloudapp.net, vous pouvez configurer une entrée de **redirection d’URL** ou de **transfert d’URL** dans vos paramètres DNS. Vous pouvez également créer un enregistrement A.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Ajouter un enregistrement A pour votre domaine personnalisé
Pour créer un enregistrement A, vous devez tout d’abord connaître l’adresse IP virtuelle de votre service cloud. Ajoutez ensuite une entrée dans la table DNS de votre domaine personnalisé à l’aide des outils fournis par votre bureau d’enregistrement. Chaque bureau d'enregistrement possède sa propre méthode de spécification des enregistrements A, même si le fonctionnement général reste souvent similaire.

1. Utilisez l’une des méthodes suivantes pour obtenir l’adresse IP de votre service cloud.
   
   * Connectez-vous au [portail Azure Classic], sélectionnez votre service cloud, sélectionnez **Tableau de bord**, puis cherchez l’entrée **Adresse IP virtuelle (VIP) publique** dans la section **aperçu rapide**.
     
       ![section aperçu rapide illustrant l’adresse IP virtuelle publique][vip]
     
       **OR**  
   * Installez et configurez [Azure Powershell](/powershell/azure/overview), puis utilisez la commande suivante :
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Si plusieurs points de terminaison sont associés à votre service cloud, vous recevrez plusieurs lignes contenant l’adresse IP, mais toutes doivent comporter la même adresse.
     
     Enregistrez l’adresse IP. Vous en aurez besoin lors de la création d’un enregistrement A.
2. Connectez-vous au site web du bureau d’enregistrement de votre DNS et accédez à la page de gestion DNS. Recherchez la mention **Nom de domaine**, **DNS** ou **Gestion du nom de serveur**.
3. Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements A. Il se peut que vous deviez sélectionner le type d'enregistrement dans une liste déroulante ou accéder à une page de paramètres avancés.
4. Sélectionnez ou entrez le domaine ou sous-domaine qui utilisera cet enregistrement A. Par exemple, sélectionnez **www** si vous souhaitez créer un alias pour **www.domainepersonnalisé.com**. Pour créer une entrée avec des caractères génériques pour l’ensemble des sous-domaines, entrez __*__. Cela permet de couvrir tous les sous-domaines tels que **mail.domainepersonnalisé.com**, **login.domainepersonnalisé.com** et **www.domainepersonnalisé.com**.
   
    Si vous voulez créer un enregistrement A pour le domaine racine, l’entrée correspondante devrait être répertoriée avec le symbole «**@**» dans les outils DNS de votre bureau d’enregistrement.
5. Entrez l’adresse IP de votre service cloud dans le champ prévu à cet effet. Cette opération permet d’associer le domaine de l’enregistrement A avec l’adresse IP de votre déploiement de service cloud.

Par exemple, l’enregistrement A suivant transfère tout le trafic de **contoso.com** vers **137.135.70.239**, l’adresse IP de votre application déployée :

| Nom d'hôte/Sous domaine | Adresse IP |
| --- | --- |
| @ |137.135.70.239 |

Cet exemple montre comment créer un enregistrement A pour le domaine racine. Pour créer une entrée avec des caractères génériques qui couvre l’ensemble des sous-domaines, entrez «__*__» comme sous-domaine.

> [!WARNING]
> Les adresses IP dans Azure sont dynamiques par défaut. Vous souhaiterez probablement utiliser une [adresse IP réservée](../virtual-network/virtual-networks-reserved-public-ip.md) pour vous assurer que votre adresse IP ne change pas.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Gestion des services cloud](cloud-services-how-to-manage.md)
* [Mappage du contenu CDN à un domaine personnalisé](../cdn/cdn-map-content-to-custom-domain.md)
* [Configuration générale de votre service cloud](cloud-services-how-to-configure.md).
* Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portail Azure Classic]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
