```mermaid
classDiagram
    class Tipo {
        + int indice
        + string tipo
        + string modoCalculo
        + array festivos
    }

    class Festivo {
        + int dia
        + int mes
        + string nombre
        + int diasDePascua
    }

    Tipo "1" *-- "0..*" Festivo : contiene