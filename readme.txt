apt-get install libsndfile1-dev libxcb-util-dev libxcb-cursor-dev libxcb-keysyms1-dev libxcb-xkb-dev libxkbcommon-dev libxcb-xkb-dev libxkbcommon-x11-dev libcairo2-dev
git clone https://github.com/sfztools/sfizz.git
cd sfizz
#git checkout 0.3.2
git submodule update --init --recursive
# on master now the patch seems to be no longer required
#patch -p1 < /compile/doc/sfizz/vstgui.patch 
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_LTO=OFF -DSFIZZ_JACK=ON -DSFIZZ_VST=ON -DSFIZZ_TESTS=OFF -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_LIBSNDFILE=ON ..
make
# make install works quite well
make install
#rm -rf /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack
#cp -r sfizz.lv2 /usr/local/lib/lv2
#cp -r sfizz.vst3 /usr/local/lib/vst3
#cp clients/sfizz_jack /usr/local/bin
# tar czf /tmp/sfizz-dev.armv7.tar.gz /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render /usr/local/lib/pkgconfig/sfizz.pc /usr/local/include/sfizz.hpp /usr/local/include/sfizz.h /usr/local/lib/libsfizz.a
# tar czf /tmp/sfizz-dev.aarch64.tar.gz /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render /usr/local/lib/pkgconfig/sfizz.pc /usr/local/include/sfizz.hpp /usr/local/include/sfizz.h /usr/local/lib/libsfizz.a
