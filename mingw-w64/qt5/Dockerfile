FROM atiltedtree/mingw-w64:base

RUN yay --noconfirm -Syu

RUN yay --noconfirm -S wine-staging

# Boostrap freetype2 and cairo
RUN yay --noconfirm -S mingw-w64-freetype2-bootstrap
RUN yay --noconfirm -S mingw-w64-cairo-bootstrap

# Install libs needing bootraps
RUN yay --noconfirm -S mingw-w64-harfbuzz
RUN yay --noconfirm -S mingw-w64-poppler
RUN yay --noconfirm -S mingw-w64-pango
RUN yay --noconfirm --provides mingw-w64-rust-bin -S mingw-w64-librsvg

# Remove previosly boostrapped libs
RUN yay --noconfirm -Rdd mingw-w64-cairo-bootstrap
RUN yay --noconfirm -Rdd mingw-w64-freetype2-bootstrap

# Build libs proper
RUN yay --noconfirm -S mingw-w64-freetype2
RUN yay --noconfirm --rebuild -S mingw-w64-fontconfig
RUN yay --noconfirm -S mingw-w64-cairo

# Rebuild libs that needed boostrap
RUN yay --noconfirm --rebuild -S mingw-w64-harfbuzz
RUN yay --noconfirm --rebuild -S mingw-w64-poppler
RUN yay --noconfirm --rebuild -S mingw-w64-pango
RUN yay --noconfirm --rebuild -S mingw-w64-librsvg

# Install actual qt5 libs
RUN yay --noconfirm -S mingw-w64-qt5-base
RUN yay --noconfirm -S mingw-w64-qt5-base-static

# Clear yay cache
RUN rm -rf .cache/yay
