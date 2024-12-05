# Cómo Empezar a Usar Pixel con Go 🎮

Este proyecto es una guía paso a paso para aprender a usar **Pixel**, una librería para crear videojuegos en 2D utilizando el lenguaje de programación Go. Aquí encontrarás todo lo necesario para configurar tu entorno, instalar las dependencias y escribir tu primer programa funcional con Pixel.

---

## 🛠️ Requisitos

Antes de comenzar, asegúrate de tener lo siguiente:

1. [Go](https://golang.org/) instalado en tu sistema (versión 1.16 o superior). Si no lo tienes, descárgalo desde la página oficial e instálalo.
2. Un editor de texto o IDE (recomiendo Visual Studio Code, pero puedes usar cualquiera).
3. Acceso a una terminal para ejecutar comandos.

---

## 🚀 Configuración e Instalación

Sigue estos pasos para configurar tu entorno de desarrollo y empezar a usar Pixel:

1. **Crea una carpeta para tu proyecto y entra a ella:**

   ```bash
   mkdir mi-primer-juego
   cd mi-primer-juego
   
Inicialización un módulo de Go:
go mod init mi-primer-juego

Instala la librería Pixel:

go get github.com/faiface/pixel
go get github.com/faiface/pixel/pixelgl

crea un archivo llamado main.go
touch main.go

en el archivo de main copiamos el codigo para la creación de una ventana básica:

package main

import (
    "github.com/faiface/pixel"
    "github.com/faiface/pixel/pixelgl"
    "image/color"
)

func run() {
    cfg := pixelgl.WindowConfig{
        Title:  "Mi Primer Juego",
        Bounds: pixel.R(0, 0, 800, 600),
        VSync:  true,
    }
    win, err := pixelgl.NewWindow(cfg)
    if err != nil {
        panic(err)
    }

    for !win.Closed() {
        win.Clear(color.RGBA{R: 100, G: 149, B: 237, A: 255}) // Fondo azul
        win.Update()
    }
}

func main() {
    pixelgl.Run(run)
}


## Finalmente ejecutamos 

go run main.go


## Personalización y mejora

Agregar sprites: Usa imágenes para representar personajes u objetos en tu juego.
Movimiento: Detecta entradas del teclado para mover objetos en la pantalla.
Colisiones: Agrega lógica para detectar y manejar colisiones entre objetos.
Animaciones: Crea animaciones para tus sprites utilizando las herramientas de Pixel.
Sonidos: Implementa efectos de sonido o música para mejorar la experiencia.
Puntajes o niveles: Agrega un sistema de puntuación o crea niveles más complejos.

Este archivo contiene **todo lo necesario** para que cualquiera configure, instale y comience a usar Pixel con Go

