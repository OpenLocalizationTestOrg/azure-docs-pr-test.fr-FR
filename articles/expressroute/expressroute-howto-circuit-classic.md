---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et le portail Azure Classic | Microsoft Docs"
description: "Cet article vous guide tout au long des étapes hello pour la création et configuration d’un circuit ExpressRoute. Cet article vous montre également comment toocheck état de hello, mettre à jour, ou le supprimer et annuler le déploiement de votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Créer et modifier un circuit ExpressRoute à l’aide de PowerShell (classique)
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interface de ligne de commande Azure](howto-circuit-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-circuit-classic.md)
>

Cet article vous guide hello étapes toocreate un circuit ExpressRoute d’Azure à l’aide du modèle de déploiement classique de hello et les applets de commande PowerShell. Cet article vous montre également comment toocheck état de hello, mettre à jour, ou le supprimer et annuler le déploiement d’un circuit ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Avant de commencer
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Étape 1. Passez en revue les conditions préalables de hello et les articles de flux de travail
Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Étape 2. Installer les versions les plus récentes des modules de gestion de Service Azure (SM) PowerShell hello hello
Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview) pour obtenir des instructions sur la façon de tooconfigure votre ordinateur toouse hello Azure les modules PowerShell.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Étape 3. Connectez-vous à tooyour compte Azure, puis sélectionnez un abonnement
1. Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

        Login-AzureRmAccount

2. Vérifiez les abonnements hello pour le compte de hello.

        Get-AzureRmSubscription

3. Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Ensuite, utilisez hello suivant l’applet de commande tooadd tooPowerShell de votre abonnement Azure pour le modèle de déploiement classique hello.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Création et approvisionnement d’un circuit ExpressRoute
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Étape 1. Importer les modules PowerShell hello pour ExpressRoute
 Si vous ne le n'avez pas déjà fait, vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Vous importez les modules hello hello emplacement qu’ils ont été installées tooon votre ordinateur local. En fonction de la méthode hello vous avez utilisé des modules de hello tooinstall, emplacement de hello peut être différent de celui hello suivant montre l’exemple. Si nécessaire, modifier l’exemple de hello.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Étape 2. Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes
Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante.

applet de commande PowerShell de Hello `Get-AzureDedicatedCircuitServiceProvider` retourne cette information, vous allez utiliser dans les étapes suivantes :

    Get-AzureDedicatedCircuitServiceProvider

Vérifiez toosee si votre fournisseur de connectivité y sont répertoriée. Prenez note des informations suivantes, car vous en aurez besoin ultérieurement lorsque vous créez un circuit de hello :

* Nom
* PeeringLocations
* BandwidthsOffered

Vous êtes maintenant prêt toocreate un circuit ExpressRoute.         

### <a name="step-3-create-an-expressroute-circuit"></a>Étape 3. Création d’un circuit ExpressRoute
Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley. Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête.

> [!IMPORTANT]
> Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise. Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.
> 
> 

Hello Voici un exemple de demande pour une nouvelle clé de service :

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Ou, si vous voulez toocreate un circuit ExpressRoute avec un module complémentaire de hello premium, hello d’utiliser l’exemple suivant. Consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


réponse de Hello contiendra la clé du service hello. Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello suivante :

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Étape 4. Liste de tous les circuits ExpressRoute de hello
Vous pouvez exécuter hello `Get-AzureDedicatedCircuit` commande tooget une liste de tous les hello circuits ExpressRoute que vous avez créé :

    Get-AzureDedicatedCircuit

réponse de Hello sera toohello quelque chose de similaire, l’exemple suivant :

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureDedicatedCircuit` applet de commande. Exécuter hello à appel sans paramètre répertorie tous les circuits hello. Votre clé de service s’afficheront dans hello *ServiceKey* champ.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello suivante :

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Étape 5. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration
*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de mise en service sur le côté du fournisseur de services hello hello. *État* fournit l’état de hello sur hello côté de Microsoft. Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.

Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


circuit de Hello passera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Un circuit ExpressRoute doit être Bonjour suivant l’état pour vous toouse en mesure de toobe il :

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Étape 6. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello
Cela vous permet de savoir quand votre fournisseur a activé votre circuit. Après la configuration de circuit de hello, *ServiceProviderProvisioningState* affichera en tant que *configuré* comme indiqué dans hello l’exemple suivant :

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Étape 7. Créer votre configuration de routage
Consultez toohello [circuit ExpressRoute de configuration de routage (créer et modifier des homologations de circuit)](expressroute-howto-routing-classic.md) article pour obtenir des instructions pas à pas.

> [!IMPORTANT]
> Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Étape 8 : Lier un circuit ExpressRoute de tooan réseau virtuel
Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel. Consultez trop[toovirtual réseaux des circuits ExpressRoute de liaison](expressroute-howto-linkvnet-classic.md) pour obtenir des instructions pas à pas. Si vous avez besoin toocreate un réseau virtuel à l’aide du modèle de déploiement classique hello pour ExpressRoute, consultez [créer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>État de hello lors de l’obtention d’un circuit ExpressRoute
Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureCircuit` applet de commande. Exécuter hello à appel sans paramètre répertorie tous les circuits hello.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en passant la clé de service hello comme un appel de toohello de paramètre.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello l’exemple suivant :

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Modification d’un circuit ExpressRoute
Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.

Vous pouvez effectuer hello suivant sans interruption de service :

* Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.
* La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello. Notez que la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge. 
* Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle. Notez ce plan de contrôle hello modification à partir de tooMetered données illimité que données ne sont pas pris en charge.
* Vous pouvez activer et désactiver *Autoriser les opérations classiques*.

Consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations sur les limites et limitations.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>module complémentaire de tooenable hello ExpressRoute premium
Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello suivant l’applet de commande PowerShell :

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Votre circuit est désormais hello ExpressRoute premium module complémentaire fonctionnalités sont activées. Notez que nous allons commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>module complémentaire de toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.
> 
> 

#### <a name="considerations"></a>Considérations

* Vous devez vous assurer que nombre hello de réseaux virtuels liés toohello circuit est inférieure à 10 avant à la rétrogradation à partir de premium toostandard. Si vous ne le faites pas, votre demande de mise à jour échoue, et vous pourrez tarifs hello facturée.
* Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques. Si vous ne le faites pas, votre demande de mise à jour échoue, et vous pourrez tarifs hello facturée.
* Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages. Si la taille de la table de routage est supérieure à 4 000 itinéraires, session BGP hello supprimera et ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes annoncés devient inférieur à 4 000.

#### <a name="disable-hello-premium-add-on"></a>Désactiver le module complémentaire de hello premium
Vous pouvez désactiver le module complémentaire de premium hello ExpressRoute pour votre circuit existant à l’aide de hello suivant l’applet de commande PowerShell :

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bande passante du circuit ExpressRoute hello tooupdate
Vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md) pour les options de bande passante pour le fournisseur de prise en charge. Vous pouvez choisir n’importe quelle taille est supérieure à la taille de hello de votre circuit existant tant que port physique de hello (sur lequel votre circuit est créé) permet.

> [!IMPORTANT]
> Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello. Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.
>
> Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service. Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.
> 
> 

#### <a name="resize-a-circuit"></a>Redimensionner un circuit

Après avoir déterminé la taille que vous avez besoin, vous pouvez utiliser votre circuit hello suivant tooresize de commande :

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Votre circuit sera ont dimensionnés côté de Microsoft hello. Cette modification, vous devez contacter votre configurations tooupdate de fournisseur de connectivité sur leur toomatch côté. Notez que nous allons commencer à vous de facturation pour hello mis à jour option de la bande passante à partir de ce point.

Si vous voyez l’erreur suivante lors de l’augmentation de la bande passante du circuit hello de hello, il signifie qu’il ne reste aucun suffisamment de bande passante sur le port physique hello où votre circuit existant est créé. Vous avez toodelete ce circuit et créez un nouveau circuit de taille hello que vous avez besoin. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute

### <a name="considerations"></a>Considérations

* Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute pour toosucceed de cette opération. Vérifiez toosee si vous avez des réseaux virtuels qui sont liés toohello circuit si cette opération échoue.
* Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté. Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.
* Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello. Cela arrêtera la facturation pour le circuit de hello.

#### <a name="delete-a-circuit"></a>Supprimer un circuit

Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Étapes suivantes
Après avoir créé votre circuit, assurez-vous que vous hello suivant :

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](expressroute-howto-routing-classic.md)
* [Lier votre réseau virtuel de tooyour circuit ExpressRoute](expressroute-howto-linkvnet-classic.md)

