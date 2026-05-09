# automatas_APE5
# AutomataLab — APE 005
## Conversión AFND → AFD → Minimización
---

## Estructura del Proyecto

```
automata-app/
└── backend/                            ← Proyecto Spring Boot
    ├── pom.xml
    └── src/main/
        ├── java/com/automata/
        │   ├── AutomataApplication.java         ← Punto de entrada
        │   ├── controller/
        │   │   └── AutomatonController.java      ← REST endpoints
        │   ├── service/
        │   │   ├── AutomatonService.java          ← Orquestador principal
        │   │   ├── SubsetConstructionService.java ← AFND → AFD
        │   │   ├── DfaMinimizationService.java    ← Minimización
        │   │   └── StringVerificationService.java ← Verificación de cadenas
        │   ├── model/
        │   │   ├── Automaton.java                 ← Modelo de autómata
        │   │   └── ConversionResult.java          ← Resultado completo
        │   └── dto/
        │       ├── AutomatonRequest.java           ← Entrada del frontend
        │       ├── VerificationRequest.java
        │       └── VerificationResponse.java
        └── resources/
            ├── application.properties
            └── static/                  ← Frontend (HTML/CSS/JS)
                ├── index.html
                ├── css/styles.css
                └── js/
                    ├── api.js           ← Cliente HTTP
                    ├── table.js         ← Tabla de transiciones
                    ├── render.js        ← Renderizado de resultados
                    └── app.js           ← Controlador principal
```

---

## Requisitos

- **Java 21** (JDK)
- **Maven 3.8+**
- Navegador moderno (Chrome, Firefox, Edge)

---

## Ejecución

```bash
cd backend
mvn spring-boot:run
```

Luego abre: **http://localhost:8080**

---

## Endpoints REST

| Método | Ruta                      | Descripción                              |
|--------|---------------------------|------------------------------------------|
| POST   | `/api/automaton/convert`  | AFND → AFD → AFD Minimizado              |
| POST   | `/api/automaton/verify`   | Verificar cadenas (equivalencia)         |
| GET    | `/api/automaton/examples` | Ejemplos predefinidos de la práctica     |

---

## Algoritmos Implementados

### 1. Construcción de Subconjuntos (AFND → AFD)
- Calcula el cierre de cada conjunto de estados con cada símbolo
- Genera estados AFD nombrados A, B, C...
- Maneja el estado de error (∅) como "ERR"

### 2. Minimización por Tabla de Pares
- Marca pares distinguibles: (aceptación, no-aceptación)
- Propaga: si δ(p,a) y δ(q,a) son distinguibles → (p,q) es distinguible
- Fusiona estados no marcados (equivalentes) con Union-Find

### 3. Verificación de Equivalencia
- NFA: simulación paralela de estados activos
- DFA: seguimiento determinista del estado actual
- Tokenización automática (char por char o tokens multi-carácter)

---

## Ejemplos de la Práctica APE 5

| # | Nombre                   | Patrón               | Alfabeto           |
|---|--------------------------|----------------------|--------------------|
| 1 | Secuencias Genéticas     | `K G X* F`           | {K, G, X, F}       |
| 2 | E-commerce               | `H S+ C`             | {H, S, C}          |
| 3 | Chat/Slack               | `@bot (user)? cmd\|help` | {@bot, user, cmd, help} |

---


