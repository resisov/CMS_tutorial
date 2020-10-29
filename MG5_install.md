이벤트 제너레이터 매드그래프 5 설치

1. 홈 디렉토리에 압축파일을 받아온다.
```bash
wget https://launchpad.net/mg5amcnlo/2.0/2.8.x/+download/MG5_aMC_v2.8.1.tar.gz
```
2. 압축 해제
```bash
tar -xvzf MG5_aMC_v2.8.1.tar.gz
```
3. 실행과 서브 모듈 설치
```bash
cd MG5_aMC_v2_8_1
./bin/mg5_aMC

## MG5 환경 돌입
install ExRootAnalysis
install lhapdf6
quit
```

4. 간단한 이벤트 생성
```bash
./bin/mg5_aMC
generate p p > t t~
output test
launch
0
0
```
잘 생성된다!
다음 단계로 넘어간다 >> 피시아, 델피스 설치
-(Pythia_Delphes_install.md) [https://github.com/resisov/CMS_tutorial/blob/main/Pythia_Delphes_install.md]
