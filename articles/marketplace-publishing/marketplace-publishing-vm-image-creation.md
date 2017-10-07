---
title: aaaCreating une image de machine virtuelle pour hello Azure Marketplace | Documents Microsoft
description: "Obtenir des instructions détaillées sur comment toocreate un ordinateur virtuel de l’image pour hello Azure Marketplace pour d’autres toopurchase."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Guide toocreate une image de machine virtuelle pour hello Azure Marketplace
Cet article, **étape 2**, vous guide à travers la préparation hello les disques durs virtuels (VHD) que vous allez déployer toohello Azure Marketplace. Vos disques durs virtuels sont foundation hello de votre référence (SKU). processus de Hello diffère selon que vous fournissez une référence basée sur Windows ou Linux. Cet article aborde ces deux scénarios. Ce processus peut être exécuté parallèlement à la procédure de [création de compte et d’enregistrement][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Définir les offres et les références SKU
Dans cette section, vous découvrez des offres toodefine hello et leurs références (SKU) associée.

Une offre est un tooall « parent » de ses références (SKU). Vous pouvez proposer plusieurs offres. Comment vous décidez toostructure vos offres est tooyou. Lorsqu’une offre est envoyée toostaging, il est envoyé, ainsi que toutes ses références (SKU). Étudiez attentivement vos identificateurs de référence (SKU), car ils seront visibles dans l’URL de hello :

* Azure.com : http://azure.microsoft.com/marketplace/partners/{espace_de_noms_partenaire}/{ID_offre}-{ID_référence}
* Portail Azure en préversion : https://portal.azure.com/#gallery/{espace_de_noms_éditeur}.{ID_offre}{ID_référence}  

Une référence (SKU) désigne hello commercial pour une image de machine virtuelle. Une image de machine virtuelle contient un disque de système d’exploitation et aucun ou plusieurs disques de données. Il s’agit essentiellement les profils de stockage complète hello pour un ordinateur virtuel. Chaque disque a un disque dur virtuel est nécessaire par disque. Les disques de données vierge même nécessitent un toobe de disque dur virtuel créé.

Quel que soit le système d’exploitation que vous utilisez, ajoutez uniquement hello nombre minimal de disques de données requis par hello référence (SKU). Les clients ne peut pas supprimer les disques qui font partie d’une image au moment de hello du déploiement, mais peuvent toujours ajouter des disques pendant ou après le déploiement si nécessaire.

> [!IMPORTANT]
> **Ne modifiez pas le nombre de disques dans une nouvelle version de l’image.** Si vous devez reconfigurer les disques de données dans l’image de hello, définissez une nouvelle référence SKU. Publication d’une nouvelle version de l’image avec les nombres de disque différent aura potentiel hello de rupture du nouveau déploiement basé sur la nouvelle version d’image hello dans le cas des déploiements automatique mise à l’échelle des solutions grâce à des modèles ARM et d’autres scénarios.
>
>

### <a name="11-add-an-offer"></a>1.1 Ajouter une offre
1. Connectez-vous à toohello [portail de publication] [ link-pubportal] à l’aide de votre compte vendeur.
2. Sélectionnez hello **virtuels** onglet Hello portail de publication. Dans le champ d’entrée demandée hello, entrez votre nom de l’offre. nom de l’offre Hello est généralement hello nom de produit de hello ou un service que vous envisagez de toosell Bonjour Azure Marketplace.
3. Sélectionnez **Créer**.

### <a name="12-define-a-sku"></a>1.2 Définir une référence SKU
Après avoir ajouté une offre, vous devez toodefine et identifiez vos références (SKU). Vous pouvez proposer plusieurs offres, chaque offre étant elle-même associée à plusieurs références SKU. Lorsqu’une offre est envoyée toostaging, il est envoyé, ainsi que toutes ses références (SKU).

1. **Ajoutez une référence SKU.** Hello référence (SKU) requiert un identificateur qui est utilisé dans les URL hello. identificateur de Hello doit être unique au sein de votre profil de publication, mais il n’existe aucun risque de collision d’identificateur avec d’autres éditeurs.

   > [!NOTE]
   > offre de Hello et identificateurs de référence (SKU) sont affichent dans l’URL d’offre hello Bonjour Marketplace.
   >
   >
2. **Ajoutez une description de votre référence SKU.** Des descriptions résumées étant toocustomers visible, vous devez les rendre facilement accessibles en lecture. Ces informations n’a pas besoin toobe bloqué jusqu'à ce que la phase de « Push tooStaging » hello. En attendant, vous êtes libre tooedit il.
3. Si vous utilisez des références (SKU) basé sur Windows, suivez les liens suggérés hello tooacquire hello approuvée des versions de Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Créer un disque dur virtuel compatible avec Azure (Linux)
Cette section se concentre sur les meilleures pratiques pour la création d’une image d’ordinateur virtuel Linux pour hello Azure Marketplace. Pour une procédure pas à pas, consultez toohello suivant documentation : [création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Créer un disque dur virtuel compatible avec Azure (Windows)
Cette section concentre sur hello étapes toocreate une référence (SKU) basé sur Windows Server pour hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Assurez-vous que vous utilisez hello corriger les disques durs virtuels de base
Hello, système d’exploitation disque dur virtuel pour votre image de machine virtuelle doit être basé sur une image de base approuvé par Azure qui contient Windows Server ou SQL Server.

toobegin, créer une machine virtuelle à partir de hello suivant des images, situés à hello [portail Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])

Vous trouverez également des ces liens Bonjour portail de publication sous la page de référence (SKU) hello.

> [!TIP]
> Si vous utilisez le portail Azure actuel de hello ou de PowerShell, les images Windows Server publiées sur 8 septembre 2014 et versions ultérieures sont approuvées.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Créer votre machine virtuelle Windows
À partir du portail Microsoft Azure hello, vous pouvez créer votre machine virtuelle basée sur une image de base approuvée en quelques étapes simples. Hello Voici une vue d’ensemble du processus de hello :

1. Dans la page d’image de base hello, sélectionnez **créer un ordinateur virtuel** toobe dirigées toohello nouvelle [portail Microsoft Azure][link-azure-portal].

    ![dessin][img-acom-1]
2. Portail toohello avec hello compte Microsoft et de mot de passe hello abonnement Azure que vous souhaitez toouse vous connecter.
3. Suivez hello invites toocreate une machine virtuelle à l’aide d’image de base hello que vous avez sélectionné. Vous devez tooprovide un nom d’hôte (nom de l’ordinateur de hello), le nom d’utilisateur (inscrit en tant qu’administrateur) et le mot de passe pour hello machine virtuelle.

    ![dessin][img-portal-vm-create]
4. Sélectionnez la taille hello de hello VM toodeploy :

    a.    Si vous envisagez toodevelop hello disque dur virtuel local, taille de hello n’a pas d’importance. Utilisez l’une des hello machines virtuelles plus petites.

    b.    Si vous envisagez d’image de hello toodevelop dans Azure, pensez à l’aide de hello recommandé de tailles de machine virtuelle pour l’image sélectionnée de hello.

    c.    Pour plus d’informations de tarification, consultez toohello **recommandé niveaux tarifaires** sélecteur sur hello portal. Elle fournira hello trois tailles recommandées fournies par le serveur de publication hello. (Dans ce cas, serveur de publication hello est Microsoft.)

    ![dessin][img-portal-vm-size]
5. Définissez les propriétés :

    a.    Pour un déploiement rapide, vous pouvez laisser vos valeurs par défaut pour les propriétés hello sous hello **Configuration facultative** et **groupe de ressources**.

    b.    Sous **compte de stockage**, vous pouvez éventuellement sélectionner compte de stockage hello dans le système d’exploitation de hello disque dur virtuel sera stocké.

    c.    Sous **groupe de ressources**, vous pouvez éventuellement sélectionner groupe logique de hello dans le tooplace hello machine virtuelle.
6. Sélectionnez hello **emplacement** pour le déploiement :

    a.    Si vous envisagez toodevelop hello disque dur virtuel local, emplacement de hello est sans importance, car vous allez télécharger hello image tooAzure plus tard.

    b.    Si vous envisagez d’image de hello toodevelop dans Azure, envisagez d’utiliser une des régions d’américaine de Microsoft Azure hello à partir du début de hello. Cela accélère le processus copie hello VHD que Microsoft effectue à votre place lorsque vous envoyez votre image pour la certification.

    ![dessin][img-portal-vm-location]
7. Cliquez sur **Créer**. Hello machine virtuelle démarre toodeploy. En quelques minutes, vous avez un déploiement réussi et procéder à l’image de hello toocreate pour votre référence (SKU).

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 développer votre disque dur virtuel dans le cloud de hello
Nous recommandons vivement que vous développez votre disque dur virtuel dans le cloud de hello à l’aide du protocole RDP (Remote Desktop). Vous vous connectez tooRDP hello nom d’utilisateur et mot de passe spécifié lors de la configuration.

> [!IMPORTANT]
> Si vous développez votre disque dur virtuel sur site (ce qui n’est pas recommandé), consultez la page [Création d’une image de machine virtuelle sur site](marketplace-publishing-vm-image-creation-on-premise.md). Téléchargement de votre disque dur virtuel n’est pas nécessaire si vous développez dans le cloud de hello.
>
>

**Se connecter par RDP à l’aide de hello [portail Microsoft Azure][link-azure-portal]**

1. Sélectionnez **Parcourir** > **Machines virtuelles**.
2. panneau des machines virtuelles Hello s’ouvre. Assurez-vous que cette machine virtuelle que vous souhaitez tooconnect avec hello est en cours d’exécution, puis sélectionnez-le dans la liste hello des machines virtuelles déployées.
3. Ouvre un panneau qui décrit hello sélectionné la machine virtuelle. En haut de hello, cliquez sur **connexion**.
4. Vous êtes invité à tooenter hello mot de passe que vous avez spécifié lors de la configuration.

**Se connecter via RDP à l’aide de PowerShell**

toodownload un ordinateur local tooa du fichier Bureau à distance, utilisez hello [applet de commande Get-AzureRemoteDesktopFile][link-technet-2]. Dans commande toouse cette applet de commande, vous devez tooknow hello nom service de hello et nom de machine virtuelle de hello. Si vous avez créé hello VM hello [portail Microsoft Azure][link-azure-portal], vous pouvez trouver ces informations sous les propriétés de la machine virtuelle :

1. Dans le portail de Microsoft Azure hello, sélectionnez **Parcourir** > **machines virtuelles**.
2. panneau des machines virtuelles Hello s’ouvre. Sélectionnez hello machine virtuelle que vous avez déployé.
3. Ouvre un panneau qui décrit hello sélectionné la machine virtuelle.
4. Cliquez sur **Propriétés**.
5. Hello première partie du nom de domaine hello est le nom du service hello. nom d’hôte Hello est le nom d’ordinateur virtuel hello.

    ![dessin][img-portal-vm-rdp]
6. Hello applet de commande toodownload hello fichier RDP pour bureau local de l’administrateur toohello hello créé machine virtuelle est la suivante.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Peut trouver plus d’informations sur le protocole RDP sur MSDN dans l’article de hello [connecter tooan machine virtuelle Azure avec RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Configurer une machine virtuelle et créer votre référence SKU**

Après le système d’exploitation du hello que disque dur virtuel est téléchargé, utilisez Hyper-v et configurer un toobegin VM création de votre référence (SKU). Obtenir des instructions détaillées, consultez hello TechNet lien : [HyperV d’installer et configurer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 choisir la taille de disque dur virtuel correct de hello
système de d’exploitation de Windows Hello disque dur virtuel dans votre image de machine virtuelle doit être créé comme un disque dur virtuel au format fixe de 128 Go.  

Si la taille physique de hello est inférieure à 128 Go, hello disque dur virtuel doit être fragmenté. images de Windows et SQL Server base Hello fournies déjà respecter ces exigences, par conséquent, ne modifiez pas la taille de format ou hello hello Hello obtenu de disque dur virtuel.  

Les disques de données peuvent avoir une taille maximale de 1 To. Lorsque vous décidez de la taille du disque hello, n’oubliez pas que les clients ne peut pas redimensionner les disques durs virtuels au sein d’une image au moment de hello du déploiement. Ce type de disque dur virtuel doit être créé comme disque dur virtuel au format fixe. Ils doivent également être fragmentés. Les disques de données peuvent être vides ou contenir des données.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 installez les derniers correctifs de Windows hello
Hello images de base contiennent des derniers correctifs de hello des tootheir date de publication. Avant de publier le système d’exploitation de hello disque dur virtuel que vous avez créé, assurez-vous que Windows Update a été exécuté et que tous hello critique dernières mises à jour de sécurité importantes ont été installés.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 Effectuer les autres tâches de configuration et de planification utiles
Si une configuration supplémentaire est nécessaire, envisagez d’utiliser une tâche planifiée qui s’exécute au démarrage toomake tout toohello modifications finales machine virtuelle une fois qu’il a été déployé :

* Il s’agit d’une tâche de hello meilleures pratiques toohave supprime après l’exécution réussie.
* Aucune configuration ne doit s’appuient sur des lecteurs autres que les lecteurs C et D, car il s’agit hello uniquement deux lecteurs de toujours tooexist. Le lecteur C est le disque du système d’exploitation hello et le lecteur D est le disque local temporaire de hello.

### <a name="37-generalize-hello-image"></a>3.7 généraliser l’image de hello
Toutes les images Bonjour Azure Marketplace doivent être réutilisables de façon générique. En d’autres termes, le système d’exploitation de hello disque dur virtuel doit être généralisé :

* Pour Windows, hello image doit être un « Sysprep », et aucune configuration ne doit être effectuée qui ne prennent pas en charge hello **sysprep** commande.
* Vous pouvez exécuter la commande suivante à partir de hello répertoire % windir%\System32\Sysprep de hello.

        sysprep.exe /generalize /oobe /shutdown

  Obtenir des conseils sur comment système d’exploitation de hello toosysprep est fourni à l’étape de hello les article MSDN suivant : [création et téléchargement d’un disque dur virtuel de Windows Server de tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Déployer une machine virtuelle à partir de vos disques durs virtuels
Après avoir téléchargé vos disques durs virtuels (VHD de système d’exploitation hello généralisé et les données de zéro ou plusieurs disques durs virtuels de disque) tooan compte de stockage Azure, vous pouvez les enregistrer en tant qu’une image de machine virtuelle de l’utilisateur. Vous pouvez tester cette image. Remarque : étant donné que votre disque dur virtuel du système d’exploitation est généralisé, vous ne pouvez directement déployer hello machine virtuelle en fournissant hello URL de disque dur virtuel.

toolearn plus d’informations sur les images de machine virtuelle, hello révision suivant des billets de blog :

* [VM Image](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [VM Image PowerShell How To](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [À propos d’images de machines virtuelles dans Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Configurer les outils nécessaires hello, PowerShell et CLI d’Azure
* [Comment toosetup PowerShell](/powershell/azure/overview)
* [Comment toosetup CLI d’Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 Créer une image de machine virtuelle d’utilisateur
#### <a name="capture-vm"></a>Capturer la machine virtuelle
Veuillez lire les liens hello indiquées ci-dessous pour obtenir des conseils sur la capture hello machine virtuelle à l’aide de PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [interface de ligne de commande Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Généraliser une image
Veuillez lire les liens hello indiquées ci-dessous pour obtenir des conseils sur la capture hello machine virtuelle à l’aide de PowerShell/API/Azure CLI.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [interface de ligne de commande Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 Déployer une machine virtuelle à partir d’une image de machine virtuelle d’utilisateur
toodeploy une machine virtuelle à partir d’une image de machine virtuelle de l’utilisateur, vous pouvez utiliser hello actuel [portail Azure](https://manage.windowsazure.com) ou PowerShell.

**Déployer un ordinateur virtuel à partir du portail Azure actuel de hello**

1. Accédez trop**nouveau** > **de calcul** > **virtuels** > **à partir de la galerie**.

    ![dessin][img-manage-vm-new]
2. Accédez trop**Mes images**, et puis sélectionnez hello une image de machine virtuelle à partir de quels toodeploy une machine virtuelle :

   1. Image de toowhich prêtez attention particulière étant donné que vous sélectionnez hello **Mes images** affichage répertorie les images de système d’exploitation et les images de machine virtuelle.
   2. Examinez nombre hello de disques peut aider à déterminer quel type d’image que vous déployez, étant donné que la majorité de hello des images de machine virtuelle ont plusieurs disques. Toutefois, il est toujours possible de toohave une image de machine virtuelle avec un seul système d’exploitation disque, qui aurait ensuite **nombre de disques** définir too1.

      ![dessin][img-manage-vm-select]
3. Suivez l’Assistant de création de machine virtuelle hello et spécifiez le nom d’ordinateur virtuel hello, taille de machine virtuelle, emplacement, nom d’utilisateur et mot de passe.

**Déployer une machine virtuelle à partir de vos disques durs virtuels**

toodeploy qu'une machine virtuelle large de hello généralisé l’image de machine virtuelle venez de créer, vous pouvez utiliser hello suivant d’applets de commande.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Pour obtenir une assistance supplémentaire, consultez [Troubleshooting common issues encountered during VHD creation] \(Résolution des problèmes courants rencontrés durant la création du disque dur virtuel).
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Obtenir une certification pour votre image de machine virtuelle
étape suivante de Hello lors de la préparation de votre image de machine virtuelle pour hello Azure Marketplace est toohave qu'il certifié.

Ce processus inclut un outil de certification particulière, téléchargement hello vérification résultats toohello Azure conteneur où se trouvent vos disques durs virtuels, l’ajout d’une offre, définissant votre référence (SKU) et l’envoi de votre machine virtuelle de l’image pour la certification.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 télécharger et exécuter hello outil de Test de Certification pour Azure Certified
outil de certification Hello s’exécute sur une machine virtuelle en cours d’exécution, configurée à partir de votre image de machine virtuelle utilisateur, tooensure qui hello image de machine virtuelle est compatible avec Microsoft Azure. Il vérifie que les instructions hello et des exigences sur la préparation de votre disque dur virtuel ont été remplies. sortie de Hello de l’outil de hello est un rapport de compatibilité, qui doit être téléchargé sur le portail de publication de hello lors de la certification de demande.

outil de certification Hello peut être utilisé avec Windows et les machines virtuelles Linux. Il connecte tooWindows sur des ordinateurs virtuels via PowerShell et connecte tooLinux machines virtuelles, via SSH.Net :

1. Commencez par télécharger outil de certification hello en hello [site de téléchargement Microsoft][link-msft-download].
2. Ouvrez l’outil de certification hello, puis cliquez sur hello **démarrer un nouveau Test** bouton.
3. À partir de hello **tester les informations** écran, entrez un nom pour la série de tests hello.
4. Indiquez si votre machine virtuelle est exécutée sous Linux ou Windows. En fonction de votre choix, sélectionnez les options suivantes hello.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Se connecter hello certification outil tooa image Linux VM**
1. Mode d’authentification SSH sélectionnez hello : fichier de mot de passe ou la clé.
2. Si vous utilisez l’authentification par mot de passe, entrez le nom du système DNS (Domain Name) hello, nom d’utilisateur et mot de passe.
3. Si l’authentification du fichier de clé, entrez le nom DNS de hello, nom d’utilisateur et emplacement de la clé privée.

   ![Authentification de l’image de machine virtuelle Linux par mot de passe][img-cert-vm-pswd-lnx]

   ![Authentification de l’image de machine virtuelle Linux par fichier de clé][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Image de machine virtuelle basées sur Windows hello certification outil tooa de connexion**
1. Entrez le nom de machine virtuelle DNS hello complet (par exemple, MyVMName.Cloudapp.net).
2. Entrez le mot de passe et le nom d’utilisateur hello.

   ![Authentification de l’image de machine virtuelle Windows par mot de passe][img-cert-vm-pswd-win]

Après avoir sélectionné les options correctes hello pour votre image d’ordinateur virtuel Windows ou Linux, sélectionnez **tester la connexion** tooensure qu’une connexion valide à des fins de test SSH.Net ou PowerShell. Une fois une connexion est établie, sélectionnez **suivant** test de hello toostart.

Lorsque le test de hello est terminée, vous recevez des résultats de hello (Pass/Échec / d’avertissement) pour chaque élément de test.

![Scénarios de test pour une image de machine virtuelle Linux][img-cert-vm-test-lnx]

![Scénarios de test pour une image de machine virtuelle Windows][img-cert-vm-test-win]

Si un des tests de hello échouent, votre image ne sera pas validée. Si cela se produit, passez en revue les exigences de hello et apportez les modifications nécessaires.

Une fois hello de test automatique, vous êtes invité tooprovide une entrée supplémentaire sur votre image de machine virtuelle via un écran questionnaire.  Répondez aux questions de hello, puis sélectionnez **suivant**.

![Questionnaire de l’outil de certification][img-cert-vm-questionnaire]

![Questionnaire de l’outil de certification][img-cert-vm-questionnaire-2]

Une fois que vous avez terminé le questionnaire de hello, vous pouvez fournir des informations supplémentaires telles que les informations d’accès SSH pour hello image Linux VM et obtenir une explication des évaluations ayant échouées. Vous pouvez télécharger les résultats de test hello et fichiers journaux d’hello exécuté des cas de test questionnaire de toohello Ajout tooyour réponses. Enregistrer les résultats de hello Bonjour même conteneur que vos disques durs virtuels.

![Enregistrer les résultats du test de certification][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 obtenir l’URI de signature d’accès partagé hello pour vos images de machine virtuelle
Pendant le processus de publication de hello, vous spécifiez des identificateurs hello uniform resource identifier (URI) qui mènent tooeach Hello disques durs virtuels que vous avez créé pour votre référence (SKU). Microsoft a besoin de toothese d’accès aux disques durs virtuels pendant le processus de certification hello. Par conséquent, vous devez toocreate un URI de signature d’accès partagé pour chaque disque dur virtuel. Il s’agit de hello URI qui doit être entré dans le **Images** onglet Bonjour portail de publication.

signature d’accès partagé Hello URI créé doit respecter toohello suivant les exigences suivantes :

* Lors de la génération des URI de signature d’accès partagé pour vos disques durs virtuels, les autorisations de liste et de lecture seule sont suffisantes. Ne fournissez pas d’accès en écriture ou en suppression.
* Durée Hello pour l’accès doit être au minimum de trois (3) semaines à lors de la signature d’accès partagé hello URI est créé.
* toosafeguard pour l’heure UTC, jour select hello avant hello date actuelle. Par exemple, si hello date actuelle est le 6 octobre 2014, sélectionnez 5/10/2014.

URL de SAP peut être généré dans plusieurs façons tooshare votre disque dur virtuel pour Azure Marketplace.
Suivantes sont hello 3 outils recommandés :

1.  Explorateur de stockage Azure
2.  Explorateur de stockage Microsoft
3.  Interface de ligne de commande Azure

**Azure Storage Explorer (recommandé pour les utilisateurs Windows)**

Décrit les étapes de hello pour générer des URL de SAP à l’aide de l’Explorateur de stockage Azure

1. Téléchargez [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) à partir de CodePlex. Accédez trop[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) et cliquez sur **« Téléchargement »**.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Téléchargez [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) et installez après avoir décompressé l’archive.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Après que qu’il est installé, ouvrez l’application hello.
4. Cliquez sur **Ajouter un compte**.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Spécifiez le nom de compte de stockage hello, clé de compte de stockage et un domaine de points de terminaison de stockage. Ceci est le compte de stockage hello dans votre abonnement Azure où vous avez conservé votre disque dur virtuel sur le portail Azure.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Une fois que l’Explorateur de stockage Azure est connecté tooyour compte de stockage spécifique, il démarrera affichant tous hello contient dans le compte de stockage hello. Sélectionnez le conteneur hello où vous avez copié le fichier de disque dur virtuel disque hello système d’exploitation (et disques de données, si elles sont applicables pour votre scénario).

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Après avoir sélectionné un conteneur d’objets blob hello, Azure Storage Explorer démarre montrant les fichiers hello conteneur hello. Sélectionnez un fichier d’image hello (.vhd) qui doit toobe soumis.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Après avoir sélectionné le fichier .vhd de hello dans le conteneur de hello, cliquez sur hello **sécurité** onglet.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  Bonjour **sécurité de conteneur d’objets Blob** boîte de dialogue, les valeurs par défaut de congé hello sur hello **niveau d’accès** onglet, puis cliquez sur **Signatures d’accès partagé** onglet.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Suivez les étapes de hello ci-dessous toogenerate un URI de signature d’accès partagé pour l’image de disque dur virtuel hello :

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **Accéder à partir de :** toosafeguard pour l’heure UTC, jour select hello avant hello date actuelle. Par exemple, si hello date actuelle est le 6 octobre 2014, sélectionnez 5/10/2014.

    b. **L’accès est autorisé à :** sélectionner une date qui est au moins trois semaines après hello **accès autorisé à partir de** date.

    c. **Actions autorisées :** hello sélectionnez **liste** et **en lecture** autorisations.

    d. Si vous avez sélectionné votre fichier .vhd correctement, alors que votre fichier s’affiche dans **tooaccess de nom d’objet Blob** avec l’extension .vhd.

    e. Cliquez sur **Generate Signature**(Générer la signature).

    f. Dans **généré Shared Access Signature URI de ce conteneur**, recherchez hello suivant mis en surbrillance ci-dessus :

       - Assurez-vous que le nom du fichier image et **« .vhd »** sont Bonjour URI.
       - Extrémité hello de signature de hello, assurez-vous que **« = rl »** s’affiche. Cela montre qu’un accès en lecture seule et de liste a été fourni avec succès.
       - Au milieu de la signature de hello, assurez-vous que **« sr = c «** s’affiche. Cela montre que vous avez l’accès de niveau conteneur

11. tooensure qui hello généré shared access signature URI fonctionne, cliquez sur **Test dans le navigateur**. Il doit commencer le processus de téléchargement hello.

12. Copiez l’URI de signature d’accès partagé hello. Il s’agit de toopaste d’URI hello en hello portail de publication.

13. Répétez les étapes 6 à 10 pour chaque disque dur virtuel Bonjour référence (SKU).

**Explorateur de stockage Microsoft Azure (Windows/MAC/Linux)**

Décrit les étapes pour générer des URL de SAP à l’aide de Microsoft Azure Storage Explorer hello

1.  Téléchargez Microsoft Azure Storage Explorer depuis le site web [http://storageexplorer.com/](http://storageexplorer.com/). Accédez trop[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) et cliquez sur **« Télécharger pour Windows »**.

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Après que qu’il est installé, ouvrez l’application hello.

3.  Cliquez sur **Ajouter un compte**.

4.  Configurer un abonnement de tooyour Microsoft Azure Storage Explorer par tooyour compte de connexion

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Toostorage compte, sélectionnez hello conteneur

6.  Sélectionnez **« Obtenir la signature de partage d’accès... »** à l’aide du bouton droit sur Hello **conteneur**

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Date de début, date d’expiration et autorisations de la mise à jour comme suit

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Heure de début :** toosafeguard pour l’heure UTC, jour select hello avant hello date actuelle. Par exemple, si hello date actuelle est le 6 octobre 2014, sélectionnez 5/10/2014.

    b.  **Délai d’expiration :** sélectionner une date qui est au moins trois semaines après hello **l’heure de début** date.

    c.  **Autorisations :** hello sélectionnez **liste** et **en lecture** autorisations

8.  Copiez l’URI de signature d’accès partagé du conteneur

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    URL de SAP générée est pour le conteneur de niveau et nous devons maintenant nom de disque dur virtuel tooadd.

    Format d’URL SAS de niveau de conteneur :`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Insérer un nom de disque dur virtuel après le nom du conteneur hello dans l’URL de SAP comme indiqué ci-dessous`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Exemple :

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd est hello nom de disque dur virtuel puis URL SAS du disque dur virtuel`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Assurez-vous que le nom du fichier image et **« .vhd »** sont Bonjour URI.
    - Au milieu de la signature de hello, assurez-vous que **« sp = rl »** s’affiche. Cela montre qu’un accès en lecture seule et de liste a été fourni avec succès.
    - Au milieu de la signature de hello, assurez-vous que **« sr = c «** s’affiche. Cela montre que vous avez l’accès de niveau conteneur

9.  tooensure qui hello d’accès partagé générée signature URI fonctionne, le tester dans le navigateur. Il doit commencer le processus de téléchargement hello

10. Copiez l’URI de signature d’accès partagé hello. Il s’agit de toopaste d’URI hello en hello portail de publication.

11. Répétez ces étapes pour chaque disque dur virtuel Bonjour référence (SKU).

**Interface de ligne de commande Azure (méthode recommandée pour l’intégration continue/non Windows)**

Décrit les étapes de hello pour générer des URL de SAP à l’aide de CLI d’Azure

1.  Téléchargez l’interface de ligne de commande Microsoft Azure [ici](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Vous y trouverez également les différents liens pour  **[Windows](http://aka.ms/webpi-azure-cli)**  et  **[Mac OS](http://aka.ms/mac-azure-cli)**.

2.  Après le téléchargement, veuillez effectuer l’installation

3.  Créez un fichier PowerShell avec le code suivant et enregistrez-le en local

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Mettre à jour suivantes de hello dans les paramètres ci-dessus

    a. **`<StorageAccountName>`** : indiquez le nom de votre compte de stockage

    b. **`<Storage Account Key>`** : indiquez la clé de votre compte de stockage

    c. **`<Permission Start Date>`**: toosafeguard pour l’heure UTC, jour select hello avant hello date actuelle. Par exemple, si hello date actuelle est 26 octobre 2016, puis la valeur doit être 25/10/2016

    d. **`<Permission End Date>`**: Permet de sélectionner une date qui est au moins trois semaines après hello **Date de début**. La valeur doit donc être **11/02/2016**.

    Voici un code d’exemple hello après la mise à jour les paramètres appropriés

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Ouvrez l’éditeur PowerShell avec le mode « Exécuter en tant qu’administrateur » et ouvrez le fichier de l’étape 3.

5.  Script d’exécution hello et fournira que Hello d’URL SAS pour l’accès au niveau du conteneur

    Suivant sera sortie hello partie hello Signature SAS et copie hello mis en surbrillance dans un bloc-notes

    ![dessin](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Maintenant, vous obtiendrez au niveau du conteneur URL SAS et que vous devez le nom de disque dur virtuel tooadd.

    URL SAS de niveau de conteneur

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Insérer le nom du disque dur virtuel après le nom du conteneur hello dans l’URL de SAP comme indiqué ci-dessous`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Exemple :

    TestRGVM201631920152.vhd est hello nom de disque dur virtuel puis URL SAS du disque dur virtuel

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Assurez-vous que votre nom de fichier image et un « .vhd » sont Bonjour URI.
    -   Dans le milieu de la signature de hello, vérifiez que « sp = rl » s’affiche. Cela montre qu’un accès en lecture seule et de liste a été fourni avec succès.
    -   Dans le milieu de la signature de hello, vérifiez que « sr = c » s’affiche. Cela montre que vous avez l’accès de niveau conteneur

8.  tooensure qui hello d’accès partagé générée signature URI fonctionne, le tester dans le navigateur. Il doit commencer le processus de téléchargement hello

9.  Copiez l’URI de signature d’accès partagé hello. Il s’agit de toopaste d’URI hello en hello portail de publication.

10. Répétez ces étapes pour chaque disque dur virtuel Bonjour référence (SKU).


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 fournissent des informations sur l’image de machine virtuelle hello et demander la certification Bonjour portail de publication
Après avoir créé votre offre et la référence (SKU), vous devez entrer les détails de l’image hello associés à cette référence SKU :

1. Accédez toohello [portail de publication][link-pubportal], puis connectez-vous avec votre compte vendeur.
2. Sélectionnez hello **images de machine virtuelle** onglet.
3. Identificateur Hello répertorié en hello haut hello est réellement identificateur d’offre hello et identificateur de référence (SKU) de hello pas.
4. Spécifier les propriétés de hello sous hello **SKU** section.
5. Sous **famille de système d’exploitation**, cliquez sur le type de système d’exploitation associé au VHD de système d’exploitation hello hello.
6. Bonjour **système d’exploitation** zone, décrire le système d’exploitation de hello. Envisagez un format du type Famille de systèmes d’exploitation, Type, Version et Mises à jour, Par exemple, « Windows Server Datacenter 2014 R2 ».
7. Sélectionnez toosix recommandé de tailles de machine virtuelle. Il s’agit de recommandations qui obtenir du client toohello affichées dans le panneau de niveau de tarification hello Bonjour Azure Portal lors décider toopurchase et du déploiement de votre image. **Il s’agit uniquement des recommandations. client de Hello est en mesure de tooselect n’importe quelle taille de machine virtuelle qui prend en charge les disques hello spécifié dans votre image.**
8. Entrez la version de hello. le champ version Hello encapsule un produit de hello tooidentify version sémantique et ses mises à jour :
   * Versions doivent être de hello x.y.ze, où X, Y et Z sont des entiers.
   * Les images contenues dans des références SKU différentes peuvent avoir différentes versions majeures et mineures.
   * Versions au sein d’une référence (SKU) doivent être uniquement les modifications incrémentielles, ce qui augmente la version du correctif hello (Z à partir de X.Y.Z).
9. Bonjour **URL de disque dur virtuel du système d’exploitation** , entrez la signature d’accès partagé hello URI créé pour le système d’exploitation de hello disque dur virtuel.
10. Si des disques de données associés à cette référence (SKU), sélectionnez toowhich (LUN) numéro LUN hello vous souhaitez que cette toobe de disque de données monté lors du déploiement.
11. Bonjour **URL de disque dur virtuel de numéro d’unité logique X** , entrez la signature d’accès partagé hello URI créé pour les données de salutation premier disque dur virtuel.

    ![dessin](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Problèmes communs avec les URL SAS et résolution

|Problème|Message d’échec|Correctif|Lien vers la documentation|
|---|---|---|---|
|Échec lors de la copie d’images : « ? » est introuvable dans l’URL SAS|Échec : copie d’images. À l’aide des objets blob n’a pas pu toodownload fourni Uri SAS.|À l’aide de mise à jour hello Url SAS recommandé d’outils|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Échec lors de la copie d’images : les paramètres « st » et « se » ne sont pas présents dans l’URL SAS|Échec : copie d’images. À l’aide des objets blob n’a pas pu toodownload fourni Uri SAS.|Mettre à jour hello Url de SAP avec des dates de début et de fin sur celui-ci|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Échec lors de la copie d’images : « sp=rl » n’est pas présent dans l’URL SAS|Échec : copie d’images. À l’aide des objets blob n’a pas pu toodownload fourni Uri SAS|Mettre à jour hello Url SAS avec les autorisations définies en tant que « Lecture » et « liste|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Échec lors de la copie d’images : l’URL SAS contient des espaces blancs dans le nom du disque dur virtuel|Échec : copie d’images. À l’aide des objets blob n’a pas pu toodownload fourni Uri SAS.|Mettre à jour hello Url SAS, sans espaces blancs|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Échec lors de la copie d’images : erreur d’autorisation d’URL SAS|Échec : copie d’images. Blob n’a pas pu toodownload en raison de l’erreur de tooauthorization|Régénérer hello Url SAS|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Étape suivante
Une fois que vous avez terminé avec les informations de référence (SKU) hello, vous pouvez déplacer vers l’avant toohello [guide contenu marketing d’Azure Marketplace][link-pushstaging]. Dans cette étape du processus de publication de hello, vous fournissez hello marketing trop de contenu, la tarification et autres préalable nécessaire informations**étape 3 : test de votre machine virtuelle offrent intermédiaire**, où vous tester divers scénarios de cas d’utilisation avant le déploiement Hello toohello offre Azure Marketplace pour une visibilité publique et d’achat.  

## <a name="see-also"></a>Voir aussi
* [Mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
