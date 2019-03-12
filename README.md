Install Triton on Ubuntu 18.04

# install kernel 3.x
Download from kernel.ubuntu.com/~kernel-ppa/mainline/  
Download headers and images debs in one directory, eg 3.16.36Trusty  
/debDirectory/sudo dpkg -i *.deb  
Change kernel from grub(hold shift key when startup)  

# install required libs
sudo apt-get install libboost-all-dev  
sudo apt-get install python-dev  
sudo apt-get install libcapstone-dev  

# install z3
git clone http://github.com/Z3Prover/z3.git  
cd z3  
python scripts/mk_make.py --python  
cd  

# install Pin
wget 'https://software.intel.com/sites/landingpage/pintool/downloads/pin-2.14-71313-gcc.4.4.7-linux.tar.gz'  
tar xzf pin-2.14-71313-gcc.4.4.7-linux.tar.gz  

# install Triton
cd pin-2.14-71313-gcc.4.4.7-linux/source/tools  
git clone https://github.com/JonathanSalwan/Triton.git  
cd Triton  
mkdir build  
cd build  
cmake -DPINTOOL=on ..  
make  

# have to make the following change to make Pin work
sudo sysctl kernel.yama.ptrace_scope=0  
