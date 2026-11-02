# Part C. 염증 지표 → 알츠하이머병: Two-Sample Mendelian Randomization

> **류마티스관절염(RA) 연구 시리즈의 세 번째 분석**
> Part B에서 확인한 "RA–AD 연관은 HLA 다면발현 때문"이라는 결과를 이어받아, **두 질환을 잇는 공통 기전으로 흔히 거론되는 전신 염증이 AD의 원인인가**를 검증합니다.

## 프로젝트 흐름

| 파트 | 질문 | 데이터 · 방법 | 핵심 결과 |
|---|---|---|---|
| **Part A** | 한국인에서 RA와 관련된 요인은 무엇인가? | 국민건강영양조사(KNHANES), 관찰 분석 | RA 관련 위험요인 탐색 |
| **Part B** | 그 요인들은 RA의 *원인*인가? RA는 AD의 원인인가? | 2-sample MR (흡연·BMI → RA, RA·SLE → AD) | RA → AD 연관은 **HLA 영역 제외 시 소실** → 다면발현 |
| **Part C** (본 저장소) | 그렇다면 **염증 자체**는 AD의 원인인가? | 2-sample MR (CRP, IL6R cis, 사이토카인 → AD, 역방향 포함) | CRP → AD 연관은 **APOE 영역 제외 시 소실** → 다면발현 |

```
Part A  관찰 연관 (KNHANES)
   │    "RA와 함께 나타나는 요인은?"
   ▼
Part B  인과 검증 (MR)
   │    흡연·BMI → RA  /  RA·SLE → AD
   │    → RA–AD 연관은 HLA 다면발현이 주도
   ▼
Part C  기전 검증 (MR)  ◀ 이 저장소
        "공유 기전 후보인 전신 염증은 AD의 원인인가?"
        → 아니다. 처음 보인 연관은 APOE 다면발현
```

## 연구 질문

1. 유전적으로 높은 **CRP**는 AD 위험을 바꾸는가?
2. **IL-6 수용체 신호**를 낮추는 유전 변이(토실리주맙 효과 모사)는 AD 위험을 바꾸는가?
3. **개별 사이토카인**(IL-6, IL-1β, TNF-α, IL-18, MCP-1, MCP-3) 중 AD와 인과적으로 연결된 것이 있는가?
4. 거꾸로, **AD 소인이 CRP**를 바꾸는가? (역인과 점검)

## 핵심 결과

| 분석 | 주 추정치 (IVW) | 결론 |
|---|---|---|
| CRP → AD (APOE 포함, 51 SNP) | OR 0.40 (0.24–0.67), p = 4.6×10⁻⁴ | APOE 다면발현이 만든 연관 |
| **CRP → AD (APOE 제외, 49 SNP)** | **OR 1.00 (0.86–1.17), p = 0.97** | **유의한 인과 효과 없음** |
| MR-PRESSO 이상치 보정 (APOE 제외) | β = −0.005, p = 0.92 | 유의한 효과 없음 |
| IL6R cis-MR → AD (6 SNP) | OR 0.90 (0.70–1.16), p = 0.41 | 유의한 효과 없음 |
| 사이토카인 6종 → AD | 모두 FDR > 0.5 (최저 MCP-1, p = 0.086) | 검출되지 않음 (검정력 낮음) |
| 역방향 AD → CRP | IVW p = 0.97 / weighted median·mode에서 약한 음의 신호 | 약한 신호, 결론 보류 |

## Part B와 이어지는 해석

| | Part B: RA → AD | Part C: CRP → AD |
|---|---|---|
| 처음 결과 | 유의한 연관 | 유의한 연관 (보호 방향) |
| 문제 영역 | HLA (chr6) | APOE (chr19) |
| 영역 제외 후 | 연관 소실 | 연관 소실 (OR 1.00) |
| 의미 | RA라는 질환 자체가 AD 원인이라는 근거 약함 | 전신 염증 수치 자체가 AD 원인이라는 근거 없음 |

- 두 영역은 서로 다른 염색체에 있어 유전적으로 독립적입니다. 그런데도 두 분석은 **"효과가 큰 단일 영역이 노출과 결과에 동시에 작용해 가짜 인과 연관을 만든다"**는 같은 구조를 보였습니다.
- 따라서 RA와 AD를 잇는 면역 신호는 **혈중 염증 수치(CRP, 사이토카인)보다는 HLA·APOE처럼 뇌 면역세포(미세아교세포) 기능과 관련된 유전자 경로**에 있을 가능성이 상대적으로 높습니다. 이는 이번 분석에서 직접 검증한 것은 아니며, 후속 연구의 가설입니다.

자세한 결과와 그림은 https://velog.io/@lcm9903/%EC%97%B0%EA%B5%AC-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%97%BC%EC%A6%9D-%EC%A7%80%ED%91%9C%EC%99%80-%EC%95%8C%EC%B8%A0%ED%95%98%EC%9D%B4%EB%A8%B8%EB%B3%91-2-%ED%91%9C%EB%B3%B8-MR-Part-C 에 있습니다.

## 데이터 (OpenGWAS, GRCh37)

| 역할 | GWAS | ID | 표본 |
|---|---|---|---|
| 노출 | CRP — Ligthart 2018 (CHARGE) | `ieu-b-35` | 204,402 (유럽인) |
| 결과 | AD — Kunkle 2019 (IGAP) | `ieu-b-2` | 21,982 cases / 41,944 controls (유럽인) |
| 노출 | 사이토카인 — Ahola-Olli 2017 | `ebi-a-GCST004441`, `004446`, `004448`, `004426`, `004438`, `004437` | 843–8,293 (핀란드) |

- CRP와 AD GWAS 모두 UK Biobank를 포함하지 않아 표본 중복 편향을 피했습니다.
- 결과 GWAS는 Part B와 같은 AD GWAS(`ieu-b-2`)를 사용해 두 분석의 결과를 직접 비교할 수 있게 했습니다.

## 분석 방법

- **도구변수**: p < 5×10⁻⁸ (사이토카인은 p < 5×10⁻⁶), LD clumping r² < 0.001 / 10,000 kb, F ≥ 10
- **영역 제외 민감도 분석**: APOE 영역 chr19:44.4–46.5 Mb (Part B의 HLA 제외 분석과 같은 설계)
- **추정법**: IVW (주 분석), MR-Egger, Weighted median, Weighted mode
- **민감도 분석**: Cochran's Q, MR-Egger 절편, Leave-one-out, MR-PRESSO, Steiger 방향성
- **IL6R cis-MR**: IL6R ±300 kb 내 CRP 연관 변이, r² < 0.1 clumping
- **다중검정**: 사이토카인은 Benjamini–Hochberg FDR
- **역방향 MR**: AD → CRP (APOE 포함/제외)

## 파일 구성

```
.
├── inflammation_AD_MR.ipynb        # Part C 전체 분석 노트북 (R 커널)
├── inflammation_AD_MR_report.pdf   # Part C 결과 보고서
├── README.md
├── results/                        # 노트북 실행 시 생성
│   ├── mr_results_all.csv
│   ├── crp_ad_heterogeneity.csv
│   ├── crp_ad_egger_intercept.csv
│   └── crp_ad_harmonised_snps.csv
└── figures/                        # 노트북 실행 시 생성
    ├── crp_ad_scatter.png
    ├── crp_ad_forest.png
    ├── crp_ad_funnel.png
    ├── crp_ad_leaveoneout.png
    └── cytokine_ad_forest.png
```

## 실행 방법

1. **R 패키지 설치** (R ≥ 4.1)
   ```r
   install.packages(c("remotes", "dplyr", "ggplot2", "readr", "purrr", "IRkernel"))
   remotes::install_github("MRCIEU/TwoSampleMR")
   remotes::install_github("rondolab/MR-PRESSO")   # 선택
   IRkernel::installspec()                         # Jupyter R 커널 등록
   ```
2. **OpenGWAS 토큰 발급**: [api.opengwas.io](https://api.opengwas.io)에 로그인한 뒤 토큰을 생성합니다.
3. 홈 디렉터리의 `~/.Renviron`에 아래 한 줄을 추가하고 R 세션을 재시작합니다.
   ```
   OPENGWAS_JWT=<발급받은 토큰>
   ```
   > ⚠️ 토큰은 비밀번호와 같습니다. 노트북 셀에 `Sys.setenv(OPENGWAS_JWT = ...)`로 직접 쓰지 말고, `.Renviron`을 `.gitignore`에 넣어 커밋되지 않게 하세요.
4. Jupyter에서 `inflammation_AD_MR.ipynb`를 R 커널로 열고 위에서부터 순서대로 실행합니다.

**실행 환경**: R 4.6.1, TwoSampleMR 0.7.13, ieugwasr 1.2.0, MRPRESSO 1.0, ggplot2 4.0.3

## 한계와 다음 단계

**한계**
- 유럽인 GWAS만 사용해, Part A의 한국인 데이터 결과와 직접 연결하는 데 한계가 있습니다.
- 사이토카인 GWAS는 표본이 작아(843–8,293명) 검정력이 낮습니다.
- MR은 평생 지속되는 유전적 노출의 효과를 추정하므로, 단기 염증 조절(약물) 효과와는 다를 수 있습니다.

**TODO**
- [ ] **Steiger 방향성 검정 재실행**: AD GWAS의 case/control 메타데이터가 없어 오류가 났습니다. `add_metadata()`를 실행하거나 `ncase.outcome`, `ncontrol.outcome`을 지정해야 합니다.
- [ ] **IL6R cis-MR LD 보정**: `MendelianRandomization::mr_ivw(correl = TRUE)`로 잔여 LD를 반영합니다.
- [ ] **사이토카인 반복 분석**: 표본이 더 큰 Olink 염증 단백질 GWAS(Zhao 2023)를 사용합니다.
- [ ] **AD 반복 분석**: Bellenguez 2022로 반복합니다. 이때 UK Biobank 기반 노출 GWAS와의 표본 중복에 주의해야 합니다.
- [ ] **후속 가설 검증**: HLA·APOE와 연결된 뇌 면역 경로(예: 미세아교세포 관련 유전자)를 노출로 두는 분석을 검토합니다.

## 참고문헌

- Ligthart S, et al. Genome analyses of >200,000 individuals identify 58 loci for chronic inflammation and highlight pathways that link inflammation and complex disorders. *Am J Hum Genet.* 2018.
- Kunkle BW, et al. Genetic meta-analysis of diagnosed Alzheimer's disease identifies new risk loci and implicates Aβ, tau, immunity and lipid processing. *Nat Genet.* 2019.
- Ahola-Olli AV, et al. Genome-wide association study identifies 27 loci influencing concentrations of circulating cytokines and growth factors. *Am J Hum Genet.* 2017.
- Hemani G, et al. The MR-Base platform supports systematic causal inference across the human phenome. *eLife.* 2018.
- Verbanck M, et al. Detection of widespread horizontal pleiotropy in causal relationships inferred from Mendelian randomization between complex traits and diseases. *Nat Genet.* 2018.

## Author

이채민 · [github.com/lcm9903](https://github.com/lcm9903)
