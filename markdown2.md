```mermaid
sequenceDiagram

Actor U as User

Participant Web as Página Web
Participant S as Servidor
Participant DB as Base de datos
U ->> Web: Boton "Busca Publicaciones"
Activate Web
  Web -->> U: Formulario "publicacion_buscar.html" sin filtro de busqueda
Deactivate Web
U ->> Web: Envía los productos modificados
Activate Web
  Web ->> S: Envía la solicitud GET
  Activate S
    S ->> S: Coge la lista de productos
    S ->> DB: Realiza la petición de todas las publicaciones
    Activate DB
      DB -->> S: Envía la informacion de las publicaciones
    Deactivate DB
    S ->> S: Filtra las publicaciones por los productos
    S ->> Web: Devuelve el resultado
  Deactivate S
  Web ->> U: Le muestra las publicaciones filtradas
Deactivate Web
