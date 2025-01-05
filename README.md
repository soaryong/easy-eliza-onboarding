해커톤 준비하는 친구들에게 공유 하는 목적이니 가볍게 봐주세요.


---

eliza는 AI Agent Framework로 쉽게 AI Agent를 띄울 수 있다.
https://github.com/elizaos/eliza

자세한 내용을 보려면 아래 문서를 정독
https://elizaos.github.io/eliza/docs/intro/

이 문서의 목표는 엘리자를 로컬에서 돌리고
트위터 포스팅 되는 것을 확인하고
트위터에 있는 정보를 가져오는 것을 목표로 한다.

## 설정
```sh
# nodejs 설치
# eliza는 nodejs framework, typescript로 구현되어 있다.
# https://nodejs.org
node -v #v22.12.0

# nvm 설치
# eliza는 nodejs 23 환경에서 돌아가기 때문에 로컬에 노드 버전을 관리할 수 있는 nvm을 설치
# https://github.com/nvm-sh/nvm
nvm install 23
nvm use 23
node -v #v23.5.0

# pnpm 설치
# 이 문서에서는 패키지 모듈로 pnpm을 사용한다.

# git clone
git clone https://github.com/elizaos/eliza
cd eliza
```

## 프로젝트 구조
많은 파일들이 있지만 이 문서에서는 `characters/*` `.env.example`만 살펴본다

### `characters/tate.json`
```js
{
    "name": "tate",
    "clients": [],
    "modelProvider": "anthropic",
    "settings": {
        "secrets": {},
        "voice": {
            "model": "en_US-male-medium"
        }
    },
    "plugins": [],
    // ...
}
```
- clients에는 twitter, discord 등 agent가 일을 할 곳을 정해준다고 생각하면 된다.
- modelProvider에 어떤 AI를 사용할 것인지, 선택
- ... 아래 부분에 원하는 캐릭터 설정
- https://elizagen.howieduhzit.best/ 이 페이지에 있는 정보 참조

### `.env.example`
`.env` 파일에서 아래 부분에 트위터 Agent를 돌리기 위한 최소의 설정 값만 설명한다.
```sh
# .env로 파일이름을 변경한 후 세팅한다.

# ...

# Twitter/X Configuration
TWITTER_DRY_RUN=false
TWITTER_USERNAME= # Account username
TWITTER_PASSWORD= # Account password
TWITTER_EMAIL= # Account email
TWITTER_2FA_SECRET=
TWITTER_POLL_INTERVAL=120 # How often (in seconds) the bot should check for interactions
TWITTER_SEARCH_ENABLE=FALSE # Enable timeline search, WARNING this greatly increases your chance of getting banned
TWITTER_TARGET_USERS= # Comma separated list of Twitter user names to interact with
TWITTER_RETRY_LIMIT= # Maximum retry attempts for Twitter login
TWITTER_SPACES_ENABLE=false # Enable or disable Twitter Spaces logic
POST_INTERVAL_MIN= # Default: 90
POST_INTERVAL_MAX= # Default: 180
POST_IMMEDIATELY=

# ...  

ANTHROPIC_API_KEY= # For Claude

# ...

```
- 트위터 계정 정보, 포스팅 주기를 설정한다.
	- 트위터 계정은 테스트용으로 새로 파서 해보도록 한다.
	- TWITTER_POOL_INTERVAL - 위 계정을 통해 페이지 크롤링을 하게 되고 주기적으로 처리
		- 태그 트위터 글 타임라인 등 써있는 정보들을 확인 하고 그에 따른 Reaction / Reply
	- TWITTER_INTERVAL_MIN / TWITTER_INTERVAL_MAX
		- 위에 정해진 시간으로 트위터 포스팅을 한다
- Anthropic(Claude AI)
        - https://console.anthropic.com/ 여기서 가입 및 API 키 발급
	- Claude는 $10 또는 $5 정도만 넣어도 설정을 충분히 사용할 수 있다.
	- 돈 아낀다고 로컬_라마로 할 생각 하지 말자, 안돌아간다

## 실행

```sh
# 설치 및 실행
pnpm i #오류가 난 경우 아래 명령어를 통해 진행한다.
# pnpm install --no-frozen-lockfile
pnpm build
pnpm start
# 로컬에서 개발하며 돌릴 때는 pnpm dev로도 활용한다.
```
위 내용까지 실행하면 기본 캐릭터 / 설정으로 eliza는 돌아간다.
실행 하자마자 포스팅 되는 것을 확인하고, 풀링 하는 로그를 확인 할 수 있다

---



기타 스크린 샷 또는 자세한 설명은 필요하면 추가로 첨부하겠습니다.
추가로 설정할 부분 할 수 있는 일들이 엄청 많지만,
정말 단순히 실행을 바로 할 수 있는 정도로만 설명 한 것이니
수정할 부분 등은 같이 수정해주세요.
