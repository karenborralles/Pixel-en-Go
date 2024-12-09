## 🖼️ Como renderizar imágenes en pixel usando go 

Pixel es una librería poderosa que permite renderizar imágenes de forma sencilla. Aquí te enseño paso a paso cómo hacerlo correctamente.

## 1. Prepara tu Proyecto
Asegúrate de que tienes configurado tu entorno con Pixel. Si aún no lo haces, sigue estos pasos:

Inicializa tu proyecto con go mod init tu-proyecto.
Instala Pixel con:

   ```bash
   go get github.com/faiface/pixel
   go get github.com/faiface/pixel/pixelgl
   ```

2. Crea una carpeta assets/ dentro de tu proyecto y coloca una imagen (por ejemplo, personaje.png) en esa carpeta. Tu estructura debería lucir así:

   ```bash
   tu-proyecto/
   ├── assets/
   │   └── personaje.png
   └── main.go
   ```

## 2. Código para Renderizar una Imagen
Crea o abre el archivo main.go y añade el siguiente código:

```bash
   package main

import (
	"github.com/faiface/pixel"
	"github.com/faiface/pixel/pixelgl"
	"image"
	_ "image/png" // Necesario para decodificar imágenes PNG
	"os"
)

func cargarImagen(ruta string) pixel.Picture {
	// Abre el archivo de imagen
	archivo, err := os.Open(ruta)
	if err != nil {
		panic(err)
	}
	defer archivo.Close()

	// Decodifica la imagen
	img, _, err := image.Decode(archivo)
	if err != nil {
		panic(err)
	}

	// Convierte la imagen a un formato compatible con Pixel
	return pixel.PictureDataFromImage(img)
}

func run() {
	// Configura la ventana
	cfg := pixelgl.WindowConfig{
		Title:  "Renderizando una Imagen con Pixel",
		Bounds: pixel.R(0, 0, 800, 600),
		VSync:  true,
	}
	ventana, err := pixelgl.NewWindow(cfg)
	if err != nil {
		panic(err)
	}

	// Carga el sprite desde la imagen
	personajeSprite := pixel.NewSprite(cargarImagen("assets/personaje.png"), pixel.R(0, 0, 64, 64))

	// Posición inicial del sprite
	posicion := pixel.V(400, 300)

	for !ventana.Closed() {
		ventana.Clear(pixel.RGB(0.2, 0.3, 0.4)) // Fondo de color azul oscuro

		// Dibuja el sprite en la posición actual
		personajeSprite.Draw(ventana, pixel.IM.Moved(posicion))

		ventana.Update() // Actualiza la ventana
	}
}

func main() {
	pixelgl.Run(run)
}
   ```
## 3. Agrega Movimiento al Sprite
Si deseas mover el sprite con las teclas de dirección, puedes añadir esta lógica dentro del bucle principal:

```bash
   if ventana.Pressed(pixelgl.KeyLeft) {
	posicion.X -= 5
}
if ventana.Pressed(pixelgl.KeyRight) {
	posicion.X += 5
}
if ventana.Pressed(pixelgl.KeyUp) {
	posicion.Y += 5
}
if ventana.Pressed(pixelgl.KeyDown) {
	posicion.Y -= 5
}
   ```
Esto permitirá que el sprite se desplace hacia arriba, abajo, izquierda o derecha cuando se presionen las teclas correspondientes.

## 4.  Ejecuta el Programa

Guarda el archivo main.go.
Ejecuta el siguiente comando en tu terminal:

```bash
go run main.go
   ```
Si todo está correcto, deberías ver una ventana con tu imagen renderizada. Si implementaste movimiento, podrás desplazarla usando las teclas de dirección.

## 5. Consejos Adicionales

1. Optimización de Recursos: Carga cada imagen una vez y reutiliza el objeto pixel.Picture en lugar de cargarlo repetidamente.
2. Manejo de Errores: Siempre verifica si los archivos se abren y decodifican correctamente.
3. Spritesheets: Si necesitas animar personajes, puedes usar una imagen grande con múltiples fotogramas y renderizar diferentes secciones según sea necesario.

## 📚 Recursos Útiles

Si quieres aprender más, aquí tienes algunos recursos recomendados:

-Documentación oficial de Pixel: https://github.com/faiface/pixel.git

-Ejemplos oficiales de Pixel: https://github.com/faiface/pixel-examples.git

-Página oficial de Go: https://go.dev/

-Tour de Go (aprende la sintaxis básica): https://go.dev/tour/welcome/1

Este archivo contiene **todo lo necesario** para que cualquiera configure, instale y comience a usar Pixel con Go

