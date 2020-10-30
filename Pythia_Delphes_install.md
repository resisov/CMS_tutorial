## 피시아와 델피스 설치

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
wget http://home.thep.lu.se/~torbjorn/pythia8/pythia8223.tgz
tar xzvf pythia8223.tgz
cd pythia8223
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
make -j 4
```
## 피시아 버전 낫매칭 오류
 PYTHIA Abort from Pythia::Pythia: unmatched version numbers : in code 8.235 but in XML 8.223
** ERROR: can't read Pythia8 configuration file examples/Pythia8/configLHE.cmnd
델피스는 피시아 버전에 민감하다! 반드시 8.223 버전으로 깔아야한다!

## 컴파일러 오류
gcc 버전문제로 오류가 발생할 수 있다. 오류 메세지에 c++ 이 들어있다면 gcc 버전이 530으로 세팅된 CMSSW를 사용하라!


3. 델피스피시아8
```
## 피시아와 델피스를 합치기 위해 아래의 항을 따라하세요. (델피스 디렉토리에서!)
## "당신의아이디"부분을 바꿔주세요. ex. twkim or jyshin or taebh etc....

export PYTHIA8=/home/"당신의아이디"/pythia8223/
export LD_LIBRARY_PATH=$PYTHIA8/lib:$LD_LIBRARY_PATH
make -j 4 HAS_PYTHIA8=true DelphesPythia8
