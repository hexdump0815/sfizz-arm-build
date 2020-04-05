apt-get install libsndfile1-dev libxcb-util-dev libxcb-cursor-dev libxcb-keysyms1-dev libxcb-xkb-dev libxkbcommon-dev libxcb-xkb-dev libxkbcommon-x11-dev libcairo2-dev
git clone https://github.com/sfztools/sfizz.git
cd sfizz
git checkout 0.3.2
git submodule update --init --recursive
patch -p1 < /compile/doc/sfizz/vstgui.patch 
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_LTO=OFF -DSFIZZ_JACK=ON -DSFIZZ_VST=ON -DSFIZZ_TESTS=OFF -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_LIBSNDFILE=ON ..
make
