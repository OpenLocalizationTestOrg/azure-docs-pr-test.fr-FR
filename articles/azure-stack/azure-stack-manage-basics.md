---
title: Notions de base aaaAzure pile administration | Documents Microsoft
description: "Découvrez ce que vous devez tooknow tooadminister pile d’Azure."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 856738a7-1510-442a-88a8-d316c67c757c
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: twooley
ms.openlocfilehash: cdf2818e9fc819b448508ca52bbdbec259890265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-administration-basics"></a>Principes de bases de l’administration d’Azure Stack

Il existe plusieurs choses tooknow si vous êtes de nouveau tooAzure administration de la pile. Ce guide fournit une vue d’ensemble de votre rôle d’un opérateur cloud et ce que vous avez besoin tootell vos utilisateurs pour leur toobecome productif rapidement.

## <a name="understand-development-kit-builds"></a>Présentation des builds du Kit de développement

Hello de révision [Nouveautés Azure pile ?](azure-stack-poc.md) toomake de l’article que vous comprenez l’objectif de hello de hello Kit de développement de pile Azure et ses limitations. Vous devez utiliser le kit de développement hello comme un « bac à sable, « où vous pouvez évaluer la pile d’Azure et développer et tester vos applications dans un environnement hors production. (Pour plus d’informations de déploiement, consultez hello [de déploiement du Kit de développement Azure pile](azure-stack-deploy-overview.md) démarrage rapide.)

Comme Azure, nous innovons rapidement. Nous publierons régulièrement de nouvelles builds. Lorsque vous souhaitez toomove toohello build la plus récente, vous devez [redéployer Azure pile](azure-stack-redeploy.md). Ce processus prend du temps, mais les avantages hello sont que vous pouvez essayer des fonctionnalités les plus récentes hello. documentation Hello sur notre site Web reflète la dernière version Release de hello.

## <a name="learn-about-available-services"></a>Découvrir les services disponibles

Vous aurez besoin d’une prise de conscience de quels services vous ferez tooyour disponibles. Azure Stack prend en charge une partie des services Azure. liste de Hello des services pris en charge continue tooevolve.

**Services fondamentaux**

Par défaut, la pile de Azure inclut hello suivant « services fondamentaux » lorsque vous déployez Azure pile :

- Calcul
- Storage
- Mise en réseau
- Key Vault

Avec ces services fondamentaux, vous pouvez offrir aux utilisateurs de tooyour Infrastructure-as-a-Service (IaaS) avec une configuration minimale.

**Services supplémentaires**

Actuellement, nous prenons en charge hello suivant des services supplémentaires Platform-as-a-Service (PaaS) :

- App Service
- Azure Functions
- Bases de données SQL et MySQL

Ces services nécessitent une configuration supplémentaire avant de les rendre disponibles tooyour utilisateurs. Pour plus d’informations, consultez les sections « Comment-tooguides\Offer services » de hello de notre documentation et les hello « didacticiels ».

**Feuille de route des services**

Pile Azure continue tooadd prise en charge des services Azure. Pour la feuille de route hello projeté, consultez hello [Innovation d’Application hybride avec Azure et Azure pile](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409) livre blanc. Vous pouvez également surveiller hello [billets de blog Azure pile](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview) les nouvelles annonces.

## <a name="what-tools-do-i-use-toomanage"></a>Que faire outils utiliser toomanage ?
 
Vous pouvez utiliser hello [portail d’administration](azure-stack-manage-portals.md) ou PowerShell toomanage pile d’Azure. Hello plus simple façon toolearn hello concepts de base est via le portail de hello. Si vous souhaitez toouse PowerShell, il existe des étapes de préparation. Vous devez [installer](azure-stack-powershell-install.md) PowerShell, [télécharger](azure-stack-powershell-download.md) des modules supplémentaires et [configurer](azure-stack-powershell-configure-admin.md) PowerShell.

Azure Stack utilise Azure Resource Manager comme mécanisme de déploiement, de gestion et d’organisation sous-jacent. Si vous souhaitez toomanage Azure pile et aident les utilisateurs de prise en charge, vous devez apprendre sur le Gestionnaire de ressources. Consultez hello [prise en main avec Azure Resource Manager](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) livre blanc.

## <a name="your-typical-responsibilities"></a>Vos responsabilités classiques

Vos utilisateurs souhaitent toouse services. À partir de leur point de vue, votre rôle principal est toomake ces services toothem disponible. Vous devez décider quels toooffer services et rendre ces services disponibles en créant [quotas](azure-stack-setting-quotas.md), [plans](azure-stack-create-plan.md), et [offre](azure-stack-create-offer.md). 

Vous devez également tooadd éléments toohello marketplace, tels que des images de machine virtuelle. Hello plus simple est trop[télécharger des éléments du marketplace à partir d’Azure tooAzure pile](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> Si vous souhaitez tootest vos plans, les offres et les services, vous devez utiliser hello [portail de l’utilisateur](azure-stack-manage-portals.md); non portail d’administration hello.

Dans les services de tooproviding de plus, vous devez effectuer toutes les tâches régulières hello d’un tookeep d’opérateur de cloud Azure pile en cours d’exécution. Ces droits hello suivants :

- Ajouter des comptes d’utilisateur (pour le déploiement d’[Azure Active Directory](azure-stack-add-new-user-aad.md) ou d’[Active Directory Federation Services](azure-stack-add-users-adfs.md))
- [Affecter des rôles de contrôle (RBAC) d’accès en fonction du rôle](azure-stack-manage-permissions.md) (cela n’est pas restreinte tooadministrators.)
- [Surveiller l’intégrité de l’infrastructure](azure-stack-monitor-health.md)
- Gérer les ressources [réseau](azure-stack-viewing-public-ip-address-consumption.md) et de [stockage](azure-stack-manage-storage-accounts.md)
- Remplacer le matériel défectueux

## <a name="what-tootell-your-users"></a>Quelles tootell vos utilisateurs

Vous aurez besoin de vos utilisateurs sachent comment toowork avec les services dans la pile d’Azure, comment l’environnement du kit de développement de toohello tooconnect et de toolet toosubscribe toooffers.

**Comprendre comment toowork avec les services dans la pile de Azure**

Vos utilisateurs doivent connaître certaines informations avant d’utiliser des services et de créer des applications dans Azure Stack. Par exemple, il existe des exigences propres à PowerShell et aux versions d’API. Il existe également des deltas de fonctionnalité entre un service dans Azure et hello équivalent au Azure pile. Assurez-vous que vos utilisateurs examiner hello suivant des articles :

- [Considérations importantes : utilisation de services ou création d’applications pour Azure Stack](azure-stack-considerations.md)
- [Considérations relatives aux machines virtuelles dans Azure Stack](azure-stack-vm-considerations.md)
- [Stockage : Différences et considérations](azure-stack-acs-differences-tp2.md)

informations Hello dans ces articles résument les différences de hello entre un service dans Azure et de la pile de Azure. Il complète informations hello disponibles pour un service Azure dans la documentation Azure hello globale. 

**Se connecter tooAzure pile en tant qu’utilisateur**

Dans un environnement de kit de développement, si un utilisateur n’a pas hôte du kit de développement de toohello Bureau à distance accès, ils doivent configurer une connexion de réseau privé virtuel (VPN) avant de pouvoir accéder à la pile de Azure. Consultez [connecter tooAzure pile](azure-stack-connect-azure-stack.md). 

Vos utilisateurs voudront tooknow comment trop[portail de l’utilisateur l’accès hello ](azure-stack-manage-portals.md) ou comment tooconnect via PowerShell. Si vous utilisez PowerShell, les utilisateurs peuvent avoir des fournisseurs de ressources tooregister avant de pouvoir utiliser les services. (Un fournisseur de ressources gère un service. Par exemple, hello mise en réseau de fournisseur de ressources gère les ressources telles que les réseaux virtuels, les interfaces réseau et les équilibreurs de charge.) Ils doivent [installer](azure-stack-powershell-install.md) PowerShell, [télécharger](azure-stack-powershell-download.md) des modules complémentaires et [configurer](azure-stack-powershell-configure-user.md) PowerShell (qui inclut l’inscription des fournisseurs de ressources).

**S’abonner tooan offre**

Avant d’un utilisateur peut accéder aux services, ils doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) que vous avez créé comme un opérateur de cloud.

## <a name="where-tooget-support"></a>Où tooget prennent en charge

Pourquoi le Kit de développement de pile Azure, vous pouvez poser des questions de prise en charge associées Bonjour [forums Microsoft](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). Si vous cliquez sur hello aide et support icône (point d’interrogation) dans le coin supérieur droit de hello du portail d’administrateur hello, puis cliquez sur **nouveau prend en charge la demande**, ce site s’ouvre alors hello forums directement. Ces forums sont consultés régulièrement. Kit de développement hello étant un environnement d’évaluation, il n’existe aucune prise en charge officielle proposé par Microsoft prend en charge les Services (technique).

## <a name="next-steps"></a>Étapes suivantes

- [Gestion des régions dans Azure Stack](azure-stack-region-management.md)


