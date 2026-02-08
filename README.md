<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# ssyr2

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Perform the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A`.

<section class="installation">

## Installation

```bash
npm install @stdlib/blas-base-ssyr2
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var ssyr2 = require( '@stdlib/blas-base-ssyr2' );
```

#### ssyr2( order, uplo, N, α, x, sx, y, sy, A, LDA )

Performs the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A`, where `α` is a scalar, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 2.0, 1.0, 2.0, 3.0, 2.0, 1.0 ] );
var x = new Float32Array( [ 1.0, 2.0, 3.0 ] );
var y = new Float32Array( [ 1.0, 2.0, 3.0 ] );

ssyr2( 'row-major', 'upper', 3, 1.0, x, 1, y, 1, A, 3 );
// A => <Float32Array>[ 3.0, 6.0, 9.0, 2.0, 9.0, 14.0, 3.0, 2.0, 19.0 ]
```

The function has the following parameters:

-   **order**: storage layout.
-   **uplo**: specifies whether the upper or lower triangular part of the symmetric matrix `A` should be referenced.
-   **N**: number of elements along each dimension of `A`.
-   **α**: scalar constant.
-   **x**: first input [`Float32Array`][mdn-float32array].
-   **sx**: stride length for `x`.
-   **y**: second input [`Float32Array`][mdn-float32array].
-   **sy**: stride length for `y`.
-   **A**: input matrix stored in linear memory as a [`Float32Array`][mdn-float32array].
-   **LDA**: stride of the first dimension of `A` (a.k.a., leading dimension of the matrix `A`).

The stride parameters determine how elements in the input arrays are accessed at runtime. For example, to iterate over every other element of `x`,

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 2.0, 1.0, 2.0, 3.0, 2.0, 1.0 ] );
var x = new Float32Array( [ 1.0, 2.0, 3.0, 4.0, 5.0 ] );
var y = new Float32Array( [ 1.0, 2.0, 3.0 ] );

ssyr2( 'row-major', 'upper', 3, 1.0, x, 2, y, 1, A, 3 );
// A => <Float32Array>[ 3.0, 7.0, 11.0, 2.0, 13.0, 21.0, 3.0, 2.0, 31.0 ]
```

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
var Float32Array = require( '@stdlib/array-float32' );

// Initial arrays...
var x0 = new Float32Array( [ 0.0, 1.0, 1.0, 1.0 ] );
var y0 = new Float32Array( [ 0.0, 1.0, 2.0, 3.0 ] );
var A = new Float32Array( [ 1.0, 2.0, 3.0, 2.0, 1.0, 2.0, 3.0, 2.0, 1.0 ] );

// Create offset views...
var x1 = new Float32Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element
var y1 = new Float32Array( y0.buffer, y0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

ssyr2( 'row-major', 'upper', 3, 1.0, x1, 1, y1, 1, A, 3 );
// A => <Float32Array>[ 3.0, 5.0, 7.0, 2.0, 5.0, 7.0, 3.0, 2.0, 7.0 ]
```

#### ssyr2.ndarray( uplo, N, α, x, sx, ox, y, sy, oy, A, sa1, sa2, oa )

Performs the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A`, using alternative indexing semantics and where `α` is a scalar, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 2.0, 1.0, 2.0, 3.0, 2.0, 1.0 ] );
var x = new Float32Array( [ 1.0, 2.0, 3.0 ] );
var y = new Float32Array( [ 1.0, 2.0, 3.0 ] );

ssyr2.ndarray( 'upper', 3, 1.0, x, 1, 0, y, 1, 0, A, 3, 1, 0 );
// A => <Float32Array>[ 3.0, 6.0, 9.0, 2.0, 9.0, 14.0, 3.0, 2.0, 19.0 ]
```

The function has the following additional parameters:

-   **ox**: starting index for `x`.
-   **oy**: starting index for `y`.
-   **sa1**: stride of the first dimension of `A`.
-   **sa2**: stride of the second dimension of `A`.
-   **oa**: starting index for `A`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameters support indexing semantics based on starting indices. For example,

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 2.0, 3.0, 2.0, 1.0, 2.0, 3.0, 2.0, 1.0 ] );
var x = new Float32Array( [ 1.0, 2.0, 3.0, 4.0, 5.0 ] );
var y = new Float32Array( [ 1.0, 2.0, 3.0 ] );

ssyr2.ndarray( 'upper', 3, 1.0, x, -2, 4, y, 1, 0, A, 3, 1, 0 );
// A => <Float32Array>[ 11.0, 15.0, 19.0, 2.0, 13.0, 13.0, 3.0, 2.0, 7.0 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `ssyr2()` corresponds to the [BLAS][blas] level 2 function [`ssyr2`][blas-ssyr2].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-array-discrete-uniform' );
var ones = require( '@stdlib/array-ones' );
var ssyr2 = require( '@stdlib/blas-base-ssyr2' );

var opts = {
    'dtype': 'float32'
};

var N = 3;

// Create N-by-N symmetric matrices:
var A1 = ones( N*N, opts.dtype );
var A2 = ones( N*N, opts.dtype );

// Create random vectors:
var x = discreteUniform( N, -10.0, 10.0, opts );
var y = discreteUniform( N, -10.0, 10.0, opts );

ssyr2( 'row-major', 'upper', 3, 1.0, x, 1, y, 1, A1, 3 );
console.log( A1 );

ssyr2.ndarray( 'upper', 3, 1.0, x, 1, 0, y, 1, 0, A2, 3, 1, 0 );
console.log( A2 );
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/blas/base/ssyr2.h"
```

#### c_ssyr2( order, uplo, N, alpha, \*X, sx, \*Y, sy, \*A, LDA )

Performs the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A` where `α` is a scalar, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```c
#include "stdlib/blas/base/shared.h"

float A[] = { 1.0f, 2.0f, 3.0f, 2.0f, 1.0f, 2.0f, 3.0f, 2.0f, 1.0f };
const float x[] = { 1.0f, 2.0f, 3.0f };
const float y[] = { 1.0f, 2.0f, 3.0f };

c_ssyr2( CblasColMajor, CblasUpper, 3, 1.0f, x, 1, y, 1, A, 3 );
```

The function accepts the following arguments:

-   **order**: `[in] CBLAS_LAYOUT` storage layout.
-   **uplo**: `[in] CBLAS_UPLO` specifies whether the upper or lower triangular part of the symmetric matrix `A` should be referenced.
-   **N**: `[in] CBLAS_INT` number of elements along each dimension of `A`.
-   **alpha**: `[in] float` scalar constant.
-   **X**: `[in] float*` first input array.
-   **strideX**: `[in] CBLAS_INT` stride length for `X`.
-   **Y**: `[in] float*` second input array.
-   **strideY**: `[in] CBLAS_INT` stride length for `Y`.
-   **A**: `[inout] float*` input matrix.
-   **LDA**: `[in] CBLAS_INT` stride of the first dimension of `A` (a.k.a., leading dimension of the matrix `A`).

```c
void c_ssyr2( const CBLAS_LAYOUT order, const CBLAS_UPLO uplo, const CBLAS_INT N, const float alpha, const float *X, const CBLAS_INT strideX, const float *Y, const CBLAS_INT strideY, float *A, const CBLAS_INT LDA )
```

<!-- lint disable maximum-heading-length -->

#### c_ssyr2_ndarray( uplo, N, alpha, \*X, sx, ox, \*Y, sy, oy, \*A, sa1, sa2, oa )

Performs the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A`, using alternative indexing semantics and where `α` is a scalar, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```c
#include "stdlib/blas/base/shared.h"

float A[] = { 1.0f, 2.0f, 3.0f, 2.0f, 1.0f, 2.0f, 3.0f, 2.0f, 1.0f };
const float x[] = { 1.0f, 2.0f, 3.0f };
const float y[] = { 1.0f, 2.0f, 3.0f };

c_ssyr2_ndarray( CblasUpper, 3, 1.0f, x, 1, 0, y, 1, 0, A, 3, 1, 0 );
```

The function accepts the following arguments:

-   **uplo**: `[in] CBLAS_UPLO` specifies whether the upper or lower triangular part of the symmetric matrix `A` should be referenced.
-   **N**: `[in] CBLAS_INT` number of elements along each dimension of `A`.
-   **alpha**: `[in] float` scalar constant.
-   **X**: `[in] float*` first input array.
-   **sx**: `[in] CBLAS_INT` stride length for `X`.
-   **ox**: `[in] CBLAS_INT` starting index for `X`.
-   **Y**: `[in] float` second input array.
-   **sy**: `[in] CBLAS_INT` stride length for `Y`.
-   **oy**: `[in] CBLAS_INT` starting index for `Y`.
-   **A**: `[inout] float*` input matrix.
-   **sa1**: `[in] CBLAS_INT` stride of the first dimension of `A`.
-   **sa2**: `[in] CBLAS_INT` stride of the second dimension of `A`.
-   **oa**: `[in] CBLAS_INT` starting index for `A`.

```c
void c_ssyr2_ndarray( const CBLAS_UPLO uplo, const CBLAS_INT N, const float alpha, const float *X, const CBLAS_INT strideX, const CBLAS_INT offsetX, const float *Y, CBLAS_INT strideY, const CBLAS_INT offsetY, float *A, const CBLAS_INT strideA1, const CBLAS_INT strideA2, const CBLAS_INT offsetA )
```

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

### Examples

```c
#include "stdlib/blas/base/ssyr2.h"
#include "stdlib/blas/base/shared.h"
#include <stdio.h>

int main( void ) {
    // Define 3x3 symmetric matrices stored in row-major layout:
    float A1[ 3*3 ] = {
        1.0f, 2.0f, 3.0f,
        2.0f, 1.0f, 2.0f,
        3.0f, 2.0f, 1.0f
    };

    float A2[ 3*3 ] = {
        1.0f, 2.0f, 3.0f,
        2.0f, 1.0f, 2.0f,
        3.0f, 2.0f, 1.0f
    };

    // Define `x` and `y` vectors:
    const float x[ 3 ] = { 1.0f, 2.0f, 3.0f };
    const float y[ 3 ] = { 1.0f, 2.0f, 3.0f };

    // Specify the number of elements along each dimension of `A1` and `A2`:
    const int N = 3;

    // Perform the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A`:
    c_ssyr2( CblasColMajor, CblasUpper, N, 1.0f, x, 1, y, 1, A1, N );

    // Print the result:
    for ( int i = 0; i < N*N; i++ ) {
        printf( "A1[ %i ] = %f\n", i, A1[ i ] );
    }

    // Perform the symmetric rank 2 operation `A = α*x*y^T + α*y*x^T + A` using alternative indexing semantics:
    c_ssyr2_ndarray( CblasUpper, N, 1.0f, x, 1, 0, y, 1, 0, A2, N, 1, 0 );

    // Print the result:
    for ( int i = 0; i < N*N; i++ ) {
        printf( "A2[ %i ] = %f\n", i, A2[ i ] );
    }
}
```

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-base-ssyr2.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-base-ssyr2

[test-image]: https://github.com/stdlib-js/blas-base-ssyr2/actions/workflows/test.yml/badge.svg?branch=v0.1.1
[test-url]: https://github.com/stdlib-js/blas-base-ssyr2/actions/workflows/test.yml?query=branch:v0.1.1

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-base-ssyr2/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-base-ssyr2?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-base-ssyr2.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-base-ssyr2/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-base-ssyr2/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-base-ssyr2/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-base-ssyr2/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-base-ssyr2/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-base-ssyr2/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-base-ssyr2/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-base-ssyr2/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-base-ssyr2/main/LICENSE

[blas]: http://www.netlib.org/blas

[blas-ssyr2]: https://netlib.org/lapack/explore-html/dd/de5/group__her2_ga6741f2ac8fe025042fd994ccc6625b45.html

[mdn-float32array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

</section>

<!-- /.links -->
