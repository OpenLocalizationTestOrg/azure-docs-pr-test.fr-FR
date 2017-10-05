---
title: "Principes de bases de l’administration d’Azure Stack | Microsoft Docs"
description: "Découvrez tout ce qu’il faut savoir pour administrer Azure Stack."
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
ms.openlocfilehash: 73f2c739a792825ccccda39ca76abef2dd490808
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stack-administration-basics"></a>Principes de bases de l’administration d’Azure Stack

Si vous débutez avec l’administration d’Azure Stack, vous devez prendre connaissance de plusieurs choses. Ce guide fournit une vue d’ensemble de votre rôle en tant qu’opérateur cloud, et explique ce que vous devez dire à vos utilisateurs pour qu’ils deviennent rapidement productifs.

## <a name="understand-development-kit-builds"></a>Présentation des builds du Kit de développement

Consultez l’article [Qu’est-ce qu’Azure Stack ?](azure-stack-poc.md) pour être sûr de bien comprendre la fonction du Kit de développement Azure Stack et ses limitations. Vous devez utiliser le Kit de développement comme « bac à sable », dans lequel vous pouvez évaluer Azure Stack et développer et tester vos applications dans un environnement hors production. (Pour plus d’informations sur le déploiement, consultez le guide de démarrage rapide [Déploiement du Kit de développement Azure Stack](azure-stack-deploy-overview.md).)

Comme Azure, nous innovons rapidement. Nous publierons régulièrement de nouvelles builds. Quand vous souhaitez passer à la version la plus récente, vous devez [redéployer Azure Stack](azure-stack-redeploy.md). Ce processus prend du temps, mais l’avantage est que vous pouvez essayer les fonctionnalités les plus récentes. La documentation sur notre site web reflète la build la plus récente.

## <a name="learn-about-available-services"></a>Découvrir les services disponibles

Vous devez savoir quels services vous pouvez mettre à disposition de vos utilisateurs. Azure Stack prend en charge une partie des services Azure. La liste des services pris en charge continue d’évoluer.

**Services fondamentaux**

Par défaut, Azure Stack comprend les « services fondamentaux » suivants quand vous déployez Azure Stack :

- Calcul
- Storage
- Mise en réseau
- Key Vault

Avec ces services fondamentaux, vous pouvez proposer une solution IaaS (Infrastructure-as-a-Service) à vos utilisateurs avec une configuration minimale.

**Services supplémentaires**

Actuellement, nous prenons en charge les services PaaS (Platform-as-a-Service) supplémentaires suivants :

- App Service
- Azure Functions
- Bases de données SQL et MySQL

Ces services nécessitent une configuration supplémentaire avant de pouvoir être mis à disposition des utilisateurs. Pour plus d’informations, consultez les « Didacticiels » et les sections « Guides pratiques/Services d’offres » de notre documentation.

**Feuille de route des services**

Azure Stack continuera à prendre en charge de nouveaux services Azure. Pour plus d’informations sur la feuille de route prévue, consultez le livre blanc [Hybrid Application Innovation with Azure and Azure Stack (Innovation d’application hybride avec Azure et Azure Stack)](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409). Vous pouvez également consulter les nouvelles annonces dans les [billets de blog Azure Stack](https://azure.microsoft.com/blog/tag/azure-stack-technical-preview).

## <a name="what-tools-do-i-use-to-manage"></a>Quels outils dois-je utiliser pour la gestion ?
 
Vous pouvez utiliser le [portail administrateur](azure-stack-manage-portals.md) ou PowerShell pour gérer Azure Stack. Le moyen le plus simple de découvrir les concepts de base est d’utiliser le portail. Si vous souhaitez utiliser PowerShell, des étapes de préparation sont nécessaires. Vous devez [installer](azure-stack-powershell-install.md) PowerShell, [télécharger](azure-stack-powershell-download.md) des modules supplémentaires et [configurer](azure-stack-powershell-configure-admin.md) PowerShell.

Azure Stack utilise Azure Resource Manager comme mécanisme de déploiement, de gestion et d’organisation sous-jacent. Si vous comptez gérer Azure Stack et assister les utilisateurs, vous devez connaître Resource Manager. Consultez le livre blanc [Getting Started with Azure Resource Manager (Bien démarrer avec Azure Resource Manager)](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf).

## <a name="your-typical-responsibilities"></a>Vos responsabilités classiques

Vos utilisateurs souhaitent utiliser des services. De leur point de vue, votre rôle principal est de mettre ces services à leur disposition. Vous devez décider quels services offrir, et rendre ces services accessibles en créant des [quotas](azure-stack-setting-quotas.md), des [plans](azure-stack-create-plan.md) et des [offres](azure-stack-create-offer.md). 

Vous devez également ajouter des éléments à la Place de Marché, tels que des images de machines virtuelles. Le moyen le plus simple consiste à [télécharger des éléments de la Place de marché à partir d’Azure dans Azure Stack](azure-stack-download-azure-marketplace-item.md).

> [!NOTE]
> Si vous souhaitez tester vos plans, vos offres et vos services, vous devez utiliser le [portail utilisateur](azure-stack-manage-portals.md), et non le portail administrateur.

En plus de fournir des services, vous devez effectuer toutes les tâches standard d’un opérateur cloud pour veiller au bon fonctionnement d’Azure Stack. Il s’agit notamment des tâches suivantes :

- Ajouter des comptes d’utilisateur (pour le déploiement d’[Azure Active Directory](azure-stack-add-new-user-aad.md) ou d’[Active Directory Federation Services](azure-stack-add-users-adfs.md))
- [Affecter des rôles de contrôle d’accès en fonction du rôle (RBAC)](azure-stack-manage-permissions.md) (Cela ne se limite pas aux administrateurs.)
- [Surveiller l’intégrité de l’infrastructure](azure-stack-monitor-health.md)
- Gérer les ressources [réseau](azure-stack-viewing-public-ip-address-consumption.md) et de [stockage](azure-stack-manage-storage-accounts.md)
- Remplacer le matériel défectueux

## <a name="what-to-tell-your-users"></a>Ce que vous devez dire à vos utilisateurs

Vous devez dire à vos utilisateurs comment travailler avec les services dans Azure Stack, comment se connecter à l’environnement du Kit de développement et comment s’abonner aux offres.

**Utiliser des services dans Azure Stack**

Vos utilisateurs doivent connaître certaines informations avant d’utiliser des services et de créer des applications dans Azure Stack. Par exemple, il existe des exigences propres à PowerShell et aux versions d’API. Il existe également des différences de fonctionnalité entre un service dans Azure et le service équivalent dans Azure Stack. Assurez-vous que vos utilisateurs lisent les articles suivants :

- [Considérations importantes : utilisation de services ou création d’applications pour Azure Stack](azure-stack-considerations.md)
- [Considérations relatives aux machines virtuelles dans Azure Stack](azure-stack-vm-considerations.md)
- [Stockage : Différences et considérations](azure-stack-acs-differences-tp2.md)

Les informations contenues dans ces articles résument les différences entre un service dans Azure et dans Azure Stack. Elles complètent les informations disponibles pour un service Azure dans la documentation Azure globale. 

**Se connecter à Azure Stack en tant qu’utilisateur**

Dans un environnement de Kit de développement, si un utilisateur ne dispose pas d’un accès Bureau à distance à l’hôte du Kit de développement, il doit configurer une connexion de réseau privé virtuel (VPN) avant de pouvoir accéder à Azure Stack. Consultez [Se connecter à Azure Stack](azure-stack-connect-azure-stack.md). 

Vos utilisateurs souhaiteront savoir comment [accéder au portail utilisateur](azure-stack-manage-portals.md) ou comment se connecter par le biais de PowerShell. S’ils utilisent PowerShell, les utilisateurs devront peut-être inscrire des fournisseurs de ressources avant de pouvoir utiliser des services. (Un fournisseur de ressources gère un service. Par exemple, le fournisseur de ressources réseau gère des ressources telles que les réseaux virtuels, les interfaces réseau et les équilibreurs de charge.) Ils doivent [installer](azure-stack-powershell-install.md) PowerShell, [télécharger](azure-stack-powershell-download.md) des modules complémentaires et [configurer](azure-stack-powershell-configure-user.md) PowerShell (qui inclut l’inscription des fournisseurs de ressources).

**S’abonner à une offre**

Avant de pouvoir accéder à des services, un utilisateur doit [s’abonner à une offre](azure-stack-subscribe-plan-provision-vm.md) que vous avez créée en tant qu’opérateur cloud.

## <a name="where-to-get-support"></a>Où obtenir un support technique ?

Pour le Kit de développement Azure Stack, vous pouvez poser des questions relatives au support technique sur les [forums Microsoft](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). Si vous cliquez sur l’icône d’aide et de support (point d’interrogation) dans le coin supérieur droit du portail administrateur, puis sur **Nouvelle demande de support**, le site des forums s’ouvre directement. Ces forums sont consultés régulièrement. Le Kit de développement étant un environnement d’évaluation, il n’y a aucune prise en charge officielle de la part des services de support technique Microsoft.

## <a name="next-steps"></a>Étapes suivantes

- [Gestion des régions dans Azure Stack](azure-stack-region-management.md)


