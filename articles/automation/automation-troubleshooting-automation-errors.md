---
title: "aaaTroubleshooting common Azure Automation émet | Documents Microsoft"
description: "Cet article fournit des informations toohelp dépanner et résoudre les erreurs courantes Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "erreur, dépannage, problème d’automation"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Dépannage des problèmes courants dans Azure Automation 
Cet article fournit une aide à résoudre les erreurs courantes, vous pouvez rencontrer dans Azure Automation et suggère des solutions possibles tooresolve les.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Erreurs d’authentification avec des runbooks Azure Automation
### <a name="scenario-sign-in-tooazure-account-failed"></a>Scénario : Échec de connexion tooAzure
**Erreur :** erreur hello « Unknown_user_type : Type inconnu d’utilisateur » lors de l’utilisation des applets de commande Add-AzureAccount ou AzureRmAccount de connexion hello.

**Erreur de hello :** cette erreur se produit si le nom de la ressource d’informations d’identification hello n’est pas valide ou si hello nom d’utilisateur et mot de passe que vous avez utilisé de ressource d’informations d’identification toosetup hello Automation ne sont pas valides.

**Conseils de dépannage :** dans commande toodetermine quel est le problème, prenez hello comme suit :  

1. Assurez-vous que vous n’avez pas de caractères spéciaux, y compris hello  **@**  caractère de nom d’élément multimédia hello Automation d’identification que vous utilisez tooconnect tooAzure.  
2. Vérifiez que vous pouvez utiliser le nom d’utilisateur hello et un mot de passe sont stockés dans les informations d’identification Azure Automation de hello dans votre éditeur de PowerShell ISE local. Pour cela, vous pouvez hello suivant d’applets de commande hello PowerShell ISE en cours d’exécution :  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Si l’authentification échoue localement, cela signifie que vous n’avez pas correctement configuré vos informations d’identification Azure Active Directory. Consultez trop[l’authentification à l’aide d’Azure Active Directory de tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) compte Azure Active Directory blog post tooget hello correctement configuré.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Scénario : Hello toofind Impossible abonnement Azure
**Erreur :** erreur hello « hello abonnement nommé ``<subscription name>`` est introuvable » lorsque vous travaillez avec les applets de commande Select-AzureSubscription ou sélectionnez-AzureRmSubscription hello.

**Erreur de hello :** cette erreur se produit si le nom de l’abonnement hello n’est pas valide ou si l’utilisateur d’Azure Active Directory hello qui essaie de détails de l’abonnement tooget hello n’est pas configuré en tant qu’administrateur d’abonnement de hello.

**Conseils de dépannage :** dans l’ordre toodetermine si vous avez correctement authentifiée tooAzure et que vous avez accès toohello abonnement à la tentative de tooselect, prendre un hello comme suit :  

1. Vérifiez que vous exécutez hello **Add-AzureAccount** avant d’exécuter hello **Select-AzureSubscription** applet de commande.  
2. Si vous voyez toujours ce message d’erreur, modifiez votre code en ajoutant hello **Get-AzureSubscription** applet de commande suivant hello **Add-AzureAccount** applet de commande, puis exécutez hello code.  À présent vérifier si hello sortie Get-AzureSubscription contient les détails de votre abonnement.  

   * Si vous ne voyez pas les détails de l’abonnement dans la sortie de hello, cela signifie que les abonnement hello n’est pas encore initialisé.  
   * Si vous voyez les détails de l’abonnement hello dans la sortie de hello, vérifiez que vous utilisez ID ou nom de l’abonnement approprié hello avec hello **Select-AzureSubscription** applet de commande.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Scénario : Authentification tooAzure a échoué, car l’authentification multifacteur est activée.
**Erreur :** erreur hello « Add-AzureAccount : AADSTS50079 : inscription de l’authentification forte (preuve-up) est requise » lors de l’authentification tooAzure avec votre nom d’utilisateur Azure et un mot de passe.

**Erreur de hello :** si vous avez l’authentification multifacteur sur votre compte Azure, vous ne pouvez pas utiliser un tooAzure de tooauthenticate utilisateur Azure Active Directory.  Au lieu de cela, vous devez toouse un certificat ou une tooAzure tooauthenticate principal de service.

**Conseils de dépannage :** toouse un certificat avec hello applets de commande de gestion des services Azure, consultez trop[création et l’ajout d’un certificat de toomanage Azure services.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse un principal de service avec les applets de commande Azure Resource Manager, consultez trop[création service principal à l’aide du portail Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) et [l’authentification d’un principal de service avec Azure Resource Manager.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Erreurs courantes avec des runbooks
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Scénario : début de la tâche hello runbook a été tentée trois fois, mais échec toostart chaque fois
**Erreur :** votre runbook échoue avec l’erreur de hello « » a tenté de trois fois par la tâche de hello mais il a échoué. »

**Erreur de hello :** cette erreur peut être provoquée par hello suivant raisons :  

1. Limite de mémoire.  Nous avons documentées des limites sur la quantité de mémoire allouée tooa Sandbox [limites de service Automation](../azure-subscription-service-limits.md#automation-limits) pour un travail peut échouer il si utilise plus de 400 Mo de mémoire. 

2. Module incompatible.  Cela peut se produire si les dépendances de module ne sont pas correctes. Dans ce cas, votre runbook renverra généralement un message « Commande introuvable » ou « Impossible de lier le paramètre ». 

**Conseils de dépannage :** des hello suivant solutions permet de résoudre les problème de hello :  

* Toowork les méthodes suggérées dans la limite de mémoire hello sont des charges de travail toosplit hello entre plusieurs runbooks, pas traiter les données en mémoire, pas toowrite de sortie inutiles dans vos runbook ou prendre en compte le nombre des points de contrôle vous écrivez dans votre PowerShell procédures opérationnelles de flux de travail.  

* Vous devez tooupdate vos modules Azure en suivant les étapes de hello [comment tooupdate les modules Azure PowerShell dans Azure Automation](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Scénario : échec du runbook en raison d’un objet désérialisé
**Erreur :** votre runbook échoue avec l’erreur de hello « Impossible de lier le paramètre ``<ParameterName>``. Impossible de convertir hello ``<ParameterType>`` valeur de type Deserialized ``<ParameterType>`` tootype ``<ParameterType>``».

**Erreur de hello :** si votre runbook est un PowerShell Workflow, il stocke les objets complexes dans un format désérialisé dans un ordre toopersist l’état de votre runbook si hello workflow est suspendu.  

**Conseils de dépannage :**  
Un des hello suivant trois solutions pour corriger ce problème :

1. Si vous sont transférant des objets complexes à partir d’une applet de commande tooanother, encapsuler ces applets de commande dans un InlineScript.  
2. Passez hello nom ou la valeur dont vous avez besoin à partir de l’objet complexe de hello au lieu de passer l’objet complet hello.  
3. Utilisez un runbook PowerShell au lieu d’un runbook Workflow PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Scénario : Tâche du Runbook a échoué, car hello allouée quota dépassé
**Erreur :** votre tâche de runbook échoue avec l’erreur de hello « quota hello pour hello totale mensuelle des tâches temps d’exécution a été atteint pour cet abonnement ».

**Erreur de hello :** cette erreur se produit lorsque hello l’exécution du travail dépasse le quota de libre de 500 minutes hello pour votre compte. Ce quota s’applique à des types de tooall d’exécution des tâches de travail tels que le test d’une tâche de démarrage d’une tâche à partir du portail de hello, l’exécution d’un travail à l’aide de webhooks et de planification d’un tooexecute de travail à l’aide soit hello portail Azure ou dans votre centre de données. toolearn d’informations sur la tarification pour l’automatisation, consultez [Automation tarification](https://azure.microsoft.com/pricing/details/automation/).

**Conseils de dépannage :** si vous souhaitez toouse plus de 500 minutes de traitement par mois, vous devez toochange votre abonnement à partir du niveau de base de toohello hello niveau gratuit. Vous pouvez mettre à niveau le niveau de base toohello par hello en prenant comme suit :  

1. Se connecter tooyour abonnement Azure  
2. Sélectionnez compte Automation de hello que vous souhaitez tooupgrade  
3. Cliquez sur **Paramètres** > **Niveau de tarification et utilisation** > **Niveau de tarification**  
4. Sur hello **choisir votre niveau tarifaire** panneau, sélectionnez **base**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Scénario : l’applet de commande n’est pas reconnue lors de l’exécution d’un runbook
**Erreur :** votre tâche de runbook échoue avec l’erreur de hello »``<cmdlet name>``: terme de hello ``<cmdlet name>`` n’est pas reconnu comme nom de l’applet de commande, fonction, fichier de script ou programme exécutable de hello. »

**Erreur de hello :** cette erreur se produit lorsque l’applet de commande hello vous utilisez dans votre runbook ne trouve pas moteur PowerShell de hello.  Cela peut être, car le module hello contenant l’applet de commande hello est manquant dans le compte de hello, il existe un conflit de nom avec un nom, ou applet de commande hello existe également dans un autre module et Automation ne peut pas résoudre le nom de hello.

**Conseils de dépannage :** des hello suivant solutions permet de résoudre les problème de hello :  

* Vérifiez que vous avez entré un nom d’applet de commande hello correctement.  
* Assurez-vous d’applet de commande hello existe dans votre compte Automation et qu’il n’y a aucun conflit. tooverify si l’applet de commande hello est présent, ouvrez un runbook en mode édition et de recherche pour l’applet de commande hello vous souhaitez toofind dans la bibliothèque de hello ou exécutez **Get-Command ``<CommandName>``** .  Une fois que vous avez validé cette applet de commande hello est disponible toohello compte, et qu’il n’y a aucun conflit de nom avec d’autres applets de commande ou les procédures opérationnelles, ajoutez-le toohello canevas et vérifiez que vous utilisez un paramètre valide défini dans votre runbook.  
* Si vous n’avez pas un conflit de nom et l’applet de commande hello est disponible dans deux modules différents, vous pouvez résoudre ce problème à l’aide du nom qualifié complet de hello pour l’applet de commande hello. Vous pouvez par exemple utiliser **Nom_module\Nom_applet_de_commande**.  
* Si vous exécutez hello runbook local dans un groupe de travail hybride, puis assurez-vous que hello/applet de commande module est installé sur ordinateur hello qui héberge le processus de travail hybride hello.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Scénario : Un runbook en cours d’exécution longue ne parvient pas à l’exception de hello : « tâche de hello ne peut pas continuer en cours d’exécution, car il a été évincé plusieurs fois hello même point de contrôle ».
**Erreur de hello :** Voici le comportement par défaut en raison de toohello « Équitable » analyse de processus au sein d’Azure Automation, ce qui suspend automatiquement un runbook si elle s’exécute plus longtemps que 3 heures. Hello, toutefois, le message d’erreur retourné ne fournit pas de « maintenant » options. Un runbook peut être interrompu pour plusieurs raisons. Suspend se produire principalement due tooerrors. Par exemple, une exception non interceptée dans un runbook, une défaillance du réseau ou une panne sur hello Runbook Worker hello runbook en cours d’exécution, toutes les entraîne hello runbook toobe est suspendu et démarrer à partir de son dernier point de contrôle lors de la reprise.

**Conseils de dépannage :** hello documentées solution tooavoid ce problème est toouse de points de contrôle dans un flux de travail.  toolearn plus faire référence trop[flux de travail PowerShell Learning](automation-powershell-workflow.md#checkpoints).  Vous trouverez une explication plus détaillée de la distribution de charge équilibrée dans le billet de blog [Using Checkpoints in Runbooks](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/) (Utilisation de points de contrôle dans des runbooks).

## <a name="common-errors-when-importing-modules"></a>Erreurs courantes survenant lors de l’importation de modules
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Scénario : Module échoue tooimport ou d’applets de commande ne peut pas être exécutée après l’importation
**Erreur :** un module échoue tooimport ou importe correctement, mais aucun applets de commande ne sont extraits.

**Erreur de hello :** qu’un module peut ne pas importe correctement tooAzure Automation sont des raisons courantes :  

* structure de Hello ne correspond pas à la structure de hello que Automation a besoin toobe dans.  
* module de Hello dépend d’un autre module qui n’a pas été déployée tooyour compte Automation.  
* module de Hello est manquant dans ses dépendances dans le dossier de hello.  
* Hello **New-AzureRmAutomationModule** applet de commande est en cours de module de hello tooupload utilisés, et vous ne dispose de chemin d’accès de stockage complète hello ou module de hello n’avez pas chargés à l’aide d’une URL accessible publiquement.  

**Conseils de dépannage :**  
Des hello suivant solutions résoudra le problème de hello :  

* Assurez-vous que le module hello suit hello suivant le format :  
  NomModule.zip **->** NomModule ou Numéro de version **->** (ModuleName.psm1, ModuleName.psd1)
* Ouvrez le fichier .psd1 hello et voir si le module de hello possède des dépendances.  Dans ce cas, téléchargez ces toohello modules compte Automation.  
* Assurez-vous que toutes les DLL référencées sont présents dans le dossier du module hello.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Erreurs courantes avec la Configuration d’état souhaité (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Scénario : le nœud est en état d’échec avec une erreur « Introuvable »
**Erreur :** nœud de hello dispose d’un rapport avec **n’a pas pu** état et contenant des erreurs de hello « hello tentative tooget hello action à partir du serveur https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction a échoué, car une configuration valide ``<guid>`` est introuvable. »

**Erreur de hello :** cette erreur se produit généralement lorsque hello nœud attribué tooa nom de la configuration (par exemple, ABC) au lieu d’un nom de configuration de nœud (par exemple, ABC. Serveur Web).  

**Conseils de dépannage :**  

* Assurez-vous que l’attribution de nœud hello avec « nœud configuration nom » et non hello « configuration ».  
* Vous pouvez attribuer un configuration tooa nœud à l’aide du portail Azure ou avec une applet de commande PowerShell.

  * Dans l’ordre tooassign un configuration tooa nœud à l’aide du portail Azure, ouvrez hello **nœuds DSC** panneau, sélectionnez un nœud, puis cliquez sur **configuration du nœud Assign** bouton.  
  * Dans l’ordre tooassign un configuration tooa nœud à l’aide d’applet de commande PowerShell, utilisez **Set-AzureRmAutomationDscNode** applet de commande

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Scénario : aucune configuration de nœud (fichiers MOF) ne s’est produite au cours d’une compilation de configuration
**Erreur :** votre tâche de compilation DSC suspend avec l’erreur de hello : « Compilation s’est terminée correctement, mais aucun .MOF de configuration de nœud ont été générés ».

**Erreur de hello :** lorsque hello expression suivant hello **nœud** mot clé dans la configuration de hello DSC prend trop$ null puis ne sortira aucune configuration de nœuds.    

**Conseils de dépannage :**  
Des hello suivant solutions résoudra le problème de hello :  

* Assurez-vous que toohello suivant de hello expression **nœud** mot clé dans la définition de la configuration hello n’évalue pas trop NULL comme valeur de $.  
* Si vous passez ConfigurationData lors de la compilation de configuration de hello, assurez-vous que vous transmettez les valeurs attendues de hello que la configuration hello requiert de [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Scénario : hello état du nœud DSC se bloque l’état « en cours »
**Erreur :** l’agent DSC génère le message « Impossible de trouver une instance avec les valeurs de propriétés fournies ».

**Erreur de hello :** vous mise à niveau votre version WMF et WMI endommagé.  

**Conseils de dépannage :** suivez les instructions de hello Bonjour [DSC limitations et problèmes connus](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) problème de hello toofix.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Scénario : Toouse Impossible d’une information d’identification dans une configuration DSC
**Erreur :** votre tâche de compilation DSC a été interrompu avec erreur de hello : « erreur de System.InvalidOperationException lors du traitement de la propriété « informations d’identification' de type ``<some resource name>``: conversion et de stockage d’un mot de passe chiffré que le texte en clair est autorisé uniquement si PSDscAllowPlainTextPassword a la valeur tootrue ».

**Erreur de hello :** vous avez utilisé les informations d’identification dans une configuration mais n’a pas fourni un bon **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue pour chaque nœud configuration.  

**Conseils de dépannage :**  

* Assurez-vous que toopass Bonjour approprié **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue pour chaque configuration de nœud mentionnée dans la configuration de hello. Pour plus d’informations, consultez trop[actifs dans Azure Automation DSC](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Étapes suivantes
Si vous avez suivi hello dépannage ci-dessus et ne peut pas trouver les réponses hello, vous pouvez examiner les options de prise en charge supplémentaire de hello ci-dessous.

* Obtenir l’aide des experts Azure. Envoyer votre problème toohello [forums MSDN Azure ou le débordement de pile.](https://azure.microsoft.com/support/forums/).
* Signaler un incident au support Azure Accédez toohello [Azure prend en charge le site](https://azure.microsoft.com/support/options/) et cliquez sur **obtenir un support technique** sous **techniques et support de facturation**.
* Publier une demande de script sur le [Centre de scripts](https://azure.microsoft.com/documentation/scripts/) si vous recherchez une solution de runbook Azure Automation ou un module d’intégration.
* Publier vos commentaires ou vos demandes de fonctionnalités pour Azure Automation sur [User Voice](https://feedback.azure.com/forums/34192--general-feedback).
