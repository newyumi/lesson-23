## 145. Nested routing in shop page
`shop.component.js`

`exact`를 하지 않으면 /something 에도 /가 있기 때문에 /something에 매칭되어있는 컴포넌트 / 루트 컴포넌트 둘 다 보임 
match 객체에는 매칭된 라우트 정보 
shopPage에 match 객체를 받아서 하위 라우터를 설정 `match.path`
## 146. Improving naming of component
category -> collection 으로 같은 단어로 변경

## 147. Collection routing and selector
`shop.selectors.js`

라우터에서 /shop/:collectionId <- 변수로 설정 

```javascript
// COLLECTION_ID_MAP: 상수로 id값 매핑 
collections => collections.find(collection => collection.id === COLLECTION_ID_MAP[collectionUrlParam])

const mapStateToProps = (state, ownProps) => ({
  collection: selectCollection(ownProps.match.params.collectionId)(state)
	// (state) is necessary, this selector needs a part of the state depending on the URL parameter
});
```
## 148. Memoizing selectCollection and collectionUrlParam
캐싱을 통해 동일한 계산 방지 

```javascript
import memoize from 'lodash.memoize';

export const selectCollection = memoize((collectionUrlParam) =>
  createSelector(
    [selectCollections],
    (collections) => collections[collectionUrlParam]
  )
);

(collectionUrlParam) =>
  createSelector(
    [selectCollections],
    (collections) => collections[collectionUrlParam]
 )
```

## 149. Currying
다중인수를 갖는 함수, 인자의 순서 중요 
```javascript
const multiply = (a, b) => a*b
const curriedMultiply = (a) => (b) => a*b
const curriedMultiplyBy5 = curriedMultiply(5)
curriedMultiplyBy5(4) // 20

const greetCurried = (greeting) => (name) => `${greeting}, ${name}`
const greetHello = greetCurried("Hello")
greetHello("Heidi")
greetHello("Eddie")
```

## heroku deploy
Install the Heroku CLI
Download and install the Heroku CLI.

If you haven't already, log in to your Heroku account and follow the prompts to create a new SSH public key.
```$ heroku login```

Create a new Git repository
Initialize a git repository in a new or existing directory
```
$ cd my-project/
$ git init
$ heroku git:remote -a heroku-service-shop
```

Deploy your application
Commit your code to the repository and deploy it to Heroku using Git.
```
$ git add .
$ git commit -am "make it better"
$ git push heroku master
```

You can now change your main deploy branch from "master" to "main" for both manual and automatic deploys, please follow the instructions here.

Existing Git repository
For existing repositories, simply add the `heroku` remote
```
$ heroku git:remote -a heroku-service-shop
```

## heroku, firebase 인증
firebase console -> db -> Authorized domains에서 도메인을 추가해줘야함 