# shared-workspace-lockfile-behavior-research

https://pnpm.io/ja/npmrc#shared-workspace-lockfile

Compare the behavior of `shared-workspace-lockfile=false/true` in a monorepo.

## Install Dependencies

1. install `vue@3.0.0` in:
   - `shared-workspace-lockfile=false/packages/package-a`
   - `shared-workspace-lockfile=true/packages/package-a`
2. install `@babel/parser@7.12.17` in:
   - `shared-workspace-lockfile=false/packages/package-b`
   - `shared-workspace-lockfile=true/packages/package-b`

**Why install `@babel/parser@7.12.17`?**

- `vue@3.0.0` depends on `@vue/compiler-core@3.0.0`
- `@vue/compiler-core@3.0.0` depends on [`"@babel/parser": "^7.11.5"`](https://github.com/vuejs/core/blob/v3.0.0/packages/compiler-core/package.json#L35)


## Check difference between lockfiles

```bash
$ sdiff -l shared-workspace-lockfile=false/packages/package-a/pnpm-lock.yaml shared-workspace-lockfile=true/pnpm-lock.yaml
lockfileVersion: '9.0'                                        (
                                                              (
settings:                                                     (
  autoInstallPeers: true                                      (
  excludeLinksFromLockfile: false                             (
                                                              (
importers:                                                    (
                                                              (
  .:                                                          |   .: {}
                                                              > 
                                                              >   packages/package-a:
    dependencies:                                             (
      vue:                                                    (
        specifier: 3.0.0                                      (
        version: 3.0.0                                        (
                                                              (
                                                              >   packages/package-b:
                                                              >     dependencies:
                                                              >       '@babel/parser':
                                                              >         specifier: 7.12.17
                                                              >         version: 7.12.17
                                                              > 
packages:                                                     (
                                                              (
  '@babel/helper-string-parser@7.25.9':                       (
    resolution: {integrity: sha512-4A/SCr/2KLd5jrtOMFzaKjVtAe (
    engines: {node: '>=6.9.0'}                                (
                                                              (
  '@babel/helper-validator-identifier@7.25.9':                (
    resolution: {integrity: sha512-Ed61U6XJc3CVRfkERJWDz4dJwK (
    engines: {node: '>=6.9.0'}                                (
                                                              (
  '@babel/parser@7.26.7':                                     |   '@babel/parser@7.12.17':
    resolution: {integrity: sha512-kEvgGGgEjRUutvdVvZhbn/BxVt |     resolution: {integrity: sha512-r1yKkiUTYMQ8LiEI0UcQx5ETw5
    engines: {node: '>=6.0.0'}                                (
    hasBin: true                                              (
                                                              (
  '@babel/types@7.26.7':                                      (
    resolution: {integrity: sha512-t8kDRGrKXyp6+tjUh7hw2RLycl (
    engines: {node: '>=6.9.0'}                                (
                                                              (
  '@vue/compiler-core@3.0.0':                                 (
    resolution: {integrity: sha512-XqPC7vdv4rFE77S71oCHmT1K4K (
                                                              (
  '@vue/compiler-dom@3.0.0':                                  (
    resolution: {integrity: sha512-ukDEGOP8P7lCPyStuM3F2iD5w2 (
                                                              (
  '@vue/reactivity@3.0.0':                                    (
    resolution: {integrity: sha512-mEGkztGQrAPZRhV7C6PorrpT3+ (
                                                              (
  '@vue/runtime-core@3.0.0':                                  (
    resolution: {integrity: sha512-3ABMLeA0ZbeVNLbGGLXr+pNUwq (
                                                              (
  '@vue/runtime-dom@3.0.0':                                   (
    resolution: {integrity: sha512-f312n5w9gK6mVvkDSj6/Xnot1X (
                                                              (
  '@vue/shared@3.0.0':                                        (
    resolution: {integrity: sha512-4XWL/avABGxU2E2ZF1eZq3Tj7f (
                                                              (
  csstype@2.6.21:                                             (
    resolution: {integrity: sha512-Z1PhmomIfypOpoMjRQB70jfvy/ (
                                                              (
  estree-walker@2.0.2:                                        (
    resolution: {integrity: sha512-Rfkk/Mp/DL7JVje3u18FxFujQl (
                                                              (
  source-map@0.6.1:                                           (
    resolution: {integrity: sha512-UjgapumWlbMhkBgzT7Ykc5YXUT (
    engines: {node: '>=0.10.0'}                               (
                                                              (
  vue@3.0.0:                                                  (
    resolution: {integrity: sha512-ZMrAARZ32sGIaYKr7Fk2GZEBh/ (
                                                              (
snapshots:                                                    (
                                                              (
  '@babel/helper-string-parser@7.25.9': {}                    (
                                                              (
  '@babel/helper-validator-identifier@7.25.9': {}             (
                                                              (
  '@babel/parser@7.26.7':                                     |   '@babel/parser@7.12.17':
    dependencies:                                             (
      '@babel/types': 7.26.7                                  (
                                                              (
  '@babel/types@7.26.7':                                      (
    dependencies:                                             (
      '@babel/helper-string-parser': 7.25.9                   (
      '@babel/helper-validator-identifier': 7.25.9            (
                                                              (
  '@vue/compiler-core@3.0.0':                                 (
    dependencies:                                             (
      '@babel/parser': 7.26.7                                 |       '@babel/parser': 7.12.17
      '@babel/types': 7.26.7                                  (
      '@vue/shared': 3.0.0                                    (
      estree-walker: 2.0.2                                    (
      source-map: 0.6.1                                       (
                                                              (
  '@vue/compiler-dom@3.0.0':                                  (
    dependencies:                                             (
      '@vue/compiler-core': 3.0.0                             (
      '@vue/shared': 3.0.0                                    (
                                                              (
  '@vue/reactivity@3.0.0':                                    (
    dependencies:                                             (
      '@vue/shared': 3.0.0                                    (
                                                              (
  '@vue/runtime-core@3.0.0':                                  (
    dependencies:                                             (
      '@vue/reactivity': 3.0.0                                (
      '@vue/shared': 3.0.0                                    (
                                                              (
  '@vue/runtime-dom@3.0.0':                                   (
    dependencies:                                             (
      '@vue/runtime-core': 3.0.0                              (
      '@vue/shared': 3.0.0                                    (
      csstype: 2.6.21                                         (
                                                              (
  '@vue/shared@3.0.0': {}                                     (
                                                              (
  csstype@2.6.21: {}                                          (
                                                              (
  estree-walker@2.0.2: {}                                     (
                                                              (
  source-map@0.6.1: {}                                        (
                                                              (
  vue@3.0.0:                                                  (
    dependencies:                                             (
      '@vue/compiler-dom': 3.0.0                              (
      '@vue/runtime-dom': 3.0.0                               (
      '@vue/shared': 3.0.0                                    (
```
