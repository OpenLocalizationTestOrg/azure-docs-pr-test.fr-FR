---
title: aaaDeploy SAP S/4HANA ou BW/4HANA sur une machine virtuelle Azure | Documents Microsoft
description: "Déploiement de SAP S/4HANA ou BW/4HANA sur une machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Déploiement de SAP S/4HANA ou BW/4HANA sur Azure
Cet article décrit comment toodeploy S/4HANA sur Azure à l’aide de hello bibliothèque de matériel du Cloud SAP (SAP CAL) 3.0. toodeploy autres solutions SAP HANA, telles que BW/4HANA, suivent hello mêmes étapes.

> [!NOTE]
Pour plus d’informations sur hello SAP licences d’accès client, accédez à toohello [SAP Cloud application bibliothèque](https://cal.sap.com/) site Web. SAP possède également un blog sur hello [SAP Cloud Appliance bibliothèque 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Comme de 29 mai 2017, vous pouvez utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello en outre toohello préféré au moins un déploiement classique de modèle toodeploy hello licences d’accès client SAP. Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager hello et de ne pas tenir compte de modèle de déploiement classique hello.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Solution de hello toodeploy étape par étape

Hello suivant la séquence de captures d’écran montre comment toodeploy S/4HANA sur Azure à l’aide de hello des licences d’accès client SAP. hello se déroulent Hello identique pour d’autres solutions, telles que BW/4HANA.

Hello **Solutions** page répertorie quelques-unes des hello basée sur les licences d’accès client de SAP HANA les solutions disponibles sur Azure. **SAP S/4HANA 1610 FPS01, Fully-Activated équipement** est en ligne au milieu de hello :

![Solutions SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Créer un compte dans hello licences d’accès client SAP
1. toosign dans toohello SAP CAL pour hello première fois, utilisez votre utilisateur S SAP ou autre utilisateur enregistré dans SAP. Définissez ensuite un compte d’accès client SAP qui est utilisé par les appareils de toodeploy hello licences d’accès client SAP sur Azure. Dans la définition du compte de hello, vous devez :

    a. Sélectionnez le modèle de déploiement hello sur Azure (Gestionnaire de ressources ou classique).

    b. Entrez votre abonnement Azure. Abonnement tooone uniquement peut être affecté à un compte de la licence d’accès client SAP. Si vous avez besoin de plus d’un abonnement, vous devez toocreate un autre compte de licences d’accès client SAP.

    c. Donnez à hello SAP CAL autorisation toodeploy dans votre abonnement Azure.

    > [!NOTE]
    les étapes suivantes Hello montrent comment toocreate une licence d’accès client SAP compte pour les déploiements de gestionnaire de ressources. Si vous avez déjà un compte de licence d’accès client SAP qui est le modèle de déploiement classique toohello lié, vous *devez* toofollow ces toocreate étapes un nouveau compte de licences d’accès client SAP. nouveau compte de licences d’accès client SAP Hello doit toodeploy dans le modèle de gestionnaire de ressources hello.

2. Créez un compte SAP CAL. Hello **comptes** page affiche les trois possibilités pour Azure : 

    a. **Microsoft Azure (classique)** est le modèle de déploiement classique hello et n’est plus recommandée.

    b. **Microsoft Azure** est le nouveau modèle de déploiement Resource Manager hello.

    c. **Windows Azure géré par 21Vianet** est une option en Chine qui utilise le modèle de déploiement classique hello.

    toodeploy dans le modèle de gestionnaire de ressources hello, sélectionnez **Microsoft Azure**.

    ![Détails du compte SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. Entrez hello Azure **ID d’abonnement** qui se trouvent sur hello portail Azure.

   ![Comptes SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. toodeploy de licences d’accès client SAP tooauthorize hello en hello abonnement Azure que vous avez définies, cliquez sur **Authorize**. Hello suivant page s’affiche dans l’onglet du navigateur hello :

   ![Connexion aux services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Si plusieurs utilisateurs est répertorié, choisissez le compte Microsoft hello coadministrator de hello toobe lié Hello abonnement Azure que vous avez sélectionné. Hello suivant page s’affiche dans l’onglet du navigateur hello :

   ![Confirmation des services cloud d’Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Cliquez sur **Accepter**. Si l’autorisation de hello est réussie, hello définition du compte de licences d’accès client SAP s’affiche à nouveau. Après une courte période, un message confirme que le processus d’autorisation de hello a réussi.

7. tooassign hello nouvellement créée tooyour utilisateur du compte de licences d’accès client SAP, entrez votre **ID utilisateur** dans hello de zone de texte hello droit et cliquez sur **ajouter**.

   ![Association de compte toouser](./media/cal-s4h/s4h-pic8a.png)

8. Cliquez sur votre compte utilisateur de hello utiliser toosign dans toohello SAP licences d’accès client, de tooassociate **révision**. 
 
9. association de hello toocreate entre votre utilisateur et le compte de licences d’accès client SAP hello nouvellement créé, cliquez sur **créer**.

   ![Association de compte utilisateur tooSAP licence d’accès client](./media/cal-s4h/s4h-pic9b.png)

Vous avez correctement créé un compte SAP CAL capable d’effectuer les tâches suivantes :

- Utilisez le modèle de déploiement du Gestionnaire de ressources hello.
- Déployer des systèmes SAP dans votre abonnement Azure.

Vous pouvez maintenant démarrer toodeploy S/4HANA dans votre abonnement de l’utilisateur dans Azure.

> [!NOTE]
Avant de poursuivre, déterminez si vous êtes lié à des quotas de cœurs pour les machines virtuelles Azure série H. Au moment de hello, hello SAP CAL utilise H-Series machines virtuelles de Azure toodeploy parmi les solutions SAP HANA hello. Il se peut que votre abonnement Azure ne soit pas associé à des quotas de cœurs pour la série H. Dans ce cas, vous devrez peut-être toocontact prise en charge Azure tooget un quota de cœurs de série H au moins 16.

> [!NOTE]
Lorsque vous déployez une solution sur Azure Bonjour licences d’accès client SAP, vous constaterez peut-être que vous pouvez choisir qu’une seule région Azure. toodeploy dans des régions Azure autre que hello une suggéré par hello licences d’accès client SAP, vous devez toopurchase un abonnement de licence d’accès client à partir de SAP. Vous aussi avoir besoin tooopen un message avec SAP toohave votre toodeliver compte activé de licences d’accès client dans des régions Azure autre que hello celles suggérées initialement.

### <a name="deploy-a-solution"></a>Déployer une solution

Nous allons déployer une solution à partir de hello **Solutions** page Hello licences d’accès client SAP. Hello licences d’accès client SAP a deux séquences toodeploy :

- Une séquence de base qui utilise une page toodefine hello système toobe déployé
- Une séquence avancée qui vous offre différents choix en termes de tailles de machine virtuelle 

Nous allons montrer toodeployment de chemin d’accès de base hello ici.

1. Sur hello **détails du compte** page, vous devez :

    a. Sélectionnez un compte SAP CAL. (Utiliser un compte qui est associé toodeploy avec modèle de déploiement du Gestionnaire de ressources hello.)

    b. Entrez le nom de l’instance dans le champ **Name** (Nom).

    c. Sélectionnez une région Azure dans le champ **Region** (Région). Hello SAP CAL suggère une région. Si vous avez besoin d’une autre région Azure et que vous n’avez pas d’abonnement de licence d’accès client SAP, vous avez besoin d’abonnement de tooorder une licence d’accès client avec SAP.

    d. Entrez un masque de **mot de passe** pour la solution hello de huit ou neuf caractères. mot de passe Hello est utilisé pour les administrateurs de hello des différents composants de hello.

   ![Mode de base SAP CAL : créer une instance](./media/cal-s4h/s4h-pic10a.png)

2. Cliquez sur **créer**et dans la boîte de message de salutation qui s’affiche, cliquez sur **OK**.

   ![Tailles de machine virtuelle prises en charge par SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. Bonjour **clé privée** boîte de dialogue, cliquez sur **magasin** clé privée de hello toostore Bonjour licences d’accès client SAP. toouse mot de passe de clé privée de hello, cliquez sur **télécharger**. 

   ![Clé privée SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. Hello de lecture SAP CAL **avertissement** de message, puis cliquez sur **OK**.

   ![Avertissement SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    Maintenant le déploiement de hello a lieu. Après un certain temps, selon la taille de hello et la complexité de la solution de hello (licence d’accès client SAP fournit une estimation hello), hello état est affiché comme actif et opérationnel.

5. machines virtuelles de toofind hello collectées avec hello autres ressources associées dans un groupe de ressources, consultez les toohello portail Azure : 

   ![Objets de licences d’accès client SAP déployés dans le nouveau portail de hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. Sur le portail SAP CAL hello, état de hello s’affiche en tant que **Active**. solution de toohello tooconnect, cliquez sur **connexion**. Différentes options tooconnect toohello différents composants sont déployés au sein de cette solution.

   ![Instances SAP CAL](./media/cal-s4h/active_solution.png)

7. Avant de pouvoir utiliser un des systèmes de toohello déployé tooconnect hello options, cliquez sur **Getting Started Guide**. 

   ![Se connecter toohello Instance](./media/cal-s4h/connect_to_solution.png)

    noms de documentation Hello hello utilisateurs pour chacune des méthodes de connectivité hello. les mots de passe Hello pour les utilisateurs sont définies de mot de passe principal toohello que vous avez défini au début de hello hello du processus de déploiement. Dans la documentation de hello, les autres utilisateurs plus fonctionnelles sont répertoriés avec leur mot de passe, vous pouvez utiliser toosign dans toohello déployé le système. 

    Par exemple, si vous utilisez hello interface GUI SAP préinstallé sur l’ordinateur de bureau à distance Windows hello, hello système de S/4 peut ressembler à ceci :

   ![SM50 Bonjour préinstallé interface GUI SAP](./media/cal-s4h/gui_sm50.png)

    Ou, si vous utilisez hello DBACockpit, instance de hello peut ressembler à ceci :

   ![SM50 Bonjour DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

En quelques heures, une appliance SAP S/4 intègre est déployée dans Azure.

Si vous avez acheté un abonnement de licence d’accès client SAP, SAP prend entièrement en charge déploiements au travers de hello licences d’accès client SAP sur Azure. file d’attente de la prise en charge Hello est BC-VCM-licences d’accès client.







