---
title: aaaAzure Forum aux questions de la gestion des API | Documents Microsoft
description: "Découvrez les réponses hello toocommon questions, les modèles et les meilleures pratiques de gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>FAQ sur la gestion des API Azure
Obtenir les questions de toocommon réponses hello, modèles et meilleures pratiques pour la gestion des API Azure.

## <a name="contact-us"></a>Nous contacter
* [Comment puis-je poser équipe de gestion des API Microsoft Azure hello en une question ?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Forum Aux Questions
* [Qu’est-ce que cela signifie lorsqu’une fonctionnalité est disponible en version préliminaire ?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Comment puis-je sécuriser connexion hello entre la passerelle de gestion des API hello et Mes services principaux ?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Comment copier les mon instance tooa nouvelle instance du service Gestion des API ?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [Puis-je gérer mon instance de gestion des API par programme ?](#can-i-manage-my-api-management-instance-programmatically)
* [Comment pour ajouter un groupe d’administrateurs utilisateurs toohello ?](#how-do-i-add-a-user-to-the-administrators-group)
* [Pourquoi est-stratégie hello que je veux tooadd non disponible dans l’éditeur de stratégie hello ?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Comment utiliser le contrôle de version d’API dans Gestion des API ?](#how-do-i-use-api-versioning-in-api-management)
* [Comment configurer plusieurs environnements dans une seule API ?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [Puis-je utiliser SOAP avec le service Gestion des API ?](#can-i-use-soap-with-api-management)
* [Est la constante de hello gestion des API passerelle IP adresse ? Puis-je l’utiliser dans les règles de pare-feu ?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Puis-je configurer un serveur d’autorisation OAuth 2.0 avec la sécurité AD FS ?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Quelle méthode de routage utiliser Gestion des API dans les emplacements géographiques de déploiements toomultiple ?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Puis-je utiliser un toocreate de modèle une instance de service de gestion des API Azure Resource Manager ?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Puis-je utiliser un certificat SSL auto-signé pour un service principal ?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Je reçois un échec d’authentification lors de le tooclone un référentiel GIT ?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Le service Gestion des API est-il compatible avec Azure ExpressRoute ?](#does-api-management-work-with-azure-expressroute)
* [Pourquoi exigeons-nous un sous-réseau dédié dans les réseaux virtuels de type Resource Manager lorsque le service Gestion des API est déployé dans ceux-ci ?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Quelle est la taille de sous-réseau minimale hello nécessaire lors du déploiement de gestion des API dans un réseau virtuel ?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Puis-je déplacer un service de gestion des API à partir d’un abonnement tooanother ?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Existe-t-il des restrictions ou des problèmes connus liés à l’importation de mon API ?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Comment puis-je poser équipe de gestion des API Microsoft Azure hello en une question ?
Vous pouvez nous contacter de l’une des façons suivantes :

* Publiez vos questions sur notre [forum MSDN de gestion des API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Envoyer un courrier électronique trop<mailto:apimgmt@microsoft.com>.
* Nous envoyer une demande de fonctionnalité Bonjour [forum de commentaires Azure](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Qu’est-ce que cela signifie lorsqu’une fonctionnalité est disponible en version préliminaire ?
Lorsqu’une fonctionnalité est en version préliminaire, cela signifie que nous avons activement à la recherche des commentaires sur le fonctionne de la fonctionnalité de hello pour vous. Une fonctionnalité en version préliminaire est fonctionnellement complet, mais il est possible que nous allons effectuer un saut de modifier vos commentaires toocustomer de réponse. Nous vous recommandons de ne pas intégrer de manière définitive une fonctionnalité en version préliminaire à votre environnement de production. Si vous avez des commentaires sur les fonctionnalités en version préliminaire, faites-le nous savoir via une des options de contact hello dans [comment puis-je poser équipe de gestion des API Microsoft Azure hello une question ?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Comment puis-je sécuriser connexion hello entre la passerelle de gestion des API hello et Mes services principaux ?
Vous avez plusieurs connexions de hello toosecure options entre la passerelle de gestion des API hello et vos services principaux. Vous pouvez :

* Utilisez l’authentification HTTP de base. Pour plus d’informations, consultez [Configuration des paramètres de l’API](api-management-howto-create-apis.md#configure-api-settings).
* Utilisez l’authentification mutuelle SSL, comme décrit dans [comment toosecure principaux services à l’aide de l’authentification du certificat client dans Gestion des API Azure](api-management-howto-mutual-certificates.md).
* Utiliser une liste blanche des adresses IP sur votre service principal. Si vous avez une instance de gestion des API de niveau Standard ou Premium, l’adresse IP de hello de passerelle de hello reste constante. Vous pouvez définir votre tooallow d’autorisation de cette adresse IP. Vous pouvez obtenir hello adresseIP de votre instance de la gestion des API sur hello du tableau de bord Bonjour portail Azure.
* Connectez votre tooan d’instance gestion des API réseau virtuel Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Comment copier les mon instance tooa nouvelle instance du service Gestion des API ?
Vous disposez de plusieurs options si vous souhaitez toocopy une gestion des API instance tooa nouvelle instance. Vous pouvez :

* Utilisez hello sauvegarde et restauration de la fonction Gestion des API. Pour plus d’informations, consultez [la récupération d’urgence de tooimplement à l’aide de service de sauvegarde et la restauration dans la gestion des API Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Créer votre propre sauvegarde et restauration à l’aide de hello [API REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Utilisez toosave d’API REST hello et de restauration des entités de hello à partir de l’instance de service hello que vous souhaitez.
* Télécharger la configuration du service hello à l’aide de Git, puis le télécharger tooa une nouvelle instance. Pour plus d’informations, consultez [comment toosave et configurer la configuration de votre service de gestion des API à l’aide de Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>Puis-je gérer mon instance de gestion des API par programme ?
Oui, vous pouvez gérer le service Gestion des API par programme en utilisant :

* Hello [API REST de gestion des API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Hello [SDK du Service gestion de bibliothèque Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Hello [déploiement de Service](https://msdn.microsoft.com/library/mt619282.aspx) et [gestion des services](https://msdn.microsoft.com/library/mt613507.aspx) applets de commande PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Comment pour ajouter un groupe d’administrateurs utilisateurs toohello ?
Voici comment vous pouvez ajouter un groupe d’administrateurs toohello utilisateur :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Atteindre le groupe de ressources toohello a hello gestion des API instance de tooupdate.
3. Dans Gestion des API, attribuez hello **Api gestion collaborateur** utilisateur toohello de rôle.

Maintenant hello récemment ajouté collaborateurs peuvent utiliser Azure PowerShell [applets de commande](https://msdn.microsoft.com/library/mt613507.aspx). Voici comment toosign dans en tant qu’administrateur :

1. Hello d’utilisation `Login-AzureRmAccount` toosign d’applet de commande dans.
2. Définissez hello contexte toohello abonnement qui a un service de hello en utilisant `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Obtenez une URL d’authentification unique à l’aide de `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Utilisez le portail d’administration hello URL tooaccess hello.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Pourquoi est-stratégie hello que je veux tooadd non disponible dans l’éditeur de stratégie hello ?
Si hello stratégie tooadd apparaît estompée ou ombrés dans l’éditeur de stratégie de hello, veillez à ce que vous êtes dans la portée appropriée de hello pour la stratégie de hello. Chaque instruction de stratégie est conçue pour vous toouse dans les sections de la stratégie et les étendues spécifiques. sections de stratégie tooreview hello et étendues pour une stratégie, consultez Utilisation de la stratégie hello section [des stratégies de gestion des API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Comment utiliser le contrôle de version d’API dans Gestion des API ?
Vous avez plusieurs options toouse API le contrôle de version dans la gestion des API :

* Gestion des API, vous pouvez configurer des versions différentes API toorepresent. Par exemple, vous pouvez avoir deux API différentes, MonAPIv1 et MonAPIv2. Un développeur peut choisir la version de hello hello développeur souhaite toouse.
* Vous pouvez également configurer votre API avec une URL de service qui n’inclut pas un segment de version, par exemple https://mon.api. Ensuite, configurez un segment de version pour chaque modèle de [réécriture de l’URL](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL). Par exemple, vous pouvez avoir une opération avec un [modèle d’URL](api-management-howto-add-operations.md#url-template) appelé /resource et un modèle de [réécriture de l’URL](api-management-howto-add-operations.md#rewrite-url-template) appelé /v1/Resource. Vous pouvez modifier la valeur de segment hello version séparément pour chaque opération.
* Si vous souhaitez que tookeep un segment de la version « default » dans l’URL de service hello d’API, sur les opérations sélectionnées, définie une stratégie qui utilise hello [définir le service principal](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) le chemin d’accès de stratégie toochange hello demande du serveur principal.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Comment configurer plusieurs environnements dans une seule API ?
tooset plusieurs environnements, par exemple, un environnement de test et un environnement de production dans une seule API, vous avez deux options. Vous pouvez :

* Hôte de différentes API sur hello même client.
* Hôte hello les mêmes API sur plusieurs clients.

### <a name="can-i-use-soap-with-api-management"></a>Puis-je utiliser SOAP avec le service Gestion des API ?
Les [requêtes SOAP directes](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) sont désormais prises en charge. Les administrateurs peuvent importer hello WSDL de leur service SOAP et gestion des API Azure crée un serveur frontal SOAP. Une documentation relative au portail des développeurs, une console de test, des stratégies et des outils d’analyse sont disponibles pour les services SOAP.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>Est la constante de hello gestion des API passerelle IP adresse ? Puis-je l’utiliser dans les règles de pare-feu ?
À des niveaux Standard et Premium de hello, les hello adresse IP publique (VIP) du client de gestion des API hello est statique pour la durée de vie hello du client de hello, à quelques exceptions près. changements d’adresses IP Hello dans ces conditions :

* service de Hello est supprimée et recréée puis.
* abonnement au service Hello est [suspendu](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) ou [averti](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (par exemple, pour nonpayment) et puis relancé.
* Vous ajoutez ou supprimez le réseau virtuel Azure (vous pouvez utiliser de réseau virtuel au moment hello développeur et de niveau Premium uniquement).

Pour les déploiements de plusieurs régions, hello adresse régionaux change si la région de hello est libérée et puis relancée (vous pouvez utiliser plusieurs région déploiement uniquement au niveau Premium de hello).

Les clients du niveau Premium configurés pour un déploiement multirégion se voient attribués une seule adresse IP publique par région.

Dans page hello client hello portail Azure, vous pouvez obtenir votre adresse IP (ou les adresses, dans un déploiement de plusieurs région).

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Puis-je configurer un serveur d’autorisation OAuth 2.0 avec la sécurité AD FS ?
toolearn tooconfigure un serveur d’autorisation OAuth 2.0 avec la sécurité des Services de fédération Active Directory (AD FS), voir [à l’aide d’ADFS dans Gestion des API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Quelle méthode de routage utiliser Gestion des API dans les emplacements géographiques de déploiements toomultiple ?
Gestion des API utilise hello [méthode de routage du trafic performances](../traffic-manager/traffic-manager-routing-methods.md#priority) dans des emplacements géographiques déploiements toomultiple. Le trafic entrant est routé toohello les passerelle API le plus proche. Si une région est mis hors connexion, le trafic entrant est routé automatiquement toohello passerelle le plus proche suivant. Pour en savoir plus sur les méthodes de routage, consultez [Méthodes de routage de Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Puis-je utiliser un toocreate de modèle une instance de service de gestion des API Azure Resource Manager ?
Oui. Consultez hello [Service de gestion des API Azure](http://aka.ms/apimtemplate) modèles de démarrage rapide.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Puis-je utiliser un certificat SSL auto-signé pour un service principal ?
Oui. Voici comment toouse un auto-signé couche SSL (Secure Sockets) de certificat pour un serveur principal :

1. Créez une entité [Backend](https://msdn.microsoft.com/library/azure/dn935030.aspx) à l’aide du service Gestion des API.
2. Ensemble hello **skipCertificateChainValidation** propriété trop**true**.
3. Si vous ne voulez plus tooallow des certificats auto-signés, supprimer l’entité Backend de hello ou définir hello **skipCertificateChainValidation** propriété trop**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Je reçois un échec d’authentification lors de le tooclone un référentiel Git ?
Si vous utilisez le Gestionnaire d’informations d’identification Git, ou si vous essayez de tooclone un référentiel Git à l’aide de Visual Studio, vous pouvez exécuter dans un problème connu avec la boîte de dialogue informations d’identification Windows hello. boîte de dialogue Hello limite too127 caractères de longueur de mot de passe, et elle tronque le mot de passe généré par Microsoft hello. Nous travaillons sur la réduction de mot de passe hello. Pour l’instant, utilisez un interpréteur de commandes Git tooclone votre référentiel Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>Le service Gestion des API est-il compatible avec Azure ExpressRoute ?
Oui. Le service Gestion des API est compatible avec Azure ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Pourquoi exigeons-nous un sous-réseau dédié dans les réseaux virtuels de type Resource Manager lorsque le service Gestion des API est déployé dans ceux-ci ?
spécification de sous-réseau dédié Hello pour la gestion de l’API est issu de hello, qui est basé sur le modèle de déploiement classique (PAAS V1 layer). Pendant que nous pouvons déployer dans un VNET le Gestionnaire de ressources (couche V2), il n’y a des conséquences toothat. Hello modèle de déploiement classique dans Azure n’est pas fortement couplée avec le modèle de gestionnaire de ressources hello et donc si vous créez une ressource dans la couche de V2, couche de V1 hello ne connaît et problèmes peuvent se produire, telles que la gestion des API de la tentative de toouse une adresse IP qui est déjà allouée tooa (générée sous V2) de carte réseau.
toolearn plus d’informations sur la différence entre les modèles standard et le Gestionnaire de ressources dans Azure consultez trop[différence dans les modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Quelle est la taille de sous-réseau minimale hello nécessaire lors du déploiement de gestion des API dans un réseau virtuel ?
taille du sous-réseau minimale Hello nécessaire toodeploy gestion des API est [/29](../virtual-network/virtual-networks-faq.md#configuration), qui est la taille du sous-réseau minimale hello qui prend en charge de Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Puis-je déplacer un service de gestion des API à partir d’un abonnement tooanother ?
Oui. toolearn, voir [déplacer des ressources tooa nouveau groupe de ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Existe-t-il des restrictions ou des problèmes connus liés à l’importation de mon API ?
[Problèmes connus et restrictions](api-management-api-import-restrictions.md) pour les formats Open API(Swagger), WSDL et WADL.
