---
title: "résolution des problèmes de pile de Azure aaaMicrosoft | Documents Microsoft"
description: "Résolution des problèmes d’Azure Stack."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a20bea32-3705-45e8-9168-f198cfac51af
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: e274e92bc12fd6b7a2594f2f21b69ff0b9de594b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-troubleshooting"></a>Résolution des problèmes de Microsoft Azure Stack
Ce document fournit des informations de résolution des problèmes courants pour Azure Stack. 

Car hello Kit de développement Azure pile technique est proposé comme un environnement d’évaluation, il n’existe aucune prise en charge officielle de Support technique de Microsoft.  Si vous rencontrez un problème non documenté, assurez-vous que toocheck hello [Forum MSDN de pile Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) pour obtenir une assistance et des informations.  

recommandations Hello pour résoudre les problèmes qui sont décrits dans cette section proviennent de plusieurs sources et peuvent ou ne peuvent pas résoudre votre problème spécifique. Les exemples de code sont fournis en l’état et les résultats attendus ne sont pas garantis. Cette section est sujet toofrequent modifications et mises à jour en tant que produit de toohello améliorations sont implémentées.

## <a name="deployment"></a>Déploiement
### <a name="deployment-failure"></a>Échec du déploiement
Si vous rencontrez un problème lors de l’installation, vous pouvez utiliser hello exécuter à nouveau l’option d’utilisation de hello script toorestart hello déploiement à partir de l’étape qui a échoué hello.  


### <a name="at-hello-end-of-hello-deployment-hello-powershell-session-is-still-open-and-doesnt-show-any-output"></a>Extrémité hello du déploiement de hello, session de PowerShell hello est toujours ouverte et n’affiche pas de sortie
Ce comportement est probablement juste hello résultat du comportement par défaut de hello d’une fenêtre de commande PowerShell, lorsqu’il a été sélectionné. déploiement du kit de développement Hello a réussi, mais le script de hello a été suspendu lors de la sélection de fenêtre hello. Vous pouvez vérifier que cela vaut hello en recherchant des analyseurs de hello « select » dans hello de barre de titre de la fenêtre de commande hello.  Appuyez sur toounselect de clé hello ÉCHAP qu'et le message d’achèvement hello doivent être indiqué après celui-ci.

## <a name="templates"></a>Modèles
### <a name="azure-template-wont-deploy-tooazure-stack"></a>Modèle Azure ne déployer tooAzure pile
Vérifiez les points suivants :

* modèle de Hello doit utiliser un service Microsoft Azure qui est déjà disponible, ou en mode Aperçu dans la pile de Azure.
* Hello API utilisées pour une ressource spécifique est pris en charge par instance d’Azure pile locale hello et que vous ciblez un emplacement valide (« local » dans le kit de développement Azure pile vs hello « États-Unis » ou « Inde du Sud » dans Azure).
* Vous examinez [cet article](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md) sur les applets de commande Test-AzureRmResourceGroupDeployment de hello, qui catch petites différences dans la syntaxe du Gestionnaire de ressources Azure.

Vous pouvez également utiliser des modèles de pile de Azure hello déjà fournies dans hello [référentiel GitHub](http://aka.ms/AzureStackGitHub/) toohelp commencer.

## <a name="virtual-machines"></a>Machines virtuelles
### <a name="default-image-and-gallery-item"></a>Élément de la galerie et image par défaut
Vous devez d’abord ajouter un élément de la galerie et une image Windows Server pour pouvoir déployer des machines virtuelles dans Azure Stack.

### <a name="after-restarting-my-azure-stack-host-some-vms-may-not-automatically-start"></a>Après le redémarrage de l’hôte Azure Stack, certaines machines virtuelles ne démarrent pas automatiquement
Vous remarquerez peut-être que les services Azure Stack ne sont pas immédiatement disponibles après le redémarrage de votre hôte.  C’est parce que la pile Azure [infrastructure machines virtuelles](azure-stack-architecture.md#virtual-machine-roles) et RPs prendre un peu toocheck cohérence, mais qu’il démarre automatiquement par la suite.

Vous pouvez également remarquer ce locataire que machines virtuelles ne démarre pas automatiquement après un redémarrage de l’hôte de kit de développement de Azure pile hello.  Ceci est un problème connu et simplement requiert quelques étapes manuelles toobring en ligne :

1.  Sur l’hôte de kit de développement de Azure pile de hello, démarrez **Gestionnaire du Cluster de basculement** à partir du Menu Démarrer de hello.
2.  Cluster de hello sélectionnez **S-Cluster.azurestack.local**.
3.  Sélectionnez **Rôles**.
4.  Les machines virtuelles clientes apparaîtront avec l’état *enregistré*.  Une fois que tous les ordinateurs virtuels de Infrastructure sont en cours d’exécution, cliquez sur les machines virtuelles du locataire hello et sélectionnez **Démarrer** tooresume hello machine virtuelle.

### <a name="i-have-deleted-some-virtual-machines-but-still-see-hello-vhd-files-on-disk-is-this-behavior-expected"></a>J’a supprimé des ordinateurs virtuels, mais que vous rencontrez encore des fichiers de disque dur virtuel hello sur le disque. Ce comportement est-il attendu ?
Oui, c’est le comportement attendu. Il a été conçu ainsi pour les raisons suivantes :

* La suppression d’une machine virtuelle n’entraîne pas celle des VHD. Les disques sont des ressources distinctes dans le groupe de ressources hello.
* Lorsqu’un compte de stockage sera supprimé, suppression de hello est visible immédiatement via Azure Resource Manager (portail, PowerShell) mais il peut contenir des disques hello sont toujours conservés dans le stockage jusqu'à ce que le garbage collection s’exécute.

Si vous voyez des disques durs virtuels « orphelin », il est important tooknow si elles font partie du dossier hello pour un compte de stockage qui a été supprimé. Si le compte de stockage hello n’a pas été supprimé, il est normal qu’ils ont toujours lieu.

Vous pouvez en savoir plus sur la configuration de récupération de seuil et à la demande de rétention dans hello [gérer les comptes de stockage](azure-stack-manage-storage-accounts.md).

## <a name="storage"></a>Storage
### <a name="storage-reclamation"></a>Récupération du stockage
Cela peut prendre jusqu'à toofourteen heures tooshow capacité récupéré dans le portail de hello. La récupération d’espace dépend de différents facteurs, notamment le pourcentage d’utilisation des fichiers conteneurs internes dans le magasin d’objets blob de blocs. Par conséquent, selon la quantité de données est supprimé, il n’existe aucune garantie sur hello quantité d’espace qui peut être récupéré lorsque le garbage collector s’exécute.

## <a name="powershell"></a>PowerShell
### <a name="resource-providers-not-registered"></a>Fournisseurs de ressources non enregistrés
Lors de la connexion tootenant abonnements avec PowerShell, vous remarquerez cette ressource hello fournisseurs ne sont pas enregistrés automatiquement. Hello d’utilisation [module Connect](https://github.com/Azure/AzureStack-Tools/tree/master/Connect), ou hello exécution de commande suivante à partir de PowerShell (après avoir [installer et connecter](azure-stack-connect-powershell.md) en tant que client) : 
  
       Get-AzureRMResourceProvider | Register-AzureRmResourceProvider

## <a name="cli"></a>Interface de ligne de commande

* Il ne de Hello CLI en mode interactif Hello `az interactive` commande n’est pas encore prise en charge dans la pile de Azure.
* liste de hello tooget des images de machine virtuelle disponibles dans la pile d’Azure, utilisez hello `az vm images list --all` commande au lieu de hello `az vm image list` commande. En spécifiant hello `--all` option permet de s’assurer que réponse retourne uniquement les images hello qui sont disponibles dans votre environnement de la pile de Azure. 
* Alias d’image de machine virtuelle qui sont disponibles dans Azure ne peuvent pas être applicable tooAzure pile. Lors de l’utilisation des images de machine virtuelle, vous devez utiliser le paramètre d’URN entière hello (canoniques : UbuntuServer:14.04.3-LTS:1.0.0) au lieu de l’alias d’image hello. Et ce URNmust correspondent aux spécifications d’image hello dérivé hello `az vm images list` commande.
* Par défaut, CLI 2.0 utilise « Standard_DS1_v2 » comme taille de l’image par défaut machine virtuelle hello. Toutefois, cette taille n’est pas encore disponible dans la pile d’Azure, par conséquent, vous devez toospecify hello `--size` paramètre explicitement lors de la création d’un ordinateur virtuel. Vous pouvez obtenir la liste hello des tailles de machines virtuelles qui sont disponibles dans la pile d’Azure à l’aide de hello `az vm list-sizes --location <locationName>` commande.


## <a name="windows-azure-pack-connector"></a>Connecteur Windows Azure Pack
* Si vous modifiez hello mot de passe hello azurestackadmin compte après avoir déployé le kit de développement Azure pile, vous pouvez configurer n’est plus mode cloud multiples. Par conséquent, il ne sera environnement de Windows Azure Pack tooconnect possible toohello cible.
* Après avoir configuré le mode multicloud :
    * Un utilisateur peut voir tableau de bord hello uniquement une fois qu’ils réinitialiser les paramètres de portail hello. (Dans le portail de l’utilisateur hello, cliquez sur icône des paramètres de portail hello (icône d’engrenage dans le coin supérieur droit de hello). Sous **Restaurer les paramètres par défaut**, cliquez sur **Appliquer**.)
    * les titres de tableau de bord Hello peut ne pas apparaissent. Si ce problème se produit, vous devez les rajouter manuellement.
    * Des vignettes peut ne pas s’afficher correctement lorsque vous les ajoutez tout d’abord toohello le tableau de bord. toofix ce problème, actualisation hello navigateur.



