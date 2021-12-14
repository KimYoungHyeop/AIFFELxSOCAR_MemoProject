# AIFFELxSOCAR_MemoProject

- **해커톤 주제**: 정비 메모 분석 및 프로세스 자동화
- **프로젝트명**: 정비 메모를 활용한 자동완성 및 카테고리 분류 어플리케이션

<br>

## 프로젝트 요약

이 프로젝트는 모두의연구소 산하 교육기관 **AIFFEL**과 카셰어링 기업 **SOCAR**가 협력하여 진행한 해커톤에서 아이카센터 팀이 SOCAR로부터 제공받은 정비 메모 데이터를 활용하여 주어진 문제를 해결한 프로젝트입니다.

<br>

## 포스터
![해커톤3_최종발표_포스터_아이카센터](https://user-images.githubusercontent.com/42146731/145956628-6b7505c1-cc42-4516-a0b6-0145a091bfe6.jpg)

<br>

## 구성원 및 역할

* 최혜림  
  [![Tech Blog Badge](http://img.shields.io/badge/-Github-black?style=flat-square&logo=github&link=https://github.com/hyelimchoi1223)](https://github.com/hyelimchoi1223)  [![Blog Badge](http://img.shields.io/badge/-Blog-EF2D5E?style=flat-square&logo=GitHub%20Sponsors&logoColor=white&link=https://hyelimchoi1223.github.io/)](https://hyelimchoi1223.github.io/)
* 윤세휘  
  [![Tech Blog Badge](http://img.shields.io/badge/-Github-black?style=flat-square&logo=github&link=https://github.com/Beatriz-Yun)](https://github.com/Beatriz-Yun)    [![Blog Badge](http://img.shields.io/badge/-Blog-EF2D5E?style=flat-square&logo=GitHub%20Sponsors&logoColor=white&link=https://beatriz-yun.github.io/)](https://beatriz-yun.github.io/)
* 안형준  
  [![Tech Blog Badge](http://img.shields.io/badge/-Github-black?style=flat-square&logo=github&link=https://github.com/hjkornn-phys)](https://github.com/hjkornn-phys)     [![Blog Badge](http://img.shields.io/badge/-Blog-EF2D5E?style=flat-square&logo=GitHub%20Sponsors&logoColor=white&link=https://velog.io/@gibonki77)](https://velog.io/@gibonki77)
* 신관수  
  [![Tech Blog Badge](http://img.shields.io/badge/-Github-black?style=flat-square&logo=github&link=https://github.com/kwansu)](https://github.com/kwansu)    
* 김영협  
  [![Tech Blog Badge](http://img.shields.io/badge/-Github-black?style=flat-square&logo=github&link=https://github.com/KimYoungHyeop)](https://github.com/KimYoungHyeop) [![Blog Badge](http://img.shields.io/badge/-Blog-EF2D5E?style=flat-square&logo=GitHub%20Sponsors&logoColor=white&link=https://blog.naver.com/kyh568)](https://blog.naver.com/kyh568)
  

## 사용한 기술 스택

- Python
- Pytorch, Tensorflow
- Goole Colab, Jupyter Notebook
- Google Cloud Platform
- Git
- Flask, Bootstrap 
- RestAPI, MongoDB


## 크롤링을 톨한 tokenize and extract noun
구글 크롤링을 통해 여러 단어가 조합된 조합어를 토큰화 및 명사 추출한다.  

google searcher를 이용해 크롤링된 결과를 바탕으로 조합을 만든다.
```
s = '정지에서출발할때떨림발생건'
searcher = GoogleSearcher()
create_continuous_likely_dict(searcher, s)

# 정지에서출발할때떨림발생건
# {0: [('정지', 6)],
#  2: [('에', 6), ('에서', 6)],
#  4: [('출발', 8)],
#  6: [('할', 4), ('할때', 1)],
#  7: [('때', 4)],
#  8: [('떨림', 5)],
#  10: [('발생건', 0)]}
```

tokenize_all_case로 토큰화(가능한 조합들을 생성해 낸다.)
```
tokenize_all_case(searcher, '정지에서출발할때떨림발생건')

# [(정지,에서,출발,할,때,떨림,발생건), (정지,에서,출발,할때,떨림,발생건)]
```

extract_nouns함수로 명사추출
```
extract_nouns(searcher, '정지에서출발할때떨림발생건')

# 정지, 출발, 때, 발생건
```


## 시연
![시연결과](https://user-images.githubusercontent.com/63278762/145804249-70e3d9af-3422-4c52-b452-f9fa5581f555.gif)

## 화면 캡쳐
<img width="1440" alt="스크린샷 2021-12-14 오후 12 04 21" src="https://user-images.githubusercontent.com/63278762/145925898-569f378f-b93c-4d85-883b-a16bb8cb4c6b.png">
<img width="1440" alt="스크린샷 2021-12-14 오후 12 04 15" src="https://user-images.githubusercontent.com/63278762/145925932-c6118b00-14e5-4a9d-931d-37c14a9db8a5.png">
<img width="1440" alt="스크린샷 2021-12-14 오후 12 04 48" src="https://user-images.githubusercontent.com/63278762/145925919-9811cf29-21b2-4502-a3ee-0b6a9d0bef98.png">
<img width="1440" alt="스크린샷 2021-12-14 오후 12 05 09" src="https://user-images.githubusercontent.com/63278762/145925922-3552184a-b37a-4b47-853f-bfab9159c526.png">
<img width="1440" alt="스크린샷 2021-12-14 오후 12 05 47" src="https://user-images.githubusercontent.com/63278762/145925927-19070398-e2f7-4c19-8d86-0f67aa04d0ba.png">

## Reference
* [LR-NounsExtrator](https://lovit.github.io/nlp/2018/04/09/three_tokenizers_soynlp/)
* [KR-WordRank](https://lovit.github.io/nlp/2018/04/16/krwordrank/)
* [Jaccard Similarity](https://wikidocs.net/24654)
* [자모 분리 및 결합](https://needjarvis.tistory.com/627)
* [한국어 단어 자동완성 시스템의 성능 분석 및 새로운 평가 방법](http://koreascience.kr/article/JAKO201525249160709.pdf)
