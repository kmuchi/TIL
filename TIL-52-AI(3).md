### Base64

> 컴퓨터의 0과 1로 이루어진 데이터를 **64개의 출력 가능한 문자**(알파벳 대소문자 52개, 숫자 10개, 기호 `+`, `/`)로만 이루어진 긴 문자열로 변환
> 
- `data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABQAAAAUCAYAAACNiR0NAAA... (수천/수만 글자가 이어짐)`

### Rerank

- 리랭크란 내가 뽑은 후보군 다시 → LLM or 리랭크 모델에게 돌려서
- 다시 채점하는것
- 영상 장면 JOSN + 오디오 메타데이터 바탕으로 뭐가 맞는지 다시 채점