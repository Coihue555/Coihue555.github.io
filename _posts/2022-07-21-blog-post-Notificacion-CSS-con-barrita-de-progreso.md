## Notificacion en CSS con barrita de progreso de color

Ayer en mi trabajo (donde trabajamos con Dart/Flutter), me pidieron que hiciera una notificacion sencilla en CSS. YA que con Flutter aun me siento fuera de mi area de comfort, fue grato que me adjudicaran esa tarea. Era el unico que sabia de desarrollo web, y si bien los ultimos 5 años solo usaba Bootstrap escribir CSS puro por mi cuenta fue muy divertido y me hizo recuperar mi confianza y que de verdad estaba aportando al equipo.

La idea era sencilla, codigo sencillo para una notificacion minima y elegante. Me dieron 10 minutos para hacerlo y cumpli.

---

### Asi se ven

## Notificacion Info

![Notificacion Info](/assets/info.gif)

## Notificacion Error

![Notificacion Error](/assets/error.gif)

y en color verde seria un mensaje de confirmacion o tarea exitosa...


```css
@import url('https://fonts.googleapis.com/css2?family=Work+Sans');
body {
  font-family: 'Work Sans', sans-serif;
}

#notificacion {
    visibility: hidden;
    min-width: 250px;
    margin-left: -125px;
    background-color: rgb(255, 255, 255);
    color: rgb(44, 44, 44);
    text-align: center;
    font-weight: 400;
    border-radius: 7px;
    box-shadow: #646464 1px 1px 5px;
    position: fixed;
    z-index: 1;
    left: 50%;
    top: 30px;
  }

  .mensaje{
    margin: 10px;
    padding: 10px;
  }  

  #notificacion.mostrar {
    visibility: visible;
    -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
    animation: fadein 0.5s, fadeout 0.5s 2.5s;
  }

  #informacion, #error, #confirmacion{
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    visibility: hidden;
    width: 0%;
  }

  #informacion.mostrar{
    visibility: visible;
    background-color: blue;
    height: 5px;
    width: 100%;
    animation: progreso 1800ms;
  }

  #error.mostrar{
    visibility: visible;
    background-color: red;
    height: 5px;
    width: 100%;
    animation: progreso 1800ms;
  }

  #confirmacion.mostrar{
    visibility: visible;
    background-color: green;
    height: 5px;
    width: 100%;
    animation: progreso 1800ms;
  }

  @-webkit-keyframes progreso {
    0%{width: 0%; }
    90%{width: 100%; }
  }

  @keyframes progreso {
    0%{ width: 0%; }
    90%{width: 100%;}
  }
  
  @-webkit-keyframes fadein {
    from {top: 0; opacity: 0;}
    to {top: 30px; opacity: 1;}
  }
  
  @keyframes fadein {
    from {top: 0; opacity: 0;}
    to {top: 30px; opacity: 1;}
  }
  
  @-webkit-keyframes fadeout {
    from {top: 30px; opacity: 1;}
    to {top: 0; opacity: 0;}
  }
  
  @keyframes fadeout {
    from {top: 30px; opacity: 1;}
    to {top: 0; opacity: 0;}
  }
```

#### El codigo HTML

```html

<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>CDM Notificaciones</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <button onclick="llamada()">Llamar notificacion</button>

    <div id="notificacion">
        <div class="mensaje">
            Codigo HTML de error
        </div>
        <div id="informacion"></div>
        <!-- <div id="error"></div> -->
        <!-- <div id="confirmacion"></div> -->
    </div>

    <script>
        function llamada() {
            var x = document.getElementById("notificacion");
            x.classList.toggle('mostrar');
            setTimeout(function() {
                x.className = x.className.replace("mostrar", "");
            }, 3000);
            var y = document.getElementById("informacion");
            y.classList.toggle('mostrar');
            setTimeout(function() {
                y.className = y.className.replace("mostrar", "");
            }, 3000);
        }
    </script>
</body>

</html>
```
