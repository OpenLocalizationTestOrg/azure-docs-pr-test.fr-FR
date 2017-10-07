---
title: "cluster d’aaaSubmit tooan de travaux HPC Pack dans Azure | Documents Microsoft"
description: "Découvrez comment tooset d’un toosubmit d’ordinateur local travaux tooan un cluster HPC Pack dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Envoyer des travaux HPC d’un ordinateur de local tooan cluster HPC Pack déployé dans Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configurer un tooa de travaux locaux client ordinateur toosubmit [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster dans Azure. Cet article vous explique comment tooset d’un ordinateur local avec le client des outils toosubmit travail sur un cluster toohello HTTPS dans Azure. De cette façon, plusieurs utilisateurs de cluster peuvent envoyer des travaux tooa nuage cluster HPC Pack, mais sans connexion directe toohello machine virtuelle du nœud principal ou d’accéder à un abonnement Azure.

![Envoyer un cluster tooa de travail dans Azure][jobsubmit]

## <a name="prerequisites"></a>Composants requis
* **Nœud principal HPC Pack est déployé dans une machine virtuelle Azure** -nous vous recommandons d’utiliser des outils automatisés comme un [modèle de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) ou un [script Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy du nœud principal hello et cluster. Vous devez le nom DNS hello du nœud principal hello et les informations d’identification de hello d’un administrateur de cluster pour effectuer les étapes hello dans cet article.
* **Ordinateur client** : vous avez besoin d’un ordinateur client Windows ou Windows Server qui peut exécuter des utilitaires clients HPC Pack (voir [Configuration requise](https://technet.microsoft.com/library/dn535781.aspx)). Si vous souhaitez uniquement le portail web de toouse hello HPC Pack ou les travaux de toosubmit d’API REST, vous pouvez utiliser n’importe quel ordinateur client de votre choix.
* **Support d’installation de HPC Pack** -tooinstall hello utilitaires clients de HPC Pack, package d’installation gratuit hello pour la dernière version de HPC Pack (HPC Pack 2012 R2) est disponible à partir de la [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Assurez-vous que vous téléchargez hello même version de HPC Pack qui est installé sur la machine virtuelle du nœud principal hello.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Étape 1 : Installer et configurer les composants web hello sur le nœud principal de hello
tooenable un cluster de toohello reste interface toosubmit travaux via le protocole HTTPS, assurez-vous que les composants web de HPC Pack hello sont configurés sur le nœud principal HPC Pack de hello. S’ils ne sont pas déjà installés, d’abord installer les composants web hello en exécutant le fichier d’installation HpcWebComponents.msi hello. Ensuite, configurez les composants de hello en exécutant le script PowerShell HPC de hello **Set-hpcwebcomponents.ps1**.

Pour obtenir des procédures détaillées, consultez [installer les composants Web de hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Certains modèles de démarrage rapide Azure pour HPC Pack Installer et configurer automatiquement les composants web de hello. Si vous utilisez hello [script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) cluster hello de toocreate, vous pouvez éventuellement installer et configurer les composants web hello dans le cadre du déploiement de hello.
> 
> 

**composants web tooinstall hello**

1. Se connecter toohello machine virtuelle du nœud principal à l’aide des informations d’identification de hello d’un administrateur de cluster.
2. À partir du dossier d’installation de HPC Pack hello, exécutez HpcWebComponents.msi sur le nœud principal de hello.
3. Suivez les étapes de hello dans les composants web hello hello Assistant tooinstall

**composants web tooconfigure hello**

1. Sur le nœud principal de hello, démarrez HPC PowerShell en tant qu’administrateur.
2. toochange toohello emplacement du répertoire script de configuration hello, hello type commande suivante :
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure hello interface REST et démarrer hello Service Web de HPC, hello type commande suivante :
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Lorsque tooselect invité à un certificat, choisissez le certificat de hello toohello le nom DNS public de nœud principal de hello correspondant. Par exemple, si vous déployez le nœud principal de hello machine virtuelle à l’aide du modèle de déploiement classique de hello, nom du certificat hello ressemble à CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Si vous utilisez le modèle de déploiement du Gestionnaire de ressources hello, nom du certificat hello ressemble à CN =&lt;*HeadNodeDnsName*&gt;.&lt; *région*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Vous sélectionnez ce certificat ultérieurement lorsque vous envoyez le nœud principal de travaux toohello à partir d’un ordinateur local. Ne sélectionnez ou configurer un certificat qui correspond le nom de l’ordinateur du nœud principal de hello dans un domaine Active Directory de hello toohello (par exemple, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. tooconfigure le portail web hello pour la soumission de travaux, hello type commande suivante :
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Une fois hello script terminé, arrêtez et redémarrez le hello Service Planificateur de travaux HPC en tapant hello suivant de commandes :
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Étape 2 : Installer les utilitaires clients HPC Pack hello sur un ordinateur local
Si vous souhaitez que les utilitaires clients de tooinstall hello HPC Pack sur votre ordinateur, téléchargez les fichiers d’installation de HPC Pack (installation complète) à partir de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Lorsque vous commencez l’installation de hello, choisissez option d’installation de hello pour hello **utilitaires clients HPC Pack**.

toouse hello HPC Pack des outils toosubmit travaux toohello machine virtuelle nœud principal, vous également besoin tooexport un certificat à partir du nœud principal hello et l’installer sur l’ordinateur client de hello. certificat de Hello doit être dans. Format CER.

**certificat de hello tooexport à partir du nœud principal hello**

1. Sur le nœud principal de hello, ajoutez hello certificats enfichable tooa Microsoft Management Console pour hello compte d’ordinateur Local. Pour connaître les étapes tooadd hello-composant logiciel enfichable, consultez [ajouter hello le composant logiciel enfichable Certificats tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. Dans l’arborescence de la console hello, développez **certificats – ordinateur Local** > **personnel**, puis cliquez sur **certificats**.
3. Recherchez le certificat hello que vous avez configuré pour les composants web hello HPC Pack dans [étape 1 : installer et configurer les composants web hello sur le nœud principal de hello](#step-1:-install-and-configure-the-web-components-on-the-head-node) (par exemple, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Cliquez sur le certificat de hello, puis cliquez sur **toutes les tâches** > **exporter**.
5. Bonjour Assistant Exportation de certificat, cliquez sur **suivant**et vérifiez que **non, ne pas exporter la clé privée de hello** est sélectionnée.
6. Hello suivez restant des étapes de certificat hello Assistant tooexport hello DER binaire codé X.509 (. Format de la région d’exécution limitée).

**certificat de hello tooimport sur l’ordinateur client de hello**

1. Copiez le certificat hello que vous avez exporté à partir du dossier tooa hello du nœud principal sur l’ordinateur client de hello.
2. Sur l’ordinateur client de hello, exécutez certmgr.msc.
3. Dans le Gestionnaire de certificats, développez **Certificats – Utilisateur actuel** > **Autorités de certification racines de confiance**, cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches** > **Importer**.
4. Bonjour Assistant Importation de certificat, cliquez sur **suivant** et suivez hello étapes tooimport hello certificat que vous avez exporté à partir de toohello de nœud principal hello magasin des autorités de Certification racines de confiance.

> [!TIP]
> Vous pouvez voir un avertissement de sécurité, car l’autorité de certification hello sur le nœud principal de hello n’est pas reconnue par l’ordinateur client de hello. À des fins de test, vous pouvez ignorer cet avertissement et complète hello l’importation du certificat.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Étape 3 : Exécuter les travaux de test sur le cluster de hello
tooverify votre configuration, essayez les travaux en cours d’exécution sur hello du cluster dans Azure à partir de hello local ordinateur. Par exemple, vous pouvez utiliser les outils de l’interface graphique utilisateur de HPC Pack ou un cluster de commandes de ligne de commande toosubmit travaux toohello. Vous pouvez également utiliser un travaux toosubmit de portail basé sur le web.

**commandes d’envoi de travail toorun sur l’ordinateur client de hello**

1. Sur un ordinateur client sur lequel sont installés les utilitaires clients HPC Pack hello, démarrez une invite de commandes.
2. Tapez un exemple de commande. Par exemple, toolist toutes les tâches sur le cluster de hello, tapez un tooone similaire commande Hello suivant, en fonction de hello nom DNS complet du nœud principal de hello :
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    ou
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Utilisez hello nom DNS complet du nœud principal hello, pas les adresses IP hello, dans l’URL de planificateur hello. Si vous spécifiez des adresses IP de hello, une erreur s’affiche comme trop « certificat de serveur hello doit tooeither ont une chaîne valide de confiance ou toobe placé dans le magasin racine approuvé de hello. »
   > 
   > 
3. Lorsque vous y êtes invité, tapez le nom d’utilisateur hello (sous forme de hello &lt;DomainName&gt;\\&lt;nom d’utilisateur&gt;) et le mot de passe d’administrateur de cluster HPC hello ou un autre utilisateur de cluster que vous avez configuré. Vous pouvez choisir toostore informations d’identification hello localement pour d’autres travaux.
   
    Une liste de travaux s’affiche.

**toouse Gestionnaire de travaux HPC sur l’ordinateur client de hello**

1. Si vous n’a pas été précédemment stocker les informations d’identification de domaine pour un utilisateur de cluster lors de l’envoi d’un travail, vous pouvez ajouter des informations d’identification hello dans le Gestionnaire d’informations d’identification.
   
    a. Dans le panneau de configuration sur l’ordinateur client de hello, démarrez le Gestionnaire d’informations d’identification.
   
    b. Cliquez sur **Informations d’identification Windows** > **Ajouter des informations d’identification génériques**.
   
    c. Spécifiez l’adresse Internet de hello (par exemple, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt; région&gt;.cloudapp.azure.com/HpcScheduler) et le nom d’utilisateur hello (&lt;DomainName&gt;\\&lt;nom d’utilisateur&gt;) et le mot de passe d’administrateur de cluster hello ou un autre utilisateur de cluster que vous avez configuré.
2. Sur l’ordinateur client de hello, démarrez le Gestionnaire de travaux HPC.
3. Bonjour **sélectionner le nœud principal** boîte de dialogue, de type hello URL toohello nœud principal dans Azure (par exemple, https://&lt;HeadNodeDnsName&gt;. cloudapp.net ou https://&lt;HeadNodeDnsName&gt;. &lt;région&gt;. cloudapp.azure.com).
   
    Gestionnaire de travaux HPC s’ouvre et affiche une liste de tâches sur le nœud principal de hello.

**portail web de toouse hello en cours d’exécution sur le nœud principal de hello**

1. Démarrez un navigateur web sur l’ordinateur client de hello et entrez une des hello suivant des adresses, en fonction de hello nom DNS complet du nœud principal de hello :
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    ou
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Dans hello sécurité boîte de dialogue qui s’affiche, tapez informations d’identification de domaine hello de l’administrateur de cluster HPC hello. (Vous pouvez également ajouter d’autres utilisateurs de cluster dans des rôles différents. Consultez [Gestion des utilisateurs du cluster](https://technet.microsoft.com/library/ff919335.aspx).)
   
    portail web de Hello ouvre la vue de liste des travaux toohello.
3. toosubmit un exemple de travail renvoyant hello chaîne « Hello World » à partir du cluster de hello, cliquez sur **nouveau travail** de navigation de gauche hello.
4. Sur hello **nouveau travail** sous **à partir des pages d’envoi**, cliquez sur **HelloWorld**. page de soumission de travail Hello s’affiche.
5. Cliquez sur **Envoyer**. Si vous y êtes invité, fournissez les informations d’identification du domaine de hello de l’administrateur de cluster HPC hello. travail de Hello est envoyé, et ID de tâche hello apparaît sur hello **Mes travaux** page.
6. résultats de hello tooview du travail hello qui vous a envoyé, cliquez sur ID de tâche hello, puis cliquez sur **afficher les tâches** tooview sortie de la commande hello (sous **sortie**).

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez également envoyer des travaux toohello cluster Azure avec hello [API REST de HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Si vous souhaitez toosubmit les travaux de cluster à partir d’un client Linux, consultez hello Python exemple Bonjour [HPC Pack 2012 R2 SDK et des exemples de Code](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
