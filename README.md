# Dicoding Academy JavaScript - Style Guide

## Introduction

> Ada banyak sekali opsi yang bisa diikuti perihal gaya penulisan kode JavaScript. Oleh sebab itu, untuk mengurangi kebingungan, kami standarkan penulisan kode JavaScript yang digunakan dalam lingkup Dicoding Academy.

*Style guide* ini dibuat untuk menstandarkan penulisan kode JavaScript yang berada di dalam platform Dicoding Academy, seperti potongan kode yang kami ajarkan di dalam sebuah kelas. Selain itu, style guide ini bisa menjadi panduan bagi siswa untuk menstandarkan gaya penulisan kode JavaScript dalam berbagai aktivitas, salah satunya ketika pengerjaan proyek submission.



## ESLint Sharable Config

Kami menyediakan ESlint *[sharable config](https://eslint.org/docs/latest/extend/shareable-configs)* yang bisa digunakan untuk menerapkan style guide yang didefinisikan di sini.

### Using Sharable Config in ESLint  9 or Latest

Pasang package ESLint dan `eslint-config-dicodingacademy` dengan menggunakan perintah di bawah ini.

```shell
npm install --save-dev eslint eslint-config-dicodingacademy
```

Buatlah berkas [konfigurasi ESLint](https://eslint.org/docs/latest/use/configure/#extending-configuration-files) (contoh: `eslint.config.mjs`) dan di dalamnya tulis kode di bawah ini.

```javascript
import daStyle from 'eslint-config-dicodingacademy';

export default [
  daStyle,
  // other config style
];

```

Anda bisa mendeteksi kesalahan penulisan JavaScript melalui perintah di bawah ini.

```shell
npx eslint
```

Jika ada kode yang tidak sesuai dengan aturan, ESLint akan menampilkan informasinya pada STDOUT.

```text
/home/dimas/eslint-test/index.js
  1:22  error  Missing semicolon  semi

✖ 1 problem (1 error, 0 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.

```



### Using Sharable Config in ESLint < 9

Pasang package ESLint (versi di bawah 9) dan `eslint-config-dicodingacademy` dengan menggunakan perintah di bawah ini.

```shell
npm install --save-dev eslint@8 eslint-config-dicodingacademy
```

Buatlah berkas [konfigurasi ESLint](https://eslint.org/docs/v8.x/use/configure/) (contoh: `.eslintrc.js`) dan di dalamnya tulis kode di bawah ini.

```javascript
module.exports = {
  extends: ['dicodingacademy'],
  parserOptions: {
    ecmaVersion: 'latest'
  }
  // other config
};

```

Anda bisa mendeteksi kesalahan penulisan JavaScript melalui perintah di bawah ini.

```shell
npx eslint
```

Jika ada kode yang tidak sesuai dengan aturan, ESLint akan menampilkan informasinya pada STDOUT.

```text
/home/dimas/eslint-test/index.js
  1:22  error  Missing semicolon  semi

✖ 1 problem (1 error, 0 warnings)
  1 error and 0 warnings potentially fixable with the `--fix` option.

```



## Meta Rules

### Encoding menggunakan UTF-8

Untuk menampilkan dan mengubah teks dengan benar, teks editor harus mengetahui *text encoding* yang digunakan. Pastikan *text encoding* yang digunakan adalah **UTF-8**. Pada teks editor yang umum (seperti VSCode atau WebStorm), informasi encoding yang digunakan dapat ditemukan di *status bar* yang berada di bawah kode editor.

Informasi tambahan:

- https://www.jetbrains.com/help/idea/encoding.html



### Comments

Gunakan komentar untuk menjelaskan kode yang ditulis, seperti baris kode yang sulit dimengerti, informasi argumen pada sebuah fungsi, dan lain sebagainya. Jangan menambahkan komentar pada kode yang "mudah" untuk dibaca dan dimengerti.

#### Multiline Comment

Gunakan `/** ... */` untuk komentar lebih dari satu baris.

Contoh **SALAH** ⛔.

```javascript
// make() returns a new element
// based on the passed in tag name
function make(tag) {
  
  // ...
    
  return element;
}
```

Contoh **BENAR** ✅.

```javascript
/**
 * make() returns a new element
 * based on the passed in tag name
 */
function make(tag) {
  
  // ...
    
  return element;
}
```



#### Singleline Comment

Gunakan `//` untuk komentar satu baris. Sebisa mungkin komentar ditulis di baris baru.

Contoh **SALAH** ⛔.

```javascript
const interval = 60_000; // 1 hour in millis

/**
 * 1 hour in milis
 */
const interval = 60_000;
```

Contoh **BENAR** ✅.

```javascript
// 1 hour in millis
const interval = 60_000;
```



#### Type Information

Anda dapat (secara opsional) mendokumentasikan kode yang ditulis (termasuk menjelaskan informasi tipe data) menggunakan komentar yang ditulis dengan mengikuti format standar JSDoc. Format yang standar dapat dikenali oleh Code Editor sehingga dapat membantu memudahkan pengembangan.

Contoh **SALAH** ⛔ karena tidak menggunakan standar format apa pun.

```javascript
/**
 * function that sum two of numbers
 * Potentially throwing an TypeError
 * a is number
 * b is number
 */
function sum(a, b) {
  if (typeof a !== 'number' || typeof b !== 'number') {
    throw new TypeError('all given argument should be a number');
  }
  
  return a + b;
}
```

Contoh **BENAR** ✅ dengan mengikuti format JSDoc.

```javascript
/**
 * function that sum two of numbers
 * 
 * @throws {TypeError} will throw if the arguments is not number
 * @params {number} a
 * @params {number} b
 */
function sum(a, b) {
  if (typeof a !== 'number' || typeof b !== 'number') {
    throw new TypeError('all given argument should be a number');
  }
  
  return a + b;
}
```

Informasi tambahan:

- https://jsdoc.app/

  

### Action Items

Tandai sebuah  *placeholder* (hal yang perlu dilakukan) dengan teks `TODO:`. Anda bisa gunakan `//` jika to-do dijelaskan dalam satu baris atau `/** */` jika lebih dari satu baris. Jangan tambahkan karakter lain seperti `@` atau `@@` ketika menulis `TODO:` karena tidak perlu.

Berikut adalah contoh yang **SALAH** ⛔.

```javascript
function sum(a, b) {
    // @TODO: throws an TypeError when both argument is not number
    
    return a + b;
}
```

Berikut adalah contoh yang **BENAR** ✅.

```javascript
function sum(a, b) {
  // TODO: throws an TypeError when both argument is not number
  
  return a + b;
}


/**
 * TODO:
 * Create a function that:
 *  - called average
 *  - receives an array of numbers as argument
 *  - ... etc
 */
```



### Line Break (Line Endings)

Anda harus menggunakan format baris baru yang konsisten pada setiap berkas. Di panduan ini kami fokuskan hanya pada penggunaan **unix** (LF atau \n). Pada teks editor yang umum (seperti VSCode atau WebStorm), informasi *line endings* yang digunakan dapat ditemukan di *status bar* yang berada di bawah kode editor.

Informasi tambahan:

- https://www.jetbrains.com/help/webstorm/configuring-line-endings-and-line-separators.html
- https://www.cs.toronto.edu/~krueger/csc209h/tut/line-endings.html



## Code Styles

### Trailing Whitespace

Terkadang kita tidak sadar menambahkan spasi (*whitespace*) yang tidak perlu di akhir baris kode. Bila whitespace tersebut terbawa ke VCS seperti git, tidak jarang developer menjadi bingung dan frustrasi mencari "perbedaan" dari sebuah baris kode karena sulit untuk terlihat. Maka dari itu, pastikan setiap akhir baris kode bersih dari *whitespace*.

Contoh yang **SALAH** ⛔ karena baris kode (pertama) mengandung *whitespace*.

```javascript
const foo = 0;        
const bar = 5;
```

Contoh yang **BENAR** ✅. Tidak ada *whitespace* di setiap akhir baris kode.

```javascript
const foo = 0;
const bar = 5;
```



### Indentation

Penggunaan indentasi pada kode harus konsisten. Untuk menjaga konsistensi, kami menggunakan **2**  buah **spasi** sebagai indentasi.

Berikut contoh yang **SALAH** ⛔.

```javascript
function adder(by) {
    return (value) => {
        return by + value;
  }
}
```

Berikut contoh yang **BENAR** ✅.

```javascript
function adder(by) {
  return (value) => {
    return by + value;
  }
}
```



### Naming

Secara umum penamaan variabel atau fungsi harus menggunakan format `camelCase`.

Berikut contoh yang **SALAH** ⛔.

```javascript
const my_favorite_color = '#112C85';

function do_something() {
  // ...
}

const { from_json } = JSON.parse('{}');
```

Berikut contoh yang **BENAR** ✅.

```javascript
const myFavoriteColor = '#112C85';

function doSomething() {
  // ...
}

const { from_json: fromJson } = JSON.parse('{}');
```



### Arrow Function Parentheses

Agar menjaga konsistensi penulisan, selalu gunakan tanda kurung (parentheses) setiap kali membuat arrow function baik tanpa argumen, 1 argumen, atau lebih.

Berikut contoh yang **SALAH** ⛔.

```javascript
document.addEventListener('click', event => {
  // ...
});

store.subscribe(() => {
  // ...
})

server.handler((request, response) => {
  // ...
});
```

Berikut contoh yang **BENAR** ✅.

```javascript
document.addEventListener('click', (event) => {
  // ...
});

store.subscribe(() => {
  // ...
})

server.handler((request, response) => {
  // ...
});
```



### Formatting

#### Comma

Selalu tambahkan spasi di antara nilai yang dipisahkan oleh tanda koma.

Berikut contoh yang **SALAH** ⛔.

```javascript
function sum(a,b,c) {
  // ...
}

const numbers = [1,2,3,4];
const person = { name: 'Fulan',age: 30 };
```

Berikut contoh yang **BENAR** ✅.

```javascript
function sum(a, b, c) {
  // ...
}

const numbers = [1, 2, 3, 4];
const person = { name: 'Fulan', age: 30 };
```



#### Object Literals

Selalu tambahkan spasi di antara tanda `{ }` dan nama properti yang didefinsikan dalam satu baris.

Berikut contoh yang **SALAH** ⛔.

```javascript
const person = {name: 'Fulan', age: 30};
const {name, age} = person;

function printPerson({name, age}) {
  // ...
}
```

Berikut contoh yang **BENAR** ✅.

```javascript
const person = { name: 'Fulan', age: 30 };
const { name, age } = person;


function printPerson({ name, age }) {
  // ...
}
```



#### Array Literals

Jangan tambahkan spasi di antara tanda `[ ]` dan elemen di dalam array.

Berikut contoh yang **SALAH** ⛔.

```javascript
const numbers = [ 1, 2, 3 ];
const [ first, second ] = numbers;
```

Berikut contoh yang **BENAR** ✅.

```javascript
const numbers = [1, 2, 3];
const [first, second] = numbers;
```



#### Parentheses

Jangan tambahkan spasi di antara tanda `( )` dan expression yang ada di dalamnya.

Berikut contoh yang **SALAH** ⛔.

```javascript
function sum( a, b ) {
  // ...
}

const value = 1 + ( 2 * 1 );

if ( value === 1 ) {
  // ...
}
```

Berikut contoh yang **BENAR** ✅.

```javascript
function sum(a, b) {
  // ...
}

const value = 1 + (2 * 1);

if (value === 1) {
  // ...
}
```



#### Control Statement

Beri 1 spasi sebelum menggunakan tanda `()` pada *control statement* (contohnya `if`, `while`, `for`, dan lainnya). Namun, jangan berikan 1 spasi antara daftar argumen dan nama fungsi ketika mendeklarasikan regular function ataupun ketika memanggil sebuah fungsi.

Berikut contoh yang **SALAH** ⛔.

```javascript
function fight () {
  console.log('Swooosh!');
}

if(isJedi) {
  fight ();
}
```

Berikut contoh yang **BENAR** ✅.

```javascript
function figth() {
  console.log('Swooosh!');
}

if (isJedi) {
  fight();
}
```



## Language Rules

### Variable Declaration

#### Prefer using `const`

Gunakan `const` ketika membuat sebuah variabel yang tidak ditetapkan ulang nilainya.

Berikut contoh yang **SALAH** ⛔.

```javascript
let a = 1;
var b = 2;
```

Berikut contoh yang **BENAR** ✅.

```javascript
const a = 1;
const b = 2;
```



#### Using `let`, avoid `var`

Jika sebuah variabel perlu ditetapkan ulang nilainya, gunakan `let` alih-alih `var`.

Berikut contoh yang **SALAH** ⛔.

```javascript
var count = 1;

if (true) {
  count += 1;
}
```

Berikut contoh yang **BENAR** ✅.

```javascript
let count = 1;

if (true) {
  count += 1;
}
```

Informasi tambahan:

- https://dev.to/mindninjax/stop-using-var-for-declaring-variables-2p3a

### Semicolon

Di balik layar, JavaScript akan menambahkan **titik koma**--*sesuai aturan yang berlaku*--sebagai tanda berakhirnya statement pada baris kode yang tidak diberikan semicolon. Aturan ini disebut sebagai *[Automatic Semicolon Insertion (ASI)](https://tc39.es/ecma262/#sec-automatic-semicolon-insertion)*. ASI mengandung beberapa perilaku yang esentrik dan membuat kode yang kita tulis rusak jika ia salah menginterpretasikan baris kode tersebut. ASI juga akan semakin rumit dipahami seiring bertambahnya fitur atau sintaks pada bahasa pemrograman JavaScript. Dengan menuliskan titik koma (semicolon) secara eksplisit tentu akan membantu untuk mencegah masalah-masalah yang ditimbulkan karena ASI.

Berikut contoh yang **SALAH** ⛔ karena kode akan membangkitkan error.

```javascript
// will raise exception
const luke = {}
const leia = {}
[luke, leia].forEach((jedi) => jedi.father = 'vader')


// will raise exception
const reaction = "No! That’s impossible!"
(async function meanwhileOnTheFalcon() {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}())


// return undefined because ASI insert semicolon after `return`
function foo() {
  return
    'search your feelings, you know it to be foo'
}
```

Berikut contoh yang **BENAR** ✅.

``` javascript
// good
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) =>  jedi.father = 'vader');

// good
const reaction = 'No! That’s impossible!';
(async function meanwhileOnTheFalcon() {
  // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
  // ...
}());

// good
function foo() {
  return 'search your feelings, you know it to be foo';
}
```

Informasi tambahan:

-  https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214

### Strings

Agar konsisten, selalu gunakan **kutip satu** `' '` untuk membuat nilai string.

Berikut contoh yang **SALAH** ⛔.

```javascript
// Bad
const name = "Fulan";

// Bad
const address = `Bandung`;
```

Berikut contoh yang **BENAR** ✅.

```javascript
// Good
const name = 'Fulan';
const address = 'Bandung';
```

Anda boleh gunakan tanda lain untuk kasus-kasus tertentu, seperti:

Gunakan `" "` jika nilai string mengandung karakter '.

```javascript
// Bad
const movie = 'Howl\'s Moving Castle';

// Good
const movie = "Howl's Moving Castle";
```

Gunakan ` `` ` jika membutuhkan JavaScript expression dalam membangun nilai string.

```javascript
// Bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// Good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```



### Arrow Function for Function Expressions

Function di JavaScript merupakan first-class citizen. Sama seperti nilai primitif, function dapat  berupa expression dan disimpan menjadi nilai variabel, argumen fungsi, atau nilai yang dikembalikan oleh fungsi. Ketika Anda membuat function expression (contohnya menetapkan fungsi callback), gunakanlah arrow function.

Berikut contoh yang **SALAH** ⛔.

```javascript
[1, 2, 3].map(function(x) {
  return x * 2;
});
```

Berikut contoh yang **BENAR** ✅.

```javascript
[1, 2, 3].map((x) => x * 2);
```
