## import 别名
``` javascript
# jsconfig.json
{
      "compilerOptions": {
            "paths": {
                  "#root/*": [
                        "./*"
                  ],
                  "#utils/*": [
                        "./utils/*"
                  ],
                  "#service/*": [
                        "./service/*"
                  ],
                  "#middleware/*": [
                        "./middleware/*"
                  ]
            }
      },
}
# package.json
{
	...
	"imports": {
            ...
            "#root/*": "./*",
            "#utils/*": "./utils/*",
            "#middleware/*": "./middleware/*",
            "#service/*": "./service/*",
            ...
      },
	...
}


# 使用
import userService from '#service/user.service.js';
...

```