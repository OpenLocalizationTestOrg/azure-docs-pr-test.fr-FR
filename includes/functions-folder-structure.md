
code Hello pour toutes les fonctions hello dans une application de la fonction donnée réside dans un dossier racine qui contient un fichier de configuration d’hôte et un ou plusieurs sous-dossiers, chacun d’eux contenir du code hello pour une fonction distincte, comme dans hello l’exemple suivant :

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Hello *host.json* fichier contient une configuration spécifique à l’exécution et qu’il se situe dans le dossier racine de hello d’application de fonction hello. Pour plus d’informations sur les paramètres qui sont disponibles, consultez [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) dans hello WebJobs.Script référentiel wiki.

Chaque fonction a un dossier qui contient un ou plusieurs fichiers de code, configuration de function.json hello et autres dépendances.

