# Keras MOD
A modified fork of Keras, with base version 1.0.4

## Purpose
The modifications are mainly about transplanting a CTC (Connection-nist Temporal Classification) implementation [see https://github.com/daweileng/Precise-CTC] into Keras. This feature has been missing by Keras for quite a long time.

## Why not pull request for Keras master branch?
Question may be asked why not make a pull request for fchollet's Keras repository. The reason is that CTC cost is rather different from the existing objective functions in Keras, it requires different masking mechanism and not directly reflects accuracy. To avoid mass modification of Keras' current masking mechanism, I override Keras' 'sample_weights' variable for 'seq_mask' of CTC and Keras' 'masks' variable for 'sm_mask' of CTC. This should not cause problem for other network architecture or objective functions, but I lack resources to give it a thorough test.

## Functions
[1] Till now, the following train/test functions works well with CTC cost:
  * train_on_batch()
  * test_on_batch()
  * predict_on_batch()
  
The modification of 'fit()' function is in progress, but no definte schedule.

[2] For now, only 'loss' metric works with CTC cost. For accuracy evaluation, you need to do the decoding and calculate the CER outside Keras.

[3] 'Flatten' class is modified to work with FCN (Fully Convoluational Network)
