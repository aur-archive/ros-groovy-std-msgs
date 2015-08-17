pkgdesc="ROS - Standard ROS Messages."
url='http://www.ros.org/'

pkgname='ros-groovy-std-msgs'
pkgver='0.5.7'
arch=('i686' 'x86_64')
pkgrel=2
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-langs-dev
  ros-groovy-catkin
  ros-groovy-message-generation
  ros-groovy-message-runtime
  ros-groovy-langs)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/std_msgs ]; then
    cd ${srcdir}/std_msgs
    git fetch origin --tags
    git reset --hard release/std_msgs/${pkgver}
  else
    git clone -b release/std_msgs/${pkgver} git://github.com/ros-gbp/std_msgs-release.git ${srcdir}/std_msgs
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/std_msgs
  cmake ${srcdir}/std_msgs -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
