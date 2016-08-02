# SwiftSim
Vector similarity utility in Swift.  Currently, only arrays of Double are supported as input.  yIn the next update, this will be changed to be more generic.  The hope is that the numerical methods can operate on any arbitrary numerical input, and the set-basded metrics can operate on any Hashable type.  Future versions may have a more functional object Class called SwiftSwim.

## Basic Usage
```swift
let Similarity = EMSimilarity()
let A = [0.0, 1.5, 3.0, 4.5, 6.0]
let B = [2.0, 4.0, 6.0, 8.0, 10.0]

// compute the cosine similarity of A and B
Similarity.compute(A, B: B)
// 0.984731927834662
```

## Computation Modes
SwiftSim uses a stack to store its modes. To specify a new mode, you simply push a new computation mode to the stack. You can also pop modes off.

```swift
enum EMSimilarityMode {
    case Cosine
    case Tanimoto
    case Ochiai
    case JaccardIndex
    case JaccardDistance
    case Dice
    case Hamming
}
```

```swift
// push a new computation mode to the stack
Similarity.pushSimMode(.Hamming)
// compute the Hamming distance of A and B
Similarity.compute(A, B: B)
// 5.0
// go back to previous mode
Similarity.popSimMode()
Similarity.compute(A, B: B)
// 0.984731927834662
```

## Vector Lengths Mismatch Mode
By default, if A and B have different lengths, it will trigger a bail mode and return -1.0. However, you can specify a different mismatch mode like you do similarity mode.

```siwft
enum EMVectorSizeMismatchMode {
    case Bail
    case Truncate
}

// truncate the smaller vector
Similarity.pushMismatchMode(.Truncate)
```
