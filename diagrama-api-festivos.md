```mermaid
graph TD
    %% Cliente / Capa de Presentación Externa
    subgraph ClientLayer [Capa de Cliente]
        Client["Cliente Web / Móvil / Postman / Swagger UI"]
    end

    %% Capa de Entrada y Enrutamiento (API Gateway / Routes)
    subgraph PresentationLayer [Capa de Presentación / API]
        Index["index.js / app.js"]
        Routes["Rutas Express<br/><i>festivo.rutas.js</i>"]
        Validators["Middlewares / Validadores<br/><i>festivo.validador.js</i>"]
    end

    %% Capa de Lógica de Negocio (Controladores)
    subgraph BusinessLayer [Capa de Lógica de Negocio]
        Controllers["Controladores<br/><i>festivo.controlador.js</i>"]
        Services["Servicio de Cálculo de Fechas<br/><i>fechas.servicio.js</i>"]
    end

    %% Capa de Acceso a Datos (Repositorios / Modelos)
    subgraph DataAccessLayer [Capa de Acceso a Datos]
        Repositories["Repositorios / Modelos<br/><i>tipo.repositorio.js</i>"]
    end

    %% Capa de Persistencia
    subgraph PersistenceLayer [Capa de Persistencia]
        DB[("Base de Datos - MongoDB")]
    end

    %% Flujo de la Petición (Request)
    Client -->|"1. Petición HTTP"| Index
    Index -->|"2. Delega a"| Routes
    Routes -->|"3. Valida datos"| Validators
    Validators -->|"4. Pasa filtro"| Controllers
    Controllers -->|"5. Procesa lógica y calcula"| Services
    Services -->|"6. Solicita operación"| Repositories
    Repositories -->|"7. Consulta / Modifica"| DB

    %% Flujo de la Respuesta (Response)
    DB -.->|"8. Retorna datos"| Repositories
    Repositories -.->|"9. Procesa resultado"| Services
    Services -.->|"10. Devuelve fechas calculadas"| Controllers
    Controllers -.->|"11. Respuesta JSON"| Client

    %% Estilos de Nodos
    style ClientLayer fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#01579b
    style PresentationLayer fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#e65100
    style BusinessLayer fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#1b5e20
    style DataAccessLayer fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px,color:#4a0072
    style PersistenceLayer fill:#ffebee,stroke:#d32f2f,stroke-width:2px,color:#b71c1c