# JSON
[1. HTTP](#http)  
[2. JSON](#json)  
[3. Object to JSON](#object-to-json)  
[4. JSON to Object](#json-to-object)  

## HTTP
웹 어플리케이션과 같은 클라이언트들이 서버와 통신할 수 있는지를 정의한 것이 HTTP이며,  
HTTP는 Hypertext transfer Protocol의 약자로써 어떻게 Hypertext를 주고받을 수 있는지를 규약한 Protocol의 하나이다.  
클라이언트는 서버에 데이터를 request(요청)할 수 있고, 클라이언트가 요청한 것에 따라서 서버는 response(응답)을 클라이언트에 보내주는 방식으로 진행되는 것을 의미한다.  
Hypertext는 웹사이트에서 이용되어지는 Hyperlink뿐만이 아니라 전반적으로 쓰여지고 있는 리소스(문서, 파일, 이미지)들을 포함한 것 이다.  

## JSON
JSON은 Javascript Object Notation의 약자로써 자바스크립트의 Object와 관련이 있으며, 자바스크립트에서 사용되는 Object와 동일하게 key와 value로 이루어져 있다.  
또한 JSON은 브라우저 뿐만 아니라 모바일 에서 서버와 주고받을 때, 또는 서버와 통신을 하지 않아도 오브젝트를 파일 시스템에 저장할 때도 사용하고 있다.  

## Object to JSON
### stringify(obj)
``stringify(value: any, replacer?: (this: any, key: string, value: any) => any, space?: string | number): string;``  
``stringify(value: any, replacer?: (number | string)[] | null, space?: string | number): string;``  
stringify는 어떤 타입의 object를 받아와서 string타입으로 변환, 콜백함수를 선택적으로 사용할 수 있다.  
stringify는 이름은 동일하지만 전달되는 값이 조금씩 다른 두개의 api가 있는데 이러한 함수를 Overloading(오버로딩)이라고 한다.  

```
let json = JSON.stringify(true);
console.log(json);
```
![캡처](https://user-images.githubusercontent.com/73509513/157627336-9f79c2a0-7acd-47e0-9746-9673ed84ddaa.PNG)

JSON의 stringify를 이용하면 object를 JSON으로 변환할 수 있으며 boolean 타입도 변환 할 수 있다.  

```
json = JSON.stringify(['apple', 'banana']);
console.log(json);
```
![2](https://user-images.githubusercontent.com/73509513/157627350-307651be-bca3-42fe-a3f6-2cf0abd71f22.PNG)

JSON을 사용해서 배열을 변환하면 " "이 붙는데 이것은 JSON의 규격사항이다.

```
const rabbit = {
    name: 'tori',
    color: 'white',
    size: null,
    symbol: Symbol("id"),
    birthDate: new Date(),
    jump: () => {
        console.log(`${name} can jump!`);
    },
};

json = JSON.stringify(rabbit);
console.log(json);
```
![3](https://user-images.githubusercontent.com/73509513/157627392-787b5581-af63-44b2-996b-3d3833af72c1.PNG)

위의 object를 JSON으로 변환하게 되면 string 타입으로 변하게 된다.  
jump라는 함수는 JSON에 포함되지 않는데, 이는 함수는 Object에 있는 데이터가 아니기 때문에 제외되며,  
자바스크립트 내에서 자체적으로 지원하는 symbol등 특별한 데이터는 JSON에 포함되지 않는다.  

```
json = JSON.stringify(rabbit, ["name", "color"]);
console.log(json);
```
![4](https://user-images.githubusercontent.com/73509513/157627445-1fd93059-6069-4292-9ff2-3c48ab361898.PNG)

JSON에서 변환되는 것을 더 통제하고 싶다면 콜백함수를 이용하면 되는데, Object 뒤에 , 를 붙여 함수를 이용하거나 배열을 이용해 전달 할 수 있다.
그러므로 rabbit의 뒤에 배열로 name과 color를 붙이게 되면 이 두개의 property만 변환된다.
```
json = JSON.stringify(rabbit, (key, value) => {
    console.log(`key: ${key}, value: ${value}`);
    return value;
});
```
![5](https://user-images.githubusercontent.com/73509513/157627475-e2192baa-5716-47c9-aad0-2c7d64bf67f6.PNG)

모든 key와 value들이 콜백함수를 통해서 값이 전달되는 것을 확인할 수 있으며, 특이점은 제일 처음으로 전달되는 것은 rabbit의 object를 싸고있는 최상위의 값이 전달되며,  
그 후로 key와 value를 전달하게 된다.

```
json = JSON.stringify(rabbit, (key, value) => {
    console.log(`key: ${key}, value: ${value}`);
    return key === 'name' ? 'ellie' : value;
});
console.log(json);
```
![6](https://user-images.githubusercontent.com/73509513/157627558-c8682c10-849f-4eb2-9c9e-434e49dc1eef.PNG)

위처럼 key의 값에 name이 들어오게 되면 ellie라는 value로 무조건 설정하고 key가 name이 아닌경우 원래 value로 출력할 수도 있다.  

## JSON to Object
### parse(json)
parse는 json으로 부터 object를 만드는 API이다.
``parse(text: string, reviver?: (this: any, key: string, value: any) => any): any;``
parse는 json의 string 데이터를 어떤 타입의 object로 변환하며, 콜백 함수를 선택적으로 사용할 수 있다.  

```
json = JSON.stringify(rabbit);
const obj = JSON.parse(json);
console.log(json);

rabbit.jump();
```
![11](https://user-images.githubusercontent.com/73509513/157627878-9099dc50-88e8-48ae-b3b3-4254162eea9a.PNG)

jump라는 함수를 구현했지만 json에서 변활될 때 제외되어 json에서 obj로 변환되어도 jump 함수는 포함되지 않아 오류가 발생하므로 이 점을 유의해 코딩해야 한다.  

```
console.log(rabbit.birthDate.getDate());
console.log(obj.birthDate.getDate());
```
![9](https://user-images.githubusercontent.com/73509513/157627690-217e1a85-625d-48f9-8757-95023b525fc8.PNG)  
![7](https://user-images.githubusercontent.com/73509513/157627640-63da576f-8d92-4bad-97b3-502cf6a36498.PNG)

위의 rabbit object의 birthDate는 Date 타입으로 getDate라는 api를 사용할 수 있는데,  
json에서 변환한 obj에서는 오류가 발생한다.  
이는 birthDate가 json으로 변환될 때 string 타입으로 지정되어 obj에서는 Date 타입으로 지정되지 않기 때문이다.  

```
const obj = JSON.parse(json, (key, value) => {
    console.log(`key: ${key}, value: ${value}`);
    return key === 'birthDate' ? new Date(value) : value;
});
```
![8](https://user-images.githubusercontent.com/73509513/157627734-6e94663a-ab24-4d9b-bfe6-caacb3032331.PNG)

stringify와 동일하게 parse도 콜백 함수를 이용할 수 있다.  
key가 만약 birthDate면 새로운 Date라는 object를 만들고 만약 key가 birthDate가 아닐경우 value를 출력한다.  
이렇게 출력하게 되면 콜백함수로 인해 새로운 Date라는 object가 생성되어 위에서 발생한 오류가 해결된다.  
