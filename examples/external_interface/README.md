# External Interface
##### Comment interagir en JavaScript avec ma page HTML et une application Livemap

L'objet ouvert `ExternalInterface` des livemaps permet de prendre le contrôle par une page client de [certaines fonctionnalités des livemaps](#publics_methods).

Pour ce faire les livemaps doivent être [initialisées en JavaScript pur](#init_native_javascript) et non via une iframe ou une balise script.

L'objet `ExternalInterface` permet également aux utilisateurs un accès à [certains événements notifiant des changements au sein des Livemaps](#events), comme un clic sur un pinpoint ou l'ouverture d'une liste.

### Sommaire

1. [Initialisation d'une livemap](#init_native_javascript)
2. [Écouter/Supprimer des événements provenant d'une instance d'une Livemap](#externals_listeners)
3. [Événements d'écoute d'une carte](#events)
4. [Méthode ouverte d'une livemap](#publics_methods)
5. [Exemple d'un Pinpoint Object](#pinpoint_object)

<a name="init_native_javascript"></a>
### 1. Initialisation de l'ExternalInterface d'une livemap

```javascript
<html>
  <head>
    ...
  </head>
  <body>

    ...
    <script type="text/javascript"
            class="wemap_livemap"
            src="https://livemap.getwemap.com/js/livemap.min.js"
            data-emmid="xxxxx"
            data-token="xxxxx">
    </script>

    <script type="text/javascript">
      wemap.v1.getExternalInterface(function(instance) {
          // fired when map instance is ready to interact
          // store here a reference af a Livemap's ExternalInterface
          window.livemap = instance;
          window.livemap.addEventListener('mapUpdate', function(data) {
              console.log('on livemap update', data);
          });
          window.livemap.addEventListener('pinpointClick', function(data) {
              console.log('on livemap pinpoint click', data);
          });
      });
    </script>

    ...

  </body>
</html>
```

<a name="externals_listeners"></a>
### 2. Écouter/Supprimer des événements provenant d'une instance d'une Livemap

#### 2.1. addEventListener

La méthode `addEventListener` permet de s'abonner à certains événements émanant (paramètre [eventName](#events)) d'une instance d'une livemap

```javascript
window.livemap.addEventListener(eventName <String>, callbackListener <Function>);
```

#### 2.2. removeEventListener

La méthode `removeEventListener` permet de se désabonner des événements émanant d'une instance d'une livemap

```javascript
window.livemap.removeEventListener(eventName <String>, callbackListener <Function>);
```

<a name="events" />
### 3. Événements d'écoute d'une carte

**mapUpdate**

```javascript
window.livemap.addEventListener('mapUpdate', function __callback__ (){});
```
Événements propagés lorsqu'une nouvelle pile de pinpoints d'une carte ont été chargés

**pinpointClick**

```javascript
window.livemap.addEventListener('pinpointClick', function __callback__ (){});
```
Événements propagés lorsque le visiteur d'une carte clique sur un pinpoint

<a name="publics_methods"></a>
### 4. Méthode ouverte d'une livemap

**Afficher les points d'intérêts (pinpoints) autour de moi**

```javascript
window.livemap.aroundMe();
```

[page d'exemple](https://github.com/wemap/welcome/blob/master/examples/external_interface/around_me.html)

**Centrer la carte sur une position spécifique**

```javascript
window.livemap.centerTo(latlng <Position>, zoom <Number>);
```

**Obtenir la position du centre de la carte en cours d'affichage**

```javascript
// Retourne un objet Position
window.livemap.getCenter();
// Exemple:
// var coords = window.livemap.getCenter();
// console.log(coords);
// output: {latitude: 1.451, longitude: 1.456}
```

**Obtenir l'objet pinpoint le plus proche d'une position**

```javascript
window.livemap.findNearestPinpoint(center <Position>, function(result) {
    // result.pinpoint contient un Pinpoint
});
```

**Affecter un centre sur la carte en conservant le zoom en cours**

```javascript
window.livemap.setCenter(center <Position>);
```

**Affecter un zoom sur la carte en conservant le centre en cours**

```javascript
window.livemap.setZoom(zoom <Number>);
```

<a name="pinpoint_object"></a>
### 5. Types de données

**Position**

```javascript
var obj = {
    latitude: 12.34,
    longitude: 56.78
};
```

**Pinpoint**
```javascript
var obj = {
  id: ,
  name: ,
  address: ,
  description: ,
  latitude: ,
  longitude: ,
  updated: ,
  created: ,
  distanceFromCenter:
};
```
