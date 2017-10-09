
<span data-ttu-id="04d99-101">code Hello pour toutes les fonctions hello dans une application de la fonction donnée réside dans un dossier racine qui contient un fichier de configuration d’hôte et un ou plusieurs sous-dossiers, chacun d’eux contenir du code hello pour une fonction distincte, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="04d99-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="04d99-102">Hello *host.json* fichier contient une configuration spécifique à l’exécution et qu’il se situe dans le dossier racine de hello d’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="04d99-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="04d99-103">Pour plus d’informations sur les paramètres qui sont disponibles, consultez [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) dans hello WebJobs.Script référentiel wiki.</span><span class="sxs-lookup"><span data-stu-id="04d99-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="04d99-104">Chaque fonction a un dossier qui contient un ou plusieurs fichiers de code, configuration de function.json hello et autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="04d99-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

