# CMS_tutorial

X section 비교

inclusive한 암흑물질 생성 프로세스와 강제적 생성프로세스 간 산란단면적 비교

1. CMSSET
```bash
source cmsset
cd CMSSW_니_버전/src
cmsenv
cd
```

2. Launch MG5_aMC
```bash
cd MG5_니버전
./bin/mg5_aMC
```

3. inclusive sample
```bash
import model DMsimp_UFO
generate p p > t t~ xd xd~ / y1 [QCD]
output xd_inclusive
launch

3
0
0
```
생성이 끝난 후 화면에 나오는 산란단면적을 기록

4. 강제빵
```bash
import model DMsimp_UFO
generate p p > t t~ y0 [QCD]
output xd_gang
launch

3
3
## decay z > all all 밑에 다음을 추가
decay y0 > xd xd~
:wq

0
```
생성이 끝난 후 화면에 나오는 산란단면적을 기록 후 3과 4의 결과를 비교

