# 2021_korean_competition
2021 국립국어원 인공 지능 언어 능력 평가

## Docker 이미지 다운 and 모델 평가 방법

1. Docker 이미지 다운로드(cuda11.0 지원)
2. Docker 이미지 load & container 실행
```console
docker run --gpus 1 --rm -it rocket
```
3. 환경설정
```console
conda activate rocket
pip install -r requirements.txt
```
4.평가용 데이터 삽입(./data/boolq/ , ... 각 4가지 Task별 폴더에 삽입)
5.평가 코드(get_result.py)를 arguments(데이터 경로, batchsize 등)와 함께 실행 (40분 정도 소요)
```console

python get_result.py --batch_size 100 --num_worker 5 --boolq_data_path 'data/boolq/_.tsv' --cola_data_path 'data/cola/_.tsv' --copa_data_path 'data/copa/_.tsv' --wic_data_path 'data/wic/_.tsv' --result_file_name 'result.json' --device 'cuda:0'

```
6.평가가 완료되면 './result/' 경로에 저장된 결과파일(tsv)이 저장된다.
```console
docker run --gpus 1 --rm -it rocket
```

## 각 Task별 Train 코드
1. 환경설정
```console

pip install -r requirements.txt

```
2. 학습코드 실행
```console
bash boolq.sh roberta [bsz]
bash cola.sh roberta [bsz]
bash copa.sh roberta [bsz]
bash wic.sh roberta [bsz]
```