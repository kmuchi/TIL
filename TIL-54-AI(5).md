텍스트 토큰: "사과" → 토큰 ID(예: 3847) → 임베딩 벡터(4096-d)
이미지 토큰: 이미지 패치 → ViT 통과 → projector 통과 → 임베딩 벡터(4096-d)

### Projector

> ViT에서 만든 벡터를 → LLM에 맞게 변환해주는 어댑터 같은 것
>

### Neural Audio Codec
- 오디오판 토크나이저