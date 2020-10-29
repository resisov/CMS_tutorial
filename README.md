# CMS_tutorial
CCP서버와 CMS 소프트웨어를 활용한 입자물리학 입문자를 위한 튜토리얼

1. 사용가능한 gcc 컴파일러 버전 확인
```bash
ls /cvmfs/cms.cern.ch
```

2. SCRAM ARCH 셋팅 ## vi cmsset으로 새 파일을 아래와 같이 작성하세요.
```bash
export SCRAM_ARCH=slc7_amd64_gcc700
export VO_CMS_SW_DIR=/cvmfs/cms.cern.ch
echo "$VO_CMS_SW_DIR $SCRAM_ARCH"
source $VO_CMS_SW_DIR/cmsset_default.sh
export SSL_CERT_DIR='/etc/grid-security/certificates'
```

3. CMSSW 버전 확인
```bash
scram list
```

4. CMSSW 설치 (v10.2.23)
```bash
cmsrel CMSSW_10_2_23
```

5. 환경 셋업
```bash
cd CMSSW_10_2_23/src
cmsenv
cd
```
다음단계로 넘어간다 >> MADGRAPH 설치
