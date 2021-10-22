## Stream

스트림 가능한 소스로부터 데이터를 작은 Chunk로 쪼개 처리할 수 있게 함

큰 데이터를 처리해야하거나, 비동기적으로만 얻을 수 있는 데이터를 처리해야 할 때 유용함

#### 일반적인 구현 형태

```js
const fs = require("fs");
const rs = fs.createReadStream("file.txt", {
  encoding: "utf-8",
  highWaterMark: 65536, // 각 chunk의 사이즈를 조절할 수 있음. 65536은 default 값
});

//콜백 인자는 createReadStream단계에서 인코딩을 지정해주지 않는다면 Buffer 형태를 가짐
rs.on("data", (data) => {
  //데이터에 대한 처리 코드 작성
});

rs.on("error", (error) => {
  // 데이터에 대한 에러 처리 코드 작성
});
```

### 종류

#### Readable

스트림으로부터 읽을 수 있음

- fs.createReadStream
- process.stdin
- 서버 입장의 HTTP 요청
- 클라이언트 입장의 HTTP 응답

#### Writable

스트림에 출력할 수 있음

- fs.createWriteStream
- process.stdout
- 클라이언트 입장의 HTTP 요청
- 서버 입장의 HTTP 응답

#### Duplex

입력을 받을 수도 있고, 출력을 보낼 수도 있음

- TCP sockets
- zlib streams
- crypto streams

#### Transform

입력받은 스트림을 변환해 새로운 스트림으로 만듬

- zlib streams
- crypto streams

### 유의점

- chunk가 잘리는 지점이 일정하지 않았을 때, 원하는 처리를 못하는 문제가 발생할 수 있으니, 데이터 처리할 때 신경을 써줘야함

### pipeline을 통한 사용 예시

- pipeline : transform stream을 쉽게 활용하게 도와줌

```js
const fs = require('fs');
const stream = require('stream');
const zlib = require('zlib');

stream.pipeline( // 압축
  fs.createReadStream("read"), // 입력 스트림
  zlib.createGzip(), // 입력 받은 스트림을 transform 시킴
  fs.createWriteStream("transform.gz") // write stream으로 보냄
  (err) => {
      if(err) {
          console.error('Gzip failed', err);
      } else{
          console.log('Gzip succeeded');
      }

      stream.pipeline( // 압축해제
  fs.createReadStream("transform.gz"),
  zlib.createGunzip(),
  fs.createWriteStream("transform.unzipped")
  (_err) => {
      if(_err) {
          console.error('Gunzip failed', _err);
      } else{
          console.log('Gunzip succeeded');
      }
  }
);
  }
);
```

- promise를 활용한 코드 리팩토링

```js
const fs = require("fs");
const stream = require("stream");
const zlib = require("zlib");
const util = require("util");

async function gzip() {
  return util.promisify(stream.pipeline)(
    fs.createReadStream("read"),
    zlib.createGzip(),
    fs.createWriteStream("transform.gz")
  );
}

async function gunzip() {
  return util.promisify(stream.pipeline)(
    fs.createReadStream("transform.gz"),
    zlib.createGunzip(),
    fs.createWriteStream("transform.unzipped")
  );
}

async function main() {
  await gzip();
  await gunzip();
}

main();
```
