# PyUSB 1.0

Traduction libérale du [tutoriel originel anglais](https://github.com/walac/pyusb/blob/master/docs/tutorial.rst)

## Introduction

[PyUSB 1.0](https://walac.github.io/pyusb/) est une librairie écrite en et faite pour le langage de programmation Python. Elle est **multiplateforme** et devrait marcher avec **Python version supérieure ou égale à 2.4**. PyUSB est directement compatible avec *libusb 0.1*, *libusb 1.0*, et *OpenUSB*. Il est possible d'écrire son propre backend.

L'USB est un protocole complexe, mais PyUSB a des valeurs par défaut pour la plupart des configurations communes pour une **utilisation facilitée**. La bibliothèque supporte les **transferts isochrones** tant que le backend utilisé le fait.

## Tutoriel

### Descriptions des modules

Les modules PyUSB modules sont dans le *package* ``usb`` Il s'agit de:

Contenu	| Description
-------	| -----------
core    | Le module USB principal.
util    | Functions utilitaires.
control | Requêtes de contrôle standard.
legacy  | La couche de compatibilité 0.x.
backend | Un sous-package contenant les backends fournies.
======= | ===========

Par exemple, pour importer le module ``core``, taper:

    >>> import usb.core
    >>> dev = usb.core.find()

### Prise en main

```python
    import usb.core
    import usb.util

    # trouver notre périphérique (device)
    dev = usb.core.find(idVendor=0xfffe, idProduct=0x0001)

    # a-t'il été trouvé ?
    if dev is None:
        raise ValueError('Device not found')

    # Paramétrer la configuration active. Sans arguments,
    # la première configuration sera celle activée
    dev.set_configuration()

    # Récupérer une instance d'endpoint (point d'accès "de terminaison")
    cfg = dev.get_active_configuration()
    intf = cfg[(0,0)]

    ep = usb.util.find_descriptor(
        intf,
        # coupler le premier endpoint OUT
        custom_match = \
        lambda e: \
            usb.util.endpoint_direction(e.bEndpointAddress) == \
            usb.util.ENDPOINT_OUT)

    assert ep is not None

    # écrire les données
    ep.write('test')
```

Les deux premières lignes importent des modules du package PyUSB. ``usb.core`` est le module principal et ``usb.util`` contient des fonctions utilitaires.
La commande suivante cherche notre périphérique et retourne une instance d'objet s'il le trouve. Sinon, il retourne ``None`` et une erreur est levée.
Ensuite, nous paramétrons la configuration à utiliser. À noter qu'ici aucun argument indiquant la configuration voulue n'est indiquée. En effet, beaucoup de configurations PyUSB ont des valeurs par défaut pour les périphériques communs. Dans ce cas, la configuration utilisée est la première trouvée.
Après, nous cherchons l'endpoint qui nous intéresse dans la première interface que nous avons.
Une fois trouvé, nous lui envoyons les données.

Si nous connaissons l'adresse de l'endpoint à l'avance, nous pouvons simplement appeler la fonction ``write`` du périphérique objet:

```python
    dev.write(1, 'test')
```

Ici, nous écrivons la string 'test' à l'endpoint d'adresse *1*. Les fonctions vues seront détaillées dans les sections suivantes.