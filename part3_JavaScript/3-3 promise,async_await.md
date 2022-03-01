# Promise

위에서 봤듯이 Javascript에서는 대부분의 작업들이 비동기로 이루어진다. 콜백 함수로 처리하면 되는 문제였지만 요즘에는 프론트엔드의 규모가 커지면서 코드이 복잡도가 높아지는 상황이 발생하였다. 이러면서 콜백이 중첩되는 경우가 따라서 발생하였고, 이를 해결할 방안으로 등장한 것이 __Promise__ 패턴이다. __Promise__패턴을 사용하면 비동기 작업들을 순차적으로 진행하거나, 병렬로 진행하는 등의 컨트롤이 보다 수월해진다. 또한 예외처리에 대한 구조가 존재하기 때문에 오류 처리 등에 대해 보다 가시적으로 관리할 수 있다. 이 Promise 패턴은 ECMAScript6 스펙에 정식으로 포함되었다.

```javascript
//Promise 선언
var _promise = function (param) {
	return new Promise(function (resolve, reject) {
		// 비동기를 표현하기 위해 setTimeout 함수를 사용 
		window.setTimeout(function () {
			// 파라메터가 참이면, 
			if (param) {
				// 해결됨 
				resolve("해결 완료");
			}
			// 파라메터가 거짓이면, 
			else {
				// 실패 
				reject(Error("실패!!"));
			}
		}, 3000);
	});
};
//Promise 실행
_promise(true)
.then(function (text) {
	// 성공시
	console.log(text);
}, function (error) {
	// 실패시 
	console.error(error);
});

// console >> "해결 완료"
```

Promise는 말 그대로 "약속"이다.  "지금은 없으니까 이따가 줄게~" 라는 약속이다. 좀 더 정확히는 "지금은 없는데 이상없으면 이따가 주고 없으면 알려줄게~" 라는 약속이다.

따라서 Promise 는 다음 중 하나의 상태(state)가 될 것이다

- pending : 아직 약속을 수행 중인 상태(fulfilled 또는 reject가 되기 전)이다.
- fulfilled : 약속(promise)이 지켜진 상태이다.
- rejected : 약속(promise)이 어떤 이유에서 못 지켜진 상태이다.
- settled : 약속이 지켜졌든 안지켜졌든 일단 결론이 난 상태이다.



# Async / Await

비동기 코드를 작성하는 새로운 방법이다. 기존의 Promise로 만족하지 못하고 더 훌륭한 방법을 고안 해낸 것이다. (사실 async / await는 promise 기반). function 키워드 앞에 async 를 붙여주면 되고 function 내부의 promise를 반환하는 비동기 처리 함수앞에 await를 붙여주기만 하면 된다.

async / await의 가장 큰 장점은 Promise 보다 비동기 코드의 겉모습을 더 깔끔하게 한다는 것이다. 이 것은 es8의 공식 스펙이며 node8LTS에서 지원된다.

- `promise`로 구현

```javascript
function makeRequest() {
    return getData()
        .then(data => {
            if(data && data.needMoreRequest) {
                return makeMoreRequest(data)
                  .then(moreData => {
                      console.log(moreData);
                      return moreData;
                  }).catch((error) => {
                      console.log('Error while makeMoreRequest', error);
                  });
            } else {
                console.log(data);
                return data;
            }
        }).catch((error) => {
          console.log('Error while getData', error);
        });
}
```

- `async/await`로 구현

```javascript
async function makeRequest() { 
    try {
      const data = await getData();
      if(data && data.needMoreRequest) {
          const moreData = await makeMoreRequest(data);
          console.log(moreData);
          return moreData;
      } else {
          console.log(data);
          return data;
      }
    } catch (error) {
        console.log('Error while getData', error);
    }
}
```

#### reference

- [https://medium.com/@kiwanjung/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4](https://medium.com/@kiwanjung/번역-async-await-를-사용하기-전에-promise를-이해하기-955dbac2c4a4)
- [https://medium.com/@constell99/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-async-await-%EA%B0%80-promises%EB%A5%BC-%EC%82%AC%EB%9D%BC%EC%A7%80%EA%B2%8C-%EB%A7%8C%EB%93%A4-%EC%88%98-%EC%9E%88%EB%8A%94-6%EA%B0%80%EC%A7%80-%EC%9D%B4%EC%9C%A0-c5fe0add656c](https://medium.com/@constell99/자바스크립트의-async-await-가-promises를-사라지게-만들-수-있는-6가지-이유-c5fe0add656c)


