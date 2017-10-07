---
title: aaaAzure DevTest Labs FAQ | Documents Microsoft
description: "Trouver les réponses aux questions de toocommon Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>FAQ d’Azure DevTest Labs
Cet article répond aux questions hello plus fréquemment posées sur Azure DevTest Labs.

**Généralités**
## <a name="what-if-my-question-isnt-answered-here"></a>Que dois-je faire si je n’ai pas trouvé de réponse à ma question ici ?
Si votre question n’est pas répertoriée ici, faites-le-nous savoir pour que nous puissions vous aider à trouver une réponse.

* Publier une question sur hello [Disqus thread](#comments) à fin hello de ce forum aux questions et prendre contact avec l’équipe de Cache Azure hello et d’autres membres de la Communauté sur cet article.
* tooreach une audience plus large, publiez une question sur hello [forum Azure DevTest Labs MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)et de prendre contact avec l’équipe de Azure DevTest Labs hello et d’autres membres de la Communauté de hello.
* toomake une demande de fonctionnalité, envoyez votre toohello demandes et idées [Azure DevTest Labs User Voice](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Pourquoi dois-je utiliser Azure DevTest Labs ?
Azure DevTest Labs peut faire gagner du temps et de l’argent à votre équipe. Les développeurs peuvent créer leurs propres environnements à l’aide de plusieurs bases différentes et utiliser des artefacts tooquickly déployer et configurer des applications. À l’aide de formules et d’images personnalisées, les machines virtuelles peuvent être enregistrées en tant que modèles et reproduites facilement. En outre, les laboratoires offrent plusieurs stratégies configurables qui permettent aux administrateurs de laboratoire tooreduce déchets et gérer des environnements d’une équipe. Ces stratégies comprennent l’arrêt automatique, le seuil de coût, le nombre maximal de machines virtuelles par utilisateur et les tailles maximales de machine virtuelle. Pour obtenir une explication plus approfondie de Azure DevTest Labs, lisez hello [vue d’ensemble](devtest-lab-overview.md) ou Espion hello [vidéo de présentation](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>Que signifie « libre-service, sans problème » ?
« Sérénité, libre-service » signifie que les développeurs et testeurs créent leurs propres environnements en fonction des besoins, et les administrateurs ont la sécurité hello de savoir que Azure DevTest Labs permet de réduire des déchets et contrôler les coûts. Les administrateurs peuvent spécifier les tailles des machines virtuelles sont autorisées, nombre maximal de hello de machines virtuelles, et lorsque les ordinateurs virtuels sont démarrés et arrêtés. Azure DevTest Labs rend également les coûts de toomonitor facile et ensemble alertes toostay prenant en charge de l’utilisation des ressources de laboratoire de hello.

## <a name="how-can-i-use-azure-devtest-labs"></a>Comment puis-je utiliser Azure DevTest Labs ?
Azure DevTest Labs est utile à tout moment nécessitent de développement ou d’environnements de test et que vous souhaitez tooreproduce les rapidement et/ou les gérer avec les stratégies de réduction des coûts.

Voici quelques scénarios pour lesquels nos clients utilisent Azure DevTest Labs :

* La gestion des environnements de développement et de test dans un seul emplacement, en utilisant des images personnalisées tooshare et stratégies tooreduce coût des builds sur team de hello.
* Développement d’une application en utilisant l’état de disque des images personnalisées toosave hello tout au long des étapes du développement hello.
* Le suivi des coûts hello dans tooprogress de relation.
* Création d’environnements de test en série pour des tests d’assurance qualité.
* À l’aide des artefacts et des formules tooeasily de configurer et de reproduire une application sur différents environnements.
* Distribution des machines virtuelles pour hackathons (travail de test ou de développement collaboratif) et puis facilement l’annulation du déploiement les lors de la fin de l’événement de hello.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Combien me coûte Azure DevTest Labs ?
Azure DevTest Labs est un service gratuit, ce qui signifie que les ateliers pratiques de création et la configuration des artefacts, modèles et des stratégies de hello sont libre. Vous payez uniquement pour hello des ressources Azure utilisées dans vos laboratoires, tels que les ordinateurs virtuels, des comptes de stockage et des réseaux virtuels. Pour plus d’informations sur le coût de hello des ressources de laboratoire, en savoir plus sur [tarification d’Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Sécurité**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Quelles sont les hello différents niveaux de sécurité dans Azure DevTest Labs ?
L’accès à la sécurité est déterminé par le [contrôle d’accès en fonction du rôle (RBAC) d’Azure](../active-directory/role-based-access-built-in-roles.md). toounderstand comment accéder aux fonctionne, il vous permet de toounderstand hello différences entre une autorisation, un rôle et une étendue définie par RBAC.

* **Autorisation** -une autorisation est une action spécifique de tooa accès définie. Par exemple, une autorisation peut être virtuels tooall d’accès en lecture.
* **Rôle** -un rôle est un jeu d’autorisations qui peuvent être regroupées et tooa utilisateur attribué. Par exemple, un « propriétaire » dispose des ressources de tooall d’accès au sein d’un abonnement.
* **Étendue** -une étendue est un niveau de hiérarchie hello de ressources Azure. Par exemple, une étendue peut être un groupe de ressources ou un seul laboratoire ou hello tout abonnement.

Étendue hello d’Azure DevTest Labs, il existe deux types d’autorisations de rôles toodefine utilisateur : propriétaire du lab et l’utilisateur de laboratoire.

* **Propriétaire du lab** -propriétaire d’un lab dispose des ressources de tooany d’accès hello dans lab de hello. Par conséquent, ils peuvent modifier des stratégies, lire et écrire les machines virtuelles, modifier le réseau virtuel de hello et ainsi de suite.
* **Utilisateur de laboratoire** : un utilisateur de laboratoire peut afficher toutes les ressources de laboratoire, telles que les machines virtuelles, les stratégies et les réseaux virtuels, mais il ne peut pas modifier les stratégies ou les machines virtuelles créées par d’autres utilisateurs. Il est également possible toocreate des rôles personnalisés dans Azure DevTest Labs, et vous pouvez apprendre comment toodo dans l’article hello, [accorder des autorisations utilisateur stratégies de laboratoire toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Étant donné que les étendues sont hiérarchiques, lorsqu’un utilisateur dispose d’autorisations pour une certaine étendue, il reçoit automatiquement ces autorisations pour chaque niveau d’étendue inférieur englobé. Par exemple, si un utilisateur est affecté le rôle toohello de propriétaire de l’abonnement, puis ils ont tooall d’accéder aux ressources dans un abonnement. Ces ressources incluent toutes les machines virtuelles, tous les réseaux virtuels et tous les laboratoires. Par conséquent, un propriétaire d’abonnement hérite automatiquement de rôle hello du propriétaire de laboratoire. Toutefois, hello inverse n’est pas vrai. Propriétaire d’un laboratoire a lab accès tooa, qui est une étendue inférieure à un niveau d’abonnement hello. Par conséquent, un propriétaire du lab n’est pas en mesure de toosee virtuels ou réseaux virtuels ou toutes les ressources qui sont en dehors de l’atelier de hello.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Comment créer un tooperform aux utilisateurs de tooallow rôle une tâche spécifique ?
Un article complet sur comment toocreate des rôles personnalisés et affecter des autorisations toothat rôle se trouve ici. Voici un exemple de script qui crée le rôle de hello « DevTest Labs avancé utilisateur », qui a l’autorisation toostart et arrêtez tous les ordinateurs virtuels dans le laboratoire de hello :

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Automatisation et intégration CI/CD**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Azure DevTest Labs est-il intégré à ma chaîne d’outils CI/CD ?
Si vous utilisez VSTS, il existe un [extension d’Azure DevTest Labs tâches](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) qui vous permet de tooautomate votre version de pipeline dans Azure DevTest Labs. Voici quelques-unes des utilisations hello de cette extension :

* Création et déploiement d’une machine virtuelle automatiquement et configurer avec la build la plus récente hello à l’aide de tâches de copie des fichiers Azure ou de PowerShell VSTS.
* Capturer automatiquement l’état de hello d’une machine virtuelle après le test tooreproduce un bogue sur hello même machine virtuelle pour un examen approfondi.
* Machine virtuelle à fin hello Hello suppression hello libérer pipeline lorsqu’il n’est plus nécessaire.

Hello billets de blog suivants fournissent des instructions et des informations sur l’utilisation d’extension VSTS hello :

* [General availability of Azure DevTest Labs – VSTS extension (Disponibilité générale d’Azure DevTest Labs - extension VSTS)](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Deploying a new VM in an existing AzureDevTestLab from VSTS (Déploiement d’une nouvelle machine virtuelle dans un AzureDevTestLab existant depuis VSTS)](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [À l’aide de VSTS Release Management pour les déploiements en continu tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Pour les autres toolchains CI/CD, hello tous les mentionné précédemment scénarios qui peuvent être réalisées via hello extension des tâches VSTS peut être obtenue de la même façon via le déploiement [modèles Azure Resource Manager](https://aka.ms/dtlquickstarttemplate) à l’aide de [ Applets de commande PowerShell Azure](../azure-resource-manager/resource-group-template-deploy.md) et [SDK .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). Vous pouvez également utiliser [API REST pour DevTest Labs](http://aka.ms/dtlrestapis) toointegrate avec votre chaîne d’outils.  


**Machines virtuelles**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Pourquoi ne puis-je pas voir certaines machines virtuelles dans le panneau des Machines virtuelles Azure hello que je vois dans Azure DevTest Labs ?
Lorsqu’un ordinateur virtuel est créé dans Azure DevTest Labs, autorisation est donné tooaccess cette machine virtuelle. Vous êtes en mesure de tooview il à la fois dans le panneau de laboratoires hello et hello **virtuels** panneau. Les utilisateurs de hello DevTest Labs rôle peuvent voir tous les ordinateurs virtuels créés dans le laboratoire hello par le biais du laboratoire hello **toutes les Machines virtuelles** panneau. Toutefois, les utilisateurs de hello DevTest Labs rôle ne bénéficient pas automatiquement les ressources avec accès en lecture tooVM qu’ils ont créés. Par conséquent, ces machines virtuelles ne sont pas affichés dans hello **virtuels** panneau.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Qu’est la différence de hello entre des images personnalisées et les formules ?
Une image personnalisée est un disque dur virtuel, alors qu’une formule est une image que vous pouvez configurer avec des paramètres supplémentaires que vous pouvez enregistrer et reproduire. Une image personnalisée peut être préférable tooquickly créer plusieurs environnements avec hello même image de base, immuable. Une formule peut être préférable si vous souhaitez que la configuration de hello tooreproduce de votre machine virtuelle avec les dernières informations hello, un réseau virtuel/sous-réseau ou une taille spécifique. Pour obtenir une explication plus approfondie, consultez l’article hello, [comparaison des images personnalisées et les formules de DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Comment créer plusieurs machines virtuelles à partir de hello même modèle à la fois ?
Vous pouvez utiliser hello [VSTS tâches extension](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) ou [générer un modèle Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) lors de la création d’une machine virtuelle et [déployer le modèle de gestionnaire de ressources Azure hello à partir de Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Comment puis-je déplacer mes machines virtuelles Azure existantes dans mon laboratoire Azure DevTest Labs ?
Suivez les étapes de hello ci-dessous toocopy votre tooAzure de machines virtuelles DevTest Labs existant :

1. Copier le fichier VHD hello de votre machine virtuelle existante, l’utilisation de cette [script Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Créer l’image personnalisée de hello](devtest-lab-create-template.md) à l’intérieur de votre laboratoire Azure DevTest Labs.
3. Créer une machine virtuelle dans le laboratoire hello à partir de votre image personnalisée

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>Puis-je attacher plusieurs disques toomy machines virtuelles ?
Attachement de plusieurs disques tooVMs est pris en charge.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Si je veux toouse une image de système d’exploitation Windows pour mes tests, dois-je toopurchase un abonnement MSDN ?
Si vous avez besoin d’images de système d’exploitation client Windows toouse (Windows 7 ou version ultérieure) pour votre développement ou des tests dans Azure, puis Oui, vous devez :

- [Achetez un abonnement MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Si vous avez un contrat entreprise, créez un abonnement Azure avec hello [offre de développement et de Test entreprise](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Pour plus d’informations sur hello crédits Azure pour chaque offre MSDN, consultez [crédit Azure mensuel pour les abonnés de Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Comment automatiser les processus de hello de téléchargement des images de disque dur virtuel fichiers toocreate personnalisées ?
Nous avons deux options :

* [AzCopy Azure](../storage/common/storage-use-azcopy.md#blob-upload) peut être utilisé toocopy ou télécharger le compte de stockage toohello fichiers VHD associé lab de hello.
* [L’Explorateur Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome qui s’exécute sur Windows, OSX et Linux.   

compte de stockage de destination hello toofind associé à votre laboratoire, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **groupes de ressources** à partir du volet de gauche hello.
3. Recherchez et sélectionnez le groupe de ressources hello associé à votre laboratoire.
4. Sur hello **vue d’ensemble** panneau, sélectionnez un des comptes de stockage hello.
5. Sélectionnez **Objets Blob**.
6. Recherchez les téléchargements dans la liste de hello. Si aucune n’existe, retourner tooStep #4 et essayer un autre compte de stockage.
7. Hello d’utilisation **URL** comme destination dans votre commande AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Comment puis-je automatiser des processus hello de la suppression de hello toutes les machines virtuelles dans mon laboratoire ?
En outre toodeleting machines virtuelles à partir de votre laboratoire Bonjour portail Azure, vous pouvez supprimer toutes les machines virtuelles de hello dans votre laboratoire à l’aide d’un script PowerShell. Bonjour exemple, modifier les valeurs de paramètre hello sous hello **toochange de valeurs** commentaire. Vous pouvez récupérer hello `subscriptionId`, `labResourceGroup`, et `labName` valeurs hello lab du Panneau de hello portail Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Artefacts**
## <a name="what-are-artifacts"></a>Que sont les artefacts ?
Les artefacts sont des éléments personnalisables qui peuvent être utilisé toodeploy vos éléments les plus récents ou votre développement Outils sur une machine virtuelle. Ils sont attaché tooyour machine virtuelle lors de la création en quelques clics simples, et une fois que hello machine virtuelle est configurée, les artefacts hello déploiement et configurer votre machine virtuelle. Il existe divers artefacts préexistants dans notre [référentiel GitHub public](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), mais vous pouvez également [créer vos propres artefacts](devtest-lab-artifact-author.md) facilement.


**Configuration du labo**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Comment puis-je créer un laboratoire à partir d’un modèle Azure Resource Manager ?
Nous vous avons fourni un [référentiel GitHub de modèles Azure Resource Manager de laboratoire](https://aka.ms/dtlquickstarttemplate) que vous pouvez déployer en tant que-est ou modifiez toocreate des modèles personnalisés pour vos laboratoires. Chacun de ces modèles a un lien que vous pouvez cliquer sur toodeploy pratiques hello-est sous votre propre abonnement Azure, ou vous pouvez personnaliser le modèle de hello et [déployer à l’aide de PowerShell ou CLI d’Azure](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Pourquoi mes machines virtuelles sont-elles créées dans différents groupes de ressources avec des noms arbitraires ? Puis-je renommer ou modifier ces groupes de ressources ?
Groupes de ressources sont créés de cette manière des autorisations d’utilisateur Azure DevTest Labs toomanage hello et accès toovirtual machines. Pendant que vous pouvez déplacer le groupe de ressources tooanother hello machine virtuelle avec le nom souhaité, il donc n’est pas recommandé. Nous travaillons sur l’amélioration de ce tooallow expérience plus de souplesse.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Laboratoires combien puis-je créer sous hello même abonnement ?
Il n’existe aucune limite spécifique sur nombre hello de laboratoires qui peuvent être créés par abonnement. Toutefois, les ressources hello utilisées sont limités par abonnement. Vous pouvez lire sur hello [les quotas et limites imposées aux abonnements Azure](../azure-subscription-service-limits.md) et [comment tooincrease ces limites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Combien de machines virtuelles puis-je créer par laboratoire ?
Il n’existe aucune limite spécifique sur nombre hello de machines virtuelles qui peuvent être créés par le laboratoire. Toutefois, les ressources hello utilisées sont limités par abonnement (par exemple, des cœurs de machine virtuelle, des adresses IP publiques, etc..). Vous pouvez lire sur hello [les quotas et limites imposées aux abonnements Azure](../azure-subscription-service-limits.md) et [comment tooincrease ces limites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Comment faire pour partager un laboratoire toomy de lien direct
tooshare un lien direct tooyour les utilisateurs du laboratoire, vous pouvez effectuer hello procédure :

1. Parcourir lab toohello Bonjour portail Azure.
2. Copier l’URL de laboratoire hello depuis votre navigateur et le partager avec vos utilisateurs de laboratoire.

> [!NOTE]
> Si vos utilisateurs lab sont des utilisateurs externes avec une [compte Microsoft](#what-is-a-microsoft-account) et ils n’appartiennent pas Active Directory de la société tooyour, il peuvent recevoir une erreur lors de la navigation de lien de toohello fourni. S’ils reçoivent une erreur, demandez-leur tooclick hello de leur nom dans le coin supérieur droit de hello du portail Azure et répertoire hello sélectionnez où lab de hello existe à partir de hello **répertoire** section du menu de hello.
>
>

## <a name="what-is-a-microsoft-account"></a>Qu’est-ce qu’un compte Microsoft ?
Vous utilisez un compte Microsoft pour la plupart des opérations effectuées avec les services et les périphériques Microsoft. Il s’agit d’une adresse de messagerie et le mot de passe que vous utilisez toosign dans tooSkype, Outlook.com, OneDrive, Windows Phone et Xbox LIVE : cela signifie que les fichiers, des photos, des contacts et paramètres vous peuvent suivre tooany appareil.

> [!NOTE]
> Compte Microsoft utilisé toobe appelé « Windows Live ID ».
>
>


**Dépannage**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Mon artefact a échoué lors de la création d’une machine virtuelle. Comment puis-je résoudre ce problème ?
Consultez trop[comment toodiagnose les échecs d’artefact dans DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn comment tooobtain journaux concernant votre artefact ayant échoué.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Pourquoi mon réseau virtuel existant n’est pas enregistré correctement ?
Il se peut que votre nom de réseau virtuel contienne des points. Si, par conséquent, essayez de supprimer hello des points ou en les remplaçant par des traits d’union, puis recommencez l’enregistrement hello nouveau réseau virtuel.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Pourquoi l’erreur signalant que la ressource parente est introuvable s’affiche t-elle lors de l’approvisionnement d’une machine virtuelle à partir de PowerShell ?
Lorsqu’une ressource est une ressource de tooanother parent, ressource parente de hello doit exister avant de créer la ressource de hello enfant. Si ce n’est pas cas, vous recevez une erreur **ParentResourceNotFound**. Si vous ne spécifiez pas une dépendance sur la ressource parent de hello, ressource enfant de hello peut être déployé avant le parent de hello.

Les machines virtuelles sont des ressources enfants se trouvant dans un laboratoire d’un groupe de ressources. Lorsque vous utilisez toodeploy de modèles Azure Resource Manager via PowerShell, nom de groupe de ressources hello prévue hello script PowerShell doit être le nom du groupe de ressources de laboratoire de hello hello. Pour plus d’informations, consultez la rubrique [Résolution des erreurs courantes dans des déploiements Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Où puis-je trouver plus d’informations d’erreur si le déploiement d’une machine virtuelle échoue ?
Erreurs de déploiement de machine virtuelle sont capturées dans les journaux d’activité hello. Vous pouvez trouver lab journal d’activité de machines virtuelles via hello **journaux d’Audit** ou **diagnostics de machine virtuelle** dans le menu de ressource hello dans Panneau de la machine virtuelle du laboratoire hello (Panneau de hello affiche après avoir sélectionné hello machine virtuelle à partir de **Mes machines virtuelles** liste).

Erreur de déploiement hello se produit parfois, avant le démarrage de hello déploiement des ordinateurs virtuels - telles que lorsque la limite d’abonnement hello pour une ressource créée avec hello machine virtuelle est atteinte. Dans ce cas, les détails de l’erreur hello sont capturées au niveau de lab hello **journaux d’activité** qui peut être rechercher bas hello hello **stratégies de Configuration et** paramètres. Pour plus d’informations sur l’utilisation d’activité consigne dans Azure, consultez [affichage des journaux d’activité tooaudit des actions sur les ressources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
