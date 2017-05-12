## Neural Nets

### Convolution

* The difference between 'SAME' and 'VALID'.
    Note that 'SAME' doesn't mean the shape of the feature map 'keep the same',
    this is true only when the stride is [1, 1, 1, 1]. 
    VALID only drops the right-most columns(or bottom-most rows).
    SAME tries to pad evenly left and right and then do the convolution.
