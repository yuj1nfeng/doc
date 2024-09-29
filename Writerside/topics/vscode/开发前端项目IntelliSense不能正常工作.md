###### 项目根目录建立 jsconfig.json/tsconfig.json

```json
{
      "compilerOptions": {
            "experimentalDecorators": true,
            "module": "esnext",
            "target": "esnext",
            "exclude": ["node_modules"],
            "baseUrl": ".",
            "path":{
	            "src/*":["./src/*"]
	            ...
            }
      }

}
```

###### 配合 webpack

```json
{
	...
	  resolve: {
		  ...
		alias: {
			...
			'src': path.resolve(process.cwd(), 'src'),
		},
	},
}
```

###### 使用

-   import 时可以自动提示路径
    ![这是图片](https://erp-reportforms.oss-cn-hangzhou.aliyuncs.com/img/1.png)

-   使用时可以正常显示对象属性
    ![这是图片](https://erp-reportforms.oss-cn-hangzhou.aliyuncs.com/img/2.png)
