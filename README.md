Personal blog using Hugo:
https://rayandas.in
TIL:
https://til.rayandas.in

Clone this repo using:
```bash
git clone --recursive git@github.com:rayandas/hugo.git
```
Update the submodules using:
```bash
git submodule update --remote
``` 
Clone rayandas/etch:
```
git clone git@github.com:rayandas/etch.git themes/etch
```

Clone rayandas/etch branch's specific branch using:
```
git submodule add --branch 18-Mar-2025-Update git@github.com:rayandas/etch.git template/etch
```

Hugo version
```
hugo v0.145.0+extended+withdeploy darwin/arm64 BuildDate=2025-02-26T15:41:25Z VendorInfo=brew
```

When using hugo server to run the local server, all the html files inside `public/` will use the `localhost:1313` URL. Before the commit, change all localhost to rayandas.in and run `hugo`, it will create the xml files. then push it to github. 
