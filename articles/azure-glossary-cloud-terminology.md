---
title: Glossaire Azure - dictionnaire Azure | Microsoft Docs
description: "Utilisez le glossaire Azure pour comprendre la terminologie des technologies cloud sur la plateforme Azure Ce petit dictionnaire Azure fournit les définitions des termes les plus courants de la technologie cloud pour Azure."
keywords: "Dictionnaire Azure, terminologie cloud, glossaire Azure, définitions de terminologie, termes de cloud"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: cbc4b8cdb0ff9255d0be02b998e67686921921ea
ms.sourcegitcommit: f67f0bda9a7bb0b67e9706c0eb78c71ed745ed1d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/20/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-the-azure-platform"></a>Glossaire Microsoft Azure : un dictionnaire de la terminologie des technologies cloud sur la plateforme Azure

Le glossaire Microsoft Azure est un petit dictionnaire de la terminologie des technologies cloud pour la plateforme Azure. Voir aussi :

* [Microsoft Azure et Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) - Définitions des services Azure et de leurs équivalents AWS.<!-- I propose to link to https://azure.microsoft.com/en-us/services/ instead of this -->
* [Termes de cloud computing](https://azure.microsoft.com/overview/cloud-computing-dictionary/) - Termes généraux liés aux technologies cloud.

## <a name="account"></a>compte
Compte utilisé pour l’accès et la gestion d’un abonnement Azure. On l’appelle souvent « compte Azure », bien qu’il puisse s’agir d’un compte Microsoft professionnel, scolaire ou personnel existant, ou encore d’un nom d’utilisateur et d’un mot de passe Office 365. Vous pouvez également créer un compte pour gérer un abonnement Azure lorsque vous vous inscrivez pour bénéficier de la [version d’évaluation gratuite](https://azure.microsoft.com).  
Consultez les pages [Sign up for an Azure subscription with your Office 365 account](billing/billing-use-existing-office-365-account-azure-subscription.md) (S’inscrire à un abonnement Azure avec un compte Office 365) et [Accounts you can use to sign in](active-directory/active-directory-how-subscriptions-associated-directory.md) (Comptes utilisables pour l’inscription).

## <a name="api-app"></a>application API
Autre nom pour [application App Service](#app-service-app).

## <a name="app-service-app"></a>application App Service
Ressources de calcul fournies par [Azure App Service](app-service/app-service-web-overview.md) pour l’hébergement d’un site ou d’une application web, d’une API web ou d’un [serveur back-end d’applications mobiles](app-service-mobile/app-service-mobile-value-prop.md). Les applications App Service sont également appelées *App Services*, *applications web*, *applications API* ou *applications mobiles*.

## <a name="availability-set"></a>groupe à haute disponibilité
Une collection de machines virtuelles gérées ensemble pour permettre la redondance et la fiabilité des applications. L’utilisation d’un groupe à haute disponibilité assure qu’au moins une des machines virtuelles sera disponible pendant un événement de maintenance planifié ou non.  
Voir [Gestion de la disponibilité des machines virtuelles Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Gestion de la disponibilité des machines virtuelles Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Modèle de déploiement Azure Classic
L’un des deux [modèles de déploiement](resource-manager-deployment-model.md) utilisés pour déployer des ressources dans Azure (Azure Resource Manager est le modèle plus récent). Certains services Azure prennent en charge uniquement le modèle de déploiement du Gestionnaire de ressources, certains prennent en charge uniquement le modèle de déploiement standard, et d’autres prennent en charge les deux. La documentation de chaque service Azure spécifie le ou les modèles qu’il prend en charge.

## <a name="cli"></a>Interface de ligne de commande Microsoft Azure
Interface de ligne de commande qui peut être utilisée pour gérer les services Azure à partir de Windows, macOS et Linux.  Certains services ou fonctionnalités de service peuvent uniquement être gérés via PowerShell ou l’interface de ligne de commande. Voir [Azure CLI 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Interface de ligne de commande permettant de gérer les services Azure via une ligne de commande sur un PC Windows. Certains services ou fonctionnalités de service peuvent uniquement être gérés via PowerShell ou l’interface de ligne de commande.
Voir [Guide pratique pour installer et configurer Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>modèle de déploiement Azure Resource Manager
l’un des deux [modèles de déploiement](resource-manager-deployment-model.md) utilisés pour déployer des ressources dans Microsoft Azure (l’autre est le modèle de déploiement classique). Certains services Azure prennent en charge uniquement le modèle de déploiement du Gestionnaire de ressources, certains prennent en charge uniquement le modèle de déploiement standard, et d’autres prennent en charge les deux. La documentation de chaque service Azure spécifie le ou les modèles qu’il prend en charge.

## <a name="fault-domain"></a>domaine d’erreur
Une collection de machines virtuelles dans un groupe à haute disponibilité pouvant échouer en même temps. Exemple : un groupe de machines dans un rack partageant une source d’alimentation et un commutateur réseau communs. Dans Azure, les machines virtuelles d’un groupe à haute disponibilité sont automatiquement réparties entre plusieurs domaines d’erreur.  
Voir [Gestion de la disponibilité des machines virtuelles Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Gestion de la disponibilité des machines virtuelles Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>zone géographique
Une limite définie pour la résidence des données qui couvre généralement deux ou plusieurs régions. Les limites peuvent se trouver à l’intérieur ou à l’extérieur des frontières nationales et sont soumises aux réglementations fiscales. Chaque zone géographique couvre au moins une région. L’Asie-Pacifique et le Japon en sont des exemples. Également appelé *géographie*.  
Voir [Régions Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>géoréplication
Le processus de réplication automatique de contenu tel que les objets blob, les tables et les files d’attente au sein d’une paire régionale.  
Voir [Géo-réplication active pour Azure SQL Database](sql-database/sql-database-geo-replication-overview.md)
<!-- The meaning of "geo" in this term seems to be different than the meaning provided in the "geo" entry -->

## <a name="image"></a>image
Un fichier qui contient la configuration du système d’exploitation et des applications, et qui peut servir à créer un nombre illimité de machines virtuelles. Deux types d’images peuvent être utilisés dans Azure : l’image de machine virtuelle et l’image du système d’exploitation. Une image de machine virtuelle inclut un système d'exploitation et tous les disques attachés à une machine virtuelle lors de la création de l'image. Une image du système d’exploitation contient uniquement un système d’exploitation généralisé sans aucune configuration du disque de données.  
Voir [Parcourir et sélectionner des images de machines virtuelles Windows dans Azure avec PowerShell ou l’interface de ligne de commande](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>limites
Le nombre de ressources qui peuvent être créées ou le point de référence des performances pouvant être atteint. Les limites sont généralement associées aux abonnements ainsi qu’aux services et aux offres.  
Voir [Abonnement Azure et limites, quotas et contraintes de service](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>équilibreur de charge
Une ressource qui répartit le trafic entrant sur les ordinateurs d’un réseau. Dans Azure, un équilibreur de charge répartit le trafic sur les machines virtuelles définies dans un jeu d’équilibrage de charge. Un [équilibreur de charge](load-balancer/load-balancer-overview.md) peut être interne ou accessible sur Internet.  

## <a name="mobile-app"></a>application mobile
Autre nom pour [application App Service](#app-service-app).

## <a name="offer"></a>offer
La tarification, les crédits et les conditions associées applicables à un abonnement Azure.  
Consultez la page [Détails de l’offre Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portail
Portail web sécurisé utilisé pour déployer et gérer les services Azure.

## <a name="region"></a>region
Une zone à l’intérieur d’une zone géographique qui ne dépasse pas les frontières nationales et contient un ou plusieurs centres de données. La tarification, les services régionaux et les types d’offre sont exposés au niveau régional. Une région est généralement associée à une autre région, qui peut se trouver à plusieurs centaines de kilomètres. Les paires régionales peuvent servir dans des scénarios de récupération d’urgence et de haute disponibilité. Elles sont également appelées *emplacement*.  
Voir [Régions Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>resource
Un élément qui fait partie de votre solution Azure. Chaque service Azure vous permet de déployer différents types de ressources, comme des bases de données ou des machines virtuelles.   
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>resource group
Un conteneur dans Azure Resource Manager réunissant les ressources associées d’une application. Le groupe de ressources peut inclure toutes les ressources d’une application, ou uniquement celles qui sont regroupées de façon logique. Pour déterminer comment allouer des ressources aux groupes de ressources, choisissez l’approche la plus pertinente pour votre organisation.  
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>modèle Azure Resource Manager
Un fichier JSON qui définit de façon déclarative une ou plusieurs ressources Azure ainsi que les dépendances entre les ressources déployées. Le modèle peut être utilisé pour déployer les ressources de manière cohérente et répétée.  
Voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>fournisseur de ressources
Un service qui fournit les ressources que vous pouvez déployer et gérer via Azure Resource Manager. Chaque fournisseur de ressources propose des opérations pour travailler avec les ressources déployées. Les fournisseurs de ressources sont accessibles via le portail Azure, Azure PowerShell et plusieurs Kits de développement logiciel (SDK) de programmation.  
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>role
Un moyen de contrôler l’accès qui peut être affecté aux utilisateurs ainsi qu’aux groupes et services. Les rôles rendent possibles des actions telles que la création, la gestion et la lecture sur les ressources Azure.  
Voir [RBAC : rôles intégrés](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>Contrat de Niveau de Service (SLA)
Les contrats SLA décrivent les engagements de Microsoft en matière de temps d’activité et de connectivité. Chaque service Azure dispose d’un contrat SLA spécifique.  
Voir [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>signature d’accès partagé (SAP)
Signature qui vous permet d’accorder un accès limité à une ressource, sans exposer votre clé de compte. Par exemple, le [stockage Azure utilise SAP](storage/common/storage-dotnet-shared-access-signature-part-1.md) pour accorder l’accès client à des objets tels que des objets BLOB. [IoT Hub utilise SAP](iot-hub/iot-hub-devguide-security.md#security-tokens) pour accorder à des appareils l’autorisation d’envoyer des données de télémétrie.

## <a name="storage-account"></a>compte de stockage
Compte qui vous donne accès aux services Azure Objet blob, File d’attente, Table et Fichier dans le stockage Azure. Le nom du compte de stockage définit l’espace de noms unique pour vos objets de données de stockage Azure.  
Voir [À propos des comptes de stockage Azure](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>abonnement
Accord d’un client avec Microsoft qui lui permet de bénéficier de services Azure. La tarification des abonnements et les conditions associées sont régies par l’offre choisie pour l’abonnement.
Voir [Contrat d’abonnement à Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/) et [Association des abonnements Azure avec Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>tag
Un terme d’indexation vous permettant de catégoriser les ressources en fonction de vos exigences de gestion ou de facturation. Lorsque vous disposez d’un ensemble complexe de ressources , vous pouvez utiliser des balises pour visualiser ces ressources de la façon la plus pertinente. Par exemple, vous pouvez baliser des ressources qui jouent un rôle similaire dans votre organisation ou qui appartiennent au même département.  
Voir [Utilisation de balises pour organiser vos ressources Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>domaine de mise à jour
Une collection de machines virtuelles dans un groupe à haute disponibilité qui sont mises à jour en même temps. Les machines virtuelles dans un même domaine de mise à jour sont redémarrées simultanément lors de la maintenance planifiée. Azure ne redémarre jamais plus d’un domaine de mise à jour à la fois. Également appelé domaine de mise à niveau.  
Voir [Gestion de la disponibilité des machines virtuelles Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Gestion de la disponibilité des machines virtuelles Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>Machine virtuelle
L’implémentation logicielle d’un ordinateur physique qui exécute un système d’exploitation. Il est possible d’exécuter plusieurs machines virtuelles simultanément sur le même matériel. Dans Azure, les machines virtuelles sont disponibles en plusieurs tailles.  
Voir [Documentation sur les machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extension de machine virtuelle
Une ressource qui implémente des comportements ou des fonctionnalités facilitant le fonctionnement d’autres programmes ou qui vous offre la possibilité d’interagir avec un ordinateur en cours d’exécution. Par exemple, vous pouvez utiliser l’extension VM Access pour réinitialiser ou modifier les valeurs d’accès à distance sur une machine virtuelle Azure.
<!-- This definition seems obscure to me; maybe a list of examples would work better than a conceptual definition? -->
Voir [À propos des extensions et des fonctionnalités des machines virtuelles (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [À propos des extensions et des fonctionnalités des machines virtuelles (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>Réseau virtuel
Un réseau qui assure la connectivité entre vos ressources Azure, isolé de tous les autres locataires Azure. Une [passerelle VPN Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) vous permet d’établir des connexions entre des réseaux virtuels et [entre un réseau virtuel et un réseau local](vpn-gateway/vpn-gateway-plan-design.md). Vous pouvez contrôler complètement les blocs d’adresses IP, les paramètres DNS, les stratégies de sécurité et les tables de routage au sein d’un réseau virtuel.  
Voir [Présentation du réseau virtuel](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Application web
Autre nom pour [application App Service](#app-service-app).

## <a name="see-also"></a>Voir aussi

* [Prise en main d’Azure](https://azure.microsoft.com/get-started/)
* [Centre de ressources du cloud](https://azure.microsoft.com/resources/)  
* [Azure pour vos applications métier](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure dans votre centre de données](https://azure.microsoft.com/overview/business-apps-on-azure/)

