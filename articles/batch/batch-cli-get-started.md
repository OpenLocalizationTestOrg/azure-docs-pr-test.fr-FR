---
title: "aaaGet main CLI d’Azure pour le traitement par lots | Documents Microsoft"
description: "Obtenir une brève introduction commandes de traitement par lots toohello CLI d’Azure pour la gestion des ressources de service Azure Batch"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Gérer les ressources Batch avec Azure CLI

Bonjour Azure CLI 2.0 est la nouvelle expérience de ligne de commande de Azure pour la gestion des ressources Azure. Elle peut être utilisée sur macOS, Linux et Windows. Azure CLI 2.0 est optimisé pour gérer et administrer les ressources Azure à partir de la ligne de commande hello. Vous pouvez utiliser hello CLI d’Azure toomanage votre compte Azure Batch et vos ressources toomanage tels que les pools, les travaux et les tâches. Avec hello CLI d’Azure, vous pouvez générer des scripts nombreux hello mêmes tâches mener avec hello API de lot, le portail Azure et les applets de commande PowerShell de lot.

Cet article fournit une vue d’ensemble de l’utilisation de [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) avec Batch. Consultez [prise en main Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) pour une vue d’ensemble de l’utilisation de hello CLI avec Azure.

Microsoft recommande d’utiliser la version la plus récente hello Hello CLI d’Azure, version 2.0. Pour plus d’informations sur la version 2.0, consultez [Azure CLI 2.0 à présent disponible de façon généralisée](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Configurer hello CLI d’Azure

tooinstall hello CLI d’Azure, suivez les instructions de hello dans [installation Bonjour Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Nous recommandons que vous mettez à jour votre installation du CLI d’Azure fréquemment tootake parti du service mises à jour et améliorations.
> 
> 

## <a name="command-help"></a>Aide relative aux commandes

Vous pouvez afficher le texte d’aide pour chaque commande Bonjour CLI d’Azure en ajoutant `-h` toohello commande. Ignorez les autres options. Par exemple :

* aide tooget hello `az` de commandes, entrez :`az -h`
* tooget une liste de toutes les commandes de traitement par lots Bonjour CLI, utilisez :`az batch -h`
* aide tooget sur la création d’un compte de traitement par lots, entrez :`az batch account create -h`

En cas de doute, utilisez hello `-h` aide des options de ligne de commande de tooget sur n’importe quelle commande CLI d’Azure.

> [!NOTE]
> Les versions antérieures de hello CLI d’Azure utilisé `azure` toopreface une commande CLI. Dans la version 2.0, toutes les commandes sont désormais précédées de `az`. Être tooupdate que vos scripts toouse hello nouvelle syntaxe avec la version 2.0.
>
>  

En outre, consultez la documentation de référence de CLI d’Azure de toohello pour plus d’informations sur les [les commandes CLI d’Azure pour le lot](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Connexion et authentification

toouse hello CLI d’Azure par lot, vous devez toolog dans et s’authentifier. Il existe deux étapes simples toofollow :

1. **Connectez-vous à Azure.** Connexion à Azure donne accéder aux commandes de gestionnaire de ressources tooAzure, y compris [service de gestion par lots](batch-management-dotnet.md) commandes.  
2. **Connectez-vous à votre compte Batch.** Connectez votre donne de compte de traitement par lots accéder aux commandes du service tooBatch.   

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Il existe quelques toolog de différentes façons dans Azure, décrit en détail dans [se connecter avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Connexion interactive](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Se connecter manière interactive lorsque vous exécutez les commandes CLI d’Azure vous-même à partir de la ligne de commande hello.
2. [Connexion avec un principal de service](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Connectez-vous avec un principal de service lorsque vous exécutez des commandes Azure CLI à partir d’un script ou d’une application.

Pour des raisons de hello de cet article, nous montrons comment toolog dans Azure interactivement. Type [ouverture de session az](https://docs.microsoft.com/cli/azure/#login) sur la ligne de commande hello :

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Hello `az login` retourne la commande jeton que vous pouvez utiliser tooauthenticate, comme indiqué ici. Suivez les instructions fournies de hello tooopen une page web et envoyer tooAzure de jeton hello :

![Connectez-vous à tooAzure](./media/batch-cli-get-started/az-login.png)

les exemples Hello répertoriés dans hello [exemples de scripts de shell](#sample-shell-scripts) section également afficher comment toostart votre session CLI d’Azure par la journalisation de manière interactive dans Azure. Une fois que vous êtes connecté, vous pouvez appeler toowork de commandes avec des ressources de gestion par lots, y compris des comptes Batch, les clés, les packages d’applications et quotas.  

### <a name="log-in-tooyour-batch-account"></a>Ouvrez une session dans tooyour compte Batch

toouse hello CLI d’Azure toomanage lot ressources, telles que les pools, tâches et les tâches, vous devez toolog dans votre compte Batch et s’authentifier. toolog dans toohello service Batch, utilisez hello [connexion au compte batch az](https://docs.microsoft.com/cli/azure/batch/account#login) commande. 

Deux options s’offrent à vous pour l’authentification sur votre compte Batch :

- **Via l’authentification Azure Active Directory (Azure AD)** 

    L’authentification auprès d’Azure AD est par défaut de hello lorsque vous utilisez hello CLI d’Azure par lot et recommandée pour la plupart des scénarios. 
    
    Lorsque vous connectez tooAzure interactivement, comme décrit dans la section précédente de hello, vos informations d’identification sont mis en cache, afin de hello CLI d’Azure peut connecter vous tooyour à l’aide de ces mêmes informations d’identification du compte Batch. Si vous vous connectez à l’aide d’un principal de service de tooAzure, ces informations d’identification sont également utilisé toolog dans tooyour compte Batch.

    L’avantage d’Azure AD est que le contrôle d’accès se fait en fonction du rôle (RBAC). Avec RBAC, l’accès des utilisateurs dépend de son rôle, plutôt qu’ou non qu’ils possèdent des clés de compte hello. Au lieu de gérer les clés de compte, vous pouvez gérer les rôles RBAC et permettre à Azure AD de gérer l’accès et l’authentification.  

    L’authentification auprès d’Azure AD est requis si vous avez créé votre compte Azure Batch avec son mode d’allocation de pool jeu too'User abonnement ». 

    toolog dans tooyour lot compte à l’aide d’Azure AD, appelez hello [connexion au compte batch az](https://docs.microsoft.com/cli/azure/batch/account#login) commande : 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Via l’authentification par clé partagée.**

    [L’authentification Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) utilise votre compte d’accès des clés tooauthenticate des commandes de CLI d’Azure pour hello par lots de service.

    Si vous créez des scripts CLI d’Azure tooautomate les commandes Batch appelant, vous pouvez utiliser l’authentification Shared Key, ou un principal de service Azure AD. Dans certains scénarios, le recours à l’authentification par clé partagée peut être plus simple que la création d’un principal de service.  

    toolog à l’aide de l’authentification Shared Key, inclure hello `--shared-key-auth` option de ligne de commande hello :

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

les exemples Hello répertoriés dans hello [exemples de scripts de shell](#sample-shell-scripts) section montrent comment toolog à votre compte de traitement par lots avec hello CLI d’Azure à la fois Azure AD et la clé partagée.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Utiliser des modèles d’interface CLI Azure Batch et le transfert de fichiers (préversion)

Vous pouvez utiliser hello CLI d’Azure toorun lot travaux de bout en bout sans écrire de code. Fichiers de modèle de traitement par lots prend en charge la création des regroupements, des travaux et des tâches avec hello CLI d’Azure. Vous pouvez également utiliser des fichiers d’entrée du travail tooupload CLI d’Azure hello toohello compte de stockage Azure associé hello compte Batch et télécharger des fichiers de sortie de projet à partir de celui-ci. Pour en savoir plus, consultez la section [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md) (Utiliser des modèles d’interface CLI Batch et de transfert de fichier (préversion)).

## <a name="sample-shell-scripts"></a>Exemples de scripts de l’interpréteur de commandes

exemples de scripts Hello répertoriées dans hello suivant tableau montrent fonctionnement des commandes avec le service de traitement par lots hello et tâches courantes de gestion par lots service tooaccomplish toouse CLI d’Azure. Ces exemples de scripts couvrent la plupart des commandes hello disponibles dans hello CLI d’Azure pour le traitement par lots. 

| Script | Remarques |
|---|---|
| [Création d’un compte Batch](./scripts/batch-cli-sample-create-account.md) | Crée un compte Batch et l’associe à un compte de stockage. |
| [Ajouter une application](./scripts/batch-cli-sample-add-application.md) | Ajoute une application et télécharge les fichiers binaires du package.|
| [Gérer les pools Batch](./scripts/batch-cli-sample-manage-pool.md) | Montre comment créer, redimensionner et gérer des pools. |
| [Exécuter un travail et des tâches avec Batch](./scripts/batch-cli-sample-run-job.md) | Montre comment exécuter un travail et ajouter des tâches. |

## <a name="json-files-for-resource-creation"></a>Fichiers JSON pour la création de ressources

Lorsque vous créez des ressources de traitement par lots telles que les pools et les travaux, vous pouvez spécifier un fichier JSON contenant hello nouvelle configuration de la ressource au lieu de passer de ses paramètres en tant qu’options de ligne de commande. Par exemple :

```azurecli
az batch pool create my_batch_pool.json
```

Si vous pouvez créer la plupart des ressources de traitement par lots à l’aide d’uniquement les options de ligne de commande, certaines fonctionnalités requièrent que vous spécifiez un fichier au format JSON contenant les détails de la ressource hello. Par exemple, vous devez utiliser un fichier JSON si vous souhaitez que les fichiers de ressources toospecify pour une tâche de démarrage.

toosee hello syntaxe JSON requis toocreate une ressource, consultez le toohello [référence de l’API REST de lot] [ rest_api] documentation. Chaque « ajouter *type de ressource*« rubrique de référence d’API REST de hello contient des exemples de scripts JSON pour la création de cette ressource. Vous pouvez utiliser ces exemples de scripts JSON en tant que modèles pour toouse de fichiers JSON avec hello CLI d’Azure. Par exemple, toosee hello syntaxe JSON pour la création du pool, consultez trop[ajouter un compte du pool de tooan][rest_add_pool].

Pour un exemple de script qui spécifie un fichier JSON, consultez [Exécuter un travail et des tâches avec Batch](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Si vous spécifiez un fichier JSON quand vous créez une ressource, tous les autres paramètres que vous spécifiez sur la ligne de commande hello pour cette ressource sont ignorés.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Requêtes efficaces pour les ressources Batch

Chaque type de ressource Batch prend en charge une commande `list` qui interroge votre compte Batch et répertorie les ressources de ce type. Par exemple, vous pouvez répertorier les pools hello dans vos tâches de compte et hello dans une tâche :

```azurecli
az batch pool list
az batch task list --job-id job001
```

Lorsque vous interrogez le service de traitement par lots hello avec un `list` opération, vous pouvez spécifier la durée hello OData clause toolimit des données retournées. Étant donné que tous les filtres produit côté serveur, uniquement les données hello demandé dépasse câble de hello. Utiliser ces clauses de bande passante toosave (et par conséquent, l’heure) lorsque vous effectuez des opérations de liste.

Hello tableau suivant décrit les clauses de OData hello pris en charge par hello service Batch :

| Clause | Description |
|---|---|
| `--select-clause [select-clause]` | Retourne un sous-ensemble de propriétés pour chaque entité. |
| `--filter-clause [filter-clause]` | Retourne seules les entités qui correspondent aux hello spécifié expression OData. |
| `--expand-clause [expand-clause]` | Obtient des informations d’entité hello dans un seul appel REST sous-jacente. Hello développez clause actuellement prend en charge uniquement hello `stats` propriété. |

Pour un exemple de script qui montre comment toouse une clause OData, consultez [exécuter un travail et des tâches de traitement par lots](./scripts/batch-cli-sample-run-job.md).

Pour plus d’informations sur l’exécution de requêtes de liste efficace avec les clauses d’OData, consultez [interroger le service de traitement par lots Azure hello efficacement](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Conseils de dépannage

Hello conseils suivants lors de la résolution des problèmes de CLI d’Azure :

* Utilisez `-h` tooget **texte d’aide** pour n’importe quelle commande CLI
* Utilisez `-v` et `-vv` toodisplay **verbose** sortie de commande. Hello lorsque `-vv` indicateur est inclus, hello CLI d’Azure affiche hello réels demandes et réponses REST. Ces commutateurs sont pratiques pour afficher une sortie complète des erreurs.
* Vous pouvez afficher **commande de sortie au format JSON** avec hello `--json` option. Par exemple, `az batch pool show pool001 --json` affiche les propriétés de pool001 au format JSON. Vous pouvez ensuite copier et modifier ce toouse de sortie dans un `--json-file` (consultez [fichiers JSON](#json-files) plus haut dans cet article).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Hello [forum de lot] [ batch_forum] est analysé par les membres de l’équipe par lots. Vous pouvez y publier vos questions si vous rencontrez des problèmes ou si vous avez besoin d’aide pour une opération spécifique.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur hello CLI d’Azure, consultez hello [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).
* Pour plus d’informations sur les ressources Batch, consultez [Vue d’ensemble d’Azure Batch pour les développeurs](batch-api-basics.md).
* Pour plus d’informations sur l’utilisation de pools de toocreate de modèles, les tâches et les tâches par lots sans écrire de code, consultez [Azure Batch CLI modèles et le transfert de fichiers (aperçu)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
