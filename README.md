## 해당 코드는 교내 대회에서 사용되었으며 데이터를 첨부해 드릴 수 없습니다.

### 1. Library 설정 및 필요 함수 정의
#### 마크다운 셀 내용
- **find_wav_files**: 디렉토리 내의 .wav 파일들을 찾는 함수.
- **set_seed**: 실험의 재현성을 위해 랜덤 시드를 고정하는 함수.
  
#### 코드
- 주요 라이브러리(os, random, torch, torchaudio 등)와 유틸리티 함수 정의.
- 주요 함수:
  - **find_wav_files(path_to_dir)**: 주어진 디렉토리 내의 .wav 파일을 재귀적으로 찾고 정렬하여 반환.
  - **set_seed(seed)**: NumPy, PyTorch, Python Random에 시드를 설정하여 실행 결과의 재현성을 확보.

---

### 2. 데이터셋 관련 코드
#### 마크다운 셀 내용
- **AudioDataset**:
  - .wav 파일을 처리하는 데이터셋 클래스.
  - real과 fake 데이터의 불균형(1:7)을 해결하기 위해 real 데이터를 7배로 확장.
  - .wav 파일을 텐서(tensor)로 변환하고 샘플레이트를 통일.

- **PadDataset**:
  - 모든 오디오의 길이를 4초(샘플 크기 64600)로 맞추는 클래스.
  - 4초보다 긴 파일은 잘라내고, 짧은 파일은 반복해서 길이를 맞춤.
    
- **load_dataset & load_dataset_test**:
  - 데이터셋 로딩 함수로, 학습용과 테스트용 데이터를 각각 불러옴.

#### 코드

- **AudioDataset 클래스**:
  - .wav 파일을 읽고 텐서로 변환.
  - 샘플레이트를 원하는 값(기본 16kHz)으로 통일.
  - 데이터 불균형 문제 해결을 위해 real 데이터를 7배 확장.
    
- **PadDataset 클래스**:
  - 모든 오디오 파일의 길이를 4초로 맞춤.
  - 길이가 짧으면 반복 재생, 길면 자르기.

- **데이터셋 로딩 함수**:
  - **load_dataset**: 학습용 데이터를 로드. real과 fake 데이터를 구분하여 처리.
  - **load_dataset_test**: 테스트용 데이터를 로드. 기본적으로 4초로 패딩 처리.

---

### 3. 모델 관련 코드

#### 마크다운 셀 내용

- **RawNet**:
  - 음성 데이터를 처리하여 fake와 real의 확률을 반환하는 모델.
  - **__init__**: 네트워크 구조 초기화.
  - **__forward__**: 입력 데이터를 통해 순전파(forward)를 수행.

 ---

### 주요 기능 

#### 1. 유틸리티:
- 오디오 파일을 읽고 텐서로 변환.
- 데이터셋 불균형 문제를 해결.
- 실험 결과 재현성을 위해 시드 설정.

#### 2. 데이터셋 처리:
- 오디오 데이터를 처리하여 길이를 4초로 맞춤.
- 학습용 및 테스트용 데이터셋을 로드.

#### 모델:
- RawNet2 기반 모델을 정의.
- 순전파를 통해 real/fake 확률 예측.
