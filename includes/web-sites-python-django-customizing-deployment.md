Azure détermine que votre application utilise Python **si les deux conditions suivantes sont remplies**:

* fichier Requirements.txt dans le dossier racine de hello
* n’importe quel fichier .py dans le dossier racine de hello ou un runtime.txt qui spécifie les python

Lorsque c’est le cas de hello, il utilise un script de déploiement spécifique Python qui effectue une synchronisation standard de hello de fichiers, ainsi que les opérations de Python supplémentaires telles que :

* Gestion automatique de l’environnement virtuel
* Installation des packages répertoriés dans requirements.txt à l’aide de pip
* La création du fichier web.config approprié hello selon hello sélectionnés version Python.
* Collecte des fichiers statiques pour les applications Django

Vous pouvez contrôler certains aspects des étapes de déploiement par défaut hello sans avoir de script de hello toocustomize.

Si vous souhaitez tooskip toutes les étapes de déploiement spécifique de Python, vous pouvez créer ce fichier vide :

    \.skipPythonDeployment

Si vous souhaitez collection tooskip des fichiers statiques pour votre application Django :

    \.skipDjango 

Pour mieux contrôler le déploiement, vous pouvez remplacer le script de déploiement par défaut hello en créant hello fichiers suivants :

    \.deployment
    \deploy.cmd

Vous pouvez utiliser hello [interface de ligne de commande Azure] [ Azure command-line interface] toocreate les fichiers hello.  Utilisez cette commande à partir de votre dossier de projet :

    azure site deploymentscript --python

Lorsque ces fichiers n’existent pas, Azure crée un script de déploiement temporaire et l’exécute.  Il est identique toohello vous l’avez créée avec la commande hello ci-dessus.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
