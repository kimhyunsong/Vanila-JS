# Fail Case





클로저 사용시 유의점 

```js
const $closure = (function() {
    var contentArr = []
    return function (text){
      contentArr.push(text)
      return contentArr
      
    }
}());
console.log($closure('ab'))
console.log($closure('ac'))
console.log($closure('ad'))
console.log($closure('ae'))
```





```js
const $closure = (function() {
    var contentArr = []
    return function (text){
        contentArr = [...contentArr, text]
        return [...contentArr, text]

    }
}());

console.log($closure('ab'))
console.log($closure('ac'))
console.log($closure('ad'))
console.log($closure('ae'))
```

 전개 구문은 deepcopy에 의해서 새로운 배열을 반환하고, 자유변수 contentArr에는 영향을 주지 않는다.





innerHtml로 li태그를 직접 넣어줄 때 발생하는 문제

![image-20220324220851973](C:\Users\ssong\Desktop\toy\Fail Case.assets\image-20220324220851973.png)

map은 새로운 배열을 리턴하는 함수로 [li태그, li태그, li태그]이런식으로 반환되는데, innerHtml에는 ","가 추가적으로 들어가게 된다. 한편 괄호가 안들어가는 이유는 백틱으로 string 으로 변환해주었기 때문이다.



따라서 join을 통해 , 없이 붙여쓸 경우 아래 주석과 같이 표현할 수 있으며 html에서는 의도한대로 표현할 수 가 있다.







```js
const render = (state) =>{
    document.createElement('ul')
    _app.innerHTML = `
      ${state.map(content=>{
        return `<li>${content}</li>`
        // <li>{content}</li><li>{content}</li><li>{content}</li>
    }).join('')}

    `;
}
//li 태그를 .join으로 붙여서 쓰면 ,가 렌더링이 안됨.
```

