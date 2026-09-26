# Crucigrama de Chile

Crucigrama interactivo en español con palabras de la vida diaria y del lenguaje chileno (comidas, naturaleza, familia, etc.). Es una aplicación de **un solo archivo HTML**, sin dependencias, sin build y sin backend.

## Uso

Abre `crucigrama_chile.html` directamente en el navegador, o sírvelo con cualquier servidor estático:

```bash
python3 -m http.server 8000
# luego visita http://localhost:8000/crucigrama_chile.html
```

## Características

- **Puzzle inicial curado a mano** (grilla de 31 × 21) con 41 pistas horizontales y verticales.
- **Generador de puzzles nuevos**: arma un crucigrama aleatorio a partir de un banco de palabras (botón *Generar puzzle nuevo*).
- **Navegación con teclado y con toque**: selecciona casillas o pistas; tocar de nuevo una casilla alterna entre horizontal y vertical.
- **Revisar respuestas**: marca en verde las letras correctas y en naranja las incorrectas.
- **Pista**: revela una letra de la palabra seleccionada (o de la primera palabra incompleta).
- **Borrar respuestas**: reinicia el tablero actual.
- Las pistas resueltas se tachan y, al completar todo, aparece un mensaje de felicitación.
- Diseño responsive (columnas de pistas apiladas y casillas más pequeñas en móvil).

## Controles

| Acción | Efecto |
| --- | --- |
| Letras (A–Z, Ñ) | Escribe y avanza a la siguiente casilla |
| `Backspace` | Borra y retrocede |
| Flechas | Mueven el foco por la grilla |
| Clic en casilla / pista | Selecciona la palabra y muestra su pista |

## Estructura del código

Todo está en `crucigrama_chile.html`:

| Sección | Contenido |
| --- | --- |
| `<style>` | Estilos de la grilla, pistas y botones |
| `DATA_INICIAL` | Puzzle curado: `grid` (`"fila,col"` → letra), `numeros` y listas `clues_h` / `clues_v` |
| `BANCO_PALABRAS` | Pares `[PALABRA, "pista"]` usados por el generador (letras sin tildes; las pistas sí las llevan) |
| `ConstructorCrucigrama` / `generarCrucigrama()` | Generador aleatorio: coloca una palabra semilla y va cruzando el resto; hasta 10 intentos, máximo 34 palabras |
| `iniciarJuego`, `renderGrid`, `renderClues` | Renderizado del tablero y las listas de pistas |
| `manejarTeclado`, `seleccionarCelda`, etc. | Interacción y navegación |
| `revisarTodo`, `darPista`, `reiniciar`, `verificarVictoria` | Lógica de juego |

## Agregar palabras

Añade una entrada al arreglo `BANCO_PALABRAS`, sin tildes en la palabra:

```js
["CAZUELA", "Comida de olla con carne, papa y verduras"],
```

Quedará disponible en los próximos puzzles generados.
