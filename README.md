# Matrix Test for Mtrx library (matrix constructor, matrix properties, matrix math operations)

MatrixTest is a library for testing Mtrx library.

# Installation

```sh
$ npm install mtrx
```

# Required modules

-   const chai = require('chai')
-   const assertArrays = require('chai-arrays')
-   chai.use(assertArrays)
-   const Mtrx = require('mtrx')
-   const expect = chai.expect
-   const assert = require('assert')
-   const dse = assert.deepStrictEqual
-   const se = assert.strictEqual
-   const eq = assert.equal


## Test matrix constructor

```js
const a = new Mtrx();
describe ('Matrix constructor', () => {
    it('create 1x1 random matrix', () => {
        expect(a.length).to.equal(1)
    })
    it('create 2x3 certain matrix', () =>{
        expect(new Mtrx([[1, 2, 3], [4, 5, 6]])).deep.equal([[1, 2, 3], [4, 5, 6]])
    })
    it('check type of 2x3 certain matrix is Array', () => {
        expect(new Mtrx([[0, 7, 10], [1, 8, 11]])).to.be.array()
    })
    it('check size of 2x3 certain matrix is equal to expected', () => {
        expect(new Mtrx([[11, 27, 12], [32, 13, 28]])).to.be.ofSize(2,3)
    })
    it('check 1x3 certain matrix is array', () => {
        expect(new Mtrx([1, 2, 3])).to.be.array()
    })
    it('accept a matrix', () => {
        const a = [
            [11, 12, 13],
            [27, 48, 44]
        ]
        assert.deepEqual(new Mtrx(a), a)
    })
    it('accept a number array', () => {
        const a = [11, 18, 9, 16]
        const m = new Mtrx([
            [11, 0, 0, 0],
            [0, 18, 0, 0],
            [0, 0, 9, 0],
            [0, 0, 0, 16]
        ])
        dse(new Mtrx(a), m)
    })
    it('accept 3 numbers', () => {
        const m = new Mtrx(2, 3, 8)
        const n = new Mtrx([
            [8, 8, 8],
            [8, 8, 8]
        ])
        dse (m, n)
    })
    it('accept 2 numbers and a function', () => {
        const m = new Mtrx(3, 3, (i, j) => i + j)
        const n = new Mtrx([
            [0, 1, 2],
            [1, 2, 3], 
            [2, 3, 4]
        ])
        dse(m, n)
    })
})
```


## Test matrix properties

```js
describe('matrix properties', () => {
    const m = new Mtrx([
        [1, 2, 0, 0],
        [3, 4, 4, 0],
        [5, 6, 3, 0]
    ])
    const n = new Mtrx([
        [1, 2, 0, 0, 1],
        [3, 4, 5, 0, 1],
        [5, 6, 3, 0, 1],
        [5, 6, 3, 0, 1]
    ])
    const diag = new Mtrx([
        [6, 0 , 0,  0],
        [0, 0.6, 0, 0],
        [0, 0, 2, 0],
        [0, 0, 0, 1]
    ])
    it('get 3x4 matrix rows (matrix m)', () => {
        eq(m.rows, 3)
    })
    it('get 4x4 matrix rows (matrix n)', () => {
        eq(n.rows, 4)
    })
    it ('get rank 3x4 matrix m', () => {
        eq(m.rank, 3)
    })
    it ('get rank 4x5 matrix n', () => {
        eq(n.rank, 3)
    })
    it ('get rank 4x4 matrix diag', () => {
        eq(diag.rank, 4)
    })
    it('get 3x3 matrix determinant', () => {
        const d = new Mtrx([
            [1, 2, 0],
            [3, 4, 4],
            [5, 6, 3]
        ])
        eq(d.det, 10)
    })
})
```


## Test math matrix operations

```js
describe('matrix math functions', () => {
    const m = new Mtrx([
        [1, 3, 5],
        [8, 3, 1],
        [7, 3, 8]
    ])
    const n = new Mtrx([
        [2, 4, 8],
        [4, 4, 2],
        [3, 2, 9]
    ])
    it('add two matrix m, n, 3x3', () => {
        const r = Mtrx.add(m, n)
        const res = new Mtrx([
            [3, 7, 13],
            [12, 7, 3],
            [10, 5, 17]
        ])
        dse(r, res)
    })
    it('subtract two matrix m, n, 3x3', () => {
        const r = Mtrx.sub(m, n)
        const res = new Mtrx([
            [-1, -1, -3],
            [4, -1, -1],
            [4, 1, -1]
        ])
        dse(r, res)
    })
    it('multiply two matrix m, n, 3x3', () => {
        const r = Mtrx.mul(m, n)
        const res = new Mtrx([
            [29, 26, 59],
            [31, 46, 79],
            [50, 56, 134]
        ])
        dse(r, res)
    })
    it('multiply matrix m on constant 3', () => {
        const r = Mtrx.mul(m, 3)
        const res = new Mtrx([
            [3, 9, 15],
            [24, 9, 3],
            [21, 9, 24]
        ])
        dse(r, res)
    })
    it('multiply matrix n on constant 0.5', () => {
        const r = Mtrx.mul(n, 0.5)
        const res = new Mtrx([
            [1, 2, 4],
            [2, 2, 1],
            [1.5, 1, 4.5]
        ])
        dse(r, res)
    })
    it('divide matrix m on number 2', () => {
        const r = Mtrx.div(m, 2)
        const res = new Mtrx([
            [0.5, 1.5, 2.5],
            [4, 1.5, 0.5],
            [3.5, 1.5, 4]
        ])
        dse(r, res)
    })
})
```
