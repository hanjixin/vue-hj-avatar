# vue-hj-avatar

A beautiful vue component for image crop and upload. （vue图片剪裁上传组件）.




## Change log

#### @1.1.0


## Screenshot
![screenshot](screenshot/1.png)

## Brower compatibility
IE10+


## Env
vue@2 + webpack + es6


## Install
#### npm
```shell
$ npm install vue-hj-avatar
```


## Usage
#### Props
| Name              | Type               | Default             | Description                                         |
| ----------------| ---------------- | ---------------| ------------------------------------------|
| serviceUrl          | String            |  ''                | Server api path,like "https://www.badu,com/avatar/upload", If empty, will not be uploaded    |
| token       | String   | ''     | 业务端认证token    |


#### Events
| Name              | Description                                         |
| ----------------| ------------------------------------------|
| successUpload   | image upload success, params( imageDataUrl, imgUrl )     |
| failUpload | upload fail, params( jsonData, field, imgUrl )    |


#### Language package
> 目前只有中文
#### slot 
```
example
<div slot="uploadBtn">
          点击上传
</div>
```
```
```
// js

 import avtor from 'vue-avatar-hj'
```

// html
<avtor v-bind:serviceUrl="'http://test-gateway.hejun.com/user/upload-avatar'">
        <div slot="uploadBtn">
          点击上传
        </div>
 </avtor>
```

