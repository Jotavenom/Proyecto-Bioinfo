# Proyecto-Bioinfo


# Filogenómica Comparativa y Arquitectura de SVMPs

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat&logo=python)
![Biopython](https://img.shields.io/badge/Bioinformatics-Biopython-green?style=flat)
![Google Colab](https://img.shields.io/badge/Run%20in-Google%20Colab-orange?style=flat&logo=googlecolab)
![Status](https://img.shields.io/badge/Status-Active-success)

> **Análisis in silico de la divergencia evolutiva y conservación de motivos funcionales en Metaloproteinasas de Veneno de Serpiente (SVMPs) mediante integración de APIs bioinformáticas.**

---

##Descripción del Proyecto

Este proyecto implementa un flujo de trabajo bioinformático para caracterizar la evolución molecular de las **Metaloproteinasas de Veneno de Serpiente (SVMPs)** en 10 especies distintas.

El pipeline correlaciona la filogenia molecular tradicional con la conservación de dominios funcionales, utilizando un enfoque híbrido que combina herramientas locales (alineamiento, filogenia) con consultas a bases de datos remotas en la nube (EBI InterPro) para la anotación estructural automatizada.

---

## Hipótesis Científica

> "Si bien el dominio catalítico (**Metallopeptidase M12B**) presentará una alta conservación de secuencia  para preservar la función enzimática, los dominios auxiliares C-terminales identificados por **InterPro/SMART** mostrarán patrones de mutación acelerada, correlacionándose con la diversificación evolutiva de las especies analizadas."

---

## Objetivos

### Objetivo General
Caracterizar la evolución molecular de las SVMPs en 10 especies de serpientes, correlacionando la filogenia molecular con la conservación de dominios funcionales identificados automáticamente.

### Objetivos Específicos

**OE1 (Alineamiento):** Construir un Alineamiento Múltiple de Secuencias (MSA) robusto utilizando el algoritmo iterativo **MUSCLE** para minimizar errores de inserción de gaps.
**OE2 (Filogenia):** Inferir las relaciones evolutivas mediante un árbol de **Neighbor-Joining**, identificando clados ortólogos.
**OE3 (Arquitectura de Dominios - API):** Implementar un script en Python que consulte la API de **InterPro (EBI)** para anotar automáticamente los dominios Pfam y SMART (Catalítico, Disintegrina, Rico en Cisteína) sobre la secuencia consenso.
**OE4 (Integración):** Mapear visualmente las regiones conservadas (**Sequence Logo**) contra los dominios estructurales identificados para validar funcionalmente las regiones de alta/baja entropía.

---

## Metodología (Pipeline)

El flujo de trabajo se divide en 4 fases principales:

1.  **Ingesta (Input):**
    * Carga de archivo Multi-FASTA (usuario).
    * Validación de formato y limpieza con `Biopython`.
2.  **Procesamiento (Core):**
    * Alineamiento Múltiple utilizando **MUSCLE** (Local).
    * Generación estadística de la secuencia Consenso.
3.  **Consulta Externa (Cloud API):**
    * Envío de la secuencia consenso a **InterProScan** vía `bioservices`.
    * Recuperación de anotaciones **Pfam** (Familias de proteínas) y **SMART** (Dominios de señalización).
4.  **Análisis Evolutivo & Visualización:**
    * Cálculo de matriz de distancias y construcción del Árbol Filogenético.
    * Generación de gráfico de Entropía (**Logomaker**) superpuesto con la arquitectura de dominios.

---

## Estrategias y Stack Tecnológico

Este proyecto prioriza la reproducibilidad y la eficiencia mediante el uso de APIs REST y entornos gestionados.

### Estrategias Clave
* **Cloud Computing (API REST):** En lugar de descargar la base de datos InterPro (+50GB), utilizamos `bioservices` para realizar peticiones HTTP y recibir anotaciones en JSON/XML, manteniendo el script ligero y ejecutable en Google Colab.
* **Algoritmo MUSCLE:** Seleccionado sobre ClustalW por su mayor precisión en el refinamiento iterativo de secuencias con longitud media.
* **Visualización Nativa:** Uso de `Biopython Phylo` y `Matplotlib` para renderizar resultados sin depender de software externo.

### Librerías y Herramientas

| Componente | Herramienta | Función |
| :--- | :--- | :--- |
| **Lenguaje** | `Python 3.x` | Orquestación del flujo de trabajo. |
| **Secuencias** | `Biopython` | Parseo FASTA, manejo de AlignIO y Phylo. |
| **API Client** | `bioservices` | Conexión remota a EBI/InterProScan. |
| **Visualización** | `logomaker` | Generación de gráficos de conservación (Sequence Logos). |
| **Alineamiento** | `MUSCLE` | Binario de sistema para MSA de alta precisión. |

---

## Instalación y Uso

Este proyecto está diseñado para ejecutarse en **Google Colab**

### Prerrequisitos
Instalación de dependencias del sistema y de Python:

```bash
# Instalación del binario MUSCLE (Debian/Ubuntu/Colab)
apt-get install muscle

# Instalación de librerías Python
pip install biopython bioservices logomaker pandas matplotlib
