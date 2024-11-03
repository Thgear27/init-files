# Entiende C++ escribiendo un raster para gráficos 3D

## Pequeña historia

Uno de los primeros lenguajes de programación que aprendí fue c++, tengo que admitir que al principio fue uno de los lenguajes que más me costó aprender, había un montón de cosas que yo consideraba impredecibles, como que un arreglo se transformaba en un puntero al primer elemento cuando se pasaba por una función, errores con el namespace std, los errores inleíbles que arrojaba el compilador, entre otros. Pero con el tiempo fui aprendiendo a lidiar con estos problemas y me di cuenta que c++ es un lenguaje muy poderoso, con una sintaxis muy flexible y que permite hacer cosas muy interesantes. En cuanto entiendes cómo funciona el lenguaje mínimamente, puedes predecir lo que sucederá, qué errores arrojará el compilador y cómo solucionarlos.

Creo que la única forma de entender el lenguaje es a través de la práctica, por eso en este taller vamos a escribir un raster para gráficos 3D en C++. Para eso vamos a empezar desde lo más básico, veremos el proceso de generar un ejecutable, qué es el preprocesador, cómo se compila, cómo se linkea, cómo se ejecuta, todo esto a través de la terminal. Creo que esto sentará las bases para entender cómo funciona el lenguaje.

Este taller está basado en la serie de tutoriales de ssloy en [https://github.com/ssloy/tinyrenderer/wiki](https://github.com/ssloy/tinyrenderer/wiki)

# Temario

- ¿Por qué aprender C++?
- ¿Qué es un raster?
- Uso básica de la terminal
- Hola Mundo en C++
- Proceso de Compilación
  - Preprocesador
  - Compilación
  - Linker
  - Ejecución
- Variables y estructuras de control
- Ejercicio: Compilar el repositorio de [init-files](https://github.com/Thgear27/init-files)
- Dibujar un punto en la pantalla
- Algoritmo de Bresenham
- Dibujar un modelo 3D

# Comandos básicos de la terminal

- `ls`: Lista los archivos y directorios en el directorio actual
- `cd <directorio>`: Cambia de directorio
- `mkdir <nombre>`: Crea un directorio
- `touch <nombre>`: Crea un archivo
- `rm <nombre>`: Elimina un archivo
- `cat <archivo>`: Muestra el contenido de un archivo
- `echo "Hola mundo"`: Muestra un mensaje en la terminal
- `clear`: Limpia la terminal
- `pwd`: Muestra la ruta del directorio actual

# Proceso de compilación

Cuando escribimos un programa en C++, este pasa por un proceso de compilación con varios pasos, pero en este taller vamos a ver los que considero más importantes:

1. **Preprocesador**: En esta etapa se procesan las directivas de preprocesador, como las directivas `#include`, `#define`, `#ifdef`, `#ifndef`, entre otras. El resultado de esta etapa es un archivo con extensión `.i` que contiene el código fuente con las directivas de preprocesador resueltas.

2. **Compilación**: En esta etapa se traduce el código fuente a código ensamblador, el resultado de esta etapa es un archivo con extensión `.s` que contiene el código ensamblador.

3. **Ensamblado**: En esta etapa se traduce el código ensamblador a código máquina, el resultado de esta etapa es un archivo con extensión `.o` que contiene el código máquina.

4. **Linker**: En esta etapa se enlazan los archivos objeto generados en la etapa anterior, el resultado de esta etapa es un archivo ejecutable.

5. **Ejecución**: En esta etapa se ejecuta el archivo ejecutable.

## Comandos

- El paso de Preprocesador y Compilación puede ser realizado con el comando

```bash
g++ -c archivo.cpp -o archivo.o
```

- El paso de Linker puede ser realizado con el comando

```bash
g++ archivo.o -o ejecutable
```

- El paso de Ejecución puede ser realizado con el comando

```bash
./ejecutable
```

# Directivas de preprocesador

Las directivas de preprocesador son instrucciones que se procesan antes de la compilación, estas instrucciones empiezan con el símbolo `#`. Algunas de las directivas más comunes son:

- `#include`: Copia y pega el contenido de un archivo en el archivo actual
- `#define`: Define una macro
- `#ifdef`: Si la macro está definida, ejecuta el código
- `#ifndef`: Si la macro no está definida, ejecuta el código
- `#endif`: Fin de un bloque `#ifdef` o `#ifndef`

# El linker

El linker es una herramienta que se encarga de enlazar los archivos objeto generados en la etapa de compilación, enlaza las funciones y variables definidas en diferentes archivos objeto. El linker es el encargado de generar el archivo ejecutable.

```bash
g++ archivo.o archivo2.o archivo3.o -o ejecutable
```

# Ejercicio

Compila el repositorio de [init-files](https://github.com/Thgear27/init-files)

# Variables y estructuras de control

Esto ya lo sabes, pero lo vamos a repasar de todas formas.

## Variables

Las variables son espacios de memoria que se utilizan para almacenar valores, estas pueden ser de diferentes tipos, como enteros, flotantes, caracteres, entre otros.

```cpp
int a = 10; // int es un tipo de dato entero
float b = 3.14; // float es un tipo de dato flotante
char c = 'a'; // char es un tipo de dato caracter
MyType d = MyType(); // MyType es un tipo de dato definido por el usuario
```

## Estructuras de control

Las estructuras de control son instrucciones que permiten controlar el flujo de un programa, las estructuras de control más comunes son:

- `if`: Si se cumple una condición, ejecuta un bloque de código
- `else`: Si no se cumple la condición del `if`, ejecuta un bloque de código
- `for`: Ejecuta un bloque de código un número determinado de veces
- `while`: Ejecuta un bloque de código mientras se cumpla una condición
- `do while`: Ejecuta un bloque de código al menos una vez y luego mientras se cumpla una condición

```cpp
if (a == 10) {
  // Si a es igual a 10, ejecuta este bloque de código
} else {
  // Si a no es igual a 10, ejecuta este bloque de código
}

for (int i = 0; i < 10; i++) {
  // Ejecuta este bloque de código 10 veces
}

while (a < 10) {
  // Ejecuta este bloque de código mientras a sea menor a 10
}

do {
  // Ejecuta este bloque de código al menos una vez
} while (a < 10);
```

# Dibujar un punto en la pantalla

El código base del repositorio ya está escrito, y es el siguiente:

```cpp
#include "tgaimage.h"

const TGAColor white = TGAColor(255, 255, 255, 255);
const TGAColor red   = TGAColor(255, 0,   0,   255);

int main(int argc, char** argv) {
	TGAImage image(100, 100, TGAImage::RGB);
	image.set(52, 41, red);
	image.flip_vertically(); // i want to have the origin at the left bottom corner of the image
	image.write_tga_file("output.tga");
	return 0;
}

```

# Algoritmo de Bresenham

Puedes ver este [PDF](https://www.ercankoclar.com/wp-content/uploads/2016/12/Bresenhams-Algorithm.pdf).

El algoritmo de Bresenham es un algoritmo que permite dibujar líneas en una pantalla de forma eficiente, este algoritmo es muy utilizado en gráficos 2D y 3D. El algoritmo de Bresenham es un algoritmo incremental, es decir, que calcula los píxeles de la línea uno a uno, en lugar de calcular todos los píxeles de la línea de una sola vez.

Para poder entender el algoritmo de Bresenham, primero necesitamos entender la ecuación de la recta. La ecuación de la recta es una ecuación que describe una línea en un plano, esta ecuación tiene la forma `y = mx + b`, donde `m` es la pendiente de la recta y `b` es la ordenada al origen.

El algoritmo de Bresenham se basa en la ecuación de la recta, pero en lugar de calcular los píxeles de la línea a partir de la ecuación de la recta, calcula los píxeles de la línea a partir de la pendiente de la recta.

```cpp
void line(int x0, int y0, int x1, int y1, TGAImage &img,
          const TGAColor &color) {
  bool inverted_plane = false;
  if (std::abs(y1 - y0) >
      std::abs(x1 - x0)) { // Triangulo con pendiente mayor a 1
    std::swap(x0, y0);
    std::swap(x1, y1);
    inverted_plane = true;
  }

  if (x0 > x1) {
    std::swap(x1, x0);
    std::swap(y1, y0);
  }

  // Bresenham's algorithm
  int dx = x1 - x0;
  int dy = y1 - y0;
  int dxe = std::abs(dy) - std::abs(dx);
  int y = y0; // punto inicial que ira aumentando
  for (int x = x0; x <= x1; x++) {
    if (!inverted_plane)
      img.set(x, y, color);
    else
      img.set(y, x, color);

    dxe += std::abs(dy);

    if (dxe > 0) {
      dxe -= dx;
      y += (y1 > y0) ? 1 : -1;
    }
  }
}
```

```bash
convert output.tga output.png
```

# Dibujar un modelo 3D

Incluye los siguientes archivos en tu proyecto:

Archivo: "model.h"

```cpp
#ifndef __MODEL_H__
#define __MODEL_H__

#include <vector>
#include "geometry.h"

class Model {
private:
	std::vector<Vec3f> verts_;
	std::vector<std::vector<int> > faces_;
public:
	Model(const char *filename);
	~Model();
	int nverts();
	int nfaces();
	Vec3f vert(int i);
	std::vector<int> face(int idx);
};

#endif //__MODEL_H__
```

Archivo: "model.cpp"

```cpp
#include <iostream>
#include <string>
#include <fstream>
#include <sstream>
#include <vector>
#include "model.h"

Model::Model(const char *filename) : verts_(), faces_() {
    std::ifstream in;
    in.open (filename, std::ifstream::in);
    if (in.fail()) return;
    std::string line;
    while (!in.eof()) {
        std::getline(in, line);
        std::istringstream iss(line.c_str());
        char trash;
        if (!line.compare(0, 2, "v ")) {
            iss >> trash;
            Vec3f v;
            for (int i=0;i<3;i++) iss >> v.raw[i];
            verts_.push_back(v);
        } else if (!line.compare(0, 2, "f ")) {
            std::vector<int> f;
            int itrash, idx;
            iss >> trash;
            while (iss >> idx >> trash >> itrash >> trash >> itrash) {
                idx--; // in wavefront obj all indices start at 1, not zero
                f.push_back(idx);
            }
            faces_.push_back(f);
        }
    }
    std::cerr << "# v# " << verts_.size() << " f# "  << faces_.size() << std::endl;
}

Model::~Model() {
}

int Model::nverts() {
    return (int)verts_.size();
}

int Model::nfaces() {
    return (int)faces_.size();
}

std::vector<int> Model::face(int idx) {
    return faces_[idx];
}

Vec3f Model::vert(int i) {
    return verts_[i];
}
```

Archivo: "geometry.h"

```cpp
#ifndef __GEOMETRY_H__
#define __GEOMETRY_H__

#include <cmath>

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

template <class t> struct Vec2 {
	union {
		struct {t u, v;};
		struct {t x, y;};
		t raw[2];
	};
	Vec2() : u(0), v(0) {}
	Vec2(t _u, t _v) : u(_u),v(_v) {}
	inline Vec2<t> operator +(const Vec2<t> &V) const { return Vec2<t>(u+V.u, v+V.v); }
	inline Vec2<t> operator -(const Vec2<t> &V) const { return Vec2<t>(u-V.u, v-V.v); }
	inline Vec2<t> operator *(float f)          const { return Vec2<t>(u*f, v*f); }
	template <class > friend std::ostream& operator<<(std::ostream& s, Vec2<t>& v);
};

template <class t> struct Vec3 {
	union {
		struct {t x, y, z;};
		struct { t ivert, iuv, inorm; };
		t raw[3];
	};
	Vec3() : x(0), y(0), z(0) {}
	Vec3(t _x, t _y, t _z) : x(_x),y(_y),z(_z) {}
	inline Vec3<t> operator ^(const Vec3<t> &v) const { return Vec3<t>(y*v.z-z*v.y, z*v.x-x*v.z, x*v.y-y*v.x); }
	inline Vec3<t> operator +(const Vec3<t> &v) const { return Vec3<t>(x+v.x, y+v.y, z+v.z); }
	inline Vec3<t> operator -(const Vec3<t> &v) const { return Vec3<t>(x-v.x, y-v.y, z-v.z); }
	inline Vec3<t> operator *(float f)          const { return Vec3<t>(x*f, y*f, z*f); }
	inline t       operator *(const Vec3<t> &v) const { return x*v.x + y*v.y + z*v.z; }
	float norm () const { return std::sqrt(x*x+y*y+z*z); }
	Vec3<t> & normalize(t l=1) { *this = (*this)*(l/norm()); return *this; }
	template <class > friend std::ostream& operator<<(std::ostream& s, Vec3<t>& v);
};

typedef Vec2<float> Vec2f;
typedef Vec2<int>   Vec2i;
typedef Vec3<float> Vec3f;
typedef Vec3<int>   Vec3i;

template <class t> std::ostream& operator<<(std::ostream& s, Vec2<t>& v) {
	s << "(" << v.x << ", " << v.y << ")\n";
	return s;
}

template <class t> std::ostream& operator<<(std::ostream& s, Vec3<t>& v) {
	s << "(" << v.x << ", " << v.y << ", " << v.z << ")\n";
	return s;
}

#endif //__GEOMETRY_H__
```

Nuestro archivo main.cpp se verá de la siguiente manera:

```cpp
#include "model.h"
#include "tgaimage.h"

const TGAColor white = TGAColor(255, 255, 255, 255);
const TGAColor red = TGAColor(255, 0, 0, 255);

void line(int x0, int y0, int x1, int y1, TGAImage &img,
          const TGAColor &color) {
  bool inverted_plane = false;
  if (std::abs(y1 - y0) >
      std::abs(x1 - x0)) { // Triangulo con pendiente mayor a 1
    std::swap(x0, y0);
    std::swap(x1, y1);
    inverted_plane = true;
  }

  if (x0 > x1) {
    std::swap(x1, x0);
    std::swap(y1, y0);
  }

  // Bresenham's algorithm
  int dx = x1 - x0;
  int dy = y1 - y0;
  int dxe = std::abs(dy) - std::abs(dx);
  int y = y0; // punto inicial que ira aumentando
  for (int x = x0; x <= x1; x++) {
    if (!inverted_plane)
      img.set(x, y, color);
    else
      img.set(y, x, color);

    dxe += std::abs(dy);

    if (dxe > 0) {
      dxe -= dx;
      y += (y1 > y0) ? 1 : -1;
    }
  }
}

int main(int argc, char **argv) {
  Model *model = new Model("head.obj");
  const int width = 1000;
  const int height = 1000;

  TGAImage image(width, height, TGAImage::RGB);

  for (int i = 0; i < model->nfaces(); i++) {
    std::vector<int> face = model->face(i);
    for (int j = 0; j < 3; j++) {
      Vec3f v0 = model->vert(face[j]);
      Vec3f v1 = model->vert(face[(j + 1) % 3]);
      int x0 = (v0.x + 1.) * width / 2.;
      int y0 = (v0.y + 1.) * height / 2.;
      int x1 = (v1.x + 1.) * width / 2.;
      int y1 = (v1.y + 1.) * height / 2.;
      line(x0, y0, x1, y1, image, white);
    }
  }

  image.flip_vertically();
  image.write_tga_file("output.tga");
  return 0;
}
```
