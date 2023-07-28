```mermaid
sequenceDiagram

Actor U as User

Participant Web as Template(Publicacion_form)
Participant S as View(PublicacionCreate)
Participant M as Model(Publicacion)
Participant DB as Base de datos
U ->> Web: Envía el formulario
Activate Web
  Web ->> S: PublicacionCreate(CreateView)
  Activate S
    S ->> S: Comprueba que los datos son correctos
    S ->> S: perfil = self.request.user.profile
    S ->> M: form.instance.save()
    Activate M
      S ->> M: form.instance.productos.set(productos)
      M ->> DB: Envía la instancia
      Activate DB
        DB -->> M: Devuelve la confirmación
      Deactivate DB
      M -->> S: Envía la confirmación
    Deactivate M
    S ->> Web: return super().form_valid(form)
  Deactivate S
  Web ->> U: Muestra todas las publicaciones
Deactivate Web
