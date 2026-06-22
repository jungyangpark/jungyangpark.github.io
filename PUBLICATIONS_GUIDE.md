# Publications 페이지에서 특정 저자에게 링크 추가하기

## 방법 1: coauthors.yml 사용 (권장)

`_data/coauthors.yml` 파일에 팀원이나 공동저자 정보를 추가하면, publications 페이지에서 해당 저자 이름에 자동으로 밑줄과 링크가 생성됩니다.

### 설정 방법

1. `_data/coauthors.yml` 파일 수정:

```yaml
"park":
  - firstname: ["Jungyang", "J.", "J. Y."]
    url: https://jungyangpark.github.io

"kim":
  - firstname: ["Gildong", "G.", "G. D.", "Gil-Dong"]
    url: https://gildong-kim.com

"lee":
  - firstname: ["Younghee", "Y.", "Y. H."]
    url: https://younghee-lee.github.io
```

2. BibTeX 파일(`_bibliography/papers.bib`)에서 저자 이름 작성:

```bibtex
@article{example2024,
  title   = {Example Paper Title},
  author  = {Park, Jungyang and Kim, Gildong and Lee, Younghee},
  journal = {Journal Name},
  year    = {2024}
}
```

### 중요 포인트

- **성(lastname)**: 키로 사용 (예: `"park"`, `"kim"`)
- **이름(firstname)**: 배열로 여러 변형 가능 (예: `["Jungyang", "J.", "J. Y."]`)
- **URL**: 개인 웹사이트 주소
- BibTeX의 저자 형식: `LastName, FirstName`

## 방법 2: 논문별 개별 설정

특정 논문에서만 특정 저자에게 링크를 추가하려면:

```bibtex
@article{example2024,
  title   = {Example Paper Title},
  author  = {Park, Jungyang and Kim, Gildong},
  year    = {2024},
  website = {https://project-website.com}  # 프로젝트 웹사이트
}
```

## 예제

### 예제 1: IDEA Team 멤버들

```yaml
# _data/coauthors.yml
"park":
  - firstname: ["Jungyang"]
    url: https://jungyangpark.github.io

"smith":
  - firstname: ["John", "J."]
    url: https://john-smith.com
```

```bibtex
# _bibliography/papers.bib
@inproceedings{park2024hci,
  title     = {Human-Data Interaction in Modern Systems},
  author    = {Park, Jungyang and Smith, John and Doe, Jane},
  booktitle = {CHI 2024},
  year      = {2024}
}
```

**결과**:
- "Park, Jungyang"과 "Smith, John"에는 밑줄 + 링크
- "Doe, Jane"은 일반 텍스트 (coauthors.yml에 없음)

### 예제 2: 여러 이름 변형

```yaml
"kim":
  - firstname: ["Gildong", "G.", "G. D.", "Gil-Dong"]
    url: https://gildong-kim.com
```

이렇게 하면 다음 형식들이 모두 링크됩니다:
- `Kim, Gildong`
- `Kim, G.`
- `Kim, G. D.`
- `Kim, Gil-Dong`

## 주의사항

1. **대소문자**: 성(lastname)은 소문자로 키를 만들어야 함
2. **동명이인**: 같은 성을 가진 여러 사람은 배열로 추가
3. **순서**: BibTeX 파일의 저자 순서대로 표시됨

## 테스트

논문을 추가한 후:
1. `bundle exec jekyll serve`로 로컬 서버 실행
2. `/publications/` 페이지 확인
3. 저자 이름에 밑줄과 링크가 표시되는지 확인
