### 오디오 파일 임베딩

> 음성파일의 파형 데이터 자체는 아님
> 
- 임베딩파일 → wav (원본) 복원 불가능함
- **원본 음성파일** = 실제 음식
- **embedding** = 그 음식의 맛 프로필 숫자표

```jsx
{
  "id": 123,
  "file_name": "UI_Noisy_Impact_09.wav",
  "s3_key": "audio/cinematic/ui-notification/button-click/UI_Noisy_Impact_09.wav",
  "category": "SFX",
  "sub_category": "UI",
  "tags": ["button", "click", "impact"],
  "duration": 0.77,
  "format": "wav",
  "sample_rate": 96000,
  "channels": 2,
  "description": "Cinematic UI button click impact",
  "embedding": [-0.0067, -0.0065, 0.0213, ...]
}
```

- 메타데이터랑, 임베딩 같이 저장
- 근데 임베딩모델 바뀔수도 있으니까, 분리해서 해도됨


### pgvector

> PostgreSQL에서 벡터 검색을 할 수 있게 해주는 확장 기능
> 
- PostgreSQL에 AI임베딩 벡터를 저장하고
- 이 문장과 의미가 비슷한 데이터를 만들어줘 같은 검색을 가능하게 해주는 도구