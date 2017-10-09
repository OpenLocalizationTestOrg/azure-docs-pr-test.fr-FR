---
title: "Azure AD Connect : Mise à niveau à partir de DirSync | Microsoft Docs"
description: "Découvrez comment tooupgrade à partir de la synchronisation d’annuaire tooAzure AD Connect. Cet article décrit les étapes de hello pour la mise à niveau à partir de la synchronisation d’annuaire tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect : Mise à niveau à partir de DirSync
Azure AD Connect est hello successeur tooDirSync. Vous parvenez hello que vous pouvez mettre à niveau à partir de la synchronisation d’annuaire dans cette rubrique. Ces étapes ne fonctionnent pas pour la mise à niveau à partir d’une autre version d’Azure AD Connect ou d’Azure AD Sync.

Avant de commencer l’installation d’Azure AD Connect, assurez-vous que trop[Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) préalable hello terminé les étapes [Azure AD Connect : conditions matérielles et](active-directory-aadconnect-prerequisites.md). En particulier, que vous souhaitiez tooread sur les éléments suivants de hello, dans la mesure où ces zones sont différentes de la synchronisation d’annuaire :

* Hello version requise du .net et PowerShell. Les versions plus récentes sont toobe requis sur le serveur hello si nécessaire par DirSync.
* configuration du serveur proxy Hello. Si vous utilisez un tooreach de serveur proxy hello internet, ce paramètre doit être configuré avant la mise à niveau. Synchronisation d’annuaire utilisé toujours serveur de proxy hello configurée pour l’utilisateur hello l’installer, mais Azure AD Connect utilise les paramètres de l’ordinateur à la place.
* toobe nécessaire des URL de Hello ouvrir dans le serveur de proxy hello. Pour les scénarios de base, ceux qui sont également prises en charge par DirSync, exigences de hello sont même hello. Si vous souhaitez que toouse hello nouvelles fonctionnalités incluses dans Azure AD Connect, certaines nouvelles URL doit être ouvert.

> [!NOTE]
> Une fois que vous avez activé votre nouvelle Azure AD Connect server toostart synchronisation modifications tooAzure AD, vous devez restaure pas toousing DirSync ou Azure AD Sync. La rétrogradation à partir de clients de toolegacy de Azure AD Connect, notamment DirSync et Azure AD Sync n’est pas prise en charge et peut entraîner des tooissues telles qu’une perte de données dans Azure AD.

Si vous n’effectuez pas une mise à niveau à partir de DirSync, consultez la section [Documentation connexe](#related-documentation) pour d’autres scénarios.

## <a name="upgrade-from-dirsync"></a>Mise à niveau à partir de DirSync
Selon votre déploiement en cours de synchronisation d’annuaire, il existe différentes options de mise à niveau hello. Si hello attendue heure de mise à niveau est inférieure à trois heures, puis hello est recommandé de toodo une mise à niveau sur place. Si hello temps attendu de mise à niveau plus de trois heures, puis hello est recommandé de toodo un déploiement parallèle sur un autre serveur. Il est estimé que si vous disposez de plus de 50 000 objets il prend plus de mise à niveau de trois heures toodo hello.

| Scénario |
| --- | --- |
| [Mise à niveau sur place](#in-place-upgrade) |
| [Déploiement en parallèle](#parallel-deployment) |

> [!NOTE]
> Lorsque vous planifiez tooupgrade à partir de la synchronisation d’annuaire tooAzure AD Connect, ne désinstallez pas DirSync vous-même avant la mise à niveau hello. Azure AD Connect sera de lire et de migrer la configuration de hello à partir de la synchronisation d’annuaire et de désinstaller après avoir inspecté le serveur de hello.

**Mise à niveau sur place**  
Hello attendu la mise à niveau de temps toocomplete hello est affiché par l’Assistant de hello. Cette estimation est basée sur l’hypothèse hello qu’il prend trois heures toocomplete une mise à niveau une base de données avec 50 000 objets (utilisateurs, contacts et groupes). Si le nombre de hello d’objets dans votre base de données est inférieur à 50 000, Azure AD Connect recommande une mise à niveau sur place. Si vous décidez de toocontinue, vos paramètres actuels sont automatiquement appliquées au cours de la mise à niveau et votre serveur reprend automatiquement la synchronisation active.

Si vous souhaitez toodo une migration de configuration et que vous effectuez un déploiement en parallèle, vous pouvez remplacer recommandation de mise à niveau sur place hello. Vous pouvez par exemple effectuer hello opportunité toorefresh hello et systèmes d’exploitation. Pour plus d’informations, consultez hello [parallèles déploiement](#parallel-deployment) section.

**Déploiement en parallèle**  
Un déploiement en parallèle est recommandé si vous avez plus de 50 000 objets. Ce déploiement permet d’éviter les retards opérationnels rencontrés par vos utilisateurs. Hello installation d’Azure AD Connect tente tooestimate hello temps d’arrêt pour mise à niveau hello, mais si vous avez mis à niveau DirSync Bonjour précédentes, votre expérience est probablement toobe guide des meilleures hello.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Prise en charge toobe de configurations de DirSync mis à niveau
Hello, les modifications de configuration suivantes est prises en charge avec DirSync mis à niveau :

* Filtrage domaine et unité organisationnelle
* Autre ID (UPN)
* Synchronisation de mot de passe et paramètres hybrides d'Exchange
* Vos paramètres domaine/forêt et Azure AD
* Filtrage basé sur les attributs de l'utilisateur

Hello après modification ne peut pas être mis à niveau. Si vous avez cette configuration, la mise à niveau hello est bloqué :

* Modifications de DirSync non prises en charge, par exemple : attributs supprimés et utilisation d’une DLL d’extension personnalisée

![Blocage de la mise à niveau](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

Dans ces cas, hello est recommandé de tooinstall un nouveau serveur Azure AD Connect dans [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode) et vérifiez hello DirSync ancienne et nouvelle configuration d’Azure AD Connect. Appliquez de nouveau les éventuelles modifications à l’aide de la configuration personnalisée, comme décrit dans [Azure AD Connect Sync : configuration personnalisée](active-directory-aadconnectsync-whatis.md).

les mots de passe Hello utilisés par DirSync hello comptes de service ne peuvent pas être récupérées et ne sont pas migrés. Ces mots de passe sont réinitialisées lors de la mise à niveau de hello.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Étapes principales pour la mise à niveau à partir de la synchronisation d’annuaire tooAzure AD Connect
1. Bienvenue dans tooAzure AD Connect
2. Analyse de la configuration DirSync actuelle
3. Collecte du mot de passe administrateur global Azure AD
4. Collecter les informations d’identification pour un compte administrateur d’entreprise (utilisé uniquement lors de l’installation de hello d’Azure AD Connect)
5. Installation d'Azure AD Connect
   * Désinstaller DirSync (ou le désactiver temporairement)
   * Installer Azure AD Connect
   * Synchronisation, si nécessaire

Des étapes supplémentaires sont nécessaires dans les cas suivants :

* Vous utilisez actuellement un serveur SQL complet, local ou distant
* Vous avez plus de 50 000 objets à synchroniser

## <a name="in-place-upgrade"></a>Mise à niveau sur place
1. Lancez hello Azure AD Connect installer (MSI).
2. Consultez et acceptez les termes du contrat de toolicense et avis de confidentialité.  
   ![Bienvenue tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Cliquez sur suivante analyse toobegin de votre installation existante de DirSync.  
   ![Analyse de l’installation existante de la synchronisation d’annuaires](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Lors de l’analyse de hello est terminée, vous voyez les recommandations hello sur la façon de tooproceed.  
   * Si vous utilisez SQL Server Express et que vous avez moins de 50 000 objets, hello suivant l’écran s’affiche :  
     ![Analyse terminée tooupgrade prêt à partir de la synchronisation d’annuaire](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Si vous utilisez une instance SQL Server complète pour DirSync, vous voyez cette page à la place :  
     ![Analyse terminée tooupgrade prêt à partir de la synchronisation d’annuaire](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     informations Hello concernant hello existant serveur SQL Server de base de données utilisé par la synchronisation d’annuaire sont affichées. Apportez des modifications, si nécessaire. Cliquez sur **suivant** installation de hello toocontinue.
   * Si vous avez plus de 50 000 objets, vous voyez cet écran à la place :  
     ![Analyse terminée tooupgrade prêt à partir de la synchronisation d’annuaire](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed avec une mise à niveau sur place, cliquez sur le message de toothis suivant hello case à cocher : **continuer la mise à niveau de DirSync sur cet ordinateur.**
     toodo un [parallèles déploiement](#parallel-deployment) au lieu de cela, vous exporter les paramètres de configuration DirSync hello et déplacer le nouveau serveur hello configuration toohello.
5. Fournir le mot de passe de hello pour le compte de hello que vous utilisez actuellement tooconnect tooAzure AD. Il doit s’agir compte hello actuellement utilisé par la synchronisation d’annuaire.  
   ![Entrez vos informations d’identification Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Si vous recevez une erreur et que vous avez des problèmes de connectivité, consultez [Résoudre les problèmes de connectivité liés à Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Indiquez un compte d'administrateur d'entreprise pour Active Directory.  
   ![Entrez vos informations d'identification ADDS.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Vous êtes maintenant prêt tooconfigure. Lorsque vous cliquez sur **Mettre à niveau**, DirSync est désinstallé, puis Azure AD Connect est configuré et lance la synchronisation.  
   ![Tooconfigure prêt](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Après installation hello, déconnectez-vous et connectez-vous à nouveau tooWindows avant d’utiliser le Gestionnaire de Service de synchronisation, éditeur de règles de synchronisation, ou essayez toomake toutes les autres modifications de configuration.

## <a name="parallel-deployment"></a>Déploiement en parallèle
### <a name="export-hello-dirsync-configuration"></a>Exporter la configuration de DirSync hello
**Déploiement en parallèle avec plus de 50 000 objets**

Si vous disposez de plus de 50 000 objets, puis hello installation d’Azure AD Connect recommande un déploiement en parallèle.

Un écran semblable toohello affiche :  
![Analyse terminée](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Si vous souhaitez tooproceed déploiement parallèle, vous devez hello tooperform comme suit :

* Cliquez sur hello **exporter les paramètres** bouton. Lorsque vous installez Azure AD Connect sur un serveur distinct, ces paramètres sont migrés à partir de votre installation actuelle de DirSync tooyour nouveau Azure AD Connect.

Une fois que vos paramètres ont été exportées avec succès, vous pouvez quitter l’Assistant d’Azure AD Connect hello sur le serveur de synchronisation d’annuaire hello. Passez à l’étape suivante de hello trop[installer Azure AD Connect sur un serveur distinct](#installation-of-azure-ad-connect-on-separate-server)

**Déploiement en parallèle avec moins de 50 000 objets**

Si vous avez moins de 50 000 objets mais toujours toodo un déploiement en parallèle, puis hello suivant :

1. Exécutez le programme d’installation Azure AD Connect de hello (MSI).
2. Lorsque vous consultez hello **tooAzure accueil AD Connect** écran, quitter l’Assistant installation hello en cliquant sur hello « X » dans hello coin supérieur droit de la fenêtre hello.
3. Ouvrez une invite de commandes.
4. À partir de hello emplacement d’installation de Azure AD Connect (par défaut : C:\Program Files\Microsoft Azure Active Directory Connect) exécutez hello de commande suivante : `AzureADConnect.exe /ForceExport`.
5. Cliquez sur hello **exporter les paramètres** bouton. Lorsque vous installez Azure AD Connect sur un serveur distinct, ces paramètres sont migrés à partir de votre installation actuelle de DirSync tooyour nouveau Azure AD Connect.

![Analyse terminée](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Une fois que vos paramètres ont été exportées avec succès, vous pouvez quitter l’Assistant d’Azure AD Connect hello sur le serveur de synchronisation d’annuaire hello. Passez à l’étape suivante de hello trop[installer Azure AD Connect sur un serveur distinct](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Installation d'Azure AD Connect sur un serveur distinct
Lorsque vous installez Azure AD Connect sur un nouveau serveur, l’hypothèse de hello est que vous souhaitez tooperform une nouvelle installation d’Azure AD Connect. Étant donné que vous voulez que la configuration de DirSync hello toouse, il existe certains tootake des étapes supplémentaires :

1. Exécutez le programme d’installation Azure AD Connect de hello (MSI).
2. Lorsque vous consultez hello **tooAzure accueil AD Connect** écran, quitter l’Assistant installation hello en cliquant sur hello « X » dans hello coin supérieur droit de la fenêtre hello.
3. Ouvrez une invite de commandes.
4. À partir de hello emplacement d’installation de Azure AD Connect (par défaut : C:\Program Files\Microsoft Azure Active Directory Connect) exécutez hello de commande suivante : `AzureADConnect.exe /migrate`.
   Assistant d’installation Bonjour Azure AD Connect démarre et vous présente hello suivant d’écran :  
   ![Entrez vos informations d’identification Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Sélectionnez le fichier de paramètres hello exportée à partir de votre installation DirSync.
6. Configurez les options avancées :
   * Un emplacement d'installation personnalisé pour Azure AD Connect.
   * Une instance de SQL Server (par défaut, Azure AD Connect installe SQL Server 2012 Express). N’utilisez pas hello même instance de base de données que votre serveur de synchronisation d’annuaire.
   * Un compte de service utilisé tooconnect tooSQL serveur (si votre base de données SQL Server est distant, ce compte doit être un compte de service de domaine).
     Ces options s'affichent dans cet écran :   
     ![Entrez vos informations d’identification Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Cliquez sur **Suivant**.
8. Sur hello **tooconfigure prêt** page, laissez l’option hello **démarrer le processus de synchronisation hello dès la fin de la configuration de hello** activée. Hello serveur est maintenant en [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode) modifications ne sont pas exportée tooAzure AD.
9. Cliquez sur **Installer**.
10. Après installation hello, déconnectez-vous et connectez-vous à nouveau tooWindows avant d’utiliser le Gestionnaire de Service de synchronisation, éditeur de règles de synchronisation, ou essayez toomake toutes les autres modifications de configuration.

> [!NOTE]
> Début de la synchronisation entre Windows Server Active Directory et Azure Active Directory, mais aucune modification n’est exportée tooAzure AD. Les modifications ne peuvent être exportées activement que par un seul outil de synchronisation à la fois. Cet état est appelé [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Vérifiez que Azure AD Connect est prêt toobegin synchronisation
tooverify que Azure AD Connect est prêt tootake sur à partir de la synchronisation d’annuaire, vous devez tooopen **Synchronization Service Manager** dans le groupe de hello **Azure AD Connect** à partir du menu Démarrer de hello.

Dans l’application hello, accédez à toohello **Operations** onglet. Sous cet onglet, vérifiez que hello suit les opérations terminées :

* Importez sur hello Connecteur AD
* Importez sur hello connecteur Azure AD
* Synchronisation complète sur hello Connecteur AD
* Synchronisation complète sur hello connecteur Azure AD

![Importation et synchronisation terminées](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Passez en revue les résultats hello à partir de ces opérations et assurez-vous qu'aucun message d’erreur.

Si vous souhaitez toosee et inspectez les modifications de hello sur toobe exporté tooAzure AD, puis lisez Comment tooverify hello configuration sous [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode). Apportez les modifications de la configuration requises jusqu'à ce que tout soit correct.

Vous êtes prêt tooswitch de tooAzure de synchronisation d’annuaire Active Directory lorsque vous aurez effectué ces étapes et que vous êtes satisfait des résultats de hello.

### <a name="uninstall-dirsync-old-server"></a>Désinstallation de DirSync (ancien serveur)
* Dans **Programmes et fonctionnalités**, recherchez **Outil de synchronisation Windows Azure Active Directory**
* Désinstallez **Outil de synchronisation Windows Azure Active Directory**
* la désinstallation de Hello peut prendre too15 minutes toocomplete.

Si vous préférez toouninstall DirSync ultérieurement, vous pouvez également arrêter le serveur de hello ou désactiver hello service. Si une erreur survient, cette méthode vous permet de toore-enable il. Toutefois, il est peu probable de que cette étape suivante hello échoue donc cela ne doit pas être nécessaire.

Aucun serveur active exportation tooAzure AD est avec DirSync désinstallé ou désactivé. Hello prochaine étape tooenable Azure AD Connect doit être terminée avant que les modifications apportées à votre annuaire Active Directory local continue toobe synchronisé tooAzure AD.

### <a name="enable-azure-ad-connect-new-server"></a>Activation d'Azure AD Connect (nouveau serveur)
Après l’installation, puis rouvrez-le Azure AD se connecter va vous permettre de toomake autres modifications de configuration. Démarrer **Azure AD Connect** à partir du menu Démarrer de hello ou à partir du raccourci hello sur le bureau de hello. Assurez-vous que vous n’essayez pas de toorun hello installation MSI.

Vous devez voir s’afficher hello :  
![Tâches supplémentaires](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Sélectionnez **Configuration du mode de préproduction**.
* Désactiver la mise en lots en décochant les cases hello **mode de préproduction activé** case à cocher.

![Entrez vos informations d’identification Azure AD.](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Cliquez sur hello **suivant** bouton
* Sur la page de confirmation hello, cliquez sur hello **installer** bouton.

Azure AD Connect est maintenant votre serveur actif et vous ne devez pas basculer toousing arrière votre serveur de synchronisation d’annuaire existant.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez Azure AD Connect installée, vous pouvez [vérifier l’installation de hello et attribuer des licences](active-directory-aadconnect-whats-next.md).

En savoir plus sur ces nouvelles fonctionnalités qui ont été activées à l’installation de hello : [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md), [empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), et [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

En savoir plus sur ces sujets courants : [planificateur et comment synchroniser les tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
