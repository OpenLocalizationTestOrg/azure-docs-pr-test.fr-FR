---
title: aaaEncrypt une Machine virtuelle Azure | Documents Microsoft
description: "Ce document vous aide à tooencrypt une Machine virtuelle Azure après la réception d’une alerte à partir du centre de sécurité Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Chiffrement d’une machine virtuelle Azure
Le Centre de sécurité Azure émet une alerte si certaines de vos machines virtuelles ne sont pas chiffrées. Ces alertes s’affichera en tant que recommandation de gravité élevée et hello est tooencrypt ces machines virtuelles.

![Recommandation de chiffrement de disque](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> informations de Hello dans ce document s’appliquent à tooencrypting virtuels sans l’aide d’une clé de chiffrement de clé (qui est requis pour la sauvegarde d’ordinateurs virtuels à l’aide d’Azure Backup). Consultez l’article de hello [chiffrement de disque Azure pour Windows et des Machines virtuelles Azure Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) pour plus d’informations sur la façon de toouse un toosupport de clé de cryptage Azure Backup pour chiffrées Machines virtuelles Azure.
>
>

tooencrypt des Machines virtuelles Azure qui ont été identifiées par le centre de sécurité Azure comme nécessitant le chiffrement, nous vous recommandons de hello comme suit :

* Installez et configurez Azure PowerShell. Cette opération activera toorun hello PowerShell commandes requis tooset des conditions préalables de hello-tooencrypt requis des Machines virtuelles Azure.
* Obtenir et exécuter hello Azure disque chiffrement conditions préalables script Azure PowerShell
* Chiffrez vos machines virtuelles.

Hello ce document vise tooenable vous tooencrypt vos machines virtuelles, même si vous avez un arrière-plan peu ou pas dans Azure PowerShell.
Ce document suppose que vous utilisez Windows 10 en tant qu’ordinateur hello du client à partir de laquelle vous allez configurer le chiffrement des disques Azure.

Il existe de nombreuses approches qui peuvent être utilisés toosetup hello prerequisites et tooconfigure chiffrement pour les Machines virtuelles Azure. Si vous êtes déjà rompu dans Azure PowerShell ou CLI d’Azure, vous pouvez préférer toouse autres approches.

> [!NOTE]
> toolearn en savoir plus sur le chiffrement tooconfiguring autres approches pour les machines virtuelles Azure, consultez [chiffrement de disque Azure pour Windows et des Machines virtuelles Azure Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Installation et configuration d'Azure PowerShell
Vous devez disposer d’Azure PowerShell version 1.2.1 ou ultérieure. article de Hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) contient toutes les étapes de hello vous devez tooprovision toowork de votre ordinateur avec Azure PowerShell. approche la plus simple Hello est l’approche d’installation Web PI hello toouse mentionné dans cet article. Même si vous disposez déjà d’Azure PowerShell est installé, installez à nouveau à l’aide d’approche de Web PI hello afin que vous avez la version la plus récente d’Azure PowerShell hello.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Obtenir et exécuter des conditions préalables requises de chiffrement de disque Azure hello script de configuration
Hello Script de Configuration des conditions préalables Azure disque chiffrement configure toutes les conditions préalables de hello requis pour le chiffrement de vos Machines virtuelles Azure.

1. Page GitHub toohello accédez ayant hello [le Script de configuration requis Azure disque chiffrement](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Hello GibHub page, cliquez sur hello **Raw** bouton.
3. Utilisez **CTRL-A** tooselect tous les hello texte sur la page de hello, puis utilisez **CTRL-C** toocopy tous hello texte hello page toohello Presse-papiers.
4. Ouvrez **bloc-notes** et collez le texte hello copié dans le bloc-notes.
5. Sur votre lecteur C:, créez un dossier que vous appellerez **AzureADEScript**.
6. Enregistrez le fichier de bloc-notes hello : cliquez sur **fichier**, puis cliquez sur **Enregistrer sous**. Dans la zone de texte Nom de fichier hello, entrez **« ADEPrereqScript.ps1 »** et cliquez sur **enregistrer**. (Assurez-vous que vous placez hello nom entre guillemets hello, sinon elle sera fichier hello avec une extension de fichier .txt).

Maintenant que le contenu du script hello est enregistré, ouvrez le script de hello Bonjour PowerShell ISE :

1. Bonjour Menu Démarrer, cliquez sur **Cortana**. Demandez à **Cortana** « PowerShell » en tapant **PowerShell** dans la zone de texte Rechercher hello Cortana.
2. Cliquez avec le bouton droit sur **Windows PowerShell ISE**, puis cliquez sur **Exécuter en tant qu’administrateur**.
3. Bonjour **administrateur : Windows PowerShell ISE** fenêtre, cliquez sur **vue** puis cliquez sur **afficher le volet Script**.
4. Si vous voyez hello **commandes** volet situé à droite de hello de fenêtre hello, cliquez sur hello **« x »** dans hello coin supérieur droit de hello volet tooclose il. Si le texte hello est trop petite pour vous toosee, utilisez **CTRL + ajouter** (« Ajouter » est hello « + » se connecter). Si le texte hello est trop volumineux, utilisez **CTRL + soustraction** (soustraction est hello »-« connexion).
5. Cliquez sur **Fichier**, puis sur **Ouvrir**. Accédez toohello **C:\AzureADEScript** dossier et hello double-cliquez sur hello **ADEPrereqScript**.
6. Hello **ADEPrereqScript** contenu doit maintenant apparaître dans hello PowerShell ISE et est coloré toohelp vous consultez plus facilement les différents composants, tels que des commandes, des paramètres et des variables.

Vous devez maintenant voir quelque chose comme hello la figure ci-dessous.

![Fenêtre PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

Hello volet supérieur est référencé tooas hello « volet de script » et volet du bas hello est référencé tooas hello « console ». Nous emploierons ces termes dans la suite de cet article.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Exécution de commande PowerShell de hello disque Azure chiffrement conditions préalables
Hello script du chiffrement conditions préalables sur disque de Azure vous demandera hello informations suivantes après avoir lancé le script de hello :

* **Nom du groupe de ressources** - nom de groupe de ressources que vous souhaitez tooput de hello hello dans le coffre de clés.  Un groupe de ressources avec le nom que vous entrez hello créerez si n’existe pas déjà avec ce nom créé. Si vous disposez déjà d’un groupe de ressources que vous souhaitez toouse dans cet abonnement, puis entrez le nom hello ce groupe de ressources.
* **Nom de clé de coffre** -nom du coffre de clés hello dans le chiffrement de clés sont toobe placé. S’il n’existe aucun coffre de clés associé à ce nom, un coffre de clés sera créé en utilisant le nom que vous avez saisi. Si vous disposez déjà d’un coffre de clés que vous souhaitez toouse, entrez nom hello Hello existant du coffre de clés.
* **Emplacement** -emplacement de hello coffre de clés. Assurez-vous que hello coffre de clés et les machines virtuelles toobe chiffré sont Bonjour même emplacement. Si vous ne connaissez pas les emplacement hello, voici les étapes plus loin dans cet article qui vous indiquent comment toofind out.
* **Nom d’Application Active Directory Azure** -nom de l’application Azure Active Directory qui est utilisés toowrite secrets toohello le coffre de clés de hello. S’il n’existe aucune application de ce nom, une nouvelle application sera créée en utilisant le nom que vous avez saisi. Si vous disposez déjà d’une application Azure Active Directory que vous souhaitez toouse, entrez le nom hello de l’application Azure Active Directory.

> [!NOTE]
> Si vous pouvez obtenir des informations en tant que toowhy vous devez toocreate une application Azure Active Directory, consultez *inscrire une application avec Azure Active Directory* section dans l’article de hello [prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).
>
>

Effectuez hello suivant les étapes tooencrypt une Machine virtuelle Azure :

1. Si vous avez fermé hello PowerShell ISE, ouvrez une instance avec élévation de privilèges de hello PowerShell ISE. Suivez les instructions de hello plus haut dans cet article si hello que PowerShell ISE n’est pas déjà s’ouvre. Si vous avez fermé le script de hello, puis ouvrez hello **ADEPrereqScript.ps1** en cliquant sur **fichier**, puis **ouvrir** et en sélectionnant de script de hello dans hello **c:\ AzureADEScript** dossier. Si vous avez suivi cet article à partir du début de hello, puis déplacez simplement sur l’étape suivante de toohello.
2. Dans la console hello Hello PowerShell ISE (hello volet inférieur de hello PowerShell ISE), modifiez hello focus toohello local du script de hello en tapant **cd c:\AzureADEScript** et appuyez sur **entrée**.
3. Définir la stratégie d’exécution hello sur votre ordinateur afin que vous pouvez exécuter le script de hello. Type **Set-ExecutionPolicy Unrestricted** hello console et appuyez sur ENTRÉE. Si vous voyez une boîte de dialogue indiquer des informations sur les effets de hello de stratégie de tooexecution hello modification, cliquez sur **Oui tooall** ou **Oui** (si vous voyez **Oui tooall**, sélectionnez cette option, si Vous ne voyez pas **Oui tooall**, puis cliquez sur **Oui**).
4. Connectez-vous à votre compte Azure. Dans la console hello, tapez **AzureRmAccount de connexion** et appuyez sur **entrée**. Une boîte de dialogue s’affiche dans laquelle vous entrez vos informations d’identification (Vérifiez que vous disposez des droits toochange hello virtual machines – si vous ne disposez pas des droits, vous ne serez pas en mesure de tooencrypt les. En cas de doute, renseignez-vous auprès du propriétaire ou de l’administrateur de votre abonnement). Vous devriez voir des informations concernant vos paramètres suivants : **Environment**, **Account**, **TenantId**, **SubscriptionId** et **CurrentStorageAccount**. Hello de copie **SubscriptionId** tooNotepad. Vous en aurez besoin toouse à l’étape 6 de #.
5. Recherchez l’abonnement votre machine virtuelle appartient tooand son emplacement. Accédez trop[https://portal.azure.com](ttps://portal.azure.com) et connectez-vous.  Dans hello à gauche de la page de hello, cliquez sur **virtuels**. Vous verrez une liste de vos machines virtuelles et les abonnements hello qu'auquel ils appartiennent.

   ![Machines virtuelles](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Retour toohello PowerShell ISE. Définir le contexte d’abonnement hello dans lequel hello script sera exécuté. Dans la console hello, tapez **sélectionnez-AzureRmSubscription – SubscriptionId < your_subscription_Id >** (remplacez **< your_subscription_Id >** avec votre ID d’abonnement réel) et appuyez sur  **Entrez**. Vous verrez plus d’informations sur l’environnement, de hello **compte**, **TenantId**, **SubscriptionId** et **CurrentStorageAccount**.
7. Vous êtes maintenant de script de hello toorun prêt. Cliquez sur hello **exécuter le Script** bouton ou appuyez sur **F5** clavier de hello.

   ![Exécution du script PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. script de Hello demande **resourceGroupName :** -Entrez le nom hello de *groupe de ressources* vous souhaitez toouse, puis appuyez sur **entrée**. Si vous n’en avez, entrez un nom que vous voulez toouse un nouveau. Si vous avez déjà un *groupe de ressources* que vous souhaitez toouse (par exemple hello une figurant dans votre machine virtuelle), entrez les nom hello Hello groupe de ressources existant.
9. script de Hello demande **keyVaultName :** -Entrez le nom hello Hello *le coffre de clés* toouse de souhaité, puis appuyez sur ENTRÉE. Si vous n’en avez, entrez un nom que vous voulez toouse un nouveau. Si vous disposez déjà d’un coffre de clés que vous souhaitez toouse, entrez le nom hello hello existants *le coffre de clés*.
10. script de Hello demande **emplacement :** - Entrez nom hello d’emplacement hello dans le hello machine virtuelle que vous souhaitez tooencrypt se trouve, puis appuyez sur **entrée**. Si vous ne connaissez pas d’emplacement de hello, revenez toostep #5.
11. script de Hello demande **aadAppName :** -Entrez le nom hello Hello *Azure Active Directory* application que vous souhaitez toouse, puis appuyez sur **entrée**. Si vous n’en avez, entrez un nom que vous voulez toouse un nouveau. Si vous avez déjà un *application Azure Active Directory* que vous souhaitez toouse, entrez le nom hello hello existants *application Azure Active Directory*.
12. Une boîte de dialogue de connexion s’affiche. Fournissez vos informations d’identification (Oui, vous avez connecté une seule fois, mais vous devez maintenant toodo nouveau).
13. Hello script s’exécute et lorsque vous avez terminé il vous demandera de valeurs hello toocopy hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**et **keyVaultResourceId**. Chacune de ces Presse-papiers toohello de valeurs copier et les coller dans le bloc-notes.
14. Revenir toohello PowerShell ISE et placer des curseurs de hello à fin hello de la dernière ligne de hello, appuyez sur **entrée**.

sortie Hello du script de hello ressemble à l’écran hello ci-dessous :

![Sortie PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Chiffrer hello machine virtuelle Azure
Vous est désormais prêt tooencrypt votre machine virtuelle. Si votre machine virtuelle se trouve dans hello même groupe de ressources que votre coffre de clés, vous pouvez déplacer sur la section étapes de chiffrement toohello. Toutefois, si votre machine virtuelle n’est pas dans hello ressource de groupe en tant que votre coffre de clés, vous devez tooenter qui suit hello dans la console hello Bonjour PowerShell ISE :

**$resourceGroupName = &lt;’Virtual_Machine_RG’&gt;**

Remplacez **< Virtual_Machine_RG >** par nom hello hello du groupe de ressources dans lequel se trouvent vos machines virtuelles, entourés par un guillemet simple. Appuyez sur **Entrée**.
tooconfirm hello correct a été entré le nom de groupe de ressources, tapez qui suit hello Bonjour console PowerShell ISE :

**$resourceGroupName**

Appuyez sur **ENTRÉE**. Vous devez voir le nom hello du groupe de ressources qui se trouvent vos ordinateurs virtuels. Par exemple :

![Sortie PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Étapes du chiffrement
Tout d’abord, vous devez le nom de hello tootell PowerShell de la machine virtuelle de hello souhaité tooencrypt. Dans la console hello, tapez :

**$vmName = &lt;’your_vm_name’&gt;**

Remplacez **<'your_vm_name ' >** avec nom hello de votre machine virtuelle (Assurez-vous que le nom de hello est entourée par un guillemet simple), puis appuyez sur **entrée**.

tooconfirm hello correct de nom d’ordinateur virtuel a été entrée, tapez :

**$vmName**

Appuyez sur **ENTRÉE**. Vous devriez voir hello nom d’ordinateur virtuel de hello souhaité tooencrypt. Par exemple :

![Sortie PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Il existe deux méthodes toorun hello chiffrement commande tooencrypt tous les lecteurs sur l’ordinateur virtuel de hello. méthode première Hello est hello tootype commande Bonjour console PowerShell ISE suivante :

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Appuyez ensuite sur **ENTRÉE**.

méthode deuxième Hello est tooclick dans le volet de script hello (volet supérieur de hello PowerShell ISE hello) et faites défiler bas toohello du script de hello. Commande hello répertoriée ci-dessus, de mettre en surbrillance, puis avec le bouton droit dessus, puis cliquez **exécuter la sélection** ou appuyez sur **F8** clavier de hello.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Quelle que soit la méthode hello que vous utilisez, une boîte de dialogue s’affiche vous informant que prendra 10 à 15 minutes pour hello opération toocomplete. Cliquez sur **Oui**.

Pendant le processus de chiffrement hello est en cours, vous pouvez retourner toohello portail Azure et voir État hello de machine virtuelle de hello. Sur hello à gauche de la page de hello, cliquez sur **virtuels**, puis Bonjour **virtuels** panneau, cliquez sur nom hello de machine virtuelle de hello vous chiffrez. Dans le panneau hello qui s’affiche, vous remarquerez que hello **état** indique qu’il est **mise à jour**. ce qui prouve que le chiffrement est en cours.

![Plus de détails sur la machine virtuelle de hello](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Retour toohello PowerShell ISE. Lors de l’achèvement du script de hello, vous voyez ce qui apparaît dans la figure ci-dessous hello.

![Sortie PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate qui hello d’ordinateur virtuel est maintenant chiffré, retourner toohello portail Azure, cliquez sur **virtuels** sur hello à gauche de la page de hello. Cliquez sur nom hello de machine virtuelle de hello chiffrée. Bonjour **paramètres** panneau, cliquez sur **disques**.

![Options des paramètres](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Sur hello **disques** panneau, vous verrez que **chiffrement** est **activé**.

![Propriétés des disques](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Étapes suivantes
Dans ce document, vous avez appris comment tooencrypt une Machine virtuelle Azure. toolearn en savoir plus sur Azure Security Center, voir hello :

* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) : Découvrez comment toomonitor hello d’intégrité de vos ressources Azure
* [Gestion et répond toosecurity alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) -en savoir comment les alertes toosecurity toomanage et y répondre
* [Forum aux questions sur Azure Security Center](security-center-faq.md) – rechercher Forum aux questions sur l’utilisation du service de hello
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure
