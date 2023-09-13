# Intorduction

본 프로젝트는 Yarn Berry PnP + Nest.js + Docker 조합을 테스트하고 방법을 기록해두기 위해,

아카이빙 성격으로 생성된 것으로 지속적으로 유지 보수되지는 않습니다.

이 조합을 도입하려는 이유는 막대한 노드 모듈의 용량(거의 2GB) 때문이었는데, Yarn Berry PnP는 이를 해결해주기 때문이었습니다.

## 사용법

리눅스 환경을 가정하고 있는데, Windows나 MacOS라면 도커 데스크탑을 설치해야 할 수 있습니다.
도커가 준비가 되었다면 다음 명령으로 이미지를 빌드합니다.

```sh
docker build -t test-container .
```

그런 다음 아래 명령어로 컨테이너를 실행하면 Hello World가 출력됩니다.

```sh
docker run -it --rm -p 3000:3000 test-container
```

## 기존 프로젝트에 설정 방법

먼저 yarn 버전을 berry로 설정해야 합니다.

```sh
yarn set version berry
```

설정이 정상적으로 되었다면, `yarn --version`으로 버전을 확인할 수 있습니다.

```sh
yarn --version
```

이제 프로젝트를 초기화합니다.

```sh
yarn install
```

만약, node_modules가 남아있다면 `.yarnrc.yml` 파일을 엽니다.

```sh
nodeLinker: node-modules
```

위 속성을 삭제하고, `node_modules` 폴더를 지우고 다시 `yarn install`을 실행합니다.

VSCode에서 ZipFS라는 확장을 설치합니다.

```sh
yarn dlx @yarnpkg/sdks vscode
yarn plugin import typescript
```

또한 위 명령어를 실행하여 타입스크립트 환경을 설정해야 합니다.

테스트 후, 생성된 파일들을 제거하고 초기로 돌아가려면 아래와 같이 하시기 바랍니다.

```sh
docker system prune -a -f
```

## 참고

주의할 점은 현재 샘플은 규모가 매우 작아서 별 문제가 없습니다.

하지만 여러 글에 의하면 일부 패키지는 읽을 수 없는 현상이 있습니다.

이땐 `nodeLinker`를 활성화하거나, 패키지를 포기해야 할 수 있습니다.

해결이 되지 않으면 도입이 어려울 수 있습니다.
