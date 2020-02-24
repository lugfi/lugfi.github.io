# Sitio web LUGFI

Repositorio del sitio y blog del LUGFI, que es alojado en
[https://lugfi.github.io](https://lugfi.github.io).

## ¿Cómo contribuyo?

1. Clonar el repositorio con alguno de los siguiente métodos:
   * HTTPS: `git clone https://github.com/LUGFi/lugfi.github.io.git`
   * SSH: `git clone git@github.com:LUGFi/lugfi.github.io.git`
1. Crear una nueva rama. Por ejemplo, `git checkout -b miusuario/mipost`.
1. Realizar los cambios. Por ejemplo, agregar un post en la carpeta `_posts`.
1. Hacer un _push_ al repositorio. Siguiendo el ejemplo anterior,
   `git push -u origin miusuario/mipost`.
1. Crear un _pull request_ a través de GitHub.

## ¿Cómo lo pruebo localmente?

1. Verificar si se encuentra instalado Ruby 2.0.0 o superior con el comando
   `ruby --version`.
1. Instalar Bundler con el comando `gem install bundler`.
   Omitir este paso si ya se encuentra instalado.
1. Instalar Jekyll y sus dependencias con el comando `bundle install`.
   Omitir este paso si ya se realizó la instalación previamente.
1. Correr Jekyll localmente con el comando `bundle exec jekyll serve`.
1. Ingresar al sitio desde `http://localhost:4000`.
