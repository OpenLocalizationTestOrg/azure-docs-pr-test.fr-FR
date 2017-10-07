---
title: "machines virtuelles d’aaaMigrate tooResource Manager à l’aide de CLI d’Azure | Documents Microsoft"
description: "Cet article assiste hello plateforme prise en charge la migration de ressources à partir de tooAzure classique Gestionnaire de ressources à l’aide de CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Migrer les ressources IaaS de classique tooAzure Gestionnaire de ressources à l’aide de CLI d’Azure
Ces étapes vous montrent comment toouse Azure interface de ligne de commande (CLI) commandes toomigrate infrastructure en tant qu’une ressource de service (IaaS) à partir du modèle de déploiement du modèle toohello Azure Resource Manager hello déploiement classique. article de Hello requiert hello [CLI d’Azure](../../cli-install-nodejs.md).

> [!NOTE]
> Toutes les opérations de hello décrites ici sont idempotent. Si vous avez un problème autre qu’une fonctionnalité non prise en charge ou une erreur de configuration, nous vous recommandons de relancer hello préparer, abandonner ou valider l’opération. plateforme de Hello essaiera alors action hello à nouveau.
> 
> 

<br>
Voici un ordre de hello tooidentify organigramme dans lequel les étapes doivent toobe exécutée pendant un processus de migration

![Capture d’écran qui illustre les étapes de migration hello](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Étape 1 : préparation de la migration
Voici quelques meilleures pratiques que nous recommandons lors de l’évaluation de la migration des ressources IaaS de classique tooResource Manager :

* Lisez hello [la liste des configurations non prises en charge et fonctionnalités](../windows/migration-classic-resource-manager-overview.md). Si vous avez des ordinateurs virtuels qui utilisent des configurations non prises en charge et fonctionnalités, nous vous recommandons d’attendre toobe de prise en charge de configuration de la fonction hello annoncé. Vous pouvez également supprimer cette fonctionnalité ou sortir de cette migration tooenable de configuration si elle répond à vos besoins.
* Si vous avez automatisé scripts aujourd'hui à déployer votre infrastructure et vos applications, essayez de toocreate une configuration de test similaire à l’aide de ces scripts pour la migration. Ou bien, vous pouvez définir des environnements d’exemple à l’aide de hello portail Azure.

> [!IMPORTANT]
> Passerelles d’application ne sont pas actuellement pris en charge pour la migration de classique tooResource Manager. toomigrate un réseau virtuel classique avec une passerelle d’Application, supprimer la passerelle de hello avant l’exécution d’un réseau de Préparer opération toomove hello. Après avoir effectué la migration de hello, reconnectez le passerelle hello dans Azure Resource Manager. 
>
>Les passerelles ExpressRoute connexion circuits tooExpressRoute dans un autre abonnement ne peut pas être migrés automatiquement. Dans ce cas, supprimez la passerelle ExpressRoute de hello, migrer un réseau virtuel hello et recréez hello passerelle. Consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) pour plus d’informations.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Étape 2 : Définir votre abonnement et inscrire le fournisseur de hello
Pour les scénarios de migration, vous devez tooset de votre environnement pour les deux classique et Gestionnaire de ressources. [Installez l’interface de ligne de commande Azure](../../cli-install-nodejs.md) et [sélectionnez votre abonnement](../../xplat-cli-connect.md).

Compte de connexion tooyour.

    azure login

Sélectionnez hello abonnement Azure à l’aide de hello commande suivante.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> L’inscription est défini une fois l’étape, mais il a besoin toobe fait qu’une seule fois avant de tenter la migration. Sans inscription hello message d’erreur suivant s’affiche 
> 
> *Requête invalide : l’abonnement n’est pas inscrit pour la migration.* 
> 
> 

Enregistrer avec le fournisseur de ressources hello migration à l’aide de hello commande suivante. Notez que cette commande expire dans certains cas. Toutefois, l’inscription hello sera réussie.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Attendez cinq minutes pour hello inscription toofinish. Vous pouvez vérifier l’état hello d’approbation de hello à l’aide de hello commande suivante. Assurez-vous que RegistrationState est `Registered` avant de continuer.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Passez maintenant CLI toohello `asm` mode.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Étape 3 : Vérifiez que vous disposez assez de cœurs Machine virtuelle de Azure Resource Manager Bonjour région Azure de votre déploiement en cours ou de réseau virtuel
Pour cette étape vous devez tooswitch trop`arm` mode. Cela hello commande suivante.

```
azure config mode arm
```

Vous pouvez utiliser hello suivant CLI commande toocheck hello quantité actuelle de cœurs que dans le Gestionnaire de ressources Azure. toolearn en savoir plus sur les quotas de base, consultez [limites et hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Une fois que vous avez terminé à la vérification de cette étape, vous pouvez revenir trop`asm` mode.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Étape 4 : Option 1 - Migration de machines virtuelles dans un service cloud
Obtenez la liste de services de cloud computing à l’aide de hello commande suivante, puis sur service de cloud hello choix que vous souhaitez toomigrate hello. Notez que si hello machines virtuelles dans le service cloud hello se trouvent dans un réseau virtuel, ou si elles ont des rôles web/de travail, vous obtenez un message d’erreur.

    azure service list

Exécutez hello suivant le nom du déploiement commande tooget hello pour le service cloud hello à partir de la sortie des commentaires hello. Dans la plupart des cas, le nom du déploiement hello est hello identique au nom du service cloud hello.

    azure service show <serviceName> -vv

Tout d’abord, vérifiez si vous pouvez migrer le service de cloud computing hello hello suivant les commandes à l’aide de :

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Préparer les ordinateurs virtuels de hello dans le service cloud hello pour la migration. Vous avez deux options toochoose, à partir de.

Si vous souhaitez toomigrate hello machines virtuelles tooa plate-forme réseau virtuel créé, utilisez hello commande suivante.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Si vous souhaitez tooan toomigrate réseau virtuel dans le modèle de déploiement du Gestionnaire de ressources hello existant, utilisez hello commande suivante.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Une fois hello Préparer opération a réussi, vous pouvez examiner hello documenté tooget hello état de la migration de machines virtuelles de hello et vérifier qu’ils sont Bonjour `Prepared` état.

    azure vm show <vmName> -vv

Vérifiez la configuration de hello pour hello préparé des ressources à l’aide de l’interface CLI ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.

    azure service deployment abort-migration <serviceName> <deploymentName>

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Étape 4 : Option 2 - Migration de machines virtuelles dans un réseau virtuel
Réseau virtuel de prélèvement hello que vous souhaitez toomigrate. Notez que si le réseau virtuel de hello contient les rôles web/de travail ou des machines virtuelles avec des configurations non prises en charge, vous obtenez un message d’erreur de validation.

Obtient tous les réseaux virtuels hello dans l’abonnement hello à l’aide de hello après la commande.

    azure network vnet list

Hello sortie ressemble à ceci :

![Capture d’écran de ligne de commande hello avec le nom de réseau virtuel entier hello mis en surbrillance.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

Bonjour exemple ci-dessus, hello **%virtualnetworkname** est le nom complet de hello **« Classicubuntu16 classicubuntu16 de groupe »**.

Tout d’abord, vérifiez si vous pouvez migrer hello virtual network utilisant hello de commande suivante :

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Préparer les réseaux de hello de votre choix pour la migration à l’aide de hello commande suivante.

    azure network vnet prepare-migration <virtualNetworkName>

Vérifiez la configuration de hello pour hello préparé des machines virtuelles à l’aide de l’interface CLI ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.

    azure network vnet abort-migration <virtualNetworkName>

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Étape 5 : migration d’un compte de stockage
Une fois que vous avez terminé la migration d’ordinateurs virtuels hello, nous vous recommandons de que migrer de compte de stockage hello.

Préparer la migration à l’aide de hello commande suivante compte de stockage hello

    azure storage account prepare-migration <storageAccountName>

Vérifiez la configuration de hello pour hello préparé le compte de stockage à l’aide de l’interface CLI ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello commande suivante.

    azure storage account abort-migration <storageAccountName>

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello commande suivante.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utiliser les ressources IaaS PowerShell toomigrate classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
