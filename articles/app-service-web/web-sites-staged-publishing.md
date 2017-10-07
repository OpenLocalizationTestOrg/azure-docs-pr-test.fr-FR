---
title: "aaaSet des environnements intermédiaires pour applications web dans Azure App Service | Documents Microsoft"
description: "Découvrez comment toouse intermédiaire à la publication d’applications web dans Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Configurer des environnements intermédiaires dans Azure App Service
<a name="Overview"></a>

Lorsque vous déployez votre application web, une application web sur Linux, mobile back-end et application API trop[du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714), vous pouvez déployer tooa emplacement de déploiement distinct au lieu de l’emplacement de production par défaut hello lors de l’exécution dans hello **Standard**ou **Premium** en mode plan de Service d’applications. Les emplacements de déploiement sont en fait des applications dynamiques pourvues de leur propre nom d’hôte. Éléments de contenu et les configurations application peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production hello. Déploiement de votre emplacement de déploiement d’application tooa a hello avantages suivants :

* Vous pouvez valider la modification de l’application dans un emplacement de déploiement intermédiaire avant d’échanger celui-ci avec l’emplacement de production hello.
* Déploiement d’un emplacement de l’application tooa tout d’abord et permuter vers la production garantissent que toutes les instances de l’emplacement de hello sont préparées avant d’être permutés en production. Cela permet d’éliminer les temps d’arrêt lors du déploiement de l’application. redirection du trafic Hello est transparente, et aucune demande n’est supprimés à la suite d’opérations de permutation. Ce flux de travail peut être entièrement automatisé en configurant [Échange automatique](#Auto-Swap) lorsqu’aucune validation n’est requise avant l’échange.
* Une fois un échange, emplacement hello avec application précédemment intermédiaire a hello précédente application de production. Si les modifications de hello permutées dans l’emplacement de production hello sont pas comme prévu, vous pouvez effectuer hello que même échange immédiatement tooget votre « dernier site connu » sauvegarder.

Chaque mode de plan App Service prend en charge un nombre différent d’emplacements de déploiement. toofind nombre hello d’emplacements prend en charge par le mode de votre application, consultez [tarification de Service application](https://azure.microsoft.com/pricing/details/app-service/).

* Lorsque votre application a plusieurs emplacements, vous ne pouvez pas modifier le mode hello.
* La mise à l'échelle est uniquement disponible pour les emplacements de site de production.
* La gestion des ressources liées est uniquement prise en charge pour les emplacements de site de production. Bonjour [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) uniquement, vous pouvez éviter cet impact potentiel sur un emplacement de production en déplaçant temporairement le mode de plan App Service différents hello emplacement de production non tooa. Notez que cet emplacement de production non hello doit partager à nouveau hello même mode avec l’emplacement de production hello avant que vous pouvez échanger des emplacements de hello deux.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Ajouter un emplacement de déploiement
application Hello doit s’exécuter dans hello **Standard** ou **Premium** dans le mode de commande pour vous tooenable plusieurs emplacements de déploiement.

1. Bonjour [Azure Portal](https://portal.azure.com/), ouvrez votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Choisissez hello **les emplacements de déploiement** option, puis cliquez sur **ajouter un emplacement**.
   
    ![Add a new deployment slot][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Si l’application hello n’est pas déjà hello **Standard** ou **Premium** mode, vous recevrez un message indiquant que les modes de hello pris en charge pour l’activation de publication intermédiaire. À ce stade, vous avez hello option tooselect **mise à niveau** et accédez toohello **échelle** onglet de votre application avant de continuer.
   > 
   > 
3. Bonjour **ajouter un emplacement** panneau, donnez un nom à emplacement de hello, puis sélectionnez si tooclone configuration de l’application à partir d’un autre emplacement de déploiement existant. Cliquez sur toocontinue de case à cocher hello.
   
    ![Source de configuration][ConfigurationSource1]
   
    Hello première fois que vous ajoutez un emplacement, vous aurez seulement deux choix : configuration de clonage depuis l’emplacement par défaut de hello en production ou pas du tout.
    Une fois que vous avez créé plusieurs connecteurs, vous sera en mesure de tooclone à partir d’un emplacement autre que hello une en production :
   
    ![Sources de configuration][MultipleConfigurationSources]
4. Dans le panneau des ressources de votre application, cliquez sur **les emplacements de déploiement**, puis cliquez sur un tooopen d’emplacement de déploiement panneau des ressources de cet emplacement, avec un ensemble de mesures et la configuration comme toute autre application. Hello nom du connecteur de hello est affiché en haut de hello de hello panneau tooremind que vous visualisez hello emplacement de déploiement.
   
    ![Titre de l'emplacement de déploiement][StagingTitle]
5. Cliquez sur URL de l’application hello dans le panneau de l’emplacement hello. Notez l’emplacement de déploiement hello a son propre nom d’hôte et est également une application en temps réel. emplacement de déploiement toohello toolimit accès public, consultez [application de Service d’applications Web – bloquer les emplacements de déploiement web accès toonon-production](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Il n’existe pas de contenu après la création de l’emplacement de déploiement. Vous pouvez déployer le connecteur toohello à partir d’une branche de référentiel différent ou un référentiel complètement différent. Vous pouvez également modifier la configuration de l’emplacement hello. Hello d’utiliser les informations d’identification profil ou au déploiement associées avec l’emplacement de déploiement hello pour les mises à jour de publication.  Par exemple, vous pouvez [publier emplacement toothis avec git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configuration d’emplacements de déploiement
Lorsque vous clonez configuration à partir d’un autre emplacement de déploiement, configuration clonée de hello est modifiable. En outre, certains éléments de configuration suit le contenu hello sur un échange (non spécifique à l’emplacement) alors que les autres éléments de configuration seront conservée dans le même emplacement après un échange (spécifique à l’emplacement) de hello. Hello listes suivantes présentent configuration hello qui change lorsque vous échangez des emplacements.

**Paramètres échangés**:

* Paramètres généraux, par exemple versions d’infrastructure, 32/64 bits, sockets web
* Paramètres de l’application (peut être pas configuré toostick tooa emplacement)
* Chaînes de connexion (peut être pas configuré toostick tooa emplacement)
* Mappages de gestionnaires
* Paramètres de surveillance et de diagnostics
* Contenu WebJobs

**Paramètres non échangés**:

* Points de terminaison de publication
* Noms de domaine personnalisés
* Certificats SSL et liaisons
* Paramètres de mise à l'échelle
* Planificateurs WebJobs

tooconfigure une connexion ou le paramètre de chaîne toostick tooa l’emplacement d’application (ne pas permuté), hello d’accès **paramètres de l’Application** panneau pour un emplacement spécifique, puis sélectionnez hello **paramètre d’emplacement** boîte pour hello éléments de configuration qui est préférable de conserver les emplacement hello. Notez que le marquage un élément de configuration spécifique à l’emplacement a effet hello d’établissement de cet élément comme échangeables pas sur tous les emplacements de déploiement hello associés application hello.

![Paramètres d’emplacement][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Échanger des emplacements de déploiement 
Vous pouvez permuter les emplacements de déploiement Bonjour **vue d’ensemble** ou **les emplacements de déploiement** vue du panneau des ressources de votre application.

> [!IMPORTANT]
> Avant que vous remplacez une application à partir d’un emplacement de déploiement en production, assurez-vous que tous les connecteurs non spécifique est configuré exactement comme vous le souhaitez toohave dans la cible de l’échange hello.
> 
> 

1. tooswap les emplacements de déploiement, cliquez sur hello **échanger** bouton dans la barre de commandes hello de l’application hello ou dans la barre de commandes hello d’un emplacement de déploiement.
   
    ![Bouton Swap][SwapButtonBar]

2. Assurez-vous que cette cible de source et de changer l’échange hello sont correctement définis. Généralement, la cible de l’échange hello est l’emplacement de production hello. Cliquez sur **OK** opération hello de toocomplete. Fin de l’opération de hello, emplacements de déploiement hello ont été permutées.

    ![Échange effectué](./media/web-sites-staged-publishing/SwapImmediately.png)

    Pourquoi **échange avec aperçu** permuter le type, consultez [échange avec aperçu (MULTIPHASE swap)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Échange avec aperçu (échange multiphase)

L’échange avec l’aperçu, ou échange multiphase, simplifie la validation des éléments de configuration spécifiques d’un emplacement, tels que les chaînes de connexion.
Pour les charges de travail critiques, vous souhaitez toovalidate qui hello application se comporte comme prévu lors de la configuration de l’emplacement de production hello est appliquée, et vous devez effectuer cette validation *avant* application hello est échangée en production. C’est précisément ce que l’échange avec aperçu permet de faire.

> [!NOTE]
> L’échange avec l’aperçu n’est pas pris en charge dans les applications web sous Linux.

Lorsque vous utilisez hello **l’échange avec aperçu** option (consultez [d’échanger les emplacements de déploiement](#Swap)), du Service d’applications hello suivant :

- Conserve hello destination emplacement inchangée, charge de travail existante sur cet emplacement (par exemple, production) n’est pas affectée.
- Applique des éléments de configuration hello de hello emplacement toohello source l’emplacement de destination, notamment les chaînes de connexion spécifiques à l’emplacement de hello et les paramètres de l’application.
- Redémarre le processus de travail hello sur l’emplacement de source de hello à l’aide de ces éléments de configuration susmentionnés.
- Quand vous terminez d’échange hello : emplacement de pré-warmed-up source hello se déplace dans l’emplacement de destination hello. l’emplacement de destination Hello est déplacé dans l’emplacement de source de hello comme dans un échange manuel.
- Lorsque vous annulez l’échange de hello : réapplique les éléments de configuration hello de hello source emplacement toohello source emplacement.

Vous pouvez afficher un aperçu exactement comment l’application hello se comporte avec la configuration de l’emplacement de destination hello. Après avoir terminé la validation, vous terminez swap hello dans une étape distincte. Cette étape a hello avantage que hello source est déjà préparée avec la configuration souhaitée de hello, et les clients ne rencontrerez aucun temps d’arrêt.  

Exemples pour hello applets de commande Azure PowerShell disponibles pour l’échange de plusieurs phase sont incluses dans hello applets de commande Azure PowerShell pour la section des emplacements de déploiement.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Configurer l’échange automatique
Auto Swap rationalisation DevOps scénarios où vous toocontinuously déployer votre application avec zéro démarrage à froid et sans interruption pour les clients de fin de l’application hello. Lorsqu’un emplacement de déploiement est configuré pour l’échange automatique en production, chaque fois que vous effectuez un push votre emplacement de toothat de mise à jour de code, du Service d’applications échangera automatiquement application hello en production une fois qu’il a déjà préparée dans l’emplacement de hello.

> [!IMPORTANT]
> Lorsque vous activez l’échange automatique pour un emplacement, vérifiez que hello emplacement configuration est exactement hello prévu pour l’emplacement cible de hello (généralement un emplacement de production hello).
> 
> 

> [!NOTE]
> L’échange automatique n’est pas pris en charge dans les applications web sous Linux.

La configuration de l’échange automatique pour un emplacement est facile. Suivez les étapes de hello ci-dessous :

1. Dans **Emplacements de déploiement**, sélectionnez un emplacement autre que de production et choisissez **Paramètres de l’application** dans le panneau de ressources de cet emplacement.  
   
    ![][Autoswap1]
2. Sélectionnez **sur** pour **échange automatique**, sélectionnez emplacement cible souhaitée hello **emplacement d’échange automatique**, puis cliquez sur **enregistrer** dans la barre de commandes hello. Assurez-vous que la configuration de l’emplacement de hello est exactement hello prévu pour l’emplacement cible de hello.
   
    Hello **Notifications** un vert clignote en onglet **réussite** une fois l’opération hello est terminée.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest échange automatique pour votre application, vous pouvez d’abord sélectionner un emplacement hors production cible dans **emplacement d’échange automatique** toobecome familiarisé avec la fonctionnalité de hello.  
   > 
   > 
3. Exécuter un emplacement de déploiement de code push toothat. Échange automatique se produit après une courte période et mise à jour hello est répercutée à l’URL de l’emplacement de votre cible.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>toorollback une application de production après l’échange
Si des erreurs sont identifiées dans la production après un échange d’emplacement, restaurer les emplacements hello tootheir arrière swap préliminaire États en échangeant les emplacements de hello deux mêmes immédiatement.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Mise en route personnalisée avant la permutation
Certaines applications peuvent nécessiter des actions personnalisées de mise en route. Hello `applicationInitialization` permet d’élément de configuration dans le fichier web.config vous toospecify d’initialisation personnalisées actions toobe effectuée avant une demande est reçue. opération d’échange Hello attendra ce toocomplete préchauffage personnalisé. Voici un exemple de fragment web.config.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete un emplacement de déploiement
Dans le panneau hello pour un emplacement de déploiement, le panneau de l’emplacement de déploiement hello ouvert, cliquez sur **vue d’ensemble** (page par défaut de hello), puis cliquez sur **supprimer** dans la barre de commandes hello.  

![Supprimer un emplacement de déploiement][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Cmdlets Azure PowerShell pour les emplacements de déploiement
Azure PowerShell est un module qui fournit des applets de commande toomanage Azure via Windows PowerShell, y compris la prise en charge pour la gestion des emplacements de déploiement dans Azure App Service.

* Pour plus d’informations sur l’installation et configuration d’Azure PowerShell et sur l’authentification d’Azure PowerShell avec votre abonnement Azure, consultez [comment tooinstall et configurer Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Créer une application web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Créer un emplacement de déploiement
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Lancer un échange avec révision (MULTIPHASE swap) et s’appliquent à l’emplacement de destination emplacement configuration toosource
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Annuler un échange en attente (échange avec aperçu) et restaurer la configuration de l’emplacement source
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Échanger des emplacements de déploiement
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Supprimer un emplacement de déploiement
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Commandes de l’interface de ligne de commande Azure pour les emplacements de déploiement
Hello CLI d’Azure fournit les commandes inter-plateformes pour travailler avec Azure, y compris la prise en charge pour la gestion des emplacements de déploiement du Service d’applications.

* Pour obtenir des instructions sur l’installation et la configuration hello CLI d’Azure, y compris des informations sur la façon de tooconnect CLI d’Azure tooyour abonnement Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).
* commandes de hello toolist disponibles pour le Service d’applications Azure dans hello CLI d’Azure, appelez `azure site -h`.

> [!NOTE] 
> Pour connaître les commandes de l’interface [Azure CLI 2.0](https://github.com/Azure/azure-cli) pour les emplacements de déploiement, consultez l’article [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>azure site list
Pour plus d’informations sur les applications hello dans l’abonnement actif de hello, appelez **liste des sites azure**, comme dans hello l’exemple suivant.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
toocreate un emplacement de déploiement, appelez **créer de site azure** et spécifiez le nom hello d’une application existante et nom hello de hello emplacement toocreate, comme dans l’exemple suivant de hello.

`azure site create webappslotstest --slot staging`

contrôle de code source tooenable pour le nouvel emplacement hello, utilisez hello **--git** option, comme hello l’exemple suivant.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake hello application de production de déploiement mis à jour emplacement hello, utilisez hello **échange de site azure** commande tooperform une opération d’échange, comme dans l’exemple suivant de hello. application de production Hello ne feront pas tout temps mort, ni subiront un démarrage à froid.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete un emplacement de déploiement qui n’est plus nécessaire, utilisez hello **supprimer le site azure** commande, comme dans l’exemple suivant de hello.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Visualisez une application web en action. [Essayez App Service](https://azure.microsoft.com/try/app-service/) dès maintenant et créez une première application temporaire. Aucune carte de crédit ni aucun engagement ne sont nécessaires.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
[Azure App Service Web application – bloquer les emplacements de déploiement de production de toonon accès web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service sur Linux](./app-service-linux-intro.md)
[version d’évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

