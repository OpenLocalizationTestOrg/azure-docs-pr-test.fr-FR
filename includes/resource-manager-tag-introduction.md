Vous appliquez des balises tooyour ressources Azure toologically les organiser par catégories. Chaque balise se compose d’un nom et d’une valeur. Par exemple, vous pouvez appliquer le nom hello « Environnement » et hello « Production » tooall hello ressources en production. En l’absence de cette balise, il pourrait être difficile de savoir si une ressource est destinée au développement, aux tests ou à la production. « Environnement » et « Production » sont juste des exemples. Vous définissez des noms de hello et les valeurs qui ont un sens hello la plupart pour organiser votre abonnement.

Après avoir appliqué les balises, vous pouvez récupérer toutes les ressources hello dans votre abonnement avec ce nom de balise et la valeur. Activer les balises vous tooretrieve liés les ressources qui résident dans différents groupes de ressources. Cette approche est utile lorsque vous avez besoin des ressources de tooorganize pour la gestion ou de facturation.

Hello limites suivantes s’appliquent à tootags :

* Chaque ressource ou groupe de ressources peut inclure un maximum de 15 paires nom/valeur de balise. Cette limitation s’applique uniquement de groupe de ressources toohello tootags appliquées directement ou de ressources. Un groupe de ressources peut contenir de nombreuses ressources qui ont chacune 15 paires nom/valeur de balise. 
* nom de la balise Hello est limitée too512 caractères et hello balise too256 limité de caractères est. Pour les comptes de stockage, nom de la balise hello est limitée too128 caractères et hello balise too256 limité de caractères est.
* Groupe de ressources toohello balises appliquées ne sont pas héritées par les ressources hello dans ce groupe de ressources. 

Si vous avez plus de 15 valeurs que vous avez besoin de tooassociate avec une ressource, utilisez une chaîne JSON pour la valeur de balise hello. Hello chaîne JSON peut contenir plusieurs valeurs qui sont le nom de balise unique tooa appliqué. Cet article montre un exemple d’affectation d’une balise de toohello de chaîne JSON.
