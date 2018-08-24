Repositorio para provisionar los servidores para despliegue de la plataforma de Kubernetes.

## Prerequisites

[Vagrant](http://www.vagrantup.com/) (minimum version 1.6)
[Vagrant-esxi plugin]
[Ovftools]


## Descargar del repo
Este repo usa git submodules.

Para hacer el clone, usa la opción --recurse-submodules. 
This repo uses git submodules. 

    git clone --recurse-submodules  https://github.com/miguelangelfalcon/vagrant-esxi-nodes.git

Si necesitas hacer un pull con los últimos cambios debes usar : 

     git pull --recurse-submodules
     git submodule update --init --recursive

## Up and SSH

Para levantar la plataforma : 

    vagrant up --provider=vmware_esxi --provision

Para hacer el login en un nodo:

    vagrant ssh <nodo>


### Kubernetes

La instalación del kubernetes se tiene que realizar con kubespray

Para generar el inventario debes lanzar el script 

```bash

 python vagrant2ansible.py

```

Una vez obtenidos los datos de los nodos creados, debemos añadirlos al inventario.