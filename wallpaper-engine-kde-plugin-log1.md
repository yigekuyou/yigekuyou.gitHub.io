<services>
  <service name="tar_scm">
    <param name="scm">git</param>
    <param name="url">https://github.com/catsout/wallpaper-engine-kde-plugin.git</param>
    <param name="filename">wallpaper-engine-kde-plugin</param>
    <param name="revision">main</param>
    <param name="versionformat">%cd</param>
     <param name="version">_auto</param>
  </service>
  <service name="set_version" mode="buildtime"/>
</services>

Name:           wallpaper-engine-kde-plugin

Version:        0.1.git

Release:        0

Summary:        A kde wallpaper plugin integrating wallpaper engine

License:        GPL-2.0-only

URL:            https://github.com/catsout/wallpaper-engine-kde-plugin

Source:         %{name}-%{version}.tar

BuildRequires:  clang

BuildRequires:  libqt5-qtwebsockets-devel libqt5-qtx11extras-devel  libqt5-qtbase-private-headers-devel 

BuildRequires:  plasma-framework-devel plasma5-workspace-devel 

BuildRequires:  libqt5-qtx11extras-devel 

BuildRequires:  mpv-devel

BuildRequires:  liblz4-devel

BuildRequires:  vulkan-devel

BuildRequires:  libQt5Gui-private-headers-devel

Requires:       libvulkan1

Requires:       python3 >= 3.10 libvulkan1

BuildRoot:      %{_tmppath}/%{name}-%{version}-build

#BuildArch:      

%description
A wallpaper plugin integrating wallpaper engine into kde wallpaper setting.

%prep 

%setup -q

%build

cmake -B build -DUSE_PLASMAPKG=OFF -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING=OFF
cd build
%cmake_build

%install
%cmake_install

%files 

%defattr(-,root,root,-)

%doc README.md 

%license LICENSE
/usr/share/plasma/wallpapers/
/usr/lib64/qt5/qml/com/
/usr/share/kservices5/plasma-wallpaper-com.github.casout.wallpaperEngineKde.desktop
/usr/share/metainfo/com.github.casout.wallpaperEngineKde.appdata.xml
