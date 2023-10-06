pkgdesc="ROS - Assorted filters designed to operate on 2D planar laser scanners, which use the sensor_msgs/LaserScan type."
url='https://wiki.ros.org/laser_filters'

pkgname='ros-noetic-laser-filters'
pkgver='1.9.0'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=3
license=('BSD')

ros_makedepends=(
    ros-noetic-catkin
    ros-noetic-dynamic-reconfigure
    ros-noetic-sensor-msgs
    ros-noetic-tf
    ros-noetic-filters
    ros-noetic-message-filters
    ros-noetic-laser-geometry
    ros-noetic-pluginlib
    ros-noetic-rostest
    ros-noetic-angles
    ros-noetic-nodelet
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-dynamic-reconfigure
    ros-noetic-sensor-msgs
    ros-noetic-roscpp
    ros-noetic-tf
    ros-noetic-filters
    ros-noetic-message-filters
    ros-noetic-laser-geometry
    ros-noetic-pluginlib
    ros-noetic-angles
    ros-noetic-nodelet
)

depends=(
    ${ros_depends[@]}
)

_dir="laser_filters-${pkgver}"
source=(
    "${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-perception/laser_filters/archive/${pkgver}.tar.gz"
    "eigen.patch"
    "sync.patch"
)
sha256sums=(
    'e9e58f4e6e22717973e4a187e1472c5b6d11247b96e03f8080f339e0077e37b8'
    '30b3e241d81cf4435b6428a0dc6e81e30fd5a69588a71eb423d69f0b0e843de7'
    '9e622f2d04204cec6fa1b8051ea83d3c41b47cb3a8e3a038504022e81c704b05'
)

prepare() {
    cd ${srcdir}/${_dir}
    patch -p1 -i ${srcdir}/sync.patch
    patch -p1 -i ${srcdir}/eigen.patch
}

build() {
    # Use ROS environment variables.
    source /usr/share/ros-build-tools/clear-ros-env.sh
    [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

    # Create the build directory.
    [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
    cd ${srcdir}/build

    # Build the project.
    cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
}

package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
}
