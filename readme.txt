apt-get install libsndfile1-dev
# for vst3 support
apt-get install libxcb-util-dev libxcb-cursor-dev libxcb-keysyms1-dev libxcb-xkb-dev libxkbcommon-dev libxcb-xkb-dev libxkbcommon-x11-dev libcairo2-dev
git submodule update --init --recursive
patch -p1 < /compile/doc/sfizz/add-arm-vst-support.patch
mkdir build
cd build
# no vst support
#cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_LTO=OFF -DSFIZZ_JACK=ON -DSFIZZ_VST=OFF -DSFIZZ_TESTS=OFF -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_LIBSNDFILE=ON ..
# vst support
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_LTO=OFF -DSFIZZ_JACK=ON -DSFIZZ_VST=ON -DSFIZZ_TESTS=OFF -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_LIBSNDFILE=ON ..
patch -p1 < /compile/doc/sfizz/vstgui.patch 
make
