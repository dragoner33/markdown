```mermaid
sequenceDiagram

Actor U as User

Participant Web as Página Web
Participant S as Servidor
Participant DB as Base de datos
U ->> Web: Boton "crear publicación"
Activate Web
  Web -->> U: Formulario "publicacion_form.html"
Deactivate Web
U ->> Web: Envía el formulario
Activate Web
  Web ->> S: Envía la solicitud POST
  Activate S
    S ->> S: Comprueba que los datos son correctos
    S ->> S: Asigna usuario actual a la publicación
    S ->> DB: Envía los datos
    Activate DB
      S ->> DB: Envía los productos a la nueva instancia
      DB -->> S: Devuelve la instancia ya creada
    Deactivate DB
    S ->> Web: Devuelve a todas las publicaciones
  Deactivate S
  Web ->> U: Le muestra todas las publicaciones con la ultima creada
Deactivate Web
