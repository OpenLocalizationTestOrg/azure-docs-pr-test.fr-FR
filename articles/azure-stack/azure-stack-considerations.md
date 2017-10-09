---
title: "aaaKey les différences entre Azure et Azure pile lorsque vous utilisez les services et créez des applications | Documents Microsoft"
description: "Ce que vous devez tooknow lorsque vous utilisez des services ou créez des applications pour Azure pile."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: c81f551d-c13e-47d9-a5c2-eb1ea4806228
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: twooley
ms.openlocfilehash: e302f20aeb3c74f944cb3daaee7e0db073ab5bfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>Considérations importantes : utilisation de services ou génération d’applications pour Azure Stack

Lorsque vous utilisez des services ou générez des applications pour Azure Stack, vous devez comprendre qu’il existe des différences entre Azure Stack et Azure. Cet article fournit des considérations relatives à la clé par une vue d’ensemble de hello lorsque vous ciblez la pile de Azure comme environnement de développement de cloud hybride.

## <a name="overview"></a>Vue d'ensemble

Azure Stack est une plateforme cloud hybride qui vous permet d’utiliser les services Azure à partir du centre de données de votre entreprise ou de votre fournisseur de services. En tant que développeur, vous pouvez générer des applications qui s’exécutent sur Azure Stack. Vous pouvez ensuite déployer ces tooAzure applications pile, tooAzure, ou vous pouvez générer réellement les applications hybrides qui tirent parti de connectivité hello entre un cloud de la pile d’Azure et le Azure.

Votre administrateur du cloud Azure pile ou un fournisseur de services sera vous permettent de connaître les services qui sont disponibles pour vous toouse, et comment tooget prennent en charge. Il propose ces services par le biais de ses offres et plans personnalisés.

Hello contenu technique Azure suppose que les applications sont développées pour un service Azure au lieu de la pile de Azure. Lorsque vous générez et déployez des applications tooAzure pile, vous devez comprendre les différences clés, telles que :

* Pile Azure fournit un sous-ensemble de services de hello et les fonctionnalités qui sont disponibles dans Azure.
* Votre entreprise ou fournisseur de services permettre choisir les services qu’ils souhaitent toooffer. Cela inclut des services ou des applications personnalisés.
* Vous devez utiliser hello corriger les points de terminaison Azure pile spécifique (par exemple, les URL de hello pour l’adresse de portail hello et le point de terminaison hello Azure Resource Manager).
* Vous devez utiliser des versions de PowerShell et d’API qui sont prises en charge par Azure Stack. Ceci permet de s’assurer que vos applications fonctionnent dans Azure Stack et Azure.

## <a name="cheat-sheet-high-level-differences"></a>Aide-mémoire : principales différences

Hello tableau suivant décrit les différences de haut niveau hello entre la pile d’Azure et Azure. Gardez-les à l’esprit lorsque vous développez pour Azure Stack ou utilisez des services Azure Stack.

| Domaine | Azure (global) | Azure Stack |
| -------- | ------------- | ----------|
| Qui est en charge de son fonctionnement ? | Microsoft | Votre entreprise ou fournisseur de services.|
| Qui contactez-vous pour obtenir un support ? | Microsoft | Pour la prise en charge du Kit de développement de pile Azure, visitez hello [forums Microsoft](https://social.msdn.microsoft.com/Forums/home?forum=azurestack). Kit de développement hello étant un environnement d’évaluation, il n’existe aucune prise en charge officielle proposé par Microsoft prend en charge les Services (technique).
| Services disponibles | Consultez la liste des hello [produits Azure](https://azure.microsoft.com/services/?b=17.04b). Les services disponibles varient selon la région Azure. | Azure Stack prend en charge une partie des services Azure. <br><br>Les services réels varient en fonction de ce que votre entreprise ou fournisseur de services choisit toooffer.
| Point de terminaison Azure Resource Manager* | https://management.azure.com | Pour le kit de développement hello : https://management.local.azurestack.external
| URL du portail* | [https://portal.azure.com](https://portal.azure.com) | Pour le kit de développement hello : https://portal.local.azurestack.external
| Région | Vous pouvez sélectionner la région toodeploy à. | Pour le kit de développement hello région sera toujours **local**. <br><br>kit de développement Hello prend en charge qu’une seule région.
| Groupes de ressources | Un groupe de ressources peut s’étendre sur plusieurs régions. | Pour le kit de développement hello n'est qu’une seule région.
|Espaces de noms, types de ressources et versions d’API pris en charge | Hello plus récente (ou versions antérieures qui ne sont pas encore déconseillé). | Azure Stack prend en charge des versions spécifiques. Voir hello « Configuration requise » de cet article.
| | |

* Si vous êtes un opérateur cloud de pile d’Azure, consultez [à l’aide des portails d’administrateur et utilisateur hello dans Azure pile](azure-stack-manage-portals.md) pour plus d’informations sur les URL par administrateur hello portail et l’administrateur de point de terminaison de gestionnaire de ressources.

## <a name="helpful-tools-and-best-practices"></a>Outils utiles et meilleures pratiques
 
 Microsoft fournit plusieurs outils et des conseils qui vous aident lors du développement pour Azure Stack.

| Recommandation | Références | 
| -------- | ------------- | 
| Installez les outils appropriés hello sur votre station de travail du développeur. | - [Installer PowerShell](azure-stack-powershell-install.md)<br>- [Télécharger des outils](azure-stack-powershell-download.md)<br>- [Configurer PowerShell](azure-stack-powershell-configure-user.md)<br>- [Installer Visual Studio](azure-stack-install-visual-studio.md) 
| Passez en revue les informations sur les éléments suivants de hello :<br>- Considérations relatives au modèle Azure Resource Manager<br>-Comment toofind les modèles de démarrage rapide<br>-Utilisez un toohelp de module de stratégie vous utilisez Azure toodevelop pour la pile de Azure | [Développer pour Azure Stack](azure-stack-developer.md) | 
| Passez en revue et suivre les meilleures pratiques de hello pour les modèles. | [Modèles de démarrage rapide Resource Manager](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>Configuration requise pour la version

Azure Stack prend en charge des versions spécifiques d’Azure PowerShell et des API de service Azure. Vous devez utiliser tooensure versions prises en charge que votre application peut être déployée tooboth Azure pile et tooAzure.

toomake que que vous utilisez une version appropriée de Azure PowerShell, utilisez [profils de version d’API](azure-stack-version-profiles.md). toodetermine hello API version profil le plus récent que vous pouvez utiliser, vous devez savoir quelle build de pile de Azure que vous utilisez. Contactez votre administrateur Azure Stack pour obtenir ces informations.

>[!NOTE]
 Si vous utilisez hello Kit de développement de pile Azure, et vous disposez d’un accès administratif, consultez la section de « Déterminer la version actuelle de hello » de hello de [gérer les mises à jour](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version) toodetermine hello build de la pile de Azure.

Pour les autres API, exécutez hello suivant PowerShell commande toooutput hello espaces de noms, types de ressources et les versions d’API qui sont pris en charge dans votre abonnement Azure pile. Notez que des différences peuvent subsister au niveau de la propriété. (Pour cette commande toowork, vous devez avoir déjà [installé](azure-stack-powershell-install.md) et [configuré](azure-stack-powershell-configure-user.md) PowerShell pour un environnement de la pile de Azure. Vous devez également avoir une offre d’abonnement tooan pile d’Azure.)

 ```powershell
Get-AzureRmResourceProvider | Select ProviderNamespace -Expand ResourceTypes | Select * -Expand ApiVersions | `
Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} 
```

Exemple de sortie (tronquée) : ![Exemple de sortie de la commande Get-AzureRmResourceProvider](media/azure-stack-considerations/image1.png)
 
## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les différences au niveau du service, consultez :

* [Considérations relatives aux machines virtuelles dans Azure Stack](azure-stack-vm-considerations.md)
* [Considérations relatives au stockage dans Azure Stack](azure-stack-acs-differences.md)
* [Considérations relatives à la mise en réseau Azure Stack](azure-stack-network-differences.md)

