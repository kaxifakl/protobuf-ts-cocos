### protobuf-ts-cocos

基于[protobuf.js](https://github.com/protobufjs/protobuf.js/tree/ProtoBuf5)v5.0.3版本

此版本可以适配小游戏平台

```js
cc.resources.loadDir('proto', cc.TextAsset, (err, datas) => {
            console.log(datas);
            let files = []
            let allFile;
            for (let data of datas) {
                if (data.name == 'test') {
                    allFile = data;
                }
                files.push({ name: data.name + '.proto', text: data.text })
            }

	    //缓存所有加载好的proto文件
            ProtoBuf.cacheProtos(files)

	    //加载入口proto
            let builder = ProtoBuf.loadProto(allFile.text, allFile.name + '.proto')
            console.log(builder);
	  
	    //build package
            let cs = builder.build('cs');
            let uu = builder.build('UU')
            console.log(cs, uu);
            let main = cs['MainT'];
            let user = uu['User'];

            let bin = user.encode({ id: 1, id2: 2, id3: 3, id4: 4, id5: 5 })
            console.log(user.decode(bin));

            let bin2 = main.encode({ id: 1 })
            console.log(main.decode(bin2))
        })
```
