I am trying to compile the angular source and create a local project linked to the compiled source, so
that I am able to make small changes to the code to help learn / walk through it.

node -v
// v12.13.1

git clone https://github.com/angular/angular.git

cd angular

git checkout tags/12.0.0-next.0
git switch -c building-angular

Open /packages/common/http/src/request.ts, add the following to line 171
console.log("Test custom angular build - HTTP request")


Per https://github.com/angular/angular/blob/master/CONTRIBUTING.md :

yarn install
node ./scripts/build/build-packages-dist.js
... wait 20 minutes, apologize to computer ...

navigate into /dist/packages-dist/

run npm pack for each folder used in the other angular project

go up one directory (cd..)

ng new test-custom-angular
--yes routing
--css

in package.json, replace the dependencies with the new .tgz files:

"@angular/animations": "file:../angular/dist/packages-dist/animations/angular-animations-12.0.0-next.0.tgz",
"@angular/common": "file:../angular/dist/packages-dist/common/angular-common-12.0.0-next.0.with-local-changes.tgz",
"@angular/compiler": "file:../angular/dist/packages-dist/compiler/angular-compiler-12.0.0-next.0.tgz",
"@angular/core": "file:../angular/dist/packages-dist/core/angular-core-12.0.0-next.0.tgz",
"@angular/forms": "file:../angular/dist/packages-dist/forms/angular-forms-12.0.0-next.0.tgz",
"@angular/platform-browser": "file:../angular/dist/packages-dist/platform-browser/angular-platform-browser-12.0.0-next.0.tgz",
"@angular/platform-browser-dynamic": "file:../angular/dist/packages-dist/platform-browser-dynamic/angular-platform-browser-dynamic-12.0.0-next.0.tgz",
"@angular/router": "file:../angular/dist/packages-dist/router/angular-router-12.0.0-next.0.tgz",

npm install
ng serve

ng serve has thrown a wide variety of errors. currently I am seeing:

Compiling @angular/core : es2015 as esm2015
Error: Error on worker #1: TypeError: Cannot read property 'map' of undefined