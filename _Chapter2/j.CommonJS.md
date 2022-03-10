CommonJS
CommonJS는 모든 버전의 노드(NodeJS)가 지원하는 모듈패턴이다.

CommonJS에서 .exports를 사용하면 객체를 내보낼 수 있게된다.(NodeJS에서 많이 봤을 것이다.)
CommonJS에 import는 없다. 대신 require함수가 import의 역할을 한다.(이 또한 NodeJS에서 많이 봄)

/************** export Example **************/
  const print(message) => log(message, new Date())

  const log(message, timestamp) =>
  console.log(`${timestamp.toString()}: ${message}`}

  module.exports = {print, log} //export
/************** export Example **************/

/************** import Example **************/
  const { log, print } = require("./txt-helpers");
/************** import Example **************/