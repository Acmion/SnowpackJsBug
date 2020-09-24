# SnowpackProxyJsBug

This repository is a minimal reproduction of a "proxy.js" renaming issue with Snowpack.

## Walkthrough
1. The `src` directory contains files that are named as `filename.ext` and `filename.ext.ts`. In this context `ext` is just some other extension. This convention is often used in, for example, the C# world, with files like `filename.xaml` and `filename.xaml.cs`.
2. `src/a.ext` and `src/b.ext` are empty files.
3. `src/a.ext.ts` contains only a function.
4. `src/b.ext.ts` imports the function from `src/a.ext.ts` with the following code: 
    ```
    import a from "./a.ext";
    ```
 
5. Snowpack generates the files `build/_dist_/a.ext.js` and `build/_dist_/b.ext.js`, as expected.
6. However, `build/_dist_/b.ext.js` contains a reference to a `./a.ext.proxy.js` a file that does not exist.
7. Thus, a runtime error occurs when referencing `src/b.ext.ts` (or it's corresponding generated file).

