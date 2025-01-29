# Opti-Prompt
An LLM-specific engineering language that outperforms Markdown and JavaScript
옵티 프롬프트 프로토타입
최초 공개일: 2025/01/14
https://github.com/Roteewolf/Rotee-s-RP-prompt 에서 'Rotee's RP Prompt Mild 1.2 Preview' 의 일부 설정을 적는 것에 활용 한 것이 최초 공개.
이후 지속적으로 업그레이드 중.

이 프롬프트 작문법은 계층, 참/거짓, 추가 카테고리의 요소로 나뉩니다.

#카테고리
##하위 카테고리

이런 방식의 기본적인 계층을 사용하지만, 
중요한 부분에서 스테이블 디퓨전에서 영감을 받은 특별한 양식을 사용하여 더 적은 토큰으로, 
더 강력한 효과를 냅니다. 
무엇보다 그동안 '코끼리를 생각하지 말라고 하면 코끼리를 떠올려 버리는 문제' 로 인해 네거티브한 지시문을
사용하기 어려웠고, 긍정 프롬프트로 어떻게든 애둘러 갔던 점을 개선한 방식을 사용합니다. 
즉, 네거티브를 자유롭게 사용함으로서, 결과물을 더욱 명확하게 합니다!

{"true" = "요소1, 요소2, 요소3}
{"false" = "네거티브요소1, 네거티브요소2"}

또한, 각 요소에 중요도를 추가하고, 중요도별 단계를 나눌 수도 있습니다!

{"true" = "(요소1:1.4), 요소2, 요소3}
{"false" = "네거티브요소1, (네거티브요소2:1.9)"}

이런 식으로 가중치를 주어서, Ai가 무엇에 더 집중해야 할 지 요점을 명확히 합니다.

그렇게, 가령 챗봇을 만들게 되면....

#글로벌 설정
{"true" = "(요소1:1.4), 요소2, 요소3}
{"false" = "네거티브요소1, (네거티브요소2:1.9)"}

##캐릭터 '유미' 설정
{Remember: 캐릭터의 외모 및 복장}
{"true" = "성격요소1, 요소2, 요소3}
{"false" = "네거티브요소1, 네거티브요소2"}

##캐릭터 '철수' 설정
{"true" = "성격요소1, 요소2, 요소3}
{"false" = "네거티브요소1, 네거티브요소2"}


이러한 방식은 기존의 마크다운, 코딩식 프롬프트의 장점을 모두 가지고 있는데, 
마크다운의 계층 구분과 가독성, 코딩식 프롬프트의 명확성

그리고 이 프롬프트만의 압도적인 토큰 절약과 토큰 절약과 명확성으로 인한 Ai의 생성 비용 감소 및
좋은 결과 도출! 거기다 성능이 약간 부족한 Ai에게도 대체적으로 잘 적용됩니다!
