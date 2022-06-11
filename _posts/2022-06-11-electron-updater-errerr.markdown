# 자동 업데이트 관련 error

자동업데이트가 계속해서 실패해서 오류를 확인해보니

릴리스된 레포지토리를 확인할 수 없다는 메세지와 토큰을 확인하라는 메시지만 나온다.

하지만 나는 빌드파일도 만들어서 github에 배포한 상태이며, 토큰도 제대로 넣었따. 뭐가 문제일까 봤더니

release가 아닌 draft에서 업데이트를 확인했던 것 !

elctron-builder에서 publish 옵션에 releaseType을 release로 주어 해결하자 .

```json
{
  "publish": [
    {
      "provider": "github",
      "owner": "내꺼",
      "repo": "내꺼거",
      "private": true,
      "token": "내 토근",
      "releaseType": "release"
    }
  ],
  "directories": {
    "buildResources": "assets"
  }
}
```
