FROM archlinux
RUN pacman --needed --noconfirm -Sy archlinux-keyring
RUN pacman --needed --noconfirm -Sy base base-devel git reflector

# multilib
RUN echo -e "\n[multilib]\nInclude = /etc/pacman.d/mirrorlist" >> /etc/pacman.conf

# new mirrors
RUN reflector --save /etc/pacman.d/mirrorlist --sort rate --age 1 --latest 10 --score 10 --number 5 --protocol http
RUN pacman --noconfirm -Syu

# Add non-root user
RUN useradd -m -r -s /bin/bash archlinux
RUN echo 'archlinux ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

# Switch user and cwd
USER archlinux
WORKDIR /home/archlinux

# Install yay for AUR managment
RUN git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si --noconfirm
RUN rm -rf yay

## Basic mingw-w64 toolchain

# Bootstrap GCC
RUN yay --noconfirm -S mingw-w64-gcc-base

# Bootstrap Windows Libs
RUN yay --noconfirm -S mingw-w64-crt
RUN yay --noconfirm -Rdd mingw-w64-headers-bootstrap
RUN yay --noconfirm -S mingw-w64-winpthreads
RUN yay --noconfirm -Rdd mingw-w64-gcc-base

# Build proper GCC
RUN yay --noconfirm -S mingw-w64-gcc

# Rebuild previous boostrapped libs
RUN yay --noconfirm --rebuild -S mingw-w64-crt
RUN yay --noconfirm --rebuild -S mingw-w64-winpthreads

# Clear yay cache
RUN rm -rf .cache/yay
