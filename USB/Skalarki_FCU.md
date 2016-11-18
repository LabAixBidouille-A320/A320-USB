# Description du protocole USB du périphérique Skalarki Flight Control Unit

La société Skalarki produit des périphérique USB pour réaliser par soi-même des cockpits pour des simulateurs d'Airbus A320. Chaque module 
correspond à l'une des parties du cockpit. 

Le FCU (Flight Control Unit) correspond à ce que l'on appelle le pilote automatique. Il permet par exemple de régler une consigne pour un cap, une vitesse ou une altitude. 

![FCU](http://www.fscockpit.eu/data/images/fcu01.jpg)

Pour commencer l'exploration des périphériques Skalarki, le FCU est un bon candidat car il comporte des entrées (bouton, intérupteur, rotacteur, ...), des 
témoins lumineux et des afficheurs.

## Typologie des échanges
Dans le logiciel *SkalarkiIO Profiler 5*, les échanges avec le périphériques sont classé en quatre catégories : 
- **Inputs**
- **ADC**
- **Outputs**
- **Displays**

Les deux premières sont des entrées et les deux dernières des sorties.

### Inputs
Les **Inputs**, comme le nom l'indique correspond aux entrées des actionneurs simples (bouton, intérupteur, rotacteur, ...). 
Leur valeur est digitale, c'est à dire que dans qu'une entrée ne peut avoir que la valeur `true` ou `false`. Pour les actionneurs 
complexes avec plus de deux positions, le logiciel utilise plusieurs entrées différentes pour coder les positions.

![](skalarki_FCU_inputs.png)

Dans le cas du module FCU, il y a au total 96 inputs différentes.

### ADC
Les **ADC** correspondent à des entrées analogiques. Généralement ce sont des potentiometres ou des capteurs de position. 
La valeur est proportionnelle à la position.
![](skalarki_FCU_ADC.png)

Le FCU n'a aucun ADC donc pour le présent module nous n'irons pas plus loin sur l'analyse de ce type d'entrées.

### Outputs
Les **Outputs**, correspondent principalement à des voyants lumineux. Leur état est binaire (allumé, éteint). 

![](skalarki_FCU_outputs.png)

Dans le cas du module FCU, il y a au total 96 outputs différentes. Ils ont la particularité d'être groupés en 6 **GROUP** de 16 sorties. Dans le logiciel *SkalarkiIO Profiler 5*, ces groupes nous permettent d'activer 16 voyants en une seule opération. Dans la partie protocole la raison de ce groupement sera plus visible.

### Displays
Les témoins lumineux ne sont pas suffisants pour représenter toutes les informations affichables sur un cockpit. 
Dans un A320, il y a des afficheurs 7 segments pour rendre visibles ces informations. 
![](skalarki_FCU_displays.png)

Le module FCU possède 24 afficheurs qui semblent eux aussi être arrangés en **GROUP** de 16 dans le logiciel. L'interaction sur ces groupes ne faisant rien, il n'est pas possible de comprendre en l'état l'utilité de cette fonctionnalité.


