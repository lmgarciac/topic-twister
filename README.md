# Topic Twister – Mobile Game (Unity)

**Topic Twister** es un juego mobile desarrollado en **Unity**, realizado en el marco de una **especialización en Ingeniería de Software**, con foco en **arquitectura, testabilidad y separación de responsabilidades**.

El proyecto está compuesto por **tres repositorios independientes**:
- cliente Unity (UI + presentación)
- backend principal del juego (ASP.NET)
- backend de autenticación (Kotlin / Ktor)

---

## Repositorios

- **Unity (cliente / presentación)**  
  https://gitlab.com/luism.garciac/topic-twister

- **Backend principal – Game Logic (ASP.NET)**  
  https://github.com/ElianRemaggi/Topic-Twister-BackendAPI

- **Backend de Login / Auth (Kotlin / Ktor)**  
  https://github.com/ElianRemaggi/login-topic-twister

---

## Qué muestra este proyecto

- Arquitectura por capas inspirada en **Clean Architecture**
- Separación clara entre:
  - presentación (Unity)
  - casos de uso
  - dominio / modelo
  - acceso a datos y servicios
- Uso de **Unity como cliente**, no como contenedor de lógica de negocio
- Backend con **Use Cases explícitos** y **repositorios abstraídos**
- Desarrollo del backend con **TDD**, incluyendo tests por capa
- Integración cliente-servidor mediante HTTP y serialización JSON

---

## Arquitectura general

### Cliente (Unity)

El cliente Unity se organiza con una separación explícita de responsabilidades:

- **Actions (`Assets/Scripts/Actions`)**  
  Representan **casos de uso** del lado del cliente (login, matchmaking, obtener datos, etc.).

- **Presentation (`Assets/Scripts/Presentation`)**  
  Presenters que coordinan el flujo de la aplicación (enfoque tipo **MVP**).

- **Views / Delivery (`Assets/Scripts/Delivery`)**  
  Pantallas y componentes de UI. No contienen lógica de negocio.

- **Model (`Assets/Scripts/Model`)**  
  Clases que funcionan principalmente como **DTOs / contenedores de estado** para serialización y comunicación con el backend.

- **Repositories & Services**  
  Abstracciones para acceso a datos y servicios web, con implementaciones intercambiables (web / in-memory).

> Nota: en el cliente Unity, la lógica de negocio es mínima. Las reglas del juego viven en el backend.

---

### Backend principal (ASP.NET)

El backend del juego está organizado de forma explícita por capas:

- **Controllers**  
  Exponen la API HTTP.

- **UseCases**  
  Implementan las reglas de negocio (creación de sesiones, matchmaking, validación de respuestas, progreso del juego).

- **Model**  
  Entidades de dominio y contratos.

- **Repositories (interfaces + implementaciones)**  
  Acceso a datos desacoplado.

- **Persistencia simple en JSON (`data/*.json`)**  
  Pensada para facilitar pruebas locales y reproducibilidad.

---

## Testing (TDD)

Los proyectos están pensados con un enfoque **Test Driven Development**.

Cobertura de pruebas:
- Controllers
- UseCases
- Repositories
- Servicios de infraestructura


## Cómo ejecutar el proyecto (local)

### 1. Levantar los backends

Desde sus respectivos repositorios:

- **Login Backend (Ktor)**  
  Corre en: `http://localhost:8080`

- **Game Backend (ASP.NET)**  
  Corre en: `http://localhost:5026`

> El repositorio de Unity incluye scripts (`start_backends.bat`) para facilitar el arranque local de ambos servicios.

---

### 2. Ejecutar el cliente Unity

#### Opción A — Ejecutar desde el Editor

1. Clonar el repositorio de Unity  
2. Abrir el proyecto con una versión **Unity LTS**  
3. Abrir la escena principal del juego  
4. Ejecutar desde el **Editor**

> El proyecto está pensado para ejecutarse en modo **Portrait** (mobile).

---

#### Opción B — Build para Windows (modo simulación para probar el flujo completo)

Como alternativa, es posible generar una **build para Windows** desde Unity ajustando manualmente la resolución y el aspect ratio para simular un entorno mobile.

Esta opción permite:
- Ejecutar **múltiples instancias del juego** en paralelo
- Jugar partidas locales “contra uno mismo”
- Probar flujos de matchmaking y sesión sin dispositivos móviles

Configuración sugerida:
- Resolución fija en modo *Portrait*
- Ventana no redimensionable

>(Player Settings -> Player -> Resolution and Presentation -> Windowed -> 720 x 1280 -> Resizable Window = No

---

## Notas sobre el alcance

- Proyecto académico orientado a **arquitectura, diseño y testing**
- No busca ser un producto comercial ni un juego finalizado
- Algunas decisiones priorizan claridad conceptual y experimentación por sobre optimización o pulido final
- El **backend es la fuente de verdad** de la lógica del juego

## Estado del proyecto y deuda técnica

Este proyecto refleja un **estado real de evolución** propio de un trabajo académico desarrollado a lo largo del tiempo.

Existen aspectos de **deuda técnica conocida**, tales como:
- tests obsoletos o en desuso
- scripts experimentales no eliminados
- separación progresiva del backend hacia servicios independientes
- pruebas que ya no reflejan el comportamiento actual del sistema

Estas situaciones son **conocidas y deliberadamente conservadas** como parte del contexto del proyecto.  
El foco de este repositorio es **documentar decisiones de arquitectura, diseño y testing**, no presentar un producto pulido ni mantenido activamente.

Actualmente **no está previsto continuar el refactor ni la limpieza técnica** del proyecto.

