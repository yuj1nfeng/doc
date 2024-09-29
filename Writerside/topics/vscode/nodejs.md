###### jsconfig.json
- 这里配置 paths 只是为了让编辑器能够识别导入的路径
```json
{
    "compilerOptions": {
        "paths": {
            "@/*": [
                "./src/*"
            ],
            "@pages/*": [
                "./src/pages/*"
            ],
            "@layouts/*": [
                "./src/layouts/*"
            ],
            "@styles/*": [
                "./src/styles/*"
            ],
            "@utils/*": [
                "./utils/*"
            ],
            "@wails/*": [
                "./wailsjs/*"
            ]
        }
    }
}
```

###### vite 项目 alias 配置
- 在项目根目录下 vite.config.js
```javascript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';

// https://vitejs.dev/config/
export default defineConfig({
    plugins: [react()],
    resolve: {
        alias: {
            '@': '/src',
            '@src': '/src',
            '@styles': '/src/styles',
            '@pages': '/src/pages',
            '@layouts': '/src/layouts',
            '@utils': '/utils',
            '@wails': '/wailsjs',
        }
    }

});

```

###### umi 项目 alias 配置
- 在项目更目录下 .umirc.js
```javascript
import { defineConfig } from '@umijs/max';
import path from 'path';
export default defineConfig({
    alias: {
        '@src': path.resolve(__dirname, './src'),
        '@components': path.resolve(__dirname, './src/components'),
        '@services': path.resolve(__dirname, './src/services'),
        '@utils': path.resolve(__dirname, './src/utils'),
    },
});
```