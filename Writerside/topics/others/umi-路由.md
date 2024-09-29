```typescript
import { defineConfig } from 'umi';

export default defineConfig({
    routes: [
        { path: '/login', component: 'login', layout: false }, // 不需要layout
        { path: '/', component: 'index' }, // 默认layout
        { path: '/a', component: 'a', layout: false }, // 不需要layout
        {
            path: '/',
            component: '@/layouts/exam', // 需要单独的layout,但不需要默认的layout
            layout: false,
            routes: [
                { path: '/b', component: 'b' },
                { path: '/c', component: 'c' },
                { path: '/d', component: 'd' },
            ],
        },
    ],
    npmClient: 'pnpm',
});
```
