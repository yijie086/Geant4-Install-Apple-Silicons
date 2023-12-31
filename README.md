# Geant4-Install-Apple-Silicons
Describe how to install Geant4 on a Mac with Apple Silicons.

# Manual Installation of Geant4 on a Mac with Apple Silicons

The following steps have been tested with a Mac Studio (M2 Max Chip, macOS 13.5.2), for Geant4 11.1.0.
And the main reference is [Manual installation on macOS (with M series chip)](http://geant4-dna.in2p3.fr/styled-6/styled-12/index.html) 


## Dependences



#### Install `Homebrew`

#### Install `Xcode` from `App Store`.

#### Install `Xcode command line tools`

```
xcode-select --install
```

#### Install `CMake`

```
brew install cmake
```

#### Install `Qt@5`

```
brew install qt@5
```

#### Define `PKG_CONFIG_PATH`

**First, check the path of `qt@5` :**

The path of  `qt@5` looks like this:

```
/opt/homebrew/Cellar/qt@5/5.15.10_1/lib/
```

**Define environment variables**

Please make sure you have type in the right version number of `qt@5`. The version number may change:

```
export PKG_CONFIG_PATH=/opt/homebrew/Cellar/qt@5/<YOUR VERSION NUMBER>/lib/pkgconfig/
export PATH=/opt/homebrew/Cellar/qt@5/<YOUR VERSION NUMBER>/bin:$PATH
```

#### Install the `Xerces-C++`

```
brew install xerces-c
```

#### Install the `ROOT6`

```
brew install root
```



## Installation



#### Download `Geant4` using `git`

```
cd
git clone https://gitlab.cern.ch/geant4/geant4.git
cd geant4
git checkout v11.1.0
cd ..
```

#### Create a `build` directory

```
cd
cd geant4
mkdir build
cd build
```

#### Run `CMake`

`/Users/<YOUR USER NAME>` is the `home` directory from which any terminal session starts. 

```
cmake -S /Users/<YOUR USER NAME>/geant4 -DCMAKE_INSTALL_PREFIX=/Users/<YOUR USER NAME>/geant4-v11.1.0-install -DCMAKE_BUILD_TYPE=RelWithDebInfo -DGEANT4_USE_GDML=ON -DGEANT4_BUILD_MULTITHREADED=ON -DXERCESC_ROOT_DIR=/opt/homebrew/Cellar/xerces-c/<YOUR VERSION NUMBER> -DGEANT4_USE_QT=ON -DGEANT4_INSTALL_EXAMPLES=ON -DGEANT4_INSTALL_DATA=ON -DGEANT4_USE_SYSTEM_EXPAT=OFF -DGEANT4_BUILD_TLS_MODEL=auto ../geant4
```

#### Run the build with 8 cores

```
cmake --build . --target install -- -j8
```

#### Source `geant4.sh`

```
source ~/geant4-v11.1.0-install/bin/geant4.sh
```

To avoid doing this everytime, you can add it to `~/.zshrc`:

```
vi ~/.zshrc
```

and add a line:
```
source ~/geant4-v11.1.0-install/bin/geant4.sh
```

Now, you have installed `Geant4`.



## Run Test

#### Change the environment variables

```
export G4NEUTRONHPDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4NDL4.7
export G4LEDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4EMLOW8.2
export G4LEVELGAMMADATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/PhotonEvaporation5.7
export G4RADIOACTIVEDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/RadioactiveDecay5.6
export G4PARTICLEXSDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4PARTICLEXS4.0
export G4PIIDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4PII1.3
export G4REALSURFACEDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/RealSurface2.2
export G4SAIDXSDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4SAIDDATA2.0
export G4ABLADATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4ABLA3.1
export G4INCLDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4INCL1.0
export G4ENSDFSTATEDATA=/Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/data/G4ENSDFSTATE2.3
```
#### Copy the `B1` Example
```
cp -r /Users/<YOUR USER NAME>/geant4-v11.1.0-install/share/Geant4/examples/basic/B1 /Users/<YOUR USER NAME>/Downloads
cd /Users/<YOUR USER NAME>/Downloads/B1
```
#### `Make` the `B1` Example
```
cmake .
make -f Makefile
```
#### Run the `B1` Example
```
./exampleB1
```

#### Type in the session:

```
/run/beamOn 100
```

