---
title: glossaire aaaAzure - dictionnaire Azure | Documents Microsoft
description: "Utilisez la terminologie de hello glossaire Azure toounderstand cloud hello plateforme Azure. Ce petit dictionnaire Azure fournit les définitions des termes les plus courants de la technologie cloud pour Azure."
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
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Glossaire de Microsoft Azure : un dictionnaire de la terminologie de cloud sur hello plateforme Azure

glossaire de Microsoft Azure Hello est un dictionnaire court de la terminologie de cloud pour hello plateforme Azure. Voir aussi :

* [Microsoft Azure et Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) - Définitions des services Azure et de leurs équivalents AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Termes de cloud computing](https://azure.microsoft.com/overview/cloud-computing-dictionary/) - Termes généraux liés aux technologies cloud.

## <a name="account"></a>compte
Un compte qui a utilisé tooaccess et gérer un abonnement Azure. Il est souvent appelée tooas Azure compte même si un compte peut être une de ces : un travail existant, académique ou personnel compte Microsoft, ou un Office 365 nom d’utilisateur et mot de passe. Vous pouvez également créer un compte toomanage un abonnement Azure lorsque vous vous inscrivez pour hello [version d’évaluation gratuite](https://azure.microsoft.com).  
Consultez [souscrire un abonnement Azure avec votre compte Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) et [comptes que vous pouvez utiliser toosign dans](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>application API
Autre nom pour [application App Service](#app-service-app).

## <a name="app-service-app"></a>application App Service
Hello des ressources de calcul qui [Azure App Service](app-service/app-service-value-prop-what-is.md) offre pour héberger un [application ou le site web](app-service-web/app-service-web-overview.md), [web API](app-service-api/app-service-api-apps-why-best-platform.md), ou [principal de l’application mobile](app-service-mobile/app-service-mobile-value-prop.md). Applications de Service d’applications sont également référencé tooas *des Services d’application*, *les applications web*, *applications API*, et *des applications mobiles*.

## <a name="availability-set"></a>groupe à haute disponibilité
Une collection d’ordinateurs virtuels qui sont gérés ensemble la fiabilité et la redondance des applications tooprovide. utilisation de Hello de haute disponibilité garantit que, pendant un événement de maintenance planifiée ou non, au moins un ordinateur virtuel est disponible.  
Consultez [gérer la disponibilité des machines virtuelles Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [gérer la disponibilité hello des ordinateurs virtuels Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Modèle de déploiement Azure Classic
Une des deux [modèles de déploiement](resource-manager-deployment-model.md) utilisé toodeploy de ressources Azure (modèle hello est Azure Resource Manager). Certains services Azure prend en charge uniquement les modèles de déploiement Resource Manager hello, certains prennent en charge uniquement le modèle de déploiement classique hello et certains prennent en charge les deux. documentation Hello pour chaque service Azure Spécifie l’ou les modèles pris en charge.

## <a name="cli"></a>Interface de ligne de commande Microsoft Azure
Une interface de ligne de commande qui peuvent être utilisé toomanage des services Azure à partir de Windows, Mac OS et Linux.  Certains services ou les fonctionnalités du service peuvent être gérées uniquement via PowerShell ou hello CLI. Voir [Azure CLI 2.0](/cli/azure/overview)

## <a name="powershell"></a>Azure PowerShell
Un toomanage de l’interface de ligne de commande des services Azure via une ligne de commande à partir des PC Windows. Certains services ou les fonctionnalités du service peuvent être gérées uniquement via PowerShell ou hello CLI.
Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>modèle de déploiement Azure Resource Manager
Une des deux [modèles de déploiement](resource-manager-deployment-model.md) utilisé toodeploy de ressources Microsoft Azure (hello autres est le modèle de déploiement classique hello). Certains services Azure prend en charge uniquement les modèles de déploiement Resource Manager hello, certains prennent en charge uniquement le modèle de déploiement classique hello et certains prennent en charge les deux. documentation Hello pour chaque service Azure Spécifie l’ou les modèles pris en charge.

## <a name="fault-domain"></a>domaine d’erreur
Hello collection d’ordinateurs virtuels dans un ensemble de disponibilité peut échouer à hello même temps. Exemple : un groupe de machines dans un rack partageant une source d’alimentation et un commutateur réseau communs. Dans Azure, les machines virtuelles de hello dans un ensemble de disponibilité sont automatiquement séparés dans plusieurs domaines d’erreur.  
Consultez [gérer la disponibilité des machines virtuelles Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [gérer la disponibilité hello des ordinateurs virtuels Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>zone géographique
Une limite définie pour la résidence des données qui couvre généralement deux ou plusieurs régions. limites de Hello peuvent être dans ou au-delà des frontières nationales et sont influencées par le règlement de taxe. Chaque zone géographique couvre au moins une région. L’Asie-Pacifique et le Japon en sont des exemples. Également appelé *géographie*.  
Voir [Régions Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>géoréplication
processus de Hello de réplication automatiquement du contenu tels que les objets BLOB, tables et files d’attente au sein d’une paire régionale.  
Voir [Géo-réplication active pour Azure SQL Database](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>image
Un fichier qui contient de système d’exploitation de hello et configuration de l’application qui peut être utilisé toocreate n’importe quel nombre d’ordinateurs virtuels. Deux types d’images peuvent être utilisés dans Azure : l’image de machine virtuelle et l’image du système d’exploitation. Une image de machine virtuelle inclut un système d’exploitation et tous les disques attachés tooa virtuels lors de la création d’image de hello. Une image du système d’exploitation contient uniquement un système d’exploitation généralisé sans aucune configuration du disque de données.  
Consultez [naviguer et sélectionnez images de machine virtuelle Windows dans Azure avec PowerShell ou hello CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>limites
nombre de Hello de ressources qui peuvent être créés ou hello banc d’essai des performances qui peut être obtenue. Les limites sont généralement associées aux abonnements ainsi qu’aux services et aux offres.  
Voir [Abonnement Azure et limites, quotas et contraintes de service](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>équilibreur de charge
Une ressource qui répartit le trafic entrant sur les ordinateurs d’un réseau. Dans Azure, un équilibreur de charge distribue les machines de toovirtual trafic définis dans un jeu d’équilibrage de charge. Un [équilibreur de charge](load-balancer/load-balancer-overview.md) peut être interne ou accessible sur Internet.  

## <a name="mobile-app"></a>application mobile
Autre nom pour [application App Service](#app-service-app).

## <a name="offer"></a>offer
Hello tarification, de crédits mensuels et de la terminologie de tooan applicable abonnement Azure.  
Consultez hello [page de détails de l’offre Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portail
portail web sécurisée de Hello utilisé toodeploy et gérer les services Azure.  Il existe deux portails : hello [portail Azure](http://portal.azure.com/) et hello [portail classic](http://manage.windowsazure.com/). Certains services sont disponibles dans les deux portails, tandis que d’autres sont uniquement disponibles dans un ou autres hello. Hello [graphique de la disponibilité de portail Azure](https://azure.microsoft.com/features/azure-portal/availability/) répertorie les services qui sont disponibles dans le portail.

## <a name="region"></a>region
Une zone à l’intérieur d’une zone géographique qui ne dépasse pas les frontières nationales et contient un ou plusieurs centres de données. Tarification, services régionaux et les types d’offres sont exposés au niveau de la région de hello. Une région est généralement associée à une autre région, qui peut être des tooseveral centaines miles immédiatement. Les paires régionales peuvent servir dans des scénarios de récupération d’urgence et de haute disponibilité. Également appelée tooas *emplacement*.  
Voir [Régions Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>resource
Un élément qui fait partie de votre solution Azure. Chaque service Azure vous permet de toodeploy différents types de ressources, telles que les bases de données ou des machines virtuelles.   
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>resource group
Un conteneur dans Azure Resource Manager réunissant les ressources associées d’une application. groupe de ressources Hello peut inclure toutes les ressources hello pour une application, ou uniquement les ressources qui sont regroupés logiquement. Vous pouvez décider comment vous souhaitez que les ressources de tooallocate tooresource groupes en fonction de ce que hello plus logique pour votre organisation.  
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>modèle Azure Resource Manager
Un fichier JSON qui définit de manière déclarative un ou plusieurs ressources Azure et qui définit les dépendances entre hello déployé des ressources. modèle de Hello peut être utilisé toodeploy hello ressources régulièrement et à plusieurs reprises.  
Voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>fournisseur de ressources
Service qui fournit des ressources de hello, vous pouvez déployer et gérer par le biais du Gestionnaire de ressources. Chaque fournisseur de ressources offre des opérations pour l’utilisation des ressources hello qui sont déployés. Fournisseurs de ressources sont accessibles via hello portail Azure, Azure PowerShell et plusieurs SDK de programmation.  
Voir [Présentation d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>role
Un moyen de contrôle d’accès qui peuvent être attribuées toousers, des groupes et des services. Les rôles sont en mesure de tooperform des actions telles que créer, gérer et de lecture sur les ressources Azure.  
Voir [RBAC : rôles intégrés](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>Contrat de Niveau de Service (SLA)
accord Hello qui décrit les engagements de Microsoft pour la connectivité et le temps d’activité. Chaque service Azure dispose d’un contrat SLA spécifique.  
Voir [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>signature d’accès partagé (SAP)
Une signature qui vous permet de ressource de tooa accès toogrant limitée, sans exposer votre clé de compte. Par exemple, [le stockage Azure utilise SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant client accès tooobjects tels que des objets BLOB. [IoT Hub utilise SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) télémétrie de toosend toogrant périphériques autorisation.

## <a name="storage-account"></a>compte de stockage
Un compte qui vous donne accès toohello des services Azure Blob, file d’attente, Table et fichier dans le stockage Azure. nom de compte de stockage Hello définit hello l’espace de noms unique pour les objets de données de stockage Azure.  
Voir [À propos des comptes de stockage Azure](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>abonnement
Accord d’un client avec Microsoft qui leur permet de tooobtain Azure services. tarification d’abonnement Hello et les termes associés sont régies par offre hello choisi pour l’abonnement de hello.
Voir [Contrat d’abonnement à Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/) et [Association des abonnements Azure avec Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>tag
Un terme d’indexation qui vous permet de ressources toocategorize selon les exigences de tooyour pour gérer ou de facturation. Lorsque vous avez un ensemble complex de ressources, vous pouvez utiliser les balises toovisualize ces ressources de façon hello plus logique de hello. Par exemple, vous pouvez baliser des ressources qui servent un rôle similaire dans votre organisation ou appartiennent toohello même service.  
Consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>domaine de mise à jour
Hello collection d’ordinateurs virtuels dans un ensemble de disponibilité qui sont mis à jour à hello même temps. Machines virtuelles dans hello même domaine de mise à jour sont redémarrés ensemble pendant les maintenances planifiées. Azure ne redémarre jamais plus d’un domaine de mise à jour à la fois. Également appelée tooas un domaine de mise à niveau.  
Consultez [gérer la disponibilité des machines virtuelles Windows hello](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [gérer la disponibilité hello des ordinateurs virtuels Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>Machine virtuelle
Bonjour implémentation logicielle d’un ordinateur physique qui exécute un système d’exploitation. Plusieurs machines virtuelles peuvent s’exécuter simultanément sur hello même matériel. Dans Azure, les machines virtuelles sont disponibles en plusieurs tailles.  
Voir [Documentation sur les machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extension de machine virtuelle
Une ressource qui implémente les comportements ou des fonctionnalités soit aider d’autres programmes de travail ou un permettent de hello pour vous toointeract avec un ordinateur en cours d’exécution. Par exemple, vous pourriez utiliser hello VM accès extension tooreset ou modifier les valeurs de l’accès à distance sur une machine virtuelle Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Voir [À propos des extensions et des fonctionnalités des machines virtuelles (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [À propos des extensions et des fonctionnalités des machines virtuelles (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>Réseau virtuel
Un réseau qui assure la connectivité entre vos ressources Azure, isolé de tous les autres locataires Azure. Une [passerelle VPN Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) vous permet d’établir des connexions entre des réseaux virtuels et [entre un réseau virtuel et un réseau local](vpn-gateway/vpn-gateway-plan-design.md). Vous pouvez contrôler entièrement les blocs d’adresses IP hello, les paramètres DNS, les stratégies de sécurité et les tables d’itinéraires dans un réseau virtuel.  
Voir [Présentation du réseau virtuel](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Application web
Autre nom pour [application App Service](#app-service-app).

## <a name="see-also"></a>Voir aussi

* [Prise en main d’Azure](https://azure.microsoft.com/get-started/)
* [Centre de ressources du cloud](https://azure.microsoft.com/resources/)  
* [Azure pour vos applications métier](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure dans votre centre de données](https://azure.microsoft.com/overview/business-apps-on-azure/)

