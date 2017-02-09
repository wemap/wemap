# External Interface
##### Comment interagir en JavaScript avec ma page HTML et une application Livemap

L'objet ouvert `ExternalInterface` des livemaps permet de prendre le contrôle par une page client de [certaines fonctionnalités des livemaps](#publics_methods).

Pour ce faire les livemaps doivent être [initialisées en JavaScript pur](#init_native_javascript) et non via une iframe ou une balise script.

L'objet `ExternalInterface` permet également aux utilisateurs un accès à [certains événements notifiant des changements au sein des Livemaps](#events), comme un clic sur un pinpoint ou l'ouverture d'une liste.

## Sommaire

1. [Initialisation d'une livemap](#init_native_javascript)
2. [Écouter/Supprimer des événements provenant d'une Livemap](#externals_listeners)
  1. addEventListener
  2. removeEventListener
3. [Événements d'écoute d'une Livemap](#events)
  1. mapUpdate
  2. pinpointClick
4. [Méthode ouverte d'une livemap](#methods)
  1. Centrer la carte sur une position spécifique
  2. Obtenir la position du centre de la carte en cours d'affichage
  3. Obtenir l'objet pinpoint le plus proche d'une position
  4. Affecter un centre sur la carte en conservant le zoom en cours
  5. Affecter un zoom sur la carte en conservant le centre en cours
5. [Types de données reçues](#types)

<a name="init_native_javascript"></a>
## 1. Initialisation de l'ExternalInterface d'une livemap

```javascript
<html>
  <head>
    ...
  </head>
  <body>

    ...
    <div id="my-livemap-container" style="width:600px;height:400px;">
    <script type="text/javascript"
      class="wemap_livemap"
      src="https://livemap.getwemap.com/js/livemap.min.js"
      data-emmid="xxxxx"
      data-token="xxxxx">
    </script>
    </div>

    <script type="text/javascript">
      wemap.v1.getExternalInterface(function(instance) {
          // fired when map instance is ready to interact
          // store here a reference af a Livemap's ExternalInterface
          window.livemap = instance;
      });
    </script>

    ...

  </body>
</html>
```

<a name="externals_listeners"></a>
## 2. Écouter/Supprimer des événements provenant d'une instance d'une Livemap

### 2.1. addEventListener

> La méthode `addEventListener` permet de s'abonner à certains événements émanant (paramètre [eventName](#events)) d'une instance d'une livemap

```javascript
window.livemap.addEventListener(eventName <String>, callbackListener <Function>);
```

### 2.2. removeEventListener
> La méthode `removeEventListener` permet de se désabonner des événements émanant d'une instance d'une livemap

```javascript
window.livemap.removeEventListener(eventName <String>, callbackListener <Function>);
```

<a name="events" />
## 3. Événements d'écoute d'une Livemap

### 3.1 mapUpdate

> Cet événement est propagé lorsque la carte a chargé un nouveau jeu de données.

```javascript
window.livemap.addEventListener('mapUpdate', function() {
    alert('map update');
});
```

### 3.2 pinpointClick

> Événements propagés lorsque le visiteur d'une carte clique sur un pinpoint sur la carte.

```javascript
window.livemap.addEventListener('pinpointClick', function(evt) {
    alert('pinpoint click', evt.pinpoint);
});
```

<a name="methods"></a>
## 4. Méthode ouverte d'une livemap

### 4.1 Centrer la carte sur une position spécifique

```javascript
window.livemap.centerTo(latlng <Position>, zoom <Number>);
```

[exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/center_to.html)

### 4.2 Obtenir la position du centre de la carte en cours d'affichage

```javascript
// Retourne un objet Position
window.livemap.getCenter();
// Exemple:
// var coords = window.livemap.getCenter();
// console.log(coords);
// output: {latitude: 1.451, longitude: 1.456}
```

[exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/get_center.html)

### 4.3 Obtenir le pinpoint le plus proche d'une position

```javascript
window.livemap.findNearestPinpoint(center <Position>, function(pinpoint) {
    // un Pinpoint a été trouvé
}, function() {
    // pas de Pinpoint trouvé
});
```

[exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/find_nearest_pinpoint.html)

### 4.4 Affecter un centre sur la carte en conservant le zoom en cours

```javascript
window.livemap.setCenter(center <Position>);
```

[exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/set_center.html)

### 4.5 Affecter un zoom sur la carte en conservant le centre en cours

```javascript
window.livemap.setZoom(zoom <Number>);
```

[exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/set_zoom.html)

<a name="types"></a>

### 5. Types de données

**Position**

```javascript
var obj = {
    latitude: 38.8977,
    longitude: -77.0365
};
```

**Pinpoint**
```javascript
var obj = {
    id: 12345,
    name: 'The White House',
    address: '1600 Pennsylvania Avenue, Washington D.C.',
    description: 'The White House is the official residence and principal workplace of the President of the United States.',
    latitude: 38.8977,
    longitude: -77.0365
};
```
