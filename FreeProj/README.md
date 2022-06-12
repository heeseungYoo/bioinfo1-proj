# 생물정보학 및 실습1 Free Project 
# Title - Identification of LIN28A binding motif
## Introduction 
Crosslinking-Induced Errors Allow Identification of LIN28A Binding Sites at Single-Nucleotide Resolution
RNA-protein interaction을 찾기 위해서 CLIP-seq을 진행하게 되는데 이때 UV cross-linking단계에서 UV광선에 의해 binding sites에서 substitution과 deletion이 많이 일어나게 된다. 따라서 시퀀싱 결과에서 substitution, deletion이 많이 일어난 위치를 찾으면 Lin28A binding site를 찾을 수 있을 것이다. 
## Fig S3C 그려보기 
### pipeline
1. Substitution이 많이 일어난 position을 찾기 위해 전체 Genome에 대해서 pileup 한다. 
2. Depth 50이상으로 filtering한다. 
3. Baseread에서 Match와 Substitution만 남기고 제거한다. 
4. Shannon's entropy를 계산한 후 1.0 이상으로 Filtering한다. 
5. genome reference에서 binding position 주위 sequence를 추출한다.
  (-) strand에 cross-linked된 read 주의해서 가져온다. 
6. 가져온 sequence를 Weblogo에 그려보고 결과를 확인한다. 
### result 
<p>binding position 0에서 Guanine이 우세하게 나온 것을 확인</p> 
<p>(-2,4) 구간에서 AAGNGG pattern 확인</p> 
## LIN28A-bound sequence frequency 구하기 
FigureS3C의 결과로 binding position의 (-2,4)에 해당하는 sequenc가 binding motif일 확률이 높기 때문에 hexamer로 범위를 좁혀 binding motif를 찾아본다. 
### pipeline
1. 위와 동일한 방식으로 hexamer와 flanking hexamer를 추출한다. 
2. hexamer와 flanking hexamer의 빈도를 확인 해본다. 
### result 
<p>Hexamer의 경우 AAGNNG, AAGNGN 두 가지 pattern이 Top 10에 rank된 것을 확인</p>
<p>Flanking hexamer는 Top 10 sequence들 전부 각 position에 대해 complementary하다는 것을 확인</p>
## Step 3: Figure 2E 그려보기 
Flanking hexamer에서 양 쪽이 complementary하다는 것을 발견했기 때문에 전체 sequence에 대해서 Watson Crick pair 정도를 조사해서 2차 구조 선호도에 대해 조사한다. Hexamer의 분포에서 AAGNHG, AAGNGH 두 pattern으로 나뉘어 있는 것을 확인했으므로 두 Group으로 나누어 조사해본다.
### pipeline
1. AAGNHG에 해당하는 sequence만 모은다. 
2. binding position을 포함하는 30bp sequence에 대해서 각 position별로 complement한 sequence의 개수를 구한다. 
3. frequency에 대해서 heatmap을 그린다. 
4. 동일한 방법으로 AAGNGH에 대해서도 진행한다. 
### result 
binding position을 (0,0)으로 놓았을 때 (-3,4)에서 frequency가 가장 높고 한 칸씩 멀어지는 구간에서 frequency가 다른 지역에 비해 높게 나오는 것으로 보아 hairpin 구조를 이루는 것을 예상해 볼 수 있다. 
