<span data-ttu-id="845bf-101">Azure déterminera la version hello de toouse Python pour son environnement virtuel avec hello suivant de priorité :</span><span class="sxs-lookup"><span data-stu-id="845bf-101">Azure will determine hello version of Python toouse for its virtual environment with hello following priority:</span></span>

1. <span data-ttu-id="845bf-102">version spécifiée dans runtime.txt dans le dossier racine de hello</span><span class="sxs-lookup"><span data-stu-id="845bf-102">version specified in runtime.txt in hello root folder</span></span>
2. <span data-ttu-id="845bf-103">version spécifiée par le paramètre de Python dans la configuration de l’application web hello (hello **paramètres** > **paramètres de l’Application** panneau pour votre application web hello portail Azure)</span><span class="sxs-lookup"><span data-stu-id="845bf-103">version specified by Python setting in hello web app configuration (hello **Settings** > **Application Settings** blade for your web app in hello Azure Portal)</span></span>
3. <span data-ttu-id="845bf-104">Python 2.7 est par défaut de hello si hello ci-dessus sont spécifiés</span><span class="sxs-lookup"><span data-stu-id="845bf-104">python-2.7 is hello default if none of hello above are specified</span></span>

<span data-ttu-id="845bf-105">Valeurs valides pour le contenu de hello de</span><span class="sxs-lookup"><span data-stu-id="845bf-105">Valid values for hello contents of</span></span> 

    \runtime.txt

<span data-ttu-id="845bf-106">sont :</span><span class="sxs-lookup"><span data-stu-id="845bf-106">are:</span></span>

* <span data-ttu-id="845bf-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="845bf-107">python-2.7</span></span>
* <span data-ttu-id="845bf-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="845bf-108">python-3.4</span></span>

<span data-ttu-id="845bf-109">Si les version micro hello (le troisième chiffre) est spécifié, il est ignoré.</span><span class="sxs-lookup"><span data-stu-id="845bf-109">If hello micro version (third digit) is specified, it is ignored.</span></span>

