# final_individual_task

## 개요

가상의 코인 거래소를 제작한다. 유저는 회원가입, 자산 조회, 시세 조회, 구매 및 판매의 행위를 할 수 있다.  
수업 시간에 배운 nodejs, mongodb를 활용하여 구현한다.

## 가격조회

가격은 https://www.coingecko.com/en/api 의 api를 이용해서 가져온다. (https://www.coingecko.com/api/documentations/v3#/simple/get_simple_price)  
거래가능한 코인의 종류는 btc, xrp, eth, bch 4가지로 제한한다.  


## api 명세

성공 시 status 2xx, 클라이언트 에러로 실패 시 4x코드로 반환. 
모든 response data는 json 형태.  
authentication 필요한 코드의 경우, header의 Authorization에 Bearer: {Key} 를 포함해서 호출함.  
에러가 날 경우, {error: '{reason}'}를 보내도록.


### /register
회원가입 시 유저에게 10,000$를 제공한다.  
[:POST]

request


- name: string. 4-12글자. alphanumeric
- email: string. 100자 미만. email형식
- password: 8-16글자.


response
 - {}

### /login
[:POST]

request
- email
- password


response
- {key: {key}}

### /coins
[:GET]

request


response
- ["btc", "xrp", "bch", "eth"]

### /assets
본인의 자산을 조회한다. 없는 자산의 경우 노출시키지 않는다.
[:GET]  
:auth_required  


request

response
- ["usd": 3000, "btc": 1, "xrp": 2, "bch": 3, "eth": 4]

### /coins/:coin_name
코인의 현재 시세를 보여준다.
[:GET]

request
- 

response
가격 조회결과를 리턴한다.
- {price: 30000 }


### /coins/:coin_name/buy
코인을 구매한다. 가격은 실시간으로 가져온 api의 가격을 따른다.
[:POST]
:auth_required  

request
- quantity: number. 소수점 4번째 자리까지.

response
구매결과를 리턴한다.
- {price: 30000, quantity: 1}


### /coins/:coin_name/sell
코인을 판매한다. 가격은 실시간으로 가져온 api의 가격을 따른다.
[:POST]
:auth_required  


request
- quantity: number. 소수점 4번째 자리까지.


response
구매결과를 리턴한다.
- {price: 30000, quantity: 1}




## models

다음의 모델들이 구현되어 있어야 한다.  

users, keys, coins, assets

## 추가 스펙

- 코인 2종 추가.  
- 로그인 시 jwt사용하기.(http://jwt.io)  
- 코드샌드박스에 올려, url을 같이 제출.
- 코인 구매, 판매 시 전량구매/전량판매 기능 구현. (ex - xrp 전량 구매 => 사용가능한 usd를 다 사용하여 xrp구매)


## 제출
12.12 까지. etl을 통해 제출. 
폴더명, 파일명을 학번으로 하여 코드를 zip로 압축하여(node_modules제외) 제출.(ex - 2007-11186.zip)  
하루 늦을 때마다 5% 감점. 13일까지 제출 받음.  

