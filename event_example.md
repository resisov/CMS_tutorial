## 간단한 이벤트 생성을 해보자!

다음의 과정은 매드그래프로 양성자-양성자 충돌 후 w- 보존이 생성되며 w- 보존이 전자와 전자중성미자로 붕괴하는 과정을 생성한 것이다.

```bash
cd MG5_aMC_v2_8_1
./bin/mg5_aMC
generate p p > w- > e- ve~
output this_is_my_first
launch
0
0
```

잘 생성될것이다! 그렇지 않다면 옆자리에 도움을 요청하라!

다음 단계로 넘어가자! 이 과정은 생성된 이벤트 샘플 *.lhe의 압축을 푸는 과정이다.

```bash
quit
cd this_is_my_first/Events/run_01/
gzip -d unweighted_events.lhe.gz
```

이번에는 생성된 이벤트 샘플에 hadronization과 parton shower를 해주고, 검출기 효과를 적용해주는 DelphesPythia8에 인터페이스 하는 과정이다.

여기서부터는 CMSSW_9 버전을 활용하자!

먼저 피시아 카드를 너의 샘플에 맞게 수정해보자!
```bash
cd /home/twkim/Delphes3.4.2/examples/Pythia8
vi configLHE.cmnd
```

그러면 이런 창이 나올것이다.

```bash
! 1) Settings used in the main program.

Main:numberOfEvents = 100         ! 이 부분을 10000개로 바꾸자!
Main:timesAllowErrors = 3          ! how many aborts before run stops

! 2) Settings related to output in init(), next() and stat().

Init:showChangedSettings = on      ! list changed settings
Init:showChangedParticleData = off ! list changed particle data
Next:numberCount = 100             ! print message every n events
Next:numberShowInfo = 1            ! print event information n times
Next:numberShowProcess = 1         ! print process record n times
Next:numberShowEvent = 0           ! print event record n times

! 3) Set the input LHE file

Beams:frameType = 4
## 이 부분도 바꿔줘라! 너의 이벤트가 있는 경로로! 아래와 같이!
Beams:LHEF = /home/당신의아이디/MG5_aMC_v2_8_1/this_is_my_first/Events/run_01/unweighted_events.lhe
```

델피스 디렉토리로 돌아오자! 그 후 작동해보자!

```bash
cd /home/당신의아이디/Delphes3.4.2
./DelphesPythia8 cards/delphes_card_CMS.tcl examples/Pythia8/configLHE.cmnd wow_particle_physics.root
```

와! 이제 모든 과정이 완료되었다. 루트(*.root) 파일을 구경해보자!

```bash
root wow_particle_physics.root
TBrowser b;
```

신기하다! 옆자리의 선배에게 궁금한것을 물어보자!
