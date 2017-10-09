---
title: "aaaHow toouse Hudson avec stockage d’objets Blob | Documents Microsoft"
description: "Décrit comment toouse Hudson avec le stockage d’objets Blob Azure en tant que référentiel pour les artefacts de build."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 196b5d014b0318c5972a052f7822b568cfcc23df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>Utilisation d’Azure Storage avec une solution d’intégration continue Hudson
## <a name="overview"></a>Vue d'ensemble
Hello ci-après montre comment toouse stockage d’objets Blob en tant que référentiel d’artefacts de build créée par une solution d’intégration continue Hudson (CI), ou en tant que source des fichiers téléchargeables toobe utilisée dans un processus de génération. Un des scénarios hello où cela serait utile est lorsque vous codez dans un environnement de développement agile (à l’aide de Java ou autres langages), builds sont en cours d’exécution en fonction de l’intégration continue, et vous avez besoin d’un référentiel pour les artefacts de votre build, afin que vous pouvez , par exemple, les partager avec d’autres membres de l’organisation, vos clients, ou conserver une archive.  Un autre scénario est lorsque votre tâche de la build requiert des autres fichiers, par exemple, toodownload de dépendances dans le cadre de hello build entrée.

Dans ce didacticiel vous utiliserez le plug-in de hello le stockage Azure pour l’élément de configuration Hudson mises à disposition par Microsoft.

## <a name="introduction-toohudson"></a>Introduction tooHudson
Hudson permet l’intégration continue d’un projet de logiciel en permettant aux développeurs tooeasily intégrer leurs modifications du code et avoir génère générées automatiquement et fréquemment, accroître la productivité des développeurs de hello hello des. Les versions sont gérées et les artefacts de build peuvent être téléchargé toovarious référentiels. Cet article explique comment toouse stockage d’objets Blob Azure en tant que référentiel hello Hello des artefacts de build. Elle montre également comment les dépendances toodownload à partir du stockage d’objets Blob Azure.

Pour plus d'informations sur Hudson, consultez la page de [présentation d'Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson).

## <a name="benefits-of-using-hello-blob-service"></a>Avantages de l’utilisation du service d’objets Blob hello
Avantages de l’utilisation de hello Blob service toohost vos artefacts de build de développement agile :

* Haute disponibilité de vos artefacts de build et/ou dépendances téléchargeables.
* Performances lorsque votre solution Hudson CI télécharge vos artefacts de build.
* Performances lorsque vos clients et partenaires téléchargent vos artefacts de build.
* Contrôle sur les stratégies d'accès utilisateur, avec choix entre accès anonyme, accès par signature d'accès partagé basé sur l'expiration, accès privé, etc.

## <a name="prerequisites"></a>Composants requis
Vous serez peut-être hello suivant toouse hello service Blob avec votre solution Hudson CI :

* Une solution d'intégration continue Hudson.
  
    Si vous n’avez actuellement pas une solution de l’élément de configuration Hudson, vous pouvez exécuter une solution de l’élément de configuration Hudson à l’aide de hello suivant technique :
  
  1. Sur un ordinateur compatible Java, téléchargement hello WAR Hudson de <http://hudson-ci.org/>.
  2. À une invite de commandes est le dossier ouvert toohello contenant hello Hudson WAR, exécutez hello Hudson WAR. Par exemple, si vous avez téléchargé la version 3.1.2 :
     
      `java -jar hudson-3.1.2.war`

  3. Dans votre navigateur, ouvrez `http://localhost:8080/`. Hello du tableau de bord Hudson s’ouvre.
  4. Lors de la première utilisation de Hudson, terminer l’installation initiale de hello à `http://localhost:8080/`.
  5. Après avoir terminé la configuration initiale hello, Annuler hello qui exécute l’instance de hello Hudson WAR, démarrer hello Hudson WAR à nouveau et ouvrez à nouveau hello du tableau de bord Hudson, `http://localhost:8080/`, qui vous utiliserez tooinstall et configurer le plug-in de hello le stockage Azure.
     
      Lors d’une solution de l’élément de configuration Hudson classique est configurée toorun en tant que service, hello war de Hudson en cours d’exécution à la ligne de commande hello sera suffisant pour ce didacticiel.
* Un compte Azure. Pour créer un compte Azure, consultez la page <http://www.azure.com>.
* Un compte de stockage Azure. Si vous n’avez pas déjà un compte de stockage, vous pouvez en créer un à l’aide des étapes hello [créer un compte de stockage](../common/storage-create-storage-account.md#create-a-storage-account).
* Vous êtes familiarisé avec la solution de l’élément de configuration Hudson hello est recommandé mais pas obligatoire, comme hello contenu suivant utilisera un tooshow de l’exemple de base vous hello étapes nécessaires lors de l’utilisation du service d’objets Blob hello en tant que référentiel pour l’élément de configuration Hudson des artefacts de build.

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>Comment toouse hello service Blob avec l’élément de configuration Hudson
le service de Blob toouse hello avec Hudson, vous devez tooinstall hello plug-in de stockage Azure, configurer hello plug-in toouse votre compte de stockage et ensuite créer une action post-build qui télécharge de votre compte de stockage tooyour build artefacts. Ces étapes sont décrites dans les sections suivantes de hello.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Comment tooinstall hello plug-in de stockage Azure
1. Au sein de hello du tableau de bord Hudson, cliquez sur **gérer les Hudson**.
2. Sur hello **gérer les Hudson** , cliquez sur **gérer les plug-ins**.
3. Cliquez sur hello **disponible** onglet.
4. Cliquez sur **Others**.
5. Bonjour **artefact télépartageurs** section, sélectionnez **plug-in Microsoft Azure Storage**.
6. Cliquez sur **Installer**.
7. Une fois l’installation de hello est terminée, redémarrez Hudson.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Comment tooconfigure hello toouse plug-in de stockage Azure, votre compte de stockage
1. Au sein de hello du tableau de bord Hudson, cliquez sur **gérer les Hudson**.
2. Sur hello **gérer les Hudson** , cliquez sur **configurer le système**.
3. Bonjour **Configuration du compte de stockage Microsoft Azure** section :
   
    a. Entrez votre nom de compte de stockage, vous pouvez obtenir à partir de hello [Azure Portal](https://portal.azure.com).
   
    b. Entrez votre clé de compte de stockage, également peut être obtenu à partir de hello [Azure Portal](https://portal.azure.com).
   
    c. Utilisez la valeur par défaut de hello **URL de point de terminaison du Service Blob** si vous utilisez le cloud public Azure de hello. Si vous utilisez un autre cloud Azure, utiliser le point de terminaison hello comme hello spécifié dans [portail Azure](https://portal.azure.com) pour votre compte de stockage.
   
    d. Cliquez sur **valider les informations d’identification de stockage** toovalidate votre compte de stockage.
   
    e. [Facultatif] Si vous avez des comptes de stockage supplémentaires que vous souhaitez tooyour disponible faite Hudson l’élément de configuration, cliquez sur **ajouter plusieurs comptes de stockage**.
   
    f. Cliquez sur **enregistrer** toosave vos paramètres.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Comment toocreate une action post-build qui télécharge de votre compte de stockage build artefacts tooyour
Tout d’abord à des fins d’instruction, nous aurons besoin toocreate une tâche qui crée plusieurs fichiers et puis ajoutez hello action post-build tooupload hello fichiers tooyour compte de stockage.

1. Au sein de hello du tableau de bord Hudson, cliquez sur **nouveau travail**.
2. Nom du travail hello **MyJob**, cliquez sur **créer un travail de style libre logiciel**, puis cliquez sur **OK**.
3. Bonjour **générer** section de configuration du travail hello, cliquez sur **étape de génération ajouter** et choisissez **commande de lot Windows d’exécuter**.
4. Dans **commande**, utilisez hello suivant de commandes :

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. Bonjour **post-build Actions** section de configuration du travail hello, cliquez sur **télécharger le stockage d’objets Blob Azure artefacts tooMicrosoft**.
6. Pour **nom de compte de stockage**, sélectionnez hello toouse de compte de stockage.
7. Pour **nom du conteneur**, spécifiez le nom du conteneur hello. (conteneur de hello sera créée si elle n’existe pas lors du téléchargement des artefacts de build hello.) Vous pouvez utiliser des variables d’environnement, par conséquent, pour cet exemple, entrez **${JOB_NAME}** comme nom du conteneur hello.
   
    **Conseil**
   
    Ci-dessous hello **commande** section où vous avez entré un script pour **Windows d’exécution de commande batch** est un lien de variables d’environnement toohello reconnus par Hudson. Cliquez sur qui lient les noms de variables d’environnement toolearn hello et descriptions. Notez cet environnement variables qui contiennent des caractères spéciaux, tels que hello **BUILD_URL** variable d’environnement ne sont pas autorisés en tant que nom du conteneur ou chemin d’accès virtuel commun.
8. Cliquez sur **Rendre le nouveau conteneur public par défaut** pour cet exemple. (Si vous voulez toouse un conteneur privé, vous devez toocreate un accès partagé signature tooallow l’accès. Qui est abordée dans cet article hello. Pour en savoir plus sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [Facultatif] Cliquez sur **propre conteneur avant de le télécharger** si vous souhaitez hello conteneur toobe effacé du contenu avant que les artefacts de build sont téléchargées (laissez-la désactivée si vous ne souhaitez pas le contenu de hello tooclean du conteneur de hello).
10. Pour **tooupload de la liste des artefacts**, entrez  **texte /*.txt**.
11. Dans **Common virtual path for uploaded artifacts** (Chemin virtuel commun des artefacts téléchargés), entrez **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Cliquez sur **enregistrer** toosave vos paramètres.
13. Dans le tableau de bord Hudson de hello, cliquez sur **générer maintenant** toorun **MyJob**. Examinez la sortie de console hello pour l’état. Messages d’état pour le stockage Azure sont être inclus dans la sortie de console hello lors de l’action de post-build hello démarre les artefacts de build tooupload.
14. En cas de réussite du travail de hello, vous pouvez examiner les artefacts de build hello en ouvrant l’objet blob public de hello.
    
    a. Connectez-vous à toohello [Azure Portal](https://portal.azure.com).
    
    b. Cliquez sur **Stockage**.
    
    c. Cliquez sur le nom de compte de stockage hello que celle utilisée pour Hudson.
    
    d. Cliquez sur **Conteneurs**.
    
    e. Cliquez sur le conteneur hello nommé **myjob**, qui est la version en minuscule de hello du nom de la tâche hello que vous avez attribué lors de la création de hello travail de Hudson. Les noms de conteneurs et les noms d'objets blob sont en minuscules (et sensibles à la casse) dans le stockage Azure. Dans la liste d’objets BLOB pour le conteneur hello nommé hello **myjob** vous devez voir **hello.txt** et **date.txt**. Copier l’URL de hello pour chacun de ces éléments et ouvrez-le dans votre navigateur. Vous verrez un fichier texte hello qui a été chargé comme un artefact de build.

Une seule action post-build qui télécharge les artefacts tooAzure stockage d’objets Blob peut être créée par travail. Notez que le stockage d’objets Blob hello action post-build unique tooupload artefacts tooAzure pouvez spécifier différents fichiers (y compris les caractères génériques) et toofiles de chemins d’accès dans **tooupload de la liste des artefacts** à l’aide d’un point-virgule comme séparateur. Par exemple, si votre Hudson build génère des fichiers TXT dans votre espace de travail et les fichiers JAR **générer** dossier et que vous souhaitez tooupload les deux tooAzure stockage d’objets Blob, utilisez suivants de hello pour hello **tooupload de liste d’artefacts** valeur : **générer /\*.jar ; génération /\*.txt**. Vous pouvez également utiliser la syntaxe de double deux-points toospecify un toouse de chemin d’accès dans le nom d’objet blob hello. Par exemple, si vous souhaitez hello JAR tooget est téléchargé à l’aide de **binaires** dans le chemin d’accès des blob hello et tooget de fichiers TXT hello téléchargé à l’aide de **avis** dans le chemin d’accès des blob hello, utilisez suivants de hello pour hello  **Liste des tooupload des artefacts** valeur : **générer /\*. jar::binaries ; génération /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Comment toocreate une étape de génération qui télécharge à partir du stockage d’objets Blob Azure
Hello suit montrent comment tooconfigure une build étape des éléments de toodownload à partir du stockage d’objets Blob Azure. Il serait utile si vous souhaitez que les éléments tooinclude dans votre build, par exemple, les fichiers JAR que vous conservez dans le stockage d’objets Blob Azure.

1. Bonjour **générer** section de configuration du travail hello, cliquez sur **étape de génération ajouter** et choisissez **télécharger à partir du stockage d’objets Blob Azure**.
2. Pour **nom de compte de stockage**, sélectionnez hello toouse de compte de stockage.
3. Pour **nom du conteneur**, spécifiez hello nom de hello conteneur qui comporte des objets BLOB de hello souhaité toodownload. Vous pouvez utiliser des variables d'environnement.
4. Pour **nom d’objet Blob**, spécifiez le nom d’objet blob hello. Vous pouvez utiliser des variables d'environnement. En outre, vous pouvez utiliser un astérisque, comme un caractère générique après avoir spécifié les hello initiale ou les lettres du nom d’objet blob hello. Par exemple, **projet\*** désignera tous les objets blob dont le nom commence par **projet**.
5. [Facultatif] Pour **chemin de téléchargement**, spécifier de chemin d’accès hello sur hello machine Hudson où vous souhaitez toodownload les fichiers à partir du stockage d’objets Blob Azure. Vous pouvez utiliser des variables d’environnement. (Si vous ne fournissez pas de valeur pour **chemin de téléchargement**, fichiers hello à partir du stockage d’objets Blob Azure sera espace de travail de la tâche toohello téléchargé.)

Si vous avez d’autres éléments toodownload à partir du stockage d’objets Blob Azure, vous pouvez créer des étapes de génération supplémentaires.

Une fois que vous exécutez une build, vous pouvez vérifier hello générer la sortie de console de l’historique, ou examiner l’emplacement de téléchargement, toosee hello si BLOB prévu ont été téléchargés correctement.

## <a name="components-used-by-hello-blob-service"></a>Composants utilisés par hello service Blob
suivant de Hello fournit une vue d’ensemble des composants de service Blob hello.

* **Compte de stockage**: tous les accès tooAzure stockage s’effectue via un compte de stockage. Il s’agit de niveau le plus élevé hello d’espace de noms hello pour accéder aux objets BLOB. Un compte peut contenir un nombre illimité de conteneurs, tant que sa taille totale ne dépasse pas 100 To.
* **Conteneur**: conteneur regroupant un ensemble d’objets blob. Tous les objets blob doivent figurer dans un conteneur. Un compte peut contenir un nombre illimité de conteneurs. Un conteneur peut stocker un nombre illimité d’objets blob.
* **Objet blob**: fichier de tout type et de toute taille. Il existe deux types d’objets blob qui peuvent être enregistrés dans un stockage Azure : les objets blob de blocs et les objets blob de pages. La plupart des fichiers sont des objets blob de blocs. Objet blob de blocs unique peut être de taille too200 go. Ce didacticiel utilise des objets blob de blocs. Objets BLOB de pages, un autre type d’objet blob, peut être jusqu'à to too1 par la taille et sont plus efficace lorsque les plages d’octets dans un fichier sont modifiées fréquemment. Pour plus d’informations sur les objets blob, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Format d’URL**: les objets BLOB sont adressables en utilisant hello suivant le format d’URL :
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (format hello ci-dessus s’applique toohello des cloud public Azure. Si vous utilisez un autre cloud Azure, utilisez le point de terminaison de hello dans hello [Azure Portal](https://portal.azure.com) toodetermine votre point de terminaison d’URL.)
  
    Dans le format hello ci-dessus, `storageaccount` représente hello nom de votre compte de stockage `container_name` représente hello nom de votre conteneur, et `blob_name` représente hello le nom de votre objet blob, respectivement. Dans nom du conteneur hello, vous pouvez avoir plusieurs chemins d’accès, séparés par une barre oblique,  **/** . nom du conteneur exemple Hello dans ce didacticiel a été **MyJob**, et **${générer\_ID} / ${générer\_nombre}** a été utilisé pour le chemin virtuel commun hello, résultant hello ayant pour objet blob un URL de hello suivant du formulaire :
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>Étapes suivantes
* [Présentation d’Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [Kit de développement logiciel (SDK) Azure Storage pour Java](https://github.com/azure/azure-storage-java)
* [Référence du Kit de développement logiciel (SDK) du client Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).