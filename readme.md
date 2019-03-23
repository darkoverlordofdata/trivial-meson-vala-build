# Trivial build template 

build vala with meson

using code from the tutorial at:
https://aztlan.fciencias.unam.mx/~canek/building-vala-applications/


### build

    meson build --prefix=/usr
    cd build
    ninja
    sudo ninja install

