```mermaid
sequenceDiagram

Actor U as User

Participant Web as Template(Publicaciones_buscar)
Participant S as View(PublicacionCreate)
Participant M as Model(Publicacion)
Participant DB as Base de datos
U ->> Web: Envía los productos seleccionados
Activate Web
  Web ->> S: Envía la lista de productos
  Activate S
    S ->> S: selected_productos = self.request.GET.getlist('productos')
    S ->> M: Realiza la petición de todas las publicaciones
    Activate M
      M ->> DB: pide la informacion de las publicaciones
      Activate DB
        DB -->> M: Le devuelve todas las publicaciones
      Deactivate DB
      M -->> S: Devuelve la informacion de las publicaciones
    Deactivate M
    S ->> S: queryset = queryset.filter(productos__in=productos)
    S ->> Web: Devuelve el resultado
  Deactivate S
  Web ->> U: Le muestra las publicaciones filtradas
Deactivate Web
