---
title: "aaaHow toouse gestion des API Azure avec un réseau virtuel interne | Documents Microsoft"
description: "Découvrez comment toosetup et configurer la gestion des API Azure dans un réseau virtuel interne."
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Utiliser le service Gestion des API Azure avec un réseau virtuel interne
Réseaux virtuels Azure (réseaux virtuels), gestion des API permet de gérer les API non accessibles sur Internet de hello. Un nombre de technologies VPN est des connexions de hello toomake disponibles et gestion des API peut être déployée dans deux modes principales à l’intérieur de hello réseau virtuel :
* Externe
* Interne

## <a name="overview"></a>Vue d’ensemble
Lors de la gestion des API est déployée dans un mode de réseau virtuel interne, tous les hello service points de terminaison (passerelle, portail des développeurs, portail de publication, la gestion directe et Git) sont uniquement visibles à l’intérieur d’un réseau virtuel que vous contrôlez l’accès à. Aucun des points de terminaison de service hello sont inscrits sur le serveur DNS Public de hello.

À l’aide de gestion des API en mode interne, vous pouvez obtenir hello les scénarios suivants
* Rendre les API hébergées dans votre centre de données privé accessibles de l’extérieur en toute sécurité à des tiers à l’aide de connexions VPN ExpressRoute ou de site à site.
* Activer les scénarios de cloud hybride en exposant vos API cloud et locales par le biais d’une passerelle commune.
* Gérer vos API hébergées dans plusieurs emplacements géographiques à l’aide d’un seul point de terminaison de passerelle. 

## <a name="enable-vpn"></a>Créer une Gestion des API dans un réseau virtuel interne
Hello service de gestion des API dans le réseau virtuel interne est hébergé derrière un Balancer(ILB) de charge interne. Hello, adresse IP de hello équilibrage de charge interne est Bonjour [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) plage.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Activer la connexion au réseau virtuel à l’aide du Portail Azure
Tout d’abord créer le service de gestion des API de hello en suivant les étapes de hello [service de gestion des API créer][Create API Management service]. Puis les toobe de gestion des API configuration déployé à l’intérieur d’un réseau virtuel.

![Menu de configuration de la Gestion des API dans un réseau virtuel interne][api-management-using-internal-vnet-menu]

Après la réussite du déploiement de hello, vous devez voir hello une adresse IP virtuelle interne de votre service sur le tableau de bord hello.

![Tableau de bord Gestion des API avec réseau virtuel interne configuré][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Activer la connexion au réseau virtuel à l’aide d’applets de commande PowerShell
Vous pouvez également activer la connectivité de réseau virtuel à l’aide des applets de commande PowerShell hello.

* **Créer un service de gestion des API à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate une gestion des API Azure à l’intérieur d’un réseau virtuel de service et configurez le type de réseau virtuel interne toouse hello.

* **Déployer un service de gestion des API existant à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [AzureRmApiManagementDeployment de mise à jour](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove une gestion des API Azure existante de service à l’intérieur d’un réseau virtuel et le configurer toouse Type de réseau virtuel interne.

## <a name="apim-dns-configuration"></a>Configuration DNS
Lorsque vous utilisez la Gestion des API en mode réseau virtuel externe, DNS est géré par Azure. Pour le mode réseau virtuel interne, vous avez toomanage votre propre serveur DNS.

> [!NOTE]
> Service de gestion des API n’écoute pas toorequests provenant des adresses IP. Il ne répond que toorequests toohello nom d’hôte configuré sur ses points de terminaison de service (qui inclut la passerelle, portail des développeurs, l’éditeur Portal, point de terminaison de la gestion directe et git).

### <a name="access-on-default-host-names"></a>Accès sur les noms d’hôtes par défaut :
Lorsque vous créez un service de gestion des API dans le cloud public Azure, nommé « contoso » par exemple, hello points de terminaison de service suivants sont configurés par défaut.

>   Passerelle / Proxy : contoso.azure-api.net

> Portail des éditeurs et portail des développeurs : contoso.portal.azure-api.net

> Point de terminaison de gestion directe : contoso.management.azure-api.net

>   Git : contoso.scm.azure-api.net

tooaccess ces points de terminaison du service de gestion des API, vous pouvez créer un ordinateur virtuel dans un réseau virtuel de toohello sous-réseau connecté dans lequel la gestion des API est déployée. En supposant que hello interne adresse IP virtuelle pour votre service est 10.0.0.5, vous pouvez effectuer hello le mappage de fichier hôtes (% SystemDrive%\drivers\etc\hosts) comme suit :

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

Vous pouvez ensuite accéder à tous les points de terminaison de service hello de hello Machine virtuelle que vous avez créé. Si vous utilisez un serveur DNS personnalisé dans un réseau virtuel, vous pouvez également créer des enregistrements DNS A et accéder à ces points de terminaison à partir de l’endroit de votre choix dans votre réseau virtuel. 

### <a name="access-on-custom-domain-names"></a>Accès sur des noms de domaines personnalisés :
Si vous ne souhaitez pas tooaccess hello service Gestion des noms d’hôte par défaut hello API, vous pouvez configurer des noms de domaine personnalisé pour tous vos points de terminaison service comme ci-dessous

![Configuration d’un domaine personnalisé pour la Gestion des API][api-management-custom-domain-name]

Puis vous pouvez créer un enregistrements dans votre serveur DNS de tooaccess ces points de terminaison qui sont uniquement accessibles à partir de votre réseau virtuel.

## <a name="related-content"></a>Contenu connexe
* [Problèmes courants de configuration réseau lors de l’installation de la Gestion des API dans un réseau virtuel][Common Network Configuration Issues]
* [FAQ des réseaux virtuels](../virtual-network/virtual-networks-faq.md)
* [Création d’un enregistrement A dans DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
