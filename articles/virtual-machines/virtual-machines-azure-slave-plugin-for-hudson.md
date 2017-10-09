---
title: "aaaHow toouse hello Azure esclave plug-in avec une intégration continue Hudson | Documents Microsoft"
description: "Décrit comment toouse hello Azure esclave plug-in avec une intégration continue Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Comment toouse hello Azure esclave plug-in avec une intégration continue Hudson
Hello Azure esclave Hudson plug-in vous permet de nœuds d’esclave tooprovision sur Azure lorsque les builds en cours d’exécution distribuée.

## <a name="install-hello-azure-slave-plug-in"></a>Installer hello esclave Azure plug-in
1. Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.
2. Bonjour **gérer les Hudson** page, cliquez sur **gérer les plug-ins**.
3. Cliquez sur hello **disponible** onglet.
4. Cliquez sur **recherche** et type **Azure** toolimit hello liste toorelevant plug-ins.
   
    Si vous choisissez tooscroll liste hello de plug-ins disponibles, vous trouverez hello esclave Azure plug-in sous hello **gestion du Cluster et distribués générer** section Bonjour **d’autres** onglet.
5. Sélectionnez la case à cocher hello **plug-in de Azure esclave**.
6. Cliquez sur **Installer**.
7. Redémarrez Hudson.

Maintenant que hello plug-in est installé, les étapes suivantes hello serait hello tooconfigure plug-in avec votre toocreate un modèle qui sera utilisé pour la création d’hello machine virtuelle pour le noeud esclave hello et un profil de l’abonnement Azure.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Configurer hello esclave Azure plug-in avec le profil de votre abonnement
Un profil d’abonnement, également désignées tooas paramètres de publication, est un fichier XML qui contient les informations d’identification sécurisées ainsi que certaines informations supplémentaires, vous aurez besoin de toowork avec Azure dans votre environnement de développement. tooconfigure hello Azure esclave plug-in, vous devez :

* Votre ID d’abonnement
* Un certificat de gestion pour votre abonnement

Vous les trouverez dans votre [profil d’abonnement]. Vous trouverez ci-dessous un exemple de profil d'abonnement.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Une fois que vous avez votre profil d’abonnement, suivez ces hello de tooconfigure étapes subordonnées Azure plug-in.

1. Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.
2. Cliquez sur **Configure System**(Configurer le système).
3. Défiler hello de hello page toofind **Cloud** section.
4. Cliquez sur **Add new cloud > Microsoft Azure** (Ajouter un nouveau cloud > Microsoft Azure).
   
    ![ajouter un cloud][add new cloud]
   
    Cette opération affiche les champs hello où vous avez besoin de tooenter détails de votre abonnement.
   
    ![configurer le profil][configure profile]
5. Copiez le certificat de gestion et l’id d’abonnement hello à partir de votre profil d’abonnement et les coller dans les champs appropriés hello.
   
    Lors de la copie du certificat gestion et l’id d’abonnement hello, **pas** inclure les guillemets hello qui entourent les valeurs hello.
6. Cliquez sur **Verify configuration**(Vérifier la configuration).
7. Lors de la configuration de hello est vérifiée avec succès, cliquez sur **enregistrer**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Définir un modèle d’ordinateur virtuel pour hello Azure esclave plug-in
Un modèle d’ordinateur virtuel définit les paramètres de hello hello plug-in utilise toocreate un nœud subordonné sur Azure. Bonjour suit nous allons créer le modèle pour un VM Ubuntu.

1. Dans le tableau de bord Hudson de hello, cliquez sur **gérer les Hudson**.
2. Cliquez sur **Configure System**(Configurer le système).
3. Défiler hello de hello page toofind **Cloud** section.
4. Au sein de hello **Cloud** section, recherchez **ajouter un modèle de Machine virtuelle Azure** et cliquez sur hello **ajouter** bouton.
   
    ![ajouter un modèle d'ordinateur virtuel][add vm template]
5. Spécifiez un nom de service cloud dans hello **nom** champ. Si nom hello que vous spécifiez fait référence tooan existant du service cloud, hello machine virtuelle est approvisionné dans ce service. Dans le cas contraire, Azure en crée un nouveau.
6. Bonjour **Description** , entrez le texte qui décrit le modèle hello que vous créez. Ces informations sont uniquement à des fins documentaires et ne sont pas utilisées dans la mise en service d'un ordinateur virtuel.
7. Bonjour **étiquettes** , entrez **linux**. Cette étiquette est modèle hello tooidentify utilisé que vous créez et modèle de hello tooreference utilisé par la suite lors de la création d’un travail Hudson.
8. Sélectionnez une région où hello machine virtuelle doit être créé.
9. Sélectionnez la taille de machine virtuelle appropriée hello.
10. Spécifiez un compte de stockage où hello machine virtuelle doit être créé. Assurez-vous qu’il s’agit de hello même région que le service de cloud computing hello vous allez utiliser. Si vous souhaitez que le nouveau stockage toobe créé, vous pouvez laisser ce champ vide.
11. Durée de rétention spécifie le nombre hello de minutes avant la suppression d’une inactivité esclave Hudson. Laissez cette valeur par défaut 60 hello.
12. Dans **utilisation**, sélectionnez hello condition appropriée lorsque ce nœud subordonné sera utilisé. Pour l'instant, sélectionnez **Utilize this node as much as possible**(Utiliser ce nœud autant que possible).
    
     À ce stade, votre écran ressemble toothis quelque peu similaires :
    
     ![configuration du modèle][template config]
13. Dans **Id de famille de l’Image ou de** vous avez toospecify quelle image système sera installé sur votre machine virtuelle. Vous pouvez faire votre choix dans une liste de familles d'images ou spécifier une image personnalisée.
    
     Si vous souhaitez tooselect dans la liste des familles de l’image, entrez hello premier caractère (respecte la casse) du nom de famille d’image hello. Par exemple, le fait de taper **U** affichera une liste des familles de serveurs Ubuntu. Une fois que vous sélectionnez dans la liste de hello, Jenkins utilisera version la plus récente de cette image du système à partir de cette famille hello lors de la configuration de votre machine virtuelle.
    
     ![liste de famille de système d'exploitation][OS family list]
    
     Si vous disposez d’une image personnalisée que vous souhaitez toouse au lieu de cela, entrez le nom hello de cette image personnalisée. Noms d’images personnalisées ne figurent pas dans une liste afin que vous ayez tooensure qui hello nom a été saisi correctement.    
    
     Pour ce didacticiel, tapez **U** toobring la liste des images d’Ubuntu et sélectionnez **Ubuntu Server 14.04 LTS**.
14. Pour la **méthode de lancement**, sélectionnez **SSH**.
15. Copiez le script ci-dessous hello et collez Bonjour **script d’initialisation** champ.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Hello **script d’initialisation** sera exécuté après hello machine virtuelle est créée. Dans cet exemple, le script de hello installe Java, git et ant.
16. Bonjour **nom d’utilisateur** et **mot de passe** , saisissez les valeurs par défaut pour le compte d’administrateur hello qui sera créé sur votre machine virtuelle.
17. Cliquez sur **vérifier le modèle** toocheck si paramètres hello spécifiés sont valides.
18. Cliquez sur **Save**(Enregistrer).

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Créer un travail Hudson qui s'exécute sur un nœud subordonné sur Azure
Dans cette section, vous allez créer un travail Hudson qui s'exécutera sur un nœud subordonné sur Azure.

1. Dans le tableau de bord Hudson de hello, cliquez sur **nouveau travail**.
2. Entrez un nom pour la tâche hello que vous créez.
3. Pour le type de tâche hello, sélectionnez **créer un travail de style libre logiciel**.
4. Cliquez sur **OK**.
5. Dans la page de configuration du travail hello, sélectionnez **Restrict où ce projet peut être exécuté**.
6. Sélectionnez **nœud et étiquette de menu** et sélectionnez **linux** (que nous avons spécifié cette étiquette lors de la création du modèle d’ordinateur virtuel hello dans la section précédente de hello).
7. Bonjour **générer** , cliquez sur **étape de génération ajouter** et sélectionnez **exécuter shell**.
8. Modifier hello script suivant, en remplaçant **{nom de votre compte github}**, **{nom de votre projet}**, et **{votre répertoire de projet}** avec les valeurs appropriées et collez hello modifier le script dans la zone de texte hello qui s’affiche.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Cliquez sur **Save**(Enregistrer).
10. Hello du tableau de bord Hudson, recherchez les tâches hello vous venez de créer et cliquez sur hello **planifier une build** icône.

Hudson ensuite créer un nœud subordonné à l’aide du modèle de hello créé dans la section précédente de hello et exécuter le script hello spécifié à l’étape de génération hello pour cette tâche.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].

<!-- URL List -->

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[profil d’abonnement]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

