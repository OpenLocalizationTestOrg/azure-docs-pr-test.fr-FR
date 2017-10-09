<span data-ttu-id="00c15-101">Chaque objet blob du stockage Azure doit résider dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="00c15-101">Every blob in Azure storage must reside in a container.</span></span> <span data-ttu-id="00c15-102">Hello conteneur fait partie du nom d’objet blob hello.</span><span class="sxs-lookup"><span data-stu-id="00c15-102">hello container forms part of hello blob name.</span></span> <span data-ttu-id="00c15-103">Par exemple, `mycontainer` est le nom hello du conteneur de hello dans ces blob exemple URI :</span><span class="sxs-lookup"><span data-stu-id="00c15-103">For example, `mycontainer` is hello name of hello container in these sample blob URIs:</span></span>

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

<span data-ttu-id="00c15-104">Un nom de conteneur doit être un nom DNS valide, conforme toohello suivant les règles d’affectation de noms :</span><span class="sxs-lookup"><span data-stu-id="00c15-104">A container name must be a valid DNS name, conforming toohello following naming rules:</span></span>

1. <span data-ttu-id="00c15-105">Les noms de conteneur doivent commencer par une lettre ou un chiffre et peuvent contenir uniquement des lettres, des chiffres et hello tiret (-).</span><span class="sxs-lookup"><span data-stu-id="00c15-105">Container names must start with a letter or number, and can contain only letters, numbers, and hello dash (-) character.</span></span>
2. <span data-ttu-id="00c15-106">Chaque tiret (-) doit être immédiatement précédé et suivi d’une lettre ou d’un chiffre ; les tirets consécutifs sont interdits.</span><span class="sxs-lookup"><span data-stu-id="00c15-106">Every dash (-) character must be immediately preceded and followed by a letter or number; consecutive dashes are not permitted in container names.</span></span>
3. <span data-ttu-id="00c15-107">Toutes les lettres du conteneur doivent être minuscules.</span><span class="sxs-lookup"><span data-stu-id="00c15-107">All letters in a container name must be lowercase.</span></span>
4. <span data-ttu-id="00c15-108">Les noms de conteneurs doivent comporter entre 3 et 63 caractères.</span><span class="sxs-lookup"><span data-stu-id="00c15-108">Container names must be from 3 through 63 characters long.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00c15-109">Notez que hello nom d’un conteneur doit toujours être en minuscule.</span><span class="sxs-lookup"><span data-stu-id="00c15-109">Note that hello name of a container must always be lowercase.</span></span> <span data-ttu-id="00c15-110">Si vous incluez une lettre majuscule dans un nom de conteneur ou violer les règles d’affectation de noms de conteneur hello, vous pouvez recevoir une erreur 400 (demande incorrecte).</span><span class="sxs-lookup"><span data-stu-id="00c15-110">If you include an upper-case letter in a container name, or otherwise violate hello container naming rules, you may receive a 400 error (Bad Request).</span></span> 
> 
> 

