# Description du protocole USB du périphérique Skalarki Flight Control Unit

La société Skalarki produit des périphérique USB pour réaliser par soi-même des cockpits pour des simulateurs d'Airbus A320. Chaque module 
correspond à l'une des parties du cockpit. 

Le FCU (Flight Control Unit) correspond à ce que l'on appelle le pilote automatique. Il permet par exemple de régler une consigne pour un cap, une vitesse ou une altitude. 

![FCU](http://www.fscockpit.eu/data/images/fcu01.jpg)

Pour commencer l'exploration des périphériques Skalarki, le FCU est un bon candidat car il comporte des entrées (bouton, intérupteur, rotacteur, ...), des 
témoins lumineux et des afficheurs.

## Typologie des messages
Dans le logiciel *SkalarkiIO Profiler 5*, les messages sont structurées comme suit : 
- **Inputs**
- **ADC**
- **Outputs**
- **Displays**

### Inputs
Les **Inputs**, comme le nom l'indique correspond aux entrées des actionneurs simples (bouton, intérupteur, rotacteur, ...). 
Leur valeur est digitale, c'est à dire que dans qu'une entrée ne peut avoir que la valeur `true` ou `false`. Pour les actionneurs 
complexes avec plus de deux positions, le logiciel utilise plusieurs entrées différentes pour coder les positions.

![](skalarki_FCU_inputs.png)

Dans le cas du module FCU, il y a au total 95 inputs différentes.

### ADC
Les **ADC** correspondent à des entrées analogiques. Généralement ce sont des potentiometres ou des capteurs de position. 
La valeur est proportionnelle à la position.
![](skalarki_FCU_ADC.png)

Le FCU n'a aucun ADC donc pour le présent module nous n'irons pas plus loin sur l'analyse de ce type d'entrées.

### Outputs

Maintenant que l'on a vu les deux types d'entrées, regardons sorties. Les **Outputs**, correspondent principalement à 
des voyants lumineux. Leur état est binaire (allumé, éteint). 

![](skalarki_FCU_outputs.png)

Dans le cas du module FCU, il y a au total 95 outputs différentes. Ils ont la particularité d'être groupés en 6 **GROUP** de 16 sorties. 
On verra dans la partie protocole la raison de ce groupement.

### Displays
Les témoins lumineux ne sont pas suffisants pour représenter toutes les informations affichables sur un cockpit. 
Dans un A320, il y a des afficheurs 7 segments pour rendre visibles ces informations. 
![](skalarki_FCU_displays.png)

