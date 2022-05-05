<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>


### 1단계 - 웹 성능 테스트
1. 웹 성능예산은 어느정도가 적당하다고 생각하시나요


**내 서비스 진단 결과**([PageSpeed](https://pagespeed.web.dev) 기준)

![img](https://user-images.githubusercontent.com/53864640/166479131-325dfef7-ffa8-4af4-9f2d-4fd291a309d2.png)

**경쟁 서비스 비교**([PageSpeed](https://pagespeed.web.dev) 기준)

|                | 서울교통공사  | 네이버지도  |  카카오맵  | 내 서비스 | 경쟁사 평균 | 경쟁사 평균 대비 20% 오차 |
|:--------------|:-------|:------|:------|:------|:------|:-----------------|
|     FCP(s)     |   7.3   |  2.2   |  1.7   | 14.6  | 3.7 | 4.4              |
| Speed Index(s) |  13.3   |  5.2   |  7.0   | 14.6  | 8.5 | 10.2             |
|     LCP(s)     |   8.0   |  7.5   |  4.7   | 15.2  | 6.7 | 8.0              |
|     TTI(s)     |   8.9   |  6.8   |  4.4   | 15.3  | 6.7 | 8.0              |
|    TBT(ms)     |   410   |  350   |  100   | 560   | 287 | 344              |
|      CLS       |    0    |  0.03  | 0.005  | 0.042 | 0.01| 0.012            |
|  Total Score   |   39    |   57   |   73   | 32    | 56 | 44.8             |

사용자가 인식할 수 있는 속도차이인 20% 이상을 넘지 않기 위해<br/>
즉, 경쟁사 대비 20% 이상의 성능차이가 발생하지 않도록 위 표에 나타난 "경쟁사 평균 대비 20% 오차"를 목표치로 생각하려고 합니다.


2. 웹 성능예산을 바탕으로 현재 지하철 노선도 서비스는 어떤 부분을 개선하면 좋을까요

PageSpeed 진단 결과 추천하는 개선 방안은 다음과 같았습니다.

**FCP**
- 텍스트 압축 사용 (9.3s)
- 렌더링 차단 리소스 제거 (0.75s)
- 사용하지 않는 CSS 줄이기 (0.15s)

**TBT**
- 기본 스레드 작업 최소화하기 (2.3s)
- 자바스크립트 실행 시간 단축 (1.5s)

**LCP**
- 텍스트 압축 사용 (9.3s)
- 사용하지 않는 자바스크립트 줄이기 (3.45s)
- 렌더링 차단 리소스 제거 (0.75s)
- 콘텐츠가 포함된 최대 페인트 이미지 미리 로드 (0.33s)
- 사용하지 않는 CSS 줄이기 (0.15s)

**CLS**
- 이미지 요소에 width 및 height가 명시되어 있지 않음. (명시하기)
- 대규모 레이아웃 변경 피하기

주요 개선 방안을 추려 보면,

1. 텍스트 압축 사용
2. 렌더링 차단 리소스 제거
3. 사용하지 않는 자바스크립트, CSS 줄이기
4. 이미지 요소에 width 및 height가 명시되어 있지 않음

가 있을 것 같습니다.

---

### 2단계 - 부하 테스트 
1. 부하테스트 전제조건은 어느정도로 설정하셨나요

2. Smoke, Load, Stress 테스트 스크립트와 결과를 공유해주세요

---

### 3단계 - 로깅, 모니터링
1. 각 서버내 로깅 경로를 알려주세요

2. Cloudwatch 대시보드 URL을 알려주세요
