---
title: aaaLog dans tooAzure de hello CLI | Documents Microsoft
description: "Se connecter tooyour abonnement Azure à partir de hello Azure Interface de ligne (Azure) pour Windows, Linux et Mac"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Connectez-vous à tooAzure de hello CLI d’Azure
Hello CLI d’Azure est un ensemble de commandes open source, multiplateforme pour l’utilisation des ressources Azure. Cet article décrit tooprovide de différentes façons hello vos informations d’identification compte Azure tooconnect les tooyour de CLI d’Azure d’hello abonnement Azure :

* Exécutez hello `azure login` tooauthenticate de commande CLI via Azure Active Directory. Cette méthode vous donne accès tooCLI des commandes dans les deux [commande modes](#cli-command-modes). Lorsque vous exécutez la commande hello sans options supplémentaires, `azure login` vous invite toocontinue journalisation manière interactive via un portail web. Pour plus `azure login` options de commande, consultez les scénarios hello dans cet article, ou tapez `azure login --help`.
* Si vous devez uniquement les commandes de CLI du mode de gestion des services Azure toouse (non recommandés pour la plupart des nouveaux déploiements), vous pouvez télécharger et installer un fichier de paramètres de publication sur votre ordinateur.

Si vous n’avez pas déjà installé hello CLI, consultez [installation Bonjour Azure CLI](cli-install-nodejs.md). Si vous n’avez pas d’abonnement Azure, vous pouvez créer un [compte gratuit](http://azure.microsoft.com/free/) en quelques minutes.

Pour obtenir des informations sur les différentes identités de comptes et des différents abonnements Azure, consultez la rubrique [Association des abonnements Azure avec Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Scénario 1 : connexion à Azure avec une connexion interactive
Avec certains comptes, hello CLI requiert que vous toorun `azure login` , puis continuer le processus de connexion hello avec un navigateur web via un portail web, un processus appelé *connexion interactive*. Une raison courante est lorsque vous avez un compte professionnel ou scolaire (également appelé un *compte professionnel*) qui a la valeur toorequire l’authentification multifacteur. Utilisez également une connexion interactive avec votre compte Microsoft, lorsque vous souhaitez que les commandes du mode toouse Gestionnaire de ressources.

Une connexion interactive est facile : type `azure login` --sans l’option--comme indiqué dans hello l’exemple suivant :

```
azure login
```                                                                                             

sortie de Hello apparaît hello suivant :

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Copiez le code hello proposé tooyou dans la sortie de la commande hello et ouvrez un toohttp://aka.ms/devicelogin navigateur ou une autre page, si spécifié. (Vous pouvez ouvrir un navigateur sur hello même ordinateur, ou sur un périphérique ou un autre ordinateur.) Entrez le code de hello et vous êtes invité à tooenter hello username et password pour l’identité de hello souhaité toouse. Lorsque ce processus terminé, interface de commande hello termine la connexion de hello. Le résultat suivant peut s'afficher :

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Avec la connexion interactive, l’authentification et l’autorisation sont effectuées à l’aide d’Azure Active Directory. Si vous utilisez une identité de compte Microsoft, les processus de connexion hello accède à votre domaine par défaut de Azure Active Directory. (Si vous disposez d’un compte Azure gratuit, Azure Active Directory a peut-être créé automatiquement un domaine par défaut pour votre compte.)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Scénario 2 : connexion à azure avec un nom d’utilisateur et un mot de passe
Hello d’utilisation `azure login` avec le nom d’utilisateur hello (`-u`) paramètre tooauthenticate toouse Professionnel ou scolaire de compte qui ne requiert pas l’authentification multifacteur. Vous êtes invité à la ligne de commande hello pour le mot de passe hello (ou vous pouvez éventuellement passer le mot de passe hello comme un paramètre supplémentaire de hello `azure login` commande). Hello exemple suivant passe hello les nom d’utilisateur d’un compte professionnel :

    azure login -u myUserName@contoso.onmicrosoft.com

Vous êtes ensuite invité à tooenter votre mot de passe :

    info:    Executing command login
    Password: *********

processus de connexion Hello puis se termine.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

S’il s’agit de votre première connexion avec ces informations d’identification, vous êtes invité tooverify que vous le souhaitez toocache un jeton d’authentification. Ce message se produit également si vous avez utilisé précédemment hello `azure logout` (décrite plus loin dans l’article de hello) de commande. l’exécution de cette invite pour les scénarios d’automatisation, toobypass `azure login` avec hello `-q` paramètre.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Scénario 3 : connexion à azure avec un principal du service
Si vous créez un principal de service pour une application Active Directory, et principal du service hello dispose des autorisations de votre abonnement, vous pouvez utiliser hello `azure login` principal du service de commande tooauthenticate hello. Selon votre scénario, vous pourriez fournir des informations d’identification de hello de principal du service hello en tant que paramètres explicites de hello `azure login` commande. Par exemple, hello commande suivante passe nom principal de service hello et l’ID du client Active Directory :

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Vous êtes ensuite invité à tooprovide hello mot de passe. Vous pouvez également fournissent des informations d’identification de hello via un code de script ou une application CLI, ou utiliser un principal de service de certificat tooauthenticate hello non interactive pour les scénarios d’automatisation. Pour obtenir plus d’informations et des exemples, consultez l’article [Authentification d’un principal du service à l’aide d’Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Scénario 4 : utilisation d’un fichier de paramètres de publication
Si vous avez besoin uniquement des commandes CLI (par exemple, toodeploy machines virtuelles Azure dans le modèle de déploiement classique hello) de toouse hello Azure Service Management en mode, vous pouvez vous connecter à l’aide d’un fichier de paramètres de publication. Cette méthode installe un certificat sur votre ordinateur local qui vous permet de tooperform des tâches de gestion pour tant que l’abonnement de hello et certificat de hello sont valides.

* **fichier de paramètres de publication hello de toodownload** pour votre compte, vérifiez que hello CLI est en mode de gestion de Service en tapant `azure config mode asm`. Ensuite, exécutez hello de commande suivante :

        azure account download

Cela ouvre votre navigateur par défaut et vous invite à toosign dans toohello [portail Azure classic](https://manage.windowsazure.com). Une fois que vous êtes connecté, un fichier `.publishsettings` se télécharge. Prenez note de son emplacement.

> [!NOTE]
> Si votre compte est associé à plusieurs clients Azure Active Directory, vous pouvez être demandées par invite tooselect qui Active Directory que vous souhaitez toodownload paramètres de publication de fichiers pour.
>
>

Une fois sélectionné à l’aide de la page de téléchargement hello, ou en visitant le portail Azure classic de hello, hello Active Directory sélectionné devient hello par défaut utilisé par le portail classique de hello et de la page de téléchargement. Une fois qu’une valeur par défaut a été établie, vous voyez le texte hello '**cliquez ici page de sélection de toohello tooreturn**' haut hello de page de téléchargement hello. Utilisez hello fourni la page de sélection de lien tooreturn toohello.

* **fichier de paramètres de publication de tooimport hello**, exécutez hello commande suivante :

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Après l’importation de vos paramètres de publication, vous devez supprimer hello `.publishsettings` fichier. Il n’est plus requis par hello CLI d’Azure et présente un risque de sécurité car elle peut être utilisé toogain accès tooyour abonnement.
>
>

## <a name="cli-command-modes"></a>Modes des commandes de l’interface de ligne de commande
Hello CLI d’Azure fournit deux modes de commande pour l’utilisation des ressources Azure, avec des ensembles de commandes différents :

* **Mode de gestionnaire de ressources** - pour l’utilisation des ressources Azure dans le modèle de déploiement du Gestionnaire de ressources hello. tooset ce mode, exécutez `azure config mode arm`.
* **Mode de gestion de service** - pour l’utilisation des ressources Azure dans le modèle de déploiement classique hello. tooset ce mode, exécutez `azure config mode asm`.

Lors de la première installation, hello version actuelle de hello que CLI est en mode de gestionnaire de ressources.

> [!NOTE]
> mode de gestionnaire de ressources Hello et mode de gestion de Service sont mutuellement exclusifs. Autrement dit, les ressources créées dans un mode ne peut pas être gérés à partir de hello autre mode.
>
>

## <a name="multiple-subscriptions"></a>Abonnements multiples
Si vous avez plusieurs abonnements Azure, la connexion tooAzure accorde l’accès tooall les abonnements associés à vos informations d’identification. Un abonnement est sélectionné comme valeur par défaut de hello et utilisé par hello CLI d’Azure lors des opérations. Vous pouvez afficher les abonnements de hello, y compris les abonnement par défaut actuel hello, à l’aide de hello `azure account list` commande. Cette commande retourne des informations similaires toohello qui suivent :

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Bonjour précédant la liste, hello **actuel** colonne indique l’abonnement par défaut actuel de hello Azure-sub-1. abonnement par défaut de toochange hello, utilisez hello `azure account set` de commandes et spécifier l’abonnement hello que vous souhaitez que la valeur par défaut de toobe hello. Par exemple :

    azure account set Azure-sub-2

Cela modifie hello par défaut abonnement tooAzure-sub-2.

> [!NOTE]
> La modification d’abonnement par défaut de hello prend effet immédiatement et est une modification globale ; Si vous les exécutez à partir de nouvelles commandes CLI d’Azure, hello même instance de ligne de commande ou une autre instance, utiliser le nouvel abonnement par défaut de hello.
>
>

Si vous souhaitez toouse un abonnement par défaut par hello CLI d’Azure, mais que vous ne souhaitez pas que par défaut en cours de toochange hello, vous pouvez utiliser hello `--subscription` l’option de commande hello et fournissez hello nom d’abonnement de hello vous souhaitez toouse pour l’opération de hello.

Une fois que vous êtes connecté tooyour abonnement Azure, vous pouvez commencer à l’aide de toowork de commandes hello CLI d’Azure avec des ressources Azure.

## <a name="storage-of-cli-settings"></a>Stockage des paramètres de l'interface de ligne de commande
Si vous vous connectez avec hello `azure login` commande ou l’importation des paramètres de publication, votre profil de l’interface CLI et les journaux sont stockés dans un `.azure` répertoire se trouve dans votre `user` active. Votre répertoire `user` est protégé par votre système d’exploitation. Toutefois, nous vous recommandons d’effectuer des étapes supplémentaires tooencrypt votre `user` active. Vous pouvez le faire dans hello suivant façons :

* Sous Windows, modifier les propriétés de l’annuaire hello ou utiliser BitLocker.
* Sur le Mac, activez FileVault pour le répertoire de hello.
* Sur Ubuntu, utiliser la fonctionnalité de répertoire d’accueil de chiffrement hello. Les autres versions de Linux offrent des fonctionnalités similaires.

## <a name="logging-out"></a>Déconnexion
toolog out, hello utilisez commande suivante :

    azure logout -u <username>

Si les abonnements hello associés hello compte sont uniquement authentifié auprès d’Active Directory, la déconnexion des informations d’abonnement hello suppressions à partir du profil local de hello. Toutefois, si un fichier de paramètres de publication a été importé également pour les abonnements de hello, déconnexion supprime Active Directory lié au informations du profil local de hello.

## <a name="next-steps"></a>Étapes suivantes
* toouse, commandes CLI d’Azure, voir [les commandes CLI d’Azure en mode de gestionnaire de ressources](virtual-machines/azure-cli-arm-commands.md) et [les commandes CLI d’Azure en mode de gestion des services](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn en savoir plus sur hello CLI d’Azure, télécharger le code source, signaler des problèmes, ou contribuent toohello projet, visitez hello [référentiel GitHub pour hello CLI d’Azure](https://github.com/azure/azure-xplat-cli).
* Si vous rencontrez des problèmes à l’aide de hello CLI d’Azure ou Azure, visitez hello [Forums Windows Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
