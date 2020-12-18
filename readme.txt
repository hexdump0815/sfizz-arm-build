apt-get install libsndfile1-dev libxcb-util-dev libxcb-cursor-dev libxcb-keysyms1-dev libxcb-xkb-dev libxkbcommon-dev libxcb-xkb-dev libxkbcommon-x11-dev libcairo2-dev cmake libjack-jackd2-dev
git clone https://github.com/sfztools/sfizz.git
cd sfizz
git checkout 0.5.1
git submodule update --init --recursive
# on master now the patch seems to be no longer required
#patch -p1 < /compile/doc/sfizz/vstgui.patch 
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_LTO=OFF -DSFIZZ_JACK=ON -DSFIZZ_VST=ON -DSFIZZ_TESTS=OFF -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_LIBSNDFILE=ON ..
make
# make install works quite well
make install
#rm -rf /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render
#cp -r sfizz.lv2 /usr/local/lib/lv2
#cp -r sfizz.vst3 /usr/local/lib/vst3
#cp clients/sfizz_jack /usr/local/bin
# tar czf /tmp/sfizz-0.5.1.armv7l.tar.gz /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render
# tar czf /tmp/sfizz-0.5.1.aarch64.tar.gz /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render
# tar czf /tmp/sfizz-0.5.1.x86_64.tar.gz /usr/local/lib/lv2/sfizz.lv2 /usr/local/lib/vst3/sfizz.vst3 /usr/local/bin/sfizz_jack /usr/local/bin/sfizz_render

# side note: building on macos - the pages below seem to not be up to date
# see https://sfz.tools/sfizz/development/build/
# see https://sfz.tools/sfizz/development/build/macos
brew install cmake pkgconfig libsndfile
git clone https://github.com/sfztools/sfizz.git
cd sfizz
git checkout 0.5.1
git submodule update --init --recursive
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_STANDARD=14 -DSFIZZ_JACK=OFF -DSFIZZ_RENDER=OFF -DSFIZZ_LV2=OFF -DSFIZZ_LV2_UI=OFF -DSFIZZ_VST=ON -DSFIZZ_AU=ON -DSFIZZ_SHARED=OFF -DSFIZZ_STATIC_DEPENDENCIES=ON
# in the end it fails due to problems with the AudioToolbox framework - maybe my too old dev setup ...
