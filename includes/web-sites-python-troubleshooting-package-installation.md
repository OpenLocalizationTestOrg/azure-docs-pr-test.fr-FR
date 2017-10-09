Il est possible que certains packages ne soient pas installés via pip sous Azure.  Il peut être simplement que ce package hello n’est pas disponible sur hello Python Package Index.  Il peut être qu’un compilateur est requis (un compilateur n’est pas disponible sur l’ordinateur en cours d’exécution hello web application hello dans Azure App Service).

Dans cette section, nous allons examiner les façons toodeal avec ce problème.

### <a name="request-wheels"></a>Demande de roues
Si l’installation du package hello requiert un compilateur, vous devez essayer de contacter hello package propriétaire toorequest que roues être disponibles pour le package de hello.

Avec la disponibilité récente hello [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], il est désormais plus faciles packages toobuild ayant le code natif pour Python 2.7.

### <a name="build-wheels-requires-windows"></a>Création de roues (Windows requis)
Remarque : Lorsque vous utilisez cette option, vérifiez que package de hello toocompile à l’aide d’un environnement de Python qui correspond aux hello/architecture/version de la plateforme qui est utilisée sur l’application web de hello dans Azure App Service (Windows/32-bit/2.7 ou 3.4).

Si le package de hello ne s’installe pas, car elle requiert un compilateur, vous pouvez installer le compilateur de hello sur votre ordinateur local et générer une roulette de package de hello, qui vous serez ensuite inclure dans votre référentiel.

Les utilisateurs Mac/Linux : Si vous n’avez pas machine virtuelle Windows tooa accès, consultez [créer une Machine virtuelle exécutant Windows] [ Create a Virtual Machine Running Windows] de façon toocreate une machine virtuelle sur Azure.  Vous pouvez utiliser roues de hello toobuild, ajoutez-les toohello référentiel et ignorer hello machine virtuelle si vous le souhaitez. 

Pour les Python 2.7, vous pouvez installer [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

Pour les Python 3.4, vous pouvez installer [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

Vous devez toobuild roues, package de roulette hello :

    env\scripts\pip install wheel

Vous allez utiliser `pip wheel` toocompile une dépendance :

    env\scripts\pip wheel azure==0.8.4

Cela crée un fichier de .whl dans le dossier de \wheelhouse hello.  Ajouter le dossier de \wheelhouse hello et un référentiel de tooyour de fichiers de roulette.

Modifier votre hello de tooadd requirements.txt `--find-links` option haut hello. Cela indique un pip toolook une correspondance exacte dans le dossier local de hello avant l’index de cours toohello python package.

    --find-links wheelhouse
    azure==0.8.4

Si vous souhaitez tooinclude toutes les dépendances de vos hello \wheelhouse dossier et n’utilise pas hello python package index du tout, vous pouvez forcer l’index du package pip tooignore hello en ajoutant `--no-index` haut toohello de votre requirements.txt.

    --no-index

### <a name="customize-installation"></a>Installation personnalisée
Vous pouvez personnaliser tooinstall de script de déploiement hello un package dans hello environnement virtuel en utilisant un autre programme d’installation, tel que facile\_installer.  Reportez-vous à deploy.cmd pour obtenir un exemple commenté.  Assurez-vous que ces packages ne sont pas répertoriés dans requirements.txt, pip tooprevent de les installer.

Ajoutez ce script de déploiement toohello :

    env\scripts\easy_install somepackage

Vous pouvez également être en mesure de toouse facile\_installer tooinstall à partir d’un programme d’installation de l’exe (certains sont zip compatible, facile\_installer les prend en charge).  Ajoutez le référentiel de tooyour hello programme d’installation et appeler facilement\_installer en passant toohello de chemin d’accès hello exécutable.

Ajoutez ce script de déploiement toohello :

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Inclure un environnement virtuel de hello dans le référentiel hello (nécessite Windows)
Remarque : Lorsque vous utilisez cette option, assurez-vous que toouse un environnement virtuel qui correspond aux hello/architecture/version de la plateforme qui est utilisée sur l’application web de hello dans Azure App Service (Windows/32-bit/2.7 ou 3.4).

Si vous incluez un environnement virtuel de hello dans le référentiel de hello, vous pouvez empêcher le script de déploiement hello d’effectuer la gestion de l’environnement virtuel sur Azure en créant un fichier vide :

    .skipPythonDeployment

Nous vous recommandons de supprimer environnement virtuel existant de hello sur application hello, tooprevent les fichiers restants à partir de lors de l’environnement virtuel de hello était gérée automatiquement.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
