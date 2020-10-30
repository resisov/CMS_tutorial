피시아와 델피스 설치

이놈은 CMSSW 10_x 버전이 안먹힌다. CMSSW_9_x 버전을 새로 깔자.

0.1. SCRAM ACRH 
```bash
##vi로 다음의 항을 입력하여 새로 저장하세요. ex. cmsset_9
export SCRAM_ARCH=slc6_amd64_gcc630
export VO_CMS_SW_DIR=/cvmfs/cms.cern.ch
echo "$VO_CMS_SW_DIR $SCRAM_ARCH"
source $VO_CMS_SW_DIR/cmsset_default.sh
export SSL_CERT_DIR='/etc/grid-security/certificates'
```
0.2 cmsset
```bash
source cmsset_9
```
0.3 CMSSW_9 설치 및 환경 돌입
```bash
cmsrel CMSSW_9_1_0_pre3
cd CMSSW_9_1_0_pre3/src/
cmsenv
cd
```

이제 피시아와 델피스를 설치할 준비가 끝났다.

1. 피시아 설치
```bash
wget http://home.thep.lu.se/~torbjorn/pythia8/pythia8235.tgz
tar xzvf pythia8235.tgz
cd pythia8235
./configure
make install
```

2. 델피스 설치
```bash
git clone git://github.com/delphes/delphes.git Delphes3.4.2
cd Delphes3.4.2
git checkout tags/3.4.2pre15
./configure
sed -i -e 's/c++0x/c++1y/g' Makefile

## 피시아와 델피스를 합치기 위해 아래의 항을 따라하세요. (델피스 디렉토리에서!)
## "당신의아이디"부분을 바꿔주세요. ex. twkim or jyshin or taebh etc....

export PYTHIA8=/home/"당신의아이디"/pythia8235/
export LD_LIBRARY_PATH=$PYTHIA8/lib:$LD_LIBRARY_PATH
make -j 4 HAS_PYTHIA8=true DelphesPythia8
