Chaque objet blob du stockage Azure doit résider dans un conteneur. Hello conteneur fait partie du nom d’objet blob hello. Par exemple, `mycontainer` est le nom hello du conteneur de hello dans ces blob exemple URI :

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Un nom de conteneur doit être un nom DNS valide, conforme toohello suivant les règles d’affectation de noms :

1. Les noms de conteneur doivent commencer par une lettre ou un chiffre et peuvent contenir uniquement des lettres, des chiffres et hello tiret (-).
2. Chaque tiret (-) doit être immédiatement précédé et suivi d’une lettre ou d’un chiffre ; les tirets consécutifs sont interdits.
3. Toutes les lettres du conteneur doivent être minuscules.
4. Les noms de conteneurs doivent comporter entre 3 et 63 caractères.

> [!IMPORTANT]
> Notez que hello nom d’un conteneur doit toujours être en minuscule. Si vous incluez une lettre majuscule dans un nom de conteneur ou violer les règles d’affectation de noms de conteneur hello, vous pouvez recevoir une erreur 400 (demande incorrecte). 
> 
> 

