---
title: "aaaUsing le stockage Azure avec une Solution d’intégration continue Jenkins | Documents Microsoft"
description: "Ce didacticiel montrent comment toouse hello Azure le service blob comme un référentiel pour générer des artefacts créés par une solution d’intégration continue Jenkins."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 853c0c6c028596b3057bdc1dbbc59a9415c0fb77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Utilisation d’Azure Storage avec une solution d’intégration continue Jenkins
## <a name="overview"></a>Vue d'ensemble
Hello ci-après montre comment toouse stockage d’objets Blob en tant que référentiel d’artefacts de build créée par une solution d’intégration continue Jenkins (CI), ou en tant que source des fichiers téléchargeables toobe utilisée dans un processus de génération. Un des scénarios hello où cela serait utile est lorsque vous codez dans un environnement de développement agile (à l’aide de Java ou autres langages), builds sont en cours d’exécution en fonction de l’intégration continue, et vous avez besoin d’un référentiel pour les artefacts de votre build, afin que vous pouvez , par exemple, les partager avec d’autres membres de l’organisation, vos clients, ou conserver une archive. Un autre scénario est lorsque votre tâche de la build requiert des autres fichiers, par exemple, toodownload de dépendances dans le cadre de hello build entrée.

Dans ce didacticiel vous utiliserez hello plug-in de stockage Azure pour Jenkins CI mises à disposition par Microsoft.

## <a name="overview-of-jenkins"></a>Présentation de Jenkins
Jenkins permet l’intégration continue d’un projet de logiciel en permettant aux développeurs tooeasily intégrer leurs modifications du code et avoir génère générées automatiquement et fréquemment, accroître la productivité des développeurs de hello hello des. Les versions sont gérées et les artefacts de build peuvent être téléchargé toovarious référentiels. Cette rubrique indique comment toouse Azure stockage d’objets blob en tant que référentiel hello des artefacts de build hello. Elle montre également comment les dépendances toodownload à partir d’Azure stockage d’objets blob.

Pour plus d'informations sur Jenkins, consultez la page de [présentation de Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Avantages de l’utilisation du service d’objets Blob hello
Avantages de l’utilisation de hello Blob service toohost vos artefacts de build de développement agile :

* Haute disponibilité de vos artefacts de build et/ou dépendances téléchargeables.
* Performances lorsque votre solution Jenkins CI télécharge vos artefacts de build.
* Performances lorsque vos clients et partenaires téléchargent vos artefacts de build.
* Contrôle sur les stratégies d'accès utilisateur, avec choix entre accès anonyme, accès par signature d'accès partagé basé sur l'expiration, accès privé, etc.

## <a name="prerequisites"></a>Composants requis
Vous serez peut-être hello suivant toouse hello service Blob avec votre solution Jenkins CI :

* Une solution d'intégration continue Jenkins.
  
    Si vous n’avez actuellement pas une solution Jenkins CI, vous pouvez exécuter une solution de Jenkins CI à l’aide de hello suivant technique :
  
  1. Sur un ordinateur compatible Java, téléchargez le fichier jenkins.war à l'adresse <http://jenkins-ci.org>.
  2. À une invite de commandes est le dossier toohello ouvert qui contient jenkins.war, exécutez :
     
      `java -jar jenkins.war`

  3. Dans votre navigateur, ouvrez `http://localhost:8080/`. S’ouvre hello Jenkins tableau de bord, vous allez utiliser tooinstall et configurer le plug-in de hello le stockage Azure.
     
      Lors d’une solution de Jenkins CI classique est configurée toorun en tant que service, la guerre de Jenkins hello en cours d’exécution à la ligne de commande hello sera suffisant pour ce didacticiel.
* Un compte Azure. Pour créer un compte Azure, consultez la page <http://www.azure.com>.
* Un compte de stockage Azure. Si vous n’avez pas déjà un compte de stockage, vous pouvez en créer un à l’aide des étapes hello [créer un compte de stockage](../common/storage-create-storage-account.md#create-a-storage-account).
* Vous êtes familiarisé avec la solution de Jenkins CI hello est recommandé mais pas obligatoire, comme hello contenu suivant utilisera un tooshow de l’exemple de base vous hello étapes nécessaires lors de l’utilisation du service d’objets Blob hello en tant que référentiel pour Jenkins CI des artefacts de build.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Comment toouse hello service Blob avec Jenkins CI
le service de Blob toouse hello avec Jenkins, vous devez tooinstall hello plug-in de stockage Azure, configurer hello plug-in toouse votre compte de stockage et ensuite créer une action post-build qui télécharge de votre compte de stockage tooyour build artefacts. Ces étapes sont décrites dans les sections suivantes de hello.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Comment tooinstall hello plug-in de stockage Azure
1. Dans le tableau de bord hello Jenkins, cliquez sur **gérer les Jenkins**.
2. Bonjour **gérer les Jenkins** , cliquez sur **gérer les plug-ins**.
3. Cliquez sur hello **disponible** onglet.
4. Bonjour **artefact télépartageurs** section, cocher **plug-in Microsoft Azure Storage**.
5. Cliquez sur **Install without restart** ou sur **Download now and install after restart**.
6. Redémarrez Jenkins.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Comment tooconfigure hello toouse plug-in de stockage Azure, votre compte de stockage
1. Dans le tableau de bord hello Jenkins, cliquez sur **gérer les Jenkins**.
2. Bonjour **gérer les Jenkins** , cliquez sur **configurer le système**.
3. Bonjour **Configuration du compte de stockage Microsoft Azure** section :
   1. Entrez votre nom de compte de stockage, vous pouvez obtenir à partir de hello [Azure Portal](https://portal.azure.com).
   2. Entrez votre clé de compte de stockage, également peut être obtenu à partir de hello [Azure Portal](https://portal.azure.com).
   3. Utilisez la valeur par défaut de hello **URL de point de terminaison du Service Blob** si vous utilisez le cloud public Azure de hello. Si vous utilisez un autre cloud Azure, utiliser le point de terminaison hello comme hello spécifié dans [portail Azure](https://portal.azure.com) pour votre compte de stockage. 
   4. Cliquez sur **valider les informations d’identification de stockage** toovalidate votre compte de stockage. 
   5. [Facultatif] Si vous avez des comptes de stockage supplémentaires que vous souhaitez tooyour disponible faite Jenkins CI, cliquez sur **ajouter plusieurs comptes de stockage**.
   6. Cliquez sur **enregistrer** toosave vos paramètres.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Comment toocreate une action post-build qui télécharge de votre compte de stockage build artefacts tooyour
Tout d’abord à des fins d’instruction, nous aurons besoin toocreate une tâche qui crée plusieurs fichiers et puis ajoutez hello action post-build tooupload hello fichiers tooyour compte de stockage.

1. Dans le tableau de bord hello Jenkins, cliquez sur **un nouvel élément**.
2. Nom du travail hello **MyJob**, cliquez sur **générer un projet de logiciel de forme libre**, puis cliquez sur **OK**.
3. Bonjour **générer** section de configuration du travail hello, cliquez sur **étape de génération ajouter** et choisissez **commande de lot Windows d’exécuter**.
4. Dans **commande**, utilisez hello suivant de commandes :

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. Bonjour **post-build Actions** section de configuration du travail hello, cliquez sur **ajouter une action post-build** et choisissez **télécharger le stockage d’objets Blob artefacts tooAzure**.
6. Pour **nom de compte de stockage**, sélectionnez hello toouse de compte de stockage.
7. Pour **nom du conteneur**, spécifiez le nom du conteneur hello. (conteneur de hello sera créée si elle n’existe pas lors du téléchargement des artefacts de build hello.) Vous pouvez utiliser des variables d’environnement, par conséquent, pour cet exemple, entrez **${JOB_NAME}** comme nom du conteneur hello.
   
    **Conseil**
   
    Ci-dessous hello **commande** section où vous avez entré un script pour **Windows d’exécution de commande batch** est un lien de variables d’environnement toohello reconnus par Jenkins. Cliquez sur qui lient les noms de variables d’environnement toolearn hello et descriptions. Notez cet environnement variables qui contiennent des caractères spéciaux, tels que hello **BUILD_URL** variable d’environnement ne sont pas autorisés en tant que nom du conteneur ou chemin d’accès virtuel commun.
8. Cliquez sur **Rendre le nouveau conteneur public par défaut** pour cet exemple. (Si vous voulez toouse un conteneur privé, vous devez toocreate un accès partagé signature tooallow l’accès. Qui n’est pas abordée hello de cette rubrique. Pour en savoir plus sur les signatures d’accès partagé, consultez [Utilisation des signatures d’accès partagé (SAP)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [Facultatif] Cliquez sur **propre conteneur avant de le télécharger** si vous souhaitez hello conteneur toobe effacé du contenu avant que les artefacts de build sont téléchargées (laissez-la désactivée si vous ne souhaitez pas le contenu de hello tooclean du conteneur de hello).
10. Pour **tooupload de la liste des artefacts**, entrez  **texte /*.txt**.
11. Pour **Chemin virtuel commun pour les artefacts téléchargés**, dans le cadre de ce didacticiel, entrez **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Cliquez sur **enregistrer** toosave vos paramètres.
13. Dans le tableau de bord hello Jenkins, cliquez sur **générer maintenant** toorun **MyJob**. Examinez la sortie de console hello pour l’état. Messages d’état pour le stockage Azure figureront dans la sortie de console hello lors de l’action de post-build hello démarre les artefacts de build tooupload.
14. En cas de réussite du travail de hello, vous pouvez examiner les artefacts de build hello en ouvrant l’objet blob public de hello.
    1. Connexion toohello [Azure Portal](https://portal.azure.com).
    2. Cliquez sur **Stockage**.
    3. Cliquez sur le nom de compte de stockage hello que celle utilisée pour Jenkins.
    4. Cliquez sur **Conteneurs**.
    5. Cliquez sur le conteneur hello nommé **myjob**, qui est la version en minuscule de hello du nom de la tâche hello que vous avez attribué lors de la création du travail de Jenkins hello. Les noms de conteneurs et les noms d’objets blob sont en minuscules (et sensibles à la casse) dans le stockage Azure. Dans la liste d’objets BLOB pour le conteneur hello nommé hello **myjob** vous devez voir **hello.txt** et **date.txt**. Copier l’URL de hello pour chacun de ces éléments et ouvrez-le dans votre navigateur. Vous verrez un fichier texte hello qui a été chargé comme un artefact de build.

Une seule action post-build qui charge le stockage d’objets blob tooAzure artefacts peut être créée par travail. Notez que le stockage d’objets blob hello action post-build unique tooupload artefacts tooAzure pouvez spécifier différents fichiers (y compris les caractères génériques) et toofiles de chemins d’accès dans **tooupload de la liste des artefacts** à l’aide d’un point-virgule comme séparateur. Par exemple, si votre Jenkins build génère des fichiers TXT dans votre espace de travail et les fichiers JAR **générer** dossier et que vous souhaitez tooupload les deux tooAzure de stockage d’objets blob, utilisez suivants de hello pour hello **tooupload de liste d’artefacts** valeur : **générer /\*.jar ; génération /\*.txt**. Vous pouvez également utiliser la syntaxe de double deux-points toospecify un toouse de chemin d’accès dans le nom d’objet blob hello. Par exemple, si vous souhaitez hello JAR tooget est téléchargé à l’aide de **binaires** dans le chemin d’accès des blob hello et tooget de fichiers TXT hello téléchargé à l’aide de **avis** dans le chemin d’accès des blob hello, utilisez suivants de hello pour hello  **Liste des tooupload des artefacts** valeur : **générer /\*. jar::binaries ; génération /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Comment toocreate une étape de génération qui télécharge à partir du stockage d’objets blob Azure
Hello suit montrent comment tooconfigure une build étape des éléments toodownload depuis le stockage blob Azure. Cela peut être utile si vous souhaitez que les éléments tooinclude dans votre build, par exemple, les fichiers JAR que vous conservez dans Azure stockage d’objets blob.

1. Bonjour **générer** section de configuration du travail hello, cliquez sur **étape de génération ajouter** et choisissez **télécharger à partir du stockage d’objets Blob Azure**.
2. Pour **nom de compte de stockage**, sélectionnez hello toouse de compte de stockage.
3. Pour **nom du conteneur**, spécifiez hello nom de hello conteneur qui comporte des objets BLOB de hello souhaité toodownload. Vous pouvez utiliser des variables d'environnement.
4. Pour **nom d’objet Blob**, spécifiez le nom d’objet blob hello. Vous pouvez utiliser des variables d'environnement. En outre, vous pouvez utiliser un astérisque, comme un caractère générique après avoir spécifié les hello initiale ou les lettres du nom d’objet blob hello. Par exemple, **projet\*** désignera tous les objets blob dont le nom commence par **projet**.
5. [Facultatif] Pour **chemin de téléchargement**, spécifier le chemin d’accès hello sur l’ordinateur de Jenkins hello où vous souhaitez toodownload les fichiers depuis le stockage blob Azure. Vous pouvez utiliser des variables d’environnement. (Si vous ne fournissez pas de valeur pour **chemin de téléchargement**, fichiers hello depuis le stockage blob Azure sera espace de travail de la tâche toohello téléchargé.)

Si vous avez d’autres éléments toodownload depuis le stockage blob Azure, vous pouvez créer des étapes de génération supplémentaires.

Une fois que vous exécutez une build, vous pouvez vérifier hello générer la sortie de console de l’historique, ou examiner l’emplacement de téléchargement, toosee hello si BLOB prévu ont été téléchargés correctement.  

## <a name="components-used-by-hello-blob-service"></a>Composants utilisés par hello service Blob
suivant de Hello fournit une vue d’ensemble des composants de service Blob hello.

* **Compte de stockage**: tous les accès tooAzure stockage s’effectue via un compte de stockage. Il s’agit de niveau le plus élevé hello d’espace de noms hello pour accéder aux objets BLOB. Un compte peut contenir un nombre illimité de conteneurs, tant que sa taille totale ne dépasse pas 100 To.
* **Conteneur**: conteneur regroupant un ensemble d’objets blob. Tous les objets blob doivent figurer dans un conteneur. Un compte peut contenir un nombre illimité de conteneurs. Un conteneur peut stocker un nombre illimité d’objets blob.
* **Objet blob**: fichier de tout type et de toute taille. Il existe deux types d’objets blob qui peuvent être enregistrés dans un stockage Azure : les objets blob de blocs et les objets blob de pages. La plupart des fichiers sont des objets blob de blocs. Objet blob de blocs unique peut être des too200GB taille. Ce didacticiel utilise des objets blob de blocs. Objets BLOB de pages, un autre type d’objet blob, peut être des too1TB par la taille et sont plus efficace lorsque les plages d’octets dans un fichier sont modifiées fréquemment. Pour plus d’informations sur les objets blob, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Format d’URL**: les objets BLOB sont adressables en utilisant hello suivant le format d’URL :
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (format hello ci-dessus s’applique toohello des cloud public Azure. Si vous utilisez un autre cloud Azure, utilisez le point de terminaison de hello dans hello [Azure Portal](https://portal.azure.com) toodetermine votre point de terminaison d’URL.)
  
    Dans le format hello ci-dessus, `storageaccount` représente hello nom de votre compte de stockage `container_name` représente hello nom de votre conteneur, et `blob_name` représente hello le nom de votre objet blob, respectivement. Dans nom du conteneur hello, vous pouvez avoir plusieurs chemins d’accès, séparés par une barre oblique,  **/** . nom du conteneur exemple Hello dans ce didacticiel a été **MyJob**, et **${générer\_ID} / ${générer\_nombre}** a été utilisé pour le chemin virtuel commun hello, résultant hello ayant pour objet blob un URL de hello suivant du formulaire :
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Étapes suivantes
* [Présentation de Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Kit de développement logiciel (SDK) Azure Storage pour Java](https://github.com/azure/azure-storage-java)
* [Référence du Kit de développement logiciel (SDK) du client Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API REST des services d’Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog de l’équipe Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

Pour plus d’informations, consultez [Azure pour les développeurs Java](/java/azure).